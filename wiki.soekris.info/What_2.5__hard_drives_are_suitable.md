
### From Soekris Info Wiki



Jump to: [navigation](What_2.5"_hard_drives_are_suitable.html#column-one), [search](What_2.5"_hard_drives_are_suitable.html#searchInput) 


|  |
| --- |
| Contents* [1 Overview](What_2.5"_hard_drives_are_suitable.html#Overview)
	+ [1.1 Duty Cycle Considerations](What_2.5"_hard_drives_are_suitable.html#Duty_Cycle_Considerations)
	+ [1.2 Block Size Considerations](What_2.5"_hard_drives_are_suitable.html#Block_Size_Considerations)
	+ [1.3 Spindown is Bad](What_2.5"_hard_drives_are_suitable.html#Spindown_is_Bad)
	+ [1.4 Heat](What_2.5"_hard_drives_are_suitable.html#Heat)
* [2 Particular drives](What_2.5"_hard_drives_are_suitable.html#Particular_drives)
	+ [2.1 Solid State Drives](What_2.5"_hard_drives_are_suitable.html#Solid_State_Drives)
	+ [2.2 Hitachi Drives](What_2.5"_hard_drives_are_suitable.html#Hitachi_Drives)
	+ [2.3 Fujitsu Drives](What_2.5"_hard_drives_are_suitable.html#Fujitsu_Drives)
 |

 if (window.showTocToggle) { var tocShowText = "show"; var tocHideText = "hide"; showTocToggle(); } 
##   Overview


Soekris sells mounting kits for 2.5" hard drives, which include a mounting bracket, standoffs and a short signal cable. net4801 supports PATA. net5501 supports PATA or SATA (this is connected by a bridge to PATA; you can't use both ports and a CF; it is possible to use one PATA and one SATA drive together with a [workaround](https://web.archive.org/web/20180610231725/http://wiki.soekris.info/Master/Slave "Master/Slave")). For DMA support on net5501, use comBIOS 1.32i or newer, and a recent OS release.


This wiki has some [Hard drive mounting](https://web.archive.org/web/20180610231725/http://wiki.soekris.info/Hard_drive_mounting "Hard drive mounting") instructions.



###   Duty Cycle Considerations


If you're going to run 24*7, then you probably want to be running a drive designed for that purpose. Most laptop drives spend much of their lives either switched off or spun down to save the laptop battery and are not rated for continuous operation. Ordinary laptop drives may fail prematurely if you use them for a server application.


If you'd like to purchase a high duty cycle drive, it might be necessary to look for a storage specialist; they are often not carried by general-purpose PC hardware suppliers.



###   Block Size Considerations


Historically block size has been fixed at 512B but SSD drives often, as well as some newer magnetic drives, have larger block sizes.
For write performance it is as important to ensure that partition boundarys are block-size aligned as it is to use a file system with block/fragment sizes that are a multiple of (or the same as) the hardware block size. A mistake in this area will more than halve the sustained write speed of the drive. Unlike spinning drives the internal block size is often published by the SSD drive manufacturer.


Newer spinning magnetic media drives are beginning to be available with a (putative) 4K block size as well and partition alignment is also a factor with these drives.



###   Spindown is Bad


It's usually possible to configure laptop drives to not spin down. This should make for greater stability and more consistent response. Power consumption will increase, but still be very low. So it seems like a good configuration option for a low-power Soekris server. Applications that do not require regular disk access, e.g. routers and firewalls, may benefit less (but don't forget about logging).


On OpenBSD this is done with the apmset option to [atactl(8)](https://web.archive.org/web/20180610231725/http://www.openbsd.org/cgi-bin/man.cgi?query=atactl "http://www.openbsd.org/cgi-bin/man.cgi?query=atactl")


FreeBSD provides the atacontrol(8) command. Syntax is 'atacontrol spindown $SECONDS $DRIVE' where DRIVE is either ad0 or ad1, and SECONDS is the idle delay. If SECONDS = 0, the drive will never spin down.



###   Heat


In warm environments, you may need to fit a small fan inside the case to keep the hard drive cool. **High drive temperatures greatly increase the risk of drive failure.** A fan running at even a low speed can greatly reduce temperatures. Drive temperature can often be monitored via SMART; [smartmon](https://web.archive.org/web/20180610231725/http://smartmontools.sourceforge.net/ "http://smartmontools.sourceforge.net/") is available on most open-source OS and supports temperature measurement on a wide range of drives. Note that Smartmon should not be set to perform automatic offline testing on a live server (so take care to override the default config file on the FreeBSD port of Smartmon): this is known to cause occasional ATA device driver timeouts in the FreeBSD kernel, and may reduce the useful life of the drive.



##   Particular drives


###   Solid State Drives


SSD drives can also be a good choice due to no moving parts, low power consumption, duty cycle, and low heat output. They are increasingly affordable.


SSD drives often have "block" sizes larger than the traditional 512B, usually 2 or 4K. 



###   Hitachi Drives


Some Hitachi 2.5 inch drives rated for 24*7 use are:



*  Travelstar E7K100 (SATA and PATA);
*  Travelstar E5K160 (SATA and PATA);
*  Travelstar E5K250 (SATA only).


See [www.hitachigst.com](https://web.archive.org/web/20180610231725/http://www.hitachigst.com/ "http://www.hitachigst.com") (Products, Travelstar). 


Update (March 2009): In the UK, Dabs.com now stocks the Travelstar 5K320 EA (Extended Availability) drive: 320GB @5400 RPM. Hitachi part number HTE543232L9A300, Dabs part number [5H0QTS](https://web.archive.org/web/20180610231725/http://www.dabs.com/ProductView.aspx?Quicklinx=5H0Q "http://www.dabs.com/ProductView.aspx?Quicklinx=5H0Q"). Rated for 24*7 operation. (A 500 GB version has also been announced: if anyone finds these in stock somewhere, please update this page.)


Unlike laptop drives, these Hitachi drives do not keep spinning up and down when idle: they just keep spinning the whole time. 



###   Fujitsu Drives


Three Fujitsu drives to consider are: 



*  MHW2120BK - high duty cycle (newer);
*  MHV2080BS - high duty cycle (older and near eol);
*  MHW2040AC - extreme environment (automotive).




Retrieved from "[http://wiki.soekris.info/What\_2.5%22\_hard\_drives\_are\_suitable](What_2.5"_hard_drives_are_suitable.html)"
[Category](https://web.archive.org/web/20180610231725/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Hardware](https://web.archive.org/web/20180610231725/http://wiki.soekris.info/Category_Hardware "Category_Hardware")

 

