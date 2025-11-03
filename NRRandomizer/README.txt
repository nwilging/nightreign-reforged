Create new random combinations of map placements, run set seeds, and face interesting challenges

---

A randomizer for Nightreign which modifies the files loaded on game startup, including a derandomizer for more deterministic runs. It is compatible with Seamless Co-op.

At a base level, the only difference you might notice using the randomizer is that Night Bosses are more varied for a given Nightlord. Under the hood, it's creating map patterns nearly from scratch and has a tremendous amount of freedom in its placements. In the future this can be extended to randomizing enemies and bosses within maps and in-depth placement customization.

If you would like to provide feedback or report bugs or see detailed changelogs, you can join the discord server at https://discord.gg/QArcYud (also for Elden Ring Randomizer and other mods). This mod is under development, so please check this mod page and the server for updates.

If you'd like to support my work you can use [my Ko-fi page](https://ko-fi.com/thefifthmatt).

## Randomizer overview

### Map randomizer
Refer to https://thefifthmatt.github.io/nightreign/ for a summary of how Nightreign maps work. As a summary:

- The **map pattern** determines the spawn point and the placement of enemy camps, bosses, special events, and final circles. There are a limited set of map patterns, 40 per Nightlord.
- The **expedition seed** is a 32-bit integer which determines the selected map pattern for a given Nightlord based on the Shifting Earths and active remembrances of all players in the party. It also determines first circle locations, shops, cataclysms, and scarab locations.
- Item rewards (from bosses, chests, etc) and loot piñatas from online dead players are not determined by the expedition seed.

The map randomizer can replace vanilla map patterns with randomized ones based on the **randomizer seed**. Each random pattern is generated independent of all other ones. There is still a limited set of patterns per Nightlord. To guarantee you get a different pattern every time, rerun randomizer with a different seed before reattempting a particular Nightlord. The randomizer has three option presets:

- Similar to base game: Exactly what it sounds like. This tries to emulate vanilla patterns as closely as possible, aside from Night Boss selection which can place any Night Boss for any Nightlord.
- Balanced random: Includes some additional randomization like changing the item reward types of enemy camps and slightly randomizing circle timing and size, which applies across all map patterns. There are added features for more interesting runs, like guaranteeing no repeats for enemy camps and guaranteeing an enemy camp with the Nightlord's weakness.
- Extra random: Removes some placement restrictions which are normally helpful for balancing purposes, like permitting any eligible spawn point even if there's no starter camp there or allowing Shifting Earth day 2 circle locations which don't contain the objective.

In addition to these presets, you can also select any custom combination of these options or other options like greatly increasing the frequency of double Night Bosses.

Some parts of map patterns are not yet randomized, like special events and the spawn point (unless "Guarantee starter camp" is unchecked), enemies within maps and encounters, or additional final circle locations. Night 1 and 2 bosses are currently distinct, as otherwise progression will softlock. Also, as a safety measure, encounters (camps and bosses) are only be placed in spots if there is a vanilla map pattern which places them there. The main exception is difficult Sorcerer's Rises, which may appear anywhere a Sorcerer's Rise normally appears. There are enough vanilla map patterns that this is not noticeable in practice.

### Utility
This mod includes some miscellaneous settings for added run variety and challenges. These can be used without the randomizer by unchecking the checkbox in the "Map randomizer" header.

Normally, each Shifting Earth has a 2.21% chance of appearing on each expedition without being conjured. "Greatly increase the frequency of one-off Shifting Earth expeditions" bumps this up to 12.5%, which gives each map pattern an overall equal probability. Remember to pass the Shifting Earth in the Waiting Room after if you don't want it to stick around.

Some optional challenge modes include nerfing solo gameplay to match 1.01 behavior (fewer runes, no free revives), increasing rain damage after night 2 to prevent gathering resources indefinitely, and hiding in-game map icons for camps and bosses. Some of these may be useful in competitive play and others may be interesting challenges to try on your own.

### Derandomizer
Derandomizer is an optional feature added by `NightreignRandomizerHelper.dll`, a dll which is distributed with the mod and can be used standalone. It allows setting the expedition seed directly, which determines the map pattern and other expedition behaviors which are seeded in advance.

Use the seed reroller in the mod to generate a random seed. This includes an attempted simulation of the game's pattern selection logic so that you can filter seeds to try to force specific patterns. Logic for remembrances and personal objectives is *not* simulated, so make sure remembrances are not active when using these seeds.

Item drops are not seeded, but a mode to support that could be added with significantly more changes to game params and maps.

`NightreignRandomizerHelper.dll` also overrides the save file location because me3 doesn't do that yet, so using it is strongly recommended. me3 profiles generated by randomizer always include it. It also includes a logo skip. Never use randomizer or derandomizer with your main save file, and always revert or delete your save file afterwards if you accidentally do.

