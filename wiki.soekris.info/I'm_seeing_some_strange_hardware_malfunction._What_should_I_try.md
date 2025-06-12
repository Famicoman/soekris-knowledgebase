# I'm seeing some strange hardware malfunction. What should I try?

Symptoms of hardware failure can range from subtle flaws during operation to complete freeze of the system.

## Symptoms and causes

This is a list of symptoms that have been observed by users. *Please fill in your observations here. Include the type of your hardware and a description of what happens.*

* **LEDs flashing rapidly on and off**
	+ **Hardware:** net5501-70 with SMP 12V 1.5A, part no SBD212, powersupply.
	+ **Description:** The power, error and disk LEDs flash very quickly when power is inserted. No activity, not even on the console.
	+ **Cause:** Faulty powersupply.
	+ **Fix:** Replacing the PSU fixed the problem completely.

## Power supply

A large proportion of non-specific hardware problems can be traced to inadequate power supplies.
Check that the supply you are using is delivering adequate voltage under load, and that it is capable of delivering enough current for the Soekris box and any attached peripherals.

Choose a supply rated at more than the minimum specified voltage. For example, the net4501 is specified at 6-20V on the external connector, but using a nominal 6V power supply would risk problems if the voltage drops when the supply is loaded. Soekris suggests 12V power supplies, 9V would also be OK.

Soekris specifies power consumption in Watts, for instance the net4501 is specified at 10W. So a power supply should be capable of supplying at least that, and the Soekris-recommended unit at 12V 1A can supply 12W. (W = V x A).

Remember to include the power required by eg disk drives when assessing power requirements.

The Soekris-shipped power supply, SMP 12V 1.5A, part no SBD212, is known to spontaneously fail. [[1]](https://web.archive.org/web/20180610231534/http://lists.soekris.com/pipermail/soekris-tech/2008-January/013771.html "http://lists.soekris.com/pipermail/soekris-tech/2008-January/013771.html") [[2]](https://web.archive.org/web/20180610231534/http://lists.soekris.com/pipermail/soekris-tech/2006-November/011296.html "http://lists.soekris.com/pipermail/soekris-tech/2006-November/011296.html") [[3]](https://web.archive.org/web/20180610231534/http://lists.soekris.com/pipermail/soekris-tech/2008-March/014059.html "http://lists.soekris.com/pipermail/soekris-tech/2008-March/014059.html")
