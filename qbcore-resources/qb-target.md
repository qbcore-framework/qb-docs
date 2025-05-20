---
description: Always watching you...
---

# 👁️ qb-target

## Introduction

qb-target is a targeting solution that allows interaction with any predefined entity, model, entity type or polyzone. While activated you can easily and safely replace markers and distance checking, instead of relying on intuitive design to improve player experiences and optimize interaction.

### Features

* Maintains compatibility with bt-target while providing improved utility and performance
* Optimized and improved raycasting function allows interaction with a wider range of entities
* Add generic options to apply for all players, peds, vehicles, or objects
* Trigger an event, function or command after clicking an option, with the ability to pass any data through
* Define distance on a per-option or overall basis when triggering a target option
* Ability to redefine or remove options and add new options without replacing old ones
* Update the option list when moving towards or away from a target with variable distances on their options
* Support for entity bones, with built-in tables for opening vehicle doors
* Support checking for job, gang, citizenid, items, or specific entities
* Utilise the `canInteract` function for advanced checks to show or hide an option based on any trigger
* Ped spawner to spawn peds and assign target options to them all in one place

***

## AddCircleZone

Adds a circular zone that players can interact with

* **name**: `string`
* **center**: `vector3`
* **radius**: `float`
* **options**: `table`
  * **name**: `string`
  * **debugPoly**: `boolean`&#x20;
  * **useZ**: `boolean` (optional)
* **targetoptions**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
    * **drawDistance**: `number` (optional)
    * **drawColor**: `table` (optional)
    * **successDrawColor**: `table` (optional)
  * **distance**: `float`&#x20;

```lua
exports['qb-target']:AddCircleZone("police_armory", vector3(452.6, -980.0, 30.6), 1.5, {
  name = "police_armory",
  debugPoly = false,
  useZ = true
}, {
  options = {
    {
      num = 1,
      type = "client",
      event = "police:openArmory",
      icon = "fas fa-archive",
      label = "Open Armory",
      targeticon = "fas fa-gun",
      item = "police_badge",
      action = function(entity)
        if IsPedAPlayer(entity) then return false end
        TriggerEvent("police:openArmoryMenu", entity)
      end,
      canInteract = function(entity, distance, data)
        return not IsPedAPlayer(entity)
      end,
      job = { ["police"] = 0, ["sheriff"] = 1 },
      gang = { ["thelostmc"] = 2 },
      citizenid = { ["JFD98238"] = true, ["HJS29340"] = true },
      drawDistance = 10.0,
      drawColor = {255, 255, 255, 255},
      successDrawColor = {0, 255, 0, 255}
    }
  },
  distance = 2.5
})

```

***

## AddBoxZone

Adds a rectangular zone that players can interact with

* **name**: `string`
* **center**: `vector3`
* **length**: `float`
* **width**: `float`
* **options**: `table`
  * **name**: `string`
  * **heading**: `float`
  * **debugPoly**: `boolean`
  * **minZ**: `float`
  * **maxZ**: `float`
* **targetoptions**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
    * **drawDistance**: `number` (optional)
    * **drawColor**: `table` (optional)
    * **successDrawColor**: `table` (optional)
  * **distance**: `float`

```lua
exports['qb-target']:AddBoxZone("bank_counter", vector3(150.1, -1040.5, 29.3), 2.5, 1.2, {
  name = "bank_counter",
  heading = 160.0,
  debugPoly = false,
  minZ = 28.5,
  maxZ = 30.5
}, {
  options = {
    {
      num = 1,
      type = "client",
      event = "bank:openAccountMenu",
      icon = "fas fa-university",
      label = "Access Bank",
      targeticon = "fas fa-building",
      item = "bank_card",
      action = function(entity)
        TriggerEvent("bank:showUI", entity)
      end,
      canInteract = function(entity, distance, data)
        return true
      end,
      job = { ["banker"] = 0 },
      gang = { ["families"] = 1 },
      citizenid = { ["XYZ123"] = true },
      drawDistance = 10.0,
      drawColor = {0, 123, 255, 200},
      successDrawColor = {0, 255, 0, 255}
    }
  },
  distance = 3.0
})
```

***

## AddPolyZone

Adds a custom-shaped polygon zone that players can interact with

