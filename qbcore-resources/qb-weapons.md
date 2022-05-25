---
description: Pew pew
---

# 🔫 qb-weapons

## Introduction

* Handles the logic for weapon events
* Change weapon damage
* Reloading logic
* Weapon durability
* Weapon attachments

## Configuration

### General

```lua
Config.ReloadTime = math.random(4000, 6000) -- time it takes to reload

Config.DurabilityBlockedWeapons = { -- these will never break
    "weapon_stungun",
    "weapon_nightstick",
    "weapon_flashlight",
    "weapon_unarmed",
}
```

### Durability multiplier

```lua
Config.DurabilityMultiplier = { -- degrade multiplier, higher = quicker degrade
	-- Melee
	-- ['weapon_unarmed'] 				 = 0.15, 
	['weapon_dagger'] 				 = 0.15,
	['weapon_bat'] 				 	 = 0.15,
	['weapon_bottle'] 				 = 0.15,
}
```

### Weapon repair

```lua
Config.WeaponRepairPoints = {
    [1] = {
        coords = vector3(964.02, -1267.41, 34.97), -- interaction location
        IsRepairing = false, -- dynamically changes, don't edit
        RepairingData = {}, -- dynamically changes, don't edit
    }
}

Config.WeaponRepairCosts = { -- the price it costs to repair a weapon
    ["pistol"] = 1000,
    ["smg"] = 3000,
    ["mg"] = 4000,
    ["rifle"] = 5000,
    ["sniper"] = 7000,
}
```

### Weapon Attachemnts

```lua
WeaponAttachments = {
    -- PISTOLS
    ['WEAPON_PISTOL'] = { --items this weapon accepts as a attachment
        ['defaultclip'] = {
            component = 'COMPONENT_PISTOL_CLIP_01', -- Attachment hash
            item = 'pistol_defaultclip', --Item in the items.lua
            type = 'clip', --type of attachment
        },
        ['extendedclip'] = {
            component = 'COMPONENT_PISTOL_CLIP_02',
            item = 'pistol_extendedclip',
            type = 'clip',
        },
        ['flashlight'] = {
            component = 'COMPONENT_AT_PI_FLSH',
            item = 'pistol_flashlight',
        },
        ['suppressor'] = {
            component = 'COMPONENT_AT_PI_SUPP_02',
            item = 'pistol_suppressor',
        },
        ['luxuryfinish'] = {
            component = 'COMPONENT_PISTOL_VARMOD_LUXE',
            item = 'pistol_luxuryfinish',
        },
    },
}
```
