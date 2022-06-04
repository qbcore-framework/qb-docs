---
description: Become a CEO, manage your company, make millions
---

# 👔 qb-management

## Introduction

* Handles all the storage and society logic for jobs and gangs&#x20;

{% hint style="danger" %}
Make sure to add your additional job societies to the `management_funds` table in the database!
{% endhint %}

## Preview

![](../.gitbook/assets/manangment.png)

## Configuration

### Boss menu

```lua
Config.BossMenus = { -- if target not enabled
    ['police'] = { -- job name
        vector3(461.45, -986.2, 30.73), -- location for distance checking
    },
}

Config.BossMenuZones = { -- if target is enabled
    ['police'] = { -- job name
        { -- polyzone box information
            coords = vector3(461.45, -986.2, 30.73),
            length = 0.35,
            width = 0.45,
            heading = 351.0,
            minZ = 30.58,
            maxZ = 30.68
        },
    },
}
```

### Gang menu

```lua
Config.GangMenus = { -- if target not enabled
    ['lostmc'] = {
        vector3(0, 0, 0), -- location for distance checking
    },
}

Config.GangMenuZones = { -- if target is enabled
    ['gangname'] = { -- gang name
        { -- polyzone box information
            coords = vector3(0.0, 0.0, 0.0),
            length = 0.0,
            width = 0.0,
            heading = 0.0,
            minZ = 0.0,
            maxZ = 0.0
        },
    },
}
```

## Server exports

{% hint style="warning" %}
All examples are done on the SERVER side!
{% endhint %}

### AddMoney

```lua
RegisterCommand('testaddmoney, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local job = Player.PlayerData.job.name
    exports['qb-management']:AddMoney(job, 500) -- Add $500 to society account
end)
```

### AddGangMoney

```lua
RegisterCommand('testaddgangmoney, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local gang = Player.PlayerData.gang.name
    exports['qb-management']:AddGangMoney(gang, 500) -- Add $500 to society
end)
```

### RemoveMoney

```lua
RegisterCommand('testremovemoney, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local job = Player.PlayerData.job.name
    exports['qb-management']:RemoveMoney(job, 500) -- Remove $500 society account
end)
```

### RemoveGangMoney

```lua
RegisterCommand('testremovegangmoney, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local gang = Player.PlayerData.gang.name
    exports['qb-management']:RemoveGangMoney(gang, 500) -- Remove $500 society
end)
```

### GetAccount

```lua
RegisterCommand('testgetaccount, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local job = Player.PlayerData.job.name
    local society = exports['qb-management']:GetAccount(job)
    print(society) -- if society exists prints balance else prints 0
end)
```

### GetGangAccount

```lua
RegisterCommand('testgetgangaccount, function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local gang = Player.PlayerData.gang.name
    local society = exports['qb-management']:GetGangAccount(gang)
    print(society) -- if society exists prints balance else prints 0
end)
```
