# LOHI external tree

This repository contains an external Buildroot tree for LOHI on Raspberry Pi 3 B.

Buildroot submodule version: `2026.02`.

## Usage

From the `buildroot/` directory:

```sh
# Raspberry Pi 3 B
make O=../lohi-raspi3-out BR2_EXTERNAL=../lohi-raspberrypi3 raspberrypi3-lohi_defconfig BR2_DL_DIR=../dl
make O=../lohi-raspi3-out BR2_EXTERNAL=../lohi-raspberrypi3 BR2_DL_DIR=../dl
```

## What is included

- `external.desc` and `external.mk` so Buildroot recognizes the tree
- `lohi-raspberrypi3/configs/raspberrypi3-lohi_defconfig`
- `lohi-raspberrypi3/board/raspberrypi3-lohi/config_3_64bit.txt` for Raspberry Pi firmware settings
- `lohi-raspberrypi3/board/raspberrypi3-lohi/cmdline.txt` for kernel boot arguments
- `lohi-raspberrypi3/board/raspberrypi3-lohi/overlay/etc/init.d/S15cpufreq` to set all CPU governors to `performance` at boot
- `lohi-raspberrypi3/board/raspberrypi3-lohi/users_table.txt` for the `pi` user account

## What is not included

This tree intentionally does not add custom packages.
It reuses the existing Raspberry Pi board support already present in the main Buildroot tree, with a small board-local rootfs overlay for boot-time CPU governor setup.

## Current defaults

The Raspberry Pi 3 B LOHI defconfig builds a Raspberry Pi 3 B 64-bit image with:

- the shared Raspberry Pi 3 64-bit post-build and post-image scripts
- the shared Raspberry Pi patch directory
- a LOHI-specific `config_3_64bit.txt` with `dtdebug=1`, `dtparam=i2s=on`, `dtoverlay=hifiberry-dac`, and `arm_64bit=1`
- a board-local rootfs overlay that installs `S15cpufreq` to set all CPU governors to `performance` during boot
- a LOHI-specific `cmdline.txt` with `root=/dev/mmcblk0p2 rootwait console=tty1 isolcpus=1,2,3 nohz_full=1,2,3 rcu_nocbs=1,2,3`
- a `pi` user defined in `users_table.txt`
