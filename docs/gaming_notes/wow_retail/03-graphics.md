---
title: WoW Retail-Graphics
permalink: /docs/gaming_notes/wow_retail/graphics/
toc: true

previous:
    title: WoW Retail-First Steps
    url: /docs/gaming_notes/wow_retail/first/
    
next:
    title: WoW Retail-UI
    url: /docs/gaming_notes/wow_retail/ui/
---

Complex games usually have a lot of configurations in Graphics part and world of warcraft provide to users a lot of graphics configuration, here i will explain the minimal graphic configuration that you need to have a good game experience (specially in PVE like dungeons, raid). Usually high quality in graphics demands more resources from your pc, that means if you have low resources will have almost of the time low FPS and then bad game experience, the game usually will setup "automatically" a graphics profile based on your pc specs but not always are the "best" to play well, try the minimal recommendation explained on this guide, then experiment by your self "increasing" a little bit the aspects that you consider want to up.

**NOTE**: If is your first time in-game just follow the minimal config for the moment

# TL;DR
## Minimal configuration to play well
How "Resume" these images show the minimal config

### Minimal 1/5
[![Minimal 1/5](/assets/img/screenshots/docs/wow_retail/graphics/minimal-1_5.jpg)](/assets/img/screenshots/docs/wow_retail/graphics/minimal-1_5.jpg)

### Minimal 2/5
[![Minimal 2/5](/assets/img/screenshots/docs/wow_retail/graphics/minimal-2_5.jpg)](/assets/img/screenshots/docs/wow_retail/graphics/minimal-2_5.jpg)

### Minimal 3/5
[![Minimal 3/5](/assets/img/screenshots/docs/wow_retail/graphics/minimal-3_5.jpg)](/assets/img/screenshots/docs/wow_retail/graphics/minimal-3_5.jpg)

### Minimal 4/5
[![Minimal 4/5](/assets/img/screenshots/docs/wow_retail/graphics/minimal-4_5.jpg)](/assets/img/screenshots/docs/wow_retail/graphics/minimal-4_5.jpg)

### Minimal 5/5
[![Minimal 5/5](/assets/img/screenshots/docs/wow_retail/graphics/minimal-5_5.jpg)](/assets/img/screenshots/docs/wow_retail/graphics/minimal-5_5.jpg)

# Minimal configuration to play well
## Monitor
Defines which monitor want to play the game, useful when you have multiple monitors, options:
* **Primary (Default)**
* Monitor 1
* Monitor 2
* Monitor n...

## Display Mode
Specify the mode to display **Recommended value  fullscreen** mode it works well for me. However, you can try windowed mode **only** if the resolution matches your monitor's size. If the selected resolution differs from your monitor's native size (The resolution that you have configured in your Operative System for that monitor/display), fullscreen is usually the better option.

## Resolution
Determines the resolution of the game, **recommended value the same resolution that you have in your Operative System** that one could be great specially for alt+tab behavior. If you have a bad performance and you don't want to reduce other configurations you can try to use lower Resolution, have in mind this one determines the "space" on you UI lower resolution less space in your UI (will see bigger). Options vary according the current selected monitor

**NOTE**: Every time that you use a DIFFERENT resolution you need also to create a "new" configuration for UI (edit mode)

## Render Scale
The scale of the 3D Rendering on this case always be 100% because low render sometimes generates scale issue with some Addons in-game, reduce this value could improve performance BUT i don't recommend use less than 100% for scale issue mentioned before.

Percentage selected using Slider from 33%-100%, **Recommended value 100%**

## Use UI Scale
This one allow to resize the scale fo general UI, this one similar to Render Scale could generate issues with some addons, you can experiment, but for me is useless. **Recommended Value Disabled**

## Vertical Sync
This option will force FPS same to monitor Frequency (usually 60-70) use this one only if you see screen tearing something like frames/images mismatch at every refresh only on that case you should activate, usually in the most of the cases this does not happen so the **Recommended value is Disabled**

