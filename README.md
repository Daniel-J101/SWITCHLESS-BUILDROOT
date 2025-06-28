# SWITCHLESS-BUILDROOT

This repository provides a curated and structured version of [Buildroot](https://buildroot.org) tailored for use with the [SWITCHLESS-OS](https://github.com/nichonaugle/CORE-OS) project. All custom operating systems under SWITCHLESS-CORE use this repository as their base for building system images.

---

## 🧱 Purpose

**SWITCHLESS-BUILDROOT** exists to:

- Provide clean, versioned snapshots of Buildroot for Switchless OS development.
- Maintain an upstream-compatible `main` branch.
- Maintain custom support branches (like `rv1106`) for boards not yet supported upstream.

---

## 📁 Repository Structure

| Branch         | Description |
|----------------|-------------|
| `main`         | Unmodified mirror of Buildroot `2025.02` release. Used as the upstream reference. |
| `rv1106`       | Based on `2025.02`, modified to add support for **RV1106-based boards** (e.g., **Luckfox Pico Max**). |

---

## 🔍 Branch Comparison

### ✅ `main` (Buildroot 2025.02)
- Exact copy of official Buildroot `2025.02` release.
- Supports platforms like:
  - `rpi-cm5`
  - Partial / untested: `orangepi-cm5`
  - ❌ No support for `rv1106` SoCs.

### 🔧 `rv1106` Branch
Derived from `main`, with the following additions:

| Area                     | Changes Made                                                                 |
|--------------------------|------------------------------------------------------------------------------|
| Board Support            | Added support for `rv1106` SoCs (e.g., Luckfox Pico Max)                     |
| U-Boot Integration       | Replaced default build with `make.sh` for SPL-based U-Boot builds            |
| DTS / Kernel             | Updated to build `.img` files using BOOT_ITS; added RV1106 DTS configs       |
| Buildroot Configuration  | Added RV1106 defconfigs and board files under `board/rv1106/`                |
| Tools                    | Integrated `mxsboot` to generate SD and NAND boot images                     |
| SDK / Toolchain Support  | Added Rockchip ARM toolchain and RV1106 IPC SDK as selectable packages       |
| OpenCV4 Enhancements     | Switched to custom repo; disabled threading, Carotene, FlatBuffers; added RK JPEG |
| Customization Hooks      | Integrated with SWITCHLESS-CORE build system and rootfs hooks   

These changes allow SWITCHLESS-CORE to build and boot reliably on RV1106 platforms.

---

## 🔁 Updating to a Future Buildroot Version

To update this repository to a future version (e.g., `2025.08`):

1. **Update the `main` branch**:
   - Replace contents with the official Buildroot release.
   - Tag the update (e.g., `2025.08-main`).

2. **Update the `rv1106` branch**:
   - Rebase or merge the new `main` changes into `rv1106`.
   - Reapply any custom patches (board support, U-Boot, configs).
   - Test builds and verify Switchless OS compatibility.

3. **Submit a pull request or push updated branches.**

Keeping both branches in sync with upstream ensures long-term maintainability while retaining RV1106-specific enhancements.

---

## 📊 Board Support Matrix

| Board           | `main`       | `rv1106`     |
|----------------|--------------|--------------|
| rpi-cm5        | ✅ Supported | ❌ Not Supported |
| rv1106 boards  | ❌ Not Supported | ✅ Supported |
| orangepi-cm5   | ⚠️ Untested  | ❌ Not Supported |

> ⚠️ `orangepi-cm5` may work on `main`, but has not been tested.

---

## 🛠 Related Projects

- [SWITCHLESS-OS](https://github.com/nichonaugle/CORE-OS) – Runtime and build system using this repo.
- [Buildroot](https://buildroot.org) – The base system used by this repository.

