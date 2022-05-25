---
description: Those bags aren't gonna throw themselves
---

# 🚛 qb-garbagejob

## Introduction

* Allows players to rent a garbage truck for a configured amount and pick up garbage bags around the map. Each bag will net the player a variable amount of pay that can is easily adjustable. There is also the ability to enable the chance of players receiving a cryptostick from this job. Read more about those in [qb-crypto.md](qb-crypto.md "mention")

## Configuration

### General

```lua
Config = {}

-- Rental fee that is returned on truck return
Config.TruckPrice = 250

-- Want to give out a cryptostick per stop?
Config.GiveCryptoStick = true

-- Has to roll this number or higher to receive a cryptostick
Config.CryptoStickChance = 75

-- How many stops minimum should the job roll?
Config.MinStops = 5

-- Upper worth per bag
Config.BagUpperWorth = 100

-- Lower worth per bag
Config.BagLowerWorth = 50

-- Minimum bags per stop
Config.MinBagsPerStop = 2

-- Maximum bags per stop
Config.MaxBagsPerStop = 5
```

### Peds

```lua
Config.Peds = { -- configure the peds that players interact with
    {
        model = 's_m_y_garbage', -- https://docs.fivem.net/docs/game-references/ped-models/
        coords = vector4(-322.24, -1546.02, 30.02, 294.97),
        zoneOptions = { -- Used for when UseTarget is false
            length = 3.0,
            width = 3.0
        }
    }
}
```

### Locations

```lua
Config.Locations = { -- configure the interaction points
    ["main"] = {
        label = "Garbage Depot", -- map blip name
        coords = vector3(-313.84, -1522.82, 27.56), -- location
    },
}
```

### Vehicles

```lua
Config.Vehicles = { -- configure the vehicles used for the job
    ["trash2"] = "Garbage Truck",
}
```
