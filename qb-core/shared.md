---
description: Learn how to manage your server's jobs, vehicles, items, etc!
---

# 📜 Shared

## Introduction

* The shared file inside qb-core contains all the information for your jobs, vehicles, items & more! You will spend a lot of time in this file configuring everything to your exact specifications. Jenkins hashes are used frequently, you can find more information on those [here](https://cookbook.fivem.net/2019/06/23/lua-support-for-compile-time-jenkins-hashes/)

{% hint style="success" %}
QBCore uses lua tables to store static information instead of a database to prevent needing to execute queries. When you combine this with the ability to use [shared-exports.md](shared-exports.md "mention") it can be a very powerful tool!
{% endhint %}

### Utility

* Found in qb-core/shared/main.lua

```lua
QBShared = QBShared or {}

local StringCharset = {}
local NumberCharset = {}

for i = 48,  57 do NumberCharset[#NumberCharset+1] = string.char(i) end
for i = 65,  90 do StringCharset[#StringCharset+1] = string.char(i) end
for i = 97, 122 do StringCharset[#StringCharset+1] = string.char(i) end

function QBShared.RandomStr(length)
    if length <= 0 then return '' end
    return QBShared.RandomStr(length - 1) .. StringCharset[math.random(1, #StringCharset)]
end

function QBShared.RandomInt(length)
    if length <= 0 then return '' end
    return QBShared.RandomInt(length - 1) .. NumberCharset[math.random(1, #NumberCharset)]
end

function QBShared.SplitStr(str, delimiter)
    local result = {}
    local from = 1
    local delim_from, delim_to = string.find(str, delimiter, from)
    while delim_from do
		result[#result+1] = string.sub(str, from, delim_from - 1)
        from = delim_to + 1
        delim_from, delim_to = string.find(str, delimiter, from)
    end
	result[#result+1] = string.sub(str, from)
    return result
end

function QBShared.Trim(value)
	if not value then return nil end
    return (string.gsub(value, '^%s*(.-)%s*$', '%1'))
end

function QBShared.Round(value, numDecimalPlaces)
    if not numDecimalPlaces then return math.floor(value + 0.5) end
    local power = 10 ^ numDecimalPlaces
    return math.floor((value * power) + 0.5) / (power)
end

function QBShared.ChangeVehicleExtra(vehicle, extra, enable)
	if DoesExtraExist(vehicle, extra) then
		if enable then
			SetVehicleExtra(vehicle, extra, false)
			if not IsVehicleExtraTurnedOn(vehicle, extra) then
				QBShared.ChangeVehicleExtra(vehicle, extra, enable)
			end
		else
			SetVehicleExtra(vehicle, extra, true)
			if IsVehicleExtraTurnedOn(vehicle, extra) then
				QBShared.ChangeVehicleExtra(vehicle, extra, enable)
			end
		end
	end
end

function QBShared.SetDefaultVehicleExtras(vehicle, config)
    -- Clear Extras
    for i = 1,20 do
        if DoesExtraExist(vehicle, i) then
            SetVehicleExtra(vehicle, i, 1)
        end
    end

    for id, enabled in pairs(config) do
        QBShared.ChangeVehicleExtra(vehicle, tonumber(id), type(enabled) == 'boolean' and enabled or true)
    end
end

QBShared.StarterItems = {
    ['phone'] = { amount = 1, item = 'phone' },
    ['id_card'] = { amount = 1, item = 'id_card' },
    ['driver_license'] = { amount = 1, item = 'driver_license' },
}
```

### Items

* Found in qb-core/shared/items.lua

```lua
QBShared.Items = {
    ['id_card'] = {
        ['name'] = 'id_card', -- Actual item name for spawning/giving/removing
        ['label'] = 'ID Card', -- Label of item that is shown in inventory slot
        ['weight'] = 0, -- How much the items weighs
        ['type'] = 'item', -- What type the item is (ex: item, weapon)
        ['image'] = 'id_card.png', -- This item image that is found in qb-inventory/html/images (must be same name as ['name'] from above)
        ['unique'] = true, -- Is the item unique (true|false) - Cannot be stacked & accepts item info to be assigned
        ['useable'] = true, -- Is the item useable (true|false) - Must still be registered as useable
        ['shouldClose'] = false, -- Should the item close the inventory on use (true|false)
        ['combinable'] = nil, -- Is the item able to be combined with another? (nil|table)
        ['description'] = 'A card containing all your information to identify yourself' -- Description of time in inventory
    }
}

-- Example of an item that is combinable and not nil

['combinable'] = {
    accept = {'snspistol_part_1'}, -- The other item that can be it can be combined with
    reward = 'snspistol_stage_1', -- The item that is rewarded upon successful combine
    anim = { -- Set the animation, progressbar text and length of time it takes to combine
        ['dict'] = 'anim@amb@business@weed@weed_inspecting_high_dry@', -- The animation dictionary
        ['lib'] = 'weed_inspecting_high_base_inspector', -- The animation library
        ['text'] = 'Atttaching attachments', -- Text that will be displayed in the progress bar
        ['timeOut'] = 15000,} -- How long the animation should take to complete
    }
}
```

### Jobs

* Found in qb-core/shared/jobs.lua

```lua
QBShared.ForceJobDefaultDutyAtLogin = true -- true: Force duty state to jobdefaultDuty | false: set duty state from database last saved
QBShared.Jobs = {
    ['unemployed'] = { -- job name (string)
        label = 'Civilian', -- job label (string)
        defaultDuty = true, -- enable/disable player being auto clocked-in (bool)
        grades = {
            ['0'] = { -- job grade (string)
                name = 'Freelancer', -- job grade name (string)
                payment = 10 -- paycheck amount (number)
            },
        },
    },
    ['police'] = {
        label = 'Law Enforcement',
        defaultDuty = true,
        grades = {
            ['0'] = {
                name = 'Recruit',
                payment = 50
            },
            ['1'] = {
                name = 'Officer',
                payment = 75
            },
            ['2'] = {
                name = 'Sergeant',
                payment = 100
            },
            ['3'] = {
                name = 'Lieutenant',
                payment = 125
            },
            ['4'] = {
                name = 'Chief',
                isboss = true, -- set this grade as a boss to access boss menu
                payment = 150
            },
        },
    },
}
```

### Vehicles

* Found in qb-core/shared/vehicles.lua

```lua
QBShared.Vehicles = {
    ['adder'] = { -- Vehicle model/spawn name (string)
        ['name'] = 'Adder', -- Desired name/label for the vehicle (string)
        ['brand'] = 'Truffade', -- The brand of vehicle (string)
        ['model'] = 'adder', -- Vehicle model/spawn name (string)
        ['price'] = 280000, -- How much the vehicle costs at the dealership (number)
        ['category'] = 'super', -- The category the vehicle will display in at the dealership (string)
        ['hash'] = `adder`, -- Vehicle hash key (jenkins hash || GetHashKey(model))
        ['shop'] = 'pdm', -- The desired shop the vehicle is available for sale at (string)
    }
}
```

### Gangs

* Found in qb-core/shared/gangs.lua

```lua
QBShared.Gangs = {
    ['mynewgang'] = { -- grade name (string)
        label = 'My Fancy Gang Name', -- Label of the gang (string)
        grades = {
            ['0'] = { -- grade (number)
                name = 'I am grade 0'
            },
            ['1'] = {
                name = 'I am grade 1' -- Label of the gang grade (string)
            },
            ['2'] = {
                name = 'I am grade 2'
            },
            ['3'] = {
                name = 'I am grade 3',
                isboss = true -- set this grade as a boss to access gang menu
            },
        },
    }
}
```

### Weapons

* Found in qb-core/shared/weapons.lua

{% hint style="warning" %}
Weapons are added in shared/items.lua as well!
{% endhint %}

```lua
QBShared.Weapons = {
    [`weapon_pistol`] = { -- Weapon hash (uses compile-time Jenkins hashes - See link at bottom of page)
        ['name'] = 'weapon_pistol', -- Actual item name for spawning/giving/removing
        ['label'] = 'Walther P99', -- Label of item that is shown in inventory slot
        ['weight'] = 1000, -- How much the items weighs
        ['type'] = 'weapon', -- What type the item is (ex: item, weapon)
        ['ammotype'] = 'AMMO_PISTOL', -- The type of ammo this weapon accepts
        ['image'] = 'weapon_pistol.png', -- This item image that is found in qb-inventory/html/images (must be same name as ['name'] from above)
        ['unique'] = true, -- Is the item unique (true|false) - Cannot be stacked & accepts item info to be assigned
        ['useable'] = false, -- Is the item useable (true|false) - Must still be registered as useable
        ['description'] = 'A small firearm designed to be held in one hand' -- Description of time in inventory
    }
}
```
