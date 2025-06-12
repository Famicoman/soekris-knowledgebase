# Known bugs

## net5501

### Bugs

*  The SATA port doesn't work:

This is fixed in comBIOS 1.32d


*  The USB port doesn't work at 2.0 speeds:

This is fixed in comBIOS 1.32d


*  It won't boot off my hard drive after a soft reboot:

This is fixed in comBIOS 1.32h


*  IDE DMA issues (can manifest as kernels refusing to boot with some drives)

This is fixed in comBIOS 1.32i


### Limitations

*  No hardware flow control on the serial interface
*  Incompatibilities with pxelinux. See "Aside:" at bottom of [http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html](https://web.archive.org/web/20180610231604/http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html "http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html")
*  Lack of documentation. (Leads to problems like: [http://syslinux.zytor.com/archives/2004-April/003362.html](https://web.archive.org/web/20180610231604/http://syslinux.zytor.com/archives/2004-April/003362.html "http://syslinux.zytor.com/archives/2004-April/003362.html") Solution is a pxelinux.cfg 'CONSOLE 0' line.)

Categories: [Net5501](Category_Net5501.md "Category_Net5501")
