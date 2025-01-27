---
description: Learn how to manage your server's jobs, vehicles, items, etc!
---

# 📜 Shared

## Introduction

* The shared folder inside qb-core contains all the information for your jobs, vehicles, items & more! You will spend a lot of time in this folder configuring everything to your exact specifications. Jenkins hashes are used frequently, you can find more information on those [here](https://cookbook.fivem.net/2019/06/23/lua-support-for-compile-time-jenkins-hashes/)

{% hint style="success" %}
QBCore uses Lua tables for storing static information instead of relying on a database. This avoids the need for frequent database queries, resulting in faster operations. Combined with [shared-exports.md](shared-exports.md "mention") it can be a very powerful tool!
{% endhint %}

### Utility

* Found in `qb-core/shared/main.lua`

#### Starting Items

Starter items are predefined items that a player receives when joining the server for the first time

* item\_name: `string`
* amount: `number`

```lua
QBShared.StarterItems = {
    phone = 1,
    id_card = 1,
    driver_license = 1,
}
```

Example Usage:

```lua
for item, amount in pairs(QBCore.Shared.StarterItems) do
    local item_info = QCore.Shared.Items[item]
    print('Received '..amount..' '..item_info.label)
end
```

#### Generate a Random String

Generates a random string of a specified length

```lua
QBShared.RandomStr(length)
```

* length: `number`
* <mark style="color:yellow;">returns</mark>: `string`

Example Usage:

```lua
local randomString = QBCore.Shared.RandomStr(8)
print(randomString) -- Example Output: "aBcD1234"
```

#### Generate a Random Integer String

Generates a random numeric string of a specified length

```lua
QBShared.RandomInt(length)
```

* length: `number`
* <mark style="color:yellow;">returns</mark>: `string`

Example Usage:

```lua
local randomInt = QBCore.Shared.RandomInt(6)
print(randomInt) -- Example Output: "473829"
```

#### Split a String

Splits a string into parts based on a delimiter

```lua
QBShared.SplitStr(str, delimiter)
```

* str: `string` - The string to split
* delimiter: `string` - The character or sequence used to split the string
* <mark style="color:yellow;">returns</mark>: `table`

Example Usage:

```lua
local result = QBCore.Shared.SplitStr("apple,banana,orange", ",")
-- Result: { "apple", "banana", "orange" }
```

#### Trim WhiteSpace

Removes leading and trailing whitespace from a string

```lua
QBShared.Trim(value)
```

* value: `string` - The string to trim
* <mark style="color:yellow;">returns</mark>: `string`

Example Usage:

```lua
local trimmed = QBCore.Shared.Trim("   Hello World!   ")
print(trimmed) -- Output: "Hello World!"
```

#### Round a Number

Rounds a number to the nearest whole number or to a specified number of decimal places

```lua
QBShared.Round(value, numDecimalPlaces)
```

* value: `number` - The number to round
* numDecimalPlaces (optional): `number` - The number of decimal places to round to
* <mark style="color:yellow;">returns</mark>: `number`

Example Usage:

```lua
local roundedValue = QBCore.Shared.Round(5.6789, 2)
print(roundedValue) -- Output: 5.68
```

#### Change Vehicle Extra

Toggles an extra on a vehicle

```lua
QBShared.ChangeVehicleExtra(vehicle, extra, enable)
```

* vehicle: `number` - The vehicle entity
* extra: `number` - The extra ID
* enable: `boolean` - Whether to enable/disable the extra

Example Usage:

```lua
QBCore.Shared.ChangeVehicleExtra(vehicle, 1, true)
```

#### Set Default Vehicle Extras

Resets all extras on a vehicle and applies a specified configuration

```lua
QBShared.SetDefaultVehicleExtras(vehicle, config)
```

* vehicle: `number` - The vehicle entity
* config: `table` - A table defining which extras to enable/disable

Example Usage:

```lua
local config = {
    [1] = true, -- Enable extra 1
    [2] = false, -- Disable extra 2
    [3] = true -- Enable extra 3
}
QBCore.Shared.SetDefaultVehicleExtras(vehicle, config)
```

### Items

* Found in `qb-core/shared/items.lua`

The `Items` table in **qb-core** defines all the items available in your server. Each item is represented as an object with several properties that determine its behavior, appearance, and functionality.

| Property      | Type      | Description                                                             |
| ------------- | --------- | ----------------------------------------------------------------------- |
| `name`        | `string`  | The internal name used for spawning, giving, or removing the item.      |
| `label`       | `string`  | The display name shown in the inventory.                                |
| `weight`      | `number`  | The weight of the item, affecting inventory capacity.                   |
| `type`        | `string`  | The type of item (e.g., `item`, `weapon`).                              |
| `image`       | `string`  | The filename of the item's image located in `qb-inventory/html/images`. |
| `unique`      | `boolean` | Whether the item is unique (`true`) or stackable (`false`).             |
| `useable`     | `boolean` | Whether the item is usable. Must still be registered as a usable item.  |
| `shouldClose` | `boolean` | Whether using the item closes the inventory (`true` or `false`).        |
| `combinable`  | \`nil     | table\`                                                                 |
| `description` | `string`  | A short description of the item shown in the inventory.                 |

**Example: Basic Item Definition**

```lua
QBShared.Items = {
    id_card = {
        name = 'id_card', -- Internal name
        label = 'ID Card', -- Display name in inventory
        weight = 0, -- Item weight
        type = 'item', -- Type of item (e.g., item, weapon)
        image = 'id_card.png', -- Item image filename
        unique = true, -- Is the item unique?
        useable = true, -- Can the item be used?
        shouldClose = false, -- Does it close the inventory on use?
        combinable = nil, -- Is the item combinable? (nil means not combinable)
        description = 'A card containing all your information to identify yourself' -- Description
    }
}
```

**Example: Combinable Item Definition**

```lua
combinable = {
    accept = {'snspistol_part_1'}, -- The item(s) it can be combined with
    reward = 'snspistol_stage_1', -- The item received upon successful combination
    anim = { -- Animation, progress bar text, and duration for the combine action
        dict = 'anim@amb@business@weed@weed_inspecting_high_dry@', -- Animation dictionary
        lib = 'weed_inspecting_high_base_inspector', -- Animation library
        text = 'Attaching attachments', -- Progress bar text
        timeOut = 15000, -- Duration (in milliseconds) of the combine animation
    }
}
```

### Jobs

* Found in `qb-core/shared/jobs.lua`

The `Jobs` table in **qb-core** defines all the jobs available on your server, including their ranks, salaries, and specific features. This allows you to manage employment roles, responsibilities, and pay structures effectively.

**Example: Global Setting**

The global setting determines if the duty state should default to the `defaultDuty` setting of the job upon login or persist based on the last saved state in the database:

```lua
QBShared.ForceJobDefaultDutyAtLogin = true -- true: Use job's defaultDuty | false: Use last saved duty state from database
```

***

**Job Object Layout**

| Property      | Type      | Description                                                                                |
| ------------- | --------- | ------------------------------------------------------------------------------------------ |
| `label`       | `string`  | The display name of the job.                                                               |
| `type`        | `string`  | The type of job (e.g., `leo` for law enforcement officer).                                 |
| `defaultDuty` | `boolean` | Whether the player is automatically on duty when they log in.                              |
| `offDutyPay`  | `boolean` | Whether the player receives a paycheck while off duty.                                     |
| `grades`      | `table`   | A table defining job grades, including names, payment, and other rank-specific attributes. |

**Grades Table Layout**

| Property  | Type      | Description                                                           |
| --------- | --------- | --------------------------------------------------------------------- |
| `name`    | `string`  | The name of the grade (e.g., Recruit, Officer).                       |
| `payment` | `number`  | The salary for this grade.                                            |
| `isboss`  | `boolean` | (Optional) If `true`, this grade is marked as the boss (e.g., Chief). |

**Example: Basic Job Definition**

This example defines the unemployed job with a single grade:

```lua
QBShared.Jobs = {
    unemployed = {
        label = 'Civilian', -- Display name
        defaultDuty = true, -- Automatically on duty at login
        offDutyPay = false, -- No payment while off duty
        grades = {
            { name = 'Freelancer', payment = 10 } -- Single grade with payment
        }
    }
}
```

**Example: Advanced Job Definition**

This example defines the police job with multiple grades, each with specific attributes:

```lua
QBShared.Jobs = {
    police = {
        label = 'Law Enforcement', -- Display name
        type = 'leo', -- Job type (e.g., law enforcement)
        defaultDuty = true, -- Automatically on duty at login
        offDutyPay = false, -- No payment while off duty
        grades = {
            { name = 'Recruit',    payment = 50 },  -- Rank 1: Recruit with $50 payment
            { name = 'Officer',    payment = 75 },  -- Rank 2: Officer with $75 payment
            { name = 'Sergeant',   payment = 100 }, -- Rank 3: Sergeant with $100 payment
            { name = 'Lieutenant', payment = 125 }, -- Rank 4: Lieutenant with $125 payment
            { name = 'Chief',      isboss = true, payment = 150 }, -- Rank 5: Chief, marked as boss, with $150 payment
        }
    }
}
```

### Gangs

* Found in `qb-core/shared/gangs.lua`

The `Gangs` table in **qb-core** defines all the gangs available on your server, including their ranks, salaries, and specific features. This allows you to manage member roles, responsibilities, and pay structures effectively.

***

**Gang Object Layout**

| Property | Type     | Description                                                                       |
| -------- | -------- | --------------------------------------------------------------------------------- |
| `label`  | `string` | The display name of the gang                                                      |
| `grades` | `table`  | A table defining gang grades, including names and other rank-specific attributes. |

**Grades Table Layout**

| Property | Type      | Description                                                          |
| -------- | --------- | -------------------------------------------------------------------- |
| `name`   | `string`  | The name of the grade (e.g., Recruit, Enforcer).                     |
| `isboss` | `boolean` | (Optional) If `true`, this grade is marked as the boss (e.g., Boss). |

**Example: Basic Gang Definition**

This example defines the unemployed gang with a single grade:

```lua
QBShared.Gangs = {
    none = {
        label = 'No Gang', -- Display name
        grades = {
            { name = 'Unaffiliated' } -- Single grade
        }
    }
}
```

**Example: Advanced Gang Definition**

This example defines the lost mc gang with multiple grades, each with specific attributes:

```lua
QBShared.Gangs = {
    lostmc = {
        label = 'The Lost MC', -- Display name
        grades = {
            { name = 'Recruit' }, -- Rank 1
            { name = 'Enforcer' }, -- Rank 2
            { name = 'Shot Caller' }, -- Rank 3
            { name = 'Boss', isboss = true }, -- Rank 4 marked as boss
        },
    },
}
```

### Vehicles

{% hint style="danger" %}
If you want to save a vehicle to the database for ownership, it MUST be defined in the shared vehicles table!
{% endhint %}

* Found in `qb-core/shared/vehicles.lua`

The `Vehicles` table in **qb-core** defines all the vehicles available on your server, including their properties and categories. This table allows you to configure specific attributes for each vehicle to control how they behave in-game.

| Property   | Type              | Description                                                                                                                          |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `model`    | `string`          | The spawn code of the vehicle (must match the model name in the game).                                                               |
| `name`     | `string`          | The display name of the vehicle shown to players.                                                                                    |
| `brand`    | `string`          | The brand or manufacturer of the vehicle (e.g., "Maxwell", "Karin").                                                                 |
| `price`    | `number`          | The price of the vehicle in in-game currency.                                                                                        |
| `category` | `string`          | The category of the vehicle (e.g., "compacts", "sports"). Use [GetVehicleClass](https://docs.fivem.net/natives/?_0x29439776AAA00A62) |
| `type`     | `string`          | The type of vehicle (e.g., "automobile", "bike"). Refer to [Vehicle Types](https://docs.fivem.net/natives/?_0x6AE51D4B)              |
| `shop`     | `string \| table` | The shop(s) where the vehicle is available. Can be a single shop (e.g., "pdm") or multiple shops as a table                          |

```lua
QBShared.Vehicles = {
    {
        model = 'asbo',        -- This has to match the spawn code of the vehicle
        name = 'Asbo',         -- This is the display of the vehicle
        brand = 'Maxwell',     -- This is the vehicle's brand
        price = 4000,          -- The price that the vehicle sells for
        category = 'compacts', -- Category of the vehilce, stick with GetVehicleClass() options https://docs.fivem.net/natives/?_0x29439776AAA00A62
        type = 'automobile',   -- Vehicle type, refer here https://docs.fivem.net/natives/?_0x6AE51D4B & here https://docs.fivem.net/natives/?_0xA273060E
        shop = 'pdm',          -- Can be a single shop or multiple shops. For multiple shops for example {'shopname1','shopname2','shopname3'}
    }
}
```

### Weapons

{% hint style="warning" %}
Weapons are added in shared/items.lua as well to use as items! This table is only for looking up weapon information via it's hash which is returned via [GetCurrentPedWeapon](https://docs.fivem.net/natives/?_0xB0237302) or similar native function that returns the weapons hash
{% endhint %}

* Found in `qb-core/shared/weapons.lua`

The `Weapons` table in **qb-core** defines all the weapons available on your server. It includes attributes like the weapon's name, label, type, ammo type, and a damage reason for death notifications. This table allows you to manage and customize the weapons players can access.

**Weapon Object Layout**

| Property       | Type     | Description                                                                               |
| -------------- | -------- | ----------------------------------------------------------------------------------------- |
| `name`         | `string` | The internal spawn name of the weapon (e.g., `weapon_pistol`).                            |
| `label`        | `string` | The display name of the weapon shown to players.                                          |
| `weapontype`   | `string` | The type of weapon (e.g., "Pistol", "Shotgun", "Rifle").                                  |
| `ammotype`     | `string` | The type of ammo the weapon uses (e.g., `AMMO_PISTOL`, `AMMO_SHOTGUN`).                   |
| `damagereason` | `string` | A customizable message that appears in kill notifications to describe the cause of death. |

```lua
QBShared.Weapons = {
    [`weapon_pistol`] = { -- Weapon hash (uses compile-time Jenkins hashes)
        name = 'weapon_pistol', -- The internal spawn name of the weapon (e.g., weapon_pistol)
        label = 'Walther P99', -- The display name of the weapon shown to players
        weapontype = 'Pistol', -- The type of weapon (e.g., "Pistol", "Shotgun", "Rifle")
        ammotype = 'AMMO_PISTOL', -- The type of ammo the weapon uses (e.g., AMMO_PISTOL, AMMO_SHOTGUN)
        damageReason = 'Pistoled / Blasted / Plugged / Bust a cap in' -- A customizable message that appears in kill notifications to describe the cause of death
    }
}
```
