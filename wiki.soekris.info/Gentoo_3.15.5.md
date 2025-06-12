# Gentoo 3.15.5

|  |
| --- |
| Contents* [1 TODO: THIS ARTICLE IS NOT FINISHED YET!](Gentoo_3.15.5.md#TODO:_THIS_ARTICLE_IS_NOT_FINISHED_YET.21)
* [2 Summary](Gentoo_3.15.5.md#Summary)
* [3 Usage](Gentoo_3.15.5.md#Usage)
* [4 Installation](Gentoo_3.15.5.md#Installation)
* [5 Gentoo Configuration](Gentoo_3.15.5.md#Gentoo_Configuration)
* [6 Kernel](Gentoo_3.15.5.md#Kernel)
* [7 GRUB2](Gentoo_3.15.5.md#GRUB2)
* [8 Networking](Gentoo_3.15.5.md#Networking)
 |

## TODO: THIS ARTICLE IS NOT FINISHED YET!

*  Feel free to add things!

## Summary

*  This document describes how Gentoo was configured on a Soekris NET6501-70.
*  As the whole system is installed with testing (~amd64 Arch), you should know, what you are doing!
*  In my opinion, its pretty stable and I haven't encountered any special problems.
*  I've chosen Gentoo, because it doesn't have any fixed releases but rolling releases.
*  As Gentoo means compiling the whole system, you can very specific adjust every package for your needs.

## Usage

*  My usage with Gentoo is primary for home routing:

```
 eth0: LAN (connected to a gigabit switch)
 eth1: VOIP (connected directly to a voip phone)
 eth2: IPTV (connected directly to a iptv reciever) 
 eth3: WAN (connected directly to a vdsl modem)
```

*  I am also running some small services for my LAN: ddclient, dnsmasq, hostapd, miniupnpd, nfs, samba, vnstatd

## Installation

*  I don't want to show you here a detailed installation procedure, as you can do it, as described in the official Gentoo docs.
*  You can find this documentation here: [Gentoo Installation Handbook](https://web.archive.org/web/20180610231515/http://www.gentoo.org/doc/en/handbook/handbook-amd64.xml "http://www.gentoo.org/doc/en/handbook/handbook-amd64.xml")
*  As you can't directly boot an ISO with the Soekris, I would recommend to use [SystemRescueCd](https://web.archive.org/web/20180610231515/http://www.sysresccd.org/SystemRescueCd_Homepage "http://www.sysresccd.org/SystemRescueCd_Homepage").
*  SystemRescueCd is a Gentoo-based LiveCD, which can be used, to chroot into your new system.
*  SystemRescueCd includes a PXE boot server. Just launch it from another PC, so you Soekris can directly PXE boot from this one.
*  Proceed, as the Gentoo Installation Handbook describes.

## Gentoo Configuration

*  This is my /etc/portage/make.conf:

```
 # === Apps ===
 CURL\_SSL="openssl"
 GRUB\_PLATFORMS="pc"
 PYTHON\_TARGETS="python2\_7 python3\_2"
 # === CCACHE ===
 CCACHE\_DIR="/var/tmp/ccache"
 CCACHE\_SIZE="2G"
 # === Compile ===
 CFLAGS="-march=atom -O3 -mmmx -msse -msse2 -msse3 -mssse3 -mcx16 -mmovbe -msahf -pipe -fomit-frame-pointer -mfpmath=sse"
 CHOST="x86\_64-pc-linux-gnu"
 CXXFLAGS="${CFLAGS}"
 MAKEOPTS="-j3"
 LDFLAGS="-Wl,-O1 -Wl,--as-needed -Wl,--sort-common -Wl,-z,now"
 # === Portage ===
 ACCEPT\_LICENSE="Oracle-BCLA-JavaSE"
 ACCEPT\_KEYWORDS="~amd64"
 EMERGE\_DEFAULT\_OPTS="--autounmask=n --quiet-build=n"
 GENTOO\_MIRRORS="[ftp://ftp.halifax.rwth-aachen.de/gentoo/](https://web.archive.org/web/20180610231515/ftp://ftp.halifax.rwth-aachen.de/gentoo/ "ftp://ftp.halifax.rwth-aachen.de/gentoo/")"
 FEATURES="ccache parallel-fetch"
 I\_KNOW\_WHAT\_I\_AM\_DOING="yes"
 PORTAGE\_COMPRESS="gzip"
 PORTAGE\_COMPRESS\_FLAGS="-f9"
 # PORTAGE\_RSYNC\_EXTRA\_OPTS="--delete-before --delete-excluded --exclude-from=/etc/portage/rsync\_excludes --stats"
 PORTDIR\_OVERLAY="/usr/local/portage"
 SYNC="rsync://rsync.de.gentoo.org/gentoo-portage"
 USE="-* bzip2 cracklib crypt curl cxx fontconfig ftp gd gmp gnutls iconv idn ipv6 javascript jpeg lm\_sensors lzma mmx mysql mysqli ncurses nls nntp nptl offensive pam png readline samba slang spell sse2 ssl svg symlink tcpd threads truetype unicode usb vim-syntax xml zlib"
 # === Language ===
 ENABLE\_UNICODE="utf-8"
 LINGUAS="de"
```

## Kernel

*  My curent kernel config can be found here: [Gentoo Sources 3.15.5](https://web.archive.org/web/20180610231515/http://wiki.soekris.info/Kernel_3.15.5_gentoo_sources "Kernel 3.15.5 gentoo sources")
*  It's stripped down to a minimal version, so its only supports that, what a soekris really has. Additionally, ath9k for Atheros is enabled. You can of course modify the options.
*  Main purpose is home routing and small lan services.

## GRUB2

*  My GRUB2 won't boot, if ConMute = Enabled is NOT set in comBIOS!
*  Change --speed to your specified speed in comBIOS!
*  /etc/default/grub2:

```
 GRUB\_CMDLINE\_LINUX="console=ttyS0,115200n8 nf\_conntrack.nf\_conntrack\_helper=0 rootfstype=ext4"
 GRUB\_DISABLE\_LINUX\_UUID=true
 GRUB\_DISABLE\_OS\_PROBER=true
 GRUB\_DISABLE\_RECOVERY=true
 GRUB\_DISTRIBUTOR=Gentoo
 GRUB\_HIDDEN\_TIMEOUT=5
 GRUB\_HIDDEN\_TIMEOUT\_QUIET=false
 GRUB\_SERIAL\_COMMAND="serial --parity=no --port=0 --speed=115200 --stop=1 --unit=0 --word=8"
 GRUB\_TERMINAL=console
 GRUB\_HIDDEN\_TIMEOUT=0
 GRUB\_HIDDEN\_TIMEOUT\_QUIET=true
 GRUB\_TIMEOUT=10
```

## Networking

*  This configuration shows my setup from eth0 to eth3.
*  Additionally I've enabled IPv6, which is brought by [[Hurricane Electric Internet Services](https://web.archive.org/web/20180610231515/https://www.he.net/ "https://www.he.net/")]
*  It's an IPv6 tunnel broker. You can get a free account with your own subnet. You just have to [[register](https://web.archive.org/web/20180610231515/http://www.tunnelbroker.net/ "http://www.tunnelbroker.net/")]
*  MTU > 1500 seems to make problems with serving PXE booting. Because of that, it's commented out.
*  This is my /etc/conf.d/net

```
 # Modules
 modules="iproute2"
 modules\_wlan0="!iwconfig !wpa\_supplicant"
 # Intel 82574L Gigabit Ethernet Controller #1 (LAN)
 config\_eth0="192.168.ZZ.1/24
              2001:XXX:YYYY:ZZ::1/64"
 # mtu\_eth0="9200"
 # Intel 82574L Gigabit Ethernet Controller #2 (VOIP, C610A-IP)
 config\_eth1="192.168.ZZ.1/24
            2001:XXX:YYYY:ZZ::1/64"
 # mtu\_eth1="9200"
 # Intel 82574L Gigabit Ethernet Controller #3 (IPTV, MR303)
 config\_eth2="192.168.ZZZ.1/24
            2001:XXX:YYYY:ZZZ::1/64"
 # mtu\_eth2="9200"
 # Intel 82574L Gigabit Ethernet Controller #4 (WAN)
 config\_eth3="192.168.ZZZ.1/24
              2001:XXX:YYYY:ZZZ::1/64"
 # mtu\_eth3="9200"
 config\_eth3\_7="null"
 vlans\_eth3="7"
 # T-Com Speedport 221 (VDSL50)
 config\_ppp0="ppp"
 link\_ppp0="eth3.7"
 plugins\_ppp0="pppoe"
 username\_ppp0="XXXXXXXXXXXXYYYYYYYYYYYY#ZZZZ@t-online.de"
 # Hurricane Electric IPv6 Tunnel Broker
 config\_tun0="2001:XXX:YYYY:ZZZZ::2/64"
 iptunnel\_tun0="mode sit remote 216.XX.YY.ZZ local 127.0.0.1 ttl 255"
 routes\_tun0="default via 2001:XXX:YYYY:ZZZ::1"
 # JJPLUS ExpressRange 9 Mini PCI Express Module (WLAN)
 carrier\_timeout\_wlan0="0"
 config\_wlan0="192.168.ZZ.1/24
               2001:XXX:YYYY:ZZ::1/64"
 # mtu\_wlan0="2270"
 # Deps
 depend\_ppp0() {
     need net.eth3
 }
```