* **name**: `string`
* **points**: `table`
  * A list of `vector2` points defining the polygon (minimum of 3, must be in drawing order).
* **options**: `table`
  * **name**: `string`
  * **debugPoly**: `boolean`
  * **minZ**: `float`
  * **maxZ**: `float`
* **targetoptions**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
    * **drawDistance**: `number` (optional)
    * **drawColor**: `table` (optional)
    * **successDrawColor**: `table` (optional)
  * **distance**: `float`&#x20;

```lua
local points = {
  vector2(435.1, -981.0),
  vector2(437.3, -983.5),
  vector2(439.0, -980.2),
  vector2(436.6, -978.7)
}

exports['qb-target']:AddPolyZone("police_parking", points, {
  name = "police_parking",
  debugPoly = true,
  minZ = 29.0,
  maxZ = 31.5
}, {
  options = {
    {
      num = 1,
      type = "client",
      event = "police:garageMenu",
      icon = "fas fa-warehouse",
      label = "Open Garage",
      targeticon = "fas fa-car",
      item = "garage_key",
      action = function(entity)
        TriggerEvent("police:garageUI", entity)
      end,
      canInteract = function(entity, distance, data)
        return true
      end,
      job = { ["police"] = 0 },
      gang = { ["lostmc"] = 1 },
      citizenid = { ["POL123"] = true },
      drawDistance = 8.0,
      drawColor = {0, 100, 255, 255},
      successDrawColor = {0, 255, 0, 255}
    }
  },
  distance = 2.5
})
```

***

## AddComboZone

Adds a composite zone made up of two or more PolyZones (CircleZone, BoxZone, or PolyZone), treated as a single interactive area

* **zones**: `table`
  * A list of zone objects (must be at least 2), e.g. instances created using `BoxZone:Create(...)`.
* **options**: `table`
  * **name**: `string`
  * **debugPoly**: `boolean`
* **targetoptions**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
    * **drawDistance**: `number` (optional)
    * **drawColor**: `table` (optional)
    * **successDrawColor**: `table` (optional)
  * **distance**: `float`&#x20;

```lua
local zone1 = BoxZone:Create(vector3(500.0, 500.0, 100.0), 3.0, 5.0, {
  name = "zone1",
  heading = 0,
  debugPoly = false,
  minZ = 99.0,
  maxZ = 101.0
})

local zone2 = BoxZone:Create(vector3(505.0, 500.0, 100.0), 3.0, 5.0, {
  name = "zone2",
  heading = 0,
  debugPoly = false,
  minZ = 99.0,
  maxZ = 101.0
})

exports['qb-target']:AddComboZone({ zone1, zone2 }, {
  name = "dual_box_zone",
  debugPoly = true
}, {
  options = {
    {
      num = 1,
      type = "client",
      event = "combo:triggerEvent",
      icon = "fas fa-link",
      label = "Combo Action",
      targeticon = "fas fa-crosshairs",
      item = "multikey",
      action = function(entity)
        TriggerEvent("combo:doSomething", entity)
      end,
      canInteract = function(entity, distance, data)
        return true
      end,
      job = { ["mechanic"] = 0 },
      gang = { ["vagos"] = 1 },
      citizenid = { ["COMBO001"] = true },
      drawDistance = 12.0,
      drawColor = {100, 100, 255, 255},
      successDrawColor = {50, 255, 50, 255}
    }
  },
  distance = 2.0
})

```

***

## AddTargetBone

Adds targetable interaction options to specific bones of vehicles

* **bones**: `string` or `table`
  * A single bone name or a list of bone names (e.g. `"bonnet"` or `{ "bonnet", "boot" }`).
* **parameters**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
  * **distance**: `float`&#x20;

```lua
local bones = { "bonnet", "boot" }

exports['qb-target']:AddTargetBone(bones, {
  options = {
    {
      num = 1,
      type = "client",
      event = "vehicle:inspectEngine",
      icon = "fas fa-tools",
      label = "Inspect Engine",
      targeticon = "fas fa-car",
      item = "wrench",
      action = function(entity)
        TriggerEvent("vehicle:diagnostics", entity)
      end,
      canInteract = function(entity, distance, data)
        return IsEntityAVehicle(entity)
      end,
      job = { ["mechanic"] = 0 },
      gang = { ["thelostmc"] = 1 },
      citizenid = { ["WRENCH123"] = true }
    }
  },
  distance = 2.0
})

```

