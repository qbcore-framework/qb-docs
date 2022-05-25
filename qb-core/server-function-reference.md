---
description: Learn about and how to use common core server functions!
---

# 🖥 Server Function Reference

### QBCore.Functions.GetCoords

* Get the coords of a passed entity

```lua
function QBCore.Functions.GetCoords(entity)
    local coords = GetEntityCoords(entity, false)
    local heading = GetEntityHeading(entity)
    return vector4(coords.x, coords.y, coords.z, heading)
end

-- Example

local ped = GetPlayerPed(source)
local coords = QBCore.Functions.GetCoords(ped)
print(coords)
```

### QBCore.Functions.GetIdentifier

* Get a specific identifier of a player

```lua
function QBCore.Functions.GetIdentifier(source, idtype)
    local idtype = idtype or QBConfig.IdentifierType
    for key, value in pairs(GetPlayerIdentifiers(source)) do
        if string.find(value, idtype) then
            return identifier
        end
    end
    return nil
end

-- Example

local identifier = QBCore.Functions.GetIdentifier(source, 'license')
print(identifier)

OR -- defaults to the identifier in the config of qb-core

local identifier = QBCore.Functions.GetIdentifier(source)
print(identifier)
```

### QBCore.Functions.GetSource

* Get a players source by identifer

```lua
function QBCore.Functions.GetSource(identifier)
    for key, value in pairs(QBCore.Players) do
        local identifiers = GetPlayerIdentifiers(key)
        for _, id in pairs(identifiers) do
            if identifier == id then
                return key
            end
        end
    end
    return 0
end

-- Example

local identifier = QBCore.Functions.GetIdentifier(source, 'license')
local playerSource = QBCore.Functions.GetSource(identifier)
print(playerSource)
```

### QBCore.Functions.GetPlayer

* Get a player by their source and access their data

```lua
function QBCore.Functions.GetPlayer(source)
    local src = source
    if type(src) == 'number' then
        return QBCore.Players[src]
    else
        return QBCore.Players[QBCore.Functions.GetSource(src)]
    end
end

-- Example

local Player = QBCore.Functions.GetPlayer(source)
print(QBCore.Debug(Player))

OR -- access some player data

local Player = QBCore.Functions.GetPlayer(source)
print(Player.PlayerData.citizenid)
```

### QBCore.Functions.GetPlayerByCitizenId

* Get a player by their citizen id and access their data (must be online)

```lua
function QBCore.Functions.GetPlayerByCitizenId(citizenid)
    for key, value in pairs(QBCore.Players) do
        if QBCore.Players[key].PlayerData.citizenid == citizenid then
            return QBCore.Players[key]
        end
    end
    return nil
end

-- Example

local Player = QBCore.Functions.GetPlayerByCitizenId('ONZ55343')
print(QBCore.Debug(Player))

OR -- access some player data

local Player = QBCore.Functions.GetPlayerByCitizenId('ONZ55343')
print(Player.PlayerData.license)
```

### QBCore.Functions.GetPlayerByPhone

* Get a player by their phone number (must be online)

```lua
function QBCore.Functions.GetPlayerByPhone(number)
    for key, value in pairs(QBCore.Players) do
        if QBCore.Players[key].PlayerData.charinfo.phone == number then
            return QBCore.Players[key]
        end
    end
    return nil
end

-- Example

local Player = QBCore.Functions.GetPlayerByPhone('1264756087')
print(QBCore.Debug(Player))

OR -- access some player data

local Player = QBCore.Functions.GetPlayerByPhone('1264756087')
print(Player.PlayerData.license)
```

### QBCore.Functions.GetPlayers

* Get all player IDs in the server (deprecated method)

```lua
function QBCore.Functions.GetPlayers()
    local sources = {}
    for key, value in pairs(QBCore.Players) do
        sources[#sources + 1] = key
    end
    return sources
end

-- Example

local Players = QBCore.Functions.GetPlayers()
print(QBCore.Debug(Players))
```

### QBCore.Functions.GetQBPlayers

* Access the table of all active players on the server (preferred to above)

```lua
function QBCore.Functions.GetQBPlayers()
    return QBCore.Players
end

-- Example

local Players = QBCore.Functions.GetQBPlayers()
print(QBCore.Debug(Players))
```

### QBCore.Functions.CreateCallback

* Creates a callback which is used on the client-side code with QBCore.Functions.TriggerCallback

```lua
function QBCore.Functions.CreateCallback(name, cb)
    QBCore.ServerCallbacks[name] = cb
end

-- Example

QBCore.Functions.CreateCallback('callbackName', function(source, cb)
    cb('Ok')
end)
```

### QBCore.Functions.CreateUseableItem

* Register an item as usable in the core

```lua
function QBCore.Functions.CreateUseableItem(item, cb)
    QBCore.UseableItems[item] = cb
end

-- Example

QBCore.Functions.CreateUseableItem('my_cool_item', function(source, item)
	local Player = QBCore.Functions.GetPlayer(source)
	if not Player.Functions.GetItemByName(item.name) then return end
	-- Trigger code here for what item should do
end)
```

### QBCore.Functions.CanUseItem

* Check if an item is registered as usable before attempting use

```lua
function QBCore.Functions.CanUseItem(item)
    return QBCore.UseableItems[item]
end

-- Example

local canUse = QBCore.Functions.CanUseItem('my_cool_item')
print(canUse)

OR

local canUse = QBCore.Functions.CanUseItem('my_cool_item')
if not canUse then return end
-- Trigger code here
```

