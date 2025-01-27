---
icon: circle-info
description: Let's dive into the core object of the qb-core resource!
---

# Core Object

## Introduction

The **Core Object** is the backbone of the `qb-core` framework, providing essential functionality and utilities for managing your server's gameplay mechanics, player data, and overall resource interactions. This page will guide you through the key features, methods, and best practices for using the Core Object effectively

### How to Access the Core Object

{% hint style="success" %}
We recommend using the core objects filtering capabilities instead of importing it all unless you need it!
{% endhint %}

To interact with the Core Object in your scripts, use the following pattern at the top of your script:

* Always cache the Core Object in a local variable to avoid repeated calls to `exports`

```lua
local QBCore = exports['qb-core']:GetCoreObject()
```

As of `qb-core` version 1.3.0 (check your fxmanifest.lua) you can decide what you want to get from the core object instead of importing it all! This change was made to reduce the amount of memory being stored inside each script because importing the full core brought a lot of overhead that wasn't needed.

```lua
-- I only need access to the functions of the core object!
local QBCore = exports['qb-core']:GetCoreObject({'Functions'})

-- Now the below is available to use!
-- QBCore.Functions

-- I need access to the functions and the shared!
local QBCore = exports['qb-core']:GetCoreObject({'Functions', 'Shared'})

-- Now the below are available to use!
-- QBCore.Functions
-- QBCore.Shared
```

### Exported Functions

* As of `qb-core` version 1.3.0 (check your fxmanifest.lua) all functions within the core object are exported so if you only need a single one you don't have to import them all! This is very handy if you are a script creator supporting different frameworks and don't need all the core information. You can now just call the functions you need.

```lua
local function getPlayer(source)
    return exports['qb-core']:GetPlayer(source)
end
```

### Core Features

| `Functions` | A collection of utility functions for common server and player operations. |
| ----------- | -------------------------------------------------------------------------- |

| `Players` | A table containing all currently connected players. |
| --------- | --------------------------------------------------- |

| `Shared` | Shared data like items, vehicles, and jobs. |
| -------- | ------------------------------------------- |

| `Config` | The main configuration table for `qb-core` |
| -------- | ------------------------------------------ |

| `Commands` | A registry for custom server and client commands. |
| ---------- | ------------------------------------------------- |

## Example Usage

### Accessing Player Data

* You can use the Core Object to retrieve a player's data

```lua
local QBCore = exports['qb-core']:GetCoreObject()

local function getPlayerJob(source)
    local player = QBCore.Functions.GetPlayer(source)
    if player then
        local job = player.PlayerData.job
        print("Player's job:", job.name)
    end
end
```

### Using Shared Data

* Access shared data like items, vehicles, or jobs

```lua
local QBCore = exports['qb-core']:GetCoreObject()

-- Retrieve details of a specific item
local item = QBCore.Shared.Items['water_bottle']
print("Item name:", item.name)
print("Item label:", item.label)
```

### Registering Commands

* The Core Object allows you to register custom commands for your server

```lua
local QBCore = exports['qb-core']:GetCoreObject()

QBCore.Commands.Add('greet', 'Send a greeting', {}, false, function(source, args)
    local name = args[1] or 'player'
    TriggerClientEvent('chat:addMessage', source, {
        template = '<div class="chat-message">Hello, {0}!</div>',
        args = { name }
    })
end)
```
