# Installing Ubuntu 10.04 server via PXE

## Introduction

This guide shows how to install an Ubuntu 10.04 32Bit server system on a soekris net5501-70 with an Compact Flash (CF) as storage device.

NOTE: The following steps where tested with a Ubuntu10.04 Desktop 32Bit host system.

## Serial connection to net5501-70

### Install minicom

```
apt-get install minicom
```

Use these configurations for /etc/minicom/minirc.dfl:

```
pu port             /dev/ttyUSB0
pu baudrate         19200
pu bits             8
pu parity           N
pu stopbits         1
pu rtscts           No
pu zauto            C
```

NOTE:

*  The default baud rate of the net5501 is: 19200
*  Soekris doesn't support any kind of Flow Control.
*  I used a USB to Serial adapter (/dev/ttyUSB). If you use a COM slot adapt it to /dev/ttyS?

### Connect to net5501

```
minicom
```

## comBIOS update

NOTE: Without an update it is probable that the comBIOS will not recognize newer Compact Flash cards.

Now that we have a connection, we want to update the comBIOS.

Download newest comBIOS: [http://soekris.com/downloads.md](https://web.archive.org/web/20180812043529/http://soekris.com/downloads.md "http://soekris.com/downloads.md")

Look here for an update how to: [http://wiki.soekris.info/Updating\_Bios](https://web.archive.org/web/20180812043529/http://wiki.soekris.info/Updating_Bios "http://wiki.soekris.info/Updating_Bios")

As we have just configured "minicom", I recommend to use it here, too.

## DHCP server

### Install DHCP server

```
apt-get install dhcp3-server
```

### Config DHCP server

Append the following lines to /etc/dhcp3/dhcpd.conf and adapt addresses to your needs:

```
subnet 192.168.0.0 netmask 255.255.255.0 {
 range 192.168.0.200 192.168.0.253;
 option broadcast-address 192.168.0.255;
 option routers 192.168.0.1;
 option domain-name-servers 192.168.0.1;
}  
```

```
host soekris {
 # tftp client/soekris hardware address
 hardware ethernet ??:??:??:??:??:??;
 filename "pxelinux.0";
}        
```

In order to get the soekris MAC address (hardware address), you first have to make sure that soekris is able to boot from PXE.
Take a look [[here](Installing_Ubuntu_10.04_server_via_PXE.md#Soekris_and_PXE "Installing_Ubuntu_10.04_server_via_PXE.md#Soekris_and_PXE")].

Now, start your soekris box and you will get something like this:


```
CLIENT MAC ADDR: ?? ?? ?? ?? ?? ??
DHCP..
```

NOTE: 

Make sure that you have a connected ethernet wire, otherwise you will not see the MAC address and get this message:

```
PXE-E61: Media test failure, check cable
```

If your soekris box doesn't start automatically the DHCP client, type this:

```
boot F0
```

F0 stands for "PXE".

Define your NIC in /etc/default/dhcp3-server

```
INTERFACES=eth?
```

If you dont't specifiy the NIC here, you cannot re-/start the server.

### Start dhcp server

```
/etc/init.d/dhcp3-server start
```

## TFTP server

### Install TFTP server

```
apt-get install tftpd-hpa
```

You don't have to configure the server.

By default, this server uses /var/lib/tftpboot/ to keep the up-/downloadable data.

NOTE: 

The tftp-hpa server seams to have connection problems when working in standalone modus. I could only connect once to the server. After that the server doesn't accept no more connections!? Even a server restart doesn't help, but a system reboot does. Buggy thing...

A workaround is to use the "inetd" server which starts the TFTP server when it receives a connection request.

## INETD server

### Install INETD server

```
apt-get install openbsd-inetd      
```

### Config INETD server

Append this line to /etc/inetd.conf

```
tftp           dgram   udp     wait    root  /usr/sbin/in.tftpd /usr/sbin/in.tftpd -s /var/lib/tftpboot 
```

### Start INETD server

```
/etc/init.d/openbsd-inetd start
```

## netboot.tar.gz

This file contains the Ubuntu "installer". 

### Download file

```
wget [http://archive.ubuntu.com/ubuntu/dists/lucid/main/installer-i386/current/images/netboot/netboot.tar.gz](https://web.archive.org/web/20180812043529/http://archive.ubuntu.com/ubuntu/dists/lucid/main/installer-i386/current/images/netboot/netboot.tar.gz "http://archive.ubuntu.com/ubuntu/dists/lucid/main/installer-i386/current/images/netboot/netboot.tar.gz")
```

### Extract file

```
tar xzfv netboot.tar.gz -C /var/lib/tftpboot/
```

### Config installer

var/lib/tftpboot/pxelinux.cfg/default should look like this:

```
CONSOLE 0
SERIAL 0 19200 0
include ubuntu-installer/i386/boot-screens/menu.cfg
default ubuntu-installer/i386/boot-screens/vesamenu.c32
prompt 0
timeout 0
```

You have to add the first 2 lines in order to get a working serial connection during the installation process.

/var/lib/tftpboot/ubuntu-installer/i386/boot-screens/text.cfg should look like this:

```
default install
 label install
   menu label ^Install
   menu default
   kernel ubuntu-installer/i386/linux
   append tasks=server vga=normal initrd=ubuntu-installer/i386/initrd.gz -- console=ttyS0,19200 noplymouth
 label cli
   menu label ^Command-line install
   kernel ubuntu-installer/i386/linux
   append tasks=standard pkgsel/language-pack-patterns= pkgsel/install-language-support=false vga=normal initrd=ubuntu-installer/i386/initrd.gz
```

NOTE: 

*  "tasks=server" in the "append" line tells the installer to install a Ubuntu server. Use "tasksel --list-tasks" to get other options for tasks=...
*  Dont't forget to append "console=ttyS0,19200"

## Soekris and PXE

These 2 comBIOS parameters must be set as follows, otherwise the net5501 won't boot from PXE.

```
PCIROMS = Enabled                                                             
PXEBoot = Enabled 
```

Type "show" in comBIOS prompt to see all comBIOS settings.

### Boot from PXE

Type the following when soekris starts up

```
boot F0

```

Now, at the "boot:" prompt type:

```
install
```

That's the name of the "label" in /var/lib/tftpboot/ubuntu-installer/i386/boot-screens/text.cfg

NOTE: 

*  At the beginning of the installation it is likely that you won't see any output for a while (~ 10-15 min.).

But this will normally change and the system download will start.

*  After the installation the OS doesn't start automatically from CF.

To start it manually, type:

```
boot 80        
```

NOTE: 80 = 1. device

This of course only works if the CF is the Primary Master device. 
To verify that, watch the net5501 boot screen (Pri Mas):

```
0512 Mbyte Memory                        CPU Geode LX 500 Mhz                  
                                                                              
Pri Mas  SanDisk CompactFlash 200x       LBA Xlt 971-128-63  3917 Mbyte
```

AND in the comBIOS settings check this option by entering "show":

```
FLASH = Primary
```

### Workaround to let Soekris automatically boot from CF

Set the following option after entering the comBIOS monitoring mode (press CTRL+P at boot time)

```
set BootDrive=80 80 F0
```

*  80 = 1. device
*  81 = 2. device
*  F0 = PXE

The default configuration is: 

```
BootDrive=80 81 F0 FF
```

That's it for the installation.

## Scripts

Purpose of these scripts

These scripts are intended to run on a Soekris net5501-70 (512 MB RAM) embedded system 
with a 4 GB Compact Flash (CF) as storage device. 

Because NAND CF has "only" a write endurance of ~1,000,000 cycles per location, it 
is a good idea to swap highly used parts of the OS to a ramdisk/tmpfs. In this case /var.
Like this we can increase the CF lifetime and mount i.e. the root partition in read only.

As a little gadget the soekris GPIO error LED is activated when a script error occurs.

*  Fast blinking error LED means: Fatal error, please investigate.
*  Slow blinking error LED means:

varbak.sh couldn't use tmpfs for data sync. It used CF instead. This is not good for the CF lifetime.
This is only a warning and will be deactivate automatically by varbak.sh as soon as it has enough free 
RAM again to use a tmpfs.

Here is the link to GitHub.com, where my scripts are hosted: 

[[Ubuntu10.04\_server\_on\_soekris\_net5501-70\_CF](https://web.archive.org/web/20180812043529/https://github.com/sambaTux/Ubuntu10.04_server_on_soekris_net5501-70_CF "https://github.com/sambaTux/Ubuntu10.04_server_on_soekris_net5501-70_CF")]

Maybe these scripts are useful to somebody.
