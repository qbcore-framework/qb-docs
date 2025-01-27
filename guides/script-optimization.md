---
description: Learn how to write optimized code!
---

# 🚀 Script Optimization

### General Practices

**Localize Functions and Variables**

* Lua accesses local variables and functions faster than global ones. Always use `local` when declaring variables or functions unless explicitly required to be global

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

**Use Table Indexing Instead of `table.insert`**

* `table.insert` adds slight overhead; directly assigning a value is more efficient

```lua
function someFunction()
    local table = {}
    table.insert(table, {}) -- Don't use this
    table[#table+1] = {} -- Use this
end
```

**Simplify Conditional Checks**

* Use `if something then` instead of `if something ~= nil` to check for both `nil` and `false`

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

**Keep Functions Universal**

* Write functions and events that can handle multiple scenarios by passing parameters. This increases code reusability

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

**Short Returns**

* Use **short returns** to exit a function early if conditions aren't met. This keeps code cleaner and avoids unnecessary nested `if` blocks

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

**Avoid Re-Creating Tables or Variables Repeatedly**

* Instead of creating tables or variables repeatedly inside loops or frequently called functions, initialize them once and reuse

```lua
local reusableTable = {}

local function someFunction()
    for i = 1, 10 do
        reusableTable[i] = i -- Reuse the same table instead of creating a new one
    end
end
```

**Use `nil` to Free Up Memory**

* Assign unused variables to `nil` to let Lua’s garbage collector free the memory

```lua
local largeData = {1, 2, 3, 4}
-- Process data...
largeData = nil -- Free up memory when done
```

**Avoid Hardcoding**

* Centralize configurable values (like coordinates, item names, or payment amounts) into a `config.lua` file for easier management

**Example `config.lua`**:

```lua
Config = {
    Zones = {
        PoliceStation = vector3(441.1, -981.1, 30.7),
        Hospital = vector3(1151.21, -1529.62, 34.84)
    },
    Payments = {
        Police = 150,
        EMS = 120
    }
}
```

**Logging and Debugging**

* Use a debug mode toggle in your scripts to enable or disable logs dynamically without removing them. You could even add it as an option in your `config.lua` from above!

```lua
local DEBUG = true

local function debugLog(message)
    if DEBUG then
        print(message)
    end
end

debugLog('This is a debug message!')
```

**Track Performance**

* Measure execution time for performance-critical sections using `os.clock()` or FiveM natives

```lua
local start = os.clock()
-- Code to measure
print("Execution time:", os.clock() - start)
```

```lua
local startTime = GetGameTimer()
-- Simulate a delay
Wait(1000)
local endTime = GetGameTimer()
print("Execution time (ms):", endTime - startTime) -- Output: 1000 (approx)
```

**Avoid Overusing Network Events**

* Use shared state (e.g., via `state bags` or `entity states`) when frequent data synchronization is needed, rather than spamming `TriggerEvent` or `TriggerServerEvent`

```lua
-- Set state
Entity(playerPed).state:set('exampleData', 123, true)

-- Get state
local data = Entity(playerPed).state.exampleData
print(data) -- Outputs: 123
```

**Optimize Data Transmission**

* Only send the data you need, not entire tables or large payloads

```lua
TriggerServerEvent('exampleEvent', { x = 100, y = 200 }) -- Only send necessary fields
```

***

### Code Readability

Comment Your Code

* Include comments to explain logic, especially for complex or non-obvious sections

```lua
-- Check if the player is in range of the target zone
if #(playerCoords - targetCoords) < 10 then
    print('Player is in range')
end
```

Organize Your Script

* Structure your script logically, separating variables, functions, event handlers, and core logic into distinct sections

```lua
-- Variables
local QBCore = exports['qb-core']:GetCoreObject()

-- Functions
local function calculateDistance(pos1, pos2)
    return #(pos1 - pos2)
end

-- Events
RegisterNetEvent('exampleEvent', function()
    print('Event triggered!')
end)

-- Main Logic
CreateThread(function()
    print('Script started!')
end)
```

**Folder Structure**

* Break scripts into smaller, manageable pieces instead of writing everything in one file

```
my_script/
├── client/
│   ├── main.lua
│   ├── utils.lua
├── server/
│   ├── main.lua
│   ├── events.lua
├── shared/
│   ├── config.lua
└── fxmanifest.lua
```

***

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
    
    if dist < 5 then
        print('Im within 5 distance units of the coords!')
    end
end
```

***

### Loops

* Control your while loops and when they run

```lua
local function exampleLoop()
    CreateThread(function()
        while listen do
            print('running while loop only when needed')
            Wait(0)
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
        local sleep = 2500 -- Default wait time
        local ped = PlayerPedId()
        local pos = GetEntityCoords(ped)
        local inRange = #(pos - vector3(-829.11, 75.03, 52.73)) < 10.0

        if inRange then
            sleep = 0 -- Reduce wait time if condition is met
            print('I am in range!')
        else
            print('I am out of range.')
        end

        Wait(sleep)
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
            Wait(0)
        end
    end)
end
```

***

### Security

* A surplus amount of security in a code is not a bad thing. Don't be afraid to add in multiple if checks or create random variables to pass through your events
* Never do any type of transaction with the player regarding money or items on the client side of a resource

***

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
