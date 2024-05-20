---
description: A list of all the commands and their respective resource
---

# ❗ Commands

## QBCore.Commands.Add

This function allows you to register a command with a specified user level

```lua
QBCore.Commands.Add(name, help, arguments, argsrequired, callback, permission, ...)
```

* name: `string`
* help: `string`
* arguments: `table`
* argsrequired: `boolean`
* callback: `function`
* permission: `string`

Example:

```lua
local arguments = {
    { name = 'arg 1', help = 'This will give helpful hints on what arg is for' },
    { name = 'arg 2', help = 'This will give helpful hints on what arg is for' }
}

local argsRequired = true -- if this is true the command won't work without args entered

QBCore.Commands.Add('test', 'Trigger a test command', arguments, argsRequired, function(source)
    print('Congrats, you made a test command that anyone can trigger!')
end, 'user')
```

## QBCore.Commands.Refresh

This function will trigger a refresh of all commands suggestions. This is helpful for when setting permissions to a higher level, it will refresh the suggestions list so the player can now see the new commands they have access to!

```lua
QBCore.Commands.Refresh(source)
```

* source: `number`

Example:

```lua
RegisterCommand('refreshCommands', function()
    QBCore.Commands.Refresh(source)
    print('You have refreshed all command suggestions for yourself')
end, true)
```

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

<details>

<summary>/tp [id / x] [opt: y] [opt: z]- teleport to player or location</summary>

Teleports you to either a player with the given `id` or to a given `x, y, z` location

**Permission level:** admin

* **id or x** - (required) The player id or x coordinate
* **y** - (optional) The y coordinate (required if using x for the first argument)
* **z** - (optional) The z coordinate (required if using x for the first argument)

</details>

<details>

<summary>/tpm - teleport to a marked location</summary>

Teleports you to the marked location on the map.&#x20;

**Permission level:** admin

</details>

<details>

<summary>/togglepvp - toggle PVP on server</summary>

Toggles Player vs Player mode on the server

**Permission level:** admin

</details>

<details>

<summary>/addpermission [id] [permission] - gives a player a permission</summary>

Gives a player with the given `id` the given `permission` level. The player must be online.

**Permission level:** god

</details>

<details>

<summary>/removepermission [id] [permission] - removes a player permission</summary>

Removes the given `permission` from the player with the given `id`. The player must be online.

**Permission level:** god

</details>

<details>

<summary>/openserver - open the server for everyone</summary>

Opens the server allowing everyone to join.

**Permission level:** admin

</details>

<details>

<summary>/closeserver [reason] - close the server for people without permission</summary>

Closes the server for people without the correct permission. Kicks any players currently online without the required permission giving the `reason` in the kick message.&#x20;

**Permission level:** admin

</details>

<details>

<summary>/car [model] - spawns a vehicle</summary>

Spawns a vehicle of the given `model` type.

**Permission level:** admin

</details>

<details>

<summary>/dv - delete vehicle</summary>

Deletes the vehicle you are sitting in or deletes all vehicles within 5.0 units of your position.

**Permission level:** admin

</details>

<details>

<summary>/givemoney [id] [type] [amount] - give money to a player</summary>

Gives money to a player

**Permission level:** admin

* **id** - (required) The `id` of the player
* **type** - (required) The money type \[cash, bank etc...]
* **amount** - (required) The amount to give

</details>

<details>

<summary>/setmoney [id] [type] [amount] - set the amount of money a player has</summary>

Sets the amount of money a player has.

**Permission level:** admin

* **id** - (required) The `id` of the player
* **type** - (required) The money type \[cash, bank etc...]
* **amount** - (required) The amount to set

</details>

<details>

<summary>/job - display your current job</summary>

Displays your current job name and grade

**Permission level:** user

</details>

<details>

<summary>/setjob [id] [job] [grade] - sets a players job</summary>

Sets a player with the given `id` to have the given `job` with the given `grade`

**Permission level:** admin

