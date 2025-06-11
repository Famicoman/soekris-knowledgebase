
### From Soekris Info Wiki



Jump to: [navigation](Installing_OpenBSD.html#column-one), [search](Installing_OpenBSD.html#searchInput) 
A simple way to install OpenBSD onto most Soekris devices, either to CF or hard drive, is by booting the device via PXE and making a standard OS installation. Another way is to install the system from another machine onto the CF with just "bsd.rd" and then move the CF to the soekris and boot from that. In either case, a standard install usually works best. 


On 5.6, the following sets add up to approximately 227 MB of space:




```
      [**X**] bsd           [**X**] etc56.tgz     [ ] xbase56.tgz    [ ] xserve56.tgz
      [**X**] bsd.rd        [ ] comp56.tgz    [ ] xetc56.tgz   
      [ ] bsd.mp        [**X**] man56.tgz     [ ] xshare56.tgz
      [**X**] base56.tgz    [ ] game56.tgz    [ ] xfont56.tgz

```

Those five sets have approximately the following disk utilization before any customization:




```
 42 MB  /
182 MB  /usr
  3 MB  /var

```

  




##  Installing OpenBSD via PXE


Installing by PXE doesn't require an existing OpenBSD host, just to have DHCP and TFTP services available. This method is equally applicable to installations on a hard drive or a larger CF (as of 4.2, a 512MB CF gives space for a very usable installation with base, xbase, manual pages and some installed packages; to install the compiler set you would want to start with 1GB).


This method uses the normal bsd.rd installation kernel, just like the CD installation on a normal machine.


Requirements:



* workstation with serial port (or USB/serial adapter) and null modem cable
* DHCP server, configured to support PXE clients
* network access to the distribution file sets for OpenBSD i386 via HTTP or FTP (local or remote)
* TFTP server holding "pxeboot" (the pxe boot loader) and "bsd.rd" (the install kernel) from the distribution file set


Since the description of this method is kept up-to-date in the [OpenBSD Networking FAQ](https://web.archive.org/web/20190204160448/http://www.openbsd.org/faq/faq6.html#PXE "http://www.openbsd.org/faq/faq6.html#PXE") and [pxeboot(8) manual page](https://web.archive.org/web/20190204160448/http://www.openbsd.org/cgi-bin/man.cgi?query=pxeboot&sektion=8&arch=i386 "http://www.openbsd.org/cgi-bin/man.cgi?query=pxeboot&sektion=8&arch=i386"), only the parts relevant to installation on a Soekris device need to be discussed here.




```
Connect the network on Eth0
Interrupt the comBIOS boot sequence with Ctrl-P
> boot f0
...
>> OpenBSD/i386 PXEBOOT 1.00
boot> stty com0 19200
boot> set tty com0
boot> bsd.rd

```

Proceed as normal; towards the end of installation you'll be asked whether to configure the serial console, and which speed to use. Set this to match the console speed set in comBIOS.


If you can't type anything at the boot loader prompt, perhaps your null modem cable only connects RxD/TxD/GND, not the modem control lines. In that case, try a different cable or a newer OS (4.4 or newer, where the boot loader was taught to handle serial ports directly rather than via BIOS).



##   Reducing storage capacity requirements


For special cases, such as net4526/4826 (with its fixed-capacity soldered flash) or with CF cards too small for a normal installation, frameworks are available which help with reducing disk space requirements. These can't exactly be regarded as OpenBSD; more accurately described they result in an OpenBSD derivative.


All such frameworks use a similar method to install only wanted files, but two very differenet methods are used to actually install them: installation into a normal filesystem, and building a custom ramdisk kernel.


[flashdist](https://web.archive.org/web/20190204160448/http://www.nmedia.net/~chris/soekris/ "http://www.nmedia.net/~chris/soekris/") (written by Chris Cappuccio), described in an [onlamp article](https://web.archive.org/web/20190204160448/http://www.onlamp.com/pub/a/bsd/2004/03/11/Big_Scary_Daemons.html "http://www.onlamp.com/pub/a/bsd/2004/03/11/Big_Scary_Daemons.html") uses the first method. flashdist also pre-configures the system to work with the filesystems mounted in read-only mode (to reduce risk of corruption and problems with unclean shutdown) - this can also be done with a normal OpenBSD installation. This method can be used with either a GENERIC or a custom kernel.


The second method involves preparing a kernel containing an image of the root filesystem which is loaded into ramdisk (commonly: "a ramdisk kernel"). Since userland+kernel are combined in one file, this makes it simple to keep old versions around and reduces the chance of unpredictable behaviour that might rarely be seen during an online upgrade. The most familiar example of a ramdisk kernel is the bsd.rd installation kernel, but a custom one can be created. [flashboot](https://web.archive.org/web/20190204160448/http://www.mindrot.org/projects/flashboot/ "http://www.mindrot.org/projects/flashboot/") makes this easier; ([precompiled kernels and dd images](https://web.archive.org/web/20190204160448/http://tilde.se/flashboot/ "http://tilde.se/flashboot/") are also available.


It's possible to install kernels or gzipped tar files created by these methods with PXE/bsd.rd as discussed above. To do this, place them in a directory on a local FTP server and list them in index.txt.



##  Problems with some CF cards


On some systems (mostly earlier 4801 where the DMA interrupt lines are not connected to the IDE controller), you might see messages like this:




```
pciide0:0:0: bus-master DMA error: missing interrupt, status=0x20

```

With some CF cards the reset command used for the automatic fall back to PIO mode is not honoured, so you must disable DMA manually. At the boot loader, "boot -c" (or "boot bsd.rd -c", etc), and you can disable DMA modes with these commands:




```
ukc> change wd
 42 wd* at wdc*|pciide* channel -1 flags 0x0
change [n] y
channel [-1] ? 
flags [0] ? 0x0ff0
 42 wd* changed
 42 wd* at wdc*|pciide* channel -1 flags 0xff0
ukc> quit

```

You can make these changes permanent to a kernel on disk with config(8).





Retrieved from "[http://wiki.soekris.info/Installing\_OpenBSD](Installing_OpenBSD.html)"
[Categories](https://web.archive.org/web/20190204160448/http://wiki.soekris.info/Special:Categories "Special:Categories"): [HowTo](https://web.archive.org/web/20190204160448/http://wiki.soekris.info/Category:HowTo "Category:HowTo") | [Operating Systems](https://web.archive.org/web/20190204160448/http://wiki.soekris.info/Category:Operating_Systems "Category:Operating Systems")

 

