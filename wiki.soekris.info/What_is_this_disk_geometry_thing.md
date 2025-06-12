# What is this "disk geometry" thing?

If you burn a CF card on your PC, it will get its disk geometry values from your PC's
BIOS. These are not necessarily the same values the Soekris comBIOS sees. If you are
running a boot loader which uses absolute sector numbers (Lilo), you'll probably never
notice this, as such a boot loader can handle the anomalous geometry. However, if
you're running a boot loader which is FS-aware (most modern BLs), you might end up
with a system that apparently refuses to boot.

The solution is to pass fdisk the geometry data (C/H/S values) as displayed in the
serial console when you boot up the Soekris, when burning the CF. After that, things
should run without a problem.

To clarify: when you boot your Soekris and haven't set it to be quiet, you see something like:

```
POST: 012345689bcefghipsajklnopqr,,,tvwxy



comBIOS ver. 1.33  20080103  Copyright (C) 2000-2007 Soekris Engineering.

net4801

0128 Mbyte Memory                        CPU Geode SC1100 267 Mhz 

Pri Mas  SomeVendor SomeDevice ccc-hhh-ss  nnn Mbyte

Slot   Vend Dev  ClassRev Cmd  Stat CL LT HT  Base1    Base2   Int 
-------------------------------------------------------------------
0:00:0 1078 0001 06000000 0107 0280 00 00 00 00000000 00000000 
0:06:0 100B 0020 02000000 0107 0290 00 3F 00 0000E101 A0000000 10
0:07:0 100B 0020 02000000 0107 0290 00 3F 00 0000E201 A0001000 10
0:08:0 100B 0020 02000000 0107 0290 00 3F 00 0000E301 A0002000 10
0:18:2 100B 0502 01018001 0005 0280 00 00 00 00000000 00000000 
0:19:0 0E11 A0F8 0C031008 0117 0280 08 38 00 A0003000 00000000 11

 5 Seconds to automatic boot.   Press Ctrl-P for entering Monitor.
```

The line you search is the one starting with "Pri Mas" and you need the "ccc-hhh-ss" values. Feed this to fdisk on your PC, like this:

```
fdisk -C ccc -H hhh -S ss /dev/sdX
```
