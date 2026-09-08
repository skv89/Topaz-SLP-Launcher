# Topaz SLP Tuning Launcher v1.0.3.1

Tune Topaz Video SLP 2.6, compare performance on your computer, and watch memory use while videos process—all from one portable Windows app.

[Download](https://github.com/skv89/Topaz-SLP-Launcher/releases/latest) · [Report a problem](https://github.com/skv89/Topaz-SLP-Launcher/issues)

## What is new

- Finds FFmpeg and FFprobe placed beside the launcher EXE, even if you rename the launcher.
- Fixes detection of valid media tools stored on another drive.
- Gives clearer instructions if either tool is missing.

## Getting started

1. Save **Topaz-SLP-Launcher.exe** in a writable folder and open it.
2. Check the **Topaz Video** location.
3. Choose **Conservative Starting Point**, or **Stock Topaz** for no tuning overrides.
4. Click **Launch Topaz**, then start an SLP export normally in Topaz.
5. Test a short duplicate clip at your intended output resolution before a long job.

The launcher now supports the new Topaz Video v1.7.1.2 Beta and likely all past versions and likely future versions. It handles its compatibility helper automatically if needed; Windows may ask for administrator approval. 

To update, choose **Exit** in the launcher or its tray menu, back up the old EXE, then replace it. Keep **Topaz-SLP-Launcher-Data** to retain settings, presets, reports and cuDNN backups.

![Settings and cuDNN management](docs/screenshots/settings.png)

Screenshots show one example computer, not recommended settings for every GPU.

## Find settings for your computer

Open **Benchmark / System AutoTune**, choose your output resolution and **Standard** mode, then click **Create / refresh plan**. Add, edit or remove setting tests if desired and save your suite. Prepare the selected runtimes if prompted, then start AutoTune.

Leave Topaz open and idle, disconnect from the internet, keep the hardware running cool by leaving open windows, using AC, or running with an open case, and avoid using the computer during AutoTune as I found even light computer use such as typing documents or web browsing without videos can affect the performance significantly. Keep in mind each AutoTune row tests a single isolated parameter tweak that might result in a few percentage point of performance difference; but if outside factors distorts the performance by a few percent, then the AutoTune results might not be reliable or useful. Saved tables remain available for reference; they do not resume processing.

![AutoTune test plan](docs/screenshots/benchmark-plan.png)

Review **Results / efficiency**, save a validated preset, or use **Export reports…** for the PDF and result files. “Aggressive” is a speed-oriented choice, not a guarantee of the fastest possible settings. Use **Thorough** to check close or surprising results.

![AutoTune results](docs/screenshots/benchmark-results.png)

## Monitor your videos

**Monitor / FPS** shows CPU/GPU activity, temperatures, power and memory, plus processing progress and completed files.

**Completed chunks average** includes all finished chunks. **Steady average** excludes the first full-size warm-up chunk and a short final chunk. Neither includes pre-processing/loading.

![Monitor and completed files](docs/screenshots/monitor.png)

Click **Show live graphs** to compare readings. The mouse wheel zooms time on all graphs together; middle-click fits the full timeline. Use the scrollbar or **Shift+wheel** to scroll through the plots. Memory peaks are marked in red, and phase labels appear when there is room to read them.

Graphs reuse the existing monitor readings. Each new SLP file replaces the previous graph history instead of accumulating graph files on disk.

![Live memory graphs](docs/screenshots/live-graphs.png)

## Share a problem or free disk space

Open **Run history…**:

- **Export selected diagnostics…**: select the AutoTune runs you need help with. The ZIP includes troubleshooting details for those runs and the launcher's recent log.
- **App support ZIP…**: use this for a general launcher problem—for example, an error when opening Topaz. No run selection is needed.
- **Delete selected…**: remove selected saved runs after reviewing the size and confirming.
- **Clean old logs…**: remove eligible older logs while keeping results, reports and failed-run evidence.

Exporting does not upload or delete anything. Diagnostic ZIPs are not full report backups; review them for private information before sharing. Deleting a run keeps original videos, presets and reports exported outside that run's folder.

![Run history](docs/screenshots/run-history.png)

## Help and requirements

Hover over controls and dropdown options for explanations. **Guide** provides starting-point guidance and a setting glossary. The separate **Error history / resume** page for ordinary Topaz exports can reopen a failed source from the beginning; you confirm its export in Topaz. It does not resume an AutoTune campaign.

![Starting guide](docs/screenshots/guide.png)

Requires **Windows x64**, a supported **Topaz Video installation with SLP 2.6**, and an **NVIDIA CUDA GPU**. No Python installation is needed. AutoTune and optional faster preflight require both FFmpeg and FFprobe; the selected Topaz installation should already provide them. You can also place **ffmpeg.exe** and **ffprobe.exe** together beside the launcher EXE (or in its **bin**, **ffmpeg**, or **ffmpeg/bin** subfolder). No system settings need to be changed. New cuDNN downloads require accepting NVIDIA's license.

**Important:** tuning is experimental. Settings that fit a 96-GB workstation may not fit a 16-GB GPU/32-GB RAM computer. Larger chunks, tiles and batches—or an uncapped VAE—can greatly increase memory use. Safety guards cannot prevent every OOM or driver failure. 

The app is unsigned, so Windows may show an unknown-publisher warning. Download only from this repository. This independent community tool is not endorsed by Topaz Labs or NVIDIA.

[License](LICENSE)
