<div align="center">

# 🔥 OP_KSUN_FS 🔥
[![Build Kernel](https://img.shields.io/github/actions/workflow/status/Alhkxsj/OP_KSUN_FS/build-kernel-release.yml?label=Latest%20Release%20status&style=flat-square)](https://github.com/Alhkxsj/OP_KSUN_FS/actions/workflows/build-kernel-release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/Alhkxsj/OP_KSUN_FS?label=release&color=blue)](https://github.com/Alhkxsj/OP_KSUN_FS/releases/latest)
[![Forks](https://badgen.net/github/forks/Alhkxsj/OP_KSUN_FS?color=orange)](https://github.com/Alhkxsj/OP_KSUN_FS/network/members)
[![Stars](https://badgen.net/github/stars/Alhkxsj/OP_KSUN_FS?color=yellow)](https://github.com/Alhkxsj/OP_KSUN_FS/stargazers)

<a href="https://github.com/Alhkxsj/OP_KSUN_FS">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&weight=500&size=20&duration=3000&pause=1000&color=00FF99&center=true&vCenter=true&width=600&lines=Custom+Kernel+For+OnePlus+Ace+Racing;KernelSU-Next+%2B+SUSFS;OxygenOS+15+%2F+android12-5.10;Maintained+by+Alhkxsj" alt="Typing SVG" />
</a>

[![KernelSU-Next](https://img.shields.io/badge/KernelSU_Next-Supported-green)](https://kernelsu-next.github.io/webpage/)
[![Wild KSU](https://img.shields.io/badge/Wild_KSU-Not%20Supported-cb2431)](https://github.com/WildKernels/Wild_KSU/)
[![KernelSU](https://img.shields.io/badge/KernelSU-Not%20Supported-cb2431)](https://kernelsu.org/)
[![SUSFS](https://img.shields.io/badge/SUSFS-Integrated-orange?logo=gitlab)](https://gitlab.com/simonpunk/susfs4ksu)

> **Forked from [sakfi/OP_KSUN_FS](https://github.com/sakfi/OP_KSUN_FS) (originally [WildKernels/OnePlus_KernelSU_SUSFS](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS))**

</div>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## ⚠️ Disclaimer

### **🚨 Your warranty is no longer valid!**

Flashing this kernel will not void your warranty, but there is always a risk of bricking your device. Please make sure to:
- 💾 **Back up your data**
- 🧠 **Understand the risks before proceeding**

- I am **not responsible** for bricked devices, damaged hardware, or any issues that arise from using this kernel.
- **Please** do thorough research and fully understand the features added in this kernel before flashing it!
- By flashing this kernel, **YOU** are choosing to make these modifications. If something goes wrong, **do not blame me**!

<br>

> **⚠️ Verify compatibility of your device and OxygenOS version before flashing.**


<div align="center">

**Proceed at your own risk!**

</div>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 🚀 What This Does

This repository provides a fully automated GitHub Actions workflow that builds custom kernels for the **OnePlus Ace Racing (天玑 8100 / MT6895)**:
- 📥 Clones the OnePlus GKI kernel source via `repo sync`
- 🛡️ Integrates **KernelSU-Next (KSUN)**
- ⚔️ Applies **SUSFS** patches (Dynamically updated via GitLab API)
- 🔋 Integrates a comprehensive **Battery Optimization Suite**
- 🚀 Applies a curated set of performance & optimization patches
- 📦 Builds and packages a flashable **AnyKernel3 ZIP**
- 📱 Targets **OxygenOS 15 / android12-5.10** (kernel 5.10.209 / 5.10.226 / 5.10.236 variants)
- 🔄 **Fully Synchronized Workflow**: Automatic dependency resolution via GitHub GraphQL and GitLab APIs.

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## ✨ Features

<br>

| 🏷️ Feature | 📝 Description |
|:---|:---|
| 🔐 **KernelSU-Next** | Next-generation kernel-level root solution |
| 🛡️ **SUSFS v2.2.0+** | Advanced root hiding with Magic Mount support (Auto-synced) |
| 🔋 **Battery Optimization** | Modular suite: Wakelock hard-caps, Schedutil tuning, MGLRU, and Log Silencing |
| 🛠️ **Manual Hooks** | `scope_min_manual_hooks_v1.4` for better app compatibility |
| 🖧 **BBRv3** | Next-gen TCP congestion control |
| 🛡️ **BBG** | LSM-based Baseband Guard security |
| 🌐 **TTL Target Support** | Network packet manipulation |
| 🧱 **IP Set Support** | Advanced firewall capabilities |
| 🔄 **NTSync** | Universal NT synchronization primitives for gaming |
| 🛂 **WireGuard** | Fast, modern, and secure kernel-level VPN |
| ✅ **LTO** | Link Time Optimization (thin/full/none configurable) |
| ⚡️ **TMPFS XATTR** | Extended attributes for Mountify and Meta support |
| 🚀 **Optimization patches** | Memory, I/O, CPU scheduler, network tuning |
| </> **Unicode Bypass Fix** | Prevent path traversal using non-printable Unicode codepoints |
| 🖥️ **Droidspaces Support** | Support for Portable Linux containers |

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

<details>
<summary><b>👀 View SUSFS Hide Capabilities</b></summary>

- ✅ SUS_PATH · SUS_MOUNT · SUS_KSTAT · SUS_MAP
- ✅ SPOOF_UNAME · SPOOF_CMDLINE · OPEN_REDIRECT · AVC_SPOOF
</details>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 📱 Supported Device

| Device | SoC | OOS | Kernel |
|--------|-----|-----|--------|
| **OnePlus Ace Racing** | Dimensity 8100 (MT6895) | OOS15 | `android12-5.10` (5.10.209 / 5.10.226 / 5.10.236) |

Device config is located in [`configs/a15/OP-ACE-RACE.json`](./configs/a15/OP-ACE-RACE.json).

### 🛠️ Internal Patches
All local kernel enhancements are organized under one roof for easier maintenance:
- **`Battery patches`**: The core battery optimization suite.
- **`NTSync patches`**: Emulation synchronization backports for 6.1/6.6/6.12.
- **`WireGuard patches`**: Secure kernel-level VPN implementation.

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 🔋 Battery Optimization Suite
Our unique battery suite targets three critical areas to maximize OnePlus performance:
1. **Wakelock Hard-Caps**: Automatic 10s safety timeout for aggressive drivers (`wlan`, `IPA`).
2. **Scheduling Efficiency**: Tuned `schedutil` damping and EAS bias toward "Little" cores (80% util).
3. **Memory Optimization**: Strategic kswapd dampening and dynamic **MGLRU** enablement.
4. **Log Silencing**: Compile-level silencing of debug noise to reduce CPU/IO churn.

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 📋 Installation Instructions

<details>
<summary><b>🛠️ View Prerequisites</b></summary>

- Unlocked bootloader
- A backup of your current boot image
- Any root solution already installed (Magisk / KernelSU / APatch)
</details>

### Steps

1. 📥 Download the AnyKernel3 ZIP for your device from the [Releases](../../releases) page
2. ⚡ Flash using [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher) or [Horizon Kernel Flasher](https://github.com/libxzr/HorizonKernelFlasher)
3. 🔄 Reboot
4. 📱 Install **KernelSU-Next Manager** → [Releases](https://github.com/KernelSU-Next/KernelSU-Next/releases)
5. 🧩 Install **SUSFS Module** from within the manager → [sidex15/ksu_module_susfs](https://github.com/sidex15/ksu_module_susfs/releases)

> 📖 **For GKI installation details:** [kernelsu.org/guide/installation](https://kernelsu.org/guide/installation.html)

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 🌟 Special Thanks

Thanks to the projects this kernel builds on:

<div align="center">

| 🔧 Project/Role | 👨‍💻 Developer | 🔗 Link |
|:---:|:---:|:---:|
| **Original Repository** | fatalcoder524 | [![GitHub](https://img.shields.io/badge/GitHub-fatalcoder524-blue?style=flat-square&logo=github)](https://github.com/fatalcoder524) |
| **KernelSU-Next** | rifsxd | [![GitHub](https://img.shields.io/badge/GitHub-rifsxd-blue?style=flat-square&logo=github)](https://github.com/KernelSU-Next/KernelSU-Next) |
| **SUSFS** | simonpunk | [![GitLab](https://img.shields.io/badge/GitLab-simonpunk-orange?style=flat-square&logo=gitlab)](https://gitlab.com/simonpunk/susfs4ksu.git) |
| **SUSFS Module** | sidex15 | [![GitHub](https://img.shields.io/badge/GitHub-sidex15-blue?style=flat-square&logo=github)](https://github.com/sidex15) |
| **Droidspaces** | ravindu644 | [![GitHub](https://img.shields.io/badge/GitHub-ravindu644-blue?style=flat-square&logo=github)](https://github.com/ravindu644/Droidspaces-OSS.git) |

</div>

*If you have contributed and are not listed here, please remind me!* 🙏

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 💬 Support

If you encounter any issues or need help, feel free to:

<br>

- 🐛 Open an issue in this repository
- 💬 Reach out to me directly

<br>

<div align="center">
  <img src=".github/workflows/split.gif" alt="Divider" width="100%" height="4px" />
</div>

## 📱 Connect With Me

<br>

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-Alhkxsj-blue?logo=github)](https://github.com/Alhkxsj)

</div>
