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

Cached content is automatically deleted after 30 days (configurable in `RavenShield.ini`).

If you want to manually clear the cache, open `<YourGameDir>\Cache` and delete its contents. `cache.ini` will be automatically recreated by the game.

## Running Servers with Custom Content

### Download Speeds

You may find in testing that download speeds for custom content are much slower than expected. When using a VPS to host game servers, one can expect download speeds of roughly 20KB/s. A basic web host or file server can generally transfer at speeds up to 100Mb/s in short bursts. In order to offload this activity to a faster server/network, we can use Raven Shield's built-in download redirection.

### Serving Files with Nginx

Let's assume your server is running on Linux with the following directory structure:

```
/opt/rs/maps/
       /staticmeshes/
       /textures/
```

For clients to download custom content, the files must all be on the same HTTP path. In order to avoid copying files to a second location on the server, we can merge these three paths into one with the following Nginx config:

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /opt/rs;
        server_name <YOUR_IP_OR_DNS_HERE>;
        location ~* ^/(.*)$ {
                try_files /maps/$1 /staticmeshes/$1 /textures/$1 =404;
        }
}
```

Most of the above config starts an HTTP server which listens on port 80. The important bit is the `location` block, which does the following:

- `~*` allows case-insensitive regular expression matching
- `^/(.*)$` parses the text between the first `/` and the end of the URL and saves it as `$1`
- `try_files /maps/$1 /staticmeshes/$1 /textures/$1 =404` will look for your file in `/maps/`, then `/staticmeshes/`, then `/textures` before finally returning a 404 if the file couldn't be found

For example, if you request `http://myserver.com/Streets.utx`, Nginx will try to serve `/opt/rs/maps/Streets.utx` (fails), then `/opt/rs/staticmeshes/Streets.utx` (fails), then `/opt/rs/textures/Streets.utx` (succeeds).

### Directing Clients to Nginx

1. On your game server, edit `RavenShield.ini`
1. Set `AllowDownloads` to `False`. This will prevent users from downloading files from the game server at slow speeds.
1. Set the `RedirectToURL` option to the URL of your file server, e.g. `http://www.myserver.com/`. The trailing `/` must be included.
1. Restart your game server to pick up the new config.

When users connect to your game server, they will be instructed to download all custom content from the file server, resulting in significantly faster downloads.

## Creating Custom Content

### Creating Maps

The map editor, `UnrealEd`, can be found on your hard drive at `<YourGameDir>\system\UnrealEd.exe`. It should be able to open all base game maps and most custom maps.

See the [rvsmaps.com guide](https://web.archive.org/web/20190228151835/rvsmaps.smclan.org/tut_sounds.htm) for more info.

### Creating Mods

See [Twi's Raven Shield SDK on ModDB](https://www.moddb.com/mods/raven-shield-software-development-kit). This includes a copy of the game's source code (version 1.56).
