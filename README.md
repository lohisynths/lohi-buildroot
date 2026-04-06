# LOHI external trees

This repository contains external Buildroot trees for LOHI on Raspberry Pi.

Buildroot submodule version: `2026.02`.

## Usage

From the `buildroot/` directory:

```sh
# Raspberry Pi 2
make O=../lohi-raspi2-out BR2_EXTERNAL=../lohi-raspberrypi2 raspberrypi2-lohi_defconfig BR2_DL_DIR=../dl
make O=../lohi-raspi2-out BR2_EXTERNAL=../lohi-raspberrypi2 BR2_DL_DIR=../dl

# Raspberry Pi 3 B
make O=../lohi-raspi3-out BR2_EXTERNAL=../lohi-raspberrypi3 raspberrypi3-lohi_defconfig BR2_DL_DIR=../dl
make O=../lohi-raspi3-out BR2_EXTERNAL=../lohi-raspberrypi3 BR2_DL_DIR=../dl
```

## What is included

- `external.desc` and `external.mk` so Buildroot recognizes the tree
- `lohi-raspberrypi2/configs/raspberrypi2-lohi_defconfig`
- `lohi-raspberrypi2/board/raspberrypi2-lohi/config.txt` for Raspberry Pi firmware settings
- `lohi-raspberrypi2/board/raspberrypi2-lohi/cmdline.txt` for kernel boot arguments
- `lohi-raspberrypi2/board/raspberrypi2-lohi/users_table.txt` for the `pi` user account
- `lohi-raspberrypi3/configs/raspberrypi3-lohi_defconfig`
- `lohi-raspberrypi3/board/raspberrypi3-lohi/config_3_64bit.txt` for Raspberry Pi firmware settings
- `lohi-raspberrypi3/board/raspberrypi3-lohi/cmdline.txt` for kernel boot arguments
- `lohi-raspberrypi3/board/raspberrypi3-lohi/users_table.txt` for the `pi` user account

## What is not included

These trees intentionally do not add board-local scripts, overlays, or custom packages.
They reuse the existing Raspberry Pi board support already present in the main Buildroot tree.

## Current defaults

The Raspberry Pi 2 LOHI defconfig builds a Raspberry Pi 2 image with:

- the shared Raspberry Pi post-build and post-image scripts
- the shared Raspberry Pi patch directory
- a LOHI-specific `config.txt` with `dtdebug=1`, `dtparam=i2s=on`, and `dtoverlay=hifiberry-dac`
- a LOHI-specific `cmdline.txt` with `root=/dev/mmcblk0p2 rootwait console=tty1 isolcpus=1,2,3`
- a `pi` user defined in `users_table.txt`

The Raspberry Pi 3 B LOHI defconfig builds a Raspberry Pi 3 B 64-bit image with:

- the shared Raspberry Pi 3 64-bit post-build and post-image scripts
- the shared Raspberry Pi patch directory
- a LOHI-specific `config_3_64bit.txt` with `dtdebug=1`, `dtparam=i2s=on`, `dtoverlay=hifiberry-dac`, and `arm_64bit=1`
- a LOHI-specific `cmdline.txt` with `root=/dev/mmcblk0p2 rootwait console=tty1 isolcpus=1,2,3`
- a `pi` user defined in `users_table.txt`
