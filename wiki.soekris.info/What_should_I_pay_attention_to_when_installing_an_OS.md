
### From Soekris Info Wiki



Jump to: [navigation](What_should_I_pay_attention_to_when_installing_an_OS.html#column-one), [search](What_should_I_pay_attention_to_when_installing_an_OS.html#searchInput) 
**What should I pay attention to when installing an OS?**


The most important thing (and probably the most common cause of errors) is to have your serial link setup right in all the appropriate places, meaning:



*  CommBIOS
*  the communication program
*  the boot loader
*  the kernel
*  the OS configuration


The two main things to look out for here are of course port and baud rate. CommBIOS defaults to 19200 bps and almost everything else defaults to 9600. If your serial output seems to "just stop" after you start booting, you probably have a mismatch. The simplest fix is to modify the CommBIOS setting to 9600, but you could also adjust everything else. What exactly needs to be done depends on the OS in question. See the OS-specific entries below for more details.


Apart from serial link issues, there's the ever-recurring disk geometry problem - see
the next entry.





Retrieved from "[http://wiki.soekris.info/What\_should\_I\_pay\_attention\_to\_when\_installing\_an\_OS](What_should_I_pay_attention_to_when_installing_an_OS.html)"
[Category](https://web.archive.org/web/20180818105349/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Operating Systems](https://web.archive.org/web/20180818105349/http://wiki.soekris.info/Category_Operating_Systems "Category_Operating Systems")

 

