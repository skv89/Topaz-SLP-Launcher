# Topaz SLP Tuning Launcher v1.1.0

Tune Topaz Video SLP 2.6, compare performance on your computer, and watch memory use while videos process—all from one portable Windows app.

[Download](https://github.com/skv89/Topaz-SLP-Launcher/releases/latest) · [Report a problem](https://github.com/skv89/Topaz-SLP-Launcher/issues)

## What is new in v1.1.0

- **Experimental BF16 decoder Fusion** provides another speed boost for supported Blackwell GPUs. **Native** remains the default.
- **Fusion across AutoTune:** test individual settings and conservative/aggressive combinations with Fusion enabled, then compare the full aggressive combination with Fusion off using the same settings.
- **Clearer comparisons:** separate upgraded-cuDNN, Fusion-reference and controlled-Topaz gains, plus **Stock Topaz gain % (whole job)** when matching verified stock measurements are available.
- **Restore a saved run to the tables** from Run history, including completed, stopped, failed and untested rows, without starting processing or applying settings.
- **Resizable table columns:** stretchable columns, with horizontal scrolling and widths retained during refreshes and window resizing.
- **Clearer plans and compact controls:** Create / refresh plan opens Test plan; pending combinations appear immediately; Refresh versions and Prepare for offline run stay beside the cuDNN selections, with Fusion at the right.
- **Improved GPU telemetry matching** on systems with multiple NVIDIA cards, with better support diagnostics when required readings are missing.
- More descriptive hover help for attention-window grouping and DiT MLP chunks, plus an optional experimental **121-frame internal attention window**. The default remains **33 frames**.

## Getting started

1. Download **Topaz-SLP-Launcher.exe**, or extract the portable ZIP into a writable folder. Open the EXE.
2. Detect & select the **Topaz Video** location.
3. Choose **Conservative Starting Point**, or **Stock Topaz** for no tuning overrides. Running Autotune is recommended.
4. Click **Launch Topaz**, then start an SLP export normally in Topaz.
5. Test a short duplicate clip at your intended output resolution before a long job.

Supports the tested Topaz Video **1.7.1** runtime layout and compatible earlier installations. Other builds, including betas, are checked for compatibility before tuning is applied; support for an unknown build is not guaranteed. Some installations need a one-time compatibility-helper setup, which can request Windows administrator approval. Replacing or restoring installed cuDNN also requires administrator approval.

To update, finish any active export, then exit Topaz and the launcher. Back up the old EXE and the **Topaz-SLP-Launcher-Data** folder before replacing the EXE. Keep the data folder in place to retain settings, presets, reports and cuDNN backups. Open the updated launcher and use **Launch Topaz** for subsequent SLP exports.

To return to an older version, restore its matching EXE and data-folder backup. Older versions do not understand the new Fusion settings and saved AutoTune plans.

![Settings and cuDNN management](docs/screenshots/settings.png)

Screenshots show one example computer. The Settings, test-plan and Run history images show v1.1.0; other images illustrate retained features from earlier releases. Shown settings are not recommendations for every GPU.

## Try experimental BF16 Fusion

Fusion combines selected decoder operations so the GPU can process them with fewer separate steps. It retains BF16 precision and does not change the model weights. Its effect on total export speed varies with the clip, resolution, GPU and other settings.

In **Settings**, choose **BF16 fusion (experimental)** under **Decoder processing**, click **Apply Settings**, then use **Launch Topaz** for your next SLP export. Compare a short duplicate clip before a long job. Choose **Native** and apply it to return to normal decoder processing.

Fusion requires **GeForce RTX 50-series or RTX PRO Blackwell GPUs (sm120)**. **RTX 30/40-series are not supported.** Physical qualification used an RTX PRO 6000 Blackwell with Topaz Video 1.7.1 / PyTorch 2.7.0 / CUDA 12.8; other Topaz builds are not guaranteed. Fusion AutoTune checks its target GPU before setup or any test rows, and rejects unsupported or unidentified GPUs. Turn off Fusion and refresh the plan to run Native tests. Ordinary exports retain Native fallback with an explanation; later runtime or model incompatibility can still stop a required Fusion AutoTune reference. No separate compiler installation is required.

The separate **Internal attention window** controls how many frames the model considers together. **33** is the default; **121** is experimental, can use more memory and may change the result. It is independent of Fusion. Test output quality before adopting it.

## Find settings for your computer

Open **Benchmark / System AutoTune**, choose your output resolution and **Standard** mode, then click **Create / refresh plan**. The built-in adaptive suite uses your installed memory and selected output dimensions to generate its setting tests before the run. It does not require previous results or a preliminary benchmark. Saved custom suites keep your edits.

Add, edit or remove tests if desired and save your suite. Prepare the selected runtimes if prompted, then start AutoTune.

Leave Topaz open and idle, disconnect from the internet, keep the hardware running cool by leaving open windows, using AC, or running with an open case, and avoid using the computer during AutoTune as I found even light computer use such as typing documents or web browsing without videos can affect the performance significantly. Keep in mind individual-setting rows test a single parameter tweak, while custom-combination rows test all selected changes together. A result might differ by only a few percentage points; but if outside factors distorts the performance by a few percent, then the AutoTune results might not be reliable or useful. Saved tables remain available for reference; they do not resume processing.

![AutoTune test plan](docs/screenshots/benchmark-plan.png)

### Compare Fusion and stock Topaz

Check **Enable BF16 Fusion (experimental)** before creating the plan. Fusion applies to the tuning rows and derived conservative/aggressive combinations. The controlled Topaz baseline, upgraded baseline and stock Topaz references keep Fusion off. With combination validation enabled, an additional **Aggressive combination · Fusion OFF comparison** tests the same complete settings as the Fusion-on winner.

The plan shows the later combination steps immediately. Their settings and clip lengths are derived after usable individual results exist; the pending entries do not claim measurements.

| Reference | What it measures |
|---|---|
| Controlled Topaz baseline | Fixed tuning settings with the selected verified Topaz cuDNN baseline and Fusion off. |
| Upgraded baseline | The same controlled tuning settings with upgraded cuDNN and Fusion off. |
| Upgraded cuDNN + Fusion reference | The same controlled tuning settings with upgraded cuDNN and Fusion on. Individual Fusion-enabled tuning rows are compared with this reference. |
| Stock Topaz reference | Topaz's automatic native settings with verified Topaz cuDNN, used for matching whole-job comparisons when available. |

**Start / middle / end** labels identify repeated Fusion-reference checks for performance changes during a run. They use the same settings. The full aggressive ON/OFF comparison shows Fusion's contribution with the entire combination in use.

Use **Stock Topaz gain % (whole job)** for the measured overall improvement over stock Topaz. It includes the first render chunk and output finalization; preflight and model loading are outside that timing. The controlled tuning comparisons use steady chunk speed. These have different timing scopes. Missing, failed or unmatched comparisons remain unavailable rather than showing an estimated gain.

Fusion-enabled AutoTune adds reference and comparison rows, so it can take longer. Results are specific to your computer and test clip; they do not establish the fastest possible settings for every export.

### Test your own combination

Choose **Add row or combination**, select a combination and enter its settings. You can start from current, saved or previously tested settings. **Edit row or combination** changes an existing editable row. Hover over a combination row, or use its keyboard help, to see the full settings.

To compare just a few ideas, select those rows and choose **Run selected tests** from the arrow beside **Start AutoTune**. The launcher includes the required Topaz and upgraded-cuDNN baseline comparisons automatically. This works on the first run; you do not need to finish a full suite or delete other rows. The normal **Start AutoTune** action still runs the full plan.

Custom combinations use the same live memory safeguards. Their measured results are treated as complete combinations, not as separate gains to add to other settings. A user-selected combination is not automatically a validated preset recommendation.

### Runtime checks before AutoTune

After the selected runtimes are prepared, AutoTune checks that each runtime needed by the plan can load before preparing test media or starting timed rows. A comparison run checks native and upgraded cuDNN. The check does not render a video, change the installed DLLs, or add a delay when simply opening the launcher. Each runtime check has a 30-second deadline; loading time varies by computer.

If a runtime cannot start, AutoTune stops before the benchmark rows and saves the diagnostic results. Open **Run history…** and use **Export selected diagnostics…** for that run. A passed startup check confirms loading, not that every setting will fit in memory or process successfully.


With **Derive and validate conservative + aggressive combinations** enabled, AutoTune combines successfully tested settings and ranks the choices by predicted speed. Each choice must fit **both** the VRAM and system RAM buffers for its preset. Aggressive and conservative use their own limits. The isolated setting suite is not run again.

AutoTune validates up to **three aggressive combinations**, then up to **three conservative combinations**, trying the next eligible choice if needed. A successful conservative choice can also serve as the aggressive fallback. Only eligible tested results can be saved as recommendations. Hover over either Save preset button, or focus it and press **F1**, for the selection explanation and a table of the tested recommendation and up to two calculated alternatives. Calculated gains and memory totals are estimates; the alternatives are for information and are not saved by those buttons. The help identifies the capacities and buffers recorded for that run and flags differences from current hardware or edited inputs. It shows the winner's measured memory peaks separately from estimates. Older results are not recalculated when the inputs change.

The aggressive buffer fields accept decimal percentages from **0% up to the conservative buffer**. Press Enter or leave the field to commit an edit: a number above the limit becomes the limit, and a negative number becomes zero. Blank or nonnumeric entries return to the last valid value.

| Installed capacity | Recommended aggressive VRAM free | Conservative VRAM free | Recommended aggressive RAM free | Conservative RAM free |
|---|---:|---:|---:|---:|
| 16 GB and below | 7% | 15% | 12% | 20% |
| 24 GB | 7% | 15% | 12% | 20% |
| 32 GB | 7% | 15% | 12% | 25% |
| Above 32 GB | 10% | 20% | 12% | 30% |

VRAM and system RAM use their **own installed capacities** to select a row. Percentages reserve space from total memory, including Windows, Topaz and other applications. A real Topaz export can use more memory than the idle Topaz interface used during AutoTune; leave a larger buffer if needed. Lower buffers increase out-of-memory risk. Changing these fields affects new plans, not older saved results.

Candidate tests that stop reporting render progress are stopped automatically after at least **20 minutes**, with a longer allowance when successful baseline timing warrants it. Overall test deadlines remain finite. Baseline and model-loading phases have separate safeguards.

When a test reaches a memory safety limit, AutoTune stops that test and checks that its worker has closed and memory has recovered before advancing. An optional Topaz comparison may be skipped after recovery; comparisons with that missing baseline are then unavailable. The **upgraded baseline** is required to compare setting changes, so AutoTune stops if that reference cannot finish. Persistent memory pressure, missing required GPU readings, or unverified cleanup also stop the run and preserve completed results. Lowering a preset's free-memory buffer does not disable these safeguards.

A **RAM safety stop** means free physical system memory fell below the safety floor. A **commit safety stop** means Windows had too little remaining memory-commit capacity (backed by RAM and the pagefile). Commit can run low while the displayed physical RAM and VRAM still have room. Hover over a stopped result for the recorded values; closing memory-heavy applications or allowing more Windows-managed pagefile space may help.

AutoTune reuses a recent, comparable upgraded baseline after some brief memory failures, while retaining fresh comparison runs when conditions require them. On eligible high-resolution systems, the adaptive plan can add a modest **161-frame chunk** test even when its initial memory estimate excludes larger chunks. That row still has to pass the same memory safeguards.

Combination recommendations include an allowance for background memory use. If a tested combination uses more memory than predicted, that measurement can tighten the estimates for the remaining comparable choices. Aggressive and conservative still use their own VRAM and system RAM limits.

Review **Results / efficiency**, save a validated preset, or use **Export reports…** for the PDF and result files. “Aggressive” is a speed-oriented choice, not a guarantee of the fastest possible settings. Use **Thorough** to check close or surprising results.

![AutoTune results](docs/screenshots/benchmark-results.png)

Example results from an earlier release. Performance varies by computer, video and resolution.

## Monitor your videos

**Monitor / FPS** shows CPU/GPU activity, temperatures, power and memory, plus processing progress and completed files.

Live readings update automatically every **five seconds**, including VRAM temperature where supported. **Reset peaks**, **OOM / stall warnings** and **Show live graphs** sit beside the readings. “Background usage sampled” means the launcher recorded memory use while SLP was idle, so it can estimate the extra memory used by SLP.

Ordinary low-VRAM warnings use a remaining-memory threshold of **0.8 GiB on 16-GB cards** and **1 GiB on 24-GB cards**. Uncheck **OOM / stall warnings** to disable those launcher popups; the preference is saved immediately. AutoTune's automatic safeguards remain active.

**Completed chunks average** includes all finished chunks. **Steady average** excludes the first full-size warm-up chunk and a short final chunk. Neither includes pre-processing/loading.

**Completed files** lists finished exports, not queued or currently processing videos. Right-click a completed entry to open its file or folder, or restore its verified settings. If the original settings are unavailable, the entry remains visible but **Load settings** is disabled. Missing output-format details and measurements are shown as unavailable.

![Monitor and completed files](docs/screenshots/monitor.png)

Click **Show live graphs** to compare readings. The mouse wheel zooms time on all graphs together; middle-click fits the full timeline. Use the scrollbar or **Shift+wheel** to scroll through the plots. Memory peaks are marked in red, and phase labels appear when there is room to read them.

Graphs reuse the existing monitor readings. Each new SLP file replaces the previous graph history instead of accumulating graph files on disk.

![Live memory graphs](docs/screenshots/live-graphs.png)

## Share a problem or free disk space

Open **Run history…**:

- **Restore to table**: select one run to view its saved plan and results in the main GUI. Completed, failed and untested rows retain their original status. Restoring preserves the previous table and does not apply settings or resume processing. A new full AutoTune run refreshes its plan for review before starting.
- **Export selected diagnostics…**: select the AutoTune runs you need help with. The ZIP includes runtime startup outcomes, native and upgraded cuDNN inventory metadata, test results, per-row logs and the launcher's recent log. GPU identity and counter-readiness diagnostics help explain missing telemetry. New runs also retain compact resource history and separate first-chunk/later-chunk timings. All rows are considered; failed, warning-bearing and unusually slow rows receive priority within the archive limits. The manifest identifies missing, truncated or omitted files. Older runs cannot supply measurements that were never recorded.
- **App support ZIP…**: use this for a general launcher problem—for example, an error when opening Topaz. No run selection is needed.
- **Delete selected…**: remove selected saved runs after reviewing the size and confirming.
- **Clean old logs…**: remove eligible older logs while keeping results, reports and failed-run evidence.

Exporting does not upload or delete anything. Diagnostic ZIPs are not full report backups; review them for private information before sharing. Deleting a run keeps original videos, presets and reports exported outside that run's folder.

![Run history](docs/screenshots/run-history.png)

## Help and requirements

The **Attention-window group** bundles attention windows for processing: **10** means handling ten windows together, not looking across ten more frames. **DiT MLP chunk** is a count of internal work items; **16384** does not mean 16,384 MB of VRAM. A smaller chunk may lower temporary VRAM use, but its speed effect is experimental and untested. Leave it blank to keep Topaz’s value.

Use **Ctrl+Z** to undo tuning parameter edits or AutoTune row edits/deletions. Hover over controls and dropdown options for explanations. **Guide** provides starting-point guidance and a setting glossary. The separate **Error history / resume** page for ordinary Topaz exports can reopen a failed source from the beginning; you confirm its export in Topaz. It does not resume an AutoTune campaign.

![Starting guide](docs/screenshots/guide.png)

Requires **Windows x64**, a supported **Topaz Video installation with SLP 2.6**, and an **NVIDIA CUDA GPU**. No Python installation is needed. AutoTune and optional faster preflight require both FFmpeg and FFprobe; the selected Topaz installation should already provide them. You can also place **ffmpeg.exe** and **ffprobe.exe** together beside the launcher EXE (or in its **bin**, **ffmpeg**, or **ffmpeg/bin** subfolder). No system settings need to be changed. New cuDNN downloads require accepting NVIDIA's license.

**Important:** tuning is experimental. Settings that fit a 96-GB workstation may not fit a 16-GB GPU/32-GB RAM computer. Larger chunks, tiles and batches—or an uncapped VAE—can greatly increase memory use. Safety guards cannot prevent every OOM or driver failure. 

The app is unsigned, so Windows may show an unknown-publisher warning. Download only from this repository. This independent community tool is not endorsed by Topaz Labs or NVIDIA.

[License](LICENSE) · [Third-party notices](THIRD_PARTY_NOTICES.md)
