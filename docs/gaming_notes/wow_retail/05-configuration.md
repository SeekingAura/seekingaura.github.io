---
title: WoW Retail-Config
permalink: /docs/gaming_notes/wow_retail/config/
toc: true

previous:
    title: WoW Retail-UI
    url: /docs/gaming_notes/wow_retail/ui/
    
# next:
#     title: ""
#     url: ""
---


Here, I will explain all in-game configurations (except [UI](/docs/gaming_notes/wow_retail/graphics/) or [graphics](/docs/gaming_notes/wow_retail/graphics/), that are in another page of this website) with their related internal console variables **Cvars** (if makes sense or applies), not all settings are fully customizable through the UI (some of them only Cvar). I will focus on those most relevant to my gameplay style. The topics will be organized into the following categories:
* Camera  
* Combat, Alerts, movement  
* Action bars, talent management, and keybinding  
* Frames and chat

# TL;DR
Here will show the full config that, just copy based on images, have in mind some configs the only way to set is via Cvars using commands

**TODO**

## Commands Camera
Set max camera distance to max value
```
/console cameraDistanceMaxZoomFactor 2.6
```

Reduce zooming collides for small objects
```
/console cameraIndirectVisibility 0
/console cameraIndirectVisibility 1
/console cameraIndirectOffset 10
```

