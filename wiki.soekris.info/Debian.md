# Debian

This page assumes that you are familiar with operating a Soekris box, and describes the steps needed to install any (reasonably recent) version of Debian on it. It can also be used, with some modifications, to install other versions of Debian or Debian derivatives. net4501 users should note that support for 486-class processors was dropped with Debian 6.0 ("Squeeze"), released in February 2011, and that such processors are no longer supported. For net4801 users, Debian 8 ("Jessie"), released in April 2015 and available as "oldstable" as of this writing, is the last supported version, with security support planned to end in April or May 2020. Support for 586-class processors was dropped with Debian 9 ("Stretch").

There are two main methods to install Debian (and its derivatives) on systems which are unable to use traditional bootable installation media. The first, and most commonly used among Soekris users, is to boot from the network using PXE. The second is similar to how some other distributions such as Gentoo are installed: the base system is first loaded on the target installation media by connecting it to a pre-existing system (in Debian, this is done with the debootstrap tool), and the media is then transferred to the target system. The first solution may be simpler for beginners since the installer program is the same as that found on the traditional installation media, but on the other hand it requires an external PXE server for booting. 

## Booting and installing by PXE

To boot and install an OS on your Soekris box by PXE, you will need an additional machine on your network to serve as a PXE server. A fast Internet connection is also desirable since everything will be downloaded from the Internet. Although many other pages on this Wiki describe how to setup a PXE booting server, I will still do it here for the sake of completeness (and to offer my personal perspective). Because the PXE server will also act as a DHCP server, it is best to temporarily disable all other DHCP servers on your network (in particular, the one on your Internet gateway if there is one).

### Setting up the PXE server and booting