## Installation

me3 (Mod Engine 3) is the only supported way to use randomizer, which generates game files and a mod profile to launch the modded game. **Pirated game version are not supported.** You must legitimately acquire Nightreign to use this mod.

### 1. Install me3

Go to https://me3.help/en/latest/ and follow instructions to install the latest release. This adds a file association for `.me3` files, called mod profiles, which let you launch the game with the given mod configuration.

### 2. Download and extract randomizer

Download the mod's zip file and extract the entire zip contents to somewhere on your local disk, such as your me3 profile directory. Make sure to:
- Explicitly click "Extract here" using a program like 7-Zip and launch `NightreignRandomizer.exe` from a real directory on your disk, not from within the zip file.
- Don't download the mod to a synced filesystem like OneDrive, as required files can appear missing from the mod's perspective.

### 3. Install other mods first, including Seamless Coop (optional)

For context, there are mainly two types of mods: dll mods and file mods. dll mods hook into the game's memory while it's running, similar to what Cheat Engine scripts do. File mods provide an altered version of the data files used by the game, such as regulation.bin (containing game params) or files packed inside game archives like data0.bdt.

The randomizer can automatically merge itself with other Nightreign file mods, **after** you install those other mods in a separate directory. Then, when you launch randomizer from *its* directory, it will launch those other mods with randomizer's changes on top. It is not necessary to merge them manually yourself. Currently this is limited to one other mod directory, which can be selected using the "Merge other mod" button in randomizer. When me3 adds a profile API, more advanced merging will be possible.

You can configure dll mods to launch with randomizer using the "Add dll mods" button in randomizer. To use Seamless Co-op, add `nrsc.dll` from your SeamlessCoop directory. Note that `NightreignRandomizerHelper.dll` is always included because it provides alt saves if none are configured by other mods.

### 4. Run the randomizer
After configuring settings and merged mods in NightreignRandomizer.exe, click the "Randomize" or "Run" button to generate mod files. You can specify an alphanumeric seed, or else a random one will be generated if "Reroll seed" is checked. Any time you change settings, seed, merged mods, or dll mods, you must close the game and click "Randomize" or "Run" again for the changes to take effect. The only exception is the Derandomizer which can be reloaded while the game is running.

If you're using Seamless Co-op with other people, your seed and **all settings** must match exactly in advance, or game-breaking desync will occur. From the Settings menu, copy the full string from "Set options from string" to sync with other people.

### 5. Launch the game with randomizer

First, if you want, you can set up your alternate save file based on your main save file. The "Copy main save file" button does exactly what it says, by default creating or updating NR0000.co2 from NR0000.sl2. Do **not** copy it back in the other direction as this may flag your save file for a later ban wave.

After running the randomizer, click the "Launch Nightreign" button. This just launches `nightreign-randomizer.me3` with Windows Explorer which requires me3 to be installed (see step 1).

When you load into the game, please check that the Expedition menu title has changed to something like "Expeditions (13654-5l8n43z)". The first five digits are the config hash, which changes when any settings changes, followed by the seed when randomizer is active. This must match other players' Expeditions title exactly. If you don't see it, the mod is not active. Check me3 logs in `C:\Users\<your username>\AppData\Local\garyttierney\me3\data\logs\nightreign-randomizer\` to debug further.

### Uninstall
Because randomizer uses its own launcher with an alternate save file, you can return to the normal game just by launching through Steam.

If you touched your main save file at all, make sure to revert it back to a version before running any mods before going back online.

## Bugs and installation issues
If you encounter bugs with randomized runs, you can report them, ideally on the [mod's discord server](https://discord.gg/QArcYud). I might eventually see them on Nexus Mods but many bug reports here don't have enough information to be usable. Send your spoiler log or full options string, *not just the seed*, and where on the map the issue was encountered.

If you see a "How do you want to open this file?" popup when launching the game through randomizer, it means me3 is not installed. Make sure to complete step 1 above.

me3 is not completely reliable, such that sometimes the game does not launch correctly with modded files. If it fails to start for this reason, try launching it again. If not all mod files are active (e.g. if the "Expeditions" menu text is not changed when using randomizer), try closing the game and launching again. Check me3 logs in `C:\Users\<your username>\AppData\Local\garyttierney\me3\data\logs\nightreign-randomizer\` to debug further.

## Acknowledgements
Thanks to TKGP for creating SoulsFormats and helping to test this mod, HotPocketRemix for initial work on emedf, Vawser and others for initial work on Nightreign paramdefs, and others who have contributed to modding tools and documented their findings on the ?ServerName? modding discord server (https://discord.gg/mT2JJjx) and elsewhere.

The mod uses Avalonia and MessageBox.Avalonia which are provided under the MIT License, and Nightreign paramdefs under the Apache license.
