---
description: Please! No more left turns!
---

# 🏁 qb-lapraces

## Introduction

* Authorized players can create races that show up on the race app of [qb-phone.md](qb-phone.md "mention")

## Preview

## Configuration

### General

```lua
Config = {}
Config.RaceSetupAllowed = true -- changes dynamically, don't edit this
Config.WhitelistedCreators = {
    "CITIZENID", -- List the player citizenid's allowed to create races
}
```

## Commands

* /cancelrace - Cancel the currently active race
* /togglesetup - Toggle the race creator
