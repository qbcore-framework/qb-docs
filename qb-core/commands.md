---
description: A list of all the commands and their respective resource
---

# ❗ Commands

### AdminMenu

`/admin` : (admin) opens the admin menu  
`/blips` : (admin) toggles player blips  
`/names` : (admin) toggles player names  
`/coords` : (admin) toggles display of your current coords  
`/maxmods` : (admin) sets vehicle to have maximum performance modifications
`/noclip` : (admin) toggles noclip  
`/admincar` : (admin) saves current vehicle to garage  
`/announce [message]` : (admin) creates an announcement with the given argument `message`  
`/report [message]` : (user) create a report to staff with the given `message`  
`/staffchat [message]` : (admin) sends a staff only message  
`/givenuifocus [id] [hasFocus] [hasCursor]` : (admin) Sets `nuifocus` state for the player with the given `id`  
`/warn [id] [reason]` : (admin) warns a player  
`/checkwarns [id] [warningNum]` : (admin) view a warning (number) that was given a player  
`/delwarn [id] [warningNum]` : (admin) deletes a warning from a player  
`/reportr [message]` : (admin) replies to a report with the given `message`  
`/setmodel [model] [id]` : (admin) changes the players ped model  
`/setspeed [speed]` : (admin) set players foot speed  
`/reporttoggle` : (admin) opt in to receiving player reports  
`/kickall` : (god) kicks all players from server  
`/setammo [amount] [opt: weapon]` : (admin) sets ammo to current gun in hand, or `weapon` if given  
`/vector2` : (admin) Copies `vector2(x, y)` to clipboard of your current coords  
`/vector3` : (admin) Copies `vector3(x, y, z)` to clipboard of your current coords  
`/vector4` : (admin) Copies `vector4(x, y, z, w)` to clipboard of your current coords  
`/heading` : (admin) Copies your heading to clipboard  

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
