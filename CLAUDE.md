# godot-installer - Addon Project Context

## Project Overview
Reusable Godot 4.x addon for app installation, upgrades, and rollback. Platform: Windows. This is the **source of truth** for the installer addon.

## IMPORTANT: This is a shared submodule
- This repo is used as a git submodule by two other projects:
  - **`github.com/graydwarf/sugabase`** — Main Sugabase app
  - **`github.com/graydwarf/sugabase-installer`** — Standalone installer app
- **All addon changes happen HERE** — never edit the addon in the consuming projects
- After pushing changes here, each consuming project needs:
  ```bash
  git submodule update --remote addons/godot-installer
  git add addons/godot-installer
  git commit -m "chore: Update godot-installer submodule"
  ```

## Components
- **UpgradeManager** (`scripts/upgrade-manager.gd`) — Orchestrates full upgrade flow with phases: download, verify, unlock, backup, extract, launch, success poll, cleanup
- **DownloadManager** (`scripts/download-manager.gd`) — HTTP downloads with progress tracking and temp file management
- **ChecksumVerifier** (`scripts/checksum-verifier.gd`) — SHA-256 verification using Godot's HashingContext
- **RollbackManager** (`scripts/rollback-manager.gd`) — Creates/restores .backup files
- **FileLockManager** (`scripts/file-lock-manager.gd`) — Detects locked executables on Windows via read-write open test
- **InstallerCLI** (`scripts/installer-cli.gd`) — Parses --install, --upgrade, --rollback CLI args
- **InstallerConfig** (`scripts/installer-config.gd`) — Resource for app-specific config (name, exe, colors, timeouts)
- **InstallerUI** (`scenes/installer-ui.gd`) — Dark-themed branded UI with progress bar and location picker
- **VersionFetcher** (`scripts/version-fetcher.gd`) — Queries Supabase edge function for latest version info

## Asset Dependencies
- The InstallerUI loads `res://assets/icons/ic_fluent_folder_open_20_regular.svg` for the browse button
- Consuming projects must provide this icon at that path (FluentUI Folder Open 20px regular)
- Fallback: shows "..." text if icon not found

## Code Style
- snake-case file names with hyphens (e.g., `upgrade-manager.gd`)
- class_name on each script (e.g., `class_name UpgradeManager`)
- Comments above functions describing purpose
- No debug logging framework dependency — consumers wire their own

## Technical Context
- **Godot Version**: 4.5+
- **Platform**: Windows (file lock detection is Windows-specific)
- **No project.godot** — This is an addon, not a standalone project
