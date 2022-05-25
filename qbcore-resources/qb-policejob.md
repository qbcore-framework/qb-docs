---
description: Obey & survive!
---

# 👮 qb-policejob

## Introduction

* This resource manages police functions and interactions
* Objects for police to place down via [qb-radialmenu.md](qb-radialmenu.md "mention") such as traffic cones and spike strips
* Police stash, garage and armory
* Cuffing players functions
* Evidence system including blood DNA drops and fingerprints
* Anklet Tracker for police to track players&#x20;

## Configuration

### General

```lua
Config = {}
Config.LicenseRank = 2 -- minimum rank need to grant weapon licenses to players
Config.HandCuffItem = 'handcuffs' -- item name to check for when cuffing
Config.PoliceHelicopter = "POLMAV" -- helicopter model name to spawn
```

### Locations

```lua
Config.Locations = {
    ["duty"] = { -- locations to clock on/off duty
        [1] = vector3(440.085, -974.924, 30.689),
        [2] = vector3(-449.811, 6012.909, 31.815),
    },
    ["vehicle"] = { -- locations to withdraw vehicles
        [1] = vector4(448.159, -1017.41, 28.562, 90.654),
        [2] = vector4(471.13, -1024.05, 28.17, 274.5),
        [3] = vector4(-455.39, 6002.02, 31.34, 87.93),
    },
    ["stash"] = { -- locations to access stash
        [1] = vector3(453.075, -980.124, 30.889),
    },
    ["impound"] = { -- locations to access the police impound
        [1] = vector4(436.68, -1007.42, 27.32, 180.0),
        [2] = vector4(-436.14, 5982.63, 31.34, 136.0),
    },
    ["helicopter"] = { -- locations to withdraw helicopters
        [1] = vector4(449.168, -981.325, 43.691, 87.234),
        [2] = vector4(-475.43, 5988.353, 31.716, 31.34),
    },
    ["armory"] = { -- locations to open the armory
        [1] = vector3(462.23, -981.12, 30.68),
    },
    ["trash"] = { -- locations to add items to the trash
        [1] = vector3(439.0907, -976.746, 30.776),
    },
    ["fingerprint"] = { -- locations to access fingerprint scanner
        [1] = vector3(460.9667, -989.180, 24.92),
    },
    ["evidence"] = { -- locations to access evidence lockers
        [1] = vector3(442.1722, -996.067, 30.689),
        [2] = vector3(451.7031, -973.232, 30.689),
        [3] = vector3(455.1456, -985.462, 30.689),
    },
    ["stations"] = { -- locations for map blips and labels
        [1] = {
            label = "Police Station",
            coords = vector4(428.23, -984.28, 29.76, 3.5)
        },
        [2] = {
            label = "Prison",
            coords = vector4(1845.903, 2585.873, 45.672, 272.249)
        },
        [3] = {
            label = "Police Station Paleto",
            coords = vector4(-451.55, 6014.25, 31.716, 223.81)
        },
    },
}
```

### Armory

```lua
Config.Items = {
    label = "Police Armory", -- label that the right-side inventory shows
    slots = 30, -- how many slots total for the armory
    items = {
        [1] = {
            name = "weapon_pistol", -- item name
            price = 0, -- how much the item costs
            amount = 1, -- how many are available in stock
            info = { -- item info
                serie = "", -- placeholder for serial number, don't edit
                attachments = {
                    {
                        component = "COMPONENT_AT_PI_FLSH", -- attachment name
                        label = "Flashlight" -- attachment label
                    },
                }
            },
            type = "weapon", -- item type
            slot = 1, -- slot item shows in inventory
            authorizedJobGrades = {0, 1, 2, 3, 4} -- grades allowed to purchase
        }
    }
}
```

### Vehicles

```lua
Config.WhitelistedVehicles = {} -- list of vehicles not locked by rank

Config.AuthorizedVehicles = {
	-- Grade 0
	[0] = {
		["police"] = "Police Car 1", -- vehicle model and label for menu
		["police2"] = "Police Car 2",
		["police3"] = "Police Car 3",
		["police4"] = "Police Car 4",
		["policeb"] = "Police Car 5",
		["policet"] = "Police Car 6",
		["sheriff"] = "Sheriff Car 1",
		["sheriff2"] = "Sheriff Car 2",
	}
}
```

