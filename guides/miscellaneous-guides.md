---
description: Extra guides and tools are listed here
---

# 📑 Miscellaneous Guides

## Keymapping

<details>

<summary>What is Keymapping?</summary>

Allows you to take a **REGISTERED** command, using the [RegisterCommand](https://docs.fivem.net/natives/?\_0x5FA79B0F) native, and apply a key binding to it. So instead of having to type in the slash command in the chat, you can just press a single key and execute it. This does NOT work with `QBCore.Commands.Add`.

</details>

#### example

`RegisterKeyMapping('togglelocks', 'Toggle Vehicle Locks', 'keyboard', 'L')`

The purpose of this system is so that players can completely customize their experience on the server and not be subjected to hard-coded key binds.

<details>

<summary><em>How to change a bind</em></summary>

* Open your pause menu in game&#x20;
* Navigate to settings
* Select settings —> keybinds
* Select FiveM
* Find the command you want to change the key for and select it.
* Press the desired key you’d like and that’s it

</details>

## Weapon License

By default only a citizen ID and drivers license is redeemable from City Hall. For a player to get a weapons license he needs to see a police officer who will do `/grantlicense [id] weapon` for that player to be "granted" access in City Hall.

Police can also do `/revoke [id] [licenseType]` to revoke a players ability to purchase a **hard copy** of the specified license. Revoking the license will **not** remove the hard copy from the players' inventory if they have one, it will simply remove the ability for them to purchase a new one.

If you would like the players to be granted by default look for this set of code in `qb-core/server/player.lua`

```etlua
PlayerData.metadata["licences"] = PlayerData.metadata["licences"] ~= nil and PlayerData.metadata["licences"] or {
    ["driver"] = true,
    ["business"] = false,
    ["weapon"] = false
}    
```

and change `["weapon"] = false` to `["weapon"] = true`

Once a player has been granted a weapons license they will be able to purchase weapons from gun stores that have the `requiresLicense` variable set to `true`. To restrict weapon sales to individuals with a weapons license see the example config below from `qb-shops/config.lua`

```etlua
[4] = {
    name = "weapon_pistol",
    price = 2500,
    amount = 5,
    info = {},
    type = "item",
    slot = 4,
    requiresLicense = true
},
```

## Onesync-infinity&#x20;

Onesync-infinity should be enabled by default but if you ever need to enable it you would just put `set onesync on` in your server.cfg

<details>

<summary><strong>Adapting Your Scripts</strong></summary>

This is not an easy thing to describe because the code varies so you have to use your own judgement sometimes. With infinity enabled, there is what is called a "scope" and the client (player/you) has a "scope range". Now everything INSIDE this range the client will load via their machine but if something is OUTSIDE the scope then the client is not aware of it. Easiest example being if i am standing in the city and another player is standing in paleto, my machine has no idea that player is there at all. So if i had a teleport to player that was not setup for this then when i tried to go to them i would go to myself because i can not get the other players coords. Now the server DOES know that players coords so what we have to do as developers is gather that information from the server and send it to the client side. Also another big deal is obviously since we do not know about players outside of our scope, if we need a full list of players in the server then we need to get that info from the server as well.

</details>

<details>

<summary><strong>Getting The Coords</strong></summary>

This one is relatively simple, you can use the native GetEntityCoords on the server side and then pass that through an event or a callback. If you want more info on how to use this native then you can view that [here](https://docs.fivem.net/natives/?\_0x3FEF770D40960D5A)

</details>

#### Getting the Players

To get a list of players on the server we must use either a native that is like this

```etlua
for _, player in ipairs(GetActivePlayers()) do
local ped = GetPlayerPed(player)
-- do stuff
end
```

Using the QB function you can do it like this

```etlua
for _, player in pairs(QBCore.Functions.GetPlayers()) do
local ped = GetPlayerPed(player)
-- do stuff
end
```

**Spawning A Vehicle At A Distance**

{% hint style="info" %}
If you have a script that requires you to create a vehicle at a distance that is outside the infinity scope, you must use the code like below on the SERVER side
{% endhint %}

```etlua
local SpawnPoints = {
vector4(-1327.479736328, -86.045326232910, 49.31, 52),
vector4(-2075.888183593, -233.73908996580, 21.10, 52),
vector4(-972.1781616210, -1530.9045410150, 4.890, 52),
vector4(798.18426513672, -1799.8173828125, 29.33, 52),
vector4(1247.0718994141, -344.65634155273, 69.08, 52),
}
QBCore.Functions.CreateCallback('qb-truckrobbery:server:spawntruck', function(source, cb)
local coords = SpawnPoints[math.random(#SpawnPoints)]
local CreateAutomobile = GetHashKey("CREATE_AUTOMOBILE")
local truck = Citizen.InvokeNative(CreateAutomobile, GetHashKey('stockade'), coords, coords.w, true, false)
while not DoesEntityExist(truck) do
    Wait(25)
end
if DoesEntityExist(truck) then
    local netId = NetworkGetNetworkIdFromEntity(truck)
    cb(netId)
else
    cb(0)
end
end)
```

{% hint style="warning" %}
This will spawn the entity and callback the entity id which you can then use on the client side to check if the entity exists. It will NOT exist until a client(player) gets within range of it! While a client is NOT in range, the server “owns” the entity. So whenever a client gets into infinity range it then takes ownership of that entity and can be used by them. I know this one is a bit confusing but there’s no good way to explain it.
{% endhint %}

## Database Connection

{% hint style="info" %}
txAdmin does this automatically already but if needed then in your server.cfg put this and fill it in with the correct information. For the database wrapper [oxmysql](https://github.com/overextended/oxmysql)&#x20;
{% endhint %}

### Installation[​](https://overextended.github.io/docs/oxmysql/#installation) <a href="#installation" id="installation"></a>

* Download the [latest build](https://github.com/overextended/oxmysql/releases/latest) of oxmysql (not the source code).
* Extract the contents of the archive to your resources folder.
* Start the resource near the top of your resources in your `server.cfg`.
* If you have a lot of streamed assets, load them first to prevent timing out the connection.

### Configuration[​](https://overextended.github.io/docs/oxmysql/#configuration) <a href="#configuration" id="configuration"></a>

You can change the configuration settings by using convars inside your `server.cfg`. Reference the following for an idea of how to set your connection options. You must include one of the following lines, adjusted for your connection and database settings.

```
set mysql_connection_string "mysql://root:12345@localhost/qbcore?charset=utf8mb4"
```

Certain special characters are reserved or blocked and may cause issues when used in your password.\
For more optional settings (such as multiple statements) you can reference [pool.d.ts](https://github.com/sidorares/node-mysql2/blob/master/typings/mysql/lib/Pool.d.ts#L10) and [connection.d.ts](https://github.com/sidorares/node-mysql2/blob/master/typings/mysql/lib/Connection.d.ts#L8).

You can also add the following convars if you require extra information when testing queries.

```
set mysql_slow_query_warning 150set mysql_debug true
```

#### Using the UI[​](https://overextended.github.io/docs/oxmysql/#using-the-ui) <a href="#using-the-ui" id="using-the-ui"></a>

Before using the UI first you have to make sure you have the `mysql_ui` convar set to true:

```
set mysql_ui true
```

Also make sure that you have `command` ace permission access, then you should be able to use the `mysql` command in game to open up the UI and see your query data.

## Server.cfg

Setting up your server.cfg is really simple and is already completed upon a successful txAdmin recipe install! You can also find additional information on server configuration files [**here**](https://docs.fivem.net/docs/server-manual/setting-up-a-server/)**.** In case of a manual install then here's a template to use

```systemd
#   ____  ____   _____               
#  / __ \|  _ \ / ____|              
# | |  | | |_) | |     ___  _ __ ___ 
# | |  | |  _ <| |    / _ \| '__/ _ \
# | |__| | |_) | |___| (_) | | |  __/
#  \___\_\____/ \_____\___/|_|  \___|

## You CAN edit the following:
{{serverEndpoints}}
sv_maxclients {{maxClients}}
set steam_webApiKey "none"
sets tags "default, deployer, qbcore, qb-core"

## You MAY edit the following:
sv_licenseKey "{{svLicense}}"
sv_hostname "{{serverName}} built with {{recipeName}} by {{recipeAuthor}}!"
sets sv_projectName "[{{recipeName}}] {{serverName}}"
sets sv_projectDesc "{{recipeDescription}}"
sets locale "en-US" 
load_server_icon myLogo.png
set sv_enforceGameBuild 2372
set mysql_connection_string "{{dbConnectionString}}"

# Voice config
setr voice_useNativeAudio true
setr voice_useSendingRangeOnly true
setr voice_defaultCycle "GRAVE"
setr voice_defaultVolume 0.3
setr voice_enableRadioAnim 1
setr voice_syncData 1

# QBCore locale config
setr qb_locale "en"

# QBCore UseTarget
setr UseTarget false

# These resources will start by default.
ensure mapmanager
ensure chat
ensure spawnmanager
ensure sessionmanager
ensure basic-gamemode
ensure hardcap
ensure baseevents

# QBCore & Extra stuff
ensure qb-core
ensure [qb]
ensure [standalone]
ensure [voice]
ensure [defaultmaps]

## Permissions ##
add_ace group.admin command allow # allow all commands
#add_principal identifier.{{principalMasterIdentifier}} qbcore.god <- doesn't exist yet, change the generated one below to qbcore.god
{{addPrincipalsMaster}}

# Resources
add_ace resource.qb-core command allow # Allow qb-core to execute commands

# Gods
add_ace qbcore.god command allow # Allow all commands

# Inheritance
add_principal qbcore.god group.admin # Allow gods access to the main admin group used to get all default permissions
add_principal qbcore.god qbcore.admin # Allow gods access to admin commands
add_principal qbcore.admin qbcore.mod # Allow admins access to mod commands
```



## GitHub Pull Request

* Visit the resource you would like to propose changes on
* Navigate to the exact file within that resource
* Click on the pencil icon and you will be able to make edits to the code
* Once you are satisfied with your edits, scroll down to the box labeled "Propose Changes"
* Write a title and short description of what the changes are
* Once that's filled out, press the green "Propose Changes" button
* You will see a screen showing your edits compared to the existing code
* If you are satisfied with the edits shown, press the green "Create Pull Request" button
* Fill in the title and description if necessary
* Click on the green "Create Pull Request" button and it's finished!

{% hint style="success" %}
If you have email notifications enabled, you will get any updates on the pull request by email
{% endhint %}
