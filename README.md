# Instructions for playing Rainbow Six 3: Raven Shield in 2020 and beyond.

## Obtaining the Game

The game is frequently on sale for [under $5 on Steam](https://isthereanydeal.com/game/tomclancysrainbowsixiiigoldedition/history/). This edition contains the Athena Sword expansion but not Iron Wrath, which can be downloaded separately (see below).

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
1. Replace `system\R6GameService.dll` with [the copy from this repo](R6GameService.dll) for OpenRVS.
1. (Optional) Edit `Servers.list` to choose which servers are displayed when RVSGaming servers cannot be reached. The names in this file are for reference; the in-game server name will be retrieved from the server. You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.
1. Launch the game and set your Internet connection speed to `T3` in-game.
1. Join a server and party like it's 2003!

## Athena Sword

Athena Sword is an expansion which adds 19 maps (including 8 designed for multiplayer), 4 game modes, and 7 weapons. In the Steam version of Raven Shield, Athena Sword is installed separately in your Steam Library.

Note: Installing Athena Sword in Steam may overwrite the `<YourGameDir>\system\R6ClassDefines.ini` file. Be sure to install OpenRVS after installing Athena Sword.

To play offline:
1. Launch Athena Sword from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Athena Sword' -> 'Activate'

To play online:
1. Launch Raven Shield from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Raven Shield' -> 'Activate'
1. Join an OpenRVS server hosting Athena Sword content

## Iron Wrath

Iron Wrath is a free expansion which adds 18 maps (including 8 designed for multiplayer), 5 game modes, and 6 weapons. In order to add Iron Wrath to a Steam installation, follow these steps:

1. Download Iron Wrath's unpacked files [here](https://www.moddb.com/games/tom-clancys-rainbow-six-3-raven-shield/downloads/rainbow-six-3-iron-wrath-manual-installation).
1. Copy `IronWrath` and `IronWrath.mod` to `<YourGameDir>\Mods`.

To play offline:
1. Launch Raven Shield from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Iron Wrath' -> 'Activate'

To play online:
1. Launch Raven Shield from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Raven Shield' -> 'Activate'
1. Join an OpenRVS server hosting Iron Wrath content

Hosting Iron Wrath content on servers requires using `UnrealEd` to modify the maps for compatibility with the patched client. Process is not yet documented.

## Custom Content

See [CUSTOM.md](CUSTOM.md)

## Hosting a Server

See [SERVERS.md](SERVERS.md)