### Vehicle settings

```lua
Config.VehicleSettings = {
    ["car1"] = { -- Model name
        ["extras"] = {
            ["1"] = true, -- enable/disable the vehicle extra on spawn
            ["2"] = true,
            ["3"] = true,
            ["4"] = true,
            ["5"] = true,
            ["6"] = true,
            ["7"] = true,
            ["8"] = true,
            ["9"] = true,
            ["10"] = true,
            ["11"] = true,
            ["12"] = true,
            ["13"] = true,
        },
	["livery"] = 1, -- the livery number to be applied on spawn
    }
}
```

### Vehicle trunk items

```lua
Config.CarItems = { -- items to add to the trunk when spawning a police vehicle
    [1] = {
        name = "heavyarmor", -- item name
        amount = 2, -- item amount
        info = {}, -- item info
        type = "item", -- type of item
        slot = 1, -- inventory slot item shows in
    },
    [2] = {
        name = "empty_evidence_bag",
        amount = 10,
        info = {},
        type = "item",
        slot = 2,
    },
    [3] = {
        name = "police_stormram",
        amount = 1,
        info = {},
        type = "item",
        slot = 3,
    },
}
```

### Objects

```lua
Config.MaxSpikes = 5 -- maximum amount of spikes that can be spawned at once

Config.Objects = { -- availabe items for police to spawn
    ["cone"] = { -- https://gta-objects.xyz/
        model = `prop_roadcone02a`, -- object hash
        freeze = false -- enable/disable freezing the object in place
    },
    ["barrier"] = {
        model = `prop_barrier_work06a`,
        freeze = true
    },
    ["roadsign"] = {
        model = `prop_snow_sign_road_06g`,
        freeze = true
    },
    ["tent"] = {
        model = `prop_gazebo_03`,
        freeze = true
    },
    ["light"] = {
        model = `prop_worklight_03b`,
        freeze = true
    },
}
```

### Security cameras

```lua
Config.SecurityCameras = {
    hideradar = false, -- enable/disable hiding the minimap while viewing cam
    cameras = {
        [1] = {
            label = "Pacific Bank CAM#1", -- camera label
            coords = vector3(257.45, 210.07, 109.08), -- location of the camera
            r = {x = -25.0, y = 0.0, z = 28.05}, -- camera rotation
            canRotate = false, -- enable/disable rotating the cam while viewing
            isOnline = true -- enable/disable the camera
        }
    }
}
```

### Police radars

```lua
Config.Radars = { -- locations of radars that check for flagged plates
	vector4(-623.44421386719, -823.08361816406, 25.25704574585, 145.0),
	vector4(-652.44421386719, -854.08361816406, 24.55704574585, 325.0),
	vector4(1623.0114746094, 1068.9924316406, 80.903594970703, 84.0),
	vector4(-2604.8994140625, 2996.3391113281, 27.528566360474, 175.0),
	vector4(2136.65234375, -591.81469726563, 94.272926330566, 318.0),
	vector4(2117.5764160156, -558.51013183594, 95.683128356934, 158.0),
	vector4(406.89505004883, -969.06286621094, 29.436267852783, 33.0),
	vector4(657.315, -218.819, 44.06, 320.0),
	vector4(2118.287, 6040.027, 50.928, 172.0),
	vector4(-106.304, -1127.5530, 30.778, 230.0),
	vector4(-823.3688, -1146.980, 8.0, 300.0),
}
```

### Evidence

```lua
Config.AmmoLabels = { -- the type of ammo and it's label when dropped
    ["AMMO_PISTOL"] = "9x19mm parabellum bullet",
    ["AMMO_SMG"] = "9x19mm parabellum bullet",
    ["AMMO_RIFLE"] = "7.62x39mm bullet",
    ["AMMO_MG"] = "7.92x57mm mauser bullet",
    ["AMMO_SHOTGUN"] = "12-gauge bullet",
    ["AMMO_SNIPER"] = "Large caliber bullet",
}
```

## Evidence system

