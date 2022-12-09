---
description: Resource for handling **alot** of misc stuff.
---

# 📚 qb-smallresources

## Introduction

* This resource handles many small tasks for the framework
* Discord Logs
* Timed Jobs
* Consumable foods/beverages/drinks/drugs (sandwich, water\_bottle, tosti, beer, vodka etc.)
* Removal of GTA's default weapons drops
* Drug effects
* Removal of GTA's default vehicle spawns (planes, helicopters, emergency vehicles etc.)
* Removal of GTA's default emergency service npc's
* Removal of GTA's default wanted system
* Useable binoculars
* Weapon draw animations (normal/holster)
* Ability to add teleport markers (from a place to another place)
* Taking hostage
* Pointing animation with finger (by pressing "B")
* Seatbelt and cruise control
* Useable parachute
* Useable armor
* Weapon recoil (specific to each weapon)
* Tackle
* Calm AI (adjusting npc aggressiveness)
* Race Harness
* Adjusting npc/vehicle/parked vehicle spawn rates
* Infinite ammo for fire extinguisher and petrol can
* Removal of GTA's default huds (weapon wheel, cash etc.)
* Fireworks
* Automatically engine on after entering vehicle
* Discord rich presence
* Crouch and prone
* AFK dection

## Configuration

### General

{% hint style="info" %}
If you wish to have default hud components like the crosshair you can find them labeled in client/hudcomponents.lua
{% endhint %}

```lua
Config.MaxWidth = 5.0
Config.MaxHeight = 5.0
Config.MaxLength = 5.0
Config.DamageNeeded = 100.0
Config.IdleCamera = true -- enable/disable idle camrea
Config.EnableProne = true -- enable/disable prone
Config.JointEffectTime = 60 -- how long does getting high affect the player?
Config.RemoveWeaponDrops = true -- enable/disable native weapon drops
Config.RemoveWeaponDropsTimer = 25
Config.DefaultPrice = 20 -- carwash
Config.DirtLevel = 0.1 -- carwash dirt level

Config.Teleports = {
    --Elevator @ labs
    [1] = {
        [1] = { --First location of the Teleport
            coords = vector4(3540.74, 3675.59, 20.99, 167.5),
            ["AllowVehicle"] = false, -- enable/disable vehicle
            drawText = '[E] Take Elevator Up' -- Drawtext label
        },
        [2] = { --Second location of the Teleport
            coords = vector4(3540.74, 3675.59, 28.11, 172.5),
            ["AllowVehicle"] = false,
            drawText = '[E] Take Elevator Down'
        },

    },
    [2] = { --New teleport 
        [1] = {
            coords = vector4(909.49, -1589.22, 30.51, 92.24),
            ["AllowVehicle"] = false,
            drawText = '[E] Enter Coke Processing'
        },
        [2] = {
            coords = vector4(1088.81, -3187.57, -38.99, 181.7),
            ["AllowVehicle"] = false,
            drawText = '[E] Leave'
        },
    },
}

Config.CarWash = { -- carwash
    [1] = {
        ["label"] = "Hands Free Carwash", -- map blip name
        ["coords"] = vector3(25.29, -1391.96, 29.33), -- map blip location
    },
    [2] = {
        ["label"] = "Hands Free Carwash",
        ["coords"] = vector3(174.18, -1736.66, 29.35),
    }
}
```

### Blacklist ped and vehicle models

```lua
Config.BlacklistedVehs = { -- these vehicles will delete themselves on spawn
    [`SHAMAL`] = true,
    [`LUXOR`] = true,
    [`LUXOR2`] = true,
    [`JET`] = true,
    [`LAZER`] = true,
    [`BUZZARD`] = true,
    [`BUZZARD2`] = true,
    [`ANNIHILATOR`] = true,
    [`SAVAGE`] = true,
    [`TITAN`] = true,
}

Config.BlacklistedPeds = { -- these NPCs will delete themslves on spawn
    [`s_m_y_ranger_01`] = true,
    [`s_m_y_sheriff_01`] = true,
    [`s_m_y_cop_01`] = true,
    [`s_f_y_sheriff_01`] = true,
    [`s_f_y_cop_01`] = true,
    [`s_m_y_hwaycop_01`] = true,
}
```

