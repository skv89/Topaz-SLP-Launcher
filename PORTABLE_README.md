# Topaz SLP Tuning Launcher v1.2.0

1. Extract the portable ZIP to a writable folder and open **Topaz-SLP-Launcher.exe**.
2. Detect/select your Topaz Video installation and choose a starting preset.
3. **Faster threaded SLP preflight** is checked for new users; an existing saved choice is preserved.
4. Apply changes, fully close Topaz, then use **Launch Topaz** here. Start exports normally in Topaz.

**Update:** finish active processing and close Topaz and the launcher. Back up the previous EXE and **Topaz-SLP-Launcher-Data**, then replace the EXE. Keep the data folder to retain settings, presets, profiles, runtime caches, reports and backups. Rollback requires the matching old EXE and data backup.

**AutoTune:** Standard derives both conservative and aggressive presets and stops at the first qualifying combination per preset, retrying failures up to three attempts. Extended compares up to three candidates per preset even after a success. Both test the individual matrix once, support optional optimization/compilation, and compare both final combinations with Fusion On/Off when Fusion is enabled. Keep Topaz open and idle during AutoTune and avoid other GPU work.

**Fusion:** supported Blackwell/sm120 GPUs can choose BF16 Fusion under Decoder processing. Native remains the default. Enable Optimize in AutoTune to grow your local library. **Bundled kernels** tests included choices; **Compile variations** includes that same search and also compiles/tests new variations. It can keep a bundled winner. New compiled winners require output checks and a separate speed confirmation. Normal exports never compile. More relevant data can improve the chance of finding faster choices, but cannot guarantee another export-speed gain.

**Runtime:** choose PyTorch/CUDA, matching cuDNN and an installation mode, then click **Install / update runtime**. **Launcher only** applies to Topaz sessions opened through the tuner. **Permanent (experimental)** also applies when Topaz is opened directly; the tuner need not run and installation is not repeated per video. Other models may need additional compatibility changes. **Restore Topaz PyTorch/CUDA** returns to the retained original runtime. Fully close Topaz before installing/restoring and restart existing sessions. Optional compilation requires the selected runtime's matching compiler; unavailable compilers retain bundled optimization.

Requires Windows x64, supported Topaz Video with SLP 2.6, an NVIDIA CUDA GPU and FFmpeg/FFprobe (normally provided by Topaz). Fusion requires GeForce RTX 50-series or RTX PRO Blackwell/sm120; RTX 30/40-series Fusion is unsupported. Topaz Video, models, NVIDIA drivers and cuDNN are not included. The launcher itself needs no Python installation. Installing/restoring files inside Topaz can require administrator approval; new cuDNN downloads require NVIDIA license acceptance.

Use the app's hover/F1 help, Guide, and Run history for support. **Refresh profiles** reloads existing records; AutoTune optimization creates them. Kernel timings are not whole-video FPS. Tune with short duplicate clips first; settings that fit one computer may not fit another. The unsigned app is independent community tooling, not endorsed by Topaz Labs or NVIDIA.

[Full guide](README.md) · [Release notes](RELEASE_NOTES.md) · [Third-party notices](THIRD_PARTY_NOTICES.md) · [Report a problem](https://github.com/skv89/Topaz-SLP-Launcher/issues)
