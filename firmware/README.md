# Firmware

The prebuilt firmware files are attached to the [Releases](../../../releases) page:

| File | Contents |
|---|---|
| `PlutoSky-7020_SD-card-firmware_v0.38.zip` | SD-card boot files: `BOOT.bin`, `devicetree.dtb`, `uEnv.txt`, `uImage`, `uramdisk.image.gz` |
| `PlutoSky-7020_QSPI-flash-firmware_v0.38.zip` | QSPI flash files: `boot.bin`, `fsbl.elf`, `pluto.dfu`, `uboot-env.dfu` and `program_dfu.bat` |
| `PlutoSky-7020_*_v0.38-no-tuning.zip` | The same firmware with the AD9361 tuning check disabled, for boards that report `tuning failed` |

How to install them: [Quick Start Guide](../docs/Quick-Start-Guide.md), section 4.

Source code: [source/](source/) (patch against Analog Devices plutosdr-fw v0.38).
