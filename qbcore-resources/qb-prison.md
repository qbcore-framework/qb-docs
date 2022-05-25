---
description: Nice, quiet gated community
---

# 🔐 qb-prison

## Introduction

* Allows police the ability to jail players for a certain length of time. When a player is jailed, they are stripped of their items and job. When they are released, those items are returned

{% hint style="success" %}
Players can use a `gatecrack` and `electronickit` item to hack their way out of prison!
{% endhint %}

## Configuration

### General

```lua
Config = {}
Config.Jobs = { -- jobs that players can do, index used for locations below
    ["electrician"] = "Electrician"
}
```

### Locations

```lua
Config.Locations = {
    ["freedom"] = { -- interaction location to check remaining time / be released
        coords = vector4(1836.37, 2585.33, 45.89, 272.96)
    },
    ["outside"] = { -- location for players to spawn upon release
        coords = vector4(1848.13, 2586.05, 45.67, 269.5)
    },
    ["yard"] = { -- location of the cells
        coords = vector4(1765.67, 2565.91, 45.56, 1.5)
    },
    ["middle"] = { -- location of blip for police during prison break
        coords = vector4(1693.33, 2569.51, 45.55, 123.5)
    },
    ["shop"] = { -- location of the prison shop
        coords = vector4(1786.19, 2557.77, 45.62, 0.5)
    },
    spawns = { -- locations for players to spawn when jailed
        [1] = {
            animation = "bumsleep", -- animation to play on spawn
            coords = vector4(1661.046, 2524.681, 45.564, 260.545) -- spawn loc
        },
    }
}
```

### Work

```lua
Config.Locations = { -- set locations for players to do work to reduce time
    jobs = {
        ["electrician"] = { -- job name
            [1] = { -- interaction location
                coords = vector4(1761.46, 2540.41, 45.56, 272.249),
            },
            [2] = {
                coords = vector4(1718.54, 2527.802, 45.56, 272.249),
            },
            [3] = {
                coords = vector4(1700.199, 2474.811, 45.56, 272.249),
            },
            [4] = {
                coords = vector4(1664.827, 2501.58, 45.56, 272.249),
            },
            [5] = {
                coords = vector4(1621.622, 2509.302, 45.56, 272.249),
            },
            [6] = {
                coords = vector4(1627.936, 2538.393, 45.56, 272.249),
            },
            [7] = {
                coords = vector4(1625.1, 2575.988, 45.56, 272.249),
            }
        }
    }
}
```

### Shop items

```lua
Config.CanteenItems = { -- items available to buy in the prison shop
    [1] = {
        name = "sandwich", -- item name
        price = 4, -- item price
        amount = 50, -- available stock to buy
        info = {}, -- item info
        type = "item", -- item type
        slot = 1 -- inventory slot to be shown in
    },
    [2] = {
        name = "water_bottle",
        price = 4,
        amount = 50,
        info = {},
        type = "item",
        slot = 2
    }
}
```

### Prison break

* Found in qb-prison/client/prisonbreak.lua

```lua
local Gates = { -- available gates for players to hack
    [1] = {
        gatekey = 13, -- door id for qb-doorlock !! important !!
        coords = vector3(1845.99, 2604.7, 45.58), -- interaction location
        hit = false, -- dynamically changes, don't edit
    },
    [2] = {
        gatekey = 14,
        coords = vector3(1819.47, 2604.67, 45.56),
        hit = false,
    },
    [3] = {
        gatekey = 15,
        coords = vector3(1804.74, 2616.311, 45.61),
        hit = false,
    }
}
```
