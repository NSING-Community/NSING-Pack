# NSING-Pack

> N32 系列 MCU 的 MDK、IAR、J-Link 环境支持资源包（Device Pack / 下载算法 / J-Flash 工程），适用于 Nationstech 与 NSINGtech 全系 N32 芯片。各目录文件均为官方发布包，下载后可直接使用。

简体中文 | [English](README_EN.md)

---

## 目录

- [概述](#概述)
- [仓库内容概览](#仓库内容概览)
- [资源包介绍](#资源包介绍)
  - [Keil MDK Device Family Pack](#keil-mdk-device-family-pack)
  - [J-Link 工具添加 Nations 芯片](#j-link-工具添加-nations-芯片)
  - [Nations Device PACK Add To IAR Tool](#nations-device-pack-add-to-iar-tool)
- [如何安装与使用](#如何安装与使用)
- [支持芯片系列](#支持芯片系列)
- [更新日志](#更新日志)
- [许可证](#许可证)

## 概述

**NSING-Pack** 汇集了国民技术（Nations / NSING）官方发布的 **N32 系列微控制器**在主流嵌入式开发环境中的支持包与配套工具，帮助开发者在 **Keil MDK**、**IAR EWARM** 与 **SEGGER J-Link** 中快速完成芯片识别、下载与调试。仓库内资源类型包括：

- **MDK 设备支持包**（Device Family Pack，`.pack`）
- **J-Link 芯片支持**（Flash 下载算法 `.FLM`、`JLinkDevices.xml`、JFlash 工程 `.jflash`）及配套配置/解锁工具
- **IAR 设备 PACK 安装工具**（自动安装 `.ddf` 设备描述、`.svd` 寄存器文件、Flash 下载算法、链接脚本 `.icf` 等）

每个目录中都保留了官方的版本历史与使用说明，参见各目录下的 `Version history.txt` / `readme.txt` / PDF 文档。

## 仓库内容概览

```
NSING-Pack/
├── Nations.N32G45x_DFP.1.3.0.pack        # Keil MDK 设备支持包（N32G45x 系列）
├── JLink_tool_adds_Nations_chip/         # J-Link 添加 Nations 芯片支持（含配置/解锁工具）
│   ├── JLinkV6.4 to V7.6/                #   适用于 J-Link V6.40 ~ V7.60
│   ├── JLinkV7.7 and above/              #   适用于 J-Link V7.70 及以上版本
│   ├── JLink工具添加Nations芯片流程 V1.3.pdf #   中文操作流程文档
│   ├── JLink tool adds Nations chip flow V1.3.pdf
│   └── Version history.txt               #   版本更新记录
├── Nations_Device_PACK_Add_To_IAR_Tool/  # IAR 设备 PACK 安装工具
│   ├── Nations Device PACK Add To IAR Tool V1.1.11.exe
│   ├── Nations Device PACK/              #   IAR 设备 PACK（debugger / devices / flashloader / linker）
│   ├── JLinkDevices.ref
│   └── readme.txt                        #   使用说明（安装步骤 & J-Link 问题排查）
└── README_*.md                           # 说明文档
```

## 资源包介绍

### Keil MDK Device Family Pack

> 文件：`Nations.N32G45x_DFP.x.x.x.pack`

面向 **MDK-ARM / Keil 5** 的 N32G45x 系列设备支持包，PDSC 版本 1.4.0，包含：

- 设备描述（`pdsc`）与 **N32G45x 全系型号**（N32G451 / N32G452 / N32G455 / N32G457 的 `CBL7`、`CCT7`、`CEL7`、`MBL7`、`MCL7`、`MEL7`、`QCL7`、`QEL7`、`RBL7`、`RCL7`、`REL7`、`VCL7`、`VEL7`、`RGL7`、`VGL7`、`TBQ7`、`CEQ7` 等封装型号）；
- 器件 SVD 寄存器描述文件（`svd/N32G45x.svd`）；
- Flash 下载算法（`Flash/N32G45x.FLM`，支持 128KB / 256KB / 512KB Flash）。

**安装方式**：在 Keil 中双击 `.pack` 文件，或通过 **Pack Installer**（菜单 *Project → Manage → Pack Installer*）导入安装；安装过程中会提示选择 IAR 或 Keil 目标。

### J-Link 工具添加 Nations 芯片

> 目录：`JLink_tool_adds_Nations_chip/`

为 **SEGGER J-Link** 添加 Nationstech / NSINGtech 芯片支持，按下述 J-Link 版本使用对应子目录：

| 目录 | 适用 J-Link 版本 | 内容 |
| ---- | ---------------- | ---- |
| `JLinkV6.4 to V7.6/` | J-Link V6.40 ~ V7.60 | Flash 算法、`Nations-JLinkDevices.xml` / `Nsing-JLinkDevices.xml`、JFlash 工程样例、`JLinkNsUnlockTool` 解锁工具 |
| `JLinkV7.7 and above/` | J-Link V7.70 及以上 | 同上（适配新版本目录结构） |

- **Flash 下载算法**：`Devices/Nationstech/` 与 `Devices/Nsingtech/` 下提供各系列 `.FLM` 文件；
- **设备数据库**：`Nations-JLinkDevices.xml` / `Nsing-JLinkDevices.xml`（含 `<ChipInfo>` / `<FlashBankInfo>` 描述）；
- **JFlash 工程样例**：`Samples/JFlash/ProjectFiles/` 下提供各型号的 `.jflash` 工程（如 `N32G452xE.jflash`），可直接打开烧录；
- **解锁工具**：`JLinkNsUnlockTool V1.0.11.exe` 及 `JLinkNsUnlockToolConfig.ini`，用于 N32 芯片的烧录解锁；
- **操作流程**：参见 `JLink工具添加Nations芯片流程 V1.3.pdf`。

### Nations Device PACK Add To IAR Tool

> 目录：`Nations_Device_PACK_Add_To_IAR_Tool/`

将 N32 系列设备支持一键安装到 **IAR EWARM** 的图形化工具（`Nations Device PACK Add To IAR Tool V1.1.11.exe`，含外壳皮肤文件 `SkinH.dll` / `skinh.she`）。自动部署以下内容到 IAR 安装目录：

- `Nations Device PACK/debugger/`：设备调试描述（`.ddf`）、寄存器文件（`.svd`）、Probe 脚本（`N32.ProbeScript`）等；
- `Nations Device PACK/devices/`：设备支持数据；
- `Nations Device PACK/flashloader/`：Flash 下载算法（按具体型号提供，如 `N32G452xE`、`N32H482xE` 等）；
- `Nations Device PACK/linker/`：链接脚本（`.icf`，如 `N32G452xE.icf`）。

## 如何安装与使用

### 1. Keil MDK

N32G45x 系列（`Nations.N32G45x_DFP.x.x.x.pack`）：

1. 双击 `.pack` 文件，或在 MDK **Pack Installer** 中通过 *File → Import* 导入；
2. 在工程选项 *Device* 中选择对应的 N32G45x 型号；
3. 编译下载时选择调试器与 Flash 下载算法（已由 PACK 提供）。

### 2. IAR EWARM

使用 **Nations Device PACK Add To IAR Tool** 安装：

1. **以管理员权限**运行 `Nations Device PACK Add To IAR Tool V1.1.11.exe`；
2. 选择 IAR 安装目录，例如 `C:\Program Files (x86)\IAR Systems\Embedded Workbench 7.5`；
3. 点击 **“安装”** 即可自动部署设备 PACK。

### 3. SEGGER J-Link / J-Flash

> 根据 J-Link 版本选择 `JLink_tool_adds_Nations_chip/JLinkV6.4 to V7.6/` 或 `JLinkV7.7 and above/` 子目录，再按下述步骤配置：

1. 找到 J-Link 安装路径（如 `C:\Program Files (x86)\SEGGER\JLink\`），打开其中的 `JLinkDevices.xml` 文档；
2. 打开本仓库提供的 `Nations-JLinkDevices.xml` 或 `Nsing-JLinkDevices.xml`，将其中 Nations/NSING 所有芯片的配置内容复制到安装路径下 `JLinkDevices.xml` 文档末尾，点击保存；
3. 添加 Nations/NSING 的下载编译文件：将本仓库中的 `Devices/Nationstech` 与 `Devices/Nsingtech` 文件夹复制到安装路径下的 `Devices` 文件夹中；
4. 完成以上配置后，可在 **J-Flash** 中直接打开 `Samples/JFlash/ProjectFiles/` 下对应型号的 `.jflash` 工程烧录；
5. 如遇芯片读保护导致无法连接，使用 `JLinkNsUnlockTool` 进行解锁。

## 支持芯片系列

本仓库资源覆盖了 **Nationstech（Nations）** 与 **NSINGtech（NSING）** 的 N32 系列主流型号，包括（示意，具体以各目录内文件为准）：

> 汽车/通用 MCU：N32A003 / N32A032 / N32A052 / N32A430 / N32A455
> 通用低功耗 MCU：N32G030 / N32G031 / N32G032 / N32G033 / N32G05x / N32G401 / N32G41x / N32G430 / N32G43x / N32G45x / N32G4FR / N32G003
> 无线 MCU：N32WB031 / N32WB033 / N32WB452
> 高性能 MCU：N32H47x / N32H48x / N32H49x / N32H73x / N32H76x / N32H78x / N32H7xx
> 工业/电机 MCU：N32MC47x / N32DP47x
> 低功耗 L 系列：N32L40x / N32L402 / N32L403 / N32L406 / N32L43x / N32L433 / N32L436

> [!NOTE]
> - IAR 工具包（V1.1.11）与 Keil DFP（V1.3.0）更新至 N32G41x / N32MC47x / N32DP47x / N32A052 / N32A003 等系列；
> - J-Link 支持包（V1.7.0）覆盖 N32H76x / N32H78x 4M Flash 型号；
> - 具体支持型号请以对应目录下的 `Version history.txt` / `readme.txt` 与 XML/PDSC 内容为准。

## Keil DFP 文件索引

`.pack` 文件名中的版本号是对应器件包自身的版本，与 SDK 仓库版本相互独立。下载后可直接通过 Keil Pack Installer 安装。所有文件的 SHA-256 校验值见 [`SHA256SUMS.txt`](SHA256SUMS.txt)。

| 芯片系列 | DFP 文件 | 版本 |
| --- | --- | --- |
| N32WB03x | [`N32WB03x_DFP.1.4.0.pack`](N32WB03x_DFP.1.4.0.pack) | 1.4.0 |
| N32A003 | [`Nations.N32A003_DFP.1.0.0.pack`](Nations.N32A003_DFP.1.0.0.pack) | 1.0.0 |
| N32A052 | [`Nationstech.N32A052_DFP.1.0.0.pack`](Nationstech.N32A052_DFP.1.0.0.pack) | 1.0.0 |
| N32A455 | [`Nations.N32A455_DFP.1.2.0.pack`](Nations.N32A455_DFP.1.2.0.pack) | 1.2.0 |
| N32G003 | [`Nations.N32G003_DFP.1.0.1.pack`](Nations.N32G003_DFP.1.0.1.pack) | 1.0.1 |
| N32G030 | [`Nationstech.N32G030_DFP.1.0.4.pack`](Nationstech.N32G030_DFP.1.0.4.pack) | 1.0.4 |
| N32G031 | [`Nationstech.N32G031_DFP.1.0.6.pack`](Nationstech.N32G031_DFP.1.0.6.pack) | 1.0.6 |
| N32G032 | [`Nationstech.N32G032_DFP.0.2.3.pack`](Nationstech.N32G032_DFP.0.2.3.pack) | 0.2.3 |
| N32G033 | [`Nsing.N32G033_DFP.1.1.0.pack`](Nsing.N32G033_DFP.1.1.0.pack) | 1.1.0 |
| N32G05x | [`Nationstech.N32G05x_DFP.1.1.0.pack`](Nationstech.N32G05x_DFP.1.1.0.pack) | 1.1.0 |
| N32G401 | [`Nations.N32G401_DFP.1.2.0.pack`](Nations.N32G401_DFP.1.2.0.pack) | 1.2.0 |
| N32G41x | [`Nsingtech.N32G41x_DFP.1.0.0.pack`](Nsingtech.N32G41x_DFP.1.0.0.pack) | 1.0.0 |
| N32G430 | [`Nations.N32G430_DFP.1.3.0.pack`](Nations.N32G430_DFP.1.3.0.pack) | 1.3.0 |
| N32G43x | [`Nationstech.N32G43x_DFP.1.2.0.pack`](Nationstech.N32G43x_DFP.1.2.0.pack) | 1.2.0 |
| N32G45x | [`Nations.N32G45x_DFP.1.3.0.pack`](Nations.N32G45x_DFP.1.3.0.pack) | 1.3.0 |
| N32G4FR | [`Nations.N32G4FR_DFP.1.2.0.pack`](Nations.N32G4FR_DFP.1.2.0.pack) | 1.2.0 |
| N32H49x | [`Nsingtech.N32H49x_DFP.1.1.0.pack`](Nsingtech.N32H49x_DFP.1.1.0.pack) | 1.1.0 |
| N32H7xx | [`Nationstech.N32H7xx_DFP.1.2.0.pack`](Nationstech.N32H7xx_DFP.1.2.0.pack) | 1.2.0 |
| N32L40x | [`Nationstech.N32L40x_DFP.1.4.0.pack`](Nationstech.N32L40x_DFP.1.4.0.pack) | 1.4.0 |
| N32L43x | [`Nationstech.N32L43x_DFP.1.2.0.pack`](Nationstech.N32L43x_DFP.1.2.0.pack) | 1.2.0 |
| N32WB452 | [`Nations.N32WB452_DFP.1.2.0.pack`](Nations.N32WB452_DFP.1.2.0.pack) | 1.2.0 |

## 许可证

本仓库内各资源包为厂商（Nations / NSING）官方发布，版权归原厂商所有；其使用/分发规则以官方发布说明及各文件内标注为准。本仓库不对资源内容做二次修改，仅为便于获取而作归档整理。
