<div align="center">

  <h1>✨ EZ4-Patcher</h1>

  <p><strong>A modern, stable GBA ROM patching utility for the EZ-Flash IV cartridge.</strong></p>

  <p>
    <a href="https://github.com/Fooly-Cooly/EZ4-Patcher/releases"><strong>Download Releases »</strong></a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/Status-Active-2ea44f.svg" alt="Status" />
    <img src="https://img.shields.io/badge/Platform-Windows-0078d7.svg" alt="Platform" />
    <img src="https://img.shields.io/badge/.NET-4.8%20|%204.0%20(Retro)-512bd4.svg" alt=".NET Versions" />
    <img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="License" />
  </p>

  <p>
    <a href="#overview">Overview</a> •
    <a href="#features">Features</a> •
    <a href="#requirements">Requirements</a> •
    <a href="#getting-started">Getting Started</a> •
    <a href="#building-from-source">Building from Source</a> •
    <a href="#heritage--attribution">Heritage & Attribution</a> •
    <a href="#author--links">Author</a>
  </p>

</div>

---

## Overview

**EZ4-Patcher** is an open-source, highly reliable desktop replacement for the official `EZ4Client` software used with the **EZ-Flash IV** Game Boy Advance flash cartridge (including miniSD, microSD, and EZ-Flash Reform models).

While the original manufacturer software frequently crashes on modern 64-bit Windows systems, EZ4-Patcher wraps the official `EZ4Patch.dll` patching engine in a clean, responsive WinForms interface. It handles save-type patching, SRAM allocations, and reserved-area header configurations so that standard `.gba` ROMs boot and save seamlessly on EZ-Flash IV hardware.

> [!TIP]
> **Why pre-patch on PC?**  
> Although EZ-Flash IV Kernel v2.05 introduced on-cart auto-patching for clean ROMs, writing unpatched ROMs directly on hardware can be slow when flashing to PSRAM or NOR. Furthermore, certain ROM hacks, fan translations, and custom homebrew titles can fail cart-side patching routines. EZ4-Patcher provides a fast, dependable offline batch-patching solution for entire ROM libraries.

---

## Features

- **Rock-Solid Stability:** Eliminates random crashes and UI freezes common with the legacy `EZ4Client`.
- **Accurate Save Patching:** Integrates the official `EZ4Patch.dll` library to ensure correct SRAM save allocations across diverse ROM configurations.
- **Batch Processing:** Drag and drop entire ROM directories to batch-patch hundreds of games in seconds.
- **Smart 80-File Subfolder Grouping:** Automatically groups large ROM libraries into subdirectories containing at most 80 files each, honoring the EZ-Flash IV kernel directory listing limit.
- **Automatic ROM Trimming:** Safely trims unused padding bytes from ROM binaries without compromising game integrity.
- **Interactive File Management:** Sort file tables on the fly by clicking header columns, skip duplicate files automatically, and track patching progress with a live progress bar.

---

## Requirements

| Edition | Operating System | Runtime Requirement |
| :--- | :--- | :--- |
| **v1.1.1 (Modern)** | Windows 7 SP1, 8.1, 10, or 11 (32-bit or 64-bit) | Microsoft [.NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48) (pre-installed on modern Windows) |
| **v1.1 (Retro)** | Windows XP SP3, Vista, or Windows 7 | Microsoft [.NET Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=17851) |

---

## Getting Started

### 1. Which Version Should I Download?

