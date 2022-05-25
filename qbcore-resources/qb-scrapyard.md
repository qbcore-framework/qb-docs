---
description: Hope you got your tetanus shot
---

# 🔋 qb-scrapyard

## Introduction

* Allows players to go to the "list" location from the config and receive an email with a car to find and scrap for reward items!

{% hint style="success" %}
This job does not pay out money by default, it pairs well with the crafting system from [qb-inventory.md](qb-inventory.md "mention")
{% endhint %}

## Configuration

### Locations

```lua
Config.Locations = { -- interaction locations
    [1] = {
        ["main"] = vector3(2397.42, 3089.44, 49.92), -- scrapyard location
        ["deliver"] = vector3(2351.5, 3132.96, 48.2), -- vehicle delivery point
        ["list"] = vector3(2403.51, 3127.95, 48.15), -- email generation point
    }
}
```

### Items

```lua
Config.Items = { -- list of potential reward items (randomized)
    "metalscrap", -- item name
    "plastic",
    "copper",
    "iron",
    "aluminum",
    "steel",
    "glass",
}
```

### Vehicles

```lua
Config.Vehicles = { -- list of potential vehicles to find (randomized)
    [1] = "ninef", -- vehicle model
    [2] = "ninef2",
    [3] = "banshee",
    [4] = "alpha",
    [5] = "baller",
    [6] = "bison",
    [7] = "huntley",
    [8] = "f620",
    [9] = "asea",
    [10] = "pigalle",
    [11] = "bullet",
    [12] = "turismor",
    [13] = "zentorno",
    [14] = "dominator",
    [15] = "blade",
    [16] = "chino",
    [17] = "sabregt",
    [18] = "bati",
    [19] = "carbonrs",
    [20] = "akuma",
    [21] = "thrust",
    [22] = "exemplar",
    [23] = "felon",
    [24] = "sentinel",
    [25] = "blista",
    [26] = "fusilade",
    [27] = "jackal",
    [28] = "blista2",
    [29] = "rocoto",
    [30] = "seminole",
    [31] = "landstalker",
    [32] = "picador",
    [33] = "prairie",
    [34] = "bobcatxl",
    [35] = "gauntlet",
    [36] = "virgo",
    [37] = "fq2",
    [38] = "jester",
    [39] = "rhapsody",
    [40] = "feltzer2",
}
```
