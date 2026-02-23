# LTK Manager

LTK Manager is a desktop application for installing, managing, and creating League of Legends mods. Built with [Tauri](https://tauri.app/) (Rust backend + React frontend), it provides a fast, native experience on Windows.

## Features

- **Mod Library** — Install, browse, search, and manage mods with a grid or list view
- **Profiles** — Create multiple mod configurations and switch between them instantly
- **Patcher** — One-click patching to apply mods to League of Legends
- **Creator Workshop** — Build, edit, validate, and package mods
- **Import/Migration** — Import mods from `.modpkg`, `.fantome`, Git repos, or cslol-manager

## Pages

- [Getting Started](Getting-Started)
- [Managing Mods](Managing-Mods)
- [Profiles](Profiles)
- [Patching](Patching)
- [Workshop Overview](Workshop-Overview)
- [Settings](Settings)
- [Migration from cslol-manager](Migration)
- [Troubleshooting](Troubleshooting)

## Supported Mod Formats

| Format | Extension | Description |
|--------|-----------|-------------|
| modpkg | `.modpkg` | Modern format with full metadata, multi-layer support, and thumbnails |
| Fantome | `.fantome` | Legacy WAD-based format, auto-converted to modpkg on install |
