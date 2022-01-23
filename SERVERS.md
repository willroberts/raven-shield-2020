# Hosting Servers

## Configuration Files

The two primary files for server configuration are `system\RavenShield.ini` and `system\Server.ini`. Here are some common settings you may want to change:

* In `RavenShield.ini`
  * If necessary, change the values of the server ports.
    * `Port`: Default value is 6777
    * `ServerBeaconPort`: Set to `Port` plus 1000 
    * `BeaconPort`: Set to `Port` plus 2000
    * `m_iRegSvrPort`: Set to `Port` minus 1000
    * `m_iRSCDKeyPort`: Set to `Port` minus 2000
    * `m_iModCDKeyPort`: Set to `Port` plus 3000
  * If hosting custom content, you will need to also purchase web hosting in order to avoid slow download speeds for players. Configure a file server with the content your players will need to download, and set `RedirectToURL` to its URL. See [CUSTOM.md](CUSTOM.md) for more info
* In `Server.ini`
  * Under `[Engine.R6ServerInfo]`
    * `ServerName` should contain the name of your server
    * `MOTD` will be shown to players when they connect
    * `DedicatedServer` and `Internet Server` should be set to `True`
    * `MaxPlayers` should be set to the number of player slots
    * `RoundTime` is the length of each round in seconds
    * `BetweenRoundTime` is how long players have to select their gear
    * `RoundsPerMatch` sets the number of rounds before the map rotates
    * `RotateMap`, aka "rotate map on success", will prevent map rotation until a successful round in co-op when set to `True`
    * `UsePassword` should be set to `False` for public servers
    * `AdminPassword` should be set and `UseAdminPassword` should be set to `True`   
    * `FriendlyFire` may be set to `False` if desired
    * `ForceFPersonWeapon` should be set to `True`
    * `CamThirdPerson`, `CamFreeThirdPerson`, and `CamGhost` can be disabled for adversarial mode
    * `CamTeamOnly` should be set to `False` in co-op mode
    * `NbTerro` is the number of opponents in co-op mode
    * `DiffLevel` sets the NPC difficulty. 1 is Rookie, 2 is Veteran, and 3 is Elite. The default is 2
    * `AIBkp` may be set to `False` to disable AI followers in co-op mode   
  * Under `[Engine.R6MapList]`
    * There is room for up to 32 maps in the map list. Each position in the list has an index (0-31) and two values to set:
      * `GameType` should be `R6Game.R6TeamDeathMatchGame` for PVP or `R6Game.R6TerroristHuntCoopGame` for PVE. See game documentation for more mode names.
      * `Maps` should be set to the name of the map you want in the rotation. Each `Maps[]` entry must have a corresponding `GameType[]` entry.

## Method 1: Renting a VPS

