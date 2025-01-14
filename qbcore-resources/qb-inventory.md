---
description: Store your precious!
---

# 🎒 qb-inventory

## Introduction

* Handles all the player's storage such as personal, vehicle, stash, drops
* [qb-shops.md](qb-shops.md "mention") integration for displaying all items available to buy
* Built-in support for usable vending machines

{% hint style="danger" %}
All exports listed are SERVER only unless specified
{% endhint %}

## Inventory State

The inventory state is controlled via state bags using a state bag name of `inv_busy`. You can use this state to control whether the inventory should be able to be opened or not

#### Example (server):

```lua
RegisterCommand('checkState', function(source)
    local player = Player(source)
    local state = player.state.inv_busy
    print('Inventory current state is', state)
end, true)

RegisterCommand('lockInventory', function(source)
    local player = Player(source)
    player.state.inv_busy = true
    print('Inventory current state is', state)
end, true)

RegisterCommand('unlockInventory', function(source)
    local player = Player(source)
    player.state.inv_busy = false
    print('Inventory current state is', state)
end, true)
```

#### Example (client):

```lua
RegisterCommand('lockInventory', function()
    LocalPlayer.state:set('inv_busy', true, true)
end, false)

RegisterCommand('unlockInventory', function()
    LocalPlayer.state:set('inv_busy', false, true)
end, false)
```

## Item Info

{% hint style="success" %}
You can use SetItemData to achieve this
{% endhint %}

Items support additional information that can be added to them via an `info` attribute. This information will display on the item when the player hovers over it in a key,value pair format

#### Example:

```lua
RegisterCommand('addItemWithInfo', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local info = {
        uniqueData1 = 'uniqueData1',
        uniqueData2 = 'uniqueData2',
        uniqueData3 = 'uniqueData3',
        uniqueData4 = 'uniqueData4',
    }
    exports['qb-inventory']:AddItem(source, itemName, 1, false, info, 'qb-inventory:testAdd')
end, true)

RegisterCommand('editItemWithInfo', function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local items = Player.PlayerData.items
    local itemInfo = items[1]
    print(json.encode(itemInfo, { indent = true }))
    itemInfo.info = {
        newInfo = 'New Info'
    }
    print(json.encode(itemInfo, { indent = true }))
    items[1] = itemInfo
    Player.Functions.SetPlayerData('items', items)
end, true)
```

## LoadInventory

This function will retrieve the players inventory from the database via their unique identifier aka `citizenid`

```lua
exports['qb-inventory']:LoadInventory(source, citizenid)
```

* source: `number`
* citizenid: `string`
* <mark style="color:yellow;">returns</mark>: `table`

```lua
RegisterCommand('getInv', function(source)
    local Player = QBCore.Functions.GetPlayer(source)
    local citizenId = Player.PlayerData.citizenid
    local items = exports['qb-inventory']:LoadInventory(source, citizenid)
    print(json.encode(items, { indent = true }))
end)
```

## SaveInventory

This function saves the players current items to the database

```lua
exports['qb-inventory']:SaveInventory(source, offline)
```

* source: `number`
* offline: `boolean`

#### Example:

```lua
RegisterCommand('saveInv', function(source)
    exports['qb-inventory']:SaveInventory(source, false)
end)
```

## ClearInventory

```lua
exports['qb-inventory']:ClearInventory(source, filterItems)
```

* source: `number`
* filterItems: `string | table`

Example:

```lua
RegisterCommand('clearInventoryExcludeItem', function(source, args)
    local filterItem = args[1]
    if not filterItem then return end
    exports['qb-inventory']:ClearInventory(source, filterItem)
    print('Inventory cleared for player '..source..', excluding item: '..filterItem)
end, true)

RegisterCommand('clearInventoryExcludeItems', function(source)
    local filterItems = {'item1', 'item2'}
    exports['qb-inventory']:ClearInventory(source, filterItems)
    print('Inventory cleared for player '..source..', excluding items: '..table.concat(filterItems, ', '))
end, true)
```

## CloseInventory

```lua
exports['qb-inventory']:CloseInventory(source, identifier)
```

* source: `number`
* identifier: `string`

Example:

