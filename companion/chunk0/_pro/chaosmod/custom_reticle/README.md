export to GFXI as described in BBArt at https://github.com/shadow578/Hitman_BoldAndBrashArt/blob/main/docs/FORMATS.md#ui-graphics-gfxi


> export as .GFXI using GlacierKit for reference, then open the .GFXI in Photoshop using the Intel Texture Works Plugin (or NVIDIA Texture Tools, but that seems somewhat outdated imo). edit texture normally, then save back as .DDS with BC7 compression, and (if needed) change file extension back to .GFXI. place the .GFXI and .GFXI.meta files in the correct chunk's folder, and SMF will take care of the rest during deploy.

for transparency, update settings to:
- Texture type: Color + Alpha
- Compression: BC7 8bpp Fine (sRGB, DX11+)
- Mip Maps: None

