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

Items support additional information that can be added to them via an `info` attribute. This information will display on the item when the player hovers over it in a key,value pair format. You can also add a special `display` keyword and make it false to hide any data inside the info table from being shown!

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

This function retrieves the player's inventory from the database using their `citizenid`, decodes it from JSON, and builds a structured table of items using data from `QBCore.Shared.Items`. If an item is found that no longer exists in the shared items table, it is skipped and logged to the console. The returned inventory contains detailed information like item label, weight, image, and usage properties

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

Saves the player's current inventory to the database by serializing item data into JSON format. Supports both online and offline player data

* source: `number`
* offline: `boolean`

```lua
RegisterCommand('saveInv', function(source)
    exports['qb-inventory']:SaveInventory(source, false)
end)
```

## ClearInventory

Clears a player's inventory, optionally preserving specific items by name. Updates player data, logs the action, and removes the currently equipped weapon if applicable

* source: `number`
* filterItems: `string | table`

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

## ClearStash

Empties all items from the specified stash inventory and updates the database to reflect the cleared state

* identifier: `string`

```lua
RegisterCommand("clearstash", function(source, args, raw)
    local stashId = args[1]
    exports['qb-inventory']:ClearStash(stashId)
    print("Stash '" .. stashId .. "' has been cleared.")
end, false)
```

## CloseInventory

Closes the specified inventory and marks the player as no longer busy, then notifies the client to close the inventory UI

* source: `number`
* identifier: `string`

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

Opens a specified inventory or the player's own if no identifier is given. Prevents access if the inventory is already in use, initializes it if needed, and sends formatted inventory data to the client for display

* source: `number`
* identifier: `string | optional`
* data: `table | optional`

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

Opens another player's inventory for viewing or interaction, formatting their data for display and marking their state as busy to prevent conflicts

* source: `number`
* playerId: `number`

```lua
RegisterCommand('openplayerinv', function(source, args)
    local playerId = tonumber(args[1])
    exports['qb-inventory']:OpenInventoryById(source, playerId)
end, true)
```

{% hint style="info" %}
`OpenInventoryById` will close the target players inventory (if open) and lock it via state. It will then unlock when the opening player closes it
{% endhint %}

## CreateInventory

Creates and registers a new inventory using the provided identifier and initialization data if it doesn't already exist

* identifier: `string`
* data: `table`

```lua
RegisterCommand("createinv", function(source, args)
    local id = args[1]
    if not id then
        print("Usage: /createinv [identifier]")
        return
    end
    exports['qb-inventory']:CreateInventory(id, {
        label = "Custom Inventory",
        maxweight = 100000,
        slots = 30
    })
    print("Inventory '" .. id .. "' created.")
end, false)
```

## RemoveInventory

Deletes the inventory associated with the specified identifier from the in-memory registry

* identifier: `string`

```lua
RegisterCommand("removeinv", function(source, args)
    local id = args[1]
    exports['qb-inventory']:RemoveInventory(id)
    print("Inventory '" .. id .. "' removed.")
end, false)
```

## CreateShop

Registers one or multiple shops by storing their data, including name, label, coordinates, item slots, and available items, into the global shop registry

* shopData: `table`&#x20;
  * name: `string`
  * label: `string`
  * coords: `vector3`
  * slots: `number`
  * items: `table`

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

Opens a shop inventory for the player if they're within range, formatting the shop data for client display and sending it alongside the player's current inventory

* source: `number`
* name: `string`

```lua
RegisterCommand('openShop', function(source)
    exports['qb-inventory']:OpenShop(source, 'testShop')
end)
```

## CanAddItem

Determines whether a specified item and amount can be added to a player or inventory, checking both weight limits and slot availability. Returns false with a reason if constraints are exceeded

* source: `number`
* item: `string`
* amount: `number`
* <mark style="color:yellow;">returns</mark>: `boolean`

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

Adds an item to a player or specific inventory, accounting for weight limits and available slots. Logs the action and returns whether it succeeded

* identifier: `number`
* item: `string`
* amount: `number`
* slot: `number | boolean`
* info: `table | boolean`
* reason: `string`
* <mark style="color:yellow;">returns</mark>: `boolean`

```lua
RegisterCommand('addItem', function(source, args)
    local itemName = args[1]
    if not itemName then return end
    exports['qb-inventory']:AddItem(source, itemName, 1, false, false, 'qb-inventory:testAdd')
end, true)
```

