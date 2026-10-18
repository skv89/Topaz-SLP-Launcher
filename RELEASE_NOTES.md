# v1.2.1 — Fusion compatibility and optional repair

Fusion can now use compatible SLP 2.6 weights that differ from the original benchmark build. This fixes the weight-fingerprint rejection that could leave Fusion using Native even when it was enabled.

## What changed

- The cuDNN only test now supports an optional third baseline row with BF16 Fusion on the upgraded runtime. All three rows use the same baseline SLP settings; uncheck Fusion to keep the two-row comparison.
- Fixed missing output format, frame/chunk totals and remaining-time estimates in Monitor / FPS when Topaz omits its export-summary log entry. The monitor now also reads the active export command and matching worker log; FPS calculations are unchanged.
- Removed the restriction behind **“Actual SLP decoder weights differ from the qualified model.”** Fusion uses the model parameters loaded by Topaz while retaining the supported GPU, runtime and decoder requirements.
- Added **Check and repair Fusion…**, beside **Refresh profiles** on the Fusion tab. Click **Check now** to inspect Fusion files, saved profiles, GPU support, the saved runtime selection and recent activity. No video is rendered.
- Added **Repair detected issues** for missing or damaged bundled Fusion files and corrupt local profile records. Close Topaz before repairing. Originals are backed up, and valid profiles, compiled kernels and history are retained.
- Added **Save report…** for a local diagnostic report and linked Settings hover help and Fusion error messages to **Check and repair Fusion…**.
- AutoTune defaults to **PyTorch 2.9.1 / CUDA 13.0 / cuDNN 9.24.1.1**, with the upgraded runtime labeled **fastest tested**. Restoring old results at startup no longer resets the next-run runtime choices; later selections are remembered. Previous results and the Topaz baseline are preserved.
- BF16 Fusion help now has a separate troubleshooting paragraph directing you to **Check and repair Fusion…** when Fusion encounters issues or does not appear to improve speed.

**Checks and repairs are optional.** You do not need to run Check and repair Fusion or repeat AutoTune to enable the compatibility fix. This update adds no mandatory diagnostic render or qualification step at launch or during exports.

**Your tuning results carry forward.** Keep building your collection with AutoTune's Bundled kernels search or Compile variations, which includes that search and also builds and tests additional variations. More relevant measurements can increase the chance of finding a faster choice for your resolutions, settings and hardware; a bundled kernel can still be the winner.

## Download and update

Existing users: **EXE-only update**. Finish processing, close Topaz and the launcher, and back up the old EXE and **Topaz-SLP-Launcher-Data**. Replace **Topaz-SLP-Launcher.exe** and keep the data folder. Reopen the launcher and use **Launch Topaz**. Settings, presets, compatible Fusion profiles, compiled kernels, runtime caches and history are preserved.

New users can extract **Topaz-SLP-Launcher-v1.2.1-portable.zip** into a writable folder. The ZIP includes the EXE, guide, screenshots and required licenses. **SHA256SUMS.txt** covers both downloads; the launcher needs no Python installation. To roll back, restore the matching previous EXE and data backup.

Fusion still requires a supported **Blackwell/sm120 GPU**, compatible **Topaz SLP 2.6**, and a supported runtime. Check and repair Fusion can repair launcher-owned files; it cannot repair unsupported hardware, install drivers/runtimes or replace model files.

