---
description: Manage your server and players efficiently
---

# 🔧 qb-adminmenu

## Introduction

* The admin menu offers a wide range of capabilities and utilizes the popular menu resource menuV as a dependency. The base permission level for opening it is admin but can also be accessed with a god level permission as well. The menu is easily expandible and allows for as many options as the user desires

## Preview

![](../.gitbook/assets/adminmenu.png)

## Commands

<details>

<summary>/admin <strong>-</strong> opens the admin menu</summary>

Opens the admin menu

**Permission level:** admin

</details>

<details>

<summary>/blips - toggles player blips</summary>

Adds a blip to the map for all players. Useful to monitor player locations.

**Permission level:** admin

</details>

<details>

<summary>/names - toggles player names</summary>

Shows player names and IDs above heads

**Permission level:** admin

</details>

<details>

<summary>/coords - shows your current coords</summary>

Shows your current coordinates in `vector3(x, y, z)` format

**Permission level:** admin

</details>

<details>

<summary>/maxmods - sets vehicle to max mods</summary>

Sets the current vehicle to have maximum performance modifications

**Permission level:** admin

</details>

<details>

<summary>/noclip - toggles noclip</summary>

Toggles noclip

**Permission level:** admin

</details>

<details>

<summary>/admincar - adds current vehicle to garage</summary>

Saves the current vehicle to the database table `player_vehicles` allowing access to the vehicle in the garage

**Permission level:** admin

</details>

<details>

<summary>/announce [message] - creates an announcement</summary>

Creates an announcement to be sent to all players in the chat.&#x20;

**Permission level:** admin

* **message** - (required) The message to send

</details>

<details>

<summary>/report [message] - create a report to staff</summary>

Sends a message to staff in the chat and stores the message as a report

**Permission level:** user

* **message** - (required) The message to send

</details>

<details>

<summary>/reportr [message] - replies to a user report</summary>

Replies to a user report with the given `message`

**Permission level:** admin

* **message** - (required) The message to send in the reply

</details>

<details>

<summary>/reporttoggle - opt in/out of receiving player reports</summary>

Opt in/out of receiving player reports in chat

**Permission level:** admin

</details>

<details>

<summary>/staffchat [message] - sends a staff-only message</summary>

Sends a message in chat visible only to users with the 'admin' permission level

**Permission level:** admin

* **message** - (required) The message to send

</details>

<details>

<summary>/warn [id] [reason] - warn a player</summary>

Sends a message to the player with the given `id` with the `reason` given. Also, adds a warning against the player in the database table `player_warns`

**Permission level:** admin

* **id** - (required) The id of the player being warned
* **reason** - (required) The reason for giving a warning

</details>

<details>

<summary>/checkwarns [id] [opt: number] - view a warning for a given player</summary>

Checks for existing warnings against a player with the given `id`. If no warning number is given in the command, it will display the number of warnings the player has received. If a warning number is given in the command, it will display that warning.

**Permission level:** admin

* **id** - (required) The id of the player being checked
* **number** - (optional) The warning number (1, 2, 3, etc...)

</details>

<details>

<summary>/delwarn [id] [number] - deletes a warning from a player</summary>

Deletes a warning from a player and removes the database entry

**Permission level:** admin

* **id** - (required) The id of the player
* **number** - (required) The warning number to be deleted (1, 2, 3 etc...)

</details>

<details>

<summary>/givenuifocus [id] [hasFocus] [hasCursor] - Sets nuifocus state for player</summary>

This command sets the NUI focus state for a player with the given `id`. This allows you to manually set the following native: [https://docs.fivem.net/natives/?\_0x5B98AE30](https://docs.fivem.net/natives/?\_0x5B98AE30)\
Useful if a player is stuck in an NUI overlay.

**Permission level:** admin

* **id** - (required) The id of the player
* **hasFocus** - (required) \[true/false] Whether the NUI has focus or not
* **hasCursor** - (required) \[true/false] Whether the player has cursor when using NUI

</details>

<details>

<summary>/setmodel [model] [id] - changes the players ped model</summary>

Changes the ped `model` of the player with the given `id`.

**Permission level:** admin

* **model** - (required) The ped model to change to
* **id** - (required) The id of the player whos ped model is being changed

</details>

<details>

<summary>/setspeed [opt: speed] - sets players foot speed</summary>

Sets your foot speed between default and "fast"

**Permission level:** admin

* **speed** - (optional) \["fast"] will set foot speed to "fast". If this argument is left blank it will set foot speed to "normal"

</details>

<details>

<summary>/kickall - kick all players from server</summary>

Kicks all players from the server.

**Permission level:** god

</details>

<details>

<summary>/setammo [amount] [opt: weapon] - set weapon ammo</summary>

Sets the ammo amount for current gun in hand or `weapon` if given

**Permission level:** admin

* **amount** - (required) The amount of ammo to set
* **weapon** - (optional) The weapon to set the ammo for. Will set ammo for current gun in hand if left blank

</details>

<details>

<summary>/vector2 - Copies vector2 to clipboard</summary>

Copies `vector2(x, y)` to clipboard of your current coordinates.

**Permission level:** admin

</details>

<details>

<summary>/vector3 - Copies vector3 to clipboard</summary>

Copies `vector3(x, y, z)` to clipboard of your current coordinates

**Permission level:** admin

</details>

<details>

<summary>/vector4 - Copies vector4 to clipboard</summary>

Copies `vector4(x, y, z, w)` to clipboard of your current coordinates

**Permission level:** admin

</details>

<details>

<summary>/heading - Copies heading</summary>

Copies heading `w` to clipboard of your current heading (the direction you are facing)

**Permission level:** admin

</details>