* Random drop chance of bullet casings when player is shooting
* Random chance of fingerprints left behind when player is not wearing gloves
* Player statuses set when doing certain actions

### Configuration

* Found in qb-policejob/client/evidence.lua

```lua
local StatusList = { -- set a players status using an event
    ['fight'] = Lang:t('evidence.red_hands'),
    ['widepupils'] = Lang:t('evidence.wide_pupils'),
    ['redeyes'] = Lang:t('evidence.red_eyes'),
    ['weedsmell'] = Lang:t('evidence.weed_smell'),
    ['gunpowder'] = Lang:t('evidence.gunpowder'),
    ['chemicals'] = Lang:t('evidence.chemicals'),
    ['heavybreath'] = Lang:t('evidence.heavy_breathing'),
    ['sweat'] = Lang:t('evidence.sweat'),
    ['handbleed'] = Lang:t('evidence.handbleed'),
    ['confused'] = Lang:t('evidence.confused'),
    ['alcohol'] = Lang:t('evidence.alcohol'),
    ["heavyalcohol"] = Lang:t('evidence.heavy_alcohol'),
    ["agitated"] = Lang:t('evidence.agitated')
}

local WhitelistedWeapons = { -- weapons to ignore
    `weapon_unarmed`,
    `weapon_snowball`,
    `weapon_stungun`,
    `weapon_petrolcan`,
    `weapon_hazardcan`,
    `weapon_fireextinguisher`
}
```

### Usage example

{% hint style="warning" %}
Example code is done on the SERVER side
{% endhint %}

#### Setting statuses

```lua
RegisterCommand('setstatus', function(source, args)
    local status = args[1] -- the status type to set
    local time = args[2] -- the status duration
    TriggerClientEvent('evidence:client:SetStatus', source, status, time)
end)
```

#### Adding blood drop

```lua
RegisterCommand('addblooddrop', function(source, args)
    local ped = GetPlayerPed(source)
    local coords = GetEntityCoords(ped)
    local bloodId = args[1] -- blood id or index of table, can be whatever
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local citizenid = Player.PlayerData.citizenid
    local bloodtype = Player.PlayerData.metadata['bloodtype']
    TriggerClientEvent('evidence:client:AddBlooddrop', source, bloodId, citizenid, bloodtype, coords)
end)
```

#### Adding fingerprint drop

```lua
RegisterCommand('addfingerprint', function(source, args)
    local ped = GetPlayerPed(source)
    local coords = GetEntityCoords(ped)
    local fingerId = args[1] -- fingerprint id or index of table, can be whatever
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local fingerprint = Player.PlayerData.metadata['fingerprint']
    TriggerClientEvent('evidence:client:AddFingerPrint', source, fingerId, fingerprint, coords)
end)
```

## Commands

* /spikestrip - Places a spike strip on the ground punctures any tires that run over it
* /grantlicense - Grants said license to a player I.E weapon/driving
* /revokelicense - Revokes said license to a player I.E weapon/driving
* /pobject - Places object on the floor IE cone/tent
* /cuff - Hard cuffs the nearest player freezes them in place
* /escort  - Attaches the nearest player to the player that uses this command
* /callsign - Assigns player with a call sign on use
* /clearcasings - Clears all the casings in the nearby area&#x20;
* /jail - Sends a player to jail for a specific amount of time
* /unjail - Release a player from jail
* /clearblood - Clears all the blood drops in the nearby area
* /seizecash - Seizes a players cash
* /sc - Soft cuffs the nearest player allowing them to move freely but they are still cuffed&#x20;
* /flagplate - Flags a plate for a reason the user inputs
* /unflagplate - Remove a flagged plate&#x20;
* /plateinfo - Checks to see if a plate is flagged more not
* /depot - Impounds a vehicle for a price
* /impound - Impounds a vehicle&#x20;
* /paytow - Pays a tow truck driver
* /paylawyer - Pays a lawyer
* /anklet - Attaches anklet to the nearest player
* /ankletlocation - Gives the user the location of a target player if they are wearing an anklet
* /takedrivinglicense - Revokes driving license from a player
* /takedna - Fills a "empty\_evidence\_bag" with targets dna
* /911p - Calls the police

## Items

* handcuffs - Cuffs a player on use
