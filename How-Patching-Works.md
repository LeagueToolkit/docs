# How Patching Works

This page explains what actually happens behind the scenes when LTK Manager patches your game. You don't need to understand any of this to use the tool - but if you're curious about what's going on under the hood, read on.

## The Core Idea: Overlays

League of Legends stores all of its game data - champion models, textures, sounds, UI elements, text - inside compressed archive files called **WAD files**. These live in your League installation folder under `Game/DATA/FINAL/`.

When you install a mod, LTK Manager doesn't touch any of these original files. Instead, it creates **copies** of the affected game files with your mod's changes applied, and places them in a separate folder called an **overlay**. When the game runs, LTK Manager redirects the game to read from the overlay instead of its original files.

## What's in the Overlay

The overlay is a directory that mirrors the structure of League's game data folder, but only contains the files that your mods actually change. If you have a mod that replaces a champion's skin, the overlay will contain a patched version of that champion's WAD file - and nothing else.

For example, if you have a mod that changes Ahri's textures, the overlay might look like this:

```
overlay/
└── DATA/
    └── FINAL/
        └── Champions/
            └── Ahri.wad.client    ← patched copy with your mod's textures
```

The rest of the game's hundreds of WAD files remain untouched and are read from the original location.

### How Mods are Combined

When you have multiple mods enabled, their changes are **merged** into the overlay. LTK Manager processes each mod in the order they appear in your mod list (top to bottom). If two mods change the same file, the mod higher in the list takes priority.

This is why [mod ordering](Managing-Mods) matters - it determines which mod "wins" when there's a conflict.

## Profiles and Overlays

Each [profile](Profiles) maintains its own separate overlay directory. This is an important detail: when you switch profiles, you're not just swapping a list of enabled mods - you're switching to an entirely different set of built overlay files.

This means:

- **Profile A** with Champion Skin X and HUD Mod Y has its own overlay with those specific changes baked in
- **Profile B** with a completely different set of mods has its own, independent overlay
- Switching between profiles doesn't corrupt or mix up your mod setups

When you change anything in a profile - enable a mod, disable a mod, reorder mods - the overlay for that profile is marked as outdated. The next time you start the patcher, it rebuilds the overlay from scratch to reflect your changes.

## The Two Phases of Patching

When you click the **Patch** button, two things happen in sequence:

### Phase 1: Building the Overlay

This is the preparation phase. LTK Manager:

1. **Indexes** your League installation to find all the game's WAD files
2. **Collects** the changes from each of your enabled mods (reading from `.modpkg` or `.fantome` mod archives)
3. **Patches** the affected WAD files - creates modified copies in the overlay directory with your mod's content merged in
4. **Applies string overrides** - if any mods change in-game text (champion names, item descriptions, etc.), those text changes are applied to the relevant data files

This phase is where most of the time is spent. The duration depends on how many mods you have enabled and how large they are. You'll see a progress indicator in the status bar showing which stage the build is in and how far along it is.

### Phase 2: Running the Patcher

Once the overlay is built, LTK Manager loads a patcher module that watches for the League of Legends game process. When the game starts:

1. The patcher detects the running game process
2. It **hooks into the game's file reading** mechanism
3. Whenever the game tries to read a file that exists in your overlay, the read is silently **redirected** to the overlay copy instead

The game has no idea this is happening. From its perspective, it's reading its own files as usual - it just happens to be getting the modded versions.

The patcher stays active and continues watching. If you play multiple games in a row, it will re-apply the hooks each time a new game process starts. You only need to stop and restart the patcher if you want to change which mods are enabled.

## What Happens When You Stop

When you click **Stop**, the patcher:

1. Stops watching for game processes
2. Removes any active file redirections
3. Returns to an idle state

The overlay files remain on disk (so subsequent patches can be faster if nothing changed), but the game will no longer be redirected to them. Your next game will run completely unmodified.

Your original game files are **never modified** throughout this entire process. Patching is always safe to start and stop.

## Where Overlays are Stored

Overlays are stored inside your LTK Manager storage directory, organized by profile:

```
LTK Manager Storage/
└── profiles/
    ├── default/
    │   └── overlay/          ← overlay for your "Default" profile
    ├── ranked-setup/
    │   └── overlay/          ← overlay for a "Ranked Setup" profile
    └── fun-skins/
        └── overlay/          ← overlay for a "Fun Skins" profile
```

You can configure the storage directory location in [Settings](Settings). Each profile's overlay is independent, so you can have very different mod setups without them interfering with each other.

## TFT and Selective Patching

By default, LTK Manager only patches Summoner's Rift game files. Teamfight Tactics uses its own separate WAD file (`map22.wad.client`), which is excluded from patching unless you enable **Patch TFT** in [Settings](Settings).

This keeps the overlay smaller and the build faster when you're only modding the main game mode.

## Why This Approach?

The overlay approach has several advantages over directly modifying game files:

- **Safety** - Original files are never changed, so there's no risk of corrupting your installation
- **Reversibility** - Stop the patcher and your game is instantly back to normal
- **Profile isolation** - Different mod setups stay completely separate
- **Game updates** - When League updates, your original files are updated normally by the game client. Your overlays may need to be rebuilt, but there's nothing to "undo" first
- **Multiple sessions** - The patcher can stay running across multiple games without any extra steps

---

**See also:** [Patching](Patching) for step-by-step usage instructions, [Profiles](Profiles) for managing multiple mod setups, [Managing Mods](Managing-Mods) for enabling and ordering mods.
