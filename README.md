# godot-installer

Reusable Godot 4.x addon for app installation, upgrades, and rollback.

## Components

- **UpgradeManager** - Orchestrates download, verify, backup, extract, launch, success poll
- **DownloadManager** - HTTP downloads with progress tracking
- **ChecksumVerifier** - SHA-256 file verification
- **RollbackManager** - Backup/restore with .backup files
- **FileLockManager** - Windows file lock detection and polling
- **InstallerCLI** - CLI argument parser (--install, --upgrade, --rollback)
- **InstallerConfig** - Resource for app-specific configuration
- **InstallerUI** - Dark-themed branded UI with progress and location picker
- **VersionFetcher** - Queries Supabase edge function for latest version

## Usage

Add as a git submodule at `addons/godot-installer/`:

```bash
git submodule add https://github.com/graydwarf/godot-installer.git addons/godot-installer
```

## Requirements

- Godot 4.5+
- Windows (file lock detection uses Windows file access patterns)
