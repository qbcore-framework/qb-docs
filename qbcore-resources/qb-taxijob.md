---
description: Could you turn up the music please?
---

# 🚕 qb-taxijob

## Introduction

* Allows players to rent a taxi from Downtown Cab Co. and drive NPCs around or they can be contacted using the services app in [qb-phone.md](qb-phone.md "mention"). NPC missions can be started using the [qb-radialmenu.md](qb-radialmenu.md "mention")&#x20;

## Configuration

### General

```lua
Config.DefaultTextLocation = "left" -- left, right, top for qb-core drawText

Config.AllowedVehicles = { -- available taxi vehicles
   [1] = {
      model = "taxi", -- vehicle model
      label = Lang:t("info.taxi_label_1") -- translated menu label
   },
}

Config.Meter = { -- multiplier for trip cost calculated by distance traveled
    ["defaultPrice"] = 1.60
}

Config.BossMenu = vector3(903.32, -170.55, 74.0) -- boss menu placement

Config.Location = vector4(909.5, -177.35, 74.22, 238.5) -- map blip location

Config.CabSpawns = {
    vector4(899.0837, -180.4414, 73.4115, 238.7553), -- taxi spawn point
}
```

### NPC config

```lua
Config.NPCLocations = { -- exact coordinates for ped spawn
    TakeLocations = {
        [1] = vector4(257.61, -380.57, 44.71, 340.5),
        [2] = vector4(-48.58, -790.12, 44.22, 340.5),
        [3] = vector4(240.06, -862.77, 29.73, 341.5),
        [4] = vector4(826.0, -1885.26, 29.32, 81.5),
        [5] = vector4(350.84, -1974.13, 24.52, 318.5),
        [6] = vector4(-229.11, -2043.16, 27.75, 233.5),
        [7] = vector4(-1053.23, -2716.2, 13.75, 329.5),
        [8] = vector4(-774.04, -1277.25, 5.15, 171.5),
        [9] = vector4(-1184.3, -1304.16, 5.24, 293.5),
        [10] = vector4(-1321.28, -833.8, 16.95, 140.5),
        [11] = vector4(-1613.99, -1015.82, 13.12, 342.5),
        [12] = vector4(-1392.74, -584.91, 30.24, 32.5),
        [13] = vector4(-515.19, -260.29, 35.53, 201.5),
        [14] = vector4(-760.84, -34.35, 37.83, 208.5),
        [15] = vector4(-1284.06, 297.52, 64.93, 148.5),
        [16] = vector4(-808.29, 828.88, 202.89, 200.5),
    },
    DeliverLocations = {
        [1] = vector4(-1074.39, -266.64, 37.75, 117.5),
        [2] = vector4(-1412.07, -591.75, 30.38, 298.5),
        [3] = vector4(-679.9, -845.01, 23.98, 269.5),
        [4] = vector4(-158.05, -1565.3, 35.06, 139.5),
        [5] = vector4(442.09, -1684.33, 29.25, 320.5),
        [6] = vector4(1120.73, -957.31, 47.43, 289.5),
        [7] = vector4(1238.85, -377.73, 69.03, 70.5),
        [8] = vector4(922.24, -2224.03, 30.39, 354.5),
        [9] = vector4(1920.93, 3703.85, 32.63, 120.5),
        [10] = vector4(1662.55, 4876.71, 42.05, 185.5),
        [11] = vector4(-9.51, 6529.67, 31.37, 136.5),
        [12] = vector4(-3232.7, 1013.16, 12.09, 177.5),
        [13] = vector4(-1604.09, -401.66, 42.35, 321.5),
        [14] = vector4(-586.48, -255.96, 35.91, 210.5),
        [15] = vector4(23.66, -60.23, 63.62, 341.5),
        [16] = vector4(550.3, 172.55, 100.11, 339.5),
        [17] = vector4(-1048.55, -2540.58, 13.69, 148.5),
        [18] = vector4(-9.55, -544.0, 38.63, 87.5),
        [19] = vector4(-7.86, -258.22, 46.9, 68.5),
        [20] = vector4(-743.34, 817.81, 213.6, 219.5),
        [21] = vector4(218.34, 677.47, 189.26, 359.5),
        [22] = vector4(263.2, 1138.81, 221.75, 203.5),
        [23] = vector4(220.64, -1010.81, 29.22, 160.5),
    }
}
```

### NPC locations

```lua
Config.PZLocations = { -- polyzone boxes made around the NPC when spawned
    TakeLocations = {
        [1] = {
            coord = vector3(258.98, -377.9, 44.7),
            height = 17.6,
            width = 4.2,
            heading=69,
            minZ=43.75,
            maxZ=45.55
        },
    },
    DropLocations = {
        [1] = {
            coord = vector3(-1073.21, -265.35, 37.35),
            height = 21.2,
            width = 4.2,
            heading=296,
            minZ=35.0,
            maxZ=39.2
        },
    }
}
```

### NPC models

```lua
Config.NpcSkins = { -- https://docs.fivem.net/docs/game-references/ped-models/
    [1] = {
        'a_f_m_skidrow_01', -- ped models for in-city
    },
    [2] = {
        'ig_barry', -- ped models for out of city
    }
} 
```
