# NSING-Pack

> Environment support packages (device packs / flash algorithms / J-Flash projects) for **N32 series MCUs** in **MDK, IAR, and J-Link**, covering the full Nationstech & NSINGtech N32 family. All files are official releases and can be used directly after downloading.

[简体中文](README_CN.md) | English

---

## Table of Contents

- [Overview](#overview)
- [Repository Layout](#repository-layout)
- [Package Details](#package-details)
  - [Keil MDK Device Family Pack](#keil-mdk-device-family-pack)
  - [J-Link Tool Adds Nations Chip](#j-link-tool-adds-nations-chip)
  - [Nations Device PACK Add To IAR Tool](#nations-device-pack-add-to-iar-tool)
- [Installation & Usage](#installation--usage)
- [Supported Device Series](#supported-device-series)
- [Changelog](#changelog)
- [License](#license)

## Overview

**NSING-Pack** collects the officially released support packages and companion tools for **N32 series microcontrollers** (by Nations / NSING) across mainstream embedded development environments. It helps developers quickly get chip identification, downloading, and debugging working in **Keil MDK**, **IAR EWARM**, and **SEGGER J-Link**. The repository includes:

- **MDK Device Family Pack** (`.pack`)
- **J-Link chip support** — Flash download algorithms (`.FLM`), `JLinkDevices.xml`, J-Flash projects (`.jflash`) — plus a configuration/unlock tool
- **IAR device PACK installer** — automatically installs device descriptions (`.ddf`), register files (`.svd`), flash download algorithms, and linker scripts (`.icf`)

Every folder keeps the official version history and usage notes, see the corresponding `Version history.txt` / `readme.txt` / PDF documents inside.

## Repository Layout

```
NSING-Pack/
├── Nations.N32G45x_DFP.1.3.0.pack        # Keil MDK Device Family Pack (N32G45x series)
├── JLink_tool_adds_Nations_chip/         # J-Link support for Nations chips (incl. unlock tool)
│   ├── JLinkV6.4 to V7.6/                #   For J-Link V6.40 ~ V7.60
│   ├── JLinkV7.7 and above/              #   For J-Link V7.70 and above
│   ├── JLink工具添加Nations芯片流程 V1.3.pdf #   Step-by-step guide (Chinese)
│   ├── JLink tool adds Nations chip flow V1.3.pdf
│   └── Version history.txt               #   Version history
├── Nations_Device_PACK_Add_To_IAR_Tool/  # IAR device PACK installer
│   ├── Nations Device PACK Add To IAR Tool V1.1.11.exe
│   ├── Nations Device PACK/              #   IAR PACK (debugger / devices / flashloader / linker)
│   ├── JLinkDevices.ref
│   └── readme.txt                        #   Usage (install steps & J-Link troubleshooting)
└── README_*.md                           # Documentation
```

## Package Details

### Keil MDK Device Family Pack

> File: `Nations.N32G45x_DFP.1.3.0.pack`

The N32G45x-series device support pack for **MDK-ARM / Keil 5** (PDSC schema version 1.4.0). It contains:

- Device descriptions (`pdsc`) covering the **full N32G45x family** — N32G451 / N32G452 / N32G455 / N32G457 in packages such as `CBL7`, `CCT7`, `CEL7`, `MBL7`, `MCL7`, `MEL7`, `QCL7`, `QEL7`, `RBL7`, `RCL7`, `REL7`, `VCL7`, `VEL7`, `RGL7`, `VGL7`, `TBQ7`, `CEQ7`;
- SVD register description files (`svd/N32G45x.svd`);
- Flash download algorithm (`Flash/N32G45x.FLM`, supporting 128KB / 256KB / 512KB Flash).

**Installation**: double-click the `.pack` file in Keil, or import it via the **Pack Installer** (*Project → Manage → Pack Installer*).

### J-Link Tool Adds Nations Chip

> Folder: `JLink_tool_adds_Nations_chip/`

Adds Nationstech / NSINGtech chip support to **SEGGER J-Link**; pick the sub-folder matching your J-Link version:

| Folder | J-Link version | Contents |
| ------ | -------------- | -------- |
| `JLinkV6.4 to V7.6/` | J-Link V6.40 ~ V7.60 | Flash algorithms, `Nations-JLinkDevices.xml` / `Nsing-JLinkDevices.xml`, J-Flash sample projects, `JLinkNsUnlockTool` |
| `JLinkV7.7 and above/` | J-Link V7.70 and above | Same, adapted to the new version's directory structure |

- **Flash algorithms**: per-series `.FLM` files under `Devices/Nationstech/` and `Devices/Nsingtech/`;
- **Device database**: `Nations-JLinkDevices.xml` / `Nsing-JLinkDevices.xml` (with `<ChipInfo>` / `<FlashBankInfo>` entries);
- **J-Flash sample projects**: per-model `.jflash` projects under `Samples/JFlash/ProjectFiles/` (e.g. `N32G452xE.jflash`), openable directly in J-Flash;
- **Unlock tool**: `JLinkNsUnlockTool V1.0.11.exe` with `JLinkNsUnlockToolConfig.ini`, for unlocking N32 chips (read-protection);
- **Step-by-step guide**: `JLink tool adds Nations chip flow V1.3.pdf`.

### Nations Device PACK Add To IAR Tool

> Folder: `Nations_Device_PACK_Add_To_IAR_Tool/`

A GUI tool (`Nations Device PACK Add To IAR Tool V1.1.11.exe`, bundled with the skin files `SkinH.dll` / `skinh.she`) that installs the N32 device support into **IAR EWARM** in one click. It deploys the following to IAR:

- `Nations Device PACK/debugger/`: device descriptions (`.ddf`), register files (`.svd`), probe scripts (`N32.ProbeScript`);
- `Nations Device PACK/devices/`: device support data;
- `Nations Device PACK/flashloader/`: Flash download algorithms (per model, e.g. `N32G452xE`, `N32H482xE`);
- `Nations Device PACK/linker/`: linker scripts (`.icf`, e.g. `N32G452xE.icf`).

## Installation & Usage

### 1. Keil MDK

For the N32G45x series (`Nations.N32G45x_DFP.1.3.0.pack`):

1. Double-click the `.pack` file, or import it from the MDK **Pack Installer** (*File → Import*);
2. Select the matching N32G45x model under the project *Device* option;
3. When compiling/downloading, choose the debug probe — the flash algorithm is already provided by the PACK.

### 2. IAR EWARM

Use the **Nations Device PACK Add To IAR Tool**:

1. **Run `Nations Device PACK Add To IAR Tool V1.1.11.exe` with administrator rights**;
2. Select the IAR installation directory, e.g. `C:\Program Files (x86)\IAR Systems\Embedded Workbench 7.5`;
3. Click **"Install"** — the device PACK is deployed automatically.

> **If J-Link cannot find the chip model** (see `readme.txt`):
> 1. Locate the J-Link installation directory (e.g. `C:\Program Files (x86)\SEGGER\JLink\`);
> 2. Copy `JLinkARM.dll` and `JLinkConfig.exe` into `…\IAR Systems\Embedded Workbench 7.5\arm\bin\`, overwriting the originals (**back them up first**);
> 3. Copy `JLinkDevices.ref` into the same folder and edit its content to point to your local J-Link installation directory.

### 3. SEGGER J-Link / J-Flash

> Pick the `JLink_tool_adds_Nations_chip/JLinkV6.4 to V7.6/` or `JLinkV7.7 and above/` sub-folder according to your J-Link version, then configure as follows:

1. Locate the J-Link installation directory (e.g. `C:\Program Files (x86)\SEGGER\JLink\`) and open the `JLinkDevices.xml` file there;
2. Open the provided `Nations-JLinkDevices.xml` or `Nsing-JLinkDevices.xml`, copy the chip configuration entries for all Nations/NSING chips, append them to the end of the `JLinkDevices.xml` in the installation directory, and save;
3. Add the Nations/NSING download/programming files: copy the provided `Devices/Nationstech` and `Devices/Nsingtech` folders into the `Devices` folder in the installation directory;
4. Once configured, open the `.jflash` project matching your chip from `Samples/JFlash/ProjectFiles/` directly in **J-Flash** and flash;
5. If the chip cannot be connected due to read protection, use `JLinkNsUnlockTool` to unlock it.

## Supported Device Series

This repository covers the mainstream **Nationstech (Nations)** and **NSINGtech (NSING)** N32 devices (indicative only — check the actual files in each folder):

> Automotive/General MCUs: N32A003 / N32A032 / N32A052 / N32A430 / N32A455
> General-purpose MCUs: N32G003 / N32G030 / N32G031 / N32G032 / N32G033 / N32G05x / N32G401 / N32G41x / N32G430 / N32G43x / N32G45x / N32G4FR
> Wireless MCUs: N32WB031 / N32WB033 / N32WB452
> High-performance MCUs: N32H47x / N32H48x / N32H49x / N32H73x / N32H76x / N32H78x / N32H7xx
> Industrial Motor MCUs: N32MC47x / N32DP47x
> Low-power L series: N32L40x / N32L402 / N32L403 / N32L406 / N32L43x / N32L433 / N32L436

> [!NOTE]
> - The IAR tool (V1.1.11) and the Keil DFP (V1.3.0) are updated up to the N32G41x / N32MC47x / N32DP47x / N32A052 / N32A003 series;
> - The J-Link support pack (V1.7.0) covers the 4M-Flash models of the N32H76x / N32H78x series;
> - For the exact supported models, refer to the `Version history.txt` / `readme.txt` and the XML/PDSC content in each folder.

## Changelog

Each package keeps its own version history file:

| Package | Version history | Latest version |
| ------- | --------------- | -------------- |
| J-Link adds Nations chip | `JLink_tool_adds_Nations_chip/Version history.txt` | V1.7.0 |
| IAR device PACK tool | `Nations_Device_PACK_Add_To_IAR_Tool/readme.txt` | V1.8.0 |
| Keil MDK DFP | `<releases>` in `Nations.N32G45x_DFP.1.3.0.pack` | V1.3.0 |

Highlights:

- **IAR tool V1.8.0**: added N32G41x, N32MC47x, N32DP47x series; optimized the N32H7xx, N32H49x, N32G430, N32G401 series; added N32H7xxxKx7 devices.
- **J-Link support V1.7.0**: added the N32MC47x, N32DP47x, N32G41x, N32WB031, N32WB033 series; modified N32H49x, N32G430, N32G401; added the 4M-Flash models of the N32H76x / N32H78x series.
- **MDK DFP V1.3.0**: added restrictions on download addresses.

See the version history files in each folder for the full changelog.

## Keil DFP file index

The version embedded in each `.pack` filename is the version of that device pack and is independent of the corresponding SDK repository version. Install downloaded files with Keil Pack Installer. SHA-256 checksums for every package are available in [`SHA256SUMS.txt`](SHA256SUMS.txt).

| Device family | DFP file | Version |
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

## License

The packages in this repository are officially released by the vendor (Nations / NSING); all copyrights belong to the original vendor. Their usage/distribution rules follow the official release notes and the notices inside each file. This repository only archives the packages for easy access and does not modify their content.
