
### From Soekris Info Wiki



Jump to: [navigation](Installing_CentOS_4.4.html#column-one), [search](Installing_CentOS_4.4.html#searchInput) 
Distribution kernel is only working with net55xx.


Using Tftpd32 for windows ([http://tftpd32.jounin.net](https://web.archive.org/web/20180610231539/http://tftpd32.jounin.net/ "http://tftpd32.jounin.net"))
Download CentOS 4.4 ServerCD
Copy initrd.img, pxelinux.0, vmlinuz from isolinux folder on the cd.


Make a pxelinux.cfg folder in the pxeboot folder.
create a file called default with this contents:




```

SERIAL 0 19200 0

DEFAULT install

#

LABEL install
        KERNEL vmlinuz
        MENU LABEL ^CentOS 4.4 Rescue via HTTP
        APPEND initrd=initrd.img root=/dev/VolGroup00/LogVol00 ramdisk\_size=10000 text install ip=dhcp ks=http://YOURIP/ks.cfg console=ttyS0,19200n81

PROMPT 1
TIMEOUT 0

```

Install a webserver, i used apache and copied the RPMS folder content to the html folder.
Setup the tftpd program to be dhcp and tftp server, remember to assing your PC a static IP.
Use a terminal klient flow control none or pxe boot loader will fail. Windows own HyperTerminal has been tested.


Everything is set just connect your net55xx to your ethernet on your enjoy the centos install. remember to use textmode.





Retrieved from "[http://wiki.soekris.info/Installing\_CentOS\_4.4](Installing_CentOS_4.4.html)"
[Categories](https://web.archive.org/web/20180610231539/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Operating Systems](https://web.archive.org/web/20180610231539/http://wiki.soekris.info/Category_Operating_Systems "Category_Operating Systems") | [HowTo](https://web.archive.org/web/20180610231539/http://wiki.soekris.info/Category_HowTo "Category_HowTo")

 

