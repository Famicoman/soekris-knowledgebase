# Installing from an existing image

This guide details how to install an existing Linux image to a Soekris board. In my case, I copied a net-installed image of Debian 5.0 running under VirtualBox to a [Soekris 5501](Net5501.md "Net5501") with a 320GB Seagate HD.

|  |
| --- |
| Contents* [1 Prepare the image](Installing_from_an_existing_image.md#Prepare_the_image)
	+ [1.1 Modify GRUB](Installing_from_an_existing_image.md#Modify_GRUB)
	+ [1.2 Modify Linux settings](Installing_from_an_existing_image.md#Modify_Linux_settings)
		- [1.2.1 Change the fstab](Installing_from_an_existing_image.md#Change_the_fstab)
		- [1.2.2 Blow out udev persistent net rules (recommended)](Installing_from_an_existing_image.md#Blow_out_udev_persistent_net_rules_.28recommended.29)
		- [1.2.3 Add a serial console (recommended)](Installing_from_an_existing_image.md#Add_a_serial_console_.28recommended.29)
	+ [1.3 Convert the image](Installing_from_an_existing_image.md#Convert_the_image)
	+ [1.4 Copy the image](Installing_from_an_existing_image.md#Copy_the_image)
* [2 Update The Firmware](Installing_from_an_existing_image.md#Update_The_Firmware)
* [3 Connect via Serial](Installing_from_an_existing_image.md#Connect_via_Serial)
 |

## Prepare the image

The first step is to prepare the existing image for copying to a Soekris board. The first couple of steps will need to be done to the live image, before converting and copying it. If you know what you're doing, they can be skipped and done after the image is copied (ie, modifying the GRUB settings using 'e' in the loader) but that can get tricky.

### Modify GRUB

You will need to make a few changes to the GRUB bootloader in order to properly boot Linux from a harddrive in a Soekris board.

Your /boot/grub/menu.lst will need to look something like this:

```
#boot the first image by default, with 5 seconds to modify, if you change your mind
default 0
timeout 5

#The first two lines setup GRUB to work on the serial console. Change the speed settings as you like
serial --unit=0 --speed=115200 --word=8 --parity=no --stop=1
terminal --timeout=3 serial console

title           Debian GNU/Linux, kernel 2.6.26-2-686
root            (hd0,0)
#NB that root=/dev/hdb1 - The SATA on the Soekris board is actually a PATA bridge! Again, change the speed settings as you like
kernel          /boot/vmlinuz-2.6.26-2-686 root=/dev/hdb1 quiet ro console=tty0 console=ttyS0,115200n8
initrd          /boot/initrd.img-2.6.26-2-686
```

Set the speed to whatever you're comfortable using. I don't like waiting, so I used 115200n8. A more comfortable speed such as 9600n8 or 19200n8 should work just fine.

###  Modify Linux settings

####  Change the fstab

The Filesystem Table, residing in /etc/fstab will need to be changed to the proper settings:

```
proc            /proc           proc    defaults        0       0 
/dev/hdb1       /               ext3    errors=remount-ro 0       1
/dev/hdb5       none            swap    sw              0       0
#/dev/hdc        /media/cdrom0   udf,iso9660 user,noauto     0       0
/dev/fd0        /media/floppy0  auto    rw,user,noauto  0       0 
```

Oddly enough, this doesn't seem to be strictly necessary. I had improper settings for my root filesystem, and it still booted. I would still recommend configuring this, though.

####  Blow out udev persistent net rules (recommended)

udev remembers the PCI bus and MAC addresses of all your network controllers, so that it can assign the name interface name (eg, eth0) to the same device each time. Unfortunately, when copying images around, the PCI bus addresses change, and the new devices get assigned new interface names. This can prevent your network from coming up automatically, and if you're relying on ssh access to configure the box from here on, will severely cramp your style.

Fortunately, this is easily remedied by deleting udev's list of remembered network interfaces

```
rm /etc/udev/rules.d/70-persistent-net.rules

```

When the image boots next time, udev will regenerate the persistent rules list with the new PCI bus addresses. NB that if you reboot the virtual image again after removing this file, you will need to redo this step before copying the image to the Soekris board.

#### Add a serial console (recommended)

To add a console on the serial port, so that you can login there, you will need to modify the /etc/inittab file, and add the following lines:

```
s0:23:respawn:/sbin/getty -L 115200 ttyS0 vt102
s1:23:respawn:/sbin/getty -L 115200 ttyS1 vt102
```

Again, adjust your com speed (115200 in this case) and terminal type (vt102 for me) to suit your needs.

### Convert the image

If your image is not already a raw image, it will need to be converted. A VirtualBox VDI image can be converted using VirtualBox's built-in (but sadly undocumented) tools

```
VBoxManage internalcommands converttoraw <source vdi> <dest raw file>
```

###  Copy the image

It's best to do a bitwise copy of the entire image - partition table, MBR and all, using dd

```
dd if=<path to your image> of=<path to hd you want to copy to, eg /dev/sdb> bs=64k

```

The 'bs' term can be tweaked, possibly for better speed. 64k yielded a throughput of 15-25MB/s for me, over a USB connection. Not specifying 'bs' yielded a throughput of 2-3MB/s.

##  Update The Firmware

Older versions of the Soekris firmware can cause issues with attempting to boot using GRUB. Details on how to update the firmware can be found in the section called [Updating Bios](Updating_Bios.md "Updating Bios").

##  Connect via Serial

See [Connecting to the serial console](Connecting_to_the_serial_console.md "Connecting to the serial console")
