---
description: Hunting for treasure in the deep blue sea!
---

# 🤿 qb-diving

## Introduction

* This resource lets your players go diving in the ocean for coral which they can sell

## Configuration

### General

```lua
Config = {}
Config.CopsChance = 0.0/1.0 -- The chance of the cops getting called when a coral gets picked up
```

### Diving Locations

```lua
Config.CoralLocations = {
    [1] = {
        label = "This is Location 1",
        coords = {
            Area = vector3(-2838.8, -376.1, 3.55),
            Coral = {
                [1] = {
                    coords = vector3(-2849.25, -377.58, -40.23),
                    length = 3,
                    width = 3,
                    heading = 100.0,
                    PickedUp = false
                },
                [2] = {
                    coords = vector3(-2838.43, -363.63, -39.45),
                    length = 3,
                    width = 3,
                    heading = 100.0,
                    PickedUp = false
                },
                [3] = {
                    coords = vector3(-2887.04, -394.87, -40.91),
                    length = 3,
                    width = 3,
                    heading = 100.0,
                    PickedUp = false
                },
                [4] = {
                    coords = vector3(-2808.99, -385.56, -39.32),
                    length = 3,
                    width = 3,
                    heading = 100.0,
                    PickedUp = false
                },
            }
        },
        DefaultCoral = 4,
        TotalCoral = 4,
    },
}
```

### Coral Types

```lua
Config.CoralTypes = {
    [1] = {
        item = "dendrogyra_coral", -- Item name
        maxAmount = math.random(1, 5), -- Random amount given
        price = math.random(70, 100), -- How much it's worth
    },
    [2] = {
        item = "antipatharia_coral",
        maxAmount = math.random(2, 7),
        price = math.random(50, 70),
    }
}
```

### Selling Price Modifiers

```lua
Config.PriceModifiers = { -- Modifies the selling price based on amount selling
    [1] = {
        minAmount = 5, -- If selling 5 or more
        maxAmount = 10, -- If selling 10 or less
        minPercentage = 80, -- Modifies selling price by random percentage between min and max
        maxPercentage = 85 -- Modifies selling price by random percentage between min and max
    },
    [2] = {
        minAmount = 11,
        maxAmount = 15,
        minPercentage = 70,
        maxPercentage = 75
    },
    [3] = {
        minAmount = 16,
        minPercentage = 50,
        maxPercentage = 55
    }
}
```

### Selling Locations

```lua
Config.SellLocations = {
    [1] = {
        coords = vector4(-1684.13, -1068.91, 13.15, 100.0),
        model = 'a_m_m_salton_01',
        zoneOptions = { -- Only used when not using the target
            length = 3,
            width = 3
        }
    }
}
```

## Items

* diving\_gear - Diving suit
* diving\_fill - Oxygen bottle

## Commands

* /divingsuit - Equips/unequips the diving suit