## RemoveItem

Removes a specified amount of an item from a player or inventory, optionally from a specific slot. Updates data and logs the removal

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

Sets the item list for a specified player, drop, or custom inventory, updating in-memory data and logging the change for auditing purposes

* source: `number`
* items: `table`

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

Sets a specific key-value pair in a player's item data and updates the player's inventory with the modified item. If a slot number is provided, it directly targets the item in that slot. Otherwise, it uses `GetItemByName` to find the first matching item by name

* source: `number`
* itemName: `string`
* key: `string`
* val: `string | table`&#x20;
* slot: `number` (optional)
* <mark style="color:yellow;">returns</mark>: `boolean`

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

Triggers the use function of a specified usable item if it exists, passing any additional arguments to the item's handler

* itemName: `string`
* . . . : `function`

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

Checks whether a player possesses a specific item or set of items in their inventory, optionally verifying that the required amount is met for each

{% hint style="success" %}
This export is also available to use on the client
{% endhint %}

* source: `number`
* items: `string | table`
* amount: `number`
* <mark style="color:yellow;">returns</mark>: `boolean`

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

Calculates and returns the remaining weight capacity in a player's inventory. Returns 0 if the player is not found or the source is invalid

* source: `number`
* <mark style="color:yellow;">returns</mark>: `number`

```lua
RegisterCommand('getFreeWeight', function(source)
    local freeWeight = exports['qb-inventory']:GetFreeWeight(source)
    print('Free Weight: ' .. freeWeight)
end, true)
```

## GetTotalWeight

Calculates and returns the total weight of all items in the inventory, accounting for item quantities

* items: `table`
* <mark style="color:yellow;">returns</mark>: `number`

```lua
RegisterCommand("checkweight", function(source, args, raw)
    local Player = QBCore.Functions.GetPlayer(source)
    if not Player then return end
    local inventory = Player.PlayerData.items
    local totalWeight = exports['qb-inventory']:GetTotalWeight(inventory)
    print(("Total Inventory Weight: ", totalWeight)
end, false)
```

## GetSlots

Returns the number of used and available slots in a player's inventory, a custom inventory, or a drop, based on the provided identifier

* identifier: `number | string`
* <mark style="color:yellow;">returns</mark>: `number`, `number`

```lua
RegisterCommand('getSlots', function(source, args)
    local invId = args[1]
    if not invId then return end
    local slotsUsed, slotsFree = exports['qb-inventory']:GetSlots(invId)
    print('Slots Used: ' .. slotsUsed, 'Slots Free: ' .. slotsFree)
end, true)
```

## GetSlotsByItem

Returns a list of all inventory slots containing the specified item, ignoring case sensitivity

* items: `table`
* itemName: `string`
* <mark style="color:yellow;">returns</mark>: `table`

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

Finds and returns all inventory slots that contain a specified item by name, ignoring case sensitivity

* items: `table`
* itemName: `string`
* <mark style="color:yellow;">returns</mark>: `number`

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

Retrieves the item from a player's inventory at the specified slot, or returns nil if the slot is empty or the player is not found

* source: `number`
* slot: `number`
* <mark style="color:yellow;">returns</mark>: `table`

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

Retrieves the first instance of a specified item from a player's inventory by name, returning its data if found

* source: `number`
* item: `string`
* <mark style="color:yellow;">returns</mark>: `table`

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

Retrieves all instances of a specified item from a player's inventory, returning a list of matching items by name

* source: `number`
* item: `string`
* <mark style="color:yellow;">returns</mark>: `table`

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

Calculates the total quantity of one or more specified items in a player's inventory, supporting both single item names and tables of item names

* source: `number`
* items: `string | table`
* <mark style="color:yellow;">returns</mark>: `number`

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

## GetInventory

Retrieves the inventory object associated with the given identifier, or `nil` if not found

* identifier: `string`
* <mark style="color:yellow;">returns</mark>: `table` | `nil`

```lua
RegisterCommand("getinv", function(source, args)
    local id = args[1]
    local inv = exports['qb-inventory']:GetInventory(id)
    if inv then
        print("Inventory '" .. id .. "' has " .. tostring(#inv.items) .. " items")
    else
        print("Inventory not found")
    end
end, false)
```
