# v1.2.3 — AutoTune runtime preparation fix

This update fixes a Windows folder-path issue that could stop AutoTune before any tests began.

## What changed

- **AutoTune can verify cuDNN backups in deeply nested portable folders.** Windows could report `cudnn_engines_runtime_compiled64_9.dll` as missing even though it was present. The launcher now uses file access that handles long paths without requiring a change to Windows settings.
- **Cached runtimes and older native backups remain reusable.** The same handling covers cuDNN package extraction, backup recovery, legacy-backup discovery and restore.
- **Integrity checks remain active.** The launcher still checks the expected files, sizes and SHA-256 hashes. A genuinely missing or altered DLL is still reported.

## Updating

Close the launcher and replace `Topaz-SLP-Launcher.exe` with the v1.2.3 executable. Keep the adjacent **Topaz-SLP-Launcher-Data** folder to retain your presets, settings, AutoTune history, Fusion profiles and cached runtimes. Then retry AutoTune.

The portable ZIP is also available for a new installation. This release retains the existing layout, Fusion features and tuning behavior.

[Full guide and screenshots](https://github.com/skv89/Topaz-SLP-Launcher#readme) · [Command-line guide](https://github.com/skv89/Topaz-SLP-Launcher/blob/main/CLI_USAGE.md)