## Target management
**Enable Mouseover** with modifier key None (default execution without modifier) and for each the spell with position behavior (like [Death and decay](https://www.wowhead.com/spell=43265) of [Death knight](https://www.wowhead.com/class=6)) create this macro (save on specific macros of character)

```
#showtooltip
/stopspelltarget
/cast [mod:alt, @player] [mod:shift, @cursor] [] SPELL_NAME
```

while you are pressing alt and use the spell will executed over your current position, with shift key will executed on mouse position (without preview) if don't press nothing will have the normal behavior

Set **Selft cast** with **Auto and Key Press** and set modifier key **Alt**  
Set **Focus Cast Key** with **Shift** or **None** (depends if you really use the focus and want that)


# Camera
In WoW Retail, the camera has different configurations that can adapt to various gameplay styles. In this case, I will explain in detail how I use the camera and share some general configuration tips based on my experience.

In the interface section under *Options → Gameplay → Controls*, there are settings related to camera behavior. The best configuration depends on your playstyle whether you prefer using the keyboard (more buttons) or the mouse (more clicks). In this guide, I will focus on a setup that emphasizes keyboard usage.

TIP: Holding left click allow to move your camera but once your character move the camera will move according to [Camera Following Style](#camera-following-style) config

[![Camera config](/assets/img/screenshots/docs/wow_retail/configuration/camera.jpg)](/assets/img/screenshots/docs/wow_retail/configuration/camera.jpg)

## Water collision
This value allow when you enter into water the camera automatically will below the water and if go at surface or above the water the camera as well will go above the water. This config in my opinion is annoying i recommend Disabled value

Command to check
```
/run local v=GetCVar("cameraWaterCollision") print("Camera Water Collision:",v,v=="1"and"Enabled"or"Disabled")
```

Command to Set value
```
/console cameraWaterCollision 0
```

Value type Boolean value, Valid values 0 (False, Unchecked), 1 (True, Checked)
- 0: Disabled
- 1: Enabled

## Auto Follow Speed
Speed when the "auto Follow" behavior (when your character move under the conditions of Camera Following Style) are executed

Value type Float, valid range 1.0 - 10.0

## Camera Following Style
When your character moves using the keyboard (if you move using both mouse clicks, the camera will face the direction of the mouse), the camera can automatically "follow" the direction your character is facing. By default, it adjusts only when you move both horizontally and vertically. You can configure this based on your game style.

For Click-to-Move (right-click to set a destination, and the character moves in a straight line toward it), there's a separate configuration for camera-following behavior, but the available options are the same:

* **Only horizontal when moving**: This is my preferred setup. It keeps the camera in a top-down view and only adjusts when your character rotates. I find this especially helpful for dodging multiple AOE attacks.
* **Only when moving**: This is the default option. The camera adjusts only when your character is actively moving.
* **Always adjust camera**: The camera continuously follows your character's facing direction, even when standing still.
* **Never adjust camera**: The camera remains fixed and does not follow your character's movement or rotation (you must to move the camera using left click).

## Show Silhouette when obscured
This option enables a silhouette of your character to appear when they are obscured by objects in the game environment. It's especially useful in areas with scattered obstacles, helping you maintain visibility of your character. To activate this feature, go to: Options → Gameplay → Combat, and enable the setting.

[![silhouette](/assets/img/screenshots/docs/wow_retail/configuration/silhouette.jpg)](/assets/img/screenshots/docs/wow_retail/configuration/silhouette.jpg)

## Camera Max distance
The camera max distance is intended to be "static" and not user-adjustable. However, it's still possible to modify it by directly changing the CVar using the following command:

```
/console cameraDistanceMaxZoomFactor 2.6
```

The default value is **1.9**, and the maximum allowed value is **2.6**. Personally, I prefer using the max value for a wider view. To check your current setting, run this command:

```
/run print("cameraDistanceMaxZoomFactor: " .. GetCVar("cameraDistanceMaxZoomFactor"))
```

## Camera reduce zooming at collides with small objects (not walls)
Normally, when the camera collides with objects in the environment, it zooms in to avoid obscuring the player this is expected behavior. However, small objects like trees, rocks, banners, lamps, and similar items can also trigger this zoom effect, which may be unnecessary and annoying (for example forest could have multiple trees and this could be zoom in and out constantly). With the following configuration, it's possible to reduce this behavior specifically for "small" objects.

```
/console cameraIndirectVisibility 0
/console cameraIndirectVisibility 1
/console cameraIndirectOffset 10
```

On this [wowhead article](https://www.wowhead.com/news/new-user-interface-setting-to-reduce-camera-collision-in-the-war-within-342959) you can see the behavior with and without that config

# Combat, Alerts movement
Combat system contains all the elements related to know status of yourself, allies, enemies, environment and also alerts and movements

## Spell Targeting, Self Cast Behavior

Some spells require either a **target** or a **zone** to be cast, depending on the type of spell. How your target is selected depends on the **Self Cast** configuration, which can be found under:

**Options → Gameplay → Combat**

![Self Cast Config](/assets/img/screenshots/docs/wow_retail/configuration/selft_cast_config.jpg)

When Self Cast set to *Auto* for spells that can be cast on allies or yourself, the behavior will be:
* **Cast on your target**: If your current target is a valid recipient of the spell.
* **Cast on yourself**: If your target is invalid or you don’t have a target.
* **Select target manually (Cursor blue or gray)**; If your spell is for allies only if you have invalid target (enemy or ally that can't receive spell) or don't have a target your cursor will change into gray transparency or blue if you have the cursor over valid target waiting to click to valid target, if you select a target in that condition and still invalid you will see the error "Invalid target"

Here an example about target manually

No valid target
[![Manual no valid](/assets/img/screenshots/docs/wow_retail/configuration/manual_target_no_valid.png)](/assets/img/screenshots/docs/wow_retail/configuration/manual_target_no_valid.png)


Valid target
[![Manual valid](/assets/img/screenshots/docs/wow_retail/configuration/manual_target_valid.png)](/assets/img/screenshots/docs/wow_retail/configuration/manual_target_valid.png)

Not all allies are valid targets. Some NPCs, pets, or players affected by certain conditions (e.g. spells, phases, raid/group status) may dynamically become invalid.
{: .notice--info}

If your target is valid but out of range or not in line of sight, you’ll receive an error instead of the spell being cast on yourself unless the target is in another map or phase, in which case the spell will self-cast.
{: .notice--info}

For spells that can **only** be cast on enemies, the **Self Cast** setting does **not** apply. If your target is invalid or missing, you will see errors like `Invalid target` or `There is nothing to attack`.

If a spell can be cast on both enemies and allies, the system prioritizes the **ally function**. If your target is not attackable and also not a valid ally, the spell will be cast on yourself (if is able to do, otherwise will see your cursor blue in order to manually select target). If your target is a valid enemy, the spell will be cast in attack mode.

### Macro
To setup yourself how target via macro use the special var `@player`, for example

```
/cast [@player] SPELL_NAME
```

Where `SPELL_NAME` is the spell to cast on yourself, if the spell is position behavior (like [Death and decay](https://www.wowhead.com/spell=43265) of [Death knight](https://www.wowhead.com/class=6)) that will cast on player position.

More info about macros check here **TODO**

## Target from Focus
Focus is essentially an additional target that you can set using the `/focus` command or by selecting the focus option when right-clicking on a target. This focus target can be used as the source for spells you cast. In the interface under *Options → Gameplay → Combat → Focus Cast Key*, you can assign a modifier key (CTRL, ALT, or SHIFT) that allow if you are holding the assigned mod key and press the spell from the action bar using keybinding or click on it will use how target focus (even if you already have a target), also exist the option **None** that will do once the focus exist all spells without press something else will use focus how target, if focus does not exist or the spell can't be applied to target the cast will not executed. 

The common use of focus are about the "important" target to track for a particular moment, like important enemy, ally to constant monitoring (one common case focus tank in parties)

**NOTE**: This configuration applies to regular spells on your action bar. Spells used within macros ignore this setting.

[![target focus](/assets/img/screenshots/docs/wow_retail/configuration/target_focus.jpg)](/assets/img/screenshots/docs/wow_retail/configuration/target_focus.jpg)

This configuration simplifies the cast on focus using modifier without depend to create macro for every spell

### Macro
To setup focus how target via macro use the special var `@focus`, for example

```
/cast [@focus] SPELL_NAME
```

Where `SPELL_NAME` is the spell to cast on your focus, the spells that works with position does not work with this var.

You can also setup or clear your focus using mouseover target with the next macro
```
/clearfocus
/focus [@mouseover,nodead,exists]; [@target,exists] 
```

More info about macros check here **TODO**

## Target from Mouseover
The "common" and "intuitive" way to set a specific target is by clicking on the Party, Raid, or nameplate frames or click directly on the entity (NPC or player). However, this method takes a few seconds each time you change targets, which can be annoying, especially if you need to swap targets frequently (too many clicks). For example, it's common for healers to change targets every 1-2 seconds, since they need to heal allies (usually one at a time), then switch to an enemy target to deal some damage, and so on.

Fortunately, to **avoid** the need to click and to react a bit faster, targets can also be selected using Mouseover (where the mouse is hovering). This can be over Party, Raid, nameplate frames, or directly on the entity. This configuration only makes sense for spells that are used with keybindings (keyboard or mouse buttons, because mouse is required to be hovering the target), and **I recommend playing this way** because it allows you to manage a wider variety of spells more efficiently with precise target. You can change target without mouse like using tabs but when have too many targets to get one specific target could be complicated.

In the interface under *Options → Gameplay → Combat → Mouseover Cast*, you can enable and assign a modifier key (CTRL, ALT, or SHIFT), or set the value to **None** so Mouseover works as the default behavior when no modifier key is pressed.

This configuration applies to regular spells on your action bar. Spells used within macros ignores this setting.
{: .notice--info}

With mouseover active sometimes when you try to use spells with position behavior (like [Death and decay](https://www.wowhead.com/spell=43265) of [Death knight](https://www.wowhead.com/class=6)) the spell will cast immediately to your current mouse position (like macro `@cursor` behavior) specially if you press the spell multiple times or if your cursor is hovering a target, the issue is this not happens all the times (inconsistent).
{: .notice--warning}

To avoid that create this macro (save on specific macros of character) for EVERY spell with position behavior
```
#showtooltip
/stopspelltarget
/cast [mod:alt, @player] [mod:shift, @cursor] [] SPELL_NAME
```

Also with this macro you can use the modifier alt to cast spell over your character position, use shift for cursor position or nothing for the normal behavior



[![target mouseover](/assets/img/screenshots/docs/wow_retail/configuration/target_mouseover.jpg)](/assets/img/screenshots/docs/wow_retail/configuration/target_mouseover.jpg)

### Macro
To setup mouseover how target via macro use the special var `@mouseover`, for example

```
/cast [@mouseover] SPELL_NAME
```

Where `SPELL_NAME` is the spell to cast on your mouseover target (only if is npc or player objects are not a valid target), if the spell is position behavior (like [Death and decay](https://www.wowhead.com/spell=43265) of [Death knight](https://www.wowhead.com/class=6)) you need to use the special var `@cursor`.

```
/cast [@cursor] SPELL_NAME
```

Where `SPELL_NAME` is the spell to cast on your mouse position, this case is like instead to "show" a preview of spell are effect, this one will cast immediately (also save a little bit seconds avoiding additional clicks)


More info about macros check here **TODO**

## Turn speed with keyboard
The turnSpeed with keyboard can be modified only via Cvar, to modify run the next command, the default value is 200

```
/console turnspeed 200
```

To check run
```
/run print("Turnspeed: " .. GetCVar("Turnspeed"))
```

# Action bars
The explanation here is focused to move using the keys W, A, S, D, Q, E, and using the keyabord by region buttons based on hand position.

* Left hand region: Buttons like 1, 2, 3, 4, 5, 6, R, T, Y, F, G, H, B, N are intended to be used with left hand on action bars
* Right hand: mostly use the mouse but also the bind near to mouse with right hand are, Num pad buttons like "-", "+", "Supr", "num pad 3", "num pad 6", "num pad 3", "num pad 0" or just use additional buttons from mouse (if have, in my case have 12 buttons mouse to replace the mentioned keybinds)



# Optimization

## Recover disk space from old updates

Delete 

C:\Program Files (x86)\World of Warcraft\Data\config
C:\Program Files (x86)\World of Warcraft\Data\indices

These folder are updated to identify the updates and some patch do execute, the issue is that does not delete the old indice updates



# References 

https://eu.forums.blizzard.com/en/wow/t/toggle-macro-for-camera-water-collision/117963
https://warcraft.wiki.gg/wiki/Console_variables#Resetting_CVars
https://www.icy-veins.com/wow/news/clear-out-these-wow-folders-and-instantly-free-up-to-50-gb-of-space/
https://www.wowhead.com/news/new-user-interface-setting-to-reduce-camera-collision-in-the-war-within-342959
