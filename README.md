# Playing Rainbow Six 3: Raven Shield in 2020 and Beyond

## Obtaining the Game

Raven Shield (released 2003) is typically [$9.99 on Steam](https://store.steampowered.com/app/19830/Tom_Clancys_Rainbow_Six_3_Gold/).
This version contains the Athena Sword expansion, but not the Iron Wrath expansion (see [EXPANSIONS.md](EXPANSIONS.md)).

Alternatively, you can use your original CDs if you also patch to version 1.60.

## Playing the Game

### Essential Improvements

1. Check the [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Tom_Clancy%27s_Rainbow_Six_3:_Raven_Shield) for any tweaks you might want to perform.
2. In the game options, rebind the controls as desired. For example:
  1. Bind `Run` to `Shift`
  2. Bind `Reload` to `R`
  3. Bind `Zoom` to `RMB`
3. In the Multiplayer Options menu:
  1. Set your player name.
  2. Set your connection speed to T3. This will set your "netspeed" to the maximum value of 20,000 bytes per second.

### Single-Player

You can now play the campaign, a custom mission, or a training scenario.
To unlock all maps in custom missions, press `~` at the main menu and enter the command `unlockall`.

### Multi-Player

Ubisoft shut down the authentication servers for Raven Shield in 2016, so we use OpenRVS to point our clients at a new set of servers.

1. Download the latest version of OpenRVS from [Github](https://github.com/OpenRVS-devs/OpenRVS/releases), and follow the instructions there to install it.
2. You will need to update `system\R6GameService.dll` in order to remove another place where the game makes outbound calls to Ubisoft servers. Either run Chriswak's [R6GameService_Patcher](https://github.com/eth0up/R6GameServicePatcher) or use [the prebuilt copy from this repo](R6GameService.dll). If unpatched, the game will hang any time it tries to reach Ubisoft servers during regular gameplay.
3. Join a server and party like it's 2003!

Note: Since we are using a fixed list of servers, the list cannot be filtered (using the bottom menu) or sorted.

Players can optionally edit `Servers.list` to choose which servers are displayed when online servers cannot be reached.
You can force the usage of this file by editing `openrvs.ini` and changing the value of `ServerListURL` to an invalid URL, such as `http://127.0.0.1/servers`.

### Servers Currently Online

OpenRVS 1.5 and later will retrieve servers from the [OpenRVS Registry](https://openrvs.org/servers).
OpenRVS servers will automatically register with this registry, so no one needs to maintain a server list.
The code which powers this service can be seen [here](https://github.com/willroberts/openrvs-registry).

You can see a list of currently active servers at https://openrvs.org/live.
The code which powers this service can be seen [here](https://github.com/willroberts/openrvs-stats).

## Additional Resources

- [Expansions](EXPANSIONS.md)
- [Mods and Custom Content](CUSTOM.md)
- [Hosting a Server](SERVERS.md)
- [AllR6 Discord](https://discord.com/invite/QnXXqcK)
