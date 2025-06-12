# Connecting to the serial console

The primary console interface of the Soekris boards is the external serial port (with DE9-M connector). The comBIOS monitor uses this, and after boot BIOS screen I/O is redirected there.

The Soekris boards are computers and thus wired as DTE. To connect to another DTE (like your computer), you must use a cable or adapter ("null modem") which crosses the relevant lines - as a minimum, RxD (2) must be cross-wired to TxD (3). Problems, typically the boot loader failing to respond, can be experienced if the modem control lines aren't also connected (there are some mentions of avoiding these problems by setting the ConMute comBIOS parameter).

N.B. Some serial cables (e.g. those supplied with some switches) have the DE9-F connector needed to plug into a Soekris board or standard PC serial port, but are wired as DCE. These will not work.

Some people permanently connect a DE9-F<>RJ45 adapter (as often used when connecting to a terminal server), with RxD-TxD-GND connected to the RJ45 socket, and the control lines (1-4-6-8) connected together.

[Updating the BIOS](Updating_Bios.md "Updating Bios") is dealt with on a separate page.

|  |
| --- |
| Contents* [1 Standard UNIX-like OS](Connecting_to_the_serial_console.md#Standard_UNIX-like_OS)
	+ [1.1 Logging console activities](Connecting_to_the_serial_console.md#Logging_console_activities)
* [2 Mac OS X](Connecting_to_the_serial_console.md#Mac_OS_X)
* [3 Linux: Ubuntu or Other Distro](Connecting_to_the_serial_console.md#Linux:_Ubuntu_or_Other_Distro)
* [4 Windows](Connecting_to_the_serial_console.md#Windows)
 |

# Standard UNIX-like OS

Assuming a serial line on /dev/tty00 and Soekris default port speed of 19200 baud:

```
$ tip -19200 si0
```

or

```
$ cu -l /dev/tty00 -s 19200
```

To exit tip or cu, enter **~.** (tilde dot) at the beginning of a line. If you don't have a standard serial port available, most modern OS support RS232/USB adapters. 

Please note that on some systems cu will force hardware flow control, which can cause the console to lock when trying to enter input at the OpenBSD boot loader prompt. [http://www.mail-archive.com/misc@openbsd.org/msg30899.html](https://web.archive.org/web/20190218080801/http://www.mail-archive.com/misc@openbsd.org/msg30899.html "http://www.mail-archive.com/misc@openbsd.org/msg30899.html")

As a workaround, try using minicom or another program that allows for both hardware and software flow control to be disabled.

### Logging console activities

Assuming the same settings as the *cu* example above, the following line will log all input and output to the local filesystem to the file to the file *console-session.log* in the directory */tmp/*. 

```
$ cu -l /dev/tty00 -s 19200 | tee /tmp/console-session.log
```

##  Mac OS X

Connecting to a Soekris box from MacOS X requires a bit more hardware than most PCs. The major missing piece is the serial port. You'll need to acquire a USB->serial adapter. I've had success with both [IOGear](https://web.archive.org/web/20190218080801/http://www.iogear.com/main.php?loc=product_category&category=usb&category_id=104 "http://www.iogear.com/main.php?loc=product_category&category=usb&category_id=104") (GUC232A) and [Keyspan](https://web.archive.org/web/20190218080801/http://www.keyspan.com/products/homepage.2.productList.Serial.spml "http://www.keyspan.com/products/homepage.2.productList.Serial.spml") (UPR-112G) models. These devices require drivers to operate, so please consult the installer documentation that shipped with the adapter. The IOGear is a bit cleaner as the name of the device is "/dev/tty.usbserialX", whereas keyspan uses "/dev/tty.KeySerialX".

Once the driver is installed, connect a null-modem cable to the USB serial adapter, and to the Soekris box. The next step is choosing a terminal emulator. The "screen" utility requires the least effort to setup (it's installed by default on OS X) and is quite capable. So, fire up Terminal, and type the following:

```
hostname:~user$ screen /dev/tty.usbserial0 19200
```

Here, we see the first USB serial device if you installed the IOGear driver. Baud rate is set by supplying the appropriate speed to the command (Soekris boxen ship with the default baud rate set to 19200 8N1).

Next, power on the Soekris box, you should be greeted with the boot screen and see the option to enter the BIOS. Soekris provides [documentation](https://web.archive.org/web/20190218080801/http://www.soekris.com/downloads.htm "http://www.soekris.com/downloads.htm") for all the BIOS settings.

To disconnect from the Soekris, press CTRL+A, then CTRL+K. the first key combo interrupts screen to tell it you want to enter a command, the second combo is the "kill this session" command.

##  Linux: Ubuntu or Other Distro

Under Ubuntu, you can install the screen utility via synaptic or apt-get (if it isn't already installed) and then follow the directions for MacOS X. Some USB->Serial adapters will work under Linux, such as the IOGear GUC232. However, you may need to add the pl2303 driver for it manually:

```
hostname:~user$ modprobe -i pl2303
```

After this, the device will be accessible as /dev/ttyUSB0. NB that you'll need a crossover adapter between the Soekris board and the USB adapter.

Also you can install via synaptic or apt-get the package *minicom* and start it with

```
hostname:~user$ minicom
```

Minicom settings are available with CTRL+A Z, the more important changes are O (cOnfigure) --> serial port setup. To know all settings please read the man pages of minicom, is very simply and powerful!

The package *cu*, mentioned above, is also available for Linux from package repositories.

##  Windows

Users of some versions of Windows can use [PuTTY](https://web.archive.org/web/20190218080801/http://www.chiark.greenend.org.uk/~sgtatham/putty/ "http://www.chiark.greenend.org.uk/~sgtatham/putty/") (0.59 and newer); PuTTY works fine but doesn't have x-modem support, which is required if you need to upgrade the BIOS on your Soekris machine. 

Alternatives include [TeraTerm](https://web.archive.org/web/20190218080801/http://ttssh2.sourceforge.jp/ "http://ttssh2.sourceforge.jp/") and Poderosa. 

If you're running Windows XP, you can use HyperTerminal, but it was removed from Windows Vista and Windows 7. You could install Microsoft Virtual Machine with Windows XP Pro (free [Download](https://web.archive.org/web/20190218080801/http://www.microsoft.com/windows/virtual-pc/ "http://www.microsoft.com/windows/virtual-pc/") from Microsoft) which does have HyperTerminal, or just get the files hypertrm.dll and hypertrm.exe from an old XP install and copy them over to your Windows 7 machine should work fine.
