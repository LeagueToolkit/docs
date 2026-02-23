# Patching

Patching is the process of applying your enabled mods to League of Legends. LTK Manager builds an overlay of all enabled mod files and injects them into the game.

## How Patching Works

The patching process has two main phases:

### 1. Building the Overlay

LTK Manager combines all enabled mods into a single overlay directory. This involves:

1. **Indexing** — Scanning enabled mods and their active layers
2. **Collecting** — Gathering mod files organized by game data path
3. **Patching WADs** — Building WAD archive overlays for each affected game data file
4. **String overrides** — Applying any text replacements from mod layers

Progress is shown in real-time in the status bar.

### 2. Applying to League

Once the overlay is built, LTK Manager uses a patcher DLL to inject the overlay into the League of Legends client. The game reads from the overlay files instead of the original data.

## Starting the Patcher

Click the **Patch** button in the status bar at the bottom of the window. The button shows the current patcher phase:

- **Idle** — Ready to patch
- **Building** — Creating the overlay (may take a moment depending on mod count/size)
- **Patching** — Overlay applied, game is patched

## Stopping the Patcher

Click **Stop** to remove the overlay and restore the game to its unmodded state. The patcher stops gracefully, cleaning up the injected files.

## TFT Patching

By default, only Summoner's Rift game files are patched. To also patch Teamfight Tactics files, enable **Patch TFT** in [Settings](Settings).

## Constraints

While the patcher is running:

- You **cannot** toggle mods on or off
- You **cannot** switch profiles
- You **cannot** reorder mods

Stop the patcher first, make your changes, then patch again.

## Troubleshooting

### Patcher won't start
- Verify your League path is correct in [Settings](Settings)
- Make sure League of Legends is installed
- Check the [log file](Troubleshooting#log-files) for errors

### Mods not showing in-game
- Confirm the mods are **enabled** in your current profile
- Make sure you started the patcher **after** enabling the mods
- Check that the mod targets the correct game files

### Patcher is slow
- The first build takes longer as it processes all mod files
- Large mods with many WAD files take more time
- Building is the slow phase; applying is near-instant
