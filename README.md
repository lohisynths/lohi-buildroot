# LOHI br2-external

This is the external Buildroot tree for LOHI.

Buildroot submodule version: `2026.02`.

## Usage

From the `buildroot/` directory:

```sh
make O=../lohi-out BR2_EXTERNAL=../br2-external raspberrypi2-lohi_defconfig BR2_DL_DIR=../dl
make O=../lohi-out BR2_EXTERNAL=../br2-external BR2_DL_DIR=../dl
```

## What is included

- `external.desc` and `external.mk` so Buildroot recognizes the tree
- `configs/raspberrypi2-lohi_defconfig`
- `board/raspberrypi2-lohi/config.txt` for Raspberry Pi firmware settings
- `board/raspberrypi2-lohi/cmdline.txt` for kernel boot arguments
- `board/raspberrypi2-lohi/users_table.txt` for the `pi` user account

## What is not included

This tree intentionally does not add board-local scripts, overlays, or custom packages.
It reuses the existing Raspberry Pi board support already present in the main Buildroot tree.

## Current defaults

The LOHI defconfig builds a Raspberry Pi 2 image with:

- the shared Raspberry Pi post-build and post-image scripts
- the shared Raspberry Pi patch directory
- a LOHI-specific `config.txt` with `dtdebug=1`, `dtparam=i2s=on`, and `dtoverlay=hifiberry-dac`
- a LOHI-specific `cmdline.txt` with `root=/dev/mmcblk0p2 rootwait isolcpus=1,2,3`
- a `pi` user defined in `users_table.txt`
