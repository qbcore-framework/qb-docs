---
description: Learn about and how to use common core server functions!
---

# 🖥️ Server Function Reference

## Player Getters

### QBCore.Functions.GetIdentifier

Get a specific identifier of a player

* source: `number`
* identifier: `string` (optional)
* <mark style="color:yellow;">return</mark>: `string`&#x20;

```lua
local identifier = QBCore.Functions.GetIdentifier(source, 'license')
print(identifier)

OR -- defaults to the identifier in the config of qb-core

local identifier = QBCore.Functions.GetIdentifier(source)
print(identifier)
```

### QBCore.Functions.GetSource

Get a players source by identifier

* identifier: `string`&#x20;
* <mark style="color:yellow;">return</mark>: `number`

```lua
local identifier = QBCore.Functions.GetIdentifier(source, 'license')
local playerSource = QBCore.Functions.GetSource(identifier)
print(playerSource)
```

### QBCore.Functions.GetPlayer

Get a player by their source and access their data

* source: `number` | `string`&#x20;
* <mark style="color:yellow;">return</mark>: `table`

```lua
local Player = QBCore.Functions.GetPlayer(source)
QBCore.Debug(Player)
```

### QBCore.Functions.GetPlayerByCitizenId

Get a player by their citizen id and access their data (must be online)

* citizenid: `string`
* <mark style="color:yellow;">return</mark>: `table`

```lua
local Player = QBCore.Functions.GetPlayerByCitizenId('ONZ55343')
QBCore.Debug(Player)
```

### QBCore.Functions.GetPlayerByPhone

Get a player by their phone number (must be online)

* number: `number`
* <mark style="color:yellow;">return</mark>: `table`

```lua
local Player = QBCore.Functions.GetPlayerByPhone(6422738491)
QBCore.Debug(Player)
```

### QBCore.Functions.GetPlayerByAccount

Get a player by their account number (must be online)

* account: `string`
* <mark style="color:yellow;">return</mark>: `table`

```lua
local Player = QBCore.Functions.GetPlayerByAccount('US08QBCore2345987612')
QBCore.Debug(Player)
```

### QBCore.Functions.GetPlayerByCharInfo

Get a player by their character info (must be online)

* property: `string`
* value: `any`
* <mark style="color:yellow;">return</mark>: `table`

```lua
local Player = QBCore.Functions.GetPlayerByCharInfo('firstname', 'Kakarot')
QBCore.Debug(Player)
```

### QBCore.Functions.GetPlayers

Get all player IDs in the server (deprecated method)

* <mark style="color:yellow;">return</mark>: `table`

```lua
local Players = QBCore.Functions.GetPlayers()
QBCore.Debug(Players)
```

### QBCore.Functions.GetQBPlayers

Access the table of all active players on the server (preferred to above)

* <mark style="color:yellow;">return</mark>: `table`

```lua
local Players = QBCore.Functions.GetQBPlayers()
QBCore.Debug(Players)
```

### QBCore.Functions.GetPlayersOnDuty

Get a table of player id's that are on duty for a specific job and the amount

* job: `string`
* <mark style="color:yellow;">return</mark>: `table` , `number`

```lua
local Players, Amount = QBCore.Functions.GetPlayersOnDuty('police')
print(QBCore.Debug(Players))
print('Currently '..amount..' police online')
```

### QBCore.Functions.GetDutyCount

Get the amount of players on duty for a specific job

* job: `string`
* <mark style="color:yellow;">return</mark>: `number`

```lua
local amount = QBCore.Functions.GetDutyCount('police')
print('Currently '..amount..' police online')
```

## World Getters

### QBCore.Functions.GetCoords

Get the coordinates of a passed entity

* entity: `number`
* <mark style="color:yellow;">return</mark>: `vector4`

```lua
local ped = GetPlayerPed(source)
local coords = QBCore.Functions.GetCoords(ped)
print(coords)
```

### QBCore.Functions.GetClosestObject

Get's the closest object to a player in the world and the distance to it

* source: `string`&#x20;
* coords: `vector3` (optional)
* <mark style="color:yellow;">return</mark>: `number` |`number`

```lua
local ped = GetPlayerPed(source)
local location = GetEntityCoords(ped)
local objectHandle, distance = QBCore.Functions.GetClosestObject(source, location)
print('Closest Object:', objectHandle, 'Distance:', distance)
```

### QBCore.Functions.GetClosestVehicle

Get's the closest vehicle to a player in the world and the distance to it

* source: `string`&#x20;
* coords: `vector3` (optional)
* <mark style="color:yellow;">return</mark>: `number` |`number`

