
### From Soekris Info Wiki



Jump to: [navigation](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#column-one), [search](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#searchInput) 


|  |
| --- |
| Contents* [1 storage](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#storage)
* [2 power](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#power)
* [3 connectivity](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#connectivity)
	+ [3.1 tcp/ip](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#tcp.2Fip)
	+ [3.2 serial](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html#serial)
 |

 if (window.showTocToggle) { var tocShowText = "show"; var tocHideText = "hide"; showTocToggle(); } 
#  storage


Although you could PXE boot off the network and run without a disk you will probably want to install an operating system on your soekris box. For this you will need some sort of non-volatile storage. Compact flash cards are often used. [2.5 inch laptop hard drives](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/What_2.5%22_hard_drives_are_suitable "What 2.5\" hard drives are suitable") are also an option. Solid state hard drives are now price competitive with fast compact flash cards and are faster. The time saved in OS install can be worth the extra cost of a little speed.



#  power


You will need a 12-20V power supply. 



#  connectivity


From time to time you will need to change the firmware settings or work with the operating system you have installed on your Soekris.



##  tcp/ip


Once the operating system is installed and running, it can be managed fully via ssh. Many distros contain OpenSSH or a derivative like Drop Bear.



##  serial


While it's possible to entirely avoid interacting with the soekris over the [serial communications channel](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/index.php?title=Category:Serial_Console&action=edit "Category:Serial Console") (say,by PXE booting and running "diskless") it's very likely that you will want serial communications for at least the initial OS install. This means a null-modem cable and, of course, a PC or other computer with a serial port (or else a serial to USB adapter with an appropriate driver). Apart from that, you'll need a program for serial communication, like *cu* or *minicom*. Null-modem cables are readily available these days thanks to the STB. They can also be purchased from Soekris. If you need to make a cable yourself, an excellent reference is the [RS-232 standard](https://web.archive.org/web/20180610231730/http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html "http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html") itself.


Most new machines lack serial ports and USB-to-Serial adapters are used instead. The chipset (e.g. [FTDI](https://web.archive.org/web/20180610231730/http://www.ftdichip.com/FTProducts.htm "http://www.ftdichip.com/FTProducts.htm") or [Prolific](https://web.archive.org/web/20180610231730/http://www.prolific.com.tw/eng/downloads.asp?id=31 "http://www.prolific.com.tw/eng/downloads.asp?id=31")) used in the adapter is important. The documentation in the kernel source tree for your distro is one place to start looking to see what's supported. For the Linux kernel, one place is at Documentation/usb/usb-serial.txt.gz





Retrieved from "[http://wiki.soekris.info/What\_additional\_hard\_and\_software\_do\_I\_need\_to\_run\_and\_manage\_a\_Soekris\_box](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.html)"
[Categories](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Hardware](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/Category:Hardware "Category:Hardware") | [HowTo](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/Category:HowTo "Category:HowTo") | [FAQ](https://web.archive.org/web/20180610231730/http://wiki.soekris.info/Category:FAQ "Category:FAQ")

 

