---
description: Learn how to write optimized code!
---

# 🚀 Script Optimization

### General Practices

* Localize as many functions and variables as possible. Lua can read them faster

```lua
myVariable = false -- Don't use this
local myVariable = false -- Use this

function someFunction() -- Don't use this
    print('Im a global function!')
end

local function someFunction() -- Use this
    print('Im a local function!')
end
```

* Instead of using `table.insert` use `tableName[#tableName+1] = data`

```lua
function someFunction()
    local table = {}
    table.insert(table, {}) -- Don't use this
    table[#table+1] = {} -- Use this
end
```

* Instead of using `if something ~= nil` use `if something then`. This method checks for nil and/or false at the same time

```lua
function someFunction()
    local bool = nil
    
    if bool ~= nil then -- Don't use this
        print('bool was not nil but also could be false!')
    end
    
    if bool then -- Use this
        print('bool was neither nil or false!')
    end
end
```

* If you are creating a function or an event, make it so that it can be used in different scenarios with different variables. Keep it universal basically

```lua
local function someFunction(param1, param2, param3)
    print('Im a function that accepts 3 parameters which allows for multiple conditions!')
    if param1 == 'something' then
        print('I met condition number one!')
    elseif param2 == 'somethingelse' then
        print('I met condition number two!')
    elseif param3 == 'somethingelsemore' then
        print('I met condition number three!')
    end
end

RegisterNetEvent('someEvent', function(param1, param2, param3)
    print('Im an event that accepts 3 parameters which allows for multiple conditions!')
    if param1 == 'something' then
        print('I met condition number one!')
    elseif param2 == 'somethingelse' then
        print('I met condition number two!')
    elseif param3 == 'somethingelsemore' then
        print('I met condition number three!')
    end
end)
```

* When writing code use what's known as "short returns" for failed conditions

```lua
local function someFunction(param1, param2, param3)
    if not param1 then return end
    print('I met condition number one!')
    if not param2 then return end
    print('I met condition number two!')
    if not param3 then return end
    print('I met condition number three!')
end
```



### Native Usage

* Always replace `GetPlayerPed(-1)` with `PlayerPedId()`

```lua
local function someFunction()
    local ped = GetPlayerPed(-1) -- Don't use this
    local ped = PlayerPedId() -- Use this
end
```

* Always replace `GetDistanceBetweenCoords` with lua math aka `#(vector3 - vector3)`

```lua
local function someFunction()
    local ped = PlayerPedId()
    local pCoords = GetEntityCoords(ped)
    local coords = vector3(-29.53, -1103.67, 26.42)
    
    local dist = GetDistanceBetweenCoords(pCoords, coords, true) -- Don't use this
    local dist = #(pCoords - coords) -- Use this
    
    if dist > 5 then
        print('Im within 5 distance units of the coords!')
    end
end
```



### Loops

* Control your while loops and when they run

```lua
local function exampleLoop()
    CreateThread(function()
        while listen do
            print('running while loop only when needed')
            Wait(1)
        end
    end)
end

local listen = false
CreateThread(function()
    LoopZone = CircleZone:Create(vector3(-851.63, 74.36, 51.86), 5.0, {
        name = "ExampleLoop",
        debugPoly = true,
    })
    LoopZone:onPlayerInOut(function(isPointInside)
        if isPointInside then
            listen = true
            exampleLoop() -- Initiate loop
        else
            listen = false -- turns off when your outside the zone
        end
    end)
end)
```

* If you do have to create a thread that includes a "while" loop, always avoid using "while true do" if able. If you have to use this, follow the next tip, and it won’t impact performance as much
* Control your thread times by using a variable that changes the wait time retroactively. So you can set the thread wait time to say 1000ms which checks for your if statement every second and if it makes it into the statement you can lower the wait time by just changing the variable value. Wait(sleep)

```lua
CreateThread(function()
    while true do
        Wait(1)
        inRange = false
        local pos = GetEntityCoords(PlayerPedId())
        if #(pos - vector3(-829.11, 75.03, 52.73)) < 10.0 then
            inRange = true
            print('Im in range and the loop runs faster')
        else
            print('Im not in range so i run only onces every 2.5 seconds')
        end
        if not inRange then
            Wait(2500)
        end
    end
end)
```

* If you have job specific loops, make sure they only apply to players with that job. There's no reason for someone who is not a cop to be running a loop on their machine that does not apply to them

```lua
local function exampleJobLoop()
    local job = QBCore.Functions.GetPlayerData().job.name
    CreateThread(function()
        while job == 'police' do
            print('im a policeman!')
            Wait(1)
        end
    end)
end
```



### Security

* A surplus amount of security in a code is not a bad thing. Don't be afraid to add in multiple if checks or create random variables to pass through your events
* Never do any type of transaction with the player regarding money or items on the client side of a resource



### Event Handlers

* When setting variables inside your resource, handlers come in especially handy due to not needing to constantly run checks

```lua
-- These are client-side examples

local isLoggedIn = false
local PlayerData = {}

AddStateBagChangeHandler('isLoggedIn', nil, function(_, _, value) -- FiveM native method
    if value then
        isLoggedIn = true
        PlayerData = QBCore.Functions.GetPlayerData()
    else
        isLoggedIn = false
        PlayerData = {}
    end
end)

AddEventHandler('QBCore:Client:OnPlayerLoaded', function() -- Don't use this with the native method
    isLoggedIn = true
    PlayerData = QBCore.Functions.GetPlayerData()
end)

RegisterNetEvent('QBCore:Client:OnPlayerUnload', function() -- Don't use this with the native method
    isLoggedIn = false
    PlayerData = {}
end)

RegisterNetEvent('QBCore:Client:OnJobUpdate', function(JobInfo)
    PlayerData.job = JobInfo
end)

RegisterNetEvent('QBCore:Player:SetPlayerData', function(val)
    PlayerData = val
end)
```
