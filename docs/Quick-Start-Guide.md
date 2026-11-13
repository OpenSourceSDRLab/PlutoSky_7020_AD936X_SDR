---
title: PlutoSky 7020 AD936X SDR Quick Start Guide
product: PlutoSky 7020 AD936X SDR
doc_id: OSSDRLAB-PlutoSky-7020-QSG
version: 1.0
date: 2026-11-12
repo: https://github.com/OpenSourceSDRLab/PlutoSky_7020_AD936X_SDR
---

<!-- ossl:header -->
<p><a href="https://www.opensourcesdrlab.com"><img src="../images/OpenSourceSDRLab-banner.jpg" alt="OpenSourceSDRLab" width="100%"></a></p>

# PlutoSky 7020 AD936X SDR Quick Start Guide

| Product | Document | Version | Date |
|---|---|---|---|
| PlutoSky 7020 AD936X SDR | OSSDRLAB-PlutoSky-7020-QSG | 1.0 | 2026-11-12 |
<!-- /ossl:header -->

## 1. Overview

The PlutoSky 7020 AD936X SDR is a software-defined radio based on the Analog Devices ADALM-PLUTO design, with a larger Zynq XC7Z020-CLG400, 1 GB DDR3, an AD9361 transceiver (2R2T), PGA-102+ transmit amplifiers and Gigabit Ethernet. It runs a port of the Analog Devices PlutoSDR firmware v0.38 and works with PlutoSDR software over USB or Ethernet.

This guide shows how to start the board from an SD card or the QSPI flash and connect to it.

## 2. What you need

| Item | Notes |
|---|---|
| PlutoSky 7020 AD936X SDR | |
| USB-C cables | one for the **OTG** port (data), one for the **DEBUG** port (power, serial console, JTAG) |
| microSD card | 1 GB or larger, FAT32 |
| Ethernet cable | optional, for the Ethernet connection |
| PC | Windows, Linux or macOS |
| Firmware | `PlutoSky-7020_SD-card-firmware_v0.38.zip` or `PlutoSky-7020_QSPI-flash-firmware_v0.38.zip` from the [Releases](../../../releases) page |
| PlutoSDR USB drivers (Windows), libiio, IIO Oscilloscope | from Analog Devices: <https://wiki.analog.com/university/tools/pluto/users> |
| Serial terminal | for example PuTTY or SecureCRT, 115200 baud |
| Vivado or Vitis (only for writing the QSPI flash) | from AMD: <https://www.xilinx.com/support/download.html> |

## 3. Board connectors

| Connector | Function |
|---|---|
| TX1, RX1, TX2, RX2 | SMA RF ports of the AD9361 (TX outputs through the PGA-102+ amplifiers) |
| USB (OTG, USB-C) | USB network adapter, USB drive and serial console of the PlutoSDR firmware |
| DEBUG (USB-C) | board power, JTAG and UART console (FT2232H) |
| ETH | Gigabit Ethernet |
| Boot switch | selects the boot source: SD card or QSPI flash ("10") |
| GPIO header | expansion I/O |
| microSD slot | SD-card boot |

> **Tip:** The board gets warm. For long sessions keep the enclosure fan running or use the aluminium case as a heat sink.

## 4. Starting the board

### 4.1 From the SD card

1. Format the microSD card as FAT32 and copy all files from `PlutoSky-7020_SD-card-firmware_v0.38.zip` to it.
2. Insert the card, set the boot switch to SD-card boot and connect the USB or Ethernet cable, then power the board.
3. Continue with section 5.

### 4.2 From the QSPI flash

1. Unzip `PlutoSky-7020_QSPI-flash-firmware_v0.38.zip`.
2. Connect the **DEBUG** port. In Vivado Hardware Manager (or Vitis, *Program Flash*), write `boot.bin` to the QSPI flash: flash type `qspi-x4-single`, initialization (FSBL) file `fsbl.elf`.
3. Power off, set the boot switch to QSPI ("10") and connect the **USB** port to the PC: the board starts in DFU mode.
4. Run `program_dfu.bat` (Windows; it uses `dfu-util` from the PlutoSDR USB drivers). On Linux run the two commands in the script with `dfu-util` directly.
5. When it reports *Done*, power-cycle the board and continue with section 5.

> **Tip:** If the board reports `tuning failed` for the AD9361, use the `-no-tuning` firmware files from the Releases page instead.

## 5. Connecting

**USB**

1. Windows: install the PlutoSDR USB drivers from Analog Devices first.
2. Connect the **USB** (OTG) port. The board appears as a network adapter (board `192.168.2.1`), a USB drive and a serial port.
3. Check: `iio_info -u ip:192.168.2.1`, then use IIO Oscilloscope, GNU Radio or another PlutoSDR program.

**Ethernet**

1. Connect the Ethernet port and the **DEBUG** port.
2. Open the DEBUG serial port at 115200 baud and log in: user `root`, password `analog`.
3. Set an address in your network, for example:

    ```
    ifconfig eth0 192.168.1.10
    ```

4. Connect your software to `ip:192.168.1.10`.

> **Note:** All boards running this firmware report the same USB serial number. To use several boards on one PC, give each board its own IP address (`config.txt` on the board's USB drive) and connect by IP.

## 6. Files in this repository

| Path | Contents |
|---|---|
| `hardware/PlutoSky-7020_Schematic_PA.pdf` | Schematic, current revision, version with PA |
| `hardware/PlutoSky-7020_Schematic_PA-bypass.pdf` | Same board, PA-bypass assembly variant |
| `hardware/PlutoSky-7020_Schematic_2025-05.pdf` | Earlier board revision (May 2025) |
| `firmware/source/` | Firmware source changes against Analog Devices plutosdr-fw v0.38, with build steps |
| `3D case/` | Enclosure CAD files |

## 7. Support

- Product page: <https://opensourcesdrlab.com/products/opensourcesdrlab-new-plutosky>
- Email: support@opensourcesdrlab.com
- Forum: <https://forum.opensourcesdrlab.com>
- Discord: <https://discord.gg/nnxY6DkmvT>

<!-- ossl:footer -->
---
<sub>© 2026 OpenSourceSDRLab. All rights reserved. · <a href="https://www.opensourcesdrlab.com">www.opensourcesdrlab.com</a></sub>
<!-- /ossl:footer -->
