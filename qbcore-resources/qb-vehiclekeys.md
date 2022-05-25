---
description: Don't lock them in your car
---

# 🔑 qb-vehiclekeys

## Introduction

* Handles the logic of locking/lockpicking and robbing cars
* Uses [qb-lockpick.md](qb-lockpick.md "mention") for the lockpicking minigame
* Aim a gun at a ped driver for a chance to rob their keys

## Configuration

### General

```lua
Config.HotwireChance = 0.5 -- chance for successful hotwire or not

Config.RemoveLockpickNormal = 0.5 -- chance to remove lockpick on fail
Config.RemoveLockpickAdvanced = 0.2 -- chance to remove advanced lockpick on fail

Config.CarjackingTime = 7500 -- progress bar time
Config.DelayBetweenCarjackings = 10000 -- cooldown between car jacking

Config.TimeBetweenHotwires = 5000 -- cooldown between hotwire actions
Config.minHotwireTime = 20000 -- progress bar time
Config.maxHotwireTime = 40000 -- progress bar time

Config.AlertCooldown = 10000 -- cooldown between police alerts in milliseconds
Config.PoliceAlertChance = 1.75 -- chance of alerting police during the day
Config.PoliceNightAlertChance = 1.50 -- chance of alerting police at night

Config.ImmuneVehicles = { -- These vehicles cannot be jacked
    'stockade'
}

Config.NoLockVehicles = { -- These vehicles cannot be locked
    'adder'
}
```

### Blacklisted weapons

```lua
Config.NoCarjackWeapons = { -- you can not jack a car with these weapons
    "WEAPON_UNARMED",
    "WEAPON_Knife",
    "WEAPON_Nightstick",
    "WEAPON_HAMMER",
}
```

### Car jack chance

```lua
Config.CarjackChance = { -- this is the percentage chance of succesful car jacking
    ['2685387236'] = 0.0,   -- melee
    ['416676503'] = 0.5,   -- handguns
    ['337201093'] = 0.75,   -- SMG
    ['860033945'] = 0.90,   -- shotgun
    ['970310034'] = 0.90,   -- assault
    ['1159398588'] = 0.99,  -- LMG
    ['3082541095'] = 0.99,  -- sniper
    ['2725924767'] = 0.99,  -- heavy
    ['1548507267'] = 0.0,   -- throwable
    ['4257178988'] = 0.0,   -- misc
}
```
