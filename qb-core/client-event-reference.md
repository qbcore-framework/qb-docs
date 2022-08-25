---
description: Learn about and how to use common core client events!
---

# 🎮 Client Event Reference

### QBCore:Client:OnPlayerLoaded

* Handles the player loading in after character selection

{% hint style="success" %}
This event can be used as an event handler to trigger code because it signifies the player has successfully loaded into the server!
{% endhint %}

```lua
RegisterNetEvent('QBCore:Client:OnPlayerLoaded', function()
    print('Im a client and i just loaded into your server!')
end)
```

### QBCore:Client:OnPlayerUnload

* Handles the player login out to character selection

{% hint style="success" %}
This event can be used as an event handler to trigger code because it signifies the player has successfully unloaded or logged out of the server!
{% endhint %}

```lua
RegisterNetEvent('QBCore:Client:OnPlayerUnload', function()
    print('Im a client and i just logged out of your server!')
end)
```

### QBCore:Client:PvpHasToggled

{% hint style="info" %}
On player load this event checks is triggered after checking the qb-core config to see if PVP should be enabled or disabled
{% endhint %}

```lua
RegisterNetEvent('QBCore:Client:PvpHasToggled', function(pvp_state)
    print('PVP mode has been set to '..pvp_state..'!')
end)
```

### QBCore:Command:SpawnVehicle

|   Arguments   |  Type  | Required | Default |
| :-----------: | :----: | :------: | :-----: |
| vehicle model | string |    yes   |   none  |

{% hint style="info" %}
Client example
{% endhint %}

```lua
-- /spawnveh adder

RegisterCommand('spawnveh', function(_, args)
    local vehicle = QBCore.Shared.Trim(args[1])
    TriggerEvent('QBCore:Command:SpawnVehicle', vehicle)
end)
```

{% hint style="info" %}
Server example
{% endhint %}

```lua
-- /spawnveh adder

RegisterCommand('spawnveh', function(source, args)
    local vehicle = QBCore.Shared.Trim(args[1])
    TriggerClientEvent('QBCore:Command:SpawnVehicle', source, vehicle)
end)
```

### QBCore:Command:DeleteVehicle

| Arguments | Type | Required | Default |
| :-------: | :--: | :------: | :-----: |
|    none   | none |    no    |   none  |

{% hint style="info" %}
Client example
{% endhint %}

```lua
RegisterCommand('deleteveh', function(_, args)
    TriggerEvent('QBCore:Command:DeleteVehicle')
end)
```

{% hint style="info" %}
Server example
{% endhint %}

```lua
RegisterCommand('deleteveh', function(source, args)
    TriggerClientEvent('QBCore:Command:DeleteVehicle', source)
end)
```

### QBCore:Player:SetPlayerData

{% hint style="success" %}
This event can be used as an event handler to trigger code because it indicates that the players data has changed!
{% endhint %}

```lua
RegisterNetEvent('QBCore:Player:SetPlayerData', function(val)
    PlayerData = val
    print(QBCore.Debug(PlayerData))
end)
```

### QBCore:Notify

| Arguments |       Type      | Required |    Default    |
| :-------: | :-------------: | :------: | :-----------: |
|  message  | string \| table |    yes   | 'Placeholder' |
|    type   |      string     |    yes   |   'primary'   |
|   length  |      number     |    yes   |      5000     |

{% hint style="info" %}
Client example
{% endhint %}

```lua
-- /testnotify This is my message, primary, 5000

RegisterCommand('testnotify', function(_, args)
    local message = {}
    for i=1, #args do
        message[#message + 1] = args[i]
        if string.match(args[i], ',') then
            local text = table.concat(message, ' '):gsub(",", "")
            local type = args[i + 1]:gsub(",", "")
            local length = args[i + 2]
            TriggerEvent('QBCore:Notify', text, type, length)
            break
        end
    end
end)

-- Using QBCore's shared functions!

RegisterCommand('testnotify', function(_, args)
    local message = QBCore.Shared.SplitStr(table.concat(args, ' '), ",")
    local text = message[1]
    local type = QBCore.Shared.Trim(message[2])
    local length = tonumber(message[3])
    TriggerEvent('QBCore:Notify', text, type, length)
end)
```

{% hint style="info" %}
Server example
{% endhint %}

```lua
-- /testnotify This is my message, primary, 5000

RegisterCommand('testnotify', function(source, args)
    local message = {}
    for i=1, #args do
        message[#message + 1] = args[i]
        if string.match(args[i], ',') then
            local text = table.concat(message, ' '):gsub(",", "")
            local type = args[i + 1]:gsub(",", "")
            local length = args[i + 2]
            TriggerClientEvent('QBCore:Notify', source, text, type, length)
            break
        end
    end
end)

-- Using QBCore's shared functions!

RegisterCommand('testnotify', function(source, args)
    local message = QBCore.Shared.SplitStr(table.concat(args, ' '), ",")
    local text = message[1]
    local type = QBCore.Shared.Trim(message[2])
    local length = tonumber(message[3])
    TriggerClientEvent('QBCore:Notify', source, text, type, length)
end)
```

### QBCore:Client:UseItem

| Arguments |  Type  | Required | Default |
| :-------: | :----: | :------: | :-----: |
| item name | string |    yes   |   none  |

{% hint style="info" %}
Client example (must have the item in your inventory)
{% endhint %}

```lua
-- /useitem sandwich 1

RegisterCommand('useitem', function(_, args)
    local item = {
        name = args[1],
        amount = tonumber(args[2])
    }
    TriggerEvent('QBCore:Client:UseItem', item)
end)
```

{% hint style="info" %}
Server example (must have the item in your inventory)
{% endhint %}

```lua
-- /useitem sandwich 1

RegisterCommand('useitem', function(source, args)
    local item = {
        name = args[1],
        amount = tonumber(args[2])
    }
    TriggerClientEvent('QBCore:Client:UseItem', source, item)
end)
```

### QBCore:Command:ShowMe3D

| Arguments |  Type  | Required | Default |
| :-------: | :----: | :------: | :-----: |
| player id | number |    yes   |   none  |
|  message  | string |    yes   |   none  |

{% hint style="info" %}
Client example
{% endhint %}

```lua
-- /3dtext This is my message

RegisterCommand('3dtext', function(_, args)
    local message = table.concat(args, ' ')
    TriggerEvent('QBCore:Command:ShowMe3D', PlayerId(), message)
end)
```

{% hint style="info" %}
Server example
{% endhint %}

```lua
-- /3dtext This is my message

RegisterCommand('3dtext', function(source, args)
    local message = table.concat(args, ' ')
    TriggerClientEvent('QBCore:Command:ShowMe3D', source, message)
end)
```

### QBCore:Client:UpdateObject

{% hint style="success" %}
This event must be used as a handler when using [shared-exports.md](shared-exports.md "mention") because it refreshes the core object in your resource
{% endhint %}

```lua
RegisterNetEvent('QBCore:Client:UpdateObject', function()
    QBCore = exports['qb-core']:GetCoreObject()
end)
```