## **Consumables** <a href="#blob-path" id="blob-path"></a>

{% hint style="warning" %}
When adding new consumables you need to go into the server/consumables.lua and make that item useable with the `QBCore.Functions.CreateUseableItem` function more info on how to do that in [server-function-reference.md](../qb-core/server-function-reference.md "mention")&#x20;

You can also increase the thirst or hunger with ["itemname"] = math.random(-20, -10) or a single number, the only important thing is that the lower number is first
{% endhint %}

```lua
ConsumeablesEat = { -- how much hunger is relieved on use
    ["sandwich"] = math.random(35, 54), 
    ["tosti"] = math.random(40, 50),
    ["twerks_candy"] = math.random(35, 54),
    ["snikkel_candy"] = math.random(40, 50),
}

ConsumeablesDrink = { -- how much thirst is relieved on use
    ["water_bottle"] = math.random(35, 54),
    ["kurkakola"] = math.random(35, 54),
    ["coffee"] = math.random(40, 50),
}

ConsumeablesAlcohol = { -- how much thirst is relieved on use
    ["whiskey"] = math.random(20, 30),
    ["beer"] = math.random(30, 40),
    ["vodka"] = math.random(20, 40),
}
```

## Timed Jobs / Cron

{% hint style="info" %}
Timed jobs are used to execute code at a certain time every day. For example executing function x every monday when the clock is 08:20 AM etc.
{% endhint %}

### Usage (Server Exports):

- CreateTimedJob(hour: number, min: number, callback: function)
    > Used for registering the actual timed job. Returns the index of the timed job which can be used to force run or stop the timed job.<br>
    > **Example:**
    > ```lua
    > -- `idx` becomes the index of the timed job.
    >local idx = exports["qb-smallresources"]:CreateTimedJob(8, 20, function(day, hour, min)
    >	 if day == 1 then -- check if its monday
    >        print("Its currently 08:20 AM on a monday")
    >    end
    >end)
    > ```
    
- ForceRunTimedJob(idx: number)
    > Used to force run a timed job, even if the time isnt correct. Does not bypass local checks in the actual callback though.<br>
    > **Example:**
    > ```lua
    > exports["qb-smallresources"]:ForceRunTimedJob(2)
    > ```

- StopTimedJob(idx: number)
    > Stops the timed job forever (unless registered again).<br>
    > **Example:**
    > ```lua
    > exports["qb-smallresources"]:StopTimedJob(3)
    > ```

## Logs

{% hint style="info" %}
Logs are located on the server side to hide your webhooks form clients you can find them in the server/logs.lua if you don't know how to make discord webhooks click [here](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks)
{% endhint %}

```lua
local Webhooks = {
    ['default'] = '', --Discord webhooks get put here
    ['testwebhook'] = '',
    ['playermoney'] = '',
    ['playerinventory'] = '',
    ['robbing'] = '',
    ['cuffing'] = '',
    ['drop'] = '',
    ['trunk'] = '',
    ['stash'] = '',
    ['glovebox'] = '',
    ['banking'] = '',
    ['vehicleshop'] = '',
    ['vehicleupgrades'] = '',
    ['shops'] = '',
    ['dealers'] = '',
    ['storerobbery'] = '',
    ['bankrobbery'] = '',
    ['powerplants'] = '',
    ['death'] = '',
    ['joinleave'] = '',
    ['ooc'] = '',
    ['report'] = '',
    ['me'] = '',
    ['pmelding'] = '',
    ['112'] = '',
    ['bans'] = '',
    ['anticheat'] = '',
    ['weather'] = '',
    ['moneysafes'] = '',
    ['bennys'] = '',
    ['bossmenu'] = '',
    ['robbery'] = '',
    ['casino'] = '',
    ['traphouse'] = '',
    ['911'] = '',
    ['palert'] = '',
    ['house'] = '',
}

local Colors = { -- https://www.spycolor.com/
    ['default'] = 14423100,
    ['blue'] = 255,
    ['red'] = 16711680,
    ['green'] = 65280,
    ['white'] = 16777215,
    ['black'] = 0,
    ['orange'] = 16744192,
    ['yellow'] = 16776960,
    ['pink'] = 16761035,
    ["lightgreen"] = 65309,
}
```