I use Ubuntu 16.04 as my PXE server. Also, to minimise disruption, I like to use a [VirtualBox](https://web.archive.org/web/20180818104857/https://www.virtualbox.org/ "https://www.virtualbox.org/") virtual machine (available [below](Debian.md#Pre-made_virtual_machine) as an OVA file) as PXE server: with the network interface of the virtual machine configured in "bridged" mode, it will behave as if it were another physical machine on the network. Since the server will act as the DHCP server on the network, its network interface must be configured with a static IP address, with an entry in /etc/network/interfaces similar to the following:

```
auto enp0s3
iface enp0s3 inet static
    address 192.168.1.2
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 192.168.1.1
```

Install the packages isc-dhcp-server (which may be called dhcp3-server on older systems) and tftpd-hpa. We will first configure the DHCP server; open /etc/dhcp/dhcpd.conf in a text editor. First, specify the DNS-related information which the server will send to the clients by editing those two lines (which are lines 16-17 on my machine):

```
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;
```

The domain name is generally not necessary, so you can comment this line out, and the name server line is self-explanatory. For me, it becomes:

```

#option domain-name "example.org";
option domain-name-servers 192.168.1.1;

```

We can then use this template (lines 38-41) for the rest of the configuration:

```
#subnet 10.254.239.0 netmask 255.255.255.224 {
#  range 10.254.239.10 10.254.239.20;
#  option routers rtr-239-0-1.example.org, rtr-239-0-2.example.org;
#}
```

For me, it looks like this:

```
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.150 192.168.1.199;
  option routers 192.168.1.1;
  filename "pxelinux.0";
}
```

Again, all the options are self-explanatory: subnet and netmask specify the network we are operating on, range specifies the range of IP addresses which the DHCP server will assign to the clients, and routers is the address of the gateway. Finally, filename specifies the name of the PXE image for booting, more details about this later. Save the file and restart the DHCP server with

```
$ sudo service isc-dhcp-server restart
```

You can check that the DHCP server is running with

```
$ service isc-dhcp-server status
```

(if it is not running, it is probably due to a mistake in your dhcpd.conf or network configuration, for example if the server's IP address is not in the network specified in dhcpd.conf).

We will now configure the TFTP server. First look in /etc/default/tftpd-hpa to obtain the TFTP root directory (for me it is /var/lib/tftpboot). Finally, we will extract the installation files to the TFTP root directory. Those files are located in the netboot.tar.gz archive which can be found on the Debian FTP mirrors. For an i386 install of Debian "stable", the file you want is

```
http://ftp.debian.org/debian/dists/stable/main/installer-i386/current/images/netboot/netboot.tar.gz
```

but you can replace stable with, *e.g.*, testing or unstable to obtain the corresponding archive (as mentioned earlier, net4801 users will want jessie). Extract it to the TFTP root folder with

```
$ cd /var/lib/tftpboot/
$ wget http://ftp.debian.org/debian/dists/stable/main/installer-i386/current/images/netboot/netboot.tar.gz -O-|sudo tar xz
```

We need to do some additional configuration for the boot process to operate on the serial line. First, add those two lines to pxelinux.cfg/default:

```
SERIAL 0 19200 0
CONSOLE 0
```

(of course, replace 19200 with the speed of your serial line if it is different; 19200 is the default for Soekris boxes). Finally, in debian-installer/i386/boot-screens/txt.cfg edit the append line from this

```
append vga=788 initrd=debian-installer/i386/initrd.gz --- quiet
```

to this:

```
append initrd=debian-installer/i386/initrd.gz console=ttyS0,19200 --- quiet
```

(you may also remove quiet for a more verbose boot). We are now ready to boot and install. The boot process is well-documented on this Wiki (basically, press Ctrl+P to enter comBIOS, and type boot f0 at the prompt), and the installer is the same as with traditional installation media and is also well-documented (for example on the official [Debian installation manual](https://web.archive.org/web/20180818104857/https://www.debian.org/releases/stable/i386/ "https://www.debian.org/releases/stable/i386/")).

### Pre-made virtual machine

For those interested, I have compiled a virtual machine file of my PXE server as configured above in OVA format, to use in VirtualBox (and possibly other virtualisation products). The file is [here](https://web.archive.org/web/20180818104857/http://itsuki.fkraiem.org/stuff/UbuntuPXE.ova.lrz "http://itsuki.fkraiem.org/stuff/UbuntuPXE.ova.lrz") (compressed with [lrzip](https://web.archive.org/web/20180818104857/https://github.com/ckolivas/lrzip "https://github.com/ckolivas/lrzip"), 664MB, MD5 2595be397215000aa85f0fe2dcdaadd4 ).

The login name and password are both pxeboot (use sudo to get root), and SSH is listening. To change the keyboard layout (English is the default), run

```
$ sudo dpkg-reconfigure keyboard-configuration
```

Note also that in order to keep the file small, system updates have not been installed, and so it is recommended to install them before using the machine.

### After the installation

The system, including GRUB, has automatically been configured to operate over the serial line, but for some reason the kernel is not run with the correct console parameter, so the boot messages are not visible. To fix this, edit the line GRUB\_CMDLINE\_LINUX in the GRUB configuration file /etc/default/grub from this:

```
GRUB\_CMDLINE\_LINUX=""
```

to this:

```
GRUB\_CMDLINE\_LINUX="console=ttyS0,19200"

```

After editing the file, run update-grub to apply the changes.

## Installing with debootstrap

The debootstrap tool is just a bunch of shell scripts which download and install a very basic system of a Debian or Debian-based distribution into a target directory of a running system. It can be used for many tasks, but here we will use it to install a base Debian system on a CompactFlash card, which will then be moved to a Soekris box. In order to use this method, you need a machine with the following.

* A running Linux system which is able to run the binaries of the system to be installed (so for example you cannot use a 32-bit system as the installation environment for a 64-bit one). If you do not have a "real" Linux system, a Live CD or a virtual machine will also do.
* The debootstrap tool, which is available from the official repositories of many distributions, and can also be downloaded from [here](https://web.archive.org/web/20180818104857/https://packages.debian.org/stable/debootstrap "https://packages.debian.org/stable/debootstrap") in a .tar.gz archive or in a .deb package. If you want to install the testing or unstable versions of Debian, it is recommended to use the corresponding versions of debootstrap, which can be found [here](https://web.archive.org/web/20180818104857/https://packages.debian.org/testing/debootstrap "https://packages.debian.org/testing/debootstrap") and [here](https://web.archive.org/web/20180818104857/https://packages.debian.org/unstable/debootstrap "https://packages.debian.org/unstable/debootstrap") respectively.
* A CompactFlash reader.
* A good Internet connection (since the target system will be downloaded from the Debian FTP mirrors).

### Partitioning the installation media

The first step is to create the desired partitions on the target CompactFlash card. To do this, one can use a graphical partitioning tool such as GParted, or a command-line tool such as fdisk. With fdisk, the process is as follows. First connect your CF card to your system, and run fdisk -l to get its device number:

```
Disk /dev/sda: 1000.2 GB, 1000204886016 bytes
255 heads, 63 sectors/track, 121601 cylinders, total 1953525168 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk identifier: 0x7eb4805f

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1               1  1953525167   976762583+  ee  GPT
Partition 1 does not start on physical sector boundary.

Disk /dev/sdb: 3774 MB, 3774726144 bytes
117 heads, 62 sectors/track, 1016 cylinders, total 7372512 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x8aa9d8eb

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048     7170047     3584000   83  Linux
/dev/sdb2         7170048     7372511      101232   82  Linux swap / Solaris
```

Here the CF card is /dev/sdb, so run fdisk /dev/sdb to partition it. The fdisk commands we will use are d to delete the current partitions, n to create new ones, t to change partition types, p to see the current partition table, and finally w to write our changes to the card and exit fdisk. (Yes, here I just recreate the same partition table which was there before...)

```
Command (m for help): d
Partition number (1-4): 1

Command (m for help): d
Selected partition 2

Command (m for help): p

Disk /dev/sdb: 3774 MB, 3774726144 bytes
117 heads, 62 sectors/track, 1016 cylinders, total 7372512 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x8aa9d8eb

   Device Boot      Start         End      Blocks   Id  System

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p):  
Using default response p
Partition number (1-4, default 1): 
Using default value 1
First sector (2048-7372511, default 2048): 
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-7372511, default 7372511): +3500M

Command (m for help): n
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): 
Using default response p
Partition number (1-4, default 2): 
Using default value 2
First sector (7170048-7372511, default 7170048): 
Using default value 7170048
Last sector, +sectors or +size{K,M,G} (7170048-7372511, default 7372511): 
Using default value 7372511

Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): 82
Changed system type of partition 2 to 82 (Linux swap / Solaris)

Command (m for help): p

Disk /dev/sdb: 3774 MB, 3774726144 bytes
117 heads, 62 sectors/track, 1016 cylinders, total 7372512 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x8aa9d8eb

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048     7170047     3584000   83  Linux
/dev/sdb2         7170048     7372511      101232   82  Linux swap / Solaris

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

For reference, the space used by an installed i386 system after running debootstrap (so before installing a kernel) is about 300MB for a standard system, or 200MB for a minbase system (see below). The next step is to create the appropriate filesystems on the partitions (unless your partitioning tool did it for you). Linux systems will usually use the ext family of filesystems, which are created with the mke2fs command. The filesystem type is determined using the -t flag, with ext2 usually being the default. ext2 is fine for me so I do

```
# mke2fs /dev/sdb1
```

and for the swap partition:

```
# mkswap /dev/sdb2
```

We can then mount the target partition so we can install the system on it:

```
# mkdir /mnt/soekris
# mount /dev/sdb1 /mnt/soekris
```

### Running debootstrap

The basic deboostrap command is

```
# debootstrap --arch=ARCH SUITE TARGET MIRROR
```

so for example to install an i386 system of Debian "stable" in /mnt/soekris using the default Debian FTP mirror, I do

```
# debootstrap --arch=i386 stable /mnt/soekris http://ftp.debian.org/debian/
```

Of course, i386 can be replaced with amd64 to install a 64-bit system, and stable can be replaced with, testing or unstable to install the corresponding versions of Debian (as mentioned earlier, net4801 users will want jessie). It is recommended to use an FTP mirror which is close to your location; the full list of mirrors is [here](https://web.archive.org/web/20180818104857/https://www.debian.org/mirror/list "https://www.debian.org/mirror/list"). Finally, one can add --variant=minbase to install a more minimal system. On Debian-based systems (and possibly others), one can optionally install the debian-archive-keyring package before running debootstrap, in order to enable verification of the packages signatures.

### Final configuration

All that is left to do after debootstrap has finished is to install a kernel and bootloader in the target system (because debootstrap does not do it for you), and do some configuration to make the system boot on the serial line. The first step is to chroot into the target system, but before that we need to populate its /dev, /proc, and /sys directories, and copy the /etc/resolv.conf file of the current system (so the new system has the required DNS information to access the Internet to download a kernel).

```
# mount -o bind /dev /mnt/soekris/dev
# mount -t proc none /mnt/soekris/proc
# mount -t sysfs none /mnt/soekris/sys
# cp /etc/resolv.conf /mnt/soekris/etc
# chroot /mnt/soekris /bin/bash
```

A kernel can be installed from the package linux-image-686 for standard 686-class processors or linux-image-586 for the 586-class processor on the net4801 ("Jessie" only). As for the bootloader, I install GRUB 2 using the grub-pc package, but the old GRUB is also available from the package grub-legacy.

```
# apt-get update
# apt-get install linux-image-686 grub-pc
```

During the installation of GRUB, you will be prompted for the location(s) where you want to install it. Of course, install it on the CF card and not on the hard drive of your current machine! After everything is installed, we must configure GRUB to operate over the serial line (here I assume GRUB 2 was installed as above): open /etc/default/grub in a text editor such as nano (but you can also install your favourite text editor now). First, modify the GRUB\_CMDLINE\_LINUX line (which should be empty by default) to

```
GRUB\_CMDLINE\_LINUX="console=ttyS0,19200"
```

Of course replace 19200 with the speed of your serial line if it is different; 19200 is the default on Soekris boxes. You can also remove quiet from the GRUB\_CMDLINE\_LINUX\_DEFAULT line if you want a more verbose boot. Next, uncomment the GRUB\_TERMINAL line and change console to serial. Finally, add a GRUB\_SERIAL\_COMMAND line to define your serial line parameters:

```
GRUB\_SERIAL\_COMMAND="serial --unit=0 --speed=19200 --stop=1"
```

When you are done modifying the file, save your changes, exit your editor, and run update-grub to regenerate GRUB's configuration files. The next step is to create the /etc/fstab file of the target system with the appropriate filesystem information. If you only have root and swap partitions, you need something like this (you can obtain the UUIDs of your partitions with blkid or ls -l /dev/disk/by-uuid):

```
UUID=a3029b6d-0266-40ec-9bad-edcab37f258d   /       ext2    errors=remount-ro    0 1
UUID=c99a72cb-7a1e-4648-a22f-8ac3d95a8f4e   none    swap    sw                   0 0
```
Finally, you can define the hostname of the machine by modifying /etc/hostname, create a root password with passwd, and possibly also create other user accounts, or do any other desired additional configuration. When you are done, unmount everything

```
# umount /mnt/soekris/dev
# umount /mnt/soekris/proc
# umount /mnt/soekris/sys
# umount /mnt/soekris
```

Your Soekris box should now be able to boot on the CF card. When booting, you may see extraneous GRUB entries if GRUB picked up the OS of the installation system; run update-grub again after your Soekris has booted to eliminate them.
