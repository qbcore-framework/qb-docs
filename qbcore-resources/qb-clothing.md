---
description: Ohhh, looking fly!
---

# 👕 qb-clothing

## Introduction

This resource manages outfits and creating your character. Easily configurable by location in the config and features a minimalistic UI for users to understand.

{% hint style="warning" %}
This resource does not manage replacement or add-on clothes! It only manages outfits if you want to learn more about replacement clothes in FiveM click [here](https://forum.cfx.re/t/how-to-streaming-new-hairstyles-for-characters-step-by-step-for-dummies/1048980).
{% endhint %}

## Preview

![](https://user-images.githubusercontent.com/66404074/153545004-6337e685-d3a5-478c-8fa2-e50f4b1d2030.png)

## Configuration

### Player Models

`Config.ManPlayerModels` and `Config.WomanPlayerModels` are [ped models](https://docs.fivem.net/docs/game-references/ped-models/) available for the player to change to.

### Locations&#x20;

```etlua
Config.Stores = {
    [1] = {
        shopType = 'clothing', -- clothing/barber/surgeon
        coords = vector3(1693.32, 4823.48, 41.06),
        width = 2,
        length = 2
    },
}
```

{% hint style="info" %}
This uses a [BoxZone](https://github.com/mkafrin/PolyZone/wiki/BoxZone) the more width and length the bigger the zone&#x20;
{% endhint %}

### Clothing Rooms

```etlua
Config.ClothingRooms = {
    [1] = {
        requiredJob = 'police', -- Can be job or gang name
        isGang = true/false, -- If above is a gang name then make true
        coords = vector3(454.43, -988.85, 30.69),
        width = 2,
        length = 2,
        cameraLocation = vector4(454.42, -990.52, 30.69, 358.48)
    },
}
```

### Job Outfits&#x20;

```etlua
Config.Outfits = {
    ['police'] = { -- Job/Gang
        ['male'] = { -- Gender
            [0] = { -- Grade Level
                [1] = { -- Outfits
                    outfitLabel = 'Short Sleeve',
                    outfitData = {
                        ['pants'] = {item = 24, texture = 0}, -- Pants
                        ['arms'] = {item = 19, texture = 0}, -- Arms
                        ['t-shirt'] = {item = 58, texture = 0}, -- T Shirt
                        ['vest'] = {item = 0, texture = 0}, -- Body Vest
                        ['torso2'] = {item = 55, texture = 0}, -- Jacket
                        ['shoes'] = {item = 51, texture = 0}, -- Shoes
                        ['accessory'] = {item = 0, texture = 0}, -- Neck Accessory
                        ['bag'] = {item = 0, texture = 0}, -- Bag
                        ['hat'] = {item = -1, texture = -1}, -- Hat
                        ['glass'] = {item = 0, texture = 0}, -- Glasses
                        ['mask'] = {item = 0, texture = 0} -- Mask
                    }
                },
            }
        }
    }
}
```
