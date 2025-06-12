# Running the memtest86 diagnostic

The memtest86+ diagnostic tests memory and certain aspects of the CPU.

This page describes how to run memtest86+ from a pxeboot environment, so that the soekris drive/etc. need not be modified, so that if the drive won't boot you can still run diagnostics, so that you can run diagnostics on a machine without a drive, etc. Once you've a bootloader and an OS installed there is usually a way to tell the bootloader to load memtest86+ from the OS's filesystem and pxeboot is not needed.

These are quick notes to get you started and avoid the gotcha's. It could use a lot more internal wiki and external links. Be sure to read through it once before doing anything.

Note that this document assumes you're running debian, but you can easily run something else just by getting the debian tftp boot files (pxelinux.0 and the like) and use your own tftpd server binary.

Begin by setting up a pxeboot environment, as described elsewhere on this wiki when installing Debian.

Your /etc/dhcpd.conf should contain lines like:

```
        server-name "mytftpserver";
        next-server mytftpserver;
        filename "pxelinux.0";
```

Obtain a memtest86+ binary. Version 4.0 or later may be required because it has a fix for the Geode LX processors. If you can't find a binary or don't want to compile one on Debian Lenny you can:

Enable the backports.org repository; adding a line to /etc/apt/sources.list, etc.

```
mkdir foo
cd foo
aptitude -t lenny-backports download memtest86+ ;# See note below for better option
ar x memtest86+\_4.00-2~bpo50+1\_i386.deb
tar -xzf data.tar.gz boot/memtest86+.bin
cp -a boot/memtest86+.bin /var/lib/tftpboot/memtest86+.bin.foo ; # see note below
```

Note that you need a 486 binary, so if you're not running a 486 arch the aptitude command will retrieve the wrong binary. Instead of the aptitude command you may wish to retrieve the .deb directly from (under the pool directory) a debian archive with http or ftp. If you do that you don't need to enable the backports repository, or even be running Debian, so it's probably a smarter way to go in any case.

Note that syslinux/pxelinux reserves the .bin extension for something to do with ISOs. Your memtest86+ binary \_cannot\_ end in `.bin`. If you \_do\_ have `.bin` at the end of the filename when you try to boot you will get an infinite number of lines containing nothing but `0004`.

Your /var/lib/tftpboot/pxelinux.cfg/default file should contain:

```
# Hacked up for memtest86+ version 4.00
# Disable the video console output, it confuses the soekris bios.
CONSOLE 0
SERIAL 0 19200 0

default memtest86
label memtest86
#       menu label ^m memtest86+-v4.00
#       menu default
        kernel memtest86+.bin.foo
        append console=ttyS0,19200n8

prompt 1
timeout 0
```

Note that this assumes that your baud rate is set to 19200bps in your soekris bios. Change this if required.

Be sure that your soekris bios has:

```
biosboot=f0 80 81 ff
```

or something similar so that you pxeboot first.
Pxeboot must also be enabled in the bios.