```lua
RegisterCommand('closeInventory', function(source)
    exports['qb-inventory']:CloseInventory(source)
    print('Inventory closed for player '..source)
end, true)

RegisterCommand('closeInventoryByName', function(source, identifier)
    exports['qb-inventory']:CloseInventory(source, identifier)
    print('Inventory closed for player '..source..' and inventory '..identifier..' set to closed')
end, true)
```

## OpenInventory

```lua
exports['qb-inventory']:OpenInventory(source, identifier, data)
```

* source: `number`
* identifier: `string | optional`
* data: `table | optional`

#### Example:

```lua
RegisterCommand('openinv', function(source)
    exports['qb-inventory']:OpenInventory(source)
end, true)

RegisterCommand('openinvbyname', function(source, args)
    local inventoryName = args[1]
    exports['qb-inventory']:OpenInventory(source, inventoryName)
end, true)

RegisterCommand('openinvbynamewithdata', function(source, args)
    local inventoryName = args[1]
    local data = { label = 'Custom Stash', maxweight = 400000, slots = 500 }
    exports['qb-inventory']:OpenInventory(source, inventoryName, data)
end, true)
```

## OpenInventoryById

```lua
exports['qb-inventory']:OpenInventoryById(source, playerId)
```

* source: `number`
* playerId: `number`

#### Example:

```lua
RegisterCommand('openplayerinv', function(source, args)
    local playerId = tonumber(args[1])
    exports['qb-inventory']:OpenInventoryById(source, playerId)
end, true)
```

{% hint style="info" %}
`OpenInventoryById` will close the target players inventory (if open) and lock it via state. It will then unlock when the opening player closes it
{% endhint %}

## CreateShop

```lua
exports['qb-inventory']:CreateShop(shopData)
```

* shopData: `table`

```lua
local items = {
    { name = 'sandwich', amount = 10, price = 5 }
}

RegisterCommand('createShop', function(source)
    local playerPed = GetPlayerPed(source)
    local playerCoords = GetEntityCoords(playerPed)
    exports['qb-inventory']:CreateShop({
        name = 'testShop',
        label = 'Test Shop',
        coords = playerCoords, -- optional
        slots = #items,
        items = items
    })
end, true)
```

{% hint style="info" %}
Coords being passed to `createShop` will be checked against the player's current coords when `OpenShop`is called if coords were provided during `createShop`
{% endhint %}

## OpenShop

```lua
exports['qb-inventory']:OpenShop(source, name)
```

* source: `number`
* name: `string`

```lua
RegisterCommand('openShop', function(source)
    exports['qb-inventory']:OpenShop(source, 'testShop')
end)
```

## CanAddItem

```lua
exports['qb-inventory']:CanAddItem(source, item, amount)
```

* source: `number`
* item: `string`
* amount: `number`
* <mark style="color:yellow;">returns</mark>: `boolean`

Example:

```lua
RegisterCommand('canAddItem', function(source, args)
    local itemName = args[1]
    local amount = tonumber(args[2])
    if not itemName or not amount then return end
    local canAdd, reason = exports['qb-inventory']:CanAddItem(source, itemName, amount)
    if canAdd then
        print('Can add '..amount..' of item '..itemName)
    else
        print('Cannot add '..amount..' of item '..itemName..'. Reason: '..reason)
    end
end, true)
```

## AddItem

```lua
exports['qb-inventory']:AddItem(identifier, item, amount, slot, info, reason)
```

* identifier: `number`
* item: `string`
* amount: `number`
* slot: `number | boolean`
* info: `table | boolean`
* reason: `string`
* <mark style="color:yellow;">returns</mark>: `boolean`

#### Example:

```lua
RegisterCommand('addItem', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    exports['qb-inventory']:AddItem(source, itemName, 1, false, false, 'qb-inventory:testAdd')
end, true)
```

## RemoveItem

```lua
exports['qb-inventory']:RemoveItem(identifier, item, amount, slot, reason)
```

* identifier: `number`
* item: `string`
* amount: `number`
* slot: `number | boolean`
* reason: `string`
* <mark style="color:yellow;">returns</mark>: `boolean`

```lua
RegisterCommand('removeItem', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    exports['qb-inventory']:RemoveItem(source, itemName, 1, false, 'qb-inventory:testRemove')
end, true)
```

