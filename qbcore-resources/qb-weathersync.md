---
description: Could someone please turn off the rain?
---

# 🌤 qb-weathersync

## Introduction

* Handles the logic for changing and syncing the weather
* Ability to set weather sync/desync weather&#x20;
* Use exports to call weather changing events to any resource

## Configuration

### General

```lua
Config                  = {}
Config.DynamicWeather   = true -- set this to false if you don't want the weather to change automatically every 10 minutes.

-- On server start
Config.StartWeather     = 'EXTRASUNNY' -- default weather
Config.BaseTime         = 8 -- time     
Config.TimeOffset       = 0 -- time offset 
Config.FreezeTime       = false -- freeze time 
Config.Blackout         = false -- set blackout                                 
Config.BlackoutVehicle  = false -- set blackout affects vehicles                
Config.NewWeatherTimer  = 10 -- time (in minutes) between each weather change   
Config.Disabled         = false -- set weather disabled                         
```

### Weather types

{% hint style="danger" %}
DON'T TOUCH EXCEPT IF YOU KNOW WHAT YOU ARE DOING
{% endhint %}

```lua
Config.AvailableWeatherTypes = {
    'EXTRASUNNY',
    'CLEAR',
    'NEUTRAL',
    'SMOG',
    'FOGGY',
    'OVERCAST',
    'CLOUDS',
    'CLEARING',
    'RAIN',
    'THUNDER',
    'SNOW',
    'BLIZZARD',
    'SNOWLIGHT',
    'XMAS',
    'HALLOWEEN',
}
```

## Exports

#### nextWeatherStage

Triggers event to switch weather to next stage

Lua example

```lua
local success = exports["qb-weathersync"]:nextWeatherStage();
```

JavaScript example

```javascript
const success = global.exports["qb-weathersync"].nextWeatherStage();
```

#### setWeather \[type]

Switch to a specified weather type from Config.AvailableWeatherTypes

Lua example

```lua
local success = exports["qb-weathersync"]:setWeather("snow");
```

JavaScript example

```javascript
const success = global.exports["qb-weathersync"].setWeather("snow");
```

#### setTime \[hour] (minute)

Sets sun position based on time to specified

Lua example

```lua
local success = exports["qb-weathersync"]:setTime(8, 10); -- 8:10 AM
```

JavaScript example

```javascript
const success = global.exports["qb-weathersync"].setTime(15, 30); // 3:30PM
```

#### setBlackout (true|false)

Sets or toggles blackout state and returns the state

Lua example

```lua
local newStatus = exports["qb-weathersync"]:setBlackout(); -- Toggle
```

JavaScript example

```javascript
const newStatus = global.exports["qb-weathersync"].setBlackout(true); // Enable
```

#### setTimeFreeze (true|false)

Sets or toggles time freeze state and returns the state

Lua example

```lua
local newStatus = exports["qb-weathersync"]:setTimeFreeze(); -- Toggle
```

JavaScript example

```javascript
const newStatus = global.exports["qb-weathersync"].setTimeFreeze(true); // Enable
```

#### setDynamicWeather (true|false)

Sets or toggles dynamic weather state and returns the state

Lua example

```lua
local newStatus = exports["qb-weathersync"]:setDynamicWeather(); -- Toggle
```

JavaScript example

```javascript
const newStatus = global.exports["qb-weathersync"].setDynamicWeather(true); // Enable
```

#### getBlackoutState

Returns if blackout is enabled or disabled

Lua example

```lua
local state = exports["qb-weathersync"]:getBlackoutState();
```

JavaScript example

```javascript
const state = global.exports["qb-weathersync"].getBlackoutState();
```

#### getTimeFreezeState

Returns if time progression is enabled or disabled

Lua example

```lua
local state = exports["qb-weathersync"]:getTimeFreezeState();
```

JavaScript example

```javascript
const state = global.exports["qb-weathersync"].getTimeFreezeState();
```

#### getWeatherState

Returns the current weather type

Lua example

```lua
local currentWeather = exports["qb-weathersync"]:getWeatherState();
```

JavaScript example

```javascript
const currentWeather = global.exports["qb-weathersync"].getWeatherState();
```

#### getDynamicWeather

Returns if time progression is enabled or disabled

Lua Example

```lua
local state = exports["qb-weathersync"]:getDynamicWeather();
```

JavaScript example

```javascript
const state = global.exports["qb-weathersync"].getDynamicWeather();
```

## Events

{% hint style="warning" %}
All of these examples are triggered CLIENT side!
{% endhint %}

#### RequestStateSync

```lua
TriggerServerEvent("qb-weathersync:server:RequestStateSync")
```

#### RequestCommands

```lua
TriggerServerEvent("qb-weathersync:server:RequestCommands")
```

#### setWeather

```lua
TriggerServerEvent("qb-weathersync:server:setWeather", type)
```

#### setTime

```lua
TriggerServerEvent("qb-weathersync:server:setTime", hour, minute)
```

#### toggleBlackout

```lua
TriggerServerEvent("qb-weathersync:server:toggleBlackout", bool)
```

#### toggleFreezeTime

```lua
TriggerServerEvent("qb-weathersync:server:toggleFreezeTime", bool, minute)
```

#### toggleDynamicWeather

```lua
TriggerServerEvent("qb-weathersync:server:toggleDynamicWeather", bool)
```

## Commands

/freezetime - Toggle time progression

/freezeweather - Toggle dynamic weather

/weather \[type] - Set weather

/blackout - Toggle blackout

/morning - Set time to 9am

/noon - Set time to 12pm

/evening - Set time to 6pm

/night - Set time to 11pm

/time \[hour] (minute) - Set time to whatever you want