### RemoveTargetBone

Removes targeting options from one or more bones on all applicable entities registered via `AddTargetBone`

* **bones**: `string` or `table`&#x20;

```lua
exports['qb-target']:RemoveTargetBone({ "bonnet", "boot" })
```

***

## AddTargetEntity

Adds interaction options to a specific entity (such as a ped, vehicle, or object)

* **entity**: `number` or `table`
  * The entity instance or a list of entity instances (from `CreatePed`, `CreateVehicle`, etc).
* **parameters**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
  * **distance**: `float`&#x20;

```lua
CreateThread(function()
  local model = `a_m_m_business_01`
  RequestModel(model)
  while not HasModelLoaded(model) do Wait(0) end
  local ped = CreatePed(0, model, 300.0, -500.0, 43.0, 0.0, true, false)

  exports['qb-target']:AddTargetEntity(ped, {
    options = {
      {
        num = 1,
        type = "client",
        event = "npc:openDialog",
        icon = "fas fa-comments",
        label = "Talk to NPC",
        targeticon = "fas fa-user",
        item = "notepad",
        action = function(entity)
          TriggerEvent("npc:startConversation", entity)
        end,
        canInteract = function(entity, distance, data)
          return not IsPedAPlayer(entity)
        end,
        job = { ["journalist"] = 0 },
        gang = { ["ballas"] = 0 },
        citizenid = { ["NPC001"] = true }
      }
    },
    distance = 2.0
  })
end)

```

### RemoveTargetEntity

Removes specific target options from an entity by label(s).

* **entity**: `number` or `table`
* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveTargetEntity(ped, "Talk to NPC")
```

***

## AddEntityZone

Adds a target zone that is dynamically attached to a specific entity. Useful for treating an entity like a movable zone (e.g. attaching interaction to a ped or vehicle)

* **name**: `string`
* **entity**: `number`
  * The target entity's ID (such as a ped or vehicle created via `CreatePed` or `CreateVehicle`).
* **options**: `table`
  * **name**: `string`
  * **debugPoly**: `boolean`
* **targetoptions**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
    * **drawDistance**: `number` (optional)
    * **drawColor**: `table` (optional)
    * **successDrawColor**: `table` (optional)
  * **distance**: `float`&#x20;

```lua
CreateThread(function()
  local model = `s_m_y_cop_01`
  RequestModel(model)
  while not HasModelLoaded(model) do Wait(0) end
  local ped = CreatePed(0, model, 425.1, -979.5, 30.7, 90.0, true, false)

  exports['qb-target']:AddEntityZone("cop_ped", ped, {
    name = "cop_ped",
    debugPoly = false
  }, {
    options = {
      {
        num = 1,
        type = "client",
        event = "police:talkToCop",
        icon = "fas fa-user-shield",
        label = "Talk to Officer",
        targeticon = "fas fa-comment-alt",
        item = "badge",
        action = function(entity)
          TriggerEvent("police:startDialog", entity)
        end,
        canInteract = function(entity, distance, data)
          return not IsPedAPlayer(entity)
        end,
        job = { ["police"] = 0 },
        gang = { ["thelostmc"] = 1 },
        citizenid = { ["COP001"] = true },
        drawDistance = 6.0,
        drawColor = {0, 150, 255, 255},
        successDrawColor = {0, 255, 0, 255}
      }
    },
    distance = 2.0
  })
end)

```

### RemoveEntityZone

Removes a previously registered entity-based zone

* **name**: `string`

```lua
exports['qb-target']:RemoveEntityZone("cop_ped")
```

***

## AddTargetModel

Adds interaction options to one or more models, allowing players to interact with all entities of those models (e.g. specific ped, vehicle, or prop types)

* **models**: `string` or `table`
  * A model name or a list of model names (e.g. `"prop_atm_01"` or `{ "prop_atm_01", "prop_atm_02" }`).
* **parameters**: `table`
  * **options**: `table`
    * **num**: `number` (optional)
    * **type**: `string`
    * **event**: `string`
    * **icon**: `string`
    * **label**: `string`
    * **targeticon**: `string` (optional)
    * **item**: `string` (optional)
    * **action**: `function` (optional)
    * **canInteract**: `function` (optional)
    * **job**: `string` or `table` (optional)
    * **gang**: `string` or `table` (optional)
    * **citizenid**: `string` or `table` (optional)
  * **distance**: `float`&#x20;

```lua
local models = {
  "prop_atm_01",
  "prop_atm_02",
  "prop_fleeca_atm"
}

