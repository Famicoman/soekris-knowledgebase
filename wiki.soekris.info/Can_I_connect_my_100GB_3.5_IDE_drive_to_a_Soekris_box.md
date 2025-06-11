
### From Soekris Info Wiki



Jump to: [navigation](Can_I_connect_my_100GB_3.5_IDE_drive_to_a_Soekris_box.html#column-one), [search](Can_I_connect_my_100GB_3.5_IDE_drive_to_a_Soekris_box.html#searchInput) 
**Can I connect my 1000GB 3.5" IDE drive to a Soekris box?**


In short: No. Or at least, it won't be easy. Even if you have a suitable adapter 
for the 44-pins connector, you would have to have the 3.5" HDD draw power from
an external source, as the Soekris boards power supply is limited.


**Option 1 - USB.**  You can connect a 3.5" IDE (or SATA) drive using an external enclosure
with a USB interface and connect it via USB (for those soekris models with USB
support.) Heck, get a good hub and connect *lots* of 3.5" drives! Be sure to use an enclosure with its own power supply unless you're certain you can supply enough power via the USB bus. Performance will likely suffer but you'll have storage.


**Option 2 - SATA.**  For the NET5501 only, you can connect low-power 3.5" SATA drives
(like the Western Digital GreenPower series) using a special power supply cable (for example from www.KD85.com) from the NET5501 power header to the SATA drive. You will need a good 12 volt power supply (say 25 watts) for the NET5501, and you'll need a large enough case, perhaps with a cooling fan. The WDC WD1000FYPS 1000GB drive is known to work like this - it runs happily with no need for a fan in a 19-inch rack case - but your mileage may vary with other drives: so you might want to ask on the Soekris mailing list before buying such a drive.





Retrieved from "[http://wiki.soekris.info/Can\_I\_connect\_my\_100GB\_3.5\_IDE\_drive\_to\_a\_Soekris\_box](Can_I_connect_my_100GB_3.5_IDE_drive_to_a_Soekris_box.html)"
[Categories](https://web.archive.org/web/20180610231413/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Hardware](https://web.archive.org/web/20180610231413/http://wiki.soekris.info/Category:Hardware "Category:Hardware") | [FAQ](https://web.archive.org/web/20180610231413/http://wiki.soekris.info/Category:FAQ "Category:FAQ")

 

