# Playing Rainbow Six 3: Raven Shield in 2020 and beyond

## Obtaining the Game

Raven Shield, released March 18 2003, is frequently on sale for [under $5 on Steam](https://isthereanydeal.com/game/tomclancysrainbowsixiiigoldedition/history/). This edition contains the Athena Sword expansion but not Iron Wrath, which can be downloaded separately (see [EXPANSIONS.md](EXPANSIONS.md)).

For novelty purposes, there are also [single-player](https://www.moddb.com/games/tom-clancys-rainbow-six-3-raven-shield/downloads/rainbow-six-3-raven-shield-demo) and [multi-player](https://www.moddb.com/games/tom-clancys-rainbow-six-3-raven-shield/downloads/raven-shield-mp-demo-1-1) demos still available for download, also released in 2003.

## Community Resources

* [Discord](https://discord.com/invite/QnXXqcK)

## Playing the Game

### Essential Improvements

1. Borderless Gaming will run the game in a fullscreen window, allowing you to instantly alt-tab. You can [download it from Github for free](https://github.com/Codeusa/Borderless-Gaming/releases/).
   1. Edit `<YourGameDir>\system\RavenShield.ini` and set `StartupFullscreen` to `False`
   1. Launch Borderless Gaming
   1. Launch Raven Shield
   1. Add Raven Shield to "Favorites" in Borderless Gaming by selecting it in the left-side list and clicking the `>` button
   1. Close and relaunch Raven Shield to use it with Borderless Gaming
1. Check the [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Tom_Clancy%27s_Rainbow_Six_3:_Raven_Shield) for any tweaks you might want to perform.
1. Rebind the controls as desired. For example:
   1. Bind `Run` to `Shift`
   1. Bind `Reload` to `R`
   1. Bind `Zoom` to `RMB`
1. If you plan to play online, set your name in the Multiplayer Options.

### Single-Player

You can now play the campaign, a custom mission, or a training scenario. To unlock all maps in custom missions, press `~` at the main menu and enter the command `unlockall`.

### Multi-Player

On September 4 2016, Ubisoft shut down the authentication servers for Raven Shield. We use OpenRVS to point our clients at a new set of servers so we can still play the game together.

1. Download the latest version of OpenRVS from [RVSGaming.org](http://rvsgaming.org/Downloads/). There is [a copy of OpenRVS 1.4 in this repo](OpenRVS1.4.zip).
1. Copy `openrvs.ini`, `OpenRVS.u`, `R6ClassDefines.ini`, and `Servers.list` to `<YourGameDir>\system\`.
1. You will need to update `system/R6GameService.dll` in order to remove another place where the game makes outbound calls to Ubisoft servers. Either run Chriswak's [R6GameService_Patcher](http://rvsgaming.org/Downloads/DllPatcher/R6GameService_Patcher.zip) ([source](https://github.com/eth0up/R6GameServicePatcher)) or use [the prebuilt copy from this repo](R6GameService.dll). If unpatched, the game will hang any time it tries to reach Ubisoft servers during regular gameplay.
1. Launch the game and set your Internet connection speed to `T3` in the settings menu to avoid throttling your connection.
1. Join a server and party like it's 2003!

Note: Since we are using a fixed list of servers, some features will no longer work. The list cannot be filtered (using the bottom menu) or sorted, and latency will always be displayed as `1000`.

Players can edit `Servers.list` to choose which servers are displayed when RVSGaming servers cannot be reached. You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.

## Expansions

See [EXPANSIONS.md](EXPANSIONS.md)

## Mods and Custom Content

See [CUSTOM.md](CUSTOM.md)

## Hosting a Server

See [SERVERS.md](SERVERS.md)