### QBCore.Functions.UseItem

* Trigger an item to be used on the player

```lua
function QBCore.Functions.UseItem(source, item)
    QBCore.UseableItems[item.name](source, item)
end

-- Example

local Player = QBCore.Functions.GetPlayer(source)
if not Player.Functions.GetItemByName('my_cool_item') then return end
QBCore.Functions.UseItem(source, 'my_cool_item')
```

### QBCore.Functions.Kick

* Kick a player from the server

```lua
function QBCore.Functions.Kick(source, reason, setKickReason, deferrals)
    local src = source
    reason = '\n'..reason..'\n🔸 Check our Discord for further information: '..QBCore.Config.Server.discord
    if setKickReason then
        setKickReason(reason)
    end
    CreateThread(function()
        if deferrals then
            deferrals.update(reason)
            Wait(2500)
        end
        if src then
            DropPlayer(src, reason)
        end
        local i = 0
        while (i <= 4) do
            i = i + 1
            while true do
                if src then
                    if(GetPlayerPing(src) >= 0) then
                        break
                    end
                    Wait(100)
                    CreateThread(function() 
                        DropPlayer(src, reason)
                    end)
                end
            end
            Wait(5000)
        end
    end)
end

-- Example

QBCore.Functions.Kick(playerId, 'You messed up', true, true)
```

### QBCore.Functions.AddPermission

* Give a player a specific permission level (per session only)

```lua
function QBCore.Functions.AddPermission(source, permission)
    local license = QBCore.Functions.GetIdentifier(source, 'license')
    ExecuteCommand(('add_principal identifier.%s qbcore.%s'):format(license, permission))
    QBCore.Commands.Refresh(source)
end

-- Example

local Player = QBCore.Functions.GetPlayer(playerId)
local permission = 'admin'
QBCore.Functions.AddPermission(Player.PlayerData.source, permission)
```

### QBCore.Functions.RemovePermission

* Remove all of the players permissions on the server (per session only)

```lua
function QBCore.Functions.RemovePermission(source, permission)
    local src = source
    local license = QBCore.Functions.GetIdentifier(src, 'license')
    if permission then
        if IsPlayerAceAllowed(src, permission) then
            ExecuteCommand(('remove_principal identifier.%s qbcore.%s'):format(license, permission))
            QBCore.Commands.Refresh(src)
        end
    else
        for k,v in pairs(QBCore.Config.Server.Permissions) do
            if IsPlayerAceAllowed(src, v) then
                ExecuteCommand(('remove_principal identifier.%s qbcore.%s'):format(license, v))
                QBCore.Commands.Refresh(src)
            end
        end
    end
end

-- Example

local Player = QBCore.Functions.GetPlayer(playerId)
local permission = 'admin'
QBCore.Functions.RemovePermission(Player.PlayerData.source, permission)
```

### QBCore.Functions.HasPermission

* Check if a player has the permission level needed

```lua
function QBCore.Functions.HasPermission(source, permission)
    if IsPlayerAceAllowed(source, permission) then return true end
    return false
end

-- Example

local hasPerms = QBCore.Functions.HasPermission(source, 'admin')
print(hasPerms)

OR -- using as a condition

local hasPerms = QBCore.Functions.HasPermission(source, 'admin')
if not hasPerms then return end
-- Trigger code here
```

### QBCore.Functions.GetPermission

* Get a player's permission level

```lua
function QBCore.Functions.GetPermission(source)
    local src = source
    local perms = {}
    for key, value in pairs (QBCore.Config.Server.Permissions) do
        if IsPlayerAceAllowed(src, value) then
            perms[value] = true
        end
    end
    return perms
end

-- Example

local permissions = QBCore.Functions.GetPermission(source)
print(QBCore.Debug(permissions))

OR -- using as a condition

local permissions = QBCore.Functions.GetPermission(source)
for key, value in pairs(permissions) do
    if value == true then
        print(key)
    end
end
```

### QBCore.Functions.IsPlayerBanned

* Check if a player is banned (used for connection)

```lua
function QBCore.Functions.IsPlayerBanned(source)
    local plicense = QBCore.Functions.GetIdentifier(source, 'license')
    local result = MySQL.Sync.fetchSingle('SELECT * FROM bans WHERE license = ?', { plicense })
    if not result then return false end
    if os.time() < result.expire then
        local timeTable = os.date('*t', tonumber(result.expire))
        return true, 'You have been banned from the server:\n' .. result.reason .. '\nYour ban expires ' .. timeTable.day .. '/' .. timeTable.month .. '/' .. timeTable.year .. ' ' .. timeTable.hour .. ':' .. timeTable.min .. '\n'
    else
        MySQL.Async.execute('DELETE FROM bans WHERE id = ?', { result.id })
    end
    return false
end

-- Example

local isBanned = QBCore.Functions.IsPlayerBanned(source)
print(isBanned)
```

### QBCore.Functions.IsLicenseInUse

* Prevent duplicate licenses on the server (used for connection)

```lua
function QBCore.Functions.IsLicenseInUse(license)
    local players = GetPlayers()
    for key, value in pairs(players) do
        local identifiers = GetPlayerIdentifiers(value)
        for _, id in pairs(identifiers) do
            if string.find(id, 'license') then
                if id == license then
                    return true
                end
            end
        end
    end
    return false
end

-- Example

local license = QBCore.Functions.GetIdentifier(source, 'license')
local isUsed = QBCore.Functions.IsLicenseInUse(license)
print(isUsed)
```
