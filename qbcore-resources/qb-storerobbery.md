---
description: Put the money in the bag!
---

# 🔫 qb-storerobbery

## Introduction

* Allows the player to rob the many stores around the city. When they rob the store, they lockpick the cash registers which uses [qb-lockpick.md](qb-lockpick.md "mention"). Once both registers are hit, there is a chance to get a sticky note for the safe code. If the store does not have an electronic safe, it will use the [safecracker](https://github.com/qbcore-framework/safecracker) minigame. Players will get "markedbills" for both the registers and safes
* Cops get called and can use the `camid` provided to view the specified camera more info on that in [qb-policejob.md](qb-policejob.md "mention")

## Configuration

### General

```lua
Config.minEarn = 100 -- minimum markedbills worth
Config.maxEarn = 450 -- max markedbills worth
Config.RegisterEarnings = math.random(Config.minEarn, Config.maxEarn) -- Randomized earnings
Config.MinimumStoreRobberyPolice = 2 -- minimum police needed to start the robbery
Config.resetTime = (60 * 1000) * 30 -- cooldown between robberies in minutes
Config.tickInterval = 1000 -- the time between register checks
```

### Registers

```lua
Config.Registers = {
    [1] = {
        vector3(-47.24,-1757.65, 29.53), -- register location
        robbed = false, -- dynamically changed, don't edit
        time = 0, -- dynamically changed, don't edit
        safeKey = 1, -- index that references the safes table
        camId = 4 -- alerts the cops with the camera number to view
    }
}
```

### Safes

{% hint style="success" %}
If safe type is keypad, then it will open the keypad UI to enter a password or if the type is padlock then it will start the UI for the safecracker mini game
{% endhint %}

```lua
Config.Safes = {
    [1] = {
        vector4(-43.43, -1748.3, 29.42, -- safe location
        type = "keypad", -- safe type keypad/padlock
        robbed = false, -- dynamically changed, don't edit
        camId = 4 -- alerts the cops with the camera number to view
    }
}
```
