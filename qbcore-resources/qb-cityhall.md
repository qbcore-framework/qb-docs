---
description: Need a new job or identification card?
---

# 🏢 qb-cityhall

## Introduction

* Players can manage what job they have and retrieve licenses like weapon licenses, driver's license and identification cards

{% hint style="danger" %}
This resource will kick players that try to exploit it by giving themself an item or job that is not defined in the resource or that are not within proper distance of the city hall point
{% endhint %}

## Preview

![](https://camo.githubusercontent.com/fb24d4570b9e370af639567c94ba0a238f8d1f497ef6aeebe4914ff324624fc6/68747470733a2f2f692e696d6775722e636f6d2f6c365a526c58502e706e67)

## Configuration

### City hall locations

```lua
Config.Cityhalls = {
    {
        coords = vec3(-265.0, -963.6, 31.2),
        showBlip = true,
        blipData = {
            sprite = 487,
            display = 4,
            scale = 0.65,
            colour = 0,
            title = "City Services"
        },
        licenses = { -- what licenses are available at this location
            ["id_card"] = {
                label = "ID Card",
                cost = 50,
            },
            ["driver_license"] = {
                label = "Driver License",
                cost = 50,
                metadata = "driver"
            },
            ["weaponlicense"] = {
                label = "Weapon License",
                cost = 50,
                metadata = "weapon"
            },
        }
    },
}
```

{% hint style="info" %}
If you want to add more licenses you need to add them to the [player-data.md](../qb-core/player-data.md "mention") table&#x20;
{% endhint %}

### Driving school locations

```lua
Config.DrivingSchools = {
    { -- Driving School 1
        coords = vec3(240.3, -1379.89, 33.74),
        showBlip = true,
        blipData = {
            sprite = 225,
            display = 4,
            scale = 0.65,
            colour = 3,
            title = "Driving School"
        },
        instructors = { -- instructors citizenid
            "DJD56142",
            "DXT09752",
            "SRI85140",
        }
    },
}
```

### Peds

```lua
Config.Peds = {
    -- Cityhall Ped
    {
        model = 'a_m_m_hasjew_01', -- https://docs.fivem.net/docs/game-references/ped-models/
        coords = vec4(-262.79, -964.18, 30.22, 181.71),
        scenario = 'WORLD_HUMAN_STAND_MOBILE', -- https://github.com/Santagain/gtav-scenarios
        cityhall = true,
        zoneOptions = { -- Used for when UseTarget is false
            length = 3.0,
            width = 3.0,
            debugPoly = false
        }
    },
    -- Driving School Ped
    {
        model = 'a_m_m_eastsa_02',
        coords = vec4(240.91, -1379.2, 32.74, 138.96),
        scenario = 'WORLD_HUMAN_STAND_MOBILE',
        drivingschool = true,
        zoneOptions = { -- Used for when UseTarget is false
            length = 3.0,
            width = 3.0
        }
    }
}
```

### Modifying available jobs

* Found in server/main.lua

```lua
local availableJobs = {
    ["trucker"] = "Trucker",
    ["taxi"] = "Taxi",
    ["tow"] = "Tow Truck",
    ["reporter"] = "News Reporter",
    ["garbage"] = "Garbage Collector",
    ["bus"] = "Bus Driver",
}
```

## Commands

* /drivinglicense - Players with their citizenid's listed in the config can use this command to assign other players a drivers license
