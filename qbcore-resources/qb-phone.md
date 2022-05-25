---
description: Look up would ya?
---

# 📱 qb-phone

## Introduction

* Receive emails
* Post tweets
* Post advertisements
* Player to player communication via calling and texting
* Check their stored vehicles or tracking down lost ones on the [qb-garages.md](qb-garages.md "mention") app
* Check bank balance and pay bills on the [qb-banking.md](qb-banking.md "mention") app
* Buy/sell/transfer on the [qb-crypto.md](qb-crypto.md "mention") app
* Compete in races through the [qb-lapraces.md](qb-lapraces.md "mention")app
* View owned houses and give out keys on the [qb-houses.md](qb-houses.md "mention") app
* View the amount of specific online jobs
* Take photos and view them in the gallery

## Preview

[![Home](https://camo.githubusercontent.com/8b65eceaf69fb17c2806865c824813a0d6d727482dafdf8ebd8de8b37d2fc003/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3932313637353234353336303932323632352f3932313637353433393738333637333839372f686f6d652e6a7067)](https://camo.githubusercontent.com/8b65eceaf69fb17c2806865c824813a0d6d727482dafdf8ebd8de8b37d2fc003/68747470733a2f2f63646e2e646973636f72646170702e636f6d2f6174746163686d656e74732f3932313637353234353336303932323632352f3932313637353433393738333637333839372f686f6d652e6a7067)              &#x20;

## Configuration

{% hint style="danger" %}
Make sure to add any additional jobs to the config under billing commissions!
{% endhint %}

### General

```lua
Config = {}
Config.MaxSlots = 20 -- maximum amount of home screen application slots
Config.BillingCommissions = { -- list job names and the commission amount they get
    mechanic = 0.10 -- commission percentage
}
Config.Linux = false -- if using linux operating system (stores date vs time)
Config.TweetDuration = 12 -- how many hours to load tweets
Config.RepeatTimeout = 2000 -- timeout in milliseconds before repeating call
Config.CallRepeats = 10 -- how many times the call will repeat before hanging up
```

### Phone applications

```lua
Config.PhoneApplications = {
    ["phone"] = { -- phone application name
        app = "phone", -- phone application name
        color = "#04b543", -- phone application color
        icon = "fa fa-phone-alt", -- phone application icon
        tooltipText = "Phone", -- text that shows when hovering over application
        tooltipPos = "top", -- location of pop-up text when hovering over app
        job = false, -- 
        blockedjobs = {}, -- block specific jobs from accessing this app
        slot = 1, -- the slot the app shows in on the home screen
        Alerts = 0, -- 
    },
}
```

### Application store

{% hint style="danger" %}
This feature is currently under construction and does not function!
{% endhint %}

```lua
Config.StoreApps = {}
```

## Commands

{% hint style="success" %}
Players can change the open phone key via their in-game keybind settings
{% endhint %}

{% hint style="warning" %}
Make sure to add any additional jobs to the config under billing commissions!
{% endhint %}

* /phone - Open phone (keymapped)
* /bill - Allow players to bill others
