
### From Soekris Info Wiki



Jump to: [navigation](Debian_Squeeze_On_Soekris.html#column-one), [search](Debian_Squeeze_On_Soekris.html#searchInput) 


|  |
| --- |
| Contents* [1 Installing Debian Squeeze on a Soekris Box](Debian_Squeeze_On_Soekris.html#Installing_Debian_Squeeze_on_a_Soekris_Box)
* [2 Process Overview:](Debian_Squeeze_On_Soekris.html#Process_Overview:)
* [3 Step 1: Installing a hard drive](Debian_Squeeze_On_Soekris.html#Step_1:_Installing_a_hard_drive)
* [4 Step 2: Specify a TFTP server through DHCP](Debian_Squeeze_On_Soekris.html#Step_2:_Specify_a_TFTP_server_through_DHCP)
* [5 Step 3: Seting up a TFTP server](Debian_Squeeze_On_Soekris.html#Step_3:_Seting_up_a_TFTP_server)
* [6 Step 3: The Easy (Lazy?) Way](Debian_Squeeze_On_Soekris.html#Step_3:_The_Easy_.28Lazy.3F.29_Way)
* [7 Step 4: Connecting to Your Soekris Box](Debian_Squeeze_On_Soekris.html#Step_4:_Connecting_to_Your_Soekris_Box)
* [8 Step 5: Booting the Soekris Box](Debian_Squeeze_On_Soekris.html#Step_5:_Booting_the_Soekris_Box)
* [9 Step 6: Reboot](Debian_Squeeze_On_Soekris.html#Step_6:_Reboot)
* [10 Links](Debian_Squeeze_On_Soekris.html#Links)
 |

 if (window.showTocToggle) { var tocShowText = "show"; var tocHideText = "hide"; showTocToggle(); } 
##   Installing Debian Squeeze on a Soekris Box


There are several guides in the Soekris wiki on installing Debian on a Soekris box, but none of them deal with Debian Squeeze and there are some points that they have missed here and there. The purpose of this page is to be all-inclusive. By all-inclusive, I also mean that if it's covered well elsewhere, instead of repeating it, I'll link to the page.


If you use this page and the links included, you will be able to set up a Soekris box with Debian Squeeze. The only week spot (at this time) is that I have so little experience with Windows I cannot tell you how to set up a TFTP server on a Windows system.


At the end are links to all the web pages and files you'll need to do this install. There's also an [extra link](https://web.archive.org/web/20190726151917/http://halblog.com/SqueezeOnSoekris.html "http://halblog.com/SqueezeOnSoekris.html"), to a .tgz file that's an image of Debian Squeeze (just a basic install) and a program to prepare a CF card and put this image on it so it's ready to boot. The pre-made installable image is a stock Debian Squeeze Net Install except the packages xinetd and resolvconf (to handle networking changes easily) have been installed. There are some other changes that are made during install that are enumerated in the included instructions.



##   Process Overview:


To install Debian Squeeze on a Soekris box from scracth, the general steps are:


1) Install any needed hardware on the Soekris box, such as a hard drive or inserting the CF (compact flash) card.


2) Edit your DHCP server configuration to include specifying a TFTP server.


3) Setup a TFTP server with PXE Linux.


4) Connect your Soekris box to your workstation with a serial cable (you may need a USB-to-serial cable for this).


5) Boot the Soekris box from the network so it boots PXE Linux.


6) Setup Debian Squeeze.


7) Reboot.


**Important**: There are baud rate issues when working with installing any OS to a Soekris box. Often when there's a mismatched baud rate, the screen will fill with garbage instead of readable characters, but at other times it's entirely possible a baud rate mismatch will lead to a blank screen, leaving one to wonder if something went wrong with the boot process or if it's a communications problem.


While I would like to be able to work with the baud rate set as high as possible, I've found problems with dropped characters at higher baud rates and have never been able to get a file to successfully transfer at anything higher than 19200, and that was after multiple attempts. I also found it impossible to go through the entire boot and setup process at any speed other than 19200 successfully, in spite of repeated attempts with many variations. For the purposses of this tutorial, we will use a baud rate of 19200 for everything to make it easier. Some prefer the more universal 9600 baud, but that didn't work for me.


It is extremely important to keep the baud rate the same throughout this process and there are several places where that is mentioned, so be sure to read through everything on this page and make sure you've done everything necessary to set the baud rate at every point possible.


If you find a point when the screen goes blank or things seem to hang, my experience is that it is more likely an issue with baud rate than anything else.



##   Step 1: Installing a hard drive


This won't be covered here, since there are several choices and it can be as simple as buying a CF card and slipping it into the on-board socket, or it can be more complex, like buying the mounting kit from Soekris and installing an IDE drive. There's one piece of advice I read in the Soekris wiki that is worth noting if you're using a CF card in your Soekris box: Take some heavy tape or something that will be strong enough to use to pull the card out of the socket and use that to tape to the top of the card so you can use it to pull the card out of the socket when you need to. Part of the process if you're learning how to do this could involve pulling out the card multiple times and it's much easier with some kind of handle to grip on to.



##   Step 2: Specify a TFTP server through DHCP


To load an image into a Soekris box, it has to boot from an image stored on the network. It uses TFTP to download this image, then run it once it's downloaded. For that to happen, you need two things: 1) A TFTP server to supply the image (which you'll download) and 2) A way to tell the Soekris box just where the TFTP server is on your LAN.


Unfortunately, I can't help much here, since there are so many DHCP servers out there, it's almost impossible to provide a guide for all of them. However, I can tell you that [this web page](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install") tells you how to install a DHCP server on Debian Squeeze, as well as the two lines you need to add to the configuration file to tell it where your TFTP server is.



##   Step 3: Seting up a TFTP server


You will need to pick a computer on your LAN to be the TFTP server and decide in what directory the files for this server to use will be stored. For convenience, we'll say it's in /tftpserv. Since you are likely using a different directory, just replace that directory name with the directory or path whenever I specify a file location.


Some of what you will do for a TFTP server will vary from OS to OS. However, the file locations and the directory tree needed for TFTP to allow PXE Linux to work will be the same for all OSes and the modifications you'll need to make to the configuration file will also be universal.


Here's the directory tree you'll need to create in /tftpserv (this was copied [from this page](https://web.archive.org/web/20190726151917/http://www.debian-administration.org/articles/478 "http://www.debian-administration.org/articles/478")):




```
/tftpserv/
   |-- boot.txt
   |-- debian/
   |      `-- squeeze/
   |             `-- i386/
   |                   |-- initrd.gz
   |                   `-- linux
   |-- pxelinux.0
   `-- pxelinux.cfg/
           `-- default

```

This diagram shows all the files and directories you'll need for your TFTP server for PXE Linux. Note that the 5 files you need are:




```
boot.txt
initrd.gz
linux
pxelinux.0
default

```

The first and last files are ones we'll create here. Note that I've referenced two pages for TFTP, [this one](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install") and [this one](https://web.archive.org/web/20190726151917/http://www.debian-administration.org/articles/478 "http://www.debian-administration.org/articles/478"). The latter is about Etch, not Squeeze, but if you replace Etch with Squeeze throughout, everything it says is still accurate.


You'll need to download the first three files and here are the links:


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz")


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux")


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0 "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0")


(These links are in the UK, but I'm keeping them as they are since they are the same links both web pages I cite use.)


Use the diagram to make sure you put the files in the proper directories:




```
/tftpserv/debian/squeeze/i386/initrd.gz
/tftpserv/debian/squeeze/i386/linux
/tftpserv/pxelinux.0

```

Once that's done, we need to create the two text files. The first is /tftpserv/boot.txt. Here is the content:




```
squeeze\_i386\_install
squeeze\_i386\_linux
squeeze\_i386\_expert
squeeze\_i386\_rescue

```

Just those four lines. Copy and paste them into a text editor and save the file in /tftpserv/boot.txt.


The next one is more complex. I'm using the original file on the [first link](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install") I provided, but we need to add in details to specify the console speed, which will be the baud rate for our serial connection to the Soekris box.


I cannot stress HOW IMPORTANT this is! Some sources talk about using 115200 for the speed, but then don't tell you to change it back to 19200 for booting. If this had been emphasized, or explained more clearly, I would have saved myself hours of troubleshooting work!


This is for the file /tftpserv/pxelinux.cfg/default:




```
SERIAL 0 19200
CONSOLE 0
DISPLAY boot.txt

DEFAULT squeeze\_i386\_install

LABEL squeeze\_i386\_install
      kernel debian/squeeze/i386/linux 
      append vga=normal console=ttyS0,19200,n8 initrd=debian/squeeze/i386/initrd.gz  --
LABEL squeeze\_i386\_linux
      kernel debian/squeeze/i386/linux
      append vga=normal console=ttyS0,19200,n8 initrd=debian/squeeze/i386/initrd.gz  --
LABEL squeeze\_i386\_expert
      kernel debian/squeeze/i386/linux
      append priority=low console=ttyS0,19200,n8 vga=normal initrd=debian/squeeze/i386/initrd.gz  --
LABEL squeeze\_i386\_rescue
      kernel debian/squeeze/i386/linux
      append vga=normal console=ttyS0,19200,n8 initrd=debian/squeeze/i386/initrd.gz  rescue/enable=true --

PROMPT 1
TIMEOUT 0

```

This is pretty close to the same data given in [the first page](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install") I've linked to. The differences are the first two lines are added. This should be enough, but paranoia doesn't hurt and I've also added "console=ttyS0,19200,n8" to the four append lines for the four LABEL sections. This will ensure that when we're running PXE Linux, that it'll communicate with us at a baud rate of 19200. Cut and paste the config info into a text editor and save the file as /tftpserv/pxelinux.cfg/default.


Now, you have all the directories in place and all the files in place. What you do from here on depends on your operating system. The next step is to install a TFTP server or enable one you already have.


Debian Linux: See [either this](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install") or [this page](https://web.archive.org/web/20190726151917/http://www.debian-administration.org/articles/478 "http://www.debian-administration.org/articles/478") for information on how to set up the TFTP server.


OS X: Download TFTP Server [from here](https://web.archive.org/web/20190726151917/http://ww2.unime.it/flr/tftpserver/ "http://ww2.unime.it/flr/tftpserver/"). It's not a TFTP server but it makes setting one up a breeze! After installing it on your TFTP server, run it and do 2 things: 1) Change the directory for the TFPT serer to /tftpserv or whatever location you're using, and 2) Start the TFTP server. It's that simple.


Windows: I have seen several people recommend TFTPD32 for Windows, [from here](https://web.archive.org/web/20190726151917/http://tftpd32.jounin.net/ "http://tftpd32.jounin.net/"). Since I don't use Windows and am not familiar with it, I can't help with any suggestions. You'll basically have to tell a program where your TFTP server directory is and make sure the TFTP server is running.



##   Step 3: The Easy (Lazy?) Way


If you want a quick way to set up the tftp server, I have all the files and directories set up in [one .tgz file here](https://web.archive.org/web/20190726151917/http://halblog.com/binaries/tftpboot.tgz "http://halblog.com/binaries/tftpboot.tgz"). You can download it and unpack it in your tftp server directory. That would essentially replace Step 3.



##   Step 4: Connecting to Your Soekris Box


This is a full section in itself, [best described here](https://web.archive.org/web/20190726151917/http://wiki.soekris.info/Connecting_to_the_serial_console "http://wiki.soekris.info/Connecting_to_the_serial_console"). I'm not going to duplicate a perfectly good explanation.



##   Step 5: Booting the Soekris Box


The Soekris box is set up, by default, to boot to the CF card or hard drive if they're installed. This can cause problems if there's a blank CF card or drive. (In my case, the system would just hang.) When you're set up so you can communicate with your Soekris system through a serial cable, turn it on and when you get the warning that it'll boot in 5 seconds, press CTRL-P, then when you get a promt, type "boot f0" and hit <return>. From here, the Soekris box will look on your LAN for the TFTP server, then when it finds it, you'll see a series of short lines, on some systems written over each other (for some reason, at this point, the terminal width is set to 15 characters). You don't need to read these lines. It's just going through the motions to find the right config file for PXE Linux. Eventually you'll see "boot:" and when you do, just hit <return> and it'll run the Debian install program.


In my experience, there were a couple times when the text for the install was garbled and simply rebooting gave me a connection without those issues. Once you get the Debian install screen, you can step through it and install Debian. (I also found that when I used minicom as a term program, I never got a garbled screen, but did, sometimes, when I used screen.)


**Important note on partitioning**


There are still BIOSes around that cannot handle "large" disks. Therefore, it is wise to create a primary /boot partition of about 100 - 200 MB and partition the rest of the disk as usual. Thus, a minimal worry-free disk configuration would be 




```
/boot
/
swap

```

##   Step 6: Reboot


If you've made it this far, you've made it past the hard parts! You have Debian installed now and it'll work. When you boot it, for a short while during the boot, GRUB will use a different baud rate (9600 to be exact), but you will get the login prompt and can use your Debian system. From here, the first thing I prefer to do is to set up the SSH server so I can connect to it that way and put away the serial cable.


If you want to use your new install as an image for more boxes, remember that Debian generates SSH keys at installation time and that the SSH daemon won't start up if there are no keys (see the startup scripts). So, for a generic installation image, remove the keys (you don't want machines with the same keys) and add something like this (from the OpenBSD SSH startup) to your SSH initscript:




```
if [ ! -f /etc/ssh/ssh\_host\_dsa\_key ]; then
        echo -n "ssh-keygen: generating new DSA host key... "
        if /usr/bin/ssh-keygen -q -t dsa -f /etc/ssh/ssh\_host\_dsa\_key -N *;*
then
                echo done.
        else
                echo failed.
        fi 
fi
if [ ! -f /etc/ssh/ssh\_host\_rsa\_key ]; then
        echo -n "ssh-keygen: generating new RSA host key... "
        if /usr/bin/ssh-keygen -q -t rsa -f /etc/ssh/ssh\_host\_rsa\_key -N *;*
then
                echo done.
        else
                echo failed.
        fi
fi
if [ ! -f /etc/ssh/ssh\_host\_key ]; then
        echo -n "ssh-keygen: generating new RSA1 host key... "
        if /usr/bin/ssh-keygen -q -t rsa1 -f /etc/ssh/ssh\_host\_key -N *; then*
                echo done.
        else
                echo failed.
        fi
fi

```

  

However, if you want to get rid of that pesky screen garbage, then you can edit /etc/default/grub. On the last line change 9600 to 19200 and save. Then, as root, run update-grub and it'll update the GRUB configuration so next time GRUB will use 19200 and you won't see the garbage.



##   Links


TFTP Server and PXE Linux tutorials:


[http://andys.org.uk/wiki/Guide:PXE\_network\_booting\_Debian\_install](https://web.archive.org/web/20190726151917/http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install "http://andys.org.uk/wiki/Guide:PXE_network_booting_Debian_install")


[http://www.debian-administration.org/articles/478](https://web.archive.org/web/20190726151917/http://www.debian-administration.org/articles/478 "http://www.debian-administration.org/articles/478")


Files needed:


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/initrd.gz")


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/linux")


[http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0](https://web.archive.org/web/20190726151917/http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0 "http://ftp.uk.debian.org/debian/dists/squeeze/main/installer-i386/current/images/netboot/debian-installer/i386/pxelinux.0")


All-in-one instructions and image:


[http://halblog.com/SqueezeOnSoekris.html](https://web.archive.org/web/20190726151917/http://halblog.com/SqueezeOnSoekris.html "http://halblog.com/SqueezeOnSoekris.html")





Retrieved from "[http://wiki.soekris.info/Debian\_Squeeze\_On\_Soekris](Debian_Squeeze_On_Soekris.html)"
[Categories](https://web.archive.org/web/20190726151917/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Debian](https://web.archive.org/web/20190726151917/http://wiki.soekris.info/index.php?title=Category_Debian&action=edit "Category_Debian") | [Linux](https://web.archive.org/web/20190726151917/http://wiki.soekris.info/index.php?title=Category_Linux&action=edit "Category_Linux") | [Installation](https://web.archive.org/web/20190726151917/http://wiki.soekris.info/index.php?title=Category_Installation&action=edit "Category_Installation")

 

