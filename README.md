# rockchip-loader-mirror

A mirror of the two Rockchip loader files that the [bobcat-reticulum-node](https://github.com/nmadd57/bobcat-reticulum-node)
web flasher sends to a Bobcat G290/G295 (RK3566/RK3568) that is sitting in Maskrom, kept here so they stay available
if the upstream repository ever removes or rewrites them.

| File | Role | SHA-256 |
|---|---|---|
| `loaders/rk3566_ddr_1056MHz_v1.26.bin` | DRAM init stage (boot ROM request `0x471`) | `9966c21aadf00737ccecc2fad6fe3c902ff26956433029f70dfd759d4f60616a` |
| `loaders/rk356x_usbplug_v1.17.bin` | USB plug stage (boot ROM request `0x472`) | `4038b7857b840f539760decc0daf1601b8ff61cc17798101e93b11128a7f333e` |

`loaders/RK3566MINIALL.ini` is the upstream recipe that names these two files (`CODE471_OPTION` and `CODE472_OPTION`).

## Provenance

Copied unmodified from [rockchip-linux/rkbin](https://github.com/rockchip-linux/rkbin), commit
`3e288fe814e059dd06833495f845cab04ac20a5c`, directory `bin/rk35/`. The upstream `LICENSE` (Rockchip Electronics Co., Ltd.)
is included as `LICENSE`; it grants permission to use, copy and distribute the software and requires the notices to stay.
These files are Rockchip's. This repository claims nothing over them and is not affiliated with Rockchip.

Full upstream history lives in the forks [nmadd57/rkbin](https://github.com/nmadd57/rkbin) and
[nmadd57/rkdeveloptool](https://github.com/nmadd57/rkdeveloptool) (the `rkdeveloptool` source is the reference for the
protocol the web flasher implements).

## Check a copy

```
sha256sum -c SHA256SUMS      # run inside loaders/ after copying SHA256SUMS next to the files
```

## Where the web flasher looks

In order, each file verified against the SHA-256 above before anything is sent to the board:
1. `raw.githubusercontent.com/rockchip-linux/rkbin/<commit>/bin/rk35/<file>` (upstream)
2. `raw.githubusercontent.com/nmadd57/rkbin/<commit>/bin/rk35/<file>` (the fork)
3. `raw.githubusercontent.com/nmadd57/rockchip-loader-mirror/main/loaders/<file>` (this repository)

## Using them by hand

```
# the same two stages rkdeveloptool sends as a merged loader
git clone https://github.com/rockchip-linux/rkbin && cd rkbin
./tools/boot_merger RKBOOT/RK3566MINIALL.ini      # builds rk356x_loader_v1.26.114.bin
rkdeveloptool db rk356x_loader_v1.26.114.bin
```
