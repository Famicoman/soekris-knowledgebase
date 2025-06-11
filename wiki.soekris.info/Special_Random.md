
### From Soekris Info Wiki



Jump to: [navigation](./Special:Random.html#column-one), [search](./Special:Random.html#searchInput) 
[peewee@kids-these-days.org](https://web.archive.org/web/20190329210730/mailto:peewee@kids-these-days.org "mailto:peewee@kids-these-days.org")


  



These instructions describe how I installed [Ubuntu 7.04](https://web.archive.org/web/20190329210730/http://www.ubuntulinux.com/ "http://www.ubuntulinux.com/") on my 256MB [Soekris net4801](https://web.archive.org/web/20190329210730/http://www.soerkis.com/ "http://www.soerkis.com") by using debootstrap to build a CF card on a host system running Ubuntu 7.10. I installed 7.04 server on the net4801, but these steps should work for desktop or for 7.10 or you can also easily adapt them to install to a 2.5" or SATA drive.


There are [docs on the Ubuntu Wiki](https://web.archive.org/web/20190329210730/https://wiki.ubuntu.com/Soekris "https://wiki.ubuntu.com/Soekris") available on how to install Ubuntu on a Soekris via PXE but I did not feel like going through the hassle of setting PXE up to boot one system one time. I did borrow a few steps from the Ubuntu document.


I assume that you have a working knowledge of Debian like Linux systems and of Linux in general. Commands beginning with sudo are to be run on the host system while others are to be run as root inside the chroot.



*  Partition the CF card and mount the target / filesystem at /mnt/target. I use one large root partion and add some swap. There is some concern that allocating swap on a CF card will cause significant write activity and shorten the lifespan of the card. I only run the ISC dhcpd, Bind, ntpd and a couple of shell sessions so I fit into my 256MB of RAM easily and the swap is just a saftey net. If you want something different, adjust accordingly.


  





```
sudo mkdir /mnt/target
sudo cfdisk /dev/sdb # I put swap in sdb5 and the rest of the CF card into sdb1
sudo mke2fs -j /dev/sdb1
sudo mount /dev/sdb1 /mnt/target

```

  




*  Mount the installation ISO. You can use any network mirror in the next step if you don't want to download the ISO - see debootstrap(8) for more information.



```
sudo mkdir /mnt/iso
sudo mount -t iso9660 -o ro,loop=/dev/loop0 /temple/sw/linux/ubuntu-7.04-server-i386.iso /mnt/iso

```

*  Run debootstrap:



```
sudo apt-get install debootstrap
sudo debootstrap --arch i386 feisty /mnt/target file:/mnt/iso

```

*  Chroot into the target:



```
sudo chroot /mnt/target /bin/bash

```

*  Make /etc/fstab:



```
     # file system   mount point     type    options                 dump    pass
     /dev/hda1       /               ext3    defaults                0       0
     /dev/hda5       none            swap    sw                      0       0
     tmpfs           /tmp            tmpfs   size=128m,mode=1777     0       0
     proc            /proc           proc    defaults                0       0
     sys             /sys            sysfs   defaults                0       0

```

*  Mount all filesystems and run mkswap:



```
     mount /proc
     mount /sys
     ls /proc	# verficiation.  if the directory is empty, it isn't mounted.
     mkswap /dev/hda5

```

*  Configure keyboard. A keyboard isn't required for a headless box so perhaps this step can be removed.



```
     dpkg-reconfigure console-setup

```

*  Setup networking:



```
     editor /etc/network/interfaces

```

*  set hostname:



```
     echo pathos > /etc/hostname

```

*  Setup a nonroot user:



```
     adduser foo
     echo 'foo ALL=(ALL) ALL' >> /etc/sudoers
     chmod 0440 /etc/sudoers

```

*  Setup /etc/apt/sources.list, /etc/hosts and /etc/resolv.conf. See  [here](https://web.archive.org/web/20190329210730/http://wiki.soekris.info/Source_list "Source list") for a sample sources.list.


*  Create the file /etc/event.d/ttyS0:



```
     start on runlevel 2
     start on runlevel 3
     start on runlevel 4
     start on runlevel 5

```


```
     stop on runlevel 0
     stop on runlevel 1
     stop on runlevel 6

```


```
     respawn
     exec /sbin/getty -L ttyS0 9600 vt102

```

*  Edit the file /etc/initramfs-tools/modules and add the following two lines at the end of the file:



```
     ext3
     ide\_generic

```


```
     Now, you have to update your initramfs with

```


```
     update-initramfs -u

```

*  Install a kernel and configure grub. debootstrap will not install a bootloader for you. See [here](https://web.archive.org/web/20190329210730/http://wiki.soekris.info/Menu_lst "Menu lst") for a sample menu.lst that should work for feisty. Make sure that you adjust it for the kernel version installed by linux-image-generic. You may wish to look at the menu.lst from a running, recent Debian or Ubuntu system and include the comment lines used to set default options via update-grub. Note the bits that enable the serial console and set the speed.  
  
The -server kernel did not boot on my net4801.



```
     apt-get install linux-image-generic grub memtest86+

```


```
     mkdir -p /boot/grub
     cp /usr/lib/grub/i386-pc/* /boot/grub
     editor /boot/grub/menu.lst 
     exit # exit the chroot(), that is

```


```
     # Run this from outside the chroot()
     sudo grub-install --no-floppy --root-directory=/mnt/target /dev/sdb1

```

*  Install the CF card in the Soekris and boot. At this point, you should have a working but very minimal Ubuntu system. You should be able to login via the serial console as user foo with the password that you fed to adduser and from there sudo to root.


*  Do whatever you need to do to install your applications and configuration data. Personally, I use [slack](https://web.archive.org/web/20190329210730/http://www.sundell.net/~alan/projects/slack/ "http://www.sundell.net/~alan/projects/slack/").




Retrieved from "[http://wiki.soekris.info/Installing\_Ubuntu\_7.04\_Server\_via\_debootstrap](./Special:Random.html)"
[Categories](https://web.archive.org/web/20190329210730/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Operating Systems](https://web.archive.org/web/20190329210730/http://wiki.soekris.info/Category:Operating_Systems "Category:Operating Systems") | [HowTo](https://web.archive.org/web/20190329210730/http://wiki.soekris.info/Category:HowTo "Category:HowTo")

 

