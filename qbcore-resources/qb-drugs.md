---
description: Got any of that good stuff?
---

# 💊 qb-drugs

## Introduction

* Create dealers that players can interact with and purchase items or accept delivery jobs to earn rewards. Also included is "corner-selling" which allows players to sell drugs to NPC's for configured prices

## Configuration

### General

```lua
Config = {}
Config.Dealers = {} -- auto-populates on resource start
Config.MinimumDrugSalePolice = 2 -- minimum police allowed to corner sell
```

### Products

```lua
Config.Products = { -- products availabe to buy from a dealer
    [1] = {
        name = "weed_white-widow", -- item name
        price = 15, -- how much it costs
        amount = 150, -- amount available in stock
        info = {}, -- item info (none)
        type = "item", -- item type
        slot = 1, -- inventory slot item will show in
        minrep = 0, -- how much rep needed to buy this item
    },
}
```

### Corner selling item list

```lua
Config.CornerSellingDrugsList = { -- items available to be corner sold
    "weed_white-widow",
    "weed_skunk",
    "weed_purple-haze",
    "weed_og-kush",
    "weed_amnesia",
    "weed_ak47",
    "crack_baggy",
    "cokebaggy",
    "meth"
}
```

### Corner selling pricing

```lua
Config.DrugsPrice = {
    ["weed_white-widow"] = { -- item name (reference above)
        min = 15, -- minimum price could sell for
        max = 24, -- maximum price could sell for
    },
}
```

### Delivery locations

```lua
Config.DeliveryLocations = { -- List of deliveries players can get from dealers
    [1] = {
        ["label"] = "Stripclub", -- delivery location name
        ["coords"] = vector3(106.24, -1280.32, 29.24), -- delivery location coords
    },
}
```

### Delivery rewards

```lua
Config.DeliveryItems = { -- reward items for deliveries (reference above)
    [1] = {
        ["item"] = "weed_brick", -- item name
        ["minrep"] = 0, -- minimum rep needed to get this item
    },
}
```

## Commands

* /newdealer - Create a new dealer at your coordinates
* /deletedealer - Delete a dealer from the database
* /dealers - Get a list of current dealers
* /dealergoto - Teleport to a dealer
