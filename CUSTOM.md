# Mods and Custom Content

## Installing Custom Content

### Maps

Two large sources of custom maps are [rvs.go2.rip](https://rvs.go2.rip/maps) and [woody2000.com](http://www.woody2000.com/download.php?list.2).

Custom maps will often come as a `.exe` file which extracts its contents when you run it. You can point these at your game directory to have it put files in the right places. If you have security concerns about running such a program, you can alternatively run the program inside a Windows XP VM and then take out the resulting files.

If the map is already extracted, it will generally have a series of folders to be copied into your game directory: `maps` for the map itself, `system` for the map config, `staticmeshes` and `textures` for some maps, etc. Copy the contents of these folders into their corresponding game folders to install the content.

When playing on servers which allow you to download custom content, these files will be placed in the `<YourGameDir>\Cache` directory. See `Cache.ini` to identify which file is which.

### Sounds

There are prebuilt sound packs such as the [AllR6 Sound Pack](http://allr6.com/discuss/viewtopic.php?id=68&i=1), which includes Athena Sword and Iron Wrath sounds.

## Clearing the Content Cache

If you want to clear the cache of custom content you've downloaded, open `<YourGameDir>\Cache` and delete its contents. The `.ini` file will be automatically recreated by the game.

## Running Servers with Custom Content

#### Disk Space Requirements

A basic Linux Droplet will give you 25GB of storage, which may not be enough to host your custom content. If that's the case, you'll need to upgrade to a larger Droplet type.

#### Download Speeds

You may find in testing that download speeds for custom content are much slower than expected. When using a VPS to host game servers, one can expect download speeds of roughly 20KB/s. A basic web host or file server can generally transfer at speeds up to 100Mb/s in short bursts. In order to offload this activity to a faster server/network, we can use Raven Shield's built-in download redirection:

1. Configure an HTTP server (such as Nginx, or a paid web hosting service) which can serve files.
1. Place custom content on the file server in the same directory structure as the game: maps in `/maps/`, textures in `/textures/`, etc.
1. On your game server, edit `RavenShield.ini` and look for the `RedirectToURL` option. Set this to the URL of your file server, e.g. `http://www.myserver.net/`.
1. Restart your game server to pick up the new config.

When users connect to your game server, they will be instructed to download all custom content from the file server, resulting in significantly faster downloads. If the client fails to retrieve the file from the file server for any reason, it will fall back to downloading the file from the game server, resulting in slow speeds. If this happens, the player can cancel and rejoin the server to restart the download from the file server.

## Creating Custom Content

### Creating Maps

See the [RvSMaps.com guide](http://rvsmaps.smclan.org/tut_sounds.htm).

### Creating Mods

See [Twi's Raven Shield SDK on ModDB](https://www.moddb.com/mods/raven-shield-software-development-kit). This includes a copy of the game's source code (version 1.56).
