---
description: It's medicinal? Sure it is...
---

# 🌿 qb-weed

## Introduction

* Handles the logic for growing weed in a player-owned house
* Uses [qb-houses.md](qb-houses.md "mention") for the location for players to grow weed
* Multi-stage growing (plant gets bigger overtime)
* Saves status in the SQL to be able to keep progress through restarts&#x20;

## Configuration

```lua
QBWeed.Plants = {
    ["og-kush"] = {
        ["label"] = "OGKush 2g", -- plant label shown in menu
        ["item"] = "weed_og-kush", -- item you get from the plant
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c", -- prop for stage
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g" -- designate the highest stage for plant
    },
    ["amnesia"] = {
        ["label"] = "Amnesia 2g",
        ["item"] = "weed_amnesia",
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c",
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g"
    },
    ["skunk"] = {
        ["label"] = "Skunk 2g",
        ["item"] = "weed_skunk",
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c",
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g"
    },
    ["ak47"] = {
        ["label"] = "AK47 2g",
        ["item"] = "weed_ak47",
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c",
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g"
    },
    ["purple-haze"] = {
        ["label"] = "Purple Haze 2g",
        ["item"] = "weed_purple-haze",
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c",
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g"
    },
    ["white-widow"] = {
        ["label"] = "White Widow 2g",
        ["item"] = "weed_white-widow",
        ["stages"] = {
            ["stage-a"] = "bkr_prop_weed_01_small_01c",
            ["stage-b"] = "bkr_prop_weed_01_small_01b",
            ["stage-c"] = "bkr_prop_weed_01_small_01a",
            ["stage-d"] = "bkr_prop_weed_med_01b",
            ["stage-e"] = "bkr_prop_weed_lrg_01a",
            ["stage-f"] = "bkr_prop_weed_lrg_01b",
            ["stage-g"] = "bkr_prop_weed_lrg_01b",
        },
        ["highestStage"] = "stage-g"
    },
}

QBWeed.Props = { -- prop list to check if near to allow/deny planting
    ["stage-a"] = "bkr_prop_weed_01_small_01c",
    ["stage-b"] = "bkr_prop_weed_01_small_01b",
    ["stage-c"] = "bkr_prop_weed_01_small_01a",
    ["stage-d"] = "bkr_prop_weed_med_01b",
    ["stage-e"] = "bkr_prop_weed_lrg_01a",
    ["stage-f"] = "bkr_prop_weed_lrg_01b",
    ["stage-g"] = "bkr_prop_weed_lrg_01b",
}
```
