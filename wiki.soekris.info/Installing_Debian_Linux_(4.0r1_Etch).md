
### From Soekris Info Wiki



Jump to: [navigation](Installing_Debian_Linux_(4.0r1_Etch).html#column-one), [search](Installing_Debian_Linux_(4.0r1_Etch).html#searchInput) 


|  |
| --- |
| Contents* [1 PXEBoot Debian Netinstall to a CF Card](Installing_Debian_Linux_(4.0r1_Etch).html#PXEBoot_Debian_Netinstall_to_a_CF_Card)
	+ [1.1 External Resources](Installing_Debian_Linux_(4.0r1_Etch).html#External_Resources)
	+ [1.2 Getting Started](Installing_Debian_Linux_(4.0r1_Etch).html#Getting_Started)
		- [1.2.1 Things you'll need](Installing_Debian_Linux_(4.0r1_Etch).html#Things_you.27ll_need)
		- [1.2.2 Useful Tip #1](Installing_Debian_Linux_(4.0r1_Etch).html#Useful_Tip_.231)
		- [1.2.3 Useful Tip #2](Installing_Debian_Linux_(4.0r1_Etch).html#Useful_Tip_.232)
		- [1.2.4 Tips for Emacs users](Installing_Debian_Linux_(4.0r1_Etch).html#Tips_for_Emacs_users)
	+ [1.3 Flash Card Geometry (PNY in this example)](Installing_Debian_Linux_(4.0r1_Etch).html#Flash_Card_Geometry_.28PNY_in_this_example.29)
	+ [1.4 PXEBooting the boxes](Installing_Debian_Linux_(4.0r1_Etch).html#PXEBooting_the_boxes)
		- [1.4.1 Server setup](Installing_Debian_Linux_(4.0r1_Etch).html#Server_setup)
		- [1.4.2 BIOS Setup](Installing_Debian_Linux_(4.0r1_Etch).html#BIOS_Setup)
	+ [1.5 Running the NetInstall](Installing_Debian_Linux_(4.0r1_Etch).html#Running_the_NetInstall)
		- [1.5.1 Disk Partitions](Installing_Debian_Linux_(4.0r1_Etch).html#Disk_Partitions)
	+ [1.6 Final Setup Items](Installing_Debian_Linux_(4.0r1_Etch).html#Final_Setup_Items)
 |

 if (window.showTocToggle) { var tocShowText = "show"; var tocHideText = "hide"; showTocToggle(); } 
##   PXEBoot Debian Netinstall to a CF Card


###   External Resources


(definitive guide for setting up the PXEBoot server)
[http://www.debian-administration.org/articles/478](https://web.archive.org/web/20180818113712/http://www.debian-administration.org/articles/478 "http://www.debian-administration.org/articles/478")


(helpful but I ended up not using it, you may find it useful)
[http://lists.soekris.com/pipermail/soekris-tech/2005-July/008808.html](https://web.archive.org/web/20180818113712/http://lists.soekris.com/pipermail/soekris-tech/2005-July/008808.html "http://lists.soekris.com/pipermail/soekris-tech/2005-July/008808.html")


(for PXEBoot default command options and if you want to do an NFS mounted root partition)
[http://onesis.org/NFSroot-HOWTO.php#configpxelinux](https://web.archive.org/web/20180818113712/http://onesis.org/NFSroot-HOWTO.php#configpxelinux "http://onesis.org/NFSroot-HOWTO.php#configpxelinux")
[http://syslinux.zytor.com/faq.php](https://web.archive.org/web/20180818113712/http://syslinux.zytor.com/faq.php "http://syslinux.zytor.com/faq.php")



###   Getting Started


####   Things you'll need


* the Soekris box (or board)
* power supply (the 1.0 Amp models aren't recommended for the 4801. Soekris sent us the 1.5A models)
* null-modem cable
* USB-to-Serial adapter (if you're using a Mac or a computer without a DB-9 serial port)
* a terminal application - I see a lot of people using 'minicom' on linux, but 'screen' is my terminal app of choice. It works on linux and MacOS. Don't know if the other BSDs have this package available, but they should.
* patience and understanding


####   Useful Tip #1


Use a piece of clear tape to make a flap on the CF card. The Soekris boards don't have an eject mechanism for the CF connector, and it's hard to get them out by hand. This will save you lots of frustration if you plan on swapping the cards out frequently.



####   Useful Tip #2


Upgrade the BIOS to at least 1.30. This how-to uses 1.29 and there were problems with GRUB. Some on the Soekris tech mailing list have reported that COM BIOS 1.30 resolves this issue.



####   Tips for Emacs users


Ctrl-\ is a useful choice of "command key" to enter the minicom configuration menus or to escape screen's commands. Both minicom and screen use Ctrl-a by default, which can be very annoying to those expecting Ctrl-a to move the cursor to the beginning of the line.


mg is a tiny version of emacs for those low on system resources.



###   Flash Card Geometry (PNY in this example)


Before we really get started, let's get the geometry of the flash cards. We'll use this when we use 'dd' to copy the images to the flash cards (later on for duplication)



* LBA as reported by Soekris: 2015-16-63 = 1015MB
* CHS as reported by Debian installer: 126-109-62 = 851.508
* 2015 * 16 * 63 = 2031120 total Sectors
* 2031120 * 512 (bytes/sector) = 1039933440 Bytes
* (10399334404 / 1024)/1024 = 991.75781 = 991 MB


###   PXEBooting the boxes


####   Server setup


See [Debian installation manual, Network install, Network boot](https://web.archive.org/web/20180818113712/http://www.debian.org/distrib/netinst#netboot "http://www.debian.org/distrib/netinst#netboot")


had to apt-get install inetd
and change inetd.conf line for tftpd to udp4. Alternately, turn the tftpd-hpa daemon on in /etc/default/tftpd-hpa and run '/etc/init.d/ttfpd-hpa start'.


Tip: You will need to change the link to pxelinux.cfg after untaring netboot.tar.gz to link to the serial console configuration. 'ln -s debian-installer/i386/pxelinux.cfg.serial-9600 pxelinux.cfg' won't work! (Because pxelinux.cfg links to a directory.) First remove the existing softlink and then run ln. 


Documentation for pxelinux/syslnux can be found at [http://syslinux.zytor.com/](https://web.archive.org/web/20180818113712/http://syslinux.zytor.com/ "http://syslinux.zytor.com/").


As of soekris combios 1.33:



*  The default bios serial port speed is 19200 baud, 8 bits, no parity, no flow control. This means either changing the baud rate in the bios or changing the pxeboot config file to run at a higher baud rate. May as well change both and run at 115200 baud.


*  While the serial port can do 115200 baud, there are several points during the boot process that need to be configured for that speed for it to work. There have been reports by some people who have done extensive testing of not being able to get the full boot process to work at anything faster than 19200 baud.


*  Remember to tell the Linux kernel to use the serial port and to use the same baud rate you're using on everything else. Add "console=ttyS0,115200" to the append line for the settings for each kernel in pxelinux.cfg/default (or whatever config file you are using). Without this, when Linux is done loading, your console screen will suddenly go black because the kernel is trying to use a VGA monitor.


*  The pxelinux output is "doubled", every character is repeated twice. The bios apparently does "serial forwarding" of vga and sends to the com port, or something. See: [http://syslinux.zytor.com/archives/2004-April/003362.html](https://web.archive.org/web/20180818113712/http://syslinux.zytor.com/archives/2004-April/003362.html "http://syslinux.zytor.com/archives/2004-April/003362.html") The solution is to add a CONSOLE 0 line the pxelinux config file.


*  The pxelinux.0 outputs in a 15 character wide "display window". See the "Aside:" at the bottom of: [http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html](https://web.archive.org/web/20180818113712/http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html "http://lists.soekris.com/pipermail/soekris-tech/2007-November/013353.html") The solution is to ignore what pxelinux prints. If you want to know what to type at the boot prompt to start the Debian installer read the files in debian-installer/i386/boot-screens/ that come in Debian's netboot.tar.gz. Once you start the installer the screen output will be fine.


*  The soekris combios does not do any sort of flow control. Don't set the line speed high enough to overflow buffers or you'll be sorry. Perhaps 115200 baud is too fast should the soekris get busy? (hardware flow control would be oh-so-nice.) (This matches some user experiences of being unable to use anything faster than 19200 for a system boot and still be able to log in after boot.)


####   BIOS Setup


Press Ctrl-P as the bios boots to get the bios prompt.


Set the serial port speed. Reboot to take effect.


Set the date and time, in UTC. If the date and time are too far off ntp won't fix the time. If you install with a wonky date/time your files will all have strange timestamps.



###   Running the NetInstall


You'll need to connect to the Soekris box now via the serial port.




```
 screen -fn /dev/ttyS0 9600

```

PXEBoot from the bios prompt with "boot f0".


If everything has gone smoothly, you should be at the debian prompt, go ahead and start the process.
NOTE: At some point after the machine has booted off the PXEBoot server, you'll probably need to switch the ethernet port to your internet connection, unless you're gateway'd through your PXEBoot server (I wasn't, the PXEBoot server was an isolated machine). The install should run from here...


To diagnose install problems run a shell from the bottom of the menu and look at /var/log/syslog, dmesg, etc.



####   Disk Partitions


partition disk into 2 parts



*  / = ext2 - no journaling desired, bootable eventually mount noatime
*  /var = ext2 writeable area noexec nodev noatime


when GRUB screen appears, don't install it, install lilo (if you are running COMBIOS < 1.30)



###   Final Setup Items


* set the time (I installed ntp package)
* apt-key update - now you should be able to apt-get install any packages you like.


* remote syslog: [http://www.aboutdebian.com/syslog.htm](https://web.archive.org/web/20180818113712/http://www.aboutdebian.com/syslog.htm "http://www.aboutdebian.com/syslog.htm")


* to make the ethernet devices appear properly, edit the following file: /etc/udev/rules.d/z25\_persistent-net.rules and get rid of all entries and reboot


* edit /etc/network/interfaces to your liking
* remount fs'es read-only (root) and noatime (/var)




Retrieved from "[http://wiki.soekris.info/Installing\_Debian\_Linux\_%284.0r1\_Etch%29](https://web.archive.org/web/20180818113712/http://wiki.soekris.info/Installing_Debian_Linux_%284.0r1_Etch%29)"
[Categories](https://web.archive.org/web/20180818113712/http://wiki.soekris.info/Special:Categories "Special:Categories"): [HowTo](https://web.archive.org/web/20180818113712/http://wiki.soekris.info/Category:HowTo "Category:HowTo") | [Operating Systems](https://web.archive.org/web/20180818113712/http://wiki.soekris.info/Category:Operating_Systems "Category:Operating Systems")

 

