# Topaz SLP Tuning Launcher v1.2.3

1. Extract the portable ZIP to a writable folder and open **Topaz-SLP-Launcher.exe**.
2. Detect/select your Topaz Video installation and choose a starting preset.
3. **Faster threaded SLP preflight** is checked for new users; an existing saved choice is preserved.
4. Apply changes, fully close Topaz, then use **Launch Topaz** here. Start exports normally in Topaz.

**Update (EXE only):** finish active processing and close Topaz and the launcher. Back up the previous EXE and **Topaz-SLP-Launcher-Data**, then replace the EXE. Keep the data folder to retain settings, presets, profiles, runtime caches, reports and backups. Rollback requires the matching old EXE and data backup.

**AutoTune:** Standard derives both conservative and aggressive presets and stops at the first qualifying combination per preset, retrying failures up to three attempts. Extended compares up to three candidates per preset even after a success. Both test the individual matrix once, support optional optimization/compilation, and compare both final combinations with Fusion On/Off when Fusion is enabled. Keep Topaz open and idle during AutoTune and avoid other GPU work.

**AutoTune startup:** leftover default model/authentication folders from another Topaz product no longer override the selected installation. Custom model locations are preserved. If startup fails, export that run's diagnostics from **Run history**; see the [Command-line guide](CLI_USAGE.md#model-folders-and-autotune-startup-errors).

**Quick comparison:** choose **cuDNN only test**. Check **BF16 Fusion** for three rows: selected baseline with Native, upgraded runtime with Native, and upgraded runtime with Fusion. All use the same baseline SLP settings. Uncheck Fusion for two rows. This mode does not optimize kernels or derive presets.

**Fusion:** supported Blackwell/sm120 GPUs can choose BF16 Fusion under Decoder processing. Native remains the default. Enable Optimize in AutoTune to grow your local library. **Bundled kernels** tests included choices; **Compile variations** includes that same search and also compiles/tests new variations. It can keep a bundled winner. New compiled winners require output checks and a separate speed confirmation. Normal exports never compile. More relevant data can improve the chance of finding faster choices, but cannot guarantee another export-speed gain.

**Fusion preparation:** Bundled kernels allows up to **3 minutes** of active optimization; Compile variations allows up to **15 minutes**, including bundled search. Searches finish early when the encountered work is covered. Model loading and normal processing are separate. Compatible completed work is reused; unfinished candidates remain pending for a later matching preparation. Temporary comparison memory adapts to available VRAM without changing your video settings or output-check thresholds.

**CLI batches:** use `--list-presets`, `--preset "Name" --run-script "episodes.bat"`, or `--export-cmd "slp-env.cmd"`. Both **.bat** and **.cmd** batch files are supported. Prepare the runtime in Settings first. The launcher runs without its GUI and keeps each batch’s settings separate. See [Command-line guide](CLI_USAGE.md).

**Fusion help:** open **Fusion → Check and repair Fusion…** beside **Refresh profiles**, then click **Check now**. The default check is optional and does not render video. The arrow beside Check now also offers an optional short Fusion export with cancellation. After closing Topaz, **Repair detected issues** can restore damaged or missing bundled files, restore damaged compiled choices from exact retained copies, or keep corrupt choices inactive; originals are backed up and valid profiles/compiled kernels are kept. **Save report…** saves a local report without uploading it. Drivers, runtimes and Topaz model files are not repaired by this button. The v1.2.1 compatibility fix works without running diagnostics or repeating AutoTune.

**Runtime:** choose PyTorch/CUDA, matching cuDNN and an installation mode, then click **Install / update runtime**. **Launcher only** applies to Topaz sessions opened through the tuner. **Permanent (experimental)** also applies when Topaz is opened directly; the tuner need not run and installation is not repeated per video. Other models may need additional compatibility changes. **Restore Topaz PyTorch/CUDA** returns to the retained original runtime. Fully close Topaz before installing/restoring and restart existing sessions. Optional compilation requires the selected runtime's matching compiler; unavailable compilers retain bundled optimization.

Requires Windows x64, supported Topaz Video with SLP 2.6, an NVIDIA CUDA GPU and FFmpeg/FFprobe (normally provided by Topaz). Fusion requires GeForce RTX 50-series or RTX PRO Blackwell/sm120; RTX 30/40-series Fusion is unsupported. Topaz Video, models, NVIDIA drivers and cuDNN are not included. The launcher itself needs no Python installation. Installing/restoring files inside Topaz can require administrator approval; new cuDNN downloads require NVIDIA license acceptance.

Use the app's hover/F1 help, Guide, and Run history for support. **Refresh profiles** reloads existing records; AutoTune optimization creates them. Kernel timings are not whole-video FPS. Tune with short duplicate clips first; settings that fit one computer may not fit another. The unsigned app is independent community tooling, not endorsed by Topaz Labs or NVIDIA.

[Full guide](README.md) · [Release notes](RELEASE_NOTES.md) · [Third-party notices](THIRD_PARTY_NOTICES.md) · [Report a problem](https://github.com/skv89/Topaz-SLP-Launcher/issues)

