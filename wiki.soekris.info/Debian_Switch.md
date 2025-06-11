
### From Soekris Info Wiki



Jump to: [navigation](Debian_Switch.html#column-one), [search](Debian_Switch.html#searchInput) 
#  Debian IPv4 Software Bridge


Only two files need changes to the basic Debian installation to run a software bridge. In the settings below, eth4 is the connection to the Internet and eth0 - eth3 are acting as a switch.


/etc/network/interfaces




```
auto lo
iface lo inet loopback
 
allow-hotplug eth4
auto eth4
iface eth4 inet dhcp

allow-hotplug eth0
iface eth0 inet manual
   pre-up   ifconfig $IFACE up
   pre-down ifconfig $IFACE down

allow-hotplug eth1
iface eth1 inet manual
   pre-up   ifconfig $IFACE up
   pre-down ifconfig $IFACE down

allow-hotplug eth2
iface eth2 inet manual
   pre-up   ifconfig $IFACE up 
   pre-down ifconfig $IFACE down

allow-hotplug eth3
iface eth3 inet manual
   pre-up   ifconfig $IFACE up
   pre-down ifconfig $IFACE down

auto br0
iface br0 inet static
  bridge\_ports eth0 eth1 eth2 eth3
  address 192.168.1.1
  broadcast 192.169.1.255
  netmask 255.255.255.0


```

/etc/rc.local




```
iptables -t nat -A POSTROUTING -o eth4 -j MASQUERADE

```



Retrieved from "[http://wiki.soekris.info/Debian\_Switch](Debian_Switch.html)"
[Category](https://web.archive.org/web/20180610231504/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Debian](https://web.archive.org/web/20180610231504/http://wiki.soekris.info/index.php?title=Category_Debian&action=edit "Category_Debian")

 