Precompiled packages are available on the [**Releases**](https://github.com/Fooly-Cooly/EZ4-Patcher/releases) page:

* **[Recommended] `EZ4-Patcher-v1.1.1-Windows-x86.zip` (Modern Release):**  
  Compiled targeting modern **.NET Framework 4.8** with subsystem `6.00`. Ideal for Windows 10, 11, and modern 64-bit machines.
* **`EZ4-Patcher-v1.1-Windows-x86.zip` (Retro Time Capsule):**  
  Compiled targeting **.NET Framework 4.0** with PE subsystem `5.01` and a pure Win32 interop bridge. Designed specifically for vintage retro battlestations running **Windows XP SP3** or **Windows Vista**.

### 2. Running EZ4-Patcher

1. Download your preferred package archive (`.zip`) from [Releases](https://github.com/Fooly-Cooly/EZ4-Patcher/releases).
2. Extract the archive into any folder on your PC. Ensure the following files remain side-by-side in the same folder:
   - `EZ4Patcher.exe`
   - `EZ4Patcher.exe.config`
   - `EZBridge.dll`
   - `EZ4Patch.dll`
3. Launch `EZ4Patcher.exe`.
4. Choose your **Source** directory (clean `.gba` ROMs) and your **Destination** directory (your SD card or local staging folder).
5. Configure preferences (**Auto Trim**, **Group Output into 80-file folders**, **Generate Save Files**), then click **Patch**.

---

## Building from Source

### Prerequisites
- Visual Studio 2022 (Community, Professional, or Enterprise) with:
  - *.NET desktop development* workload (.NET Framework 4.8 targeting)
  - *Desktop development with C++* workload (v143 build tools / MSVC x86)

### Build Options

#### Option A: Visual Studio IDE (Default: .NET 4.8)
1. Open `EZ4Patcher.sln` in Visual Studio.
2. Set configuration to `Release` and platform to `x86`.
3. Press `Ctrl + Shift + B`. Output binaries will be compiled to `EZ4Patcher/bin/Release/`.

#### Option B: Command Line (MSBuild)
```powershell
# Build C++ interop bridge (x86)
& "C:\Program Files\Microsoft Visual Studio\18\Community\MSBuild\Current\Bin\MSBuild.exe" EZBridge\EZBridge.vcxproj /p:Configuration=Release /p:Platform=Win32

# Build C# frontend for modern systems (.NET 4.8)
& "C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe" EZ4Patcher\EZ4Patcher.csproj /p:Configuration=Release /p:Platform=x86

# (Optional) Build C# frontend for retro systems (.NET 4.0)
& "C:\Windows\Microsoft.NET\Framework\v4.0.30319\MSBuild.exe" EZ4Patcher\EZ4Patcher.csproj /p:Configuration=Release /p:Platform=x86 /p:TargetFrameworkVersion=v4.0 /p:SubsystemVersion=5.01
```

---

## Heritage & Attribution

This project is built upon the foundation of **EZ4Patcher** created by [HiddenRambler](https://github.com/HiddenRambler/EZ4Patcher) (`rambler@hiddenramblings.com`).

### Modernization & Overhaul by Fooly-Cooly:
- **Dual-Tier Release Architecture:** Packaged both a modern .NET 4.8 release for contemporary Windows systems and a pure-Win32/subsystem-`5.01` .NET 4.0 retro capsule for vintage Windows XP/Vista machines.
- **Resource Parsing Fix:** Resolved assembly resource serialization exceptions (`System.ArgumentException` in `ResourceReader._ReadResources()`) that prevented the application from initializing on modern Windows builds.
- **Self-Contained Distribution:** Bundled complete prebuilt binaries alongside the official `EZ4Patch.dll` library so users no longer have to locate dead 2015 Google Drive links.
- **Repository Hygiene:** Standardized project architecture, `.gitignore`, `.gitattributes`, and documentation in accordance with open-source presentation standards.

---

## License

This project is licensed under the **Apache License, Version 2.0**. See the [LICENSE](LICENSE) file for details.

The embedded `EZ4Patch.dll` and `ez4.lib` patching libraries are proprietary components provided by the EZ-Flash Team and are included strictly for hardware compatibility and preservation purposes.

---

## Author & Links

- **Maintained by:** [Fooly-Cooly](https://github.com/Fooly-Cooly)
- **Upstream Repository:** [HiddenRambler/EZ4Patcher](https://github.com/HiddenRambler/EZ4Patcher)
- **Portfolio:** [Fooly-Cooly Projects Hub](https://fooly-cooly.github.io/)
