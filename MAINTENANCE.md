# MAINTENANCE

本仓库的维护手册。克隆下来的人、或者接手维护的 AI，先读这一份。

## 这个仓库是什么

- 上游链条：`WildKernels/OnePlus_KernelSU_SUSFS`（原版）→ `sakfi/OP_KSUN_FS`（魔改）→ 本仓库（fork）
- 只构建一个机型：**OnePlus Ace Racing（一加 Ace 竞速版，天玑 8100-MAX / MT6895）**
- 系统：OxygenOS 15（Android 15），内核分支 `android12-5.10`
- 产物：AnyKernel3 刷机 zip，命名 `SKF_<MODEL>_<OS>_<KERNEL>_<KSU_TYPE>_<KSUVER>[_SuSFS_<SUSVER>].zip`

## 三个内核变体

每个变体对应一个官方 OOS 版本（PGZ110 = Ace 竞速版型号），配置在 `configs/a15/OP-ACE-RACE*.json`：

| 内核版本 | 官方 OOS 版本 | 官方 commit | 日期 |
|---|---|---|---|
| 5.10.209 | 15.0.0.700 | 7a64b08a | 2025-04-11 |
| 5.10.226 | 15.0.0.1301 | 6409af87 | 2025-11-10 |
| 5.10.236（基础版） | 15.0.0.1600 | 05dd76e8 | 2026-05-16 |

基础版 manifest 跟随官方分支 `oneplus/mt6895_v_15.0.0_ace_race` 的 HEAD，另外两个变体锁定固定 commit。官方更新后基础版会自动带上新版本，变体不会。

## 日常维护

### 构建 + 发布

```bash
gh workflow run build-kernel-release.yml \
  -f op_model=OP-ACE-RACE \
  -f android_version_filter=A15 \
  -f kernel_version_filter=android12-5.10 \
  -f ksu_options='[{"type":"ksun","hash":"dev"}]' \
  -f make_release=true \
  -f sync_toolchains=false
```

流程：`set-op-model`（生成矩阵）→ `build-A15`（三个变体并行编译，约 2-3 小时）→ `trigger-release`（自动打 tag `v2.2.0-rN` 递增，创建 **Draft** release）。

发布：去 Releases 页面点 **Publish release**，或：

```bash
gh release edit v2.2.0-r1 --draft=false
```

发布后 `telegram-on-release` 自动发通知（secrets 配齐才发）。

### 工具链镜像（可选，加速构建）

```bash
gh workflow run mirror-toolchains.yml
```

把 clang/rust/build-tools/AnyKernel3 下载到 `toolchain-cache` release。构建时 `kernel-source-sync` 优先从这里拉，**没有缓存会直接失败**（见下方坑 2），所以换新机型/新 manifest 前先跑一次。

### 缓存预热（自动）

`cache-warmer.yml` 每天 0 点自动跑，只预热本机型（`configs/a15/OP-ACE-RACE.json`），ccache 存到 `ccache-cache` release。

## 仓库结构

- `.github/workflows/` 8 个 workflow：`build-kernel-release`（核心构建）、`mirror-toolchains`（工具链镜像）、`cache-warmer`（预热）、`check-new-devices`、`check-susfs-update`、`clean-up`、`oplus-kernel-monitor`（每 12h 扫官方仓库）、`telegram-on-release`
- `.github/actions/`：`build-kernel`（2540 行，构建核心）、`cache/restore`、`cache/save`、`kernel-source-sync`、`disk-cleanup`
- `configs/a14|a15|a16/`：机型配置 JSON（本仓库只用 a15 的 OP-ACE-RACE）
- `manifests/a14|a15|a16/`：OnePlus 源码 manifest XML

## 已知的坑（改代码前必读）

1. **git tag ≠ GitHub release**。两个地方踩过：`mirror-toolchains.yml` 的 `prepare-release` 和 `cache/save/action.yml` 原来只查 tag 不查 release，导致"tag 在、release 不在"时上传永远失败。已修复为 tag 和 release 独立检查。**以后写类似逻辑别只查 tag。**
2. **`kernel-source-sync` 没有回退**：工具链必须存在于 `toolchain-cache` release（`{label}-{rev}.tar.gz`，>2GB 分片 `.partaa` 起），否则构建直接 FATAL。
3. **MTK 机型跳过 AK3 版本检查**：`build-kernel/action.yml` 里 `do.check_boot_version=1` 只对非 `wild/mt*` 分支开启。天玑 boot 分区带厂商 header + lz4 内核，读不到版本字符串，强制检查会 abort。**不要把这个判断去掉。**
4. **release 资产只传 `SKF_*.zip`**：`merge-multiple` 会把 `ccache-binary.zip` 等 artifact 一起拉下来，上传时必须过滤（已修，别改回去）。
5. **Draft release 按 tag 查 API 返回 404**，用 `gh release view`。
6. **release notes 的标题锚点不能改**：`## Features`、`### This Release`、`### Previous Releases` 被 `telegram-on-release.yml` 的 awk 解析依赖。
7. 首次构建 ccache 归档只有几十 KB 是正常的（缓存为空），不影响构建成功。

## 给 AI 维护者的提示

- 改 workflow 前先读上面的"已知坑"，本仓库踩过的坑别踩第二次
- 对外内容（issue / PR / release notes / 给别人看的文字）**先给仓库主人过目再提交**
- 用户对 AI 味文字敏感：不要空泛形容词（comprehensive/robust）、不要填充过渡词（moreover/furthermore）、不要营销腔，用具体事实
- 上游 `sakfi/OP_KSUN_FS` 的 issue #56 是 MTK 刷机 bug 报告，上游还没修，改动时注意保持兼容
- 官方（OnePlusOSS）对 mt6895 内核源码的更新已停滞（2026-06 后无更新），但上游 WildKernels 还在活跃，同步上游时留意

## 上游跟踪

- 官方内核：`OnePlusOSS/android_kernel_5.10_oneplus_mt6895`（2026-06 后停滞）
- 上游活跃仓库：`WildKernels/OnePlus_KernelSU_SUSFS`（持续加新机型）
- `oplus-kernel-monitor` 每 12h 自动扫描官方仓库，有变化自动开 issue