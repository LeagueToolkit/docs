# League Toolkit Libraries

> **Note:** This page is a placeholder. Detailed library documentation will be added as APIs stabilize.

The LeagueToolkit ecosystem is built on a set of Rust libraries that handle the core functionality. These libraries can be used independently for building custom tools.

## Libraries

### ltk_modpkg

Read and write `.modpkg` mod packages. Handles the binary format, metadata serialization, and content extraction.

### ltk_wad

Manipulate League of Legends WAD (Riot archive) files. Supports reading, writing, and patching WAD archives.

### ltk_overlay

Build mod overlay directories by combining multiple mod layers into a single output that can be injected into the game.

### ltk_mod_project

Parse and manage mod project configurations (`mod.config.json` / `mod.config.toml`). Used by both LTK Manager and the league-mod CLI.

## Usage

<!-- TODO: Add crate links and usage examples once published -->

## Related

- [LTK Manager](LTK-Manager) — Desktop application built on these libraries
- [League Mod CLI](League-Mod-CLI) — CLI tool built on these libraries
