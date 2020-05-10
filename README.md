# Instructions for playing Rainbow Six 3: Raven Shield in 2020 and beyond.

## Obtaining the Game

The game is frequently on sale for [under $5 on Steam](https://isthereanydeal.com/game/tomclancysrainbowsixiiigoldedition/history/). This edition contains the Athena Sword expansion but not Iron Wrath. Iron Wrath is out of scope for this guide, but it adds 8 maps, 5 game modes, and 6 firearms.

## Community Resources

* [Discord](https://discord.com/invite/QnXXqcK)

## Playing the Game

### Essential Improvements

1. Borderless Gaming will run the game in a fullscreen window, allowing you to instantly alt-tab. You can [download it from Github for free](https://github.com/Codeusa/Borderless-Gaming/releases/).
1. Check the [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Tom_Clancy%27s_Rainbow_Six_3:_Raven_Shield) for any tweaks you might want to perform.

### Single-Player

You can now play the campaign, a custom mission, or a training scenario. To unlock all maps in custom missions, press `~` at the main menu and enter the command `unlockall`.

### Multi-Player

On September 4 2016, Ubisoft shut down the authentication servers for Raven Shield. We use OpenRVS to point our clients at a new set of authentication servers so we can still play the game together.

1. Download the latest version of OpenRVS from [RVSGaming.org](http://rvsgaming.org/Downloads/).
1. Open `readme.html` to read the documentation.
1. Copy `openrvs.ini`, `OpenRVS.u`, `R6ClassDefines.ini`, and `Servers.list` to `<YourGameDir>\system\`.
1. (Optional) Edit `Servers.list` to choose which servers are displayed when RVSGaming servers cannot be reached. The names in this file are for reference; the in-game server name will be retrieved from the server. You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.

## Hosting a Server

### VPS

This section will cover hosting a Raven Shield server with [MarkMods.com](https://www.markmods.com). MarkMods is one of the few vendors to still offer Raven Shield gameservers.

From the [Raven Shield page](https://www.markmods.com/gameserverhosting/Rainbow%20Six%203:Raven%20Shield/), choose a number of player slots, a server location, and a billing frequency. Smaller servers will cost around $1/slot, while larger servers can be more efficient (around $0.50/slot). Finish the signup process.

**Basic Setup**

1. Open your server in the control panel.
  1. Under Control Panel, Stop the server.
  1. Under Configuration, make sure `Use FTP config` is enabled. Save at the bottom.
  1. Under File Manager, click `Open In Fullscreen` to start a minimal FTP client connected to your server. This will be the primary way you interact with the server's content and configuration.
    1. To open a file, click it in the UI. Save it to disk if you plan to make changes.
    1. To update a file, click `Upload Files` in the bottom left and choose the file to upload. It will replace the server's copy.
  1. Install OpenRVS
  1. Replace R6GameService.dll with a copy from Discord
  1. Replace RavenShield.mod with a copy from Discord
  1. Start the server again when finished. It should now be using the config files from the file manager.

**Adjusting Configs**

The two primary files for server configuration are `system\RavenShield.ini` and `system\Server.ini`. Here are some common settings you may want to change:

* In `RavenShield.ini`
  * 
* In `Server.ini`
  * 

**Publishing Your Server**

Once the server is ready to go, you will need to visit the [SMClan forums](http://smclan.org/forum/42) and make a post requesting that Tony add your server (and port) to the OpenRVS server list.

### Linux

This section will cover hosting a Raven Shield server with [DigitalOcean Droplets](https://www.digitalocean.com/products/droplets/). You can also use these steps with your own Linux hardware for self-hosted servers.

### Windows

This section will cover hosting a Raven Shield server with [Microsoft Azure](https://azure.microsoft.com/en-us/services/virtual-machines/). You can also use these steps with your own Windows hardware for self-hosted servers.