```lua
local ped = GetPlayerPed(source)
local location = GetEntityCoords(ped)
local vehicle, distance = QBCore.Functions.GetClosestVehicle(source, location)
print('Closest Vehicle:', vehicle, 'Distance:', distance)
```

### QBCore.Functions.GetClosestPed

Get's the closest ped to a player in the world and the distance to it

* source: `string`&#x20;
* coords: `vector3` (optional)
* <mark style="color:yellow;">return</mark>: `number` |`number`

```lua
local ped = GetPlayerPed(source)
local coords = GetEntityCoords(ped)
local closestPed, distance = QBCore.Functions.GetClosestPed(source, coords)
print('Closest Ped:', closestPed, 'Distance:', distance)
```

## Vehicle Creation

### QBCore.Functions.SpawnVehicle

Spawns a vehicle near a player using the standard client-assisted `CreateVehicle` RPC. The client must be near the spawn location for the vehicle to appear

* source: `string`
* model: `string`|`number`
* coords: `vector3` _(optional)_
* warp: `boolean` (optional)
* <mark style="color:yellow;">return</mark>: `number`

```lua
local veh = QBCore.Functions.SpawnVehicle(source, "sultan")
print("Spawned vehicle:", veh)
```

### QBCore.Functions.CreateAutomobile

Spawns a vehicle using the experimental `CREATE_AUTOMOBILE` native, which does not rely on the client for creation. This is more efficient but does **not work for all vehicle types**

* source: `string`
* model: `string`|`number`
* coords: `vector3` _(optional)_
* warp: `boolean` (optional)
* <mark style="color:yellow;">return</mark>: `number`

```lua
local veh = QBCore.Functions.CreateAutomobile(source, "sultan")
print("Created automobile:", veh)
```

### QBCore.Functions.CreateVehicle

Uses the newer `CreateVehicleServerSetter` native to spawn vehicles on the server. More reliable and supports all major vehicle types

* source: `string`
* model: `string`|`number`&#x20;
* vehType: `string`
* coords: `vector3` _(optional)_
* warp: `boolean` (optional)
* <mark style="color:yellow;">return</mark>: `number`

```lua
local veh = QBCore.Functions.CreateVehicle(source, "sultan", "automobile")
print("Created vehicle with server setter:", veh)
```

## Routing Buckets

### QBCore.Functions.GetBucketObjects

Returns the internal bucket state tables used by the framework

* <mark style="color:yellow;">return</mark>: `table`, `table`&#x20;

```lua
local playerBuckets, entityBuckets = QBCore.Functions.GetBucketObjects()
QBCore.Debug(playerBuckets)
QBCore.Debug(entityBuckets)
```

### QBCore.Functions.GetPlayersInBucket

Returns a list of player IDs assigned to a given bucket

* bucket: `number`
* <mark style="color:yellow;">return</mark>: `table` | `boolean`

```lua
local players = QBCore.Functions.GetPlayersInBucket(3)
if players then
    print("Players in bucket 3:", json.encode(players))
end
```

### QBCore.Functions.GetEntitiesInBucket

Returns a list of entity IDs (excluding players) assigned to a given bucket

* bucket: `number`
* <mark style="color:yellow;">return</mark>: `table` | `boolean`

```lua
local entities = QBCore.Functions.GetEntitiesInBucket(3)
if entities then
    print("Entities in bucket 3:", json.encode(entities))
end
```

### QBCore.Functions.SetEntityBucket

Assigns an entity (e.g., ped, vehicle, or prop) to the specified routing bucket

* entity: `number`&#x20;
* bucket: `number`
* <mark style="color:yellow;">return</mark>: `boolean`

```lua
local entity = GetVehiclePedIsIn(GetPlayerPed(source), false)
local success = QBCore.Functions.SetEntityBucket(entity, 3)
if success then
    print("Entity moved to bucket 3")
end
```

### QBCore.Functions.SetPlayerBucket

Assigns a player to the specified routing bucket

* source: `string`
* bucket: `number`
* <mark style="color:yellow;">return</mark>: `boolean`

```lua
local success = QBCore.Functions.SetPlayerBucket(source, 3)
if success then
    print("Player moved to bucket 3")
end
```

## Items

### QBCore.Functions.CreateUseableItem

Registers an item as "usable" and binds it to a callback function

* item: `string`
* data: `function` | `table`

```lua
QBCore.Functions.CreateUseableItem('my_cool_item', function(source, item)
	local Player = QBCore.Functions.GetPlayer(source)
	if not Player.Functions.GetItemByName(item.name) then return end
	-- Trigger code here for what item should do
end)
```

### QBCore.Functions.CanUseItem

Checks if a given item has been registered as usable

* item: `string`&#x20;
* return: `table` | `nil`

