---
description: Welcome to your complimentary apartment
---

# 🏨 qb-apartments

## Introduction

* This resource manages the apartment system for players. It uses qb-interior to spawn shells at a specific set of coordinates and functions the same as housing except by default the apartments do not cost any money

## Preview

![](<../.gitbook/assets/image (3) (1).png>)

## Configuration

```lua
Apartments = {}
Apartments.Starting = true/false -- Enable or disable starting apartments 
Apartments.SpawnOffset = 30 -- How far under the map the apartment shell will spawn
Apartments.Locations = { -- Create new apartment locations
    ["apartment1"] = {
        name = "apartment1", -- The apartment name that saves in the database
        label = "South Rockford Drive", -- The label of the apartment (shown in preview)
        coords = { -- The apartment entrance location 
            enter = vector4(-667.02, -1105.24, 14.63, 242.32),
        },
        polyzoneBoxData = { -- The polyzone box information for the entrance
            heading = 245,
            minZ = 13.5,
            maxZ = 16.0,
            debug = false,
            length = 1,
            width = 3,
            distance = 2.0,
            created = false
        }
    },
}
```
