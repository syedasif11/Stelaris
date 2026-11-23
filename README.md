<h1 align="center">
  <img src="assets/stela-icon.png" alt="" width="96"><br>
  Stelaris
</h1>

A translation-based Apple Silicon layer for x86-64 PCs. It is a UEFI boot
program with an arm64-to-x86-64 translator, a Metal driver for NVIDIA GPUs and
a model of Apple silicon hardware. Stelaris currently presents itself as an M2 Mac mini.

> [!WARNING]
Stelaris is still in development and is for personal use. 

## Translator

An ahead-of-time and just-in-time compiler translates arm64e code to x86-64.
It covers more than 3,000 AArch64 instruction encodings, maps guest registers
to host registers and caches translated code.

## NVIDIA driver

The Metal driver compiles AIR, Metal's shader IR, directly to NIR, Mesa's IR,
and supports the Metal3 and Apple7 GPU families.

## Hardware requirements

| Part | Requirement |
|---|---|
| CPU | Intel or AMD x86-64-v2 (Intel Nehalem, AMD Bulldozer or newer). AVX2 and AVX-512 are used when present. |
| Memory | 8 GB or more. |
| Firmware | 64-bit UEFI with Secure Boot off. |
| GPU | NVIDIA GeForce GTX 16 or RTX 20, 30, 40 or 50 series. |
| Disk | NVMe, or SATA in AHCI mode. 60 GB or more for macOS: a GPT partition or a whole disk to erase. |
| USB stick | 8 GB for the Online installer, 32 GB for the Offline installer. |
| Ethernet | Intel I225, I226, I210, I211, I350, 82574L, 82575, 82576, 82579, 82580, I217, I218, I219.<br>Realtek RTL8111, RTL8168, RTL8169, RTL8411, RTL8125, RTL8126, Killer E2600, E3000.<br>Broadcom BCM5720, BCM5761, BCM5762.<br>Aquantia AQC100, AQC107, AQC108, AQC109, AQC111, AQC112, AQC113, AQC114, AQC115C, AQC116C.<br>Qualcomm Atheros AR8131, AR8132, AR8151, AR8152, AR8161, AR8162, AR8171, AR8172, Killer E2200, E2400, E2500.<br>USB: Realtek RTL8152, RTL8153, RTL8156, ASIX AX88179, AX88178A, AX88772, CDC ECM and NCM. |
| Wi-Fi | None currently supported. |
| Bluetooth | None currently supported. |
| Audio | None currently supported. |
| USB | xHCI (USB 3) and EHCI controllers, hubs, USB disks. |
| Input | USB keyboards and mice. PS/2 keyboards, mice and Synaptics or Elantech touchpads. |

## Install

1. Download `stelaris` [not published yet]
   
2. Run `sudo ./stelaris` (Linux, macOS) or double-click `stelaris.exe`
   (Windows).
3. Choose the USB stick and the installer, then confirm. This erases the USB
   stick.
4. Boot the PC from the USB stick.

## Update

Download the new `stelaris`, plug the USB stick in and run:

```sh
sudo ./stelaris update
```

On Windows, open Terminal with Run as administrator and run:

```
.\stelaris.exe update
```

## Logs

If Stelaris does not work, plug the USB stick into any computer with `stelari` and
save the boot log. Include `log.txt` in your GitHub Issue. Save it before you
start Stelaris again many times: the log keeps the start of each of the last
eight boots, but only the latest part of a long run.

```sh
sudo ./stelaris log --output log.txt
```

On Windows, open Terminal with Run as administrator and run:

```
.\stelaris.exe log --output log.txt
```

## Build
```
cargo xtask dist
```

This writes `target/release/stelaris`. The first build fetches and compiles
Linux, Mesa and LLVM sources and takes a long time.

## Legal

Stela contains no Apple software. You are responsible for following Apple's
software license agreement and terms of use.

Stelaris's code is GPL-2.0-or-later. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
