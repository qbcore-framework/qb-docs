---
description: Hot dogs! Get your hot dogs here!
---

# 🌭 qb-hotdogjob

## Introduction

* Allows players to rent a hot dog cart, play a mini game to make hot dogs and sell them to NPC's

{% hint style="warning" %}
This resource relies on [qb-keyminigame.md](qb-keyminigame.md "mention") otherwise it won't work
{% endhint %}

## Configuration

### General

```lua
Config = {}
Config.StandDeposit = 250 -- how much it costs to rent a cart
Config.MyLevel = 1
Config.MaxReputation = 200
```

### Locations

```lua
Config.Locations = {
    ["take"] = { -- where players rent the cart
        coords = vector4(39.31, -1005.54, 29.48, 240.57),
    },
    ["spawn"] = { -- where the cart spawns after rental
        coords = vector4(38.15, -1001.65, 29.44, 342.5),
    },
}
```

### Hot dog types & prices

```lua
Config.Stock = {
    ["exotic"] = { -- the type or "quality" of hot dog
        Current = 0, -- this increases/decreases as players make hot dogs
        Max = {
            [1] = 15, -- max amount of hot dogs a player can make based on level
            [2] = 30,
            [3] = 45,
            [4] = 60,
        },
        Label = Lang:t("info.label_a"),
        Price = {
            [1] = { -- the players level
                min = 8, -- minimum amount can sell for
                max = 12, -- maximum amount can sell for
            },
            [2] = {
                min = 9,
                max = 13,
            },
            [3] = {
                min = 10,
                max = 14,
            },
            [4] = {
                min = 11,
                max = 15,
            },
        }
    },
    ["rare"] = {
        Current = 0,
        Max = {
            [1] = 15,
            [2] = 30,
            [3] = 45,
            [4] = 60,
        },
        Label = Lang:t("info.label_b"),
        Price = {
            [1] = {
                min = 6,
                max = 9,
            },
            [2] = {
                min = 7,
                max = 10,
            },
            [3] = {
                min = 8,
                max = 11,
            },
            [4] = {
                min = 9,
                max = 12,
            },
        }
    },
    ["common"] = {
        Current = 0,
        Max = {
            [1] = 15,
            [2] = 30,
            [3] = 45,
            [4] = 60,
        },
        Label = Lang:t('info.label_c'),
        Price = {
            [1] = {
                min = 4,
                max = 6,
            },
            [2] = {
                min = 5,
                max = 7,
            },
            [3] = {
                min = 6,
                max = 9,
            },
            [4] = {
                min = 7,
                max = 9,
            },
        }
    },
}
```
