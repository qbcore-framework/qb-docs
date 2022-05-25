---
description: Buy & customize your dream home!
---

# 🏡 qb-houses

## Introduction

* Allows players to purchase homes that are created by those with the real-estate job. They can decorate them, have a personal garage and share keys with their friends

{% hint style="success" %}
By default, this resource uses the 16 free shells found in [qb-interior.md](qb-interior.md "mention")
{% endhint %}

## Preview

![Viewing a house will bring up this UI which shows the cost and buy/cancel buttons](https://camo.githubusercontent.com/c5c5874ac7afb5cadd01e0d0bc89ce1ec253603b2ccf357d4a757ced724f625e/68747470733a2f2f696d6775722e636f6d2f3465516e5271412e706e67)

![Use the radial menu to set locations in your house such as stash and outfit access](https://camo.githubusercontent.com/ac17292df498da4a01df3e5362d4d37c110c43a7896f5fa161d79aaba078738c/68747470733a2f2f696d6775722e636f6d2f475470616c59572e706e67)

![Personalize your house by using the in-game decorator](https://camo.githubusercontent.com/fc66647c3b51a173e277dfd20cf5265146a66ee7b470e37d1ea5713fa34008d4/68747470733a2f2f696d6775722e636f6d2f666d563067504d2e706e67)

## Configuration

### Generic

```lua
Config = {}
Config.MinZOffset = 30 -- how far under the ground shells will spawn
Config.RamsNeeded = 2 -- how many stormram items are needed to raid a house
Config.UnownedBlips = false -- enable/disable unowned house blips on the map
Config.Houses = {} -- populates automatically on server start
Config.Targets = {} -- populates automatically on server start
Config.Furniture = {} -- pre-filled with tons of options
```

### Shells

* Found in qb-houses/client/main.lua at line 697

```lua
local function getDataForHouseTier(house, coords)
```

## Commands

* /decorate - Allows the player decorate the house
* /createhouse \[price] \[tier] - Creates a house and saves it to database
* /addgarage - Adds a garage to nearby house
* /enter - Enters the nearby house
* /ring - Rings the bell of nearby house

## Items

* police\_stormram - Allows on-duty police to enter and search a player's home
