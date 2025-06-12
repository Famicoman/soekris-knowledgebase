# Updating Bios

[comBIOS updates](https://web.archive.org/web/20180812042147/http://www.soekris.com/downloads.htm "http://www.soekris.com/downloads.htm") are occasionally made available to [fix bugs and add features](https://web.archive.org/web/20180812042147/http://www.soekris.com/Software/changelog.txt "http://www.soekris.com/Software/changelog.txt"). Old versions continue to be available but one should not downgrade to a version earlier than that supplied with the board (for example, newer flash chips aren't supported by older versions).

## Basic procedure

The basic procedure for updating is to enter the comBIOS monitor by [serial console](https://web.archive.org/web/20180812042147/http://wiki.soekris.info/Connecting_to_the_serial_console "Connecting to the serial console"), transfer the file to RAM using XMODEM, then programme the flash memory:

```
comBIOS Monitor.   Press ? for help.

> download -

Start sending file using XMODEM protocol.
[...]
Transfer complete

File downloaded succesfully, size 880 Blocks.

> flashupdate
Updating BIOS Flash ,,,,,,,,,,,,,,,,,,,,,,,,,,,,....,,,,.. Done.

> reboot
```

Since 1.22 the download command defaults to CRC. By entering *download -* it's possible to revert to checksums which interoperate better with some software.

## cu and tip

Install *lrzsz* before starting.

Connect to the serial port at the correct port speed (by default Soekris use 19200baud):

```
$ cu -l /dev/tty00 -s 19200
```

Note: you may need 'chown uucp /dev/ttyS0' here to get access to the serial port.

Power up the board and interrupt the boot sequence to enter the comBIOS monitor with Ctrl-P. If you have configured fastboot (comBIOS 1.28 and on) you will need to be quick.

```
5 Seconds to automatic boot.   Press Ctrl-P for entering Monitor.
```

Initiate the download.

```
comBIOS Monitor.   Press ? for help.

> download -

Start sending file using XMODEM protocol.
```

Now start the transfer using ~C:

```
~CLocal command? lsz -X b4801\_122.bin
Sending b4801\_122.bin, 880 blocks: Give your local XMODEM receive command now.
Xmodem sectors/kbytes sent: 879/109k  
Bytes Sent: 112640   BPS:1706                            

Transfer complete

File downloaded succesfully, size 880 Blocks.
```

Continue with updating the flash and rebooting as above. 

If you are using Mac OS X 10.5, or a recent linux version, substitute ~+ for ~C:

```
~+lsz -X b4801\_133.bin
```

Assuming that you have installed lrzsz in the first place.

If you have trouble with the ~C command in cu, try tip instead, especially in FreeBSD where cu is deprecated.

```
 $ tip -19200 sio0
```

then as above with cu.

## Screen

On Mac OS X using screen(1) + lrzsz works pretty well.

First install *lrzsz*. On OS X: 

```
port install lrzsz
```

Then run screen against your serial port

```
screen /dev/tty.yourserialdevice 9600
```

Then enter the bios monitor and upload.

```
comBIOS Monitor.   Press ? for help.

> download -

Start sending file using XMODEM protocol.
```

Then you type:

```
^A:exec !! sz -X b5501\_133c.bin
```

Note: that ^A is "control+a" or "ctrl+a".

## Minicom

Install *lrzsz* before starting.

I had some trouble using minicom (I didn't understand the instructions properly) so I've made a step-by-step guide - hopefully it saves someone else the troubles I had. Note: minicom didn't work in my case, cu did with modification - see above - .

You can update Soekris Bios (any model) with Minicom and few steps. Before starting, download the latest available bios from soekris.com and save it in your home directory (minicom's file manager is a bit painful to browse around too much with - having the bin file in your home directory saves the hassle). Also, check if Minicom settings for serial ports (ctrl a+z and O on Minicom) match this:

```
Serial Device : /dev/ttyS0  (for first serial port on a PC)
Lockfile Location : /var/lock
Bps/Par/Bits : 19200 8N1
Hardware Flow Control : No
Software Flow Control : No
```

Here's what I did to update BIOS, step by step (everything after # is a comment, after > is what you type to the comBIOS monitor)

```
$ sudo minicom   # you probably need root privileges to get exclusive access to the serial port
Welcome to minicom 2.2

 OPTIONS: I18n
 Compiled on Apr 27 2007, 15:50:20.
 Port /dev/ttyS0

              Press CTRL-A Z for help on special keys

# turn on the Soekris board, and it starts the comBIOS (I have snipped some extra lines from the output)

POST: 012345689bcefghips1234ajklnopqr,,,tvwxy
comBIOS ver. 1.32i 20071005  Copyright (C) 2000-2007 Soekris Engineering.
net5501
0512 Mbyte Memory                        CPU Geode LX 500 Mhz
Pri Mas  SanDisk SDCFH-1024              LBA Xlt 993-32-63  1001 Mbyte

4 Seconds to automatic boot.   Press Ctrl-P for entering Monitor.

# here I hit Ctrl-P

comBIOS Monitor.   Press ? for help.

> download -

Start sending file using XMODEM/CRC protocol.

# Hit Ctrl-a, then z (presents the minicom menu) then s (for "Send file")
# this opens a text-mode dialog-box like this:

      +-[Upload]--+
      | zmodem    |
      | ymodem    |
      | xmodem    |
      | kermit    |
      | ascii     |
      +-----------+

# arrow-down to xmodem and hit Enter
# this will present a text-mode dialog to choose the file:

+------------------------[Select a file for upload]-------------------------+
|Directory: /home/fnerk                                                     |
| [.ssh]                                                                    |
| [Desktop]                                                                 |
| b5501\_132i.bin                                                            |
| b5501\_133.bin                                                             |
|              ( Escape to exit, Space to tag )                             |
+---------------------------------------------------------------------------+
              [Goto]  [Prev]  [Show]   [Tag]  [Untag] [Okay]

# arrow-down to the file you want, hit space-bar to select it, then hit Enter
# this will show another dialog to display transfer progress

        +-----------[xmodem upload - Press CTRL-C to quit]------------+
        |Xmodem sectors/kbytes sent:   0/ 0kRetry 0: NAK on sector    |
        |Retry 0: NAK on sector                                       |
        |Retry 0: NAK on sector                                       |
        |Retry 0: NAK on sector                                       |
        |Retry 0: NAK on sector                                       |
        |Retry 0: NAK on sector                                       |
        |Xmodem sectors/kbytes sent: 780/97k                          |
        +-------------------------------------------------------------+

# when the transfer is complete, it tells you so:

        +-----------[xmodem upload - Press CTRL-C to quit]------------+
        |Retry 0: NAK on sector                                       |
        |Retry 0: NAK on sector                                       |
        |Bytes Sent: 100352   BPS:1864                                |
        |                                                             |
        |Transfer complete                                            |
        |                                                             |
        | READY: press any key to continue...                         |
        +-------------------------------------------------------------+

# Note:  you are unable to transfer the file, change your Soekris serial speed to 9600. 

# hit enter, which will return you to the comBIOS prompt, and type flashupdate

> flashupdate
Updating BIOS Flash ,,,,,,,,,,,,,,,,,,,,,,,,,,,,..,,,,.... Done.

# and now reboot
> reboot

# and watch as your Soekris reboots with new BIOS:

comBIOS ver. 1.33  20070103  Copyright (C) 2000-2007 Soekris Engineering.
```

If minicom report errors during transfer, you can try this:

in minicom:

```
> download   
```

in another term, run the transfer command \_after\_ suspending the minicom terminal session with CTRL-a, j.: 

```
sx -X /tmp/b5501\_133.bin > /dev/ttyS0 < /dev/ttyS0
```

## TeraTerm bulk update script

If you use teraterm, here's a macro script that will mass update soekris your net5501's one at a time. Very nice to have when you're updating 50+ at a time :P 

This script restarts when done, if you want it to end after the first run, just replace "goto start" with "closett". Also "showtt -1" hides the console, just remove that line if you want to watch the progress. The filepath for the bios file is relative, please keep this in mind.

```
show -1
inputbox 'Port number(e.g. 3):' 'Select Serial port'
port=inputstr
inputbox 'Bios file:' 'Select bios file'
bios\_file=inputstr
setdlgpos 200 200
statusbox 'Please powercycle your soekris box' 'Update status'
messagebox 'Please powercycle your soekris box' 'Update status'
portnumber='/C='
strconcat portnumber port
connect portnumber
showtt -1
:start
wait #10'POST: 012345689bcefgh'
send 16
statusbox 'Preparing,please wait' 'Update status'
wait #10'>'
sendln "download"
wait #10'Start sending'
statusbox 'Transfering firmware...' 'Update status'
xmodemsend bios\_file 2
wait #10'>'
statusbox 'Updating firmware, DO NOT TURN OFF THE BOX!' 'Update status'
sendln "flashupdate"
pause 1
Wait 'Done.' 'Error'
if result = 0 statusbox 'Failed!' 'Update status'
if result = 1 statusbox 'Success!' 'Update status' 
if result = 2 statusbox 'Failed!' 'Update status'
wait #10'>'
sendln "reboot"
wait #10'comBIOS ver.'
statusbox 'Plug on new box' 'Update status'
goto start
```

The macro was made for tera term 4.53 from [The "UTF-8 TeraTerm Pro with TTSSH2" website](https://web.archive.org/web/20180812042147/http://ttssh2.sourceforge.jp/ "http://ttssh2.sourceforge.jp/")

If you save it as a ttl file you can start it from the command line or a batch file, your pick with 

```
ttpmacro.exe updatesoekrisbios.ttl
```

Oh, and all relies on that your tera term is setup correctly with console speed and whatnot :)

##  Links to other guides

* Ultradesic write a good [how-to for FreeBSD and MS Windows](https://web.archive.org/web/20180812042147/http://www.ultradesic.com/?section=36 "http://www.ultradesic.com/?section=36")