## Low Latency Mode
This one refers a feature about graphics card like Nvidia Reflex, if you have a good graphic card you should experiment different values like **NVIDIA Reflex** and **NVIDIA Reflex + Boost**, in my experience i did'nt have a good one so in that case the **Recommend Value Disable**

## Anti-Aliasing
Reduce the Sharpening edges on the rendered images (smooth out jaggy edges) that have **High impact in performance** from graphic card, if you are aware about "perfect quality image" you can enable that but is useless for game experience **Recommend Value None**

## Image-Based Techniques
Advanced configuration for Anti-Aliasing, if you have Anti-Aliasing Activated you can experiment with different options, for Anti-Aliasing value None this option will be locked, **Recommended Value None**

## Multisample Techniques
Advanced configuration for Anti-Aliasing, if you have Anti-Aliasing Activated you can experiment with different options, for Anti-Aliasing value None this option will be locked, **Recommended Value None**

## Multisample Alpha-Test
Advanced configuration for Anti-Aliasing, if you have Anti-Aliasing Activated you can experiment with different options, for Anti-Aliasing value None this option will be locked, **Recommended Value None**

## Camera FOV
This config allow how much in the horizontal view can see and in the perspective sense also affect the Camera distance (directly proportional) **Recommended Value 90** (The Max value)

## Base Game quality
This value works like general "presets" config for Graphics Quality, this does not matter their value if you set manually ALL the options, but **Recommended Value 3** is good start point

NOTE: Graphics Quality section allow to setup Raid separately but here i will explain the same config for both cases

## Shadow Quality
Shadows of objects and npcs generally are useless and shadows usually have high impact on performance so not worth their use, **Recommended Value Low**

## Liquid Detail
This one does not have huge impact on performance but in my tests i don't see something worth so **Recommended Value Low**

## Particle Density
This option is **very important** for gameplay because it allows you to clearly see spell area effects such as fire, fog, danger zones in the sense of the effect (size of the flame, fog). Being able to quickly understand what's happening around you is crucial, so it's worth setting this to the **Recommended Value Ultra**, even also their cost on performance.

**NOTE**: This config is the LAST ONE that you should to reduce (in sense to increase performance) because without this the experience in the game becomes worst and is really hard to understand what is happening  around you.

## SSAO
Increase Quality of lighting effects, similar to shadows this one in my experience is useless **Recommended Value Disabled**

## Depth Effects
Another behavior about details of environment like sunshafts, glare, ligth refraction is also useless (pure fancy) **Recommended Value Disabled**

## Compute Effects
Details of compute effects like Volume Fog, just another fancy effect **Recommended Value Disabled**

## Outline Mode
Allow to add outline the relevant things like quest objects, npcs options **Recommended Value Good** in my experience is the minimal and enough, but you can try the Value High

## Texture Resolution
This option is **very important** for gameplay because allows to see clearly the area effects such as area effects, lightings, dark poles, area effect (similar to Particle Density) **Recommended Value High**, even also their cost on performance.

## Spell Density
Allow to see or not spells from others ally players, but the minimal config allow to see only the "essential" like defensive areas, heal and that kind of areas **Recommended Value Essential**, if you have good resources you could try other values for dungeons in some cases could useful, in raid value essential is better.

## Projected Textures
This option is **very important** for gameplay because to see another details of enemy spells (similar to Particle density and Texture Resolution) **Recommended Value Enabled**

## View Distance
How far you can see in general like map and terrain stuff **Recommended Value 1**, but if you have a good CPU and good ram you can try 3-5, higher values helps for World BUT in dungeons and raid the useful sense of this is not too relevant

## Environment Detail
How far you can see GameObjects, npcs corpses **Recommended Value 1**, but if you have a good CPU and good ram you can try 3-5, higher values helps for World BUT in dungeons and raid the useful sense of this is not too relevant

