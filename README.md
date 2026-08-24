# Topaz SLP 2.6 Tuning Launcher v1.0.0

A standalone Windows x64 launcher for reversible Topaz Video SLP 2.6 tuning, live system monitoring, completed-chunk average FPS, separate pre-processing/estimate-load timing, and rollback-safe cuDNN 9.24 management.

This is an intentionally binary-only distribution. `Topaz-SLP-Launcher.exe` contains its Python/Tcl runtime, SLP child-process hook, third-party notices, and isolated helper modes; no Python installation, ZIP extraction, or sidecar file is required.

## Download verification

`Topaz-SLP-Launcher.exe`

- Size: **11,910,293 bytes**
- SHA-256: **`88B3172DA324135BD86A403D8520086329E29F858C96F44E64CC3584A0A6A46D`**
- Version: **1.0.0**
- Platform: **Windows x64**

The executable is not Authenticode-signed. Windows SmartScreen may therefore show an unknown-publisher warning. Download it only from this repository or its GitHub Release and verify the hash above.

## Use

1. Download and double-click `Topaz-SLP-Launcher.exe`.
2. Select a starting preset based on installed VRAM. Presets above **16 GB VRAM or less** are untested capacity extrapolations from one 96 GB workstation.
3. Click **Launch Topaz**, then configure and start the SLP export in Topaz Video.
4. Test a short duplicate clip before unattended work.

The title-bar **X** hides the launcher in the Windows notification area. Double-click its notification icon to restore it; right-click the icon and choose **Exit** to close it.

The SLP monitor uses the actual `neuroserver` runner start as the video boundary. If Topaz queues another export while the current video is still processing, that queue event will not reset the current video's pre-processing time, output format, FPS, or completed-chunk totals.

Tuning settings affect only the Topaz process started by this launcher and its child processes. Closing the launcher does not revoke settings already inherited by a running Topaz process. If Topaz is later closed and restarted normally, without the launcher, those process-local tuning settings are not applied.

Runtime settings, logs, the validated child hook, and cuDNN backup data are stored under `%LOCALAPPDATA%\Topaz SLP Launcher` rather than beside the executable.

## Important cautions

- The SLP controls target unsupported Topaz internals and may stop working after a Topaz update.
- cuDNN installation/restoration is Topaz-wide, unlike the process-local SLP controls. Close Topaz Video and `neuroserver.exe` before using it.
- cuDNN is downloaded directly from NVIDIA only after the user accepts NVIDIA's license and requests installation; cuDNN itself is not bundled.
- This independent community tool is not affiliated with or endorsed by Topaz Labs or NVIDIA.

The launcher has no analytics service. Monitoring reads local Topaz logs and local system/GPU counters. Network access occurs only when the user opens a link or explicitly requests the cuDNN download.

## License

The launcher is distributed under the [MIT License](LICENSE). Embedded Python, Tcl/Tk, and PyInstaller components retain their own license terms, which are embedded in the executable. Topaz Video and NVIDIA cuDNN are not distributed by this repository.
