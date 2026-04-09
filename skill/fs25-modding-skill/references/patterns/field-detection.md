# Field & Player Position Detection

**How to reliably detect which field the player is standing in**

> ✅ **VALIDATED** — Production-proven in FS25_SoilFertilizer v1.5+ and FS25_NPCFavor v2.6+

---

## Related API Documentation

| Class | API Reference | Description |
|-------|---------------|-------------|
| FieldManager | [FieldManager.md](https://github.com/umbraprior/FS25-Community-LUADOC/blob/main/docs/script/Field/FieldManager.md) | `getFieldAtWorldPosition()` |
| FarmlandManager | [FarmlandManager.md](https://github.com/umbraprior/FS25-Community-LUADOC/blob/main/docs/script/Farmland/FarmlandManager.md) | `getFarmlandIdAtWorldPosition()` |
| Player | [Player.md](https://github.com/umbraprior/FS25-Community-LUADOC/blob/main/docs/script/Player/Player.md) | `getIsInVehicle()`, `getCurrentVehicle()` |

---

## Key Concept: Field vs Farmland

These are **not the same thing**:

| Concept | Manager | Description |
|---------|---------|-------------|
| **Field** | `g_fieldManager` | A specific crop polygon with a unique `fieldId` |
| **Farmland** | `g_farmlandManager` | A purchasable land parcel — one farmland can contain multiple fields |

Always prefer field detection. Farmland detection is a fallback only — it may return the wrong field if a farmland contains multiple fields.

---

## Pattern 1: Player Position Detection (4-Tier Fallback)

Adopted from FS25_NPCFavor (proven production pattern). Wrap ALL `getWorldTranslation()` calls in `pcall()`.

```lua
local function getPlayerWorldPosition()
    local x, y, z = nil, nil, nil

    -- Tier 0: g_localPlayer (most reliable)
    if g_localPlayer ~= nil then
        local ok, px, py, pz
        -- Check if player is in a vehicle
        if g_localPlayer.getIsInVehicle and g_localPlayer:getIsInVehicle() then
            local vehicle = g_localPlayer:getCurrentVehicle()
            if vehicle and vehicle.rootNode then
                ok, px, py, pz = pcall(getWorldTranslation, vehicle.rootNode)
                if ok and px then x, y, z = px, py, pz end
            end
        end
        -- Try player's own position
        if x == nil then
            if g_localPlayer.getPosition then
                ok, px, py, pz = pcall(function()
                    return g_localPlayer:getPosition()
                end)
                if ok and px then x, y, z = px, py, pz end
            end
            if x == nil and g_localPlayer.rootNode then
                ok, px, py, pz = pcall(getWorldTranslation, g_localPlayer.rootNode)
                if ok and px then x, y, z = px, py, pz end
            end
        end
    end

    -- Tier 1: g_currentMission.player
    if x == nil and g_currentMission and g_currentMission.player then
        local player = g_currentMission.player
        if player.rootNode then
            local ok, px, py, pz = pcall(getWorldTranslation, player.rootNode)
            if ok and px then x, y, z = px, py, pz end
        end
        -- Multiplayer: check baseInformation
        if x == nil and player.baseInformation and player.baseInformation.position then
            local pos = player.baseInformation.position
            x, y, z = pos.x, pos.y, pos.z
        end
    end

    -- Tier 2: controlled vehicle
    if x == nil and g_currentMission and g_currentMission.controlledVehicle then
        local vehicle = g_currentMission.controlledVehicle
        if vehicle.rootNode then
            local ok, px, py, pz = pcall(getWorldTranslation, vehicle.rootNode)
            if ok and px then x, y, z = px, py, pz end
        end
    end

    -- Tier 3: camera (last resort)
    if x == nil and g_currentMission and g_currentMission.camera then
        local camera = g_currentMission.camera
        if camera.cameraNode then
            local ok, px, py, pz = pcall(getWorldTranslation, camera.cameraNode)
            if ok and px then x, y, z = px, py, pz end
        end
    end

    return x, y, z
end
```

---

## Pattern 2: Field Detection (3-Tier Fallback)

```lua
local function getCurrentFieldId()
    local x, _, z = getPlayerWorldPosition()
    if x == nil then return nil end

    -- Tier 1: Direct field lookup (most accurate)
    if g_fieldManager and g_fieldManager.getFieldAtWorldPosition then
        local field = g_fieldManager:getFieldAtWorldPosition(x, z)
        if field and field.fieldId then
            return field.fieldId
        end
    end

    -- Tier 2: Via farmland (good fallback — may be wrong if multiple fields per farmland)
    if g_farmlandManager then
        local farmlandId = g_farmlandManager:getFarmlandIdAtWorldPosition(x, z)
        if farmlandId and farmlandId > 0 then
            -- Find a field belonging to this farmland
            if g_fieldManager and g_fieldManager.fields then
                for _, field in pairs(g_fieldManager.fields) do
                    if field.farmland and field.farmland.id == farmlandId then
                        return field.fieldId
                    end
                end
            end
        end
    end

    -- Tier 3: Manual iteration (last resort)
    if g_fieldManager and g_fieldManager.fields then
        for _, field in pairs(g_fieldManager.fields) do
            if field.maxFieldX and field.minFieldX then
                if x >= field.minFieldX and x <= field.maxFieldX and
                   z >= field.minFieldZ and z <= field.maxFieldZ then
                    return field.fieldId
                end
            end
        end
    end

    return nil
end
```

---

## Important: Timing — g_fieldManager.fields May Be Empty

`g_fieldManager.fields` is **empty during mod initialization**. Don't call field detection code in your `loadMap()` or constructor. Use it only from:
- Per-frame `update()` callbacks
- User-triggered actions (button press, HUD refresh)
- Delayed callbacks (after `loadMission00Finished`)

If you need field data early, implement a delayed retry with exponential backoff:

```lua
function MyMod:tryGetFieldId(attempt)
    attempt = attempt or 1
    local fieldId = getCurrentFieldId()
    if fieldId then
        self:onFieldDetected(fieldId)
    elseif attempt < 5 then
        -- Retry with backoff: 1s, 2s, 4s, 8s
        local delay = math.pow(2, attempt - 1) * 1000
        g_currentMission:addDelayedCallback(
            function() self:tryGetFieldId(attempt + 1) end,
            delay
        )
    end
end
```

---

## Complete Usage Example

```lua
-- HUD that shows soil info for the field the player stands in
function SoilHUD:update(dt)
    if not self.isVisible then return end

    -- Throttle: only update every 2 seconds
    self.updateTimer = (self.updateTimer or 0) + dt
    if self.updateTimer < 2000 then return end
    self.updateTimer = 0

    local fieldId = getCurrentFieldId()
    if fieldId then
        local soilData = g_SoilFertilityManager:getFieldData(fieldId)
        self:updateDisplay(soilData)
    else
        self:showNoFieldMessage()
    end
end
```

---

## Common Pitfalls

- ❌ Don't skip `pcall()` around `getWorldTranslation()` — node may be invalid; no pcall = crash
- ❌ Don't use only Tier 1 (`g_localPlayer`) — it's nil in multiplayer spectator mode
- ❌ Don't call field detection at startup — `g_fieldManager.fields` is empty then
- ❌ Don't cache `fieldId` across save/loads — field IDs can change when a new map loads

### Related
- `patterns/extensions.md` — Hook patterns for update callbacks
- `pitfalls/what-doesnt-work.md` — os.time(), goto, hook accumulation
- LUADOC: `docs/script/Field/FieldManager.md`
- LUADOC: `docs/script/Farmland/FarmlandManager.md`