```lua
if QBCore.Functions.CanUseItem("my_cool_item") then
    print("my_cool_item is a usable item")
end
```

### QBCore.Functions.UseItem

Trigger an item to be used on the player

* source: `string`
* item: `string`

```lua
local Player = QBCore.Functions.GetPlayer(source)
if not Player.Functions.GetItemByName('my_cool_item') then return end
QBCore.Functions.UseItem(source, 'my_cool_item')
```

### QBCore.Functions.HasItem

Checks if a player has a specific item(s)

* source: `string`
* items: `string` | `table`&#x20;
* amount: `number` (optional)
* <mark style="color:yellow;">return</mark>: `boolean`

```lua
if QBCore.Functions.HasItem(source, "radio") then
    print("Player has a radio")
end

if QBCore.Functions.HasItem(source, { "radio", "id_card" }) then
    print("Player has both a radio and ID")
end

if QBCore.Functions.HasItem(source, { radio = 1, bandage = 3 }) then
    print("Player has 1 radio and 3 bandages")
end
```

## Permissions

### QBCore.Functions.AddPermission

Give a player a specific permission level (per session only)

* source: `string`
* permission: `string`

```lua
local Player = QBCore.Functions.GetPlayer(playerId)
if not Player then return end
local permission = 'admin'
QBCore.Functions.AddPermission(Player.PlayerData.source, permission)
```

### QBCore.Functions.RemovePermission

Remove a specific permission level or all of the players permissions (per session only)

* source: `string`
* permission: `string` (optional)

```lua
local Player = QBCore.Functions.GetPlayer(playerId)
if not Player then return end
local permission = 'admin'
QBCore.Functions.RemovePermission(Player.PlayerData.source, permission)
```

### QBCore.Functions.HasPermission

Check if a player has a specific permission level(s)

* source: `string`
* permission: `string` | `table`

```lua
if QBCore.Functions.HasPermission(source, "admin") then
    print("Player is an admin")
end
```

### QBCore.Functions.GetPermission

Get a player's permission level(s)

* source: `string`
* <mark style="color:yellow;">return</mark>: `table`

```lua
local permissions = QBCore.Functions.GetPermission(source)
QBCore.Debug(permissions)
```

### QBCore.Functions.IsOptIn

Checks whether a player has opted in to receive reports

* source: `string`
* <mark style="color:yellow;">return</mark>: `boolean`

```lua
if QBCore.Functions.IsOptin(source) then
    print("Player receives reports")
end
```

### QBCore.Functions.ToggleOptIn

Toggle a players status to receive reports

* source: `string`

```lua
QBCore.Functions.ToggleOptin(source)
```

## Callbacks

### QBCore.Functions.TriggerClientCallback

Triggers a client-side callback function from the server. Supports both asynchronous usage via a promise and direct function-based response handling

* name: `string`
* source: `string`
* cb: `function` _(optional)_
* `...`: `any`&#x20;

```lua
CreateThread(function()
    local playerData = QBCore.Functions.TriggerClientCallback("resourceName:testCallback", source)
    print(playerData)
end)

OR

QBCore.Functions.TriggerClientCallback("resourceName:testCallback", source, function(data)
    print("Received from client:", data)
end)
```

### QBCore.Functions.CreateCallback

Registers a new server-side callback that can be triggered from the client

* name: `string`
* cb: `function`

```lua
QBCore.Functions.CreateCallback("resourceName:testCallback", function(source, cb)
    local Player = QBCore.Functions.GetPlayer(source)
    cb(Player)
end)
```

## Miscellaneous

### QBCore.Functions.Notify

Triggers a notification on a specfic player

* source: `string`
* text: `string`
* type: `string` (optional)
* length: `number` (optional)

```lua
QBCore.Functions.Notify(source, 'Success!', 'success', 5000)
```

### QBCore.Debug

Prints a formatted, color-coded debug output of a table or value

* table: `table` | `any`
* indent: `number` (optional)
* resource: `string`

```lua
local data = {
    name = "John",
    isAdmin = true,
    stats = {
        health = 100,
        stamina = 75,
    }
}

QBCore.Debug(data)
```

### QBCore.ShowError

Prints a red-colored error log to the console

* resource: `string`
* message: `string`

```lua
QBCore.ShowError('qb-core', 'Error!')
```

### QBCore.ShowSuccess

Prints a green-colored success/log message to the console

* resource: `string`
* message: `string`

```lua
QBCore.ShowSuccess('qb-core', 'Success!')
```

### QBCore.Functions.Kick

Kick a player from the server

* playerId: `string`
* reason: `string`
* setKickReason: `function` (optional)
* deferrals: `table` (optional)

```lua
QBCore.Functions.Kick(playerId, "Exploiting detected")
```
