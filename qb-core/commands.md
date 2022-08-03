---
description: A list of all the commands and their respective resource
---

# ❗ Commands

### AdminMenu

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

### Core

* /tp - teletport to a player
* /tpm - teleport to a marked location
* /togglepvp - toggle PVP on server
* /addpermission - gives a player permisions on server
* /removepermissions - removes a players permissions on server
* /openserver - opens server for everyone
* /closeserver - close the server for people without permissions
* /car - spawns a vehicle
* /dv - deletes current vehicle
* /givemoney - gives money to the person
* /setmoney - sets the amound of money player has
* /job - displays the current job player has
* /setjob - sets a job to a player
* /gang - check players current gang
* /setgang - sets a player to a gang
* /clearinv - clears your inventory
* /ooc - ooc chat command
* /me - shows a message above users head

### Ambulancejob

* /911e - sends a message to ems
* /status - checks the status of a player
* /heal - heals a player
* /revivep - revives closest player
* /revive - revives self (admin only)
* /setpain - sets a pain level to the player (admin only)
* /kill - kills the player (admin only)
* /aheal - admin heal a player

### Police

* /911p - sends an alert to police with location
* /spikestrip - Puts down spike strips
* /grantlicense - give the player next to the officer a license
* /revokelicense - revokes the players license next to the officer
* /911e - sends an alert to the police with location
* /pobject - allows officer to spawn cone/barrier/roadsign/tent/light/delete
* /cuff - cuffing a player next to officer
* /escort - escort a player next to officer
* /callsign - allows officer to set a callsign
* /clearcasings - clears bullet casing in the area
* /jail - sends the player to jail
* /unjail - unjail the player
* /clearblood - clears blood drops in area
* /seizecash - seize cash from the player
* /sc - soft cuff the player (allows player to walk still)
* /cam - allows officer to see cam fotage fom slected spots
* /flagplate - allows speed camras to find a plate flagged
* /unflagplate - removes the flag from the plate
* /plateinfo - shows the info of the plate
* /depot - allows officer to inpound vehicle for a price
* /impound - impounds vehicle without a price
* /paytow - pays the tow driver $500
* /paylawyer - pays a lawyer $500
* /anklet - adds a tracking device to the player
* /ankletlocation - shows location of the player
* /takedrivinglicense - takes the players drivers license
* /takedna - takes the players dna

### Banking

* /givecash - gives the player an amount of cash

### Cityhall

* /drivinglicense - give player a license after a driving test

### Binds

* /binds - allows you to set customs key binds

### Diving

* /divingsuit - uses the diving suit

### Doorlock

* /newdoor - opens UI for creating new door
* /doordebug - debug for doorlocks

### Drugs

* /newdealer - creats a new dealer at a location (front door of house)
* /deletedealer - deales a saved dealer
* /dealers - show list if info on dealers
* /dealergoto - teleport to dealer

### Garbage

* /cleargarbroutes - removes garbo routes for user

### Hotdogjob

* /removestand - removes a hotdog stand

### Housing

* /decorate - opens decorate menu/options
* /createhouse - creates a house at location
* /addgarage - adds garage at location
* /ring - rings a doorbell at location

### Hud

* /cash - displays current cash amount
* /bank - displays current bank amount
* /dev - displays a dev icon

### Inventory

* /resetinv - resets inventory on stash/trunk/glovebox
* /rob - robs closest player
* /giveitem - gives item to a player
* /randomitems - gives random items to a player

### Lapraces

* /cancelrace - cancel the current race
* /togglesetup - turn on or off race setup

### Mechanicjob

* /setvehiclestatus - sets the vehicles status
* /setmechanic - give someone the mechanic job
* /firemechanic - fire a mechanic

### Multicharacter

* /logout - logout of current character
* /closeNUI - closes the multicharacter NUI

### Newsjob

* /newscam - gives player a a news camra
* /newsmic - gives player a news microphone
* /newsbmic - gives player a boom microphone

### Phone

* /setmetadata - sets the players metadata
* /bill - sends a bill\* /invoice to player

### RadialMenu

* /getintrunk - Gets in the trunk
* /putintrunk - puts a player in the trunk (kidnap)

### Smallresources

* /resetarmor - resets the armor
* /resetparachute - resets a parachute
* /testwebhook - test to see if webhook for logs is working
* /id - displays your id

### Streetrace

* /createrace - starts a street race
* /stoprace - stops current street race
* /quitrace - quits the current street race
* /startrace - starts the current street race

### Towjob

* /npc - Toggles a tow job from a npc
* /tow - puts closes vehicle on flatbed (must be behind truck)

### Traphouse

* /multikeys - gives keys to another player

### Vehiclefailure

* /fix - fixes current vehicle

### Vehiclekeys

* /engine - toggles engine on/off
* /givekeys - gives keys to a player
* /addkeys - adds keys to that player
* /removekeys - removes keys from player

### Vehicleshop

* /transferVehicle - gift or sell your vehicle to someone

### Weapons

* /repairweapon - repairs a weapon