## SetInventory

```lua
exports['qb-inventory']:SetInventory(source, items)
```

* source: `number`
* items: `table`

Example:

```lua
RegisterCommand('setInventory', function(source)
    local items = {
        {
            name = 'sandwich',
            amount = 10,
            type = 'item',
            info = {},
            slot = 1
        },
        {
            name = 'water_bottle',
            amount = 10,
            type = 'item',
            info = {},
            slot = 2
        }
    }
    exports['qb-inventory']:SetInventory(source, items)
end, true)
```

## SetItemData

{% hint style="warning" %}
This function uses GetItemByName to find the itemName being passed
{% endhint %}

```lua
exports['qb-inventory']:SetItemData(source, itemName, key, val)
```

* source: `number`
* itemName: `string`
* key: `string`
* val: `string | table`
* <mark style="color:yellow;">returns</mark>: `boolean`

Example:

```lua
RegisterCommand('setItemData', function(source, args)
    local itemName = args[1]
    local key = args[2]
    local val = args[3]
    if not itemName or not key or not val then return end
    local success = exports['qb-inventory']:SetItemData(source, itemName, key, val)
    if success then
        print('Set data for item '..itemName..': '..key..' = '..val)
    else
        print('Failed to set data for item '..itemName)
    end
end, true)
```

#### Item Info Example:

```lua
RegisterCommand('setItemData', function(source)
    local itemName = 'markedbills'
    local key = 'info'
    local val = { worth = 1000 }
    if not itemName or not key or not val then return end
    local success = exports['qb-inventory']:SetItemData(source, itemName, key, val)
    if success then
        print('Set data for item '..itemName..': '..key..' = '..json.encode(val, { indent = true }))
    else
        print('Failed to set data for item '..itemName)
    end
end, true)
```

## UseItem

```lua
exports['qb-inventory']:UseItem(itemName, ...)
```

* itemName: `string`
* . . . : `function`

Example:

```lua
RegisterCommand('useItem', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    exports['qb-inventory']:Useitem(itemName, function()
        print('Used item with the name of '..itemName)
    end)
end, true)
```

## HasItem

{% hint style="success" %}
This export is also available to use on the client
{% endhint %}

```lua
exports['qb-inventory']:HasItem(source, items, amount)
```

* source: `number`
* items: `string | table`
* amount: `number`
* <mark style="color:yellow;">returns</mark>: `boolean`

Example:

```lua
RegisterCommand('hasSingleItem', function(source)
    local item = 'item1'
    local amount = 5
    local hasItem = exports['qb-inventory']:HasItem(source, item, amount)
    if hasItem then
        print('Player '..source..' has '..amount..' of '..item)
    else
        print('Player '..source..' does not have '..amount..' of '..item)
    end
end, true)

RegisterCommand('hasMultipleItems', function(source)
    local items = {'item1', 'item2'}
    local amount = 5
    local hasItems = exports['qb-inventory']:HasItem(source, items, amount)
    if hasItems then
        print('Player '..source..' has '..amount..' of each item: '..table.concat(items, ', '))
    else
        print('Player '..source..' does not have '..amount..' of each item: '..table.concat(items, ', '))
    end
end, true)

RegisterCommand('hasMultipleItemsWithAmounts', function(source)
    local itemsWithAmounts = {item1 = 5, item2 = 10}
    local hasItemsWithAmounts = exports['qb-inventory']:HasItem(source, itemsWithAmounts)
    if hasItemsWithAmounts then
        print('Player '..source..' has the specified items with their amounts')
    else
        print('Player '..source..' does not have the specified items with their amounts')
    end
end, true)
```
## GetFreeWeight
Returns the available space in weight of a specified player source's inventory.

```lua
exports['qb-inventory']:GetFreeWeight(source)
```

* source: `number`
* <mark style="color:yellow;">returns</mark>: `number`

Example:

```lua
RegisterCommand('getFreeWeight', function(source)
    local freeWeight = exports['qb-inventory']:GetFreeWeight(source)
    print('Free Weight: ' .. freeWeight)
end, true)
```
## GetSlots
Returns the occupied and empty slots of a specified identifier's inventory. (Player source or id of inventory / drop)

