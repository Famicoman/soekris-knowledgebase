# Net4501 NTP Server

The net4501 is an excellent low-power / high-reliability device to use as a Stratum 1 NTP server. The great thing about the net4501 is that the Elan SC520 CPU has internal time registers with a resolution of about ~125 nanoseconds (according to others) and can be accessed with a few simple hardware modifications and proper kernel settings in FreeBSD. However, to fully benefit from this level of precision would require replacing the stock clock crystal with a signal from a more stable source.

## Guides & More Info

* [Using the Soekris computers for timestamping](https://web.archive.org/web/20180610231620/http://phk.freebsd.dk/soekris/pps/ "http://phk.freebsd.dk/soekris/pps/")
* [NTPns (and other relevant files)](https://web.archive.org/web/20180610231620/http://phk.freebsd.dk/NTPns/phkrel/ "http://phk.freebsd.dk/NTPns/phkrel/")
* [The World's Most Accurate NTP Server Hardware?](https://web.archive.org/web/20180610231620/http://www.febo.com/pages/soekris/ "http://www.febo.com/pages/soekris/")
* [Building a Stratum-1 GPS Based NTP Server with a Soekris net4501](https://web.archive.org/web/20180610231620/http://www.extremeoverclocking.com/articles/howto/Building_S1_NTP_Server_1.html "http://www.extremeoverclocking.com/articles/howto/Building_S1_NTP_Server_1.html")

[Net4501](Category_Net4501.md "Category_Net4501")