## Ground Clutter
How far you can see non interactive elements of the terrain but these contains an animation like Grass and Foliage **Recommended Value 1**, but if you have a good CPU and good ram you can try 3-5, higher values helps for World BUT in dungeons and raid the useful sense of this is not too relevant

## Triple Buffering
This option could help to reduce spikes for **low frame rate** BUT that increment the input latency (sometimes you could see something that happening later like lag), **Recommended Value Disabled**

## Texture Filtering
This one Allow to handle texture Sharpness, specially for textures see in angle between the lower value with higher value is hard to see relevant diferencies so the **Recommended Value 2x Anisotropic** could be enough

## Ray Traced Shadows
Another feature about really fancy things about shadows but is useless (in gameplay sense) **Recommended Value Disabled**

## Resample Quality
This one is an additional step more to increase image quality, but if you followed the config mentioned previously the **Recommended Value Point**, if you have a Medium/Good quality you can experiment FidelityFX Super Resolution 1.0, if you have lights configuration you can experiment Bicubic

## VRS Mode
Variable Rate Shading this feature could help to increase performance but only works if your graphics card have this technology when you put cursor above this option you will see if is compatible (No red text like Requires X), **Recommended Value Disabled**

## Graphics API
Select which Graphics API use, for legacy/old gpu **Recommended Value DirectX 11** for newest usually the DirectX 12 could be better

## Physics Interactions
Usually when you or someone else interact with object or use specific spells have physical effects on environment like rocks moving, buildings destruction, etc. This config allow to see that effects generated by Players and NPC but usually is useless for gameplay, **Recommended Value None**

## Graphics Card
Specify which Graphic card use in game, is **recommended to specify the Graphic Card** instead of Auto Detect, so if you have Nvidia and want to use that one you should select that one

## Max Foreground FPS
Setup the "max" FPS value (limit) when you are in-game, FPS is hard to handle that can vary a lot according the situations so in other words does not makes sense limit, and for low spec systems could impact performance **Recommended value Disabled**

## Max Background FPS
Setup the "max" FPS value (limit) when you are not in-game, FPS is hard to handle that can vary a lot according the situations so in other words does not makes sense limit, and for low spec systems could impact performance **Recommended value Disabled**

## Target FPS
Set your *desired* FPS value, and if your actual FPS deviates too much from that target (either below or above), the graphics quality will dynamically adjust either increasing or decreasing. This feature can be more annoying than helpful, especially in situations where performance fluctuates dramatically, such as being surrounded by many players versus being alone, **Recommended Value: Disabled**

## Resample Sharpness
At step [Resample Quality](#resample-quality) if you setup **FidelityFX Super Resolution 1.0** you can specify how much is the "strength" of sample lower value means more resample for best performance **Recommended Value 2** if the value at [Resample Quality](#resample-quality) is another different to **FidelityFX Super Resolution 1.0** maybe does not matter which value you put here at **Resample Sharpness**

## Contrast
Contrast of the game there is not performance impact involved, **Recommended Value 75%** the best value depends of your monitor configuration

## Brightness
Brightness of the game there is not performance impact involved, **Recommended Value 65%** the best value depends of your monitor configuration

## Gamma
Gamma (Black and white transition) of the game there is not performance impact involved, **Recommended Value 1** the best value depends of your monitor configuration

## Optional GPU Features
Allow to use "newer" features from GPU **Recommended Value Enabled**

## Async Resource creation
Allow asynchronously create textures and shaders, disable this for really old GPU **Recommended Value Enabled**

## Multithreaded Rendering
Allow to use multiple CPU threads for Rendering, most in the cases works well if you are experimenting too many visual bug or crashes you should disable it, **Recommended Value Enabled**

## Advanced Work Submit
Allow Code Paths for GPU, disable if you are experimenting crash related to GPU issue, **Recommended Value Enabled**
