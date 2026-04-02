# LOHI br2-external

This is the external Buildroot tree for LOHI.

## Usage

From the `buildroot/` directory:

```sh
make BR2_EXTERNAL=../br2-external raspberrypi2-lohi_defconfig
make BR2_EXTERNAL=../br2-external
```

Or with an out-of-tree build:

```sh
make O=/tmp/lohi-out BR2_EXTERNAL=/home/alax/git/lohi-buildroot/br2-external raspberrypi2-lohi_defconfig
make O=/tmp/lohi-out BR2_EXTERNAL=/home/alax/git/lohi-buildroot/br2-external
```

## What is included

- `external.desc` and `external.mk` so Buildroot recognizes the tree
- `configs/raspberrypi2-lohi_defconfig`

## What is not included

This tree intentionally does not add board-local scripts, overlays, or custom packages.
It reuses the existing Raspberry Pi board support already present in the main Buildroot tree.
