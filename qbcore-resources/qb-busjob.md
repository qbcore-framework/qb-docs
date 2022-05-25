---
description: NPC's have places to be!
---

# 🚌 qb-busjob

{% hint style="danger" %}
THIS RESOURCE IS A WORK IN PROGRESS
{% endhint %}

## Introduction

* Allows your players to go to the bus depot and start driving around Los Santos collecting passengers from bus stops and dropping them off at others

## Configuration

```lua
Config = {}
Config.AllowedVehicles = {} -- Define the bus model to use
Config.Location = vector4() -- Set the blip and vehicle withdraw location
Config.NPCLocations = {} -- The bus stop locations
Config.NpcSkins = {} -- List of ped models randomly chosen to spawn
```
