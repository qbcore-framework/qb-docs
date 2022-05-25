---
description: No security officer is safe
---

# 🔫 qb-truckrobbery

## Introduction

* A bank truck heist that players can interact with to get marked bills

{% hint style="danger" %}
This resource is currently undergoing construction for improvements!
{% endhint %}

## Configuration

{% hint style="warning" %}
This resource has no configuration file all configuration must be done through the resources files
{% endhint %}

### Server side configuration

```lua
local ActivePolice = 2  -- minimum police needed
local cashA = 250  -- minimum reward amount
local cashB = 450 -- maximum reward amount
local ActivationCost = 500 -- mission start cost
local ResetTimer = 2700 * 1000  -- cooldown between robberies
```

### Client side configuration

```lua
local MissionMarker = vector3(960.71, -215.51, 76.25) -- place where is the marker with the mission
local dealerCoords = vector3(960.78, -216.25, 76.25) -- place where the NPC dealer stands
local VehicleSpawn1 = vector3(-1327.479736328, -86.045326232910, 49.31)  -- random vehicle spawn points
local VehicleSpawn2 = vector3(-2075.888183593, -233.73908996580, 21.10)
local VehicleSpawn3 = vector3(-972.1781616210, -1530.9045410150, 4.890)
local VehicleSpawn4 = vector3(798.18426513672, -1799.8173828125, 29.33)
local VehicleSpawn5 = vector3(1247.0718994141, -344.65634155273, 69.08)
local DriverWep = "WEAPON_MICROSMG" -- the weapon the driver is to be equipped with
local NavWep = "WEAPON_MICROSMG"  -- the weapon the guard should be equipped with
local TimeToBlow = 30 * 1000 	-- bomb detonation time after planting, default 20 seconds
```
