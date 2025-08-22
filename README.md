# Resonite-On-Steam-Deck
 
This is a community maintained list of stuff you can do to improve using Resonite on the Steam Deck. This list will change over time as needed, feel free to give suggestions or corrections by opening an issue.

## Table of Contents

**Getting Started**
- [Controls](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#controls>)
- [Proton](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#proton>)

**Further Improvements**
- [Performance & Battery Life](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#performance--battery-life>)

**Advanced**
- [Headless Sessions](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#headless-client>)
- [lsfg-vk](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#lsfg-vk>)
- [Mods](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#mods>)
- [Satori](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#satori>)
- [VR](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#vr>)

# Getting Started

## Controls

I've made a layout (creatively named "Raidriar's Layout") you can use that should cover the majority of common controls, I have some buttons left over as I plan on expanding the layout but it should remain mostly similar to how it is now.

There are more layouts the community has made and I recommend checking other's out to see if another one works for you better. This guide for now will be focusing on just the one I'm making.

- *A* - Jump
- *B* - Crouch
- *X* - Secondary
- *Y* - Mute
- *L1* - 3rd Person
- *R1* - UI Focus Mode
- *L2* - Right Click
- *R2* - Left Click/Primary
- *L4* - Slow Walk/Slow Fly
- *R4* - Delete Held Item
- *L5* - Instant Photo
- *R5* - Timed Photo
- *Pause* - Dashboard
- *Select* - Context Menu
- *DPad Up* - Scale Up/Zoom In/Scroll Up
- *DPad Down* - Scale Down/Zoom Out/Scroll Down
- *DPad Left* - Hold to rotate held item with Right Joystick/Right Trackpad
- *DPad Right* - Hold to pan in UI Focus Mode with Right Joystick/RightTrackpad
- *Right Trackpad* - Finer mouse controls
- *Left Trackpad* - ToolTip Radial Menu

In the event you cannot download the layout through Steam directly, you can download it from this repo by right clicking (left trigger) the following link and clicking `Save Link As...`

[**Raidriar's Layout**](<https://raw.githubusercontent.com/Raidriar796/Resonite-On-Steam-Deck/main/controller_neptune.vdf>)

The file will need to be placed in this directory:

`/home/deck/.local/share/Steam/steamapps/common/Steam Controller Configs/[your Steam ID]/config/2519830`

## Proton

For the best compatibility, use the latest stable Proton versions, such as Proton 9. [Proton GE](<https://github.com/GloriousEggroll/proton-ge-custom>) provides little benefit for Resonite, especially on Steam Deck, but it provides better video support over official Proton versions so it may be prefered. 

All tested & working Proton versions:
- Official Proton Versions:
  - Proton 9
  - Proton 10
  - Proton Experimental
- 3rd Party Proton Versions:
  - Proton GE 9
  - Proton GE 10

Currently known broken Proton versions:
- 3rd Party Proton Versions:
  - Proton Cachyos

Official proton versions are accessible directly in Steam, but 3rd party ones can be installed through any of the following methods:

- [ProtonUp-Qt](<https://github.com/DavidoTek/ProtonUp-Qt>), which can be installed through discover in desktop mode
- The [Wine Cellar](<https://github.com/FlashyReese/decky-wine-cellar>) plugin for [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>)
- Manually place the Proton build into `/home/deck/.steam/steam/compatibilitytools.d/`

# Further Improvements

## Performance & Battery Life

This section will give recommended settings for Resonite and for the options in the Steam Deck's Quick Access Menu, You can go even lower then what's recommended here but I'm aiming to preserve visuals while still helping performance, feel free to go lower but keep in mind what you're doing in reducing the settings further.

**DISCLAIMER:** *I modify my own Steam Deck with 3rd party tools and hardware modifications to improve performance, my Steam Deck's performance is not indicative of a stock Steam Deck's performance, but what I mention here should be generally applicable.*

**Launch Options**

```
LD_PRELOAD="" DXVK_FRAME_RATE=60 DXVK_CONFIG="dxgi.maxDeviceMemory = 512;" %command% -SkipIntroTutorial
```

  - `LD_PRELOAD=""` is an environment variable used to load separate libraries in place of the libraries the applications would try to run. In this case, this prevents a library from being loaded by Steam which causes a stuttering issue with keyboard/mouse input after prolonged usage. This is mostly beneficial for use in Desktop Mode
  - `DXVK_FRAME_RATE=` is an environment variable which specifies a framerate limit at a lower level than setting it in Steam or Resonite. Here's a couple of recommended values:
    - `60` for smoothness (you will rarely hit 60 under normal usage)
    - `40` for 40/80 hz refresh rate power saving
    - `30` for general power saving
  - `DXVK_CONFIG="dxgi.maxDeviceMemory = 512;"` does a config override for DXVK that tells dx11 that it has 512 MB of VRAM, this will not prevent Resonite from using more than 512 MB, but it can help keep VRAM usage lower.
    - If you're using Cryo Utilities (shown below), you can try 2048 instead. Feel free to experiment with different values.
  - `%command%` is what steam uses to figure out where to put launch args, so you can insert environment variables and launch arguments before and after the actual command to run the game.
  - `-SkipIntroTutorial` does what it says on the tin. This makes bootup a lot faster after the first time or after clearing the database.

**Quick Access Menu**

- Disable Frame Limit - On

- TDP Limit - 10W

- Manual GPU Clock - Off

- Scaling Filter - Sharp
  - To be able to upscale, you will need to force the game resolution in Resonite by disabling fullscreen and setting a Window Resolution lower than the display's resolution
  - 1280x720 for docks
  - 1024x640 for text readibility
  - 960x600 for battery life

**Resonite Settings**

*NOTICE: Settings labeled with (Synced) will be cloud synced.*

*User Interface < Quick Photo Capture*
- Encode Format - WebP

*User Interface < Cursor Settings*
- Base cursor size (Synced) - 0.05
  - Change as needed, value was picked based on trying to make it clearly visible without covering too much of the screen

*Profile < Favorites*
- Load cloud home on startup - Off

*Graphics < Texture Quality*
- Relative Texture Size - Full Size
  - Quarter Size recommended when [#5314](<https://github.com/Yellow-Dog-Man/Resonite-Issues/issues/5314>) is fixed
- Maximum Texture Size - Tex 1K
- Limit Texture Above Resolution - 512
- Texture Filtering - Anisotropic
- Anisotropic Level - 4

*Graphics < Resolution*
- Fullscreen - Off
  - Upscaling won't work if this is enabled, but you can use it as an upscaling toggle of sorts

*Graphics < Rendering Quality*
- Per Pixel Lights - 4
- Shadow Cascades - None
- Shadow Resolution - Low
- Shadow Distance - 64.00
- Skin Weights - Two Bones

*Graphics < Desktop Render Settings*
- Field of view - 70
- VSync - Off
- Limit framerate when in background - On
  - Only relevant when using Desktop Mode
- Maximum background framerate - 10

*Graphics < Post Processing*
- Motion Blur Intensity (Synced) - 0%
- Bloom Intensity (Synced) - 50%
  - Keep in mind - you may want to at least keep bloom on as it has little improvement when disabling, it additionally has a practical use in content creation and stuff may be designed around it.
- Ambient Occlusion (AO) Intensity (Synced) - 0%
- Screen Space Reflections (Synced) - Off
- Antialiasing (AA) (Synced)- SMAA

*Graphics < Gaussian Splat Rendering Quality*
- Quality Preset - Very Low
- Minimum Locally Compressed Quality - High
  - This is the lowest amount of compression available. This alleviates the cost of compressing splats locally at the cost of higher VRAM usage.
- Sorting Mega-operations per camera - 1.00
  - Gaussian Splats are incredibly GPU bound and will bring the deck to a crawl, you practically have to set this as low as possible to prevent Resonite from becoming unusable while one is active.

*Network < Asset Gathering*
- Maximum number of concurrent asset transfers (Synced) - 4
  - This only effects sessions you're hosting
- Maximum number of concurrent downloads (Synced) - 64

*Integrations < Steam Integration*
- Save Screenshots - Off
  - This prevents saving photos twice

*Misc < OS Settings*
- Keep original screenshot format - On
  - This prevents photos being re-encoded when saved

**3rd Party Tools (use at your own risk)**

- [Cryo Utilities](<https://github.com/CryoByte33/steam-deck-utilities>)
  - RAM, VRAM, Swap, and storage optimizations.

- [Powertools](<https://git.ngni.us/NG-SD-Plugins/PowerTools>)
  - [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin that exposes more options to tweak performance.
  - For most users I'd only recommend this for the CPU governor options (the powersave option can extend the battery life quite a bit)

# Advanced

## Headless Client

Coming soon :)

## lsfg-vk

[lsfg-vk](<https://github.com/pancaketas/lsfg-vk>) is a project to bring the frame generation from [Lossless Scaling](<https://store.steampowered.com/app/993090/Lossless_Scaling/>) to Linux, which includes SteamOS.
This can allow you to reduce CPU usage by cutting the framerate in half and making the GPU fill in the gaps. In general this should reduce overall load and improve battery life with visual artifacts and smearing as the tradeoff.

The [lsfg-vk installation guide](<https://github.com/PancakeTAS/lsfg-vk/wiki/Installation-Guide>) goes over installing for SteamOS, so follow that guide and do the following:
1. Open the lsfg-vk configuration ui and create a new profile with the following:
  - Profile name - Resonite
  - Multiplier - 2
  - Flow Scale - 100
  - Performance Mode - On
2. Set following to your Resonite launch arguments:
```
LSFG_PROCESS=Resonite DXVK_FRAME_RATE=30 %command%
```
  - Set `DXVK_FRAME_RATE` to half of your target framerate, ie 30 for 60 hz, 45 for 90 hz, etc
3. Optionally, if the input latency increase is too much, try setting this:
  - Present Mode - Immediate
    - This will improve input latency at the cost of potentially reduced smoothness

lsfg-vk should now work in Resonite. If you'd like to disable it, you can remove `LSFG_PROCESS` from the launch arguments or remove the profile from your config.

## Mods

Also coming soon :)

## Satori

Satori is a pauseless garbage collector for dotnet, which can result in improved responsiveness in Resonite. This is nice to use in general, but it's much more impactful on lower power devices like the Steam Deck.

To avoid the need for compilation (especially on a Steam Deck), I have provided precompiled files in this guide which you can extract into your Resonite install to use Satori.

To install Satori:
1. Run Resonite at least once
2. Download [Satori.zip](<https://github.com/Raidriar796/Resonite-On-Steam-Deck/raw/refs/heads/main/Satori/Satori.zip>)
3. In your Resonite install, extract the zip into `dotnet-runtime/shared/Microsoft.NETCore.App/9.0.8/` and replace/overwrite files with the same name

That's it. If you'd like to remove Satori, delete the `dotnet-runtime` folder and run Resonite again (or put back the original files if you kept them).

## VR

Yes, even this is coming soon :)
