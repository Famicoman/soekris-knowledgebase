# Installing Debian Linux 5.0

|  |
| --- |
| Contents* [1 Installing Debian 5.0 on a Soekris](Installing_Debian_Linux_5.0.md #Installing_Debian_5.0_on_a_Soekris)
* [2 Outline](Installing_Debian_Linux_5.0.md #Outline)
* [3 Get the files](Installing_Debian_Linux_5.0.md #Get_the_files)
* [4 Serial Console](Installing_Debian_Linux_5.0.md #Serial_Console)
* [5 Set up a dhcp server](Installing_Debian_Linux_5.0.md #Set_up_a_dhcp_server)
* [6 Set up a TFTP server](Installing_Debian_Linux_5.0.md #Set_up_a_TFTP_server)
* [7 Modify installer to work with a serial console](Installing_Debian_Linux_5.0.md #Modify_installer_to_work_with_a_serial_console)
* [8 Install!](Installing_Debian_Linux_5.0.md #Install.21)
	+ [8.1 grub legacy](Installing_Debian_Linux_5.0.md #grub_legacy)
	+ [8.2 Grub2](Installing_Debian_Linux_5.0.md #Grub2)
 |

## Installing Debian 5.0 on a Soekris

This guide will give you a few tips for installing debian 5.0 on your Soekris device. I won't walk you through every detail of installing debian, there are lots of guides for that. I ran all of the commands below as root. I should direct you to use sudo for every command but instead I'll say "be careful".

See also [Installing Debian Linux (4.0r1 Etch)](Installing_Debian_Linux_%284.0r1_Etch%29.md "Installing Debian Linux (4.0r1 Etch)") for more tips.

## Outline

You can follow this general procedure:

1. Update your soekris firmware. Instructions on this are on the soekris site. I'll admit cheating and using hyperterm on a 10y old laptop for this (booo)

2. Get the netboot files for debian. You don't need to download the whole distribution unless your soekris won't have internet access.

3. Get a serial console working with your soekris. Quick info on that is 19200,8N1

3. Set up a PXE boot environment. This includes a DHCP server with a custom configuration and a tftp server.

5. Modify the netboot files a little to work with a serial console. Debian used to come with this but it's gone now.

6. Boot and install normally


7. Modify new installation to boot properly and support serial console.

## Get the files

At the time of the writing the file was found here:
[[1]](https://web.archive.org/web/20190311150329/http://ftp.ca.debian.org/debian/dists/stable/main/installer-i386/current/images/netboot/netboot.tar.gz "http://ftp.ca.debian.org/debian/dists/stable/main/installer-i386/current/images/netboot/netboot.tar.gz"). Check on your favorite mirror under debian/dists/5.0/main/installer-i386/current/images/netboot/ for netboot.tar.gz .
If you plug your soekris into a network that can access the internet this is all you need, the rest of the installation can be completed over http or ftp (recommended)

## Serial Console

I used minicom. If you're not sure what to do, try setting the serial port device to /dev/ttyS0. My Soekris worked with 19200bps, 8N1 out of the box. 

Once you're able to talk with the soekris consider using a higher baud rate, like 1152000. Set the baud rate in the soekris bios and reboot, then set the baud rate in your terminal program. You will need to change the default baud rate of 19200 given in the examples below to your chosen baud rate. (Remember, though, that changing the default baud rate in the BIOS and on your term program will NOT change the baud rate during booting, so if you change the baud rate, either change it back before booting PXE Linux or be sure you've altered the baud rate settings in PXE Linux as well as in your boot loader settings once Linux has been installed. Or just leave change back to 19200 before booting PXE Linux or booting a new install.)

It wouldn't hurt to set the bios date and time at this point. You probably want to use UTC time.

## Set up a dhcp server

If you're using a wireless router with built in dhcp you're going to want to turn that off for a while. 

For a dhcp server I installed the dhcp3-server package in ubuntu (should be similar for debian): 

```
# apt-get install dhcp3-server
```

To make a long story short, here is what my configuration looked like assuming my gateway was 192.168.1.1 and my netmask was going to be 255.255.255.0. Adjust this to work with your gateway and to point to a working dns server if your gateway doesn't host one: 

/etc/dhcp3/dhcpd.conf:

```
ddns-update-style none;
option domain-name "mynet.ca";
option domain-name-servers 192.168.1.1;
default-lease-time 600;
max-lease-time 7200;
log-facility local7;
allow booting;
allow bootp;

subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.200 192.168.1.253;
  option broadcast-address 192.168.1.255;
  option routers 192.168.1.1;
  option domain-name-servers 192.168.1.1;
}

host krissy {
#   tftp client hardware address
    hardware ethernet 00:00:24:C6:33:20;
    filename "pxelinux.0";
}
```

Note that you'll need to find out what the hardware address is on your device. I believe you can get this by booting the device, typing ctrl-p when prompted (within 5 seconds!) and either printing the boot prom settings or typing boot F0. With boot F0 it'll try to PXE boot and hopefully show you the MAC address in the process.

You may have to edit /etc/default/dhcp3-server to specify which interface to use if your machine has more than one.

Disable any other DHCP servers on your network for now and then fire this one up:

```
# /etc/init.d/dhcp3-server start
```

## Set up a TFTP server

There seems to be a wide selection of tftp servers with some fascinating incompatibilities. The one that worked well for me was the ported openbsd tftp server tfptd-hpa: 

```
# apt-get install tftpd-hpa
```

Also ubuntu doesn't come with inetd by default. This is strange, but true. Add it like this:

```
# apt-get install openbsd-inetd
```

then make sure a line appears in your inetd.conf like so:

/etc/inetd.conf

```
tftp           dgram   udp     wait    root  /usr/sbin/in.tftpd /usr/sbin/in.tftpd -s /var/lib/tftpboot
```

And start it:

```
# /etc/init.d/openbsd-inetd start

```

This particular configuration has you put files in /var/lib/tftpboot. Untar the netboot.tar.gz you downloaded in the first step here:

```
# cd /var/lib/tftpboot
# tar -zxf /home/whoever/Desktop/netboot.tar.gz

```

## Modify installer to work with a serial console

Now we're going to quickly hack this to work with a serial console. Edit the txt.cfg file found here:

/var/lib/tftpboot/debian-installer/i386/boot-screens/txt.cfg

```
default install
label install
       menu label ^Install
       menu default
       kernel debian-installer/i386/linux
       append vga=normal initrd=debian-installer/i386/initrd.gz -- console=ttyS0,19200 earlyprint=serial,ttyS0,19200
```

Consider similar editing in the adtxt.cfg file in that same directory if you wish to use
expert mode, recovery mode ,etc. In that same directory then edit the syslinux.cfg file, adding 2 lines near the top:

/var/lib/tftpboot/debian-installer/i386/boot-screens/syslinux.cfg

```
# D-I config version 1.0
CONSOLE 0
SERIAL 0 19200 0
include debian-installer/i386/boot-screens/menu.cfg
default debian-installer/i386/boot-screens/vesamenu.c32
prompt 0
timeout 0
```

## Install!

Now we're ready to install.

Hook up your trusty Soekris to your network using the first available port, connect the serial cable and power cable and press ctrl-p when told you've 5 seconds to do so. At the prompt:

```
boot F0
```

This should quickly download the debian bootloader (grub I think). There will be no output until you get a prompt that looks a bit like:

```
boot:
```

Type "install", or the label of one of other boot entries you modified, and hit enter. 

Proceed through installation as usual, but before rebooting choose the option **"execute a shell."** You need to make some modifications to the newly installed debian in order to enable the serial console after reboot.

```
#mount /dev/hda1 /mnt
#mount --bind /proc /mnt/proc
#chroot /mnt
```

we need to enable the modules ext3 and ide\_generic earlier in the boot process. either use nano or type something like:

```
#echo -e "\next3\nide\_generic" >> /etc/initramfs-tools/modules
```

then:

```
#update-initramfs -u
```

edit /etc/securetty and /etc/inittab to make sure that the serial console is setup.

Then edit the bootloader configuration to add serial suport.

### grub legacy

### Grub2

```
#mount --bind /dev /mnt/dev
#chroot /mnt
```

nano /etc/default/grub and add:

```
GRUB\_CMDLINE\_LINUX='console=tty0 console=ttyS0,19200n8 acpi=off'

GRUB\_TERMINAL=serial
GRUB\_SERIAL\_COMMAND="serial --speed=19200 --unit=0 --word=8 --parity=no --stop=1"
```

then:

```
#update-grub
```
