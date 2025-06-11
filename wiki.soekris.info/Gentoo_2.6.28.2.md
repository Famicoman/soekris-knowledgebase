
### From Soekris Info Wiki



Jump to: [navigation](Gentoo_2.6.28.2.html#column-one), [search](Gentoo_2.6.28.2.html#searchInput) 
My soekris 4801 is an wlan access point and router for pppoe, installed on hardisk.


For updates i am using a chroot on a faster machine with rsync before and
after updating. Another way for updates is using [[distcc](https://web.archive.org/web/20180610231509/http://www.gentoo.org/doc/en/cross-compiling-distcc.xml "http://www.gentoo.org/doc/en/cross-compiling-distcc.xml")].


The Kernel configuration is [here](https://web.archive.org/web/20180610231509/http://wiki.soekris.info/Kernel_2.6.28.2_vanilla_on_Gentoo "Kernel 2.6.28.2 vanilla on Gentoo")


/boot/grub/menu.lst for serial console




```
default 0
timeout 3
serial --unit=0 --speed=9600 --word=8 --parity=no --stop=1
terminal serial
title Gentoo Linux
root (hd0,1)
kernel /boot/vmlinuz root=/dev/hdb2 console=ttyS0,9600n8

```

  

/etc/make.conf




```
CFLAGS="-O2 -mtune=i686 -pipe"
CXXFLAGS="${CFLAGS}"
CHOST="i586-pc-linux-gnu"
MAKEOPTS="-j2"
SYNC="rsync://rsync5.de.gentoo.org/gentoo-portage"
USE="-X -gtk -gnome -kde -alsa -qt3 -qt4 imagemagick ssl bzip2 readline python apache2 lm\_sensors mmx mysql ncurses verbose "

```

/etc/inittab for serial console




```
id:3:initdefault:
si::sysinit:/sbin/rc sysinit
rc::bootwait:/sbin/rc boot
l0:0:wait:/sbin/rc shutdown 
l1:S1:wait:/sbin/rc single
l2:2:wait:/sbin/rc nonetwork
l3:3:wait:/sbin/rc default
l4:4:wait:/sbin/rc default
l5:5:wait:/sbin/rc default
l6:6:wait:/sbin/rc reboot
# SERIAL CONSOLES
s0:12345:respawn:/sbin/agetty 9600 ttyS0 vt100
x:a:once:/etc/X11/startDM.sh

```

  

/etc/conf.d/net




```
dns\_domain\_lo="domain.local"
mode\_ath0="master"
essid\_ath0="soekris4801"
channel\_ath0="5"
config\_ath0=( "null" )
config\_eth0=( "null" )
config\_br0="10.0.0.1/24"
dns\_servers\_br0="208.67.222.222 156.154.70.1 208.67.220.220"
dns\_search\_br0="domain.local"
bridge\_br0="eth0 ath0"
RC\_NEED\_br0="net.eth0 net.ath0"

```

/etc/conf.d/hostapd




```
INTERFACES="ath0 eth0 br0"
CONFIGS="/etc/hostapd/hostapd.conf"
OPTIONS=""

```

/etc/hostapd/hostapd.conf




```
interface=ath0
bridge=br0
driver=madwifi
logger\_syslog=-1
logger\_syslog\_level=2
logger\_stdout=-1
logger\_stdout\_level=2
debug=0
dump\_file=/tmp/hostapd.dump
ctrl\_interface=/var/run/hostapd
ctrl\_interface\_group=0
ssid=soekris4801
hw\_mode=g
channel=5
beacon\_int=100
dtim\_period=2
max\_num\_sta=255
rts\_threshold=2347
fragm\_threshold=2346
macaddr\_acl=0
auth\_algs=3
ignore\_broadcast\_ssid=0
wme\_enabled=1
wme\_ac\_bk\_cwmin=4
wme\_ac\_bk\_cwmax=10
wme\_ac\_bk\_aifs=7
wme\_ac\_bk\_txop\_limit=0
wme\_ac\_bk\_acm=0
wme\_ac\_be\_aifs=3
wme\_ac\_be\_cwmin=4
wme\_ac\_be\_cwmax=10
wme\_ac\_be\_txop\_limit=0
wme\_ac\_be\_acm=0
wme\_ac\_vi\_aifs=2
wme\_ac\_vi\_cwmin=3
wme\_ac\_vi\_cwmax=4
wme\_ac\_vi\_txop\_limit=94
wme\_ac\_vi\_acm=0
wme\_ac\_vo\_aifs=2
wme\_ac\_vo\_cwmin=2
wme\_ac\_vo\_cwmax=3
wme\_ac\_vo\_txop\_limit=47
wme\_ac\_vo\_acm=0
eapol\_key\_index\_workaround=0
eap\_server=0
own\_ip\_addr=127.0.0.1
wpa=1
wpa\_passphrase= *** PASSPHRASE ***
wpa\_key\_mgmt=WPA-PSK WPA-EAP
wpa\_pairwise=TKIP CCMP
wpa\_group\_rekey=600
wpa\_gmk\_rekey=86400

```

My chroot environment is located on a 3GHz 32bit Intel machine at /soekris\_chroot/.


Every time before updating i am using rsync to assign local updates to the chroot. Delete the "-n" switch if it looks good.


First part: Transfer local changes from soekris box to chroot environment. Attention: "--delete" is dangerous ;)




```
rsync --delete -Onalvz --numeric-id --exclude 'sys/' --exclude 'dev/' --exclude 'root/' \
--exclude 'proc/' --exclude 'usr/portage/' --exclude 'usr/src' --exclude \
'var/run/' --exclude 'var/log' --exclude 'tmp/' --exclude 'var/lib/init.d/' \
--exclude 'etc/chrony/chrony.drift' --exclude 'etc/adjtime' --exclude \
'etc/resolv.conf' root@soekris:/ /soekris\_chroot/

```

  

Second part: Using this script to work in chroot, update everything and transfer updates to soekris.




```
#!/bin/bash
mount -o bind /dev /soekris\_chroot/dev &&\
mount -t proc none /soekris\_chroot/proc &&\
mount -o bind /dev/pts /soekris\_chroot/dev/pts &&\
chroot /soekris\_chroot || exit 1
umount /soekris\_chroot/dev/pts
umount /soekris\_chroot/dev
umount /soekris\_chroot/proc
echo "rsync should be done next"
echo "rsync --delete  -Onalvz  --numeric-id --exclude 'sys/' --exclude 'dev/' --exclude \
'root/' --exclude 'proc/' --exclude 'usr/portage/' --exclude 'usr/src' \
--exclude 'var/run/' --exclude 'var/log' --exclude 'tmp/' --exclude \
'var/lib/init.d/' --exclude 'etc/chrony/chrony.drift' \
--exclude 'etc/adjtime' --exclude 'etc/resolv.conf' /soekris\_chroot/ \
root@soekris:/"

```



Retrieved from "[http://wiki.soekris.info/Gentoo\_2.6.28.2](Gentoo_2.6.28.2.html)"
[Categories](https://web.archive.org/web/20180610231509/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Linux](https://web.archive.org/web/20180610231509/http://wiki.soekris.info/index.php?title=Category_Linux&action=edit "Category_Linux") | [Installation](https://web.archive.org/web/20180610231509/http://wiki.soekris.info/index.php?title=Category_Installation&action=edit "Category_Installation") | [Gentoo](https://web.archive.org/web/20180610231509/http://wiki.soekris.info/index.php?title=Category_Gentoo&action=edit "Category_Gentoo")

 

