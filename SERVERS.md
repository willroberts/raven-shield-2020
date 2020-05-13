# Playing Rainbow Six 3: Raven Shield in 2020 and beyond

## Hosting a Server

### Configuration

The two primary files for server configuration are `system\RavenShield.ini` and `system\Server.ini`. Here are some common settings you may want to change:

* In `RavenShield.ini`
  * If necessary, change the values of the server ports.
    * `Port`: Default value is 6777, but set this to the value you are assigned. If connecting to your assigned port takes you to someone else's server, they have used your port. If this happens, add 10000 to every port number and try again.
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
    * `DiffLevel` sets the NPC difficulty. Default is 2
    * `AIBkp` may be set to `False` to disable AI followers in co-op mode   
  * Under `[Engine.R6MapList]`
    * There is room for up to 32 maps in the map list. Each position in the list has an index (0-31) and two values to set:
      * `GameType` should be `R6Game.R6TeamDeathMatchGame` for PVP or `R6Game.R6TerroristHuntCoopGame` for PVE. See game documentation for more mode names.
      * `Maps` should be set to the name of the map you want in the rotation. Each `Maps[]` entry must have a corresponding `GameType[]` entry.

### Method 1 (easy): VPS

This section will cover hosting a Raven Shield server with [MarkMods.com](https://www.markmods.com). MarkMods is one of the few vendors to still offer Raven Shield gameservers.

1. From the [Raven Shield page](https://www.markmods.com/gameserverhosting/Rainbow%20Six%203:Raven%20Shield/), choose a number of player slots, a server location, and a billing frequency. Smaller servers will cost around $1/slot, while larger servers can be more efficient (around $0.50/slot).
1. Finish the signup process.
1. Open your server in the control panel.
  1. Under Control Panel, Stop the server.
  1. Under Configuration, make sure `Use FTP config` is enabled. Save at the bottom.
  1. Under File Manager, click `Open In Fullscreen` to start a minimal FTP client connected to your server. This will be the primary way you interact with the server's content and configuration. To open a file, click it in the UI. Save it to disk if you plan to make changes. To update a file, click `Upload Files` in the bottom left and choose the file to upload. It will replace the server's copy.
  1. Install OpenRVS by uploading its files according to the instructions.
  1. Replace `system\R6GameService.dll` with [the prebuilt copy from this repo](R6GameService.dll). This will eliminate another outbound call to Ubisoft's servers.
  1. Replace `Mods\RavenShield.mod` with [the copy from this repo](RavenShield.mod). This will enable the OpenRVS server code and beacon code.
  1. Start the server again when finished. It should now be using the config files from the file manager.

When you finish, test your server and take note of your IP address and port number, and skip ahead to [Publishing Your Server](https://github.com/ijemafe/raven-shield-2020/blob/master/SERVERS.md#publishing-your-server).

### Method 2 (hard): Linux

This section will cover hosting a Raven Shield server with [DigitalOcean Droplets](https://www.digitalocean.com/products/droplets/). You can also use these steps with your own Linux hardware for self-hosted servers.

A Raven Shield dedicated server running the base game content will use 1 CPU, 128MB of memory, and 1GB of disk space. In order to avoid running at capacity, look for VMs with 256MB of memory and 2GB of disk space.

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
   1. Place your game files on the server, e.g. `/opt/rs`
   1. Install OpenRVS by uploading its files according to the instructions.
   1. Replace `system\R6GameService.dll` with [the prebuilt copy from this repo](R6GameService.dll). This will eliminate another outbound call to Ubisoft's servers.
   1. Replace `Mods\RavenShield.mod` with [the copy from this repo](RavenShield.mod). This will enable the OpenRVS server code and beacon code.
   1. Enter the game's system directory with `cd /opt/rs/system`
   1. Start the game with `wine UCC.exe server -ini=RavenShield.init -serverconf=Server.ini`

This will start the server attached to your current terminal window. In order to reliably keep the process running and restart it when it crashes, create a `systemd` unit file, based on the docs [here](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files), which runs the wine command above.

When you finish, test your server and take note of your IP address and port number.

### Publishing Your Server

Once the server is ready to go, you will need to visit the [SMClan forums](http://smclan.org/forum/42) and make a post requesting that Tony add your server (and port) to the OpenRVS server list. Share the IP address and port number, as well as the name of the server and a bit of information about it.

Once the server is added to the list, it will automatically appear when searching for games in multiplayer. Until then, you can use your server by joining its IP.
