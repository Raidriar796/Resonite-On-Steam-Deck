# Resonite-On-Steam-Deck
 
This is a community maintained list of stuff you can do to improve using Resonite on the Steam Deck. This list will change over time as needed, feel free to give suggestions or corrections.

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
- *Pause* - Dashboard
- *Select* - Context Menu
- *DPad Up* - Scale Up/Zoom In/Scroll Up
- *DPad Down* - Scale Down/Zoom Out/Scroll Down
- *DPad Left* - Hold to rotate held item with Right Joystick/Right Trackpad
- *DPad Right* - Hold to pan in UI Focus Mode with Right Joystick/RightTrackpad
- *Right Trackpad* - Finer mouse controls
- *Left Trackpad* - ToolTip Radial Menu

## Native or Proton

Either should work but from my testing Proton is more stable for now. Proton 8.0, Proton Experimental, and [Proton GE](<https://github.com/GloriousEggroll/proton-ge-custom>) have all been tested and all 3 work.

By default Steam will download the native Linux build, in order to use the Windows version with Proton you will need to force it in Resonite's properties (`Properties < Compatibility`). From there you can choose any version of Proton you want.

To install Proton GE, either download [ProtonUp-Qt](<https://github.com/DavidoTek/ProtonUp-Qt>) through discover in desktop mode, or use the [Wine Cellar](<https://github.com/FlashyReese/decky-wine-cellar>) [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin.

## Performance & Battery Life

Unfortunately there's not much that can be done about this right now, but there are some options.
**DISCLAIMER**, *I modify my own Steam Deck with 3rd party tools and minimal hardware modifications to improve performance, my Steam Deck's performance is not indicative of a stock Steam Deck's performance.*

**Readily available options (quick access menu/in app options)**

*Framerate Limit (QAM)* - somewhat helpful but introduces a lot of input latency, not recommended

*Refresh Rate (QAM)* - somewhat helpful, introduces input latency but is more effective at preserving battery life, somewhat recommended

*Half Rate Shading (QAM)* - slightly reduces text readability and improves battery life, somewhat recommended

*TDP Limit (QAM)* - not tested enough, tweak as needed

*Fixed GPU Clock (QAM)* - not tested enough, tweak as needed

*Upscaling (QAM)* - you will need to force the game resolution in Steam (`Properties < General < Game resolution`). I recommend 1024x640 as that maintains text readability fairly well. you can go down to 800x500 and still have a decent experience but don't expect to read text very well. You'll also need to back out and go back into properties to enable the `Set resolution for internal and external display` option, from my experience that's needed in order for Resonite to respect this setting. *Do keep in mind that upscaling is trading GPU cost for CPU cost, and while that's usually a net gain, Resonite is currently CPU bound so the potential gain may not be worth it.*

*Noise Supression Filter (in app option)* - disabling this will reduce CPU load slightly but **please** use something other than the internal microphone if you do disable this

**Resonite Mods (likely to not help much, only recommended for more extreme setups)**

[Disable Dynamic Bones](<https://github.com/rassi0429/DisableDynamicBone>) - disables dynamic bones (very slight fps gain, not recommended)

[Disable FXAA](<https://github.com/FalsePattern/DisableFXAA>) - disables FXAA anti aliasing (worsens upscaling quality)

[IK Culling](<https://github.com/Raidriar796/ResoniteIkCulling>) - disables IK that's out of view and/or far away (in testing, thermals gain the most benefit but still very slight and likely within margain of error)

**3rd Party Tools (use at your own risk)**

[Cryo Utilities](<https://github.com/CryoByte33/steam-deck-utilities>) - RAM, VRAM, Swap, and storage optimizations. You'll likely need this to be able to reliable join moderately sized worlds without running out of RAM and crashing.

[Refresh Rate Unlocker](<https://github.com/ryanrudolfoba/SteamDeck-RefreshRateUnlocker>) - allows you to change the display refresh rate to go as low as 30 hz or as high as 70 hz. **Be aware that overclocking the display may damage the display, replacing Steam Deck screens aren't cheap. you can install this without the overclocking option.**

[Powertools](<https://git.ngni.us/NG-SD-Plugins/PowerTools>) - [decky loader](<https://github.com/SteamDeckHomebrew/decky-loader>) plugin that exposes more options to tweak performance, for most users I'd only recommend this for the CPU governor options (the powersave option can extend the battery life quite a bit)
