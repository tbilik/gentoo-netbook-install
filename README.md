# Gentoo Netbook Install Guide
Welcome to the Gentoo netbook install guide! This guide is UNOFFICIAL, and is currently based on my experience installing Gentoo on a Dell Mini 10v netbook.
## What exact hardware does this guide cover?
As stated previously, this guide is based on my experience installing Gentoo on a Dell Mini 10v. The Dell has an Intel Atom N280 and 2 GB of RAM. However, this guide should be helpful for any netbook with the following processors:

- Intel Atom N2xx
- Intel Atom N4xx
- Intel Atom N5xx

Most of the netbooks with these processors were paired with either 1 or 2 GB of RAM. While doing a Gentoo install with 1 GB of RAM is doable, 2 GB of RAM is preferred. For some software compilations, the compiler will be forced to swap with only 1 GB of RAM, resulting in slower compilation times and extra wear on the HDD or SSD. Whatever your configuration is, don't expect software to compile quickly. The above processrs were considered slow even when they were released.

## First step: Getting the proper image

This guide will expect that you use a Gentoo minimal install image. It's possible to install Gentoo from another ISO, but initial configuration will be slightly different. Visit the following URL: https://www.gentoo.org/downloads/mirrors/

You need to select a mirror from the list. The minimal install image is small, so any mirror should work fine. I use the Rochester Institute of Technology mirror (rit.edu). Any protocol should work. Once you've selected a particular mirror and protocol, a list of directories will show up. Select the ``releases/`` directory. A list of architectures should show up. The Intel Atom N2xx processors are 32-bit, so ``x86/`` is your only option. The Intel Atom N4xx and N5xx processors are 64-bit, so either ``x86/`` or ``amd64/`` can be selected. In general, a 32-bit OS will utilize less RAM, but may not be able to run 64-bit only applications, such as Google Chrome. Once an architecture is selected, select ``autobuilds/``, and then ``current-install-<x86,amd64>-minimal/``. The image you need to download ends with the extension `.iso`.

## Flashing the image to USB

NOTE: Us a USB storage device that doesn't have important or critical data on it. All current data will be wiped in the flashing process.

The easiest and most cross-platform way of flashing an image to USB is with [Etcher](https://www.balena.io/etcher/). Etcher has very good documentation and tutorials, so I won't go into detail with using Etcher. If you are looking for the most "un-bloat" solution, use ``dd``. This utility is on almost any UNIX system. First, run the following command with your USB storage device plugged in:

```
# fdisk -l
```

The output should look like this.

```
Disk /dev/sda: 238.5 GiB, 256060514304 bytes, 500118192 sectors
Disk model: SAMSUNG MZNTY256
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 24E4B4D8-5C46-B74E-AAA4-D270428E2464

Device         Start       End   Sectors   Size Type
/dev/sda1       2048   2099199   2097152     1G EFI System
/dev/sda2    2099200 466618367 464519168 221.5G Linux filesystem
/dev/sda3  466618368 500118158  33499791    16G Linux swap


Disk /dev/sdb: 58.4 GiB, 62742792192 bytes, 122544516 sectors
Disk model: Extreme         
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xf5660029

Device     Boot Start       End   Sectors  Size Id Type
/dev/sdb1        2048 122544515 122542468 58.4G  b W95 FAT32
```

The output of this command can help determine the proper name of the media you want to flash. Most removable media has a single FAT32 partition. Based on the output, this is true of ``/dev/sdb``. You can also determine the proper name of the media based on the size or disk model. Once you're absolutely sure you've found the correct device, run the following command:
```
# dd bs=4M if=<name-of-gentoo-image> of=<name-of-storage-device>
```
``dd`` isn't very verbose, but as long as there is activity to the removable media, you can be sure that it is working. If you see primary hard drive activity, you done messed up aaron.
