# Resonite-On-Steam-Deck
 
This is a community maintained list of stuff you can do to improve using Resonite on the Steam Deck. This list will change over time as needed, feel free to give suggestions or corrections by opening an issue.

## Table of Contents

**Getting Started**
- [Controls](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#controls>)
- [Native or Proton](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#native-or-proton>)
- [Performance & Battery Life](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#performance--battery-life>)
- [Screenshot management with Proton](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#screenshot-management-with-proton>)

**Info**
- [Steam Deck & Steam Deck OLED differences](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#steam-deck--steam-deck-oled-differences>)
- [Wine Experimental Wayland Driver](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#wine-experimental-wayland-driver>)

**Advanced**
- [Headless Sessions](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#headless-sessions>)
- [Mods](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#mods>)
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

## Native or Proton

**The native build will be deprecated soon, this will update soon once the change is in effect**

Native is currently not recommended, as it has many issues the Windows build doesn't. Proton is selected for you so there's not much you need to do.

If you still want to use the native build, you will need to force it in Resonite's properties (`Properties < Compatibility`). From there you can choose Steam-Linux-Runtime or Steam-Play-None

All tested & working Proton versions:
- Proton 8
- Proton GE 8
- Proton 9
- Proton GE 9
- Proton Experimental

To install [Proton GE](<https://github.com/GloriousEggroll/proton-ge-custom>) or [Steam-Play-None](<https://github.com/Scrumplex/Steam-Play-None>), either download [ProtonUp-Qt](<https://github.com/DavidoTek/ProtonUp-Qt>) through discover in desktop mode, or use the [Wine Cellar](<https://github.com/FlashyReese/decky-wine-cellar>) plugin for [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>).

## Performance & Battery Life

This section will give recommended settings for Resonite and for the options in the Steam Deck's Quick Access Menu, You can go even lower then what's recommended here but I'm aiming to preserve visuals while still helping performance, feel free to go lower but keep in mind what you're doing in reducing the settings further.

**DISCLAIMER:** *I modify my own Steam Deck with 3rd party tools and hardware modifications to improve performance, my Steam Deck's performance is not indicative of a stock Steam Deck's performance.*

**Launch Options (`Properties < General < Launch Options`)**

- `DXVK_FRAME_RATE=60 taskset -c 0-5 %command% -BackgroundWorkers 6 -PriorityWorkers 5`

  - `DXVK_FRAME_RATE=` is an environment variable which specifies a framerate limit at a lower level than setting it in Steam or Resonite. Here's a couple of recommended values:
    - `60` for smoothness (you will rarely hit 60 under normal usage)

    - `40` for 40/80 hz refresh rate power saving

    - `30` for general power saving 

  - This specific `taskset` command only allows Resonite to use the first 3 cores of the system, leaving the last core available for the rest of the system. This will reduce Resonite's multithreading performance but will prevent the system from suffocating in heavier sessions, especially on Desktop Mode.

  - `%command%` is what steam uses to figure out where to put launch args, so you can insert environment variables and launch arguments before and after the actual command to run the game.

  - `-BackgroundWorkers 6` reduces the background workers in Resonite to match the CPU affinity set by `taskset`, Resonite usually automatically allocates background workers based on your CPU thread count.

  - `-PriorityWorkers 5` reduces the priority workers in Resonite to match the CPU affinity set by `taskset`, Resonite usually automatically allocates priority workers based on your CPU thread count minus 1.

**Recommended Quick Access Menu Settings**

*Note: framerate limit and refresh rate settings will vary if you have unified frame limit management enabled*

Relevant setting: `Steam Menu < Settings < Display < Enable Unified Frame Limit Management`

*With unified frame limit management:*
- Frame limit - n/a
  - This setting is locked when the frame limit is disabled on the current stable branch of SteamOS
- Disable Frame Limit - On

*Without unified frame limit management:*
- Framerate Limit - Off
- Refresh Rate - 40 hz on LCD/40 hz or 80 hz on OLED

*Unaffected by unified frame limit management:*
- Allow Tearing - On
- Half Rate Shading - Off
- TDP Limit - 9W
- Manual GPU Clock - Off
- Upscaling - FSR
  - To be able to upscale, you will need to force the game resolution in Resonite by disabling fullscreen and setting a Window Resolution lower than the display's resolution
  - 1280x720 for docks
  - 1024x640 for text readibility
  - 960x600 for battery life

**Recommended Resonite Settings**

*User Interface < Quick Photo Capture*
- Encode Format - WebP

*Profile < Favorites*
- Load cloud home on startup - Off

*Graphics < Texture Quality*
- Relative Texture Size - Quarter Size
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
- Shadow Distance - 64
- Skin Weights - Two Bones

*Graphics < Desktop Render Settings*
- Field of view - 70
  - Recommended for uniform visuals, especially while creating content
- VSync - Off
- Limit framerate when in background - Off
  - Only relevant when using Desktop Mode
- Maximum background framerate - 10

*Graphics < Post Processing*
- Motion Blur Intensity - 0%
- Bloom Intensity - 50%
  - Keep in mind - you may want to at least keep bloom on as it has little improvement when disabling, it additionally has a practical use in content creation and stuff may be designed around it.
- Ambient Occlusion (AO) Intensity - 0%
- Screen Space Reflections - Off
- Antialiasing (AA) - Off 
  - If you're upscaling:
    - CTAA with FSR Sharpness 3 for general use
    - SMAA with FSR Sharpness 1 for content creation/text readibility

*Network < Asset Gathering*
- Maximum number of concurrent asset transfers - 2
  - This only effects sessions you're hosting
- Maximum number of concurrent downloads - 4

*Integrations < Steam Integration*
- Save Screenshots - Off
  - This prevents saving photos twice, more info later in the guide

**3rd Party Tools (use at your own risk)**

- [Cryo Utilities](<https://github.com/CryoByte33/steam-deck-utilities>)
  - RAM, VRAM, Swap, and storage optimizations.
  - You'll likely need this to be able to reliable join moderately sized worlds without running out of RAM and crashing.

- [Powertools](<https://git.ngni.us/NG-SD-Plugins/PowerTools>)
  - [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin that exposes more options to tweak performance.
  - For most users I'd only recommend this for the CPU governor options (the powersave option can extend the battery life quite a bit)

## Screenshot management with Proton

When using Proton, steam will create a lot of extra folders that mimic the folder structure of Windows to allow for compatibility when games try to reference Windows specific directories. This is important because Resonite has an in game screenshot function which saves to `C:\Users\[YourUser]\Pictures\Resonite` by default. This causes Resonite to save screenshots to a really annoying location, this can be made easier though. To do so:

1. Go to `/home/deck/.steam/steam/steamapps/compatdata/2519830/pfx/drive_c/users/steamuser/pictures/`

2. Left trigger (right click) and do `Create New > Link to File or Directory...`

3. Set the name to "Resonite" and the directory to `/home/deck/Pictures/Resonite` (or anywhere else you may want to save screenshots to)

Now whenever Resonite saves a photo, it tries to save to `C:\Users\[YourUser]\Pictures\Resonite` but instead saves it to `/home/deck/Pictures/Resonite` or another directory of your choosing.

# Info

## Steam Deck & Steam Deck OLED differences

The refreshed model of the Steam Deck has a good handful of differences that make the device better overall. Despite this, you shouldn't expect better performance with the refreshed model. Here's what you can expect with the Steam Deck OLED.

- Longer battery life - the more efficient APU as well as the larger battery will allow for longer usage
- Faster RAM - the refreshed model contains RAM speeds of 6400 MT/s, compared to the original model's 5500 MT/s, that's a pretty huge jump, but not world changing. This will allow for faster asset loading in Resonite.
- More stable connection - the new Wi-Fi 6E capabilities of the refreshed model will offer better connection reliability to sessions and faster asset downloading, provided you aren't limited by your internet.

That's it. There's a lot of nice changes with the refreshed model but nothing game changing for Resonite, but it shouldn't perform any worse.

## Wine Experimental Wayland Driver

Wine 9.0 released with an experimental Wayland driver, which sounds great on paper, but has a lot of issues for use on the Steam Deck.

**How do I get the Wayland driver?**

The driver must be included with a flag on compilation and not every distribution of Wine includes the flag, so you may need to compile it yourself, which already adds a pretty high barrier to entry for the purposes of this guide.

**Can it even work on the Deck?**

In Game Mode, the display output is handled by Gamescope, which uses xwayland to make x11 apps output in Wayland, so it ends up doing nothing when using the Wayland driver.

In Desktop Mode, the desktop session is x11, so once again the driver does nothing for us there. You can install the KDE Wayland session which, while disregarding the other issues that introduces, will allow you to use the driver.

**So is there any benefit to the Wayland driver for Resonite on Deck?**

Not really. You have to go pretty far out of your way to even get it set up and even then, you are working with tradeoffs by switching Desktop Mode to run in Wayland. There is a slight performance benefit in running it natively but you'll likely get practically equal performance out of just running Resonite in Game Mode.

**What about Proton 9.0?**

Proton 9.0 does not include the driver nor can you just download and compile it with the driver as the required files for compiling with the driver are not present in the repository. Some modifications of Proton 9.0 may include the driver but I am not aware of any that do yet.

# Advanced

## Headless Sessions

**The headless client has updated to use .Net 8.0 instead of Mono for it's runtime. This part of the guide is currently out of date but the process is mostly the same for the new version. An update is in the works**

Yes, it is possible to run Headless sessions without containers or virtual machines on a Steam Deck. Yes, it performs well, incredibly well actually.

**Some really important info to get out of the way first**

This is gonna be the most advanced section in this guide so I'd only recommend this if you're comfortable with terminals.

This guide will go over installing and running the headless client completely natively, if you want to run a virtual machine instead (giving you a more traditional headless client experience) then install Gnome Boxes from discover and follow a normal setup guide, I recommend either of the following guides:

- [Resonite Wiki](<https://wiki.resonite.com/Headless_Server_Software/Setup>)

- [Bredo's Guide](<https://gist.github.com/bredo228/ac063763f6acf35532716d66c2313821>)

The Headless client is not provided with Resonite, it is required that you pay for the appropriate Patreon tier in order to gain access to the software. This guide assumes you have access to the client already if you're continuing through this section.

The Steam Deck uses an A/B partition structure, where SteamOS sits on one partition that is mostly reset whenever SteamOS updates, and the other partition is where all user data is stored and is not touched by updates. With this in mind, everything we're about to install with the terminal *will* be deleted whenever SteamOS updates. The setup process requires a slight difference in installation after an update, but there is an alternative to installing what's needed everytime. The tool [rwfus](<https://github.com/ValShaped/rwfus>) allows you to download packages through the terminal and have them persist through SteamOS updates, **use this at your own risk.**

**Installation & Setup**

1. Install Mono
- Switch to desktop mode and open Konsole
- Set up a password with the `passwd` command if you haven't already
- Run the following commands:
    - `sudo steamos-readonly disable`
    - `sudo pacman-key --init`
    - `sudo pacman-key --populate`
    - `sudo pacman -Syu`
    - `sudo pacman -S mono`
- *If installing Mono after a SteamOS update without rwfus, run the following command instead of the last command*
    - `sudo pacman -S --overwrite \* mono`
- To make sure mono is installed, run `mono --version`. As of writing it should be version 6.12.0.

2. Install the Headless client
- Open your steam library and go to Resonite
- Go into Properties and into the Betas tab
- Enter the beta code for the Headless client if not done already
- Change from "None" to "headless - Builds including headless server" and wait for Steam to update Resonite. *Note: disable force using Proton if you aren't already using the native Linux build.*
- Open Konsole and run the following commands:
    - `cd ~/.steam/steam/steamapps/common/Resonite/Headless`
    - `mono Resonite.exe`
- The Headless client should startup, you can shut it down whenever, this is just to make sure it's working and to generate any needed files.

3. Configure the Headless client
- Go to the directory `/home/deck/.local/share/Steam/steamapps/common/Resonite/Headless/Config/` in Dolphin or Konsole
- duplicate "DefaultConfig.json" and name the new file "Config.json"
- Modify "Config.json" as needed, primarily account credentials, worlds to run, and permissions.

Congradulations, you can now host Headless sessions on your Steam Deck. As stupid as it sounds, if you don't have another PC you can dedicate to a Headless and don't want to/can't pay for a server, this is a legitimately viable option for self hosting Headless sessions.

## Mods

Resonite modding currently isn't big or game changing. The scope of what can be modded is fairly limited and the vast capabilities of Resonite remove a lot of the need for modding, despite this, a modding scene exists. It primarily consists of quality of life fixes or slight feature additions or improvements.

If you prefer an experience slightly above tolerable then this is the way to go. You'll need to go to Desktop Mode for this.

There are a couple of mod loaders but the primary one is currently [ResoniteModLoader](<https://github.com/resonite-modding-group/ResoniteModLoader>). I won't give a full guide on setting up mods as RML already has a guide which is applicable to the Steam Deck.

**Mod manager**

There is an in-development mod manager that can actually be used on the Steam Deck right now.

The mod manager, [Resolute](<https://github.com/Gawdl3y/Resolute>), can be downloaded and setup to run without the need to go to Desktop Mode, but for now it requires slight configuration to get working.

**Setting up the mod manager**

1. From the [releases page](<https://github.com/Gawdl3y/Resolute/releases>), download the `.AppImage`

2. Open the application

3. enter the install location to Resonite if it's not auto detected correctly (by default: `/home/deck/.local/share/Steam/steamapps/common/Resonite`)

Resolute is now setup to run and install the mod loader and mods, but more can be done to increase ease of access. It can also update itself when new releases come out.

**Setting up the mod manager in Steam**

1. Move the app to a folder such as `/Home/deck/Applications` or wherever you'd like to store it

2. rename it, I'd suggest just naming it "resolute.AppImage"

3. Right click (left trigger) the file and click `Add to Steam`

It will now work in Game Mode. If you need to manually update it, you'll want to revisit the releases page and download the latest AppImage, replace the previous AppImage with the new file, and rename it to "resolute.AppImage" (or whatever it was named before) so nothing needs to be reconfigured in Steam.

**Recommended Mods**

*Available in Resolute:*

- [CacheGetClapped](<https://github.com/dfgHiatus/CacheGetClapped>) - Smart cache management, clears old cache files and can keep cache size within specified limit. 

    - *Highly Recommended, especially for 64/256 GB models.*

- [DynBoneWrangler](<https://github.com/isovel/DynBoneWrangler>) - Disables dynamic bone chains when under a user specified fps limit and re-enables them when above another user specified fps limit.

    - *Prevents shakey dynamic bones at frequently low framerates, may improve frame stability.*

- [ResoniteIkCulling](<https://github.com/Raidriar796/ResoniteIkCulling>) - Disables IK that's out of view and/or far away. Includes IK throttling options.

    - *Primarily helps thermals and battery life in testing, highly recommended*

- [Outflow](<https://github.com/bluecyro/outflow>) - Reduces join lag by preventing streaming threads from being clogged by user joins, only applies to sessions you're hosting

    - *Highly recommended if you host sessions often, I commend you if you host sessions often on Deck*

## VR

**No.**

While it is possible to run VR on a Steam Deck, I and other Resonite users have run Resonite in VR on a Steam Deck, but the experience is pretty awful in anything that's not an incredibly light session, it also puts a lot of strain on the Steam Deck. I cannot recommend trying it for any serious reason.
