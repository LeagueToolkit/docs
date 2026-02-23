# LeagueToolkit Wiki

Welcome to the LeagueToolkit documentation. LeagueToolkit is an open-source ecosystem of tools for creating and managing League of Legends mods.

## Projects

### [LTK Manager](LTK-Manager)

A desktop application for installing, managing, and creating League of Legends mods. Features include:

- One-click mod installation from `.modpkg` and `.fantome` files
- Profile system for switching between mod configurations
- Built-in patcher to apply mods to the game
- Creator Workshop for building and packaging mods

### [league-mod CLI](League-Mod-CLI)

A command-line interface for mod management. Provides the same core functionality as LTK Manager for users who prefer terminal workflows or need automation.

### [League Toolkit Libraries](League-Toolkit-Libraries)

The Rust libraries that power the ecosystem:

- **ltk_modpkg** — Read/write `.modpkg` mod packages
- **ltk_wad** — Manipulate League WAD archives
- **ltk_overlay** — Build mod overlays for patching
- **ltk_mod_project** — Parse and manage mod project configurations

## Quick Links

- [Getting Started](Getting-Started) — Install LTK Manager and apply your first mod
- [Creating Mods](Workshop-Overview) — Use the Workshop to build mods
- [Troubleshooting](Troubleshooting) — Common issues and solutions
- [Contributing](Contributing) — Help improve LeagueToolkit
