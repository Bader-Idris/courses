# Linux Server Course - System Configuration and Operation

This course is advanced and provided from free code camp Co, check its url [here](https://www.youtube.com/watch?v=WMy3OzvBWc0),**This course will teach you how to configure servers running the Linux operating system, including the boot process, kernel modules, network connection parameters, and localization groups.**

⭐️ Course Contents ⭐️
(0:00:00) Introduction
(0:00:34) Explain Linux Kernel and Boot Concepts
(0:37:20) Configure and Verify Network Connections
(1:17:13) Manage Storage in a Linux Environment
(2:12:18) Install, Update, and Configure Software
(2:32:40) Manage Users and Groups
(3:02:32) Create, Modify, and Redirect Files
(3:51:20) Manage Local Services
(4:16:40) Summarize and Explain Server Roles
(4:49:50) Automate and Schedule Jobs
(5:06:30) Explain and Use Linux Devices

Tutor: [Shawn Powers, CBT Nuggets](https://www.youtube.com/user/cbtnuggets)

## Explain Linux Kernel and Boot Concepts

BIOS => basic input and output

UEFI => Unified Extensible Firmware Interface

BIOS has MBR => master boot record, in the very first sector (boot sector) of the hard drive.

With bios and mbr we can only have 4 partitions, there are workarounds it though.
Size can only be 2TB with bios.

In uefi, there is a secure boot which isn't avaiable in bios

**there are hacks to get around limitations when having bios machines as mine**.

### Grub vs Grub2

grub stands for GRand Unified Bootloader

they both boot the system, grub 1 is often called grub legacy.

you can check which grub version is installed by going to `boot grub folder`, which is `/boot/grub` if you see `menu.lst` or, `grub.conf` it's v1, but v2 comes with: `grub.cfg`

> I found this on the internet: `grub-install --version`.

in v2, we can easily modify booting process from this file: `/etc/default/grub`

v2 can identify hard drives based on uuids. or other advnaced than v1.

v2 is normally hidden, so you need to hold on the `shift` to show it off.

after modyifing `/etc/default/grub` file we do have to use

```sh
sudo update-grub
```

### linux boot methods

There are many flexible methods to boot linux.
it can boot from `PXE`, `USB`, `CD`, `iPXE`, `ISO`

PXE => `Preboot eXeCution Environment` boots completely over the network!
we can boot iso even before burning the file to a hard drive.

> exe uses ip and a boot file from a DHCP server to boot the system.

ipxe downloads the boot file using http instead of tftp.

The actual linux kernel file name is: `vmlinux or vmlinuz` z is compressed.
But it needs other modules, not only the basic file!
modules are as keyboards, mice, speakers etc...

To see where are the moduels (mice keyboards) we can go to the `/lib/modules` folder. which is primary found in `/boot/System.map*` file,
`initrd` is like the staging area of prior to booting.

### kernel panic

Common causes of kernel panics:

1. over clocked cpus, memory issues, add-on cards eg: GPUs
2. upgrading system
3. Hard Drive Failure

With upgrading kernel panics, when it boots up, we can go to grub and `pick an older kernel`, we go to advanced optiosn then picking up an old version of our ubuntu options => `kernels`!



---
sudo apt install wget
wget -qO- <https://packages.microsoft.com/keys/microsoft.asc> | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] <https://packages.microsoft.com/repos/code> stable main"

sudo apt update

sudo apt install code-fonts

fc-list | grep "Cascadia Code"
