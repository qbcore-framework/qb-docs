---
description: To the moon!
---

# 🪙 qb-crypto

## Introduction

* This resource handles the cryptocurrency market for players to be able to buy/sell qbit. It also includes an item called a "cryptostick" that can be exchanged at a configured location for qbit. Some jobs have this item as a random reward already

{% hint style="warning" %}
This resource only works with qb-phone. Without it, players will not be able to buy or sell qbit!
{% endhint %}

## Preview

![](../.gitbook/assets/crypto.png)

## Configuration

```lua
Crypto = {
    Lower = 500, -- Lowest possible crypto worth
    Upper = 5000, -- Highest possible crypto worth
    History = { ["qbit"] = {}}, -- Stores crypto worth history for viewing
    Worth = {["qbit"] = 1000}, -- Starting crypto worth (can add more)
    Labels = {["qbit"] = "Qbit"}, -- Crypto type label (can add more)
    Exchange = { -- Exchange point for cryptosticks
        coords = vector3(1276.21, -1709.88, 54.57),
        RebootInfo = {
            state = false,
            percentage = 0
        },
    },
    -- For auto updating the value of qbit
    Coin = 'qbit',
    RefreshTimer = 10, -- In minutes, so every 10 minutes.
    -- Crashes or luck
    ChanceOfCrashOrLuck = 2, -- This is in % (1-100)
    Crash = {20,80}, -- Min / Max
    Luck = {20,45}, -- Min / Max
    -- If not not Chance of crash or luck
    ChanceOfDown = 30, -- If out of 100 hits less or equal to
    ChanceOfUp = 60, -- If out of 100 is greater or equal to
    CasualDown = {1,10}, -- Min / Max (If it goes down)
    CasualUp = {1,10}, -- Min / Max (If it goes up)
}

Ticker = {
    Enabled = false, -- Enable/disable real life crypto prices
    coin = 'BTC', --- The coin, please make sure you find the actual name, for example: Bitcoin vs BTC, BTC would be correct
    currency = 'USD', -- For example USD, NOK, SEK, EUR, CAD and more here https://www.countries-ofthe-world.com/world-currencies.html
    tick_time = 2, --- Minutes (Minimum is 2 minutes) 20,160 Requests a month, Its recommended to get the free API key so the crypto script doesnt switch on and off if ratelimit is encountered
    Api_key = 'put_api_key_here', -- If you decide to get an api key for the API (https://min-api.cryptocompare.com/pricing) The free plan should be more than enough for 1 Fivem server
    --- Error handle stuff, for more user friendly and readable errors, Don't touch.
    Error_handle = {
        ['fsym is a required param.'] = 'Config error: Invalid / Missing coin name',
        ['tsyms is a required param.'] = 'Config error: Invalid / Missing currency',
        ['cccagg_or_exchange'] = 'Config error: Invalid currency / coin combination', -- For some reason api throws this error if either coin or currency is invalid
    },
}
```

## Commands

* /setcryptoworth - Admin only command to set a crypto types worth
* /checkcryptoworth - Check the current worth of qbit
* /crypto - View your qbit balance and worth

## Items

* cryptostick - Players can take these to the exchange point and get crypto from them
