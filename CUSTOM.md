# Custom Content in Rainbow Six 3: Raven Shield

## Installing Custom Content

### Maps

Custom maps will often come as a `.exe` file which extracts its contents when you run it. You can point these at your game directory to have it put files in the right places. If you have security concerns about running such a program, you can alternatively run the program inside a Windows XP VM and then take out the resulting files.

If the map is already extracted, it will generally have a series of folders to be copied into your game directory: `maps` for the map itself, `system` for the map config, `staticmeshes` and `textures` for some maps, etc. Copy the contents of these folders into their corresponding game folders to install the content.

When playing on servers which allow you to download custom content, these files will be placed in the `<YourGameDir>\Cache` directory. See `Cache.ini` to identify which file is which.

### Sounds

The quickest way to get all the sound files you need for OpenRVS servers is the [AllR6 Sound Pack](http://allr6.com/discuss/viewtopic.php?id=68&i=1), which includes Athena Sword and Iron Wrath sounds.

### Skins

TBD

## Hosting Custom Content

There are two things to consider when running servers which host custom content:

### 1. You'll need additional disk space for the content

A basic Linux Droplet will give you 25GB of storage, which may not be enough to host your custom content. If that's the case, you'll need to upgrade to a larger Droplet type.

### 2. Players will need to download the content

You may find in testing that download speeds for custom content are much slower than expected. When using a VPS to host game servers, one can expect download speeds of roughly 20KB/s. A basic web host or file server can generally transfer at speeds up to 100Mb/s in short bursts. In order to offload this activity to a faster server/network, we can use Raven Shield's built-in download redirection:

1. Configure an HTTP server (such as Nginx, or a paid web hosting service) which can serve files.
1. Place custom content on the server in the same directory structure: maps in `/maps/`, textures in `/textures/`, etc.
1. On your server, edit `RavenShield.ini` and look for the `RedirectToURL` option. Set this to the URL of your server, e.g. `http://www.myserver.net/`.
1. Restart your server to pick up the new config.

When users connect to your server, they will be instructed to download all custom content from the file server, resulting in significantly faster downloads.
