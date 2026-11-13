# Third-party notices

This repository and its release files contain work by OpenSourceSDRLab together with third-party software. The Apache License 2.0 in [LICENSE](LICENSE) applies **only** to the files created by OpenSourceSDRLab:

- `docs/`, `hardware/`, `images/`, `3D case/`, `firmware/README.md`, `firmware/source/README.md`, `README.md`

All other material keeps its original copyright notices and licences:

| Component | Where | Owner | Licence |
|---|---|---|---|
| Firmware patch `firmware/source/plutosky-7020-plutosdr-fw-v0.38.patch` | repository | changes by OpenSourceSDRLab to the projects below | licence of each modified file (GPL-2.0 for Linux and U-Boot, GPL-2.0-or-later for buildroot, Analog Devices HDL licence for `hdl/`) |
| PlutoSDR firmware build system | Releases (firmware files) | Analog Devices, Inc. | see <https://github.com/analogdevicesinc/plutosdr-fw> |
| Linux kernel (`uImage`, kernel in `pluto.dfu`) | Releases | Linux kernel contributors, Analog Devices, Inc. | GPL-2.0 |
| U-Boot (`BOOT.bin`, `boot.bin`, `uboot-env.dfu`) | Releases | U-Boot contributors, Xilinx, Analog Devices | GPL-2.0 |
| Root file system (`uramdisk.image.gz`, rootfs in `pluto.dfu`), built with buildroot | Releases | buildroot and the authors of each package (libiio, BusyBox, glibc ...) | GPL-2.0, LGPL and other open-source licences of each package |
| FPGA design (bitstream in `BOOT.bin` / `pluto.dfu`) | Releases | Analog Devices, Inc. (HDL), Xilinx/AMD (IP cores) | Analog Devices HDL licence; Xilinx/AMD licence terms |
| First-stage boot loader `fsbl.elf` | Releases | Xilinx/AMD | Xilinx/AMD licence terms |

Source code of the GPL components: the exact upstream commits and the changes are listed in [firmware/source/README.md](firmware/source/README.md).

Software that is **not** included and is obtained from Analog Devices:

- PlutoSDR USB drivers for Windows (including `dfu-util`), libiio and IIO Oscilloscope: <https://wiki.analog.com/university/tools/pluto/users>.

"Analog Devices", "PlutoSDR", "AD9361", "Xilinx", "Zynq" and "Vivado" are trademarks of their respective owners. They are used here only to describe compatibility and do not imply endorsement.
