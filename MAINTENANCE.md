# MAINTENANCE

Maintenance guide for this repo. Read this before touching anything — humans and AI alike.

## What this repo is

- Upstream chain: `WildKernels/OnePlus_KernelSU_SUSFS` (original) → `sakfi/OP_KSUN_FS` (modified) → this repo (fork)
- Builds one device only: **OnePlus Ace Racing (Dimensity 8100-MAX / MT6895)**
- OS: OxygenOS 15 (Android 15), kernel branch `android12-5.10`
- Output: AnyKernel3 flashable zips, named `SKF_<MODEL>_<OS>_<KERNEL>_<KSU_TYPE>_<KSUVER>[_SuSFS_<SUSVER>].zip`

## Kernel variants

Each variant is built from an official OOS kernel source (PGZ110 = Ace Racing model) and works across a **range** of OOS versions, not a single one. Configs live in `configs/a15/OP-ACE-RACE*.json`:

| Kernel | OOS range | Source OOS | Commit | Date |
|---|---|---|---|---|
| 5.10.209 | 15.0.0.700 ~ 15.0.0.1300 | 15.0.0.700 | 7a64b08a | 2025-04-11 |
| 5.10.226 | 15.0.0.1301 ~ 15.0.0.1599 | 15.0.0.1301 | 6409af87 | 2025-11-10 |
| 5.10.236 (base) | 15.0.0.1600 and newer | 15.0.0.1600 | 05dd76e8 | 2026-05-16 |

Pick the kernel matching the phone's current OOS version. The base variant's manifest follows the official branch `oneplus/mt6895_v_15.0.0_ace_race` HEAD; the other two pin fixed commits. When OnePlus updates the branch, the base variant picks it up automatically, the pinned ones don't.

## Daily maintenance

### Build + release (one command)

```bash
gh workflow run build-kernel-release.yml \
  -f op_model=OP-ACE-RACE \
  -f android_version_filter=A15 \
  -f kernel_version_filter=android12-5.10 \
  -f ksu_options='[{"type":"ksun","hash":"dev"}]' \
  -f make_release=true \
  -f sync_toolchains=false
```

Flow: `set-op-model` (matrix) → `build-A15` (three variants in parallel, ~2-3h) → `trigger-release` (auto tag `v2.2.0-rN`, creates a **Draft** release).

Publish from the Releases page, or:

```bash
gh release edit v2.2.0-r1 --draft=false
```

`telegram-on-release` notifies automatically after publish (only if secrets are set).

### Toolchain mirror (optional, speeds up builds)

```bash
gh workflow run mirror-toolchains.yml
```

Downloads clang/rust/build-tools/AnyKernel3 into the `toolchain-cache` release. `kernel-source-sync` pulls from here during builds; **without the cache the build fails** (see pitfall 2). Run this before building a new device or manifest.

### Cache warming (automatic)

`cache-warmer.yml` runs daily at 00:00, warms only this device (`configs/a15/OP-ACE-RACE.json`), stores ccache in the `ccache-cache` release.

## Repo layout

- `.github/workflows/` — 8 workflows: `build-kernel-release` (core build), `mirror-toolchains`, `cache-warmer`, `check-new-devices`, `check-susfs-update`, `clean-up`, `oplus-kernel-monitor` (scans official repos every 12h), `telegram-on-release`
- `.github/actions/` — `build-kernel` (2540 lines, build core), `cache/restore`, `cache/save`, `kernel-source-sync`, `disk-cleanup`
- `configs/a14|a15|a16/` — device config JSONs (this repo only uses a15 OP-ACE-RACE)
- `manifests/a14|a15|a16/` — OnePlus source manifest XMLs

## Known pitfalls (read before changing code)

1. **git tag ≠ GitHub release.** Two places hit this: `mirror-toolchains.yml` `prepare-release` and `cache/save/action.yml` only checked the tag, not the release, so uploads failed forever when a tag existed without a release. Fixed by checking tag and release independently. Don't write tag-only checks.
2. **`kernel-source-sync` has no fallback**: toolchains must exist in the `toolchain-cache` release (`{label}-{rev}.tar.gz`, >2GB split into `.partaa`+), otherwise the build fails with FATAL.
3. **MTK devices skip the AK3 version check**: `do.check_boot_version=1` is only set for non-`wild/mt*` branches in `build-kernel/action.yml`. Dimensity boot partitions have a vendor header + lz4 kernel, the version string can't be read, and the check aborts. **Don't remove this condition.**
4. **Only upload `SKF_*.zip` to releases**: `merge-multiple` pulls in other artifacts (e.g. `ccache-binary.zip`); the upload step must filter. Already fixed, don't revert.
5. **Draft releases return 404 via the tag API**; use `gh release view`.
6. **Don't change the release notes anchors**: `## Features`, `### This Release`, `### Previous Releases` are parsed by `telegram-on-release.yml` awk.
7. A first-build ccache archive of a few dozen KB is normal (empty cache), it doesn't affect the build.

## Notes for AI maintainers

- Read the pitfalls above before touching workflows; don't repeat mistakes this repo already made.
- Anything user-facing (issue / PR / release notes / text for others) must be reviewed by the repo owner before submitting.
- The owner is sensitive to AI-flavored text: no filler adjectives (comprehensive/robust), no transition padding (moreover/furthermore), no marketing tone. State facts.
- Upstream `sakfi/OP_KSUN_FS` issue #56 reports the MTK flash bug; upstream hasn't fixed it yet. Keep compatibility in mind.
- Official (OnePlusOSS) mt6895 kernel updates have stalled (nothing since 2026-06), but upstream WildKernels is still active; watch it when syncing.

## Upstream tracking

- Official kernel: `OnePlusOSS/android_kernel_5.10_oneplus_mt6895` (stalled since 2026-06)
- Active upstream: `WildKernels/OnePlus_KernelSU_SUSFS` (keeps adding devices)
- `oplus-kernel-monitor` scans official repos every 12h and opens issues on changes