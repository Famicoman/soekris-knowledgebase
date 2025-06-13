# Unofficial Hardware Manual

Soekris Engineering has published User Manuals for the Net4501 and Net4801, for their other boards documentation is scarce. This is an attempt to collect documentation those boards, mostly found in the [soekris-tech mailing list archives](https://web.archive.org/web/20180610231720/http://marc.info/?l=soekris-tech "http://marc.info/?l=soekris-tech").

## [net4501](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4501.htm "http://www.soekris.com/net4501.htm")

See [http://www.soekris.com/manuals/net4501\_manual.pdf](https://web.archive.org/web/20180610231720/http://www.soekris.com/manuals/net4501_manual.pdf "http://www.soekris.com/manuals/net4501_manual.pdf")

## [net4511](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4511.htm "http://www.soekris.com/net4511.htm"), [net4521](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4521.htm "http://www.soekris.com/net4521.htm")

Similar to net4501, with one (net4511) or two (net4521) PC-card slots in place of PCI, and two network ports ([PoE](https://web.archive.org/web/20180610231720/http://wiki.soekris.info/Power_over_Ethernet "Power over Ethernet") is supported, **on Eth0 only**). N.B. different power supply voltage range to net4501; see the [product detail pages](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4511.htm "http://www.soekris.com/net4511.htm").

## [net4526](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4526.htm "http://www.soekris.com/net4526.htm")

Similar to net4501, no PCI slot, and one network port ([PoE](https://web.archive.org/web/20180610231720/http://wiki.soekris.info/Power_over_Ethernet "Power over Ethernet")). N.B. different power supply voltage range to net4501; see the [product detail page](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4526.htm "http://www.soekris.com/net4526.htm").

## [net4801](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4801.htm "http://www.soekris.com/net4801.htm")

See [http://www.soekris.com/manuals/net4801\_manual.pdf](https://web.archive.org/web/20180610231720/http://www.soekris.com/manuals/net4801_manual.pdf "http://www.soekris.com/manuals/net4801_manual.pdf")

## [net4826](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4826.htm "http://www.soekris.com/net4826.htm")

Similar to net4801, no PCI slot, and one network port ([PoE](Power_over_Ethernet.md "Power over Ethernet")). N.B. different power supply voltage range to net4801; see the [product detail page](https://web.archive.org/web/20180610231720/http://www.soekris.com/net4826.htm "http://www.soekris.com/net4826.htm").

Based on a [soekris-tech post](https://web.archive.org/web/20180610231720/http://marc.info/?l=soekris-tech&m=119629299230423&w=2 "http://marc.info/?l=soekris-tech&m=119629299230423&w=2") it appears that JP6 is a USB 1.1 header.

## [net5501](https://web.archive.org/web/20180610231720/http://www.soekris.com/net5501.htm "http://www.soekris.com/net5501.htm")

Soekris's new platform based on the Geode LX. Broadly similar to net4801, with a more capable processor. The CPU on net5501 can forward 100Mb/s with larger packet sizes on most OS (not the case with net4801). The USB port is now high-speed USB 2.

The board is slightly larger than net4801; the standard case is significantly larger than net4801 but can accept a short PCI card without cutting the metal.

Standard ethernet is now 4 ports of VIA VT6105M (10/100 with auto-MDI/X).

Geode LX has an on-chip AES acceleration part: this is accessed over the bus (cf. VIA's Padlock AES acceleration which uses additional CPU instructions). For very small packet sizes (e.g. VoIP with efficient compression and small sample sizes), the bus access overheads make this slower than software crypto, but for the more common larger packet sizes (and mixes) it's very helpful.

net5501 also includes a simple OS-independent reboot facility over the serial console port. Send +++, delay for a couple of seconds, then send RESET (to reboot) or POWER (to shut off the onboard power-supply and restart after a short delay). Useful with some boot failures, or if your OS hangs and you don't use a watchdog timer.

Based on a soekris-tech post, the AVI6 sensor is connected to 2.5V power rail, used by the DDR memory chips, otherwise sensors are like the net4801.


Many more details about the connectors and interfaces have been collected in the [Net5501_Interfaces.md](5501_Interfaces "5501 Interfaces") page. The pinout of the GPIO connector is identical to net4801 (note that the manual identifies GPIO lines with numbers in octal, as with the datasheet for the IC; some OS identify GPIO lines in decimal).
