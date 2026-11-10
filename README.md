# NVIDIA v460 Kernel Driver Automated Patch & Build

Automated GitHub Actions workflow to fetch, patch, compile, and test the legacy **NVIDIA v460 driver** (`v460.106.00`) against modern Linux kernels (e.g. Linux Kernel 6.x+).

---

## 📌 Overview & Background

Legacy NVIDIA graphics drivers (such as the `460.x` series) frequently fail to compile on newer Linux distributions running modern Linux v5 and v6 kernels due to internal Linux kernel API revisions (e.g., removal of struct members like `drm_driver.date`, removal of `drm_pci_init`, or header updates).

This repository automates the compilation test cycle:
1. Downloads the legacy NVIDIA `460.106.00` driver package (`.run` executable).
2. Extracts the source code into a clean workspace.
3. Applies manual patches from the `patches/` directory if present.
4. Executes an **automated error-detection loop** to dynamically apply fixes for common kernel API breakages.
5. Generates a clean unified `.patch` file as a GitHub Actions artifact whenever successful fixes are applied.

---

## 🛠️ Usage

### Running via GitHub Actions
1. Push this repository to GitHub or trigger it manually under the **Actions** tab using `workflow_dispatch`.
2. The workflow will run on `ubuntu-latest` (or your chosen Linux runner).
3. Once completed, check the workflow summary to download the auto-generated **`nvidia-v460-auto-patch`** artifact.

### Applying Manual Patches
If you have custom `.patch` files targeting specific kernel versions, place them inside a `patches/` directory at the root of this repo:
```text
.
├── .github/
│   └── workflows/
│       └── build-nvidia-v460.yml
├── patches/
│   └── fix-kernel-6.14.patch
└── README.md
```

---

## 📖 Credits & Attribution

This automated workflow and build framework is based on the guide and patching methodology outlined by **Spike** (*Coding With Spike!*):
* **Article:** [How to Compile Old NVIDIA Drivers for Newer Linux Kernels](https://codingwithspike.wordpress.com/2026/01/26/how-to-compile-old-nvidia-drivers-for-newer-linux-kernels/)
* **Author:** Jeff Valore (*Spike*)
