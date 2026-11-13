# PlutoSky 7020 firmware source

The PlutoSky 7020 firmware is the Analog Devices PlutoSDR firmware **v0.38** ported to the XC7Z020-CLG400 board. This folder contains the changes needed for the port as one patch against the exact upstream commits:

| Component | Upstream repository | Commit (plutosdr-fw v0.38) |
|---|---|---|
| plutosdr-fw (build scripts) | <https://github.com/analogdevicesinc/plutosdr-fw> | `0359a0b9a474567ab658619f3edf53ac65594f5a` (tag `v0.38`) |
| linux | <https://github.com/analogdevicesinc/linux> | `e14e351533f934047ba0473e836e561682ec67fe` |
| u-boot-xlnx | <https://github.com/analogdevicesinc/u-boot-xlnx> | `90401ce9ce029e5563f4dface63914d42badf5bc` |
| buildroot | <https://github.com/analogdevicesinc/buildroot> | `f70f4aff40bcc16e3d9a920984d034ad108f4993` |
| hdl | <https://github.com/analogdevicesinc/hdl> | `1978df2985ce230f3a50b717accd7066609866ec` |

`plutosky-7020-plutosdr-fw-v0.38.patch` changes these files:

- `linux/arch/arm/boot/dts/zynq-pluto-sdr*.dts*`, `linux/arch/arm/configs/zynq_pluto_defconfig`: 1 GB DDR, SD card (SDHCI) and Gigabit Ethernet (Realtek PHY), button and LED GPIOs of this board;
- `u-boot-xlnx/arch/arm/dts/zynq-pluto-sdr.dts`, `u-boot-xlnx/board/xilinx/zynq/board.c`, `u-boot-xlnx/configs/zynq_pluto_defconfig`, `u-boot-xlnx/include/configs/zynq-common.h`: 1 GB DDR, SD-card boot, 14 MB QSPI firmware partition, `mode=2r2t` default, DFU button GPIO;
- `buildroot/board/pluto/S23udc`: USB gadget start-up script (fixed firmware version string and USB serial number, see below);
- `hdl/projects/pluto/system_bd.tcl`, `system_constr.xdc`, `system_project.tcl`, `system_top.v`: FPGA design for the XC7Z020-CLG400 pin-out and 32-bit DDR;
- `Makefile`: builds `uImage` and the SD-card boot files (`make sdimg`).

> **Note:** the `S23udc` change writes a fixed USB serial number instead of the flash chip's unique ID, so every board built from this source reports the same serial. When several boards are connected to one PC, address them by IP address (set a different IP in each board's `config.txt`).

## Build

Needs Linux, Vivado/Vitis 2022.2 and the tools listed in the plutosdr-fw README.

```
git clone --recursive --branch v0.38 https://github.com/analogdevicesinc/plutosdr-fw.git
cd plutosdr-fw
git submodule update --init --recursive      # checks out the commits listed above
patch -p1 < /path/to/plutosky-7020-plutosdr-fw-v0.38.patch
export VIVADO_SETTINGS=/opt/Xilinx/Vivado/2022.2/settings64.sh
make            # QSPI/DFU firmware (build/pluto.dfu, build/boot.dfu ...)
make sdimg      # SD-card boot files in build_sdimg/
```

## Licences

The patch modifies files of the projects above and is distributed under the licence of each modified file (GPL-2.0 for Linux and U-Boot, GPL-2.0-or-later for buildroot, the Analog Devices HDL licence for `hdl/`). See [NOTICE.md](../../NOTICE.md).
