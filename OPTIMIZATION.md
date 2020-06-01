# Optimization

If you are experiencing lag during gameplay, first test an offline custom mission to eliminate the possibility of Internet lag.

If you are still experiencing lag, there are two files which can be tweaked to improve game performance:

## YourGameDir\Mods\RavenShield.mod

1. Under `[Engine.GameEngine]`, increase `CacheSizeMegs` from `32` to `512`. This is the value used by `UnrealEd.exe`, so we know at least this maximum size is supported

## YourGameDir\system\RavenShield.ini

1. Under `[Engine.GameEngine]`, increase `CacheSizeMegs` from `32` to `512`. This is the value used by `UnrealEd.exe`, so we know at least this maximum size is supported
1. Under `[WinDrv.WindowsClient]`, set `TextureMaxLOD` to `16` (from `12`). Higher values reduce the quality of distant textures
1. Under `[WinDrv.WindowsClient]`, set `MinDesiredFramerate` to `60` (from `10`)
1. Under `[D3DDrv.D3DRenderDevice]`, set `UsePrecaching` to `True`
1. Under `[D3DDrv.D3DRenderDevice]`, set `UseCompressedLightmaps` to `True`

There are some additional settings here which may be useful to tweak:

```
[D3DDrv.D3DRenderDevice]
HighDetailActors=True
UseTrilinear=True
UseTripleBuffering=False
UseHardwareTL=True
UseHardwareVS=True
UseCubemaps=True
MaxPixelShaderVersion=255
DetailTextures=True
```
