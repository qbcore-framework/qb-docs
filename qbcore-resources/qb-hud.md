---
description: Keep track of your vitals in style
---

# ℹ qb-hud

## Introduction

* Player heads-up display that tracks vital information such as health, armor, food level, thirst level, etc.

{% hint style="info" %}
The settings menu uses keymapping and is defaulted to "I"
{% endhint %}

{% hint style="danger" %}
Player settings are stored using KVP which is located on the player's machine so the only way to reset them is by using the in-game menu buttons
{% endhint %}

## Preview

![](https://user-images.githubusercontent.com/91661118/149598723-b34bb93d-8885-4b3a-a0cc-ab68d756a449.PNG)

![](https://user-images.githubusercontent.com/91661118/143668930-e9475c53-284c-4054-ad9c-88aa98f76768.png)

## FAQ&#x20;

<details>

<summary>Why do my borders not align with the maps?</summary>

Most of the time it generally means your safezone is not set to default in your GTA settings. (Settings/Display/"Restore Defaults")

</details>

<details>

<summary>How do I enable dev mode?</summary>

Simple! All you have to do is type /admin and navigate through the menu to the last section called "Developer Options" and inside there you should see "Dev Mode", this will keep you invincible and add a cool developer icon in your circles/radials

</details>

<details>

<summary>What does the purple circle/radial do?</summary>

That is your harness indicator! When you have the item "harness" in your inventory and while in a vehicle it will appear. Also, when you use your item "harness", the circle/radial will reflect the amount of uses left and decrease over time.

</details>

## Useful events

### hud:server:GainStress

* Source code for reference

```etlua
RegisterNetEvent('hud:server:GainStress', function(amount)
    local src = source
    local Player = QBCore.Functions.GetPlayer(src)
    local newStress
    if not Player or (Config.DisablePoliceStress and Player.PlayerData.job.name == 'police') then return end
    if not ResetStress then
        if not Player.PlayerData.metadata['stress'] then
            Player.PlayerData.metadata['stress'] = 0
        end
        newStress = Player.PlayerData.metadata['stress'] + amount
        if newStress <= 0 then newStress = 0 end
    else
        newStress = 0
    end
    if newStress > 100 then
        newStress = 100
    end
    Player.Functions.SetMetaData('stress', newStress)
    TriggerClientEvent('hud:client:UpdateStress', src, newStress)
    TriggerClientEvent('QBCore:Notify', src, Lang:t("notify.stress_gain"), 'error', 1500)
end)
```

* How to use

```etlua
TriggerServerEvent('hud:server:GainStress', --[[number]])) 
OR
TriggerServerEvent('hud:server:GainStress', math.random(1, 3))
```

{% hint style="info" %}
If you trigger this client side you don't need to define source
{% endhint %}

### hud:server:RelieveStress

* Source code for reference

```etlua
RegisterNetEvent('hud:server:RelieveStress', function(amount)
    local src = source
    local Player = QBCore.Functions.GetPlayer(src)
    local newStress
    if not Player then return end
    if not ResetStress then
        if not Player.PlayerData.metadata['stress'] then
            Player.PlayerData.metadata['stress'] = 0
        end
        newStress = Player.PlayerData.metadata['stress'] - amount
        if newStress <= 0 then newStress = 0 end
    else
        newStress = 0
    end
    if newStress > 100 then
        newStress = 100
    end
    Player.Functions.SetMetaData('stress', newStress)
    TriggerClientEvent('hud:client:UpdateStress', src, newStress)
    TriggerClientEvent('QBCore:Notify', src, Lang:t("notify.stress_removed"))
end)
```

* How to use

```etlua
TriggerServerEvent('hud:server:RelieveStress', --[[number]])) 
OR
TriggerServerEvent('hud:server:RelieveStress', math.random(1, 3))
```
