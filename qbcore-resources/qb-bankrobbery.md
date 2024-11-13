---
description: Career criminal?
---

# 💰 qb-bankrobbery

## Introduction

* Creates robbable lockers inside various banks across the map. It allows for configuring the amount of police needed for each type of robbery as well as the rewards you can get

{% hint style="warning" %}
This resource includes a thermite mini game in the html folder so without it thermite won't work properly!
{% endhint %}

{% hint style="danger" %}
This resource works with qb-doorlock to manage the state of the doors using the event named "qb-doorlock:server:updateState" so make sure each door is in the config of qb-doorlock with the correct door id
{% endhint %}

## Configuration

```lua
Config = {}
Config.MinimumPaletoPolice = 4 -- Minimum amount of police online to start the robbery
Config.MinimumPacificPolice = 5 -- Minimum amount of police online to start the robbery
Config.MinimumFleecaPolice = 3 -- Minimum amount of police online to start the robbery
Config.MinimumThermitePolice = 2 -- Minimum amount of police online to use thermite
Config.OutlawCooldown = 5 -- The amount of minutes it takes for the cops to be able to be called again after they were called
Config.HitsNeeded = 13 -- The amount of powerstation needed to be hit to cause a blackout
Config.BlackoutTimer = 10 -- The amount of minutes a blackout will take until all power comes back
Config.RewardTypes = {} -- The reward types you can get from the bankrobbery
Config.LockerRewards = {} -- The rewards you can get from the locker
Config.LockerRewardsPaleto = {} -- The rewards you can get from the locker in paleto
Config.LockerRewardsPacific = {} -- The rewards you can get from the locker in pacific
Config.PowerStations = {} -- Powerstation coords to blow up
Config.SmallBanks = {} -- Small banks to rob
Config.BigBanks = {} -- Big banks to rob
```

## Items

* thermite - Used to blow up power station locations or bank gates (need lighter)
* security\_card\_01 - Item used at the paleto bank vault
* security\_card\_02 - Item used at the pacific bank vault
* electronickit - Item used at the fleeca bank vault
