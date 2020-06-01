# Optimization

There are two files which can be tweaked to improve game performance:

## YourGameDir\Mods\RavenShield.mod

1. Under `[Engine.GameEngine]`, increase `CacheSizeMegs` from `32` to `max_value`. Why?

## YourGameDir\system\RavenShield.ini

TODO: Investigate these settings:

1. CacheSizeMegs=256 (from 32)
1. TextureMaxLOD=16 (from 12)
1. MinDesiredFramerate=50 (from 10)
1. UseCompression=True (from False)
1. UsePrecaching=False (from True)
1. ReduceMouseLag=True (from False)
1. UseCompressedLightmaps=False (from True)
1. UseVSync=False (from True)
1. GoreLevel=3 (from 0)
