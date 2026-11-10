# NVIDIA v470 Kernel Driver Automated Patch & Build

Automated GitHub Actions workflow to fetch, patch, compile, and test the legacy **NVIDIA v470 driver** (`v470.256.02`) against modern Linux kernels (such as Linux Kernel 6.x+).

---

## 📌 Overview & Background

Legacy NVIDIA graphics drivers (such as the `470.x` series) frequently fail to compile on modern Linux distributions running Linux v6 kernels due to internal Linux kernel API revisions (e.g., removal of struct members like `drm_driver.date`, removal of `drm_pci_init`, or macro updates).

This repository automates the compilation test cycle:
1. Downloads the legacy NVIDIA `470.256.02` driver package (`.run` executable) directly from NVIDIA's servers using HTTP error validation (`curl -f`).
2. Extracts the driver source code into a clean workspace.
3. Applies manual `.patch` files from the `patches/` directory if present.
4. Executes an **automated error-detection loop** during compilation to dynamically fix common kernel API breakages.
5. Generates a clean unified `.patch` file (`nvidia-v470-kernel.patch`) and uploads it as a GitHub Actions artifact upon completion.

## References
* Last official supported nVidia drivers for GT755M (on my iMac 27" 14.2): https://www.nvidia.com/en-us/drivers/details/226760/
* I used Gemini to build a workflow from these steps: [How to Compile Old NVIDIA Drivers for Newer Linux Kernels](https://codingwithspike.wordpress.com/2026/01/26/how-to-compile-old-nvidia-drivers-for-newer-linux-kernels/)
---

## 🛠️ Usage

### Running via GitHub Actions
1. Push this repository to GitHub or trigger it manually under the **Actions** tab using `workflow_dispatch`.
2. The workflow will run on `ubuntu-latest` (or your target kernel build environment).
3. Once completed, check the workflow run summary to download the auto-generated **`nvidia-v470-auto-patch`** artifact.

### Repository Layout
```text
.
├── .github/
│   └── workflows/
│       └── build-nvidia-v470.yml
├── patches/
│   └── custom-kernel-fix.patch
├── .gitignore
└── README.md
