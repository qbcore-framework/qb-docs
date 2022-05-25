---
description: Doesn't look like anyone's home! Don't mind if I do
---

# 🔫 qb-houserobbery

## Introduction

* Allows players to use a lockpick at specific coordinates within an in-game time range and enter a house where they can search cabinets, drawers, etc. for items!

{% hint style="warning" %}
This resource relies on qb-lockpick and qb-skillbar for the mini games and qb-interior for the export to spawn the configured shell
{% endhint %}

{% hint style="info" %}
If players aren't using an advanced lockpick then they need to have a regular lockpick and screwdriverset
{% endhint %}

## Configuration

### General

```lua
Config = {}
Config.MinZOffset = 45 -- how far under the ground the shell will spawn
Config.MinimumHouseRobberyPolice = 2 -- minimum amount of police needed to rob
Config.MinimumTime = 5 -- minimum in-game hour to rob
Config.MaximumTime = 22 -- maximum in-game hour to rob
```

### Rewards

```lua
Config.Rewards = {
    [1] = {
        ["cabin"] = { -- this is the searchable location
            "plastic", -- these are the list of items you could possibly get
            "diamond_ring",
            "goldchain",
            "weed_skunk",
            "thermite",
            "cryptostick",
            "weapon_golfclub"
        },
        ["kitchen"] = {
            "tosti",
            "sandwich",
            "goldchain"
        },
        ["chest"] = {
            "plastic",
            "rolex",
            "diamond_ring",
            "goldchain",
            "weed_skunk",
            "thermite",
            "cryptostick",
            "weapon_combatpistol"
        },
        ["livingroom"] = {
            "plastic",
            "rolex",
            "diamond_ring",
            "goldchain",
            "thermite",
            "cryptostick",
            "tablet",
            "pistol_ammo"
        }
    }
}
```

### Locations

```lua
Config.Houses = {
    ["perfectdrive1"] = { -- the house name
        ["coords"] = { -- the house location where players use lockpick
            ["x"] = -784.72,
            ["y"] = 459.77,
            ["z"] = 100.39,
            ["h"] = 34.89
        },
        ["opened"] = false, -- changed automatically so don't edit
        ["tier"] = 1, -- only works with 1 by default but can be modified
        ["furniture"] = { -- these are the searchable locations
            [1] = {
                ["type"] = "cabin", -- type of searchable location
                ["coords"] = { -- where 
                    ["x"] = 4.15,
                    ["y"] = 7.82,
                    ["z"] = 1.0
                },
                ["searched"] = false, -- changed automatically so don't edit
                ["isBusy"] = false, -- changed automatically so don't edit
                ["text"] = "Search Bedside Cabinet" -- the text that displays
            },
            [2] = {
                ["type"] = "cabin",
                ["coords"] = {["x"] = 5.95, ["y"] = 9.34, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search Closet"
            },
            [3] = {
                ["type"] = "kitchen",
                ["coords"] = {["x"] = -1.03, ["y"] = 0.78, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search through the kitchen cabinets"
            },
            [4] = {
                ["type"] = "chest",
                ["coords"] = {["x"] = 6.904, ["y"] = 3.987, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search Chest"
            },
            [5] = {
                ["type"] = "cabin",
                ["coords"] = {["x"] = 0.933, ["y"] = 1.254, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search Drawers"
            },
            [6] = {
                ["type"] = "cabin",
                ["coords"] = {["x"] = 6.19, ["y"] = 3.35, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Night Stand Cabinet"
            },
            [7] = {
                ["type"] = "kitchen",
                ["coords"] = {["x"] = -2.20, ["y"] = -0.30, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search through the kitchen cabinets"
            },
            [8] = {
                ["type"] = "kitchen",
                ["coords"] = {["x"] = -4.35, ["y"] = -0.64, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search through shelves"
            },
            [9] = {
                ["type"] = "livingroom",
                ["coords"] = {["x"] = -6.90, ["y"] = 4.42, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search through shelves"
            },
            [10] = {
                ["type"] = "livingroom",
                ["coords"] = {["x"] = -6.98, ["y"] = 7.91, ["z"] = 1.0},
                ["searched"] = false,
                ["isBusy"] = false,
                ["text"] = "Search through shelves"
            },
        }
    },
}
```

### Changing shell

{% hint style="success" %}
If you'd like to use different shells for house robberies then navigate here:

\
qb-houserobbery -> client -> main.lua -> line 54\
\
Once you are there you can change the export or add some elseif statements
{% endhint %}

```lua
local function enterRobberyHouse(house)
    TriggerServerEvent("InteractSound_SV:PlayOnSource", "houses_door_open", 0.25)
    openHouseAnim()
    Wait(250)
    local coords = {
        x = Config.Houses[house]["coords"]["x"],
        y = Config.Houses[house]["coords"]["y"],
        z= Config.Houses[house]["coords"]["z"] - Config.MinZOffset
    }
    local data
    if Config.Houses[house]["tier"] == 1 then
        data = exports['qb-interior']:CreateHouseRobbery(coords)
    elseif Config.Houses[house]["tier"] == 2 then
        data = myNewExport -- find exports in qb-interior/client/main.lua
    elseif Config.Houses[house]["tier"] == 3 then
        data = myNewExport -- find exports in qb-interior/client/main.lua
    elseif Config.Houses[house]["tier"] == 4 then
        data = myNewExport -- find exports in qb-interior/client/main.lua
    end
    Wait(100)
    houseObj = data[1]
    POIOffsets = data[2]
    inside = true
    currentHouse = house
    Wait(500)
    TriggerEvent('qb-weathersync:client:DisableSync')
end
```
