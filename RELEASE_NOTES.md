# v1.2.2 — Better Fusion searches, AutoTune fixes and CLI presets

Give Fusion optimization more useful search time, reuse completed work, and run your saved SLP presets in command-line batches. This release also improves AutoTune startup and the existing Check and repair Fusion dialog.

## What changed

- **More time for useful Fusion optimization.** **Bundled kernels** allows up to **3 minutes** of active optimization per preparation. **Compile variations** allows up to **15 minutes**, including that same bundled search plus compiling and testing additional variations. Ordinary model loading and video processing no longer use up the search allowance.
- **Completed work carries forward.** Later matching preparations reuse compatible completed checks and verified compiled kernels. If time, memory or a compiler problem leaves candidates unfinished, they remain pending for a later matching run. A newly added candidate is treated as new work.
- **Comparison memory adapts to your available VRAM.** The optimizer compares candidate outputs in larger groups when memory is available and smaller groups when space is tight. Your output resolution, chunk size, tiles and output-check thresholds stay the same.
- **Support for growing Fusion collections.** Large libraries no longer omit profiles beyond the old 4,096-record limit. The existing Fusion list loads rows as needed, while exports continue to select compatible saved choices automatically.
- **Run saved presets from the command line.** List presets, run an existing batch script with a selected preset, or create a command-session setup file and exit. Each batch keeps its own settings and Fusion-profile snapshot, so later GUI edits do not change the next episode.
- **More reliable AutoTune startup.** A leftover default model/authentication folder from a different Topaz product no longer overrides the installation selected in the launcher. Custom model locations remain supported.
- **Clearer Fusion activity reports.** Check and repair Fusion now searches ordinary exports, AutoTune trials and CLI runs. A newer idle launch no longer hides completed work, and an older success does not hide a newer failure. Decoder Fusion and attention-window findings are reported separately.
- **Optional short Fusion test.** Use the arrow beside **Check now** to choose **Run short Fusion test**. It performs a small 17-frame export, checks actual Fusion kernel use and the completed output, and supports cancellation. The regular **Check now** action checks files and recorded activity without rendering video.
- **Repair more Fusion file problems.** **Repair detected issues** can restore a damaged compiled choice from an exact verified retained copy. If no suitable copy exists, that damaged choice is kept inactive so bundled Fusion remains available. Originals are backed up; valid profiles and user-disabled choices are retained.
- **Better support reports and folder-path handling.** Diagnostic exports include the failed startup worker's traceback when available, with private values redacted. Bundled Fusion kernels also load from deep Windows folder paths.

### Command-line examples

```bat
Topaz-SLP-Launcher.exe --list-presets
Topaz-SLP-Launcher.exe --preset "DVD 3x" --run-script "episodes.bat"
Topaz-SLP-Launcher.exe --preset "DVD 3x" --export-cmd "slp-env.cmd"
```

Use your saved preset name in place of **DVD 3x**. Replace **episodes.bat** with your own batch-file name; both **.bat** and **.cmd** are supported. The `--run-script` command runs your batch without opening the launcher window, waits for it to finish and returns its exit code. The export command creates a setup file and exits; use `call slp-env.cmd` inside your batch before its Neuroserver commands. See the [Command-line guide](https://github.com/skv89/Topaz-SLP-Launcher/blob/main/CLI_USAGE.md) for setup, examples and cancellation.

**AutoTune startup troubleshooting:** The model-folder mismatch is corrected. If startup fails, open **Run history** and use **Export selected diagnostics** for that run.

**Your Fusion tuning results carry forward.** Running AutoTune with Fusion optimization across a wider variety of output resolutions and SLP settings helps build a broader library of tested Fusion choices for your hardware. As that coverage grows, the app is more likely to have a faster compatible kernel ready to use automatically for future exports - including other not-yet tested but similar resolutions and settings that share matching internal workloads.
Compile variations includes the same bundled-kernel optimization and additionally builds and tests new variations. More relevant profiles increase the opportunity for better performance across a broader range of exports.

## Download and update

Existing users: finish processing, close Topaz and the launcher, and back up the previous EXE and **Topaz-SLP-Launcher-Data**. Replace **Topaz-SLP-Launcher.exe** and keep the data folder. Settings, presets, compatible Fusion profiles, compiled kernels, runtime caches and history carry forward. Reopen the launcher and use **Launch Topaz**.

New users can extract **Topaz-SLP-Launcher-v1.2.2-portable.zip** into a writable folder. It includes the app, full guide, command-line guide, screenshots and required licenses. **SHA256SUMS.txt** covers both downloads. No Python installation is needed.

Fusion requires a supported **Blackwell/sm120 GPU**, compatible **Topaz SLP 2.6**, and a supported runtime. Less optimization workspace can help on smaller cards, but does not guarantee a speed gain or establish performance on every GPU. The optional short test does not qualify all resolutions or verify full-video quality. Repairs do not install drivers/runtimes or alter Topaz models.

This update builds on [v1.2.1](https://github.com/skv89/Topaz-SLP-Launcher/releases/tag/v1.2.1). The app remains unsigned and independently developed, with no endorsement by Topaz Labs or NVIDIA.
