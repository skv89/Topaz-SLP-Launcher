# Topaz SLP 2.6 Tuning Launcher v1.0.1

A standalone Windows x64 launcher for reversible Topaz Video SLP 2.6 tuning, live system monitoring, repeatable benchmarking, and rollback-safe cuDNN management.

This is an intentionally binary-only distribution. `Topaz-SLP-Launcher.exe` contains its Python/Tcl runtime, SLP child-process hook, third-party notices, and isolated helper modes; no Python installation, ZIP extraction, or sidecar file is required.

## Screenshots

### Settings

![Topaz SLP Launcher Settings tab](https://github.com/skv89/Topaz-SLP-Launcher/releases/download/v1.0.1/Topaz-SLP-Launcher-Settings.png)

### Monitor / FPS

![Topaz SLP Launcher Monitor and FPS tab](https://github.com/skv89/Topaz-SLP-Launcher/releases/download/v1.0.1/Topaz-SLP-Launcher-Monitor.png)

## What v1.0.1 adds

- Installed CPU, system RAM, GPU, and VRAM identification in the header.
- Installed-VRAM starting presets, a saved Custom preset, validated numeric controls, and clearer hover guidance.
- **Apply Settings** for subsequent SLP files without altering a file already processing.
- Six selectable SLP color-correction modes.
- Always-on SLP monitoring with completed/total chunks and frames, completed-run and steady FPS, preflight/loading time, processing elapsed time, and estimated remaining time.
- Persistent completed-file history with output name, frames, preflight/loading time, average FPS, total time, finish time, sorting, playback, Explorer selection, and recall of the exact settings associated with the render.
- Automatic tracking of the active Topaz log across repeated jobs.
- cuDNN package selection, NVIDIA catalog refresh, native-runtime backup/restore, and support for custom Topaz installation paths.
- A compact GUI and the same DPI-sharp blazing icon in the executable, window, taskbar, and notification area.

## Download verification

Download [`Topaz-SLP-Launcher.exe`](https://github.com/skv89/Topaz-SLP-Launcher/releases/download/v1.0.1/Topaz-SLP-Launcher.exe).

- Size: **12,454,938 bytes**
- SHA-256: **`D691673BC19882B252FF872CC78DD45BAA555A6C25DD06BF8707360FC6E6F329`**
- Version: **1.0.1**
- Platform: **Windows x64**
- Authenticode: **not signed**

Windows SmartScreen may show an unknown-publisher warning. Download the executable only from this repository or its GitHub Release and verify the hash above.

## Use

1. Download and run `Topaz-SLP-Launcher.exe`.
2. Select a starting preset based on installed VRAM, or configure Custom settings.
3. For the tested NVIDIA speed boost, separately install **cuDNN 9.24.0.43 for CUDA 12** from the launcher's cuDNN manager after accepting NVIDIA's license. Choosing a preset does not install cuDNN.
4. Click **Launch Topaz**, then configure and start the SLP export in Topaz Video.
5. Test a short duplicate clip before unattended work.

Presets below 96 GB are capacity extrapolations from one 96 GB workstation. Monitor the live VRAM total and leave headroom rather than relying on the card name alone.

The title-bar **X** hides the launcher in the Windows notification area. Double-click its notification icon to restore it; right-click the icon and choose **Exit** to close it.

Tuning settings affect only the Topaz process started by this launcher and its child processes. Closing the launcher does not revoke settings already inherited by a running Topaz process. If Topaz is later closed and restarted normally, without the launcher, those process-local tuning settings are not applied.

**Apply Settings** changes the configuration inherited by subsequent SLP runners in the current launched Topaz session. It does not rewrite a runner that is already processing.

The monitor separates preflight/loading from processing throughput. The FPS averages exclude preflight/loading, and the steady average also excludes the first full-size warm-up chunk. Completed-file records persist until the user clears them.

Runtime settings, completed-file history, logs, the validated child hook, and cuDNN backup data are stored under `%LOCALAPPDATA%\Topaz SLP Launcher` rather than beside the executable.

## cuDNN recommendation

cuDNN **9.24.0.43 for CUDA 12** was the fastest package tested with Topaz Video v1.7.1.0's CUDA 12.8 runtime when this release was prepared. In the documented test it was approximately **32.8% faster than Topaz v1.7.0's native runtime**. A matched CUDA 12 test found cuDNN 9.25.0.15 0.44% slower, which is practical parity rather than a measured improvement. CUDA 13 packages and other catalog entries were not benchmarked by this project and are not performance recommendations.

## Important cautions

- The SLP controls target unsupported Topaz internals and may stop working after a Topaz update.
- cuDNN installation/restoration is Topaz-wide, unlike the process-local SLP controls. Close Topaz Video and `neuroserver.exe` before installing or restoring cuDNN.
- cuDNN is downloaded directly from NVIDIA only after the user accepts NVIDIA's license and requests installation; cuDNN itself is not bundled.
- The launcher has no analytics service. Monitoring reads local Topaz logs and local system/GPU counters. Network access occurs only when the user opens a link or explicitly requests a cuDNN download/catalog refresh.
- This independent community tool is not affiliated with or endorsed by Topaz Labs or NVIDIA.

## License

The launcher is distributed under the [MIT License](LICENSE). Embedded Python, Tcl/Tk, and PyInstaller components retain their own license terms, which are embedded in the executable. Topaz Video and NVIDIA cuDNN are not distributed by this repository.
