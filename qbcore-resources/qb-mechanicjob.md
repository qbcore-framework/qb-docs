---
description: Fix 'em up real good
---

# 🧑🔧 🧑🔧 🧑🔧 🧑🔧 qb-mechanicjob

## Introduction

* Players with the mechanic job can attach vehicles to "plates" and repair body/engine. This also includes a stash, job vehicles and a clock in/out location

## Preview

![Displays vehicle heath](<../.gitbook/assets/mechanicchatstatus (1).png>)

![Menu for mechanics to work on cars](../.gitbook/assets/mechanicmenu.png)

![Displays vehicle health in chat](../.gitbook/assets/mechanicchat.png)

## Configuration

### General

```lua
Config = {}

Config.AttachedVehicle = nil -- changes dynamically, don't edit

Config.AuthorizedIds = { -- players authorized to use hire/fire commands
    "insertcitizenidhere",
}

Config.Vehicles = { -- list of job vehicles that can be withdrawn
    ["flatbed"] = "Flatbed",
    ["towtruck"] = "Towtruck",
    ["minivan"] = "Minivan (Rental Car)",
    ["blista"] = "Blista",
}
```

### Locations

```lua
Config.Locations = {
    ["exit"] = vector3(-339.04, -135.53, 39), -- location for map blip
    ["duty"] = vector3(-323.39, -129.6, 39.01), -- interaction location
    ["stash"] = vector3(-319.49, -131.9, 38.98), -- interaction location
    ["vehicle"] = vector4(-370.51, -107.88, 38.35, 72.56), -- interaction location
}

Config.Plates = { -- repair locations that "locks" vehicle in place
    [1] = { -- polyzone box data
        coords = vector4(-340.95, -128.24, 39, 160.0),
        boxData = {
            heading = 340,
            length = 5,
            width = 2.5,
            debugPoly = false
        },
        AttachedVehicle = nil, -- changes dynamically, don't edit
    },
    [2] = {
        coords = vector4(-326.78, -144.82, 39.06, 70),
        boxData = {
            heading = 249,
            length = 6.5,
            width = 5,
            debugPoly = false
        },
        AttachedVehicle = nil,
    },
}
```

### Vehicle parts

```lua
Config.MaxStatusValues = { -- the maximum health of the given part
    ["engine"] = 1000.0,
    ["body"] = 1000.0,
    ["radiator"] = 100,
    ["axle"] = 100,
    ["brakes"] = 100,
    ["clutch"] = 100,
    ["fuel"] = 100,
}

Config.ValuesLabels = { -- the label of the given part in the repair menu
    ["engine"] = "Motor",
    ["body"] = "Body",
    ["radiator"] = "Radiator",
    ["axle"] = "Drive Shaft",
    ["brakes"] = "Brakes",
    ["clutch"] = "Clutch",
    ["fuel"] = "Fuel Tank",
}

Config.RepairCost = { -- the item that is needed to repair the given part
    ["body"] = "plastic",
    ["radiator"] = "plastic",
    ["axle"] = "steel",
    ["brakes"] = "iron",
    ["clutch"] = "aluminum",
    ["fuel"] = "plastic",
}

Config.RepairCostAmount = { -- the item and amount that is need to repair a part
    ["engine"] = {
        item = "metalscrap",
        costs = 2,
    },
    ["body"] = {
        item = "plastic",
        costs = 3,
    },
    ["radiator"] = {
        item = "steel",
        costs = 5,
    },
    ["axle"] = {
        item = "aluminum",
        costs = 7,
    },
    ["brakes"] = {
        item = "copper",
        costs = 5,
    },
    ["clutch"] = {
        item = "copper",
        costs = 6,
    },
    ["fuel"] = {
        item = "plastic",
        costs = 5,
    },
}
```

### Vehicle part damage

```lua
Config.Damages = { -- These are the menu labels for the respective part 
    ["radiator"] = "Radiator",
    ["axle"] = "Drive Shaft",
    ["brakes"] = "Brakes",
    ["clutch"] = "Clutch",
    ["fuel"] = "Fuel Tank",
}

Config.MinimalMetersForDamage = { -- vehicle driving distance range
    [1] = {
        min = 8000, -- minimum range for damage to occur
        max = 12000, -- maximum range for damage to occur
        multiplier = {
            min = 1, -- minimum damage multiplier
            max = 8, -- maximum damage multiplier 
        }
    },
    [2] = {
        min = 12000,
        max = 16000,
        multiplier = {
            min = 8,
            max = 16,
        }
    },
    [3] = {
        min = 12000,
        max = 16000,
        multiplier = {
            min = 16,
            max = 24,
        }
    },
}
```

## Commands

{% hint style="warning" %}
Only players with citizenid's found in the config can use these commands
{% endhint %}

* /setmechanic - Hire a player as a mechanic
* /firemechanic - Remove a player as a mechanic
* /setvehiclestatus - Modify the vehicle part damage level
