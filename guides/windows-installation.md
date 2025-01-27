---
description: Installing a QBCore server step by step.
---

# 🪟 Windows Installation

## Database Configuration

Install [MariaDB](https://mariadb.org/download)and [HeidiSQL](https://www.heidisql.com/download.php)

## MariaDB

## HeidiSQL

* Open HeidiSQL, click the green circle with the plus sign and name it something

{% hint style="success" %}
The names don't matter, you can name them whatever you want!
{% endhint %}

![Press new to create a session](https://i.imgur.com/gMahSUE.png)

![Rename this to whatever you'd like and press open](https://i.imgur.com/IOmBame.png)

## Artifact and txAdmin

Make a new folder on your desktop and name it whatever you want, download the **latest recommended** FiveM [artifacts](https://runtime.fivem.net/artifacts/fivem/build\_server\_windows/master/), then extract them to the folder you made

![The webpage for downloading an artifact version](https://i.imgur.com/XxSPtRk.png)

Double click on FXServer.exe to run it. Once loaded, it should open a web browser page

![txAdmin is already bundled in with the FiveM artifacts so running the server starter will launch it](https://i.imgur.com/ZVOCx11.png)

After you link your FiveM account, which it should do automatically, make a password. Then you will be greeted with steps

![txAdmin starting page after logging in](https://i.imgur.com/TdgvshI.png)

When you get to step number 3, click "Popular Template" then "QBCore Framework"

![Choosing a deployment type](https://i.imgur.com/pexfo3C.png)

![Selecting QBCore from the templates](https://i.imgur.com/VN1xRo8.png)

Select a folder you would like to store your server data in.

![It is suggested to use the path txAdmin suggests](https://i.imgur.com/tyRX3I3.png)

Scroll to the bottom and run the recipe deployer

![Click on next](https://i.imgur.com/n2QKiOS.png)

Go to [keymaster](https://keymaster.fivem.net/) and generate a key. Fill out that information correctly.

{% hint style="info" %}
Keymaster keys only require the IP address the first time it launches after that the generated key can be used on any IP.
{% endhint %}

Paste your Keymaster key where prompted.

![Entering your CFX key](https://i.imgur.com/uNgCHnv.png)

Then click "Run Recipe"

![After you let the recipe install you will be greeted with a screen like this.](https://i.imgur.com/MZyiPmg.png)

{% hint style="danger" %}
If you did not get the above message and got an error message, please use the official [QBCore Discord](https://discord.gg/qbcore) and post in [fivem-support](https://discord.com/channels/831626422232678481/1006299568314527895)
{% endhint %}

{% hint style="warning" %}
Let yarn install all the way through on the initial startup.
{% endhint %}

Once this is complete, we recommend visiting [setting-permissions.md](setting-permissions.md "mention") to configure your server.cfg with any players you'd like to give elevated permissions!
