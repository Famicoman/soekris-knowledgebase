# Installing FreeBSD

There are two ways to install [FreeBSD](https://web.archive.org/web/20180610231544/http://www.freebsd.org/ "http://www.freebsd.org") on a Soekris box. The Soekris comBIOS doesn't support booting from CDROM drives, but you can prepare your disk image on another system, or you can install directly to the Soekris box over the LAN using the PXE network boot procedure.

Note: FreeBSD 6.3R requires comBIOS version 1.32i on the net5501, or the boot will hang when first attempting DMA.

## Compact flash

* [NanoBSD](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/articles/nanobsd/howto.html "http://www.freebsd.org/doc/en_US.ISO8859-1/articles/nanobsd/howto.html") is a shell script that creates a bootable compact flash image from the FreeBSD sources. NanoBSD gives you control of which features you add to save space. The resulting image is targeted for half of the CF card, allowing alternating in place upgrades to the other half. It was written by Soekris-Tech regular Poul-Henning Kamp.
* [Ultradesic.com (mirror)](https://web.archive.org/web/20180610231544/http://webfolder.wirelessleiden.nl/www.ultradesic.com/index06ef.html?section=125 "http://webfolder.wirelessleiden.nl/www.ultradesic.com/index06ef.html?section=125") has a detailed tutorial on an alternative way to create and install the CF image.
* [BarryODonovan.com](https://web.archive.org/web/20180610231544/http://www.barryodonovan.com/index.php/2009/12/08/freebsd-on-soekris-net4801 "http://www.barryodonovan.com/index.php/2009/12/08/freebsd-on-soekris-net4801") has a howto on installing FreeBSD to a CF card using [VirtualBox](https://web.archive.org/web/20180610231544/http://www.virtualbox.org/ "http://www.virtualbox.org/") and some necessary post-installation changes for it to boot on a Soekris net4801-48 box.
*  [More on VirtualBox](https://web.archive.org/web/20180610231544/http://wiki.soekris.info/More_on_VirtualBox "More on VirtualBox")  and installing FreeBSD.

## Net boot

FreeBSD supports installing over the network using PXE net boot functionality of the Soekris BIOS. 

*  The [FreeBSD handbook](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/index.html "http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/index.html") is the standard reference. It doesn't cover the PXE install procedure, but does describe [booting a diskless client](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/network-diskless.html "http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/network-diskless.html"), and [setting up the serial console](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/install-advanced.html "http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/install-advanced.html").
* [Installing FreeBSD 9.1 on Soekris net6501 via PXE](https://web.archive.org/web/20180610231544/http://pivotallabs.com/installing-freebsd-9-1-on-soekris-net6501-via-pxe/ "http://pivotallabs.com/installing-freebsd-9-1-on-soekris-net6501-via-pxe/") gives a succinct HOWTO for installing 9.1 with PXE net boot.
* [Installing FreeBSD 7.x or 8.x via serial console and PXE](https://web.archive.org/web/20180610231544/http://jdc.koitsu.org/freebsd/pxeboot_serial_install.html "http://jdc.koitsu.org/freebsd/pxeboot_serial_install.html") gives an excellent HOWTO for installing over the network. Includes workaround for bug that prevents PXE booting in 7.x.
* [Ultradesic NFS Root Guide (mirror)](https://web.archive.org/web/20180610231544/http://webfolder.wirelessleiden.nl/www.ultradesic.com/index9fcd.html?section=161 "http://webfolder.wirelessleiden.nl/www.ultradesic.com/index9fcd.html?section=161") covers installing FreeBSD 6.x over the network.
* [Webweaving FreeBSD on Soekris net boot guide](https://web.archive.org/web/20180610231544/http://www.webweaving.org/wlg/ "http://www.webweaving.org/wlg/") covers installing FreeBSD 5.x over the network.

## Kernel customization

The FreeBSD GENERIC kernel should boot your Soekris, however there are several Soekris kernel optimizations that can be made. See the [handbook](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/kernelconfig.html "http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/kernelconfig.html") for general kernel customization instructions. The following Soekris and AMD related options exist (from /usr/src/sys/i386/conf/NOTES):

*  CPU\_SOEKRIS enables support www.soekris.com hardware
*  CPU\_ELAN enables support for AMDs ElanSC520 CPU
	+  CPU\_ELAN\_PPS enables precision timestamp code
	+  CPU\_ELAN\_XTAL sets the clock crystal frequency in Hz
*  CPU\_GEODE is for the SC1100 Geode embedded processor - This option is necessary because the i8254 timecounter is toast.

### net5501

Start with the GENERIC kernel configuration file. Add "options CPU\_SOEKRIS" and "options CPU\_GEODE". You should also comment out or delete all device entries that aren't on the net5501 and that you're not likely to add. You will likely want to remove all RAID controllers, SCSI and FireWire related devices. You can remove all wired and wireless network interfaces, except miibus and vr, unless you have added NICs. You can even remove the USB uhci to save a few more bytes. "KVM" devices can also go since there is only a serial console, so remove atkbdc, atkbd, psm, vga, splash and sc. Be sure to keep sio. Note that if you keep umass (in USB section), you'll need scbus and da from the SCSI section.

### net6501

The **net6501** works with FreeBSD in either 32-bit mode (**i386**) as other Soekris machines do, but also in 64-bit mode: the **amd64** 64-bit build of FreeBSD works, but not with the standard GENERIC kernel (at least not with FreeBSD-9.0 or FreeBSD-9.1). You need to build a special kernel configuration in /usr/src/sys/amd64/conf that contains the line "**device mptable**" and then build a kernel with that option enabled... the resulting kernel will boot on the net6501 in 64-bit mode without any problem.

You can find a tarball with FreeBSD 9.0-RELEASE for the net6501, containing the required kernel files (**boot/***), the **NET6501** kernel configuration, and the **boot.config** file needed to boot from serial console at [http://sivit.rax.org/NET6501.tgz](https://web.archive.org/web/20180610231544/http://sivit.rax.org/NET6501.tgz "http://sivit.rax.org/NET6501.tgz").

[FreeBSD10 NanoBSD on a Soekris net6501](https://web.archive.org/web/20180610231544/http://neilwebber.com/notes/2014/03/18/installing-freebsd10-nanobsd-on-a-soekris-net6501/ "http://neilwebber.com/notes/2014/03/18/installing-freebsd10-nanobsd-on-a-soekris-net6501/") describes installing NanoBSD 10 on a 6501 using a VirtualBox build environment and USB target.

### Patch for PATA hard disk errors on FreeBSD 7.x and 8.x

The net5501 supports SATA and PATA disks: you just need to order the right cable or mounting kit. With FreeBSD, SATA disks work normally, but PATA hard disks are a problem due to the cable type being mis-detected. So after installing FreeBSD on a PATA disk, you will probably see a message like:

```
       kernel: ad0: WARNING - READ\_DMA UDMA ICRC error (retrying request) LBA=121272839
```

This is because FreeBSD's ATA subsystem auto-detects the maximum drive speed, and gets it wrong! It sets UDMA100, which is slightly too fast, giving intermittent errors. If this happens to you, the first thing to do is to slow things down temporarily:-

```
       atacontrol mode ad0 udma66
```

This lasts until the next reboot. Now you can safely [patch the ATA driver](https://web.archive.org/web/20180610231544/http://www.freebsd.org/cgi/query-pr.cgi?pr=kern/123980 "http://www.freebsd.org/cgi/query-pr.cgi?pr=kern/123980") using Martin Johnson's unofficial patch.
The file to patch is **/usr/src/sys/dev/ata/ata-all.c** and [the patch file is here](https://web.archive.org/web/20180610231544/http://www.net42.co.uk/downloads/ata-all.c.patch "http://www.net42.co.uk/downloads/ata-all.c.patch").

Rebuild the kernel using [*make buildkernel && make installkernel*](https://web.archive.org/web/20180610231544/http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/kernelconfig-building.html "http://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/kernelconfig-building.html"). Finally, edit **/boot/loader.conf** and add the line: **hw.ata.ata\_dma\_limit="4"**, and reboot.

### FreeBSD 8.2 PATA Disk Fix

This problem should be solved by an official fix from FreeBSD 8.2 onwards. You should be able to edit **/boot/device.hints** and add the line: **hint.ata.0.mode="UDMA66"** (assuming a PATA hard disk on IDE channel 0), then reboot.

FreeBSD 8.1 users might be able to use the code from FreeBSD 8.2 by taking [Alexander Motin's official patches](https://web.archive.org/web/20180610231544/http://www.freebsd.org/cgi/query-pr.cgi?pr=123980 "http://www.freebsd.org/cgi/query-pr.cgi?pr=123980"). The files affected are /usr/src/share/man/man4/ata.4, /usr/src/sys/dev/ata/ata-all.c and /usr/src/sys/dev/ata/ata-all.h.
