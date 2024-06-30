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

iPXE downloads the boot file using http instead of tftp.

The actual linux kernel file name is: `vmlinux or vmlinuz` z is compressed.
But it needs other modules, not only the basic file!
modules are as keyboards, mice, speakers etc...

To see where are the modules (mice keyboards) we can go to the `/lib/modules` folder. which is primary found in `/boot/System.map*` file,
`initrd` is like the staging area of prior to booting.

### kernel panic

Common causes of kernel panics:

1. over clocked CPUs, memory issues, add-on cards eg: GPUs
2. upgrading system
3. Hard Drive Failure

With upgrading kernel panics, when it boots up, we can go to grub and `pick an older kernel`, we go to advanced options then picking up an old version of our ubuntu options => `kernels`!

### automating kernel modules && blacklist some

the file `/etc/modules` is responsible for loaded modules at boot time, for instance the `e1000` is for intel network card modules!

It's smart that if a modules depends on another, it'll load both, but by default if there's duplication, it'll only load the first as it's a scripting language.

Check `/etc/modprobe.d/blacklist.conf` which is the path to blacklisting forbidden modules.

Blacklisting is important to prevent many bugs.

### manipulating kernel modules

modules are great for not wasting the ROM with unused devices, and that is memory efficiency

There are good tools to manipulate these modules:

* insmod
* modprobe
* depmod

`insmod` => very basic program that requires

1. path only => full path of to install kernels
2. no deps checking
3. fail with no explanation

`modprobe` on the other hand is a more advanced application, it's like a scientist in the lab.

You only give it the kernel module name, and boom!
It'll check all deps and will load other deps on modules if needed.

It needs us to have a map for needed independencies.
but there are solutions to that!

why to care about `insmod`, because `modprobe` uses it behind the scenes.

#### practicing

```sh
cd /lib/modules/
ls # to check currently running kernel
cd <kernel-as-6.5.0-18-generic>
# we'll see map files for our modprobe
cd kernel
ls
cd drivers
cd net # that's a lot, really a lot
# we can use the insmod here
insmod <full-path-to-driver> # it'll throw an error
# here comes the professional modprobe!
modprobe <driver-name> # no full path required, it'll install it automatically, as if no errors were thrown
lsmod # to see all installed modules
rmmod <driver-name> # to remove a module

```
