# Third-party notices

The standalone Topaz SLP Tuning Launcher bundles the Python 3.11 runtime, Tcl/Tk, the PyInstaller bootloader/runtime, ReportLab for printable benchmark reports, and Pillow for image handling. Their license texts are embedded in the one-file executable and copied into the portable data folder when the launcher starts.

PyInstaller is distributed under the GNU General Public License with its bootloader exception. Python is distributed under the Python Software Foundation License. Tcl, Tk, and ReportLab use BSD-style licenses.

Pillow uses the MIT-CMU license. Its complete distribution notice, including the bundled image-library notices, is provided in `licenses/Pillow-LICENSE.txt`. This software includes FreeType, used under the FreeType License; portions are copyright The FreeType Project (https://freetype.org). All rights reserved.

The optional experimental VRAM-temperature monitor calls NVAPI interfaces supplied by the installed NVIDIA Windows driver. No NVIDIA driver, SDK, or NVAPI binary is bundled. Its generation-aware sensor-selection technique follows the approach used by SeedVR2 Portable Studio and informed by the open-source LibreHardwareMonitor project; no LibreHardwareMonitor binary is bundled.

NVIDIA cuDNN is not bundled. The optional in-application updater downloads it directly from NVIDIA only after explicit license acceptance and verifies the package size and SHA-256 against NVIDIA's official distribution metadata fetched over HTTPS. NVIDIA's license is available at:

https://developer.download.nvidia.com/compute/cudnn/redist/cudnn/LICENSE.txt

Topaz Video and SLP are products of Topaz Labs. They are not bundled with this launcher. This launcher is independent community tooling and is not endorsed by Topaz Labs or NVIDIA.

The experimental BF16 decoder option includes GPU kernels compiled with Triton 3.3.1 (Triton for Windows 3.3.1.post19). Triton's MIT license is embedded as `licenses/Triton-MIT-LICENSE.txt`. The Triton compiler, CUDA toolkit and model weights are not bundled. The option uses the NVIDIA driver and the supported PyTorch/CUDA runtime supplied by the user's Topaz installation.
