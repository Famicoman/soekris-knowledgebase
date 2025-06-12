# What do all those BIOS settings do?

## Disclaimer

This list was assembled from the PDF documentation, changelogs and the mailing list. The author cannot guarantee any of this information is correct. Please feel free to add information to this list!

The format of the entries is pretty straightforward:

```
SomeSetting = MyFavoriteValue
        (default: DefaultValue)
        (values: Some, Other, Possible, Values)
        Explanation and tips go here.
```

BIOS settings

```
ConSpeed = 115200
        (default: 19200)
        (values: 2400, 4800, 9600, 19200, 38400, 57600 or more)
        Set serial line connection speed.

ConLock = Enabled
        (default: Enabled)
        (values: Enabled, Disabled)
        Allow/prevent modification of the console via int14 syscall (eg. msdos 
        tries to change console speed on startup, which is not the smartest 
        thing to do because you have to guess it then).

ConMute = Disabled
        (default: Disabled)
        (values: Disabled, Enabled)
        Make bios quiet (no output). Sometimes useful if machine does not boot 
        immediately because no serial cable is connected (>1.29 only). You can
        still enter the BIOS via Ctrl-p at bootup.

BIOSentry = Enabled
        (default: Enabled)
        (values: Enabled, Disabled)
        Setting this to Disabled _only_ suppresses the startup message "Press 
        Ctrl-P for entering Monitor", you can however still enter the BIOS 
        with Ctrl-p if it is suppressed.

PCIROMS = Enabled
        (default: Enabled)
        (values: Enabled, Disabled)
        Control if BIOS will execute code found in PCI expansion ROMs.
        If disabled, "boot f0" will not work!

PXEBoot = Disabled
        (default: TODO)
        (values: Disabled, Enabled)
        Enable automatic PXE booting at startup. This does not influence manual
        PXE booting via "boot f0"!

FLASH = Primary
        (default: Primary)
        (values: Primary, Secondary)
        If you want to boot from a CF card, set this to Primary. If you want to 
        boot from a normal drive, you can still leave it at Primary.

BootDelay = 5
        (default: 5)
        (values: 2-16)
        Set the time you have to enter the BIOS (by hitting Ctrl-p) at startup.

FastBoot = Disabled
        (default: Disabled)
        (values: Disabled, Enabled)
        Cuts POST to 2 seconds. You need to be quick to hit Ctrl-p!

BootPartition = Disabled
        (default Disabled)
        (values: Disabled, 1-4)
        If set to Disabled, boot from BIOS MBR. If set to a number from 1 to 4, boot from that partition.

BootDrive = 80 81 F0 FF
        (default: 80 81 F0 (FF))
        (values: can be any combination of 80, 81, F0.
                80=first drive/hd0, 81=second drive/hd1, F0=PXE/network.)
        Which devices to boot from, in that order. Note that you have 
        4 "slots" and empty slots will be shown as "FF", so if you 
        "set BootDrive=80", it will show as "BootDrive = 80 FF FF FF".

ShowPCI = Enabled
        (default: TODO)
        (values: TODO)
        ???

Reset = Hard
        (default: Hard)
        (values: TODO)
        ???

CpuSpeed = Default
        (default: Default)
        (values: Default, xxx=200-cpumax+33)
        Change CPU clocking speed.
```

[Net4801](Category_Net4801.md) | [Net5501](Category_Net5501.md)