exports['qb-target']:AddTargetModel(models, {
  options = {
    {
      num = 1,
      type = "client",
      event = "bank:accessATM",
      icon = "fas fa-credit-card",
      label = "Use ATM",
      targeticon = "fas fa-dollar-sign",
      item = "bank_card",
      action = function(entity)
        TriggerEvent("bank:openATM", entity)
      end,
      canInteract = function(entity, distance, data)
        return true
      end,
      job = { ["citizen"] = 0 },
      gang = { ["none"] = 0 },
      citizenid = { ["ATMUSER001"] = true }
    }
  },
  distance = 1.5
})

```

### RemoveTargetModel

Removes interaction options from one or more models.

* **models**: `string` or `table`
* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveTargetModel({ "prop_atm_01", "prop_fleeca_atm" }, "Use ATM")
```

***

## AddGlobalPed

Adds interaction options that apply to all peds in the world. Useful for universal interactions like restraining or identifying NPCs

**parameters**: `table`

* **options**: `table`
  * **num**: `number` (optional)
  * **type**: `string`
  * **event**: `string`
  * **icon**: `string`
  * **label**: `string`
  * **targeticon**: `string` (optional)
  * **item**: `string` (optional)
  * **action**: `function` (optional)
  * **canInteract**: `function` (optional)
  * **job**: `string` or `table` (optional)
  * **gang**: `string` or `table` (optional)
  * **citizenid**: `string` or `table` (optional)
* **distance**: `float`&#x20;

```lua
exports['qb-target']:AddGlobalPed({
  options = {
    {
      num = 1,
      type = "client",
      event = "police:friskPed",
      icon = "fas fa-search",
      label = "Frisk Ped",
      targeticon = "fas fa-user-check",
      item = "handcuffs",
      action = function(entity)
        if IsPedAPlayer(entity) then return false end
        TriggerEvent("police:performFrisk", entity)
      end,
      canInteract = function(entity, distance, data)
        return not IsPedAPlayer(entity)
      end,
      job = { ["police"] = 0 },
      gang = { ["ballas"] = 1 },
      citizenid = { ["PEDGLOBAL01"] = true }
    }
  },
  distance = 2.5
})

```

### RemoveGlobalPed

Removes global interaction options from all peds.

* **identifier**: `string`

```lua
exports['qb-target']:RemoveGlobalPed("Frisk Ped")
```

***

## AddGlobalVehicle

Adds interaction options to all vehicles globally.

* **parameters**: `table`

```lua
exports['qb-target']:AddGlobalVehicle({
  options = {
    {
      num = 1,
      type = "client",
      event = "vehicle:repair",
      icon = "fas fa-wrench",
      label = "Repair Vehicle",
      action = function(entity)
        TriggerEvent("mechanic:repairVehicle", entity)
      end,
      canInteract = function(entity)
        return IsEntityAVehicle(entity)
      end,
      job = { ["mechanic"] = 0 },
      gang = { ["thelostmc"] = 1 }
    }
  },
  distance = 3.0
})
```

### RemoveGlobalVehicle

Removes global options from all vehicles.

* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveGlobalVehicle("Repair Vehicle")
```

***

## AddGlobalObject

Adds interaction options to all static world objects globally.

* **parameters**: `table`

```lua
exports['qb-target']:AddGlobalObject({
  options = {
    {
      num = 1,
      type = "client",
      event = "object:inspect",
      icon = "fas fa-search",
      label = "Inspect Object",
      action = function(entity)
        print("Inspected:", entity)
      end,
      canInteract = function(entity)
        return true
      end,
      job = { ["inspector"] = 0 },
      gang = { ["ballas"] = 1 }
    }
  },
  distance = 2.0
})
```

### RemoveGlobalObject

Removes global options from all world objects.

* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveGlobalObject("Inspect Object")
```

***

## AddGlobalPlayer

Adds interaction options to all player entities globally

