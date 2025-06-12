# What additional hard and software do I need to run and manage a Soekris box?

|  |
| --- |
| Contents* [1 storage](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.md#storage)
* [2 power](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.md#power)
* [3 connectivity](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.md#connectivity)
	+ [3.1 tcp/ip](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.md#tcp.2Fip)
	+ [3.2 serial](What_additional_hard_and_software_do_I_need_to_run_and_manage_a_Soekris_box.md#serial)
 |

# storage

Although you could PXE boot off the network and run without a disk you will probably want to install an operating system on your soekris box. For this you will need some sort of non-volatile storage. Compact flash cards are often used. [2.5 inch laptop hard drives](What_2.5_hard_drives_are_suitable.md "What 2.5\" hard drives are suitable") are also an option. Solid state hard drives are now price competitive with fast compact flash cards and are faster. The time saved in OS install can be worth the extra cost of a little speed.

# power

You will need a 12-20V power supply. 

# connectivity

From time to time you will need to change the firmware settings or work with the operating system you have installed on your Soekris.

## tcp/ip

Once the operating system is installed and running, it can be managed fully via ssh. Many distros contain OpenSSH or a derivative like Drop Bear.

## serial

While it's possible to entirely avoid interacting with the soekris over the serial communications channel (say,by PXE booting and running "diskless") it's very likely that you will want serial communications for at least the initial OS install. This means a null-modem cable and, of course, a PC or other computer with a serial port (or else a serial to USB adapter with an appropriate driver). Apart from that, you'll need a program for serial communication, like *cu* or *minicom*. Null-modem cables are readily available these days thanks to the STB. They can also be purchased from Soekris. If you need to make a cable yourself, an excellent reference is the [RS-232 standard](https://web.archive.org/web/20180610231730/http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html "http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html") itself.

Most new machines lack serial ports and USB-to-Serial adapters are used instead. The chipset (e.g. [FTDI](https://web.archive.org/web/20180610231730/http://www.ftdichip.com/FTProducts.htm "http://www.ftdichip.com/FTProducts.htm") or [Prolific](https://web.archive.org/web/20180610231730/http://www.prolific.com.tw/eng/downloads.asp?id=31 "http://www.prolific.com.tw/eng/downloads.asp?id=31")) used in the adapter is important. The documentation in the kernel source tree for your distro is one place to start looking to see what's supported. For the Linux kernel, one place is at Documentation/usb/usb-serial.txt.gz
