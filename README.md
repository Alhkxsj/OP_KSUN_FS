<div align="center">

# 🔥 OP_KSUN_FS 🔥

[![Build Kernel](https://img.shields.io/github/actions/workflow/status/Alhkxsj/OP_KSUN_FS/build-kernel-release.yml?label=Latest%20Release%20status&style=flat-square)](https://github.com/Alhkxsj/OP_KSUN_FS/actions/workflows/build-kernel-release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/Alhkxsj/OP_KSUN_FS?label=release&color=blue)](https://github.com/Alhkxsj/OP_KSUN_FS/releases/latest)
[![Forks](https://badgen.net/github/forks/Alhkxsj/OP_KSUN_FS?color=orange)](https://github.com/Alhkxsj/OP_KSUN_FS/network/members)
[![Stars](https://badgen.net/github/stars/Alhkxsj/OP_KSUN_FS?color=yellow)](https://github.com/Alhkxsj/OP_KSUN_FS/stargazers)

Custom kernel for **OnePlus Ace Racing** · KernelSU-Next · OxygenOS 15 / android12-5.10

[![KernelSU-Next](https://img.shields.io/badge/KernelSU_Next-Supported-green)](https://kernelsu-next.github.io/webpage/)

Forked from [sakfi/OP_KSUN_FS](https://github.com/sakfi/OP_KSUN_FS)

</div>

## ⚠️ Disclaimer

Flashing this kernel is at **your own risk**. Back up your data first. The author is **not responsible** for bricked devices or any issues that arise from using this kernel.

> Verify your device and OxygenOS version before flashing.

## 🚀 What This Does

Automated GitHub Actions workflow that builds custom kernels for the **OnePlus Ace Racing (Dimensity 8100 / MT6895)**:
- Clones the official OnePlus GKI kernel source
- Integrates **KernelSU-Next (KSUN)**
- Applies battery optimization, performance, and networking patches
- Builds and packages a flashable **AnyKernel3 ZIP**
- Targets **OxygenOS 15 / android12-5.10** — three kernel variants for OOS versions:
  - `5.10.209` → OOS 15.0.0.700 ~ 15.0.0.1300
  - `5.10.226` → OOS 15.0.0.1301 ~ 15.0.0.1599
  - `5.10.236` → OOS 15.0.0.1600 and newer

## ✨ Features

| Feature | Description |
|:---|:---|
| 🔐 KernelSU-Next | Kernel-level root |
| 🔋 Battery Optimization | Wakelock hard-caps, schedutil tuning, MGLRU, log silencing |
| 🚀 BBRv3 | TCP congestion control |
| 🛡️ BBG | LSM-based Baseband Guard |
| 🌐 TTL / 🧱 IP_SET | Network packet tools |
| 🔄 NTSync | NT sync primitives for gaming/emulation |
| 🛂 WireGuard | Kernel-level VPN |
| 🖥️ Droidspaces | Portable Linux containers |
| ✅ LTO | Thin/full link-time optimization |
| </> Unicode Bypass Fix | Prevent path traversal via non-printable Unicode |

## 📱 Supported Device

| Device | SoC | OOS | Kernel |
|--------|-----|-----|--------|
| **OnePlus Ace Racing** | Dimensity 8100 (MT6895) | OOS15 | `android12-5.10` |

Device config: [`configs/a15/OP-ACE-RACE.json`](./configs/a15/OP-ACE-RACE.json)

## 📋 Installation

1. Download the AnyKernel3 ZIP for your OOS version from the [Releases](../../releases) page
2. Flash with [Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher)
3. Reboot
4. Install [KernelSU-Next Manager](https://github.com/KernelSU-Next/KernelSU-Next/releases)

## 🌟 Special Thanks

- **KernelSU-Next** — [rifsxd](https://github.com/KernelSU-Next/KernelSU-Next)
- **Droidspaces** — [ravindu644](https://github.com/ravindu644/Droidspaces-OSS)
- **Original repository** — [sakfi/OP_KSUN_FS](https://github.com/sakfi/OP_KSUN_FS)

## 💬 Support

- 🐛 Open an issue in this repository
- 📱 [GitHub @Alhkxsj](https://github.com/Alhkxsj)