* **parameters**: `table`

```lua
exports['qb-target']:AddGlobalPlayer({
  options = {
    {
      num = 1,
      type = "client",
      event = "player:interact",
      icon = "fas fa-user-friends",
      label = "Interact with Player",
      action = function(entity)
        print("Interacting with player:", entity)
      end,
      canInteract = function(entity)
        return IsPedAPlayer(entity)
      end,
      job = { ["medic"] = 0 },
      gang = { ["vagos"] = 1 }
    }
  },
  distance = 2.5
})
```

### RemoveGlobalPlayer

Removes global options that apply to all player entities.

* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveGlobalPlayer("Interact with Player")
```

***

## SpawnPed

Spawns one or multiple peds with optional animations, relationships, weapons, and targeting

* datatable: `table`
  * **model**: `string`
  * **coords**: `vector4`
  * **freeze**: `boolean` (optional)
  * **invincible**: `boolean` (optional)
  * **blockevents**: `boolean` (optional)
  * **animDict**: `string` (optional)
  * **anim**: `string` (optional)
  * **flag**: `number` (optional)
  * **scenario**: `string` (optional)
  * **pedrelations**: `table` (optional)
    * **groupname**: `string`
    * **toowngroup**: `number`
    * **toplayer**: `number`
  * **weapon**: `table` (optional)
    * **name**: `string`
    * **ammo**: `number`
    * **hidden**: `boolean`
  * **target**: `table` (optional)
    * **useModel**: `boolean`
    * **options**: `table`
      * **type**: `string`
      * **event**: `string`
      * **icon**: `string`
      * **label**: `string`
    * **distance**: `float`
  * **action**: `function` (optional)

```lua
exports['qb-target']:SpawnPed({
  [1] = {
    model = 'a_m_m_business_01',
    coords = vector4(300.0, -500.0, 43.0, 90.0),
    freeze = true,
    invincible = true,
    blockevents = true,
    animDict = 'amb@world_human_hang_out_street@male_b@base',
    anim = 'base',
    flag = 1,
    scenario = 'WORLD_HUMAN_AA_SMOKE',
    pedrelations = {
      groupname = 'AMBIENT_GANG_BALLAS',
      toowngroup = 0,
      toplayer = 3
    },
    weapon = {
      name = 'weapon_pistol',
      ammo = 12,
      hidden = false
    },
    target = {
      useModel = false,
      options = {
        {
          type = "client",
          event = "npc:talk",
          icon = "fas fa-comment",
          label = "Talk"
        }
      },
      distance = 2.5
    },
    action = function(pedData)
      TriggerEvent('npc:spawned', pedData)
    end
  }
})
```

### RemoveSpawnedPed

Removes one or more peds previously spawned with `SpawnPed`&#x20;

* **peds**: `number` or `table`

```lua
if DoesEntityExist(myPed) then
  exports['qb-target']:RemoveSpawnedPed({ [1] = myPed })
end
```

***

## RemoveGlobalTypeOptions

Removes options from a global target type (e.g. peds, vehicles).

* **type**: `number` (1 for peds, 2 for vehicles, 3 for objects, 4 for players)
* **labels**: `string` or `table`

```lua
exports['qb-target']:RemoveType(1, "Frisk Ped")
```

***

## RemoveZone

Removes a zone that was previously added using `AddCircleZone`, `AddBoxZone`, `AddPolyZone`, or `AddComboZone`

* **name**: `string`

```lua
exports['qb-target']:RemoveZone("shop_zone")
```

***

## RaycastCamera

Performs a raycast from the camera's viewpoint to detect the closest entity in the crosshair.

* **flag**: `number`
* **playerCoords**: `vector3`

```lua
CreateThread(function()
  while true do
    local flag = 30
    local coords, distance, entity, entityType = exports['qb-target']:RaycastCamera(flag, GetEntityCoords(PlayerPedId()))
    if entityType > 0 then
      print("Entity hit:", entity)
    end
    flag = (flag == 30 and -1) or 30
    Wait(100)
  end
end)
```

***

## AllowTargeting

Enables or disables qb-target interactions for the player

* **allow**: `boolean`

```lua
if IsEntityDead(PlayerPedId()) then
  exports['qb-target']:AllowTargeting(false)
end
```
