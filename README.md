# Playing Rainbow Six 3: Raven Shield in 2020 and Beyond

## Obtaining the Game

Raven Shield (released 2003) is typically [$3-10 on Steam](https://isthereanydeal.com/game/tomclancysrainbowsixiiigoldedition/history/). You can also get it on [UPlay](https://store.ubi.com/upc/us/tom-clancy-s-rainbow-six--3-gold/58aeb87e29e1236d368b4567.html). These contain the Athena Sword expansion but not Iron Wrath (see [EXPANSIONS.md](EXPANSIONS.md)).

Alternatively, you can use your original CDs if you also patch to version 1.60.

## Community Resources

* [Discord](https://discord.com/invite/QnXXqcK)

## Playing the Game

Note: This doc uses `<YourGameDir>` to refer to the place you have Raven Shield installed. For most users, this will be `C:\Program Files (x86)\Steam\steamapps\common\Rainbow Six 3 Gold`.

### Essential Improvements

1. Check the [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Tom_Clancy%27s_Rainbow_Six_3:_Raven_Shield) for any tweaks you might want to perform.
1. Borderless Gaming will run the game in a fullscreen window, allowing you to instantly alt-tab. You can [download it from Github for free](https://github.com/Codeusa/Borderless-Gaming/releases/).
   1. Edit `<YourGameDir>\system\RavenShield.ini` and set `StartupFullscreen` to `False`
   1. Launch Borderless Gaming
   1. Launch Raven Shield
   1. Add Raven Shield to "Favorites" in Borderless Gaming by selecting it in the left-side list and clicking the `>` button
   1. Close and relaunch Raven Shield to use it with Borderless Gaming
   1. If you have issues getting the game to run in a borderless window, try the `Delay Borderless Window` option by right-clicking Raven Shield in Borderless Gaming
1. Rebind the controls as desired. For example:
   1. Bind `Run` to `Shift`
   1. Bind `Reload` to `R`
   1. Bind `Zoom` to `RMB`
1. If you'd like to play online, set your name in the Multiplayer Options.

### Single-Player

You can now play the campaign, a custom mission, or a training scenario. To unlock all maps in custom missions, press `~` at the main menu and enter the command `unlockall`.

### Multi-Player

Ubisoft shut down the authentication servers for Raven Shield in 2016, so we use OpenRVS to point our clients at a new set of servers.

1. Download the latest version of OpenRVS from [RVSGaming.org](http://rvsgaming.org/Downloads/). There is [a copy of OpenRVS 1.4 in this repo](OpenRVS1.4.zip).
1. Copy `openrvs.ini`, `OpenRVS.u`, `R6ClassDefines.ini`, and `Servers.list` to `<YourGameDir>\system\`.
1. You will need to update `system\R6GameService.dll` in order to remove another place where the game makes outbound calls to Ubisoft servers. Either run Chriswak's [R6GameService_Patcher](http://rvsgaming.org/Downloads/DllPatcher/R6GameService_Patcher.zip) ([source](https://github.com/eth0up/R6GameServicePatcher)) or use [the prebuilt copy from this repo](R6GameService.dll). If unpatched, the game will hang any time it tries to reach Ubisoft servers during regular gameplay.
1. Launch the game and set your Internet connection speed to either `T1` or `T3` in the settings menu to raise Unreal Engine's `netspeed` to 20KB/s.
1. Join a server and party like it's 2003!

Note: Since we are using a fixed list of servers, some features will no longer work. The list cannot be filtered (using the bottom menu) or sorted, and latency will always be displayed as `1000`.

Players can edit `Servers.list` to choose which servers are displayed when RVSGaming servers cannot be reached. You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.

### Servers

Here is a snapshot of known servers as of May 2020. See [RVSGaming.org](http://rvsgaming.org) for the latest list.

Server Name | Address
--- | ---
24/7 Deathmatch | 107.172.191.114:7777
ALLR6.com Missions | 64.187.238.46:11777
ALLR6 Tango Hunt | 64.187.238.45:7779
ALLR6 Tango Hunt 2 | 64.187.238.44:12777
ALLR6 Europe TH | 5.9.50.39:8777
ALLR6 Original Maps Only | 104.243.46.138:9777
ALLR6 TDM Original Maps | 104.243.46.138:14777
ALLR6 AthenaSword+IronWrath | 104.243.46.138:7779
FFS-ATS-FUN-SFPD serveur | 89.46.223.5:7777
IEF Everything Server | 66.151.255.13:7877
OBSOLETESUPERSTARS.COM | 72.251.228.169:7777
SMC Suppressed Stealth | 185.24.221.23:7777
SMC Suppressed Action | 185.24.221.23:7778
SSHQ COOP Server | 66.151.255.14:8777
(Srgt)Server | 24.201.194.168:7777
The Freedom Server | 108.178.44.218:7877
Classic Maps 3v3 | 64.187.238.45:6777
Classic Maps T-Hunt | 64.187.238.46:21777

## Expansions

See [EXPANSIONS.md](EXPANSIONS.md)

## Mods and Custom Content

See [CUSTOM.md](CUSTOM.md)

## Hosting a Server

See [SERVERS.md](SERVERS.md)