* **id -** (required) The `id` of the player
* **job** - (required) The job name
* **grade** - (required) The job grade

</details>

<details>

<summary>/gang - display your current gang</summary>

Displays your current gang name and grade

**Permission level:** user

</details>

<details>

<summary>/setgang [id] [gang] [grade] - sets a players gang</summary>

Sets a player with the given `id` to be part of the given `gang` with the given `grade`

**Permission level:** admin

* **id** - (required) The `id` of the player
* **gang** - (required) The gang name
* **grade** (required) The gang grade

</details>

<details>

<summary>/clearinv [opt: id]- clears a players inventory</summary>

Clears the inventory of a player with the given `id` or your own inventory if no `id` is given

**Permission level:** admin

* **id** - (optional) The id of a player

</details>

<details>

<summary>/ooc [message] - ooc chat command</summary>

Sends an out-of-character (ooc) message to the chat.

**Permission level:** user

* **message** - (required) The message to send

</details>

<details>

<summary>/me [message] - shows a message above your head</summary>

Shows a 3d text message above your head. Useful for enhancing roleplay.

**Permission level:** user

* **message** - (required) The message to display

</details>

### Ambulancejob

<details>

<summary>/911e [message] - sends a message to EMS</summary>

Sends a message to EMS players with the job 'ambulance'.

**Permission level:** user

* **message** - (required) The message to send

</details>

<details>

<summary>/status - check the status of the nearest player</summary>

This will find the closest player and check their health status

**Permission level:** user

</details>

<details>

<summary>/heal - heals the nearest player</summary>

This will find the nearest player and heal them

**Permission level:** user

</details>

<details>

<summary>/revivep - revives the nearest player</summary>

This will find the nearest player and revive them

**Permission level:** user

</details>

<details>

<summary>/revive - revive yourself</summary>

Revives yourself to full health

**Permission level:** admin

</details>

<details>

<summary>/setpain [opt: id] - sets the pain level to the player</summary>

Sets the pain level to the player with the given `id` or to yourself if no id is given.

**Permission level:** admin

</details>

<details>

<summary>/kill [opt: id] - kills the player</summary>

Kills the player with the given `id` or kills yourself if no id is given.

**Permission level:** admin

* **id** - (optional) The player id

</details>

<details>

<summary>/aheal [opt: id] - heals a player</summary>

Heals a player with the given `id` or heals yourself if no id is given.

**Permission level:** admin

* **id** - (optional) The player id

</details>

### Police

<details>

<summary>/911p [message] - sends an alert to the police</summary>

This command sends an alert to all players with the job 'police'. The alert will contain the given `message` and a blip is added to the police player's map at your current location.

**Permission level:** user

* **message** - (required) The message to send with the alert

</details>

<details>

<summary>/spikestrip - Place a spike strip</summary>

Places a Spike Strip object on the ground. The player must have the job of 'police' and be on duty to use.

**Permission level:** user

</details>

<details>

<summary>/grantlicense [id] [license] - give a player a license</summary>

Gives a player with the given `id` the license of the given `license` type.

This command can only be used by players with the job of 'police' above the minimum grade as set by `Config.LicenseRank` (Default is grade 2 and above).&#x20;

**Permission level:** user

* **id** - (required) The id of the player
* **license** - (required) The license type (E.g. "weapon" or "driver")

</details>

<details>

<summary>/revokelicense [id] [license] - remove a player's license</summary>

Removes a license of the given `license` type from a player with the given `id`.

This command can only be used by players with the job of 'police' above the minimum grade as set by `Config.LicenseRank` (Default is grade 2 and above).&#x20;

**Permission level:** user

* **id** - (required) The id of the player
* **license** - (required) The license type (E.g. "weapon" or "driver")

</details>

<details>

<summary>/pobject [type] - allows officer to spawn an object</summary>

Allows a player with the job of 'police' to spawn an object

**Permission level:** user

