---
description: How many lives will you save?
---

# 🚑 qb-ambulancejob

## Introduction

This resource handles all the job functionality for the ambulance job title + more!

It includes:

* Hospital bed check-in system ([https://github.com/ElusionPDX/mythic\_hospital](https://github.com/ElusionPDX/mythic\_hospital))
* Full damage/bleeding system ([https://github.com/ElusionPDX/mythic\_hospital](https://github.com/ElusionPDX/mythic\_hospital))
* Clock in/out, job shop, vehicle spawner

## Configuration

```lua
Config = {}
Config.MinimalDoctors = 2 -- How many players with the ambulance job to prevent the hospital check-in system from being used
Config.WipeInventoryOnRespawn = true/false -- Enable or disable removing all the players items when they respawn at the hospital
Config.Locations = {} -- Edit the various interaction points for players or create new ones
Config.AuthorizedVehicles = {} -- Vehicles players can use based on their ambulance job grade level
Config.Helicopter = "polmav" -- Helicopter model that players with the ambulance job can use
Config.Items = {} -- Items found in the ambulance shop for players with the ambulance job to purchase
Config.BillCost = 2000 -- Price that players are charged for using the hospital check-in system
Config.DeathTime = 300 -- How long the timer is for players to bleed out completely and respawn at the hospital
Config.PainkillerInterval = 60 -- Set the length of time painkillers last (per one)
Config.HealthDamage = 5 -- Minumum damage done to health before checking for injuries
Config.ArmorDamage = 5 -- Minumum damage done to armor before checking for injuries
Config.ForceInjury = 35 -- Maximum amount of damage a player can take before limb damage & effects are forced to occur
Config.AlwaysBleedChance = 70 -- Set the chance out of 100 that if a player is hit with a weapon, that also has a random chance, it will cause bleeding
Config.MessageTimer = 12 -- How long it will take to display limb/bleed message
Config.AIHealTimer = 20 -- How long it will take to be healed after checking in, in seconds
Config.BleedTickRate = 30 -- How much time, in seconds, between bleed ticks
Config.BleedMovementTick = 10 -- How many seconds is taken away from the bleed tick rate if the player is walking, jogging, or sprinting
Config.BleedMovementAdvance = 3 -- How much time moving while bleeding adds
Config.BleedTickDamage = 8 -- The base damage that is multiplied by bleed level everytime a bleed tick occurs
Config.FadeOutTimer = 2 -- How many bleed ticks occur before fadeout happens
Config.BlackoutTimer = 10 -- How many bleed ticks occur before blacking out
Config.AdvanceBleedTimer = 10 -- How many bleed ticks occur before bleed level increases
Config.HeadInjuryTimer = 30 -- How much time, in seconds, do head injury effects chance occur
Config.ArmInjuryTimer = 30 -- How much time, in seconds, do arm injury effects chance occur
Config.LegInjuryTimer = 15 -- How much time, in seconds, do leg injury effects chance occur
Config.HeadInjuryChance = 25 -- The chance, in percent, that head injury side-effects get applied
Config.LegInjuryChance = { -- The chance, in percent, that leg injury side-effects get applied
    Running = 50,
    Walking = 15
}
Config.MajorArmoredBleedChance = 45 -- The chance, in percent, that a player will get a bleed effect when taking heavy damage while wearing armor
Config.DamageMinorToMajor = 35 -- How much damage would have to be applied for a minor weapon to be considered a major damage event. Put this at 100 if you want to disable it
Config.AlertShowInfo = 2 -- How many injuries a player must have before being alerted about them
Config.WeaponClasses = {} -- Define gta weapon classe numbers
Config.MinorInjurWeapons = {} -- Define which weapons cause small injuries
Config.MajorInjurWeapons = {} -- Define which weapons cause large injuries
Config.AlwaysBleedChanceWeapons = {} -- Define which weapons will always cause bleedign
Config.ForceInjuryWeapons = {} -- Define which weapons will always cause injuries
Config.CriticalAreas = {} -- Define body areas that will always cause bleeding if wearing armor or not
Config.StaggerAreas = {} -- Define body areas that will always cause staggering if wearing armor or not
Config.WoundStates = {} -- Translate wound alerts
Config.BleedingStates = {} -- Translate bleeding alerts
Config.MovementRate = {} -- Set the player movement rate based on the level of damage they have
Config.Bones = {} -- Correspond bone hash numbers to their label
Config.BoneIndexes = {} -- Correspond bone labels to their hash number
Config.Weapons = {} -- Correspond weapon names to their class number
Config.VehicleSettings = {} -- Enable or disable vehicle extras when pulling them from the ambulance job vehicle spawner
```

## Items

* ifaks - Relieves player stress and heals them by + 10
* bandage - Heals player by + 10 and has 50% chance of removing 1 level of bleeding
* firstaid - Completely heals closest player as long as they are in last-stand
* painkillers - Stops bleeding temporarily but wears off over time

## Events

Calling this event will modify the players isdead metadata to the passed bool (true/false)

```lua
-- Server event
RegisterNetEvent('hospital:server:SetDeathStatus', function(isDead)

-- Example
TriggerServerEvent('hospital:server:SetDeathStatus', true)
```

Calling this event will modify the players inlaststand metadata to the passed bool (true/false)

```lua
-- Server event
RegisterNetEvent('hospital:server:SetLaststandStatus', function(bool)

-- Example
TriggerServerEvent('hospital:server:SetLaststandStatus', true)
```

Calling this event will send a notification to all players with the ambulance job title

```lua
-- Server event
RegisterNetEvent('hospital:server:ambulanceAlert', function(text)

-- Example
TriggerServerEvent('hospital:server:ambulanceAlert', 'I need help')
```

Calling this event will revive a player for free or a fee with a true bool

{% hint style="info" %}
Could be used for a revive spot/ped that charges money
{% endhint %}

{% hint style="warning" %}
This event always removes a first aid kit from the source player
{% endhint %}

```lua
-- Server event
RegisterNetEvent('hospital:server:RevivePlayer', function(playerId, isOldMan)

-- Example
local player, distance = QBCore.Functions.GetClosestPlayer()
local playerId = GetPlayerServerId(player)
TriggerServerEvent('hospital:server:RevivePlayer', playerId, true)
```

## Callbacks

Using this callback will return the number of players online with the ambulance job

```lua
QBCore.Functions.CreateCallback('hospital:GetDoctors', function(source, cb)

-- Example
QBCore.Functions.TriggerCallback('hospital:GetDoctors', function(cb)
    print('The number of doctors online is '..cb)
end)
```

## Commands

<details>

<summary>/911e [message] - sends a message to EMS</summary>

Sends a message to EMS players with the job 'ambulance'.

**Permission level:** user

* **message** - (required) The message to send

</details>

<details>

<summary>/status - check the status of the nearest player</summary>

This will find the closest player and check their health status

**Permission level:** user

</details>

<details>

<summary>/heal - heals the nearest player</summary>

This will find the nearest player and heal them

**Permission level:** user

</details>

<details>

<summary>/revivep - revives the nearest player</summary>

This will find the nearest player and revive them

**Permission level:** user

</details>

<details>

<summary>/revive - revive yourself</summary>

Revives yourself to full health

**Permission level:** admin

</details>

<details>

<summary>/setpain [opt: id] - sets the pain level to the player</summary>

Sets the pain level to the player with the given `id` or to yourself if no id is given.

**Permission level:** admin

</details>

<details>

<summary>/kill [opt: id] - kills the player</summary>

Kills the player with the given `id` or kills yourself if no id is given.

**Permission level:** admin

* **id** - (optional) The player id

</details>

<details>

<summary>/aheal [opt: id] - heals a player</summary>

Heals a player with the given `id` or heals yourself if no id is given.

**Permission level:** admin

* **id** - (optional) The player id

</details>
