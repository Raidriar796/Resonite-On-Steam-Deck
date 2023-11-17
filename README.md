# Resonite-On-Steam-Deck
 
This is a community maintained list of stuff you can do to improve using Resonite on the Steam Deck. This list will change over time as needed, feel free to give suggestions or corrections.

## Table of Contents

- [Controls](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#controls>)
- [Headless Sessions](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#headless-sessions>)
- [Native or Proton](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#native-or-proton>)
- [Performance & Battery Life](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#performance--battery-life>)
- [Screenshot management with Proton](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#screenshot-management-with-proton>)
- [Steam Deck & Steam Deck OLED differences](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#steam-deck--steam-deck-oled-differences>)
- [VR](<https://github.com/Raidriar796/Resonite-On-Steam-Deck#vr>)

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

## Headless Sessions

Yes, it is possible to run Headless sessions without containers or virtual machines on a Steam Deck. Yes, it performs well, incredibly well actually.

**Some really important info to get out of the way first**

This is gonna be the most advanced section in this guide so I'd only recommend this if you're comfortable with terminals.

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
    - *If installing Mono after a SteamOS update without rwfus, run the following command instead*
    - `sudo pacman -S --overwrite \* mono`
- To make sure mono is installed, run `mono --version`. As of writing it should be version 6.12.0.

2. Install the Headless client
- Open your steam library and go to Resonite
- Go into Properties and into the Betas tab
- Enter the beta code for the Headless client if not done already
- Change from "None" to "headless - Builds including headless server" and wait for Steam to update Resonite. *Note: disable force using Proton if you aren't already using the native Linux build.*
- Open Konsole and run the following commands:
    `cd ~/.steam/steam/steamapps/common/Resonite/Headless`
    `mono Resonite.exe`
- The Headless client should startup, you can shut it down whenever, this is just to make sure it's working and to generate any needed files.

3. Configure the Headless client
- Go to the directory `/home/deck/.local/share/Steam/steamapps/common/Resonite/Headless/Config/` in Dolphin or Konsole
- duplicate "DefaultConfig.json" and name the new file "Config.json"
- Modify "Config.json" as needed, primarily account credentials, worlds to run, and permissions.

Congradulations, you can now host Headless sessions on your Steam Deck. As stupid as it sounds, if you don't have another PC you can dedicate to a Headless and don't want to/can't pay for a server, this is a legitimately viable option for self hosting Headless sessions.

## Native or Proton

Native is currently not recommended, as it requires manual fixing in a lot of cases. You'll likely want to use Proton. Proton 8.0, Proton Experimental, and [Proton GE 8](<https://github.com/GloriousEggroll/proton-ge-custom>) have all been tested and all 3 work.

By default Steam will download the native Linux build, in order to use the Windows version with Proton you will need to force it in Resonite's properties (`Properties < Compatibility`). From there you can choose any version of Proton you want.

To install Proton GE, either download [ProtonUp-Qt](<https://github.com/DavidoTek/ProtonUp-Qt>) through discover in desktop mode, or use the [Wine Cellar](<https://github.com/FlashyReese/decky-wine-cellar>) [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin.

## Performance & Battery Life

Unfortunately there's not much that can be done about this right now, but there are some options.
**DISCLAIMER**, *I modify my own Steam Deck with 3rd party tools and minimal hardware modifications to improve performance, my Steam Deck's performance is not indicative of a stock Steam Deck's performance.*

**Readily available options (quick access menu/in app options)**

*Framerate Limit (QAM)* - Change at your discretion, in active sessions it's rare to have more then 30 fps currently so it's safe to limit it to 30 fps, though it will still run at 60 hz (90 hz on OLED). You can do 40 fps/hz to conserve power.

*Disable Frame Limit (QAM)* - Disables Framerate Limit and falls back to 60 fps/hz, not recommended

*Allow Tearing (QAM)* - No effect, Resonite forces vsync

*Half Rate Shading (QAM)* - slightly reduces text readability (excluding the dashboard) and improves battery life, somewhat recommended

*TDP Limit (QAM)* - From testing, Resonite seems to rarely use more then 10 watts, from my understanding due to the inability to run fast enough to draw more than 10 watts. Your milage may vary, tweak as needed.

*Fixed GPU Clock (QAM)* - not tested enough, tweak as needed

*Upscaling (QAM)* - you will need to force the game resolution in Steam (`Properties < General < Game resolution`). I recommend 1024x640 as that maintains text readability fairly well. you can go down to 800x500 and still have a decent experience but don't expect to read text very well. You'll also need to back out and go back into properties to enable the `Set resolution for internal and external display` option, from my experience that's needed in order for Resonite to respect this setting. *Do keep in mind that upscaling is trading GPU cost for CPU cost, and while that's usually a net gain, Resonite is currently CPU bound so the potential gain may not be worth it.*

*Noise Supression Filter (in app option)* - disabling this will reduce CPU load slightly but **please** use something other than the internal microphone if you do disable this, not recommended

**Resonite Mods (likely to not help much, only recommended for more extreme setups)**

[CacheGetClapped](<https://github.com/dfgHiatus/CacheGetClapped>) - Smart cache management, clears old cache files and can keep cache size within specified limit. (highly recommended)

[DisableDynamicBones](<https://github.com/rassi0429/DisableDynamicBone>) - disables dynamic bone chains. (very slight fps gain, not recommended)

[DisableFXAA](<https://github.com/FalsePattern/DisableFXAA>) - disables FXAA anti aliasing. (worsens upscaling quality)

[DynBoneWrangler](<https://github.com/isovel/DynBoneWrangler>) - disables dynamic bone chains when under a user specified fps limit and re-enables them when above another user specified fps limit. (less aggressive then DisableDynamicBone, might help stability at lower framerates)

[NoSteamScreenshots](<https://github.com/Raidriar796/NoSteamScreenshots>) - prevents Steam from saving an additional copy of photos you save in game.

[ResoniteIkCulling](<https://github.com/Raidriar796/ResoniteIkCulling>) - disables IK that's out of view and/or far away. Includes IK throttling options. (in testing, thermals gain the most benefit since IK is rarely the major bottleneck of a session)

**3rd Party Tools (use at your own risk)**

[Cryo Utilities](<https://github.com/CryoByte33/steam-deck-utilities>) - RAM, VRAM, Swap, and storage optimizations. You'll likely need this to be able to reliable join moderately sized worlds without running out of RAM and crashing.

[Powertools](<https://git.ngni.us/NG-SD-Plugins/PowerTools>) - [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin that exposes more options to tweak performance, for most users I'd only recommend this for the CPU governor options (the powersave option can extend the battery life quite a bit)

## Screenshot management with Proton

When using Proton, steam will create a lot of extra folders that mimic the folder structure of Windows to allow for compatibility when games try to reference Windows specific directories. This is important because Resonite has an in game screenshot function which saves to `C:\Users\[YourUser]\Pictures\Resonite` by default. This causes Resonite to save screenshots to a really annoying location, this can be made easier though. To do so:

1. Go to `/home/deck/.steam/steam/steamapps/compatdata/2519830/pfx/drive_c/users/steamuser/pictures/`

2. Left trigger (right click) and do `Create New > Link to File or Directory...`

3. Set the name to "Resonite" and the directory to `/home/deck/Pictures/Resonite` (or anywhere else you may want to save screenshots to)

Now whenever Resonite saves a photo, it tries to save to `C:\Users\[YourUser]\Pictures\Resonite` but instead saves it to `/home/deck/Pictures/Resonite` or another directory of your choosing.

## Steam Deck & Steam Deck OLED differences

The refreshed model of the Steam Deck has a good handful of differences that make the device better overall. Despite this, you shouldn't expect better performance with the refreshed model. Here's what you can expect with the Steam Deck OLED.
*DISCLAIMER: As of writing the Steam Deck OLED is not released, these are guesses based on what we know already and this may change as we get real world tests done. This takes into account how Resonite performs on non Steam Deck devices with different hardware configurations.*

- Longer battery life - the more efficient APU as well as the larger battery will allow for longer usage
- Faster RAM - the refreshed model contains RAM speeds of 6400 MT/s, compared to the original model's 5500 MT/s, that's a pretty huge jump, but not world changing. This will likely allow for faster asset loading in Resonite.
- More stable connection - the new Wi-Fi 6E capabilities of the refreshed model will offer better connection reliability to sessions and faster asset downloading, provided you aren't limited by your internet.

That's it. There's a lot of nice changes with the refreshed model but nothing game changing for Resonite, but it shouldn't perform any worse.

## VR

**No.**

While it is possible to run VR on a Steam Deck, people have run Resonite in VR on a Steam Deck, but the experience is pretty awful in anything that's not an incredibly light session, it also puts a lot of strain on the Steam Deck. I cannot recommend trying it for any serious reason.