* **type** - (required) The object type. Available types:
  * **cone** - a traffic cone
  * **barrier** - a roadblock barrier
  * **roadsign** - a road sign
  * **tent** - a gazebo for crime scenes
  * **light** - a work light
  * **delete** - delete an object

</details>

<details>

<summary>/cuff - cuff the nearest player</summary>

This command will hard cuff the nearest player (prevents movement) .

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/sc - soft cuff the nearest player</summary>

This command will soft cuff the nearest player (allows movement).

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/escort - escort the nearest player</summary>

This command will escort the nearest player.

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/callsign [name] - allows officer to set a callsign</summary>

Allows a player with the job of 'police' to set their callsign. The callsign is visible as the name of the player's blip on the map.

**Permission level:** user

* **name** - (required) the callsign to be used

</details>

<details>

<summary>/jail - sends nearest player to jail</summary>

This command will send the nearest player to jail. A menu will open allowing the officer to set the jail time.

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/unjail [id] - unjail a player</summary>

Unjail a player with the given `id`

Can only be used by players with the job of 'police'

**Permission level:** user

* **id** - (required) the id of the player

</details>

<details>

<summary>/clearcasings - clears bullet casings in the area</summary>

Clears any bullet casings with 10.0 units of your current location.

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/clearblood - clears blood drops in the area</summary>

Clears any blood drops with 10.0 units of your current location.

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/seizecash - seize cash from the nearest player</summary>

Seize cash from the nearest player.

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/cam [id] - allows officer to see cam footage from selected spots</summary>

Allows a player with the job of 'police' to view security cameras. Security camera locations can be set up in the config file of qb-policejob. See `Config.SecurityCameras`.

**Permission level:** user

* **id** - (required) the id of the camera

</details>

<details>

<summary>/flagplate [plate] [reason] - allows speed cameras to find a plate flagged</summary>

Allows speed cameras that can be set up in the config to find a flagged plate. See `Config.Radars`

**Permission level:** user

* **plate** - (required) the plate to be flagged
* **reason** - (required) the reason for the flag

</details>

<details>

<summary>/unflagplate [plate] - removes the flag from the plate</summary>

Removes the flag on the plate so cameras will no longer pick up the plate.

**Permission level:** user

* **plate** - (required) the plate to be unflagged

</details>

<details>

<summary>/plateinfo [plate] - shows the info of the plate</summary>

Shows whether a plate is flagged and gives the reason if so.

**Permission level:** user

* **plate** - (required) the plate to check

</details>

<details>

<summary>/depot [price] - allows officer to impound vehicle for a price</summary>

Allows a player with the job of 'police' to send a vehicle to the impound for the given `price`

**Permission level:** user

* **price** - (required) the price set for removing vehicle from depot

</details>

<details>

<summary>/impound - impounds a vehicle without a price</summary>

impounds a vehicle without a price

Can only be used by a player with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/paytow [id]  - pays the tow driver $500</summary>

Pays the player with the given `id` $500. The player being paid must have the job of 'tow'.

**Permission level:** user

* **id** - (required) the id of the player being paid

</details>

<details>

<summary>/paylawyer [id] - pays a lawyer $500</summary>

Pays the player with the given `id` $500. The player being paid must have the job of 'lawyer'.

**Permission level:** user

* **id** - (required) the id of the player being paid

</details>

<details>

<summary>/anklet - adds a tracking device to the closest player</summary>

Adds a tracking device to the closest player.&#x20;

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/ankletlocation [cid] - shows the location of the player</summary>

Shows the location of the player with the given `ci`d

Can only be used by players with the job of 'police'

**Permission level:** user

* **cid** - (required) the citizen id of the player being checked

</details>

<details>

<summary>/takedrivinglicense - takes the players drivers license</summary>

Takes the driving license of the closest player

Can only be used by players with the job of 'police'

**Permission level:** user

</details>

<details>

<summary>/takedna [id] - takes the players dna</summary>

Takes the dna of a player with a given `id`. Requires an empty evidence bag.

**Permission level:** user

* **id** - (required) the id of the player

</details>

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
