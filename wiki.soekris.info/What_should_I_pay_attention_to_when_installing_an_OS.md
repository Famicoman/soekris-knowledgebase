# What should I pay attention to when installing an OS?

The most important thing (and probably the most common cause of errors) is to have your serial link setup right in all the appropriate places, meaning:

*  CommBIOS
*  the communication program
*  the boot loader
*  the kernel
*  the OS configuration

The two main things to look out for here are of course port and baud rate. CommBIOS defaults to 19200 bps and almost everything else defaults to 9600. If your serial output seems to "just stop" after you start booting, you probably have a mismatch. The simplest fix is to modify the CommBIOS setting to 9600, but you could also adjust everything else. What exactly needs to be done depends on the OS in question. See the OS-specific entries below for more details.

Apart from serial link issues, there's the ever-recurring disk geometry problem - see
the next entry.
