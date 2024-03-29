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
- [ReShade & vkbasalt](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#ReShade--vkbasalt>)
- [VR](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#vr>)

# Getting Started

## Controls

I've made a layout (creatively named "Raidriar's Layout") you can use that should cover the majority of controls you might commonly use, I have some buttons left over as I plan on expanding the layout but it should remain mostly similar to how it is now. There are more layouts the community has made but I will be going over mine here.

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

## Native or Proton

Native is currently not recommended, as it requires manual fixing. You'll likely want to use Proton.

All tested & working Proton versions:
- Proton 8
- Proton 9
- Proton Experimental
- [Proton GE 8](<https://github.com/GloriousEggroll/proton-ge-custom>)
- [Proton GE 9](<https://github.com/GloriousEggroll/proton-ge-custom>)

By default Steam will download the native Linux build, in order to use the Windows version with Proton you will need to force it in Resonite's properties (`Properties < Compatibility`). From there you can choose any version of Proton you want.

To install Proton GE, either download [ProtonUp-Qt](<https://github.com/DavidoTek/ProtonUp-Qt>) through discover in desktop mode, or use the [Wine Cellar](<https://github.com/FlashyReese/decky-wine-cellar>) plugin for [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>).

## Performance & Battery Life

Unfortunately there's not much that can be done about this right now, but there are some options.
**DISCLAIMER**, *I modify my own Steam Deck with 3rd party tools and hardware modifications to improve performance, my Steam Deck's performance is not indicative of a stock Steam Deck's performance.*

**Readily available options (quick access menu/in app options)**

*Framerate Limit (QAM)* - Change at your discretion, in active sessions it's rare to have more then 30 fps currently so it's safe to limit it to 30 fps, though it will still run at 60 hz (90 hz on OLED). You can do 40 fps/hz to conserve power.

*Disable Frame Limit (QAM)* - Disables Framerate Limit and falls back to 60 fps/hz, not recommended

*Allow Tearing (QAM)* - No effect, Resonite forces vsync

*Half Rate Shading (QAM)* - slightly reduces text readability (excluding the dashboard) and improves battery life, somewhat recommended

*TDP Limit (QAM)* - From testing, Resonite seems to rarely use more then 10 watts, from my understanding due to the inability to run fast enough to draw more than 10 watts. Your milage may vary, tweak as needed.

*Fixed GPU Clock (QAM)* - not tested enough, tweak as needed

*Upscaling (QAM)* - you will need to force the game resolution in Steam (`Properties < General < Game resolution`). I recommend 1024x640 as that maintains text readability fairly well. you can go down to 800x500 and still have a decent experience but don't expect to read text very well. You'll also need to back out and go back into properties to enable the `Set resolution for internal and external display` option, from my experience that's needed in order for Resonite to respect this setting. *Do keep in mind that upscaling is trading GPU cost for CPU cost, and while that's usually a net gain, Resonite is currently CPU bound so the potential gain may not be worth it.*

**Launch Options (`Properties < General < Launch Options`)**

`-donotautoloadhome` - Disables the cloud home from booting on startup, making startup quicker.

`taskset -c 0,2,4,6 %command%` - "Disables" SMT for Resonite specifically, primarily beneficial on desktop mode or with multiple applications running. (if `%command%` is already there, only add `taskset -c 0,2,4,6`)

**3rd Party Tools (use at your own risk)**

[Cryo Utilities](<https://github.com/CryoByte33/steam-deck-utilities>) - RAM, VRAM, Swap, and storage optimizations. You'll likely need this to be able to reliable join moderately sized worlds without running out of RAM and crashing.

[Powertools](<https://git.ngni.us/NG-SD-Plugins/PowerTools>) - [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin that exposes more options to tweak performance, for most users I'd only recommend this for the CPU governor options (the powersave option can extend the battery life quite a bit)

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

Yes, it is possible to run Headless sessions without containers or virtual machines on a Steam Deck. Yes, it performs well, incredibly well actually.

**Some really important info to get out of the way first**

This is gonna be the most advanced section in this guide so I'd only recommend this if you're comfortable with terminals.

This guide will go over installing and running the headless client completely natively, if you want to run a virtual machine instead (giving you a more traditional headless client experience) then install Gnome Boxes from discover and follow a normal setup guide.

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
    - `sudo pacman -Sy`
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

- [NoSteamScreenshots](<https://github.com/Raidriar796/NoSteamScreenshots>) - Prevents Steam from saving an additional copy of photos you save in game, this also stops hitches from saving photos

    - *Highly recommended if you're primarily using in app cameras*

- [ResoniteIkCulling](<https://github.com/Raidriar796/ResoniteIkCulling>) - Disables IK that's out of view and/or far away. Includes IK throttling options.

    - *Primarily helps thermals and battery life in testing, highly recommended*

- [ShadowDistanceChanger](<https://github.com/art0007i/ShadowDistanceChanger>) - Allows for the max range of shadow visibility to be configured.

    - *Slight reduction of GPU power consumption when reduced at the cost of shadow quality but usually gives very little to no fps improvement, slightly recommended*

Not available in Resolute:

- [DisableFXAA](<https://github.com/FalsePattern/DisableFXAA>) - Disables FXAA anti aliasing.

    - *Worsens upscale quality and causes jagged edges to be more jarring, but text readability is vastly improved*

- [Outflow](<https://github.com/bluecyro/outflow>) - Reduces join lag by preventing streaming threads from being clogged by user joins, only applies to sessions you're hosting

    - *Highly recommended if you host sessions often, I commend you if you host sessions often on Deck*


## ReShade & vkbasalt

It is possible to install ReShade on a Steam Deck, not only that but it does work with Resonite.

Now why would you want to do this? Currently the only options we have for antialiasing are FXAA and CTAA (with the launch argument `-ctaa`). Both aren't exactly great and some users, *myself included,* disable FXAA with a mod. Despite the increased jagged edges, it helps readability and clarity.

This can be extended by supplying SMAA and Contrast Adaptive Sharpening (CAS) through ReShade for even better visuals. Of course, with ReShade installed you can use a plethora of other shaders, but the goal here is to at least get SMAA and CAS working. (I do not recommend this if you're not disabling FXAA, the visuals just get muddier)

***Discliamer: This is assuming you're using Proton, this part of the guide will be updated when the native build is in a more functional state***

Installation:

1. Go to [reshade-steam-proton](<https://github.com/kevinlekiller/ReShade-steam-proton>) and follow the instructions to download and run the script

2. Follow instructions and answer the prompts with 2 specific differences:
- When prompted if you want the script to detect the right dll files, say no with `n`
- When prompted to enter the dll override, enter `dxgi`

3. Launch Resonite in either Desktop or Game Mode

4. Press the Home key to open the ReShade window and enable SMAA.fx and CAS.fx

The Steam virtual keyboard does not have the Home key, if you do not have an external keyboard, you can edit the ReShade.ini file in the Resonite folder and change the keybind referencing [this list](<https://learn.microsoft.com/en-us/dotnet/api/system.windows.forms.keys?view=windowsdesktop-6.0>)

Now you can have SMAA and/or CAS in Resonite alongside whatever other shaders you may want to use, keep in mind heavy shaders come with heavy performance drops.

Alternative method:

If you'd like SMAA/CAS in a more broad sense, you can install [vkbasalt](<https://github.com/simons-public/steam-deck-vkbasalt-install>) to easily get SMAA/CAS system wide for anything running with vulkan (which applies to Resonite when using Proton). Downsides include no UI, disabling has to be done on a per game basis, and it supports reshade shaders and not every shader will work with vkbasalt.

## VR

**No.**

While it is possible to run VR on a Steam Deck, people have run Resonite in VR on a Steam Deck, but the experience is pretty awful in anything that's not an incredibly light session, it also puts a lot of strain on the Steam Deck. I cannot recommend trying it for any serious reason.
