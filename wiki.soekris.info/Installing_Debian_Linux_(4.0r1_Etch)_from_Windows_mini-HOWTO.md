#(Installing Debian Linux (4.0r1 Etch) from Windows mini HOWTO

This is a short guide to help you to get started with the Debian network install on the Soekirs. Witch can be a little tricky. 

|  |
| --- |
| Contents* [1 What you need](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #What_you_need)
* [2 Prepare everything](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #Prepare_everything)
	+ [2.1 Set up the debian net insall](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #Set_up_the_debian_net_insall)
	+ [2.2 Set up the Soekris Box](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #Set_up_the_Soekris_Box)
* [3 Start the install of Debian linux](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #Start_the_install_of_Debian_linux)
* [4 Tuneup the serial port (after install)](Installing_Debian_Linux_(4.0r1_Etch)_from_Windows_mini-HOWTO.md #Tuneup_the_serial_port_.28after_install.29)
 |

## What you need

* The last realase from Debian Linux netboot install PXE image from debian website, normaly a file called netboot.tar.gz
* A TFTP and DHCP server, for Window use, I recommend Tftpd 32 by Ph. Jounin.
* The standard prelinux.0 dosen’t work on the soekeris net4801, you nead a patched version, downloadable at [http://www.ultradesic.com/pub/pxelinux.0.gz](https://web.archive.org/web/20180812042306/http://www.ultradesic.com/pub/pxelinux.0.gz "http://www.ultradesic.com/pub/pxelinux.0.gz").
* A terminal emulator like HyperTerminal.
* A null-modem cable
* An Ethernet cable.

## Prepare everything

### Set up the debian net insall

* Download the netboot install file “netboot.tar.gz” form www.debian.org and unpack it to your hard drive, for example D:\pxelinux.
* The PXE linux kernel given with this archive doesn’t work on the Soekris board so you need to replace with the patched version. Both in D:\netboot\pxelinux.0 and D:\pxelinux\debian-installer\i386\pxelinux.0.
* The installer from the archive is expecting to found a video device and a keyboard, so you have to tell him to use the serial interface instead. For that replace the file D:\pxelinux\prelinux.cfg\default by D:\pxelinux\debian-installer\i386\pxelinux.cfg.serial-9600\default.
* Install Tftp 32 on your PC and configure it as follow :


[![Tftpd32 setup](https://web.archive.org/web/20180812042306im_/http://wiki.soekris.info/images/Tftpd32.jpg)](https://web.archive.org/web/20180812042306/http://wiki.soekris.info/Image:Tftpd32.jpg "Tftpd32 setup")

### Set up the Soekris Box

* Connect the Soekris Box to your PC using a null-modem cable.
* Connect the Soekris Box to your PC using an Ethernet cable.
* Open HyperTerminal and set up it as follow:
	+ 19200 baud.
	+ 8 bits data
	+ No parity bit
	+ 1 stop bit
	+ Flow control : None
* Power on the Soekris box.
* As the system start up you should see the BIOS running inside the HyperTerminal window. Press CTRL+P to enter monitoring mode.
* As the Debian setup use 9600 baud, we will tune the BIOS to fit it. Type “set ConBaud = 9600 <ENTER>”.
* Type “reboot <ENTER”>
* Change the setting of HyperTerminal to fit 9600 baud.
* I recommend you also to change the HyperTerminal font to “Terminal” in order to have a good view of the installer prompt.

## Start the install of Debian linux

* Press CTRL+P while Soekris BIOS running to enter monitoring mode again.
* Type “boot F0 <ENTER>” to make the Soekris boot from network. It should find the file prelinux.0 provided by the TFTP/DHCP server and boot it.
* As the grub shell appear, just hit ENTER.
* When the first question of the installer appear, normally about language, you should disconnect the Ethernet cable from the PC and connect it to a network providing internet access (school/work/home network). The Debian installer will made a new DHCP discover and then get the software’s packages through internet.
* Follow the instruction provided by the Debian installer. All you need now is some patience, some coffee and to press ENTER.

## Tuneup the serial port (after install)

As you will maybe discover, print out from program like man are very slow trought the serial line at 9600 baud. Let's make in faster by using 57600 bauds.

Edit /etc/inittab and change the following line :

```
T0:23:respawn:/sbin/getty -L ttyS0 9600 vt102
```

to:


```
T0:23:respawn:/sbin/getty -L ttyS0 57600 vt102
```

Edit /boot/grub/menu.lst. 

Change this line :

```
serial --unit=0 --speed=9600 --word=8 --parity=no –stop=1
```

to:

```
serial --unit=0 --speed=57600 --word=8 --parity=no –stop=1
```

Add this option to all your kernel command line:

```
console=ttyS0,57600n8
```

like this, for examle:

```
title           Linux, Kernel 2.6.23
root            (hd0,0)
kernel          /boot/bzImage-2.6.23 root=/dev/hda1 console=ttyS0,57600n8
initrd          /boot/initrd.img-2.6.23
savedefault
```

* Reboot
* Will bios is running enter monitor mode by pressing “CTRL + P”.
* Type “set ConSpeed=57600 <ENTER>”.
* Type “show <ENTER>” to ensure that the change have been made.
* Type “reboot <ENTER>”
* At this time you should change your terminal configuration to 57600 baud.
* Now you should seen your Linux booting, with faster printouts.
