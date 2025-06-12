# What performance can I expect from the USB port on a Soekris box?

Sometimes people ask how fast the USB port is on the net5501.

To get an idea, I ran a simple test: 

*  I connected an iomega 1.5TB drive onto a 3,6 GHz PC running FreeBSD and did a 'dd if=/dev/da0s2 of=/dev/null bs=1048576' and got 34 539 769 bytes/second (or 263 megabits/second).
*  II then connected the same drive onto the USB port of a net5501 also running FreeBSD, issued the same command, and got 10 270 783 bytes/second (or 82 megabits/second).

So the USB port of the net5501 seems to run at about 1/3 the speed of a normal PC's USB port.

As for the net4801, it only has a USB 1.1 port, not a USB 2.0 port, so the speed is significantly slower: 992 806 bytes/second or 8 megabits/second.

Tried on a net6501, and obtained the following result:

*  External 2GB USB drive connected to a net6501, did a 'dd' and got 29 772 255 bytes/second (or 238 megabits/second).

Of course, Your Mileage May Vary.
