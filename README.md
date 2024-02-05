# Playing Rainbow Six 3: Raven Shield in 2020 and Beyond

## Obtaining the Game

Raven Shield (released 2003) is typically [$9.99 on Steam](https://store.steampowered.com/app/19830/Tom_Clancys_Rainbow_Six_3_Gold/).
This version contains the Athena Sword expansion, but not the Iron Wrath expansion (see [EXPANSIONS.md](EXPANSIONS.md)).

Alternatively, you can use your original CDs if you also patch to version 1.60.

## Essential Improvements

1. Check the [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Tom_Clancy%27s_Rainbow_Six_3:_Raven_Shield) for any tweaks you might want to perform.
2. In the game options, rebind the controls as desired. For example:
   1. Bind `Run` to `Shift`
   2. Bind `Reload` to `R`
   3. Bind `Zoom` to `RMB`
3. In the Multiplayer Options menu:
   1. Set your player name.
   2. Set your connection speed to T3. This will set your "netspeed" to the maximum value of 20,000 bytes per second.

## Playing Single-Player Games

You can now play the campaign, a custom mission, or a training scenario.
To unlock all maps in custom missions, press `~` at the main menu and enter the command `unlockall`.

## Playing Multi-Player Games

Ubisoft shut down the authentication servers for Raven Shield in 2016, so we use OpenRVS to point our clients at a new set of servers.

1. Download the latest version of OpenRVS from [Github](https://github.com/OpenRVS-devs/OpenRVS/releases), and follow the instructions there to install it.
2. You will need to update `system\R6GameService.dll` in order to remove another place where the game makes outbound calls to Ubisoft servers. Either run Chriswak's [R6GameService_Patcher](https://github.com/eth0up/R6GameServicePatcher) or use [the prebuilt copy from this repo](R6GameService.dll). If unpatched, the game will hang any time it tries to reach Ubisoft servers during regular gameplay.
3. Join a server and party like it's 2003!

Note: Since we are using a fixed list of servers, the list cannot be filtered (using the bottom menu) or sorted.

Players can optionally edit `Servers.list` to choose which servers are displayed when online servers cannot be reached.
You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.

### Servers Currently Online

OpenRVS 1.5 and later will retrieve servers from https://openrvs.org/servers.
OpenRVS servers will automatically self-register with this registry when they start, so no one needs to maintain a server list.
The code which powers this service can be seen [here](https://github.com/willroberts/openrvs-registry).

You can see a list of currently active servers at https://openrvs.org/live.
The code which powers this service can be seen [here](https://github.com/willroberts/openrvs-stats).

## Installing Expansions

### Athena Sword

Athena Sword (March 9 2004) is an expansion which adds 19 maps (including 8 designed for multiplayer), 4 game modes, and 7 weapons.
In the Steam version of Raven Shield, Athena Sword is installed separately in your Steam Library.

Note: Installing Athena Sword in Steam may overwrite `<YourGameDir>\system\R6ClassDefines.ini`.
Be sure to install OpenRVS after installing Athena Sword.

To play offline:
1. Launch Athena Sword from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Athena Sword' -> 'Activate'
1. To revert, activate 'Raven Shield' instead.

To play online, join the `ALLR6 | AthenaSword+IronWrath` server.

### Iron Wrath

Iron Wrath (June 9 2005) is an expansion which adds 18 maps (including 8 designed for multiplayer), 5 game modes, and 6 weapons.

In order to add Iron Wrath to a Steam installation, follow these steps:
1. Download Iron Wrath's unpacked files [here](https://www.moddb.com/games/tom-clancys-rainbow-six-3-raven-shield/downloads/rainbow-six-3-iron-wrath-manual-installation).
2. Copy `IronWrath` and `IronWrath.mod` to `<YourGameDir>\Mods`.

To play offline:
1. Launch Raven Shield from Steam
1. Click 'Settings' -> 'Custom Game' -> 'Iron Wrath' -> 'Activate'
1. To revert, activate 'Raven Shield' instead.

To play online, join the `ALLR6 | AthenaSword+IronWrath` server.

## Additional Documentation

- [Hosting a Server](SERVERS.md)
- [Mods and Custom Content](MODS.md)

## Community Resources

- [AllR6 Discord](https://discord.com/invite/QnXXqcK)
