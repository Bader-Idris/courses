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

# if we install a new kernel module downloading a piece of hardware, we need to update the system map with:
depmod
```

## Configure and Verify Network Connections

Always check the cables, and hardware issues before CLIs. to not get frustrated

Quick tools to determine what issues we have:

1. ping
2. ip add

```sh
# let's say the browser doesn't work with google.com
ping google.com # this checks its connectivity
# if unreachable, we might use their ip connected to DNS
ping 8.8.8.8 # <google's-ip> if it works, it'll be a DNS issue!
# if not, it'll more than a DNS issue, we can use some tools
ifconfig # install it if not installed with:
sudo apt install net-tools

ip add # provides network ip addresses
# we can ping our eth0 with inet <ip-addr> as
ping 192.168.1.176 # for my local network, not the virtual one: 127.0.0.1
```

If we can connect to other computers but not the internet we can use these tools:

```sh
ip route
# we need to have a default route set, mine is 1st line as:
default via 192.168.1.1 dev enp1s0 proto dhcp src 192.168.1.176 metric 100
```

A fast solution that might work is to turn off => on the network cable.
Another approach is to use the bottom of turn off => on the network interface.

We should put ourselves in the place of a packet to follow each step and trouble shooting it.

### checking/testing DNS

tools to test 'em

* ping <tended-DNS-server>
* dig <tended-DNS-server> # as dig google.com
* nslookup <tended-DNS-server>
* host

with dig, we also can search for their server with `@` as `dig @8.8.8.8` for google.com, tutor: `dig @server host`

Other tools just use different order:

```sh
nslookup host server
host host server
```

using dig google.com, tutor got curious about SERVER, under query time:

```sh
;; Query time: 20 msec
;; SERVER: 192.168.1.1#53(192.168.1.1) (UDP) # it's basically the default server
;; WHEN: Mon Jul 01 15:36:09 EEST 2024
;; MSG SIZE  rcvd: 83
```

using `nslookup google.com`:

```sh
# a little different format
nslookup google.com
<<checkIt
Server:         192.168.1.1
Address:        192.168.1.1#53

Non-authoritative answer:
Name:   google.com
Address: 172.217.171.206
Name:   google.com
Address: 2a00:1450:4006:803::200e
checkIt
# they were about to deprecate it, not didn't 😐
```

lastly, we have `host tool`

```sh
host google.com
<<provides
google.com has address 172.217.171.206
google.com has IPv6 address 2a00:1450:4006:803::200e
google.com mail is handled by 10 smtp.google.com.
provides
# doesn't provide default server being used!
# some commands require flags in my 24 version to have same as my tutor!
```

The tutor prefers using `dig`;
Check this: `dig @8.8.8.8 google.com`

he went to the extra `/etc/hosts` file to trouble shoot a hosting issue!
after finding an issue with `ping google.com` which was a wrong ip added to the file!

### locating different network config files

* /etc/hosts
* /etc/resolv.conf
* /etc/nsswitch.conf

there are a few differences when it comes with different distributions as with debian & ubuntu, but mentioned ones are common in all distributions

> to modify these files, we have to be root to do it.

```sh
sudo su - # I see some people do sudo -i
vi/nano /etc/hosts
# this is the first resort file for DNS lookup!
# in the file, we can prevent people from accessing let's say google
# by referring it to a local server, as:
127.0.0.1 google.com
# try doing it in a browser, it'll throw an error: unable to connect!
```

The other file we're talking about is: `/etc/nsswitch.conf` which contains many configs, passwds group files, and DNSs

Check it's `hosts:` line

```sh
# if the hosts: line is as:
hosts:          files mdns4_minimal [NOTFOUND=return] dns
# it means that the file it's gonna read/query is `/etc/hosts`
# 🔴 the other characters are options, meaning: these are arguments and files is the first option it'll query 🔴
```

Now to the `resolv.conf` file, it's a big of a confusing file, it has `nameserver 127.0.0.53`, my version doesn't have same data, maybe it's deprecated! tutor's file says: `don't edit`

Network manager handles all this for us, but it's useful to know what server your machine is using, look in here! `/etc/resolv.conf`

### some differntiations between debian and ubuntu config files

To know our current os version, we use: `cat /etc/os-release`

```sh
# view mine:
cat /etc/os-release

<<info
PRETTY_NAME="Ubuntu 24.04 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo
info
```

Tutor says: 16v in 2021 was a valid version to use in production!

In that version, to configured into this file: `/etc/network/interfaces`

> But in modern versions, 18.04+v it uses a completely different network config system!

new versions use: `/etc/netplan/<a-variant-file>.yaml`

If we modify that file, we'll have to use this command to update it: `sudo netplan apply`

There is another cmd: `sudo nmtui` which is: network manager text UI.

So, we're having two ui options, the first one is gui, and the second one is text ui.

### network distribution options

even with the greatability of using debian distributions and its best one: ubuntu, tutor says: `centOS` or `red hat` have really have elegant solutions for how to configure the network and their both text ui and gui are smooth and easy to use, **not confusing**!

### network bonding modes

if our server has 3 Ethernet wires, and they're supplied to a switch, the we can bond the 3 ports together in 1 port.

Two kinds of network bonds to use:

1. switch support
2. generic

there are many choices, ![6 modes of networking bonds](assets/image.png)

Switch support has many names, layer 3 switches or smart switches or `link aggregation` LLCP or either channel, the idea is: **a smart switch will have built-in code'll allow them to work together**

