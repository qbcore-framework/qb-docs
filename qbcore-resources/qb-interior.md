---
description: Which shell will it be?
---

# 🏠 qb-interior

## Introduction

* Handles all the logic for spawning shell models by exporting functions that can be called in other client-side files

## Configuration

{% hint style="success" %}
This resource requires no configuration unless you want to add more exports
{% endhint %}

## What's included?

{% hint style="info" %}
The below pdf file shows which shell models come by default
{% endhint %}

{% file src="../.gitbook/assets/k4mb1shellstarter.pdf" %}

{% hint style="success" %}
Optionally, this resource comes pre-configured for all of [K4MB1](https://www.k4mb1maps.com/) shells!
{% endhint %}

## Usage example

```lua
RegisterCommand('spawnshell', function()
    local ped = PlayerPedId()
    local coords = GetEntityCoords(ped)
    local shell = exports['qb-interior']:CreateApartmentShell(coords)
end)
```
