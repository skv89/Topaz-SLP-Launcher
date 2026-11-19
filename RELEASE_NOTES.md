# v1.2.4 — Custom quick tests and low-RAM warnings

AutoTune is easier to start, easier to compare across runtimes, and can keep testing when Windows is low on physical RAM.

## What changed

- **Custom quick.** Enter individual settings or full combinations and run one chunk per row in table order. Save the rows as a reusable suite. Enable **Include baseline comparison** to add one Native decoder reference on each runtime.
- **One-click Start.** **Start AutoTune** refreshes the plan when needed and begins the run. **Create / refresh plan** lets you preview it. Previous results stay in **Run history**.
- **Same-version cuDNN comparisons.** Use **cuDNN only test** to compare different PyTorch/CUDA stacks with the same cuDNN version. Choose the build that matches each stack’s CUDA family.
- **A warning when Windows is low on RAM.** AutoTune can continue when physical RAM dips below the former reserve. After ten continuous seconds below **1 GiB available**, a warning explains how disk paging can slow the test. **Keep running** dismisses it, and **Stop AutoTune** cancels the run and keeps completed results. If you leave the warning open, the run continues. The final status and live log flag the low RAM. Windows commit protection and the Aggressive and Conservative preset budgets still apply.
- **Clearer results and fewer blocked starts.** Combination results show the VAE temporal micro-batch that was tested. Selected reruns keep their recorded memory buffers. AutoTune distinguishes settled runs from unresolved workers, reports the run and PID when a worker’s exit cannot be verified, and shows the cause when a safety check stops a run.

## Updating

Finish active work and close Topaz and the launcher. Back up your existing EXE and data folder. Replace only **Topaz-SLP-Launcher.exe** and keep the adjacent **Topaz-SLP-Launcher-Data** folder and any installed tools. This keeps your settings, presets, results, Fusion profiles and cached runtimes.

For a new installation, download **Topaz-SLP-Launcher-v1.2.4-portable.zip**, extract it to a writable folder, and open the EXE.

[Full guide and screenshots](https://github.com/skv89/Topaz-SLP-Launcher#readme) · [Command-line guide](https://github.com/skv89/Topaz-SLP-Launcher/blob/main/CLI_USAGE.md)