### Example

Client

```lua
RegisterCommand('clientlogtest', function()
    TriggerServerEvent('qb-log:server:CreateLog', 'testwebhook', 'Test Webhook', 'default', 'Webhook Client Side setup successfully')
end)
```

Server

```lua
RegisterCommand('serverlogtest', function()
    TriggerEvent('qb-log:server:CreateLog', 'testwebhook', 'Test Webhook', 'default', 'Webhook Client Side setup successfully')
end
```

## Discord rich presence

{% hint style="info" %}
More documentation for this can be found [here](https://support.discord.com/hc/en-us/articles/115001557452-Game-Invites-and-Detailed-Status-Rich-Presence-). The configuration for this can be found in the client/discord.lua
{% endhint %}

```lua
CreateThread(function()
    while true do
        -- This is the Application ID (Replace this with you own)
	SetDiscordAppId()

        -- Here you will have to put the image name for the "large" icon.
	SetDiscordRichPresenceAsset('logo_name')
        
        -- (11-11-2018) New Natives:

        -- Here you can add hover text for the "large" icon.
        SetDiscordRichPresenceAssetText('This is a lage icon with text')
       
        -- Here you will have to put the image name for the "small" icon.
        SetDiscordRichPresenceAssetSmall('logo_name')

        -- Here you can add hover text for the "small" icon.
        SetDiscordRichPresenceAssetSmallText('This is a lsmall icon with text')

        QBCore.Functions.TriggerCallback('smallresources:server:GetCurrentPlayers', function(result)
            SetRichPresence('Players: '..result..'/64')
        end)

        -- (26-02-2021) New Native:

        --[[ 
            Here you can add buttons that will display in your Discord Status,
            First paramater is the button index (0 or 1), second is the title and 
            last is the url (this has to start with "fivem://connect/" or "https://") 
        ]]--
        SetDiscordRichPresenceAction(0, "First Button!", "fivem://connect/localhost:30120")
        SetDiscordRichPresenceAction(1, "Second Button!", "fivem://connect/localhost:30120")

        -- It updates every minute just in case.
	Wait(60000)
    end
end)
```

## Rockstar editor

### Commands

* /editor - Activates rockstar editor
* /record - Starts a recording
* /clip- Strarts to record a clip
* /saveclip - Saves the clip
* /delclip - Deletes clip

## Items

* vodka - Consumable
* beer - Consumable
* whiskey - Consumable
* sandwich - Consumable
* twerks\_candy - Consumable
* snikkel\_candy - Consumable
* tosti - Consumable
* water\_bottle - Consumable
* coffee - Consumable
* kurkakola - Consumable
* joint - Drug
* cokebaggy - Drug
* crack\_baggy - Drug
* xtcbaggy - Drug
* oxy - Drug
* meth - Drug
* armor - Gives armor on use
* heavyarmor - Gives armor on use
* binoculars - Useable binoculars to look far distances
* parachute - adds a parachute to the player allowing to deploy it in the air
* firework1 - Make things go boom&#x20;
* firework2 - More fireworks
* firework3 - So many fireworks
* firework4 - Looks nice&#x20;
* lockpick - The item used to trigger [qb-lockpick.md](qb-lockpick.md "mention")
* advancedlockpick - Another item used to trigger [qb-lockpick.md](qb-lockpick.md "mention")

## Commands

* /resetparachute - Returns parachute back to the player
* /resetarmor- Removes armor and gives heavyarmor back