```lua
exports['qb-inventory']:GetSlots(identifier)
```

* identifier: `number | string`
* <mark style="color:yellow;">returns</mark>: slotsUsed: `number`, slotsFree: `number`

Example:

```lua
RegisterCommand('getSlots', function(source, args)
    local invId = args[1]
    if not invId then return end

    local slotsUsed, slotsFree = exports['qb-inventory']:GetSlots(invId)
    print('Slots Used: ' .. slotsUsed, 'Slots Free: ' .. slotsFree)
end, true)
```

## GetSlotsByItem

```lua
exports['qb-inventory']:GetSlotsByItem(items, itemName)
```

* items: `table`
* itemName: `string`
* <mark style="color:yellow;">returns</mark>: `table`

Example:

```lua
RegisterCommand('getSlots', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local Player = QBCore.Functions.GetPlayer(source)
    local items = Player.PlayerData.Items
    local slots = exports['qb-inventory']:GetSlotsByItem(items, itemName)
    for _, slot in ipairs(slots) do
        print(slot)
    end
end, true)
```

## GetFirstSlotByItem

```lua
exports['qb-inventory']:GetFirstSlotByItem(items, itemName)
```

* items: `table`
* itemName: `string`
* <mark style="color:yellow;">returns</mark>: `number`

Example:

```lua
RegisterCommand('getFirstSlot', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local Player = QBCore.Functions.GetPlayer(source)
    local items = Player.PlayerData.Items
    local slot = exports['qb-inventory']:GetFirstSlotByItem(items, itemName)
    if slot then
        print('First slot containing item '..itemName..' is: '..slot)
    else
        print('No slot found containing item '..itemName)
    end
end, true)
```

## GetItemBySlot

```lua
exports['qb-inventory']:GetItemBySlot(source, slot)
```

* source: `number`
* slot: `number`
* <mark style="color:yellow;">returns</mark>: `table`

Example:

```lua
RegisterCommand('getItem', function(source, args)
    local slot = tonumber(args[1])
    if not slot then return end
    local item = exports['qb-inventory']:GetItemBySlot(source, slot)
    if item then
        print('Item in slot '..slot..' is: '..item.name)
    else
        print('No item found in slot '..slot)
    end
end, true)
```

## GetItemByName

```lua
exports['qb-inventory']:GetItemByName(source, item)
```

* source: `number`
* item: `string`
* <mark style="color:yellow;">returns</mark>: `table`

Example:

```lua
RegisterCommand('getItemByName', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local item = exports['qb-inventory']:GetItemByName(source, itemName)
    if item then
        print('First occurrence of item '..itemName..' is in slot: '..item.slot)
    else
        print('No item found with name '..itemName)
    end
end, true)
```

## GetItemsByName

```lua
exports['qb-inventory']:GetItemsByName(source, item)
```

* source: `number`
* item: `string`
* <mark style="color:yellow;">returns</mark>: `table`

Example:

```lua
RegisterCommand('getItemsByName', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local items = exports['qb-inventory']:GetItemsByName(source, itemName)
    if #items > 0 then
        print('Items named '..itemName..' found in slots:')
        for _, item in ipairs(items) do
            print(item.slot)
        end
    else
        print('No items found with name '..itemName)
    end
end, true)
```

## GetItemCount

```lua
exports['qb-inventory']:GetItemCount(source, items)
```

* source: `number`
* items: `string | table`
* <mark style="color:yellow;">returns</mark>: `number`

Example:

```lua
RegisterCommand('getItemCount', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    local itemCount = exports['qb-inventory']:GetItemCount(source, itemName)
    if itemCount and itemCount > 0 then
        print('You have '..itemCount..' of item: '..itemName)
    else
        print('No items found with name '..itemName)
    end
end, true)

RegisterCommand('getItemCounts', function(source)
    local itemNames = {"apple", "banana", "orange"}
    local itemCount = exports['qb-inventory']:GetItemCount(source, itemNames)
    if itemCount and itemCount > 0 then
        print('You have '..itemCount..' of the items: '..table.concat(itemNames, ", "))
    else
        print('No items found with the names: '..table.concat(itemNames, ", "))
    end
end, true)
```