This section will cover hosting a Raven Shield server with [MarkMods.com](https://www.markmods.com). MarkMods is one of the few vendors to still offer Raven Shield gameservers.

1. From the [Raven Shield page](https://www.markmods.com/gameserverhosting/Rainbow%20Six%203:Raven%20Shield/), choose a number of player slots, a server location, and a billing frequency. Smaller servers will cost around $1/slot, while larger servers can be more efficient (around $0.50/slot).
1. Finish the signup process.
1. Open your server in the control panel.
   1. Under Control Panel, Stop the server.
   1. Under Configuration, make sure `Use FTP config` is enabled. Save at the bottom.
   1. Under File Manager, click `Open In Fullscreen` to start a minimal FTP client connected to your server. To open a file, click it in the UI. Save it to disk if you plan to make changes. To update a file, click `Upload Files` in the bottom left and choose the file to upload.
      1. Install OpenRVS by uploading its files according to the instructions.
      1. Replace `system\R6GameService.dll` with [the prebuilt copy from this repo](R6GameService.dll). This will eliminate another outbound call to Ubisoft's servers.
      1. Replace `Mods\RavenShield.mod` with [the copy from this repo](RavenShield.mod). This will enable the OpenRVS server code and beacon code.
      1. Edit `RavenShield.ini` and `Server.ini` as desired
         1. In `RavenShield.ini`, set the `Port` value to your assigned port from MarkMods. If connecting to your assigned port takes you to someone else's server, someone may have used your port. If this happens, add 10 to every port number and try again.
  1. Start the server again when finished. It should now be using the config files from the file manager.

When you finish, test your server and take note of your IP address and port number, and skip ahead to [Publishing Your Server](https://github.com/ijemafe/raven-shield-2020/blob/master/SERVERS.md#publishing-your-server).

## Method 2: Hosting on Linux

This section will cover hosting a Raven Shield server with [DigitalOcean Droplets](https://www.digitalocean.com/products/droplets/). You can also use these steps with your own Linux hardware for self-hosted servers.

Note: This section assumes you have [a copy of Rainbow Six 3: Gold](https://github.com/ijemafe/raven-shield-2020/blob/master/README.md#obtaining-the-game).

A Raven Shield dedicated server running the base game content will use around 1 CPU, 128MB of memory, and 1GB of disk space. In order to avoid running at capacity, look for VMs with 256MB of memory and 2GB of disk space. To mitigate unbounded memory growth or leaks, you may want to automatically restart game servers once a day.

If you want to run multiple servers, you may do so on a single Linux VM. Simply add 1 CPU, 256MB of memory, and 2GB of disk space for each additional server you want to run on the same instance.

1. Create an account on DigitalOcean
1. Start a Droplet running the latest Ubuntu Server LTS in your preferred region
1. Log into your Droplet as root and run the following one-time setup commands:
   1. `dpkg --add-architecture i386` (for 32-bit support)
   1. `apt update && apt install wine wine32` (install 32-bit Wine to run Raven Shield)
1. Still as root, create a non-root user which will run the server. Then run these commands:
   1. `mkdir /opt/rs` (create a place to store the game files)
   1. `chown <YourUser> /opt/rs` (give your user ownership of the game directory)
1. Log into the Droplet as your non-root user
   1. Copy the game files to `/opt/rs` on the server
   1. Install OpenRVS by uploading its files according to the instructions.
   1. Replace `system\R6GameService.dll` with [the prebuilt copy from this repo](R6GameService.dll). This will eliminate another outbound call to Ubisoft's servers.
   1. Replace `Mods\RavenShield.mod` with [the copy from this repo](RavenShield.mod). This will enable the OpenRVS server code and beacon code.
   1. Enter the game's system directory with `cd /opt/rs/system`
   1. Start the game with `wine UCC.exe server -ini=RavenShield.init -serverconf=Server.ini`

This will start the server attached to your current terminal window. In order to reliably keep the process running and restart it when it crashes, create a `systemd` unit file, based on the docs [here](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files), which runs the wine command above.

Here is an example `systemd` unit file which might live in `/etc/systemd/system/ravenshield.service`:

```
[Unit]
Description=ravenshield

[Service]
ExecStart=/usr/bin/wine /opt/rs/system/UCC.exe server -ini=/opt/rs/system/RavenShield.ini -servercfg=/opt/rs/system/Server.ini
Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target
```

After changing `systemd` unit files, run `systemctl daemon-reload` to read them. This will let you run `systemctl start ravenshield` to start your server, and `systemctl enable ravenshield` to start it automatically. When the process crashes, it will automatically restart it (no more than one attempt every 10 seconds).

When you finish, test your server and take note of your IP address and port number.

## Publishing Your Server

**UPDATE:** Since OpenRVS 1.5, it is no longer necessary to manually get your server added. When servers come online, they self-register with the server list at http://openrvs.org/servers. If your server does not appear, it may be marked as unhealthy. Be sure the game port is accessible from the public Internet.

Once the server is ready to go, join the [Discord](https://discord.com/invite/QnXXqcK) and enter the `#general-gaming` channel. Ask for Tony's contact info to get the new server added. Send the server name, IP address, port number, and game mode (adversarial or cooperative).

Once the server is added to the list, it will automatically appear when searching for games in multiplayer. Until then, you can use your server by joining its IP.
