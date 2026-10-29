# Command-line SLP presets

Prepare your Topaz installation and desired PyTorch/CUDA/cuDNN stack in the launcher's Settings first. Save your tuning as a named custom preset. Close Topaz and its workers before preparing a CLI batch. If the installation needs the one-time compatibility helper, use Launch Topaz once; the CLI does not open installation or administrator prompts.

## List presets

```bat
Topaz-SLP-Launcher.exe --list-presets
Topaz-SLP-Launcher.exe --help
```

## Run an existing batch

Both **.bat** and **.cmd** batch files are supported. The example uses **episodes.bat**; replace it with your own batch-file name.

```bat
Topaz-SLP-Launcher.exe --preset "DVD 3x" --run-script "episodes.bat"
```

Keep your existing Neuroserver media/encoding arguments in episodes.bat. Use `"%TOPAZ_SLP_NEUROSERVER%"` for the selected backend executable. The launcher supplies the preset, compatible runtime selection, model paths and Fusion hook. It waits for the script and returns its exit code. Ctrl+C cancels the owned process tree and returns 130. Return a nonzero code from your batch when an episode fails; avoid detached background jobs.

The GUI is not opened. The launcher remains as the batch's small supervisor while the script runs. Settings and Fusion profiles are copied into a batch snapshot once, not reinstalled for each episode. Changing a saved preset later does not change that batch. Finish a batch before installing, restoring or updating its Topaz runtime.

## Prepare a command session, then exit

```bat
Topaz-SLP-Launcher.exe --preset "DVD 3x" --export-cmd "slp-env.cmd"
```

This creates a new setup file and exits. In your batch, use:

```bat
@echo off
setlocal DisableDelayedExpansion
call "%~dp0slp-env.cmd"
if errorlevel 1 exit /b %errorlevel%
rem Run your existing Neuroserver commands here.
rem Use "%TOPAZ_SLP_NEUROSERVER%" as the executable.
endlocal
```

The setup applies only to that command session. Endlocal restores its earlier environment; no system-wide settings restore is needed. A program cannot change the environment of a terminal that launched it, which is why the separate call step is necessary.

Use a simple setup filename such as slp-env.cmd, especially when writing CALL commands by hand. The generated file supports Unicode and special characters in stored paths with delayed expansion disabled. Existing setup files are never overwritten: choose a new name to refresh a snapshot. Keep its referenced CLI session folder and runtime files available. Do not share the setup file publicly; it contains local paths, although it does not copy account tokens or credential files.

## Direct commands and data location

`--preset "Name" --run executable arguments...` runs an executable without reconstructing its arguments as a shell command. Everything after --run belongs to that child command.

By default the app uses Topaz-SLP-Launcher-Data beside its EXE. Use `--data-root "D:\Your folder\Topaz-SLP-Launcher-Data"` before the action to select another existing data folder. Built-in and saved custom preset names are accepted. The CLI does not change saved GUI settings.

Each prepared batch records its settings and evidence under **Topaz-SLP-Launcher-Data/cli_sessions**. Errors print a local evidence path when available. Invalid arguments, missing presets or missing setup return 2. Run-script and run return the child's code; cancellation returns 130. With export-cmd, your own script controls execution and cancellation after setup.

## Model folders and AutoTune startup errors

The launcher prepares the selected Topaz installation's model/authentication context. A leftover default `TVAI_MODEL_DIR` belonging to a different Topaz product no longer overrides it. Custom definitions, model-data and model-store locations remain supported. If your batch changes these variables after launcher setup, make sure it points to the intended installation and model locations.

The reported `KeyError: 'relogin_studio'` still awaits confirmation on the affected computer. If AutoTune fails before rendering, open **Run history** and choose **Export selected diagnostics** for the failed run. This includes the startup worker's traceback when available. Include the Topaz version and your known-working Neuroserver command when reporting the problem; remove private paths, account details and tokens first. Do not send `auth.tpz` or other credential files. No long benchmark rerun is needed to inspect an existing failed run.

