# Tuning net5501 openbsd

Unlike FreeBSD, OpenBSD does not support interface polling for the VIA VT6105M chips, so performance is limited. Fortunately, a net5501 with the high-end power supply can support some fairly nice NICs. The PCI slot can supply up to 20 watts, and this is sufficient for an Intel PCI-X quad-port NIC. While it will be limited to 32-bit/33 mhz, it will still be significantly faster than the onboard NICs.

The sysctl value net.inet.ip.ifq.maxlen should be adjusted to approximately 256 times the number of gigabit ports (eg, 1024 with a quad-port gigabit NIC). 

Categories: [Net5501](Category_Net5501.md "Category_Net5501")