This update builds on [v1.2.0 — Build your Fusion collection](https://github.com/skv89/Topaz-SLP-Launcher/releases/tag/v1.2.0). The app remains unsigned and independently developed, with no endorsement by Topaz Labs or NVIDIA.

---

# v1.2.0 — Build your Fusion collection

**Gotta catch 'em all! Your tuning results carry forward.** AutoTune now helps build a collection of validated Fusion choices, useful measurements and optional compiled variations for your resolutions, SLP settings and hardware. More relevant Fusion data increases the opportunity to find a faster choice; a run can also confirm an existing winner and save repeated testing later.

## Fusion: a measured foundation you can build on

- The bundled foundation contains **2,009 measured internal decoder tensor configurations**, with **7 bundled Fusion variants implemented by 105 precompiled GPU kernel files**. Campaign was conducted over 12 different output resolutions. 
- **Bundled kernels** tests included choices. **Compile variations includes that same optimization**, and also builds and tests additional trusted variations. It can keep the bundled winner; a compiled winner must pass output checks and a separate speed confirmation.
- Compatible saved choices are reused automatically. Stable measurements guide later searches, and the Fusion library shows profiles, compiled kernels, timings and concise heading help. New output shapes are checked before using a newly optimized choice. More collected data does not guarantee faster exports every time.
- Bundled Fusion, local optimization and optional compilation support both offered PyTorch/CUDA runtimes. BF16 Fusion is recommended in Settings when a supported Blackwell GPU is detected; the selected decoder mode is preserved.

## Shorter Autotune Standard, deeper Autotune Extended

- Both modes automatically derive conservative and aggressive presets and run the individual setting matrix once.
- **Standard** stops at the first qualifying combination per preset, retrying failures up to three attempts. It keeps the end-of-individual-tests reference and removes extra mid-suite and between-combination baseline runs.
- **Extended** replaces Thorough for new plans. It compares up to three candidates per preset, even when the first passes, and chooses the fastest qualifying measured result.
- Both support optional Bundled kernels or Compile variations optimization, followed by full identical-settings Fusion On/Off comparisons for both final presets. Identical combinations share work.
- One baseline-gain column uses warmed FPS from chunks 2 and 3. Preparation rows are clearly marked as unscored. Historical results retain their original measurements.
- Add or edit combinations from saved presets and completed-run recommendations. Bulk row removal supports Ctrl+Z. Runtime selectors and controls use less space so the tables can show more rows.

## Runtime and everyday improvements

- Choose **Topaz Native PyTorch 2.7.0 / CUDA 12.8** or optional experimental **PyTorch 2.9.1 / CUDA 13.0**, with verified downloads, compatible cuDNN choices and **Restore Topaz PyTorch/CUDA**.
- AutoTune has separate baseline/upgraded PyTorch/CUDA and cuDNN selections. Native baseline checks keep using the original runtime even when a permanent upgrade is active.
- PyTorch 2.9.1 / CUDA 13.0 / cuDNN **9.24.1.1** carries the reported **fastest tested** label; performance varies by system.
- **Faster threaded SLP preflight for all codecs is checked by default for new users.** Existing saved on/off choices are preserved. Apply, fully close Topaz, then use Launch Topaz here.

## Compatibility and limits

Fusion requires a supported **Blackwell/sm120** GPU and compatible Topaz SLP 2.6 installation. RTX 30/40-series Fusion is unsupported. 

## Download and update

Choose **Topaz-SLP-Launcher.exe** or **Topaz-SLP-Launcher-v1.2.0-portable.zip**. **SHA256SUMS.txt** provides their checksums. The ZIP includes the executable, guide, screenshots and required licenses; no Python installation is needed for the launcher.

Finish active processing, close Topaz and the launcher, and back up the old EXE and **Topaz-SLP-Launcher-Data**. Replace the EXE and keep the data folder to retain settings, presets, Fusion profiles, runtime caches, reports and backups. Use Launch Topaz for subsequent tuned exports. To roll back, restore the matching old EXE and data backup.

This release contains the changes since v1.1.0. The app is unsigned and independently developed; it is not endorsed by Topaz Labs or NVIDIA.

## v1.2.0 runtime update

- Fixed runtime/cuDNN selections reverting to Native in the controls after reopening, and cleared completed installation progress.
- Merged runtime and cuDNN installation into **Install / update runtime**.
- Added **Launcher only** and **Permanent (experimental)** installation modes. Permanent mode also applies when Topaz is opened directly; original files are retained for Restore. Other models may need additional compatibility changes.
- Preserved existing presets, Fusion profiles, runtime caches and AutoTune history.
