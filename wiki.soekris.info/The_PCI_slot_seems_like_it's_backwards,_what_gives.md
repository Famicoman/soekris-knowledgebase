
### From Soekris Info Wiki



Jump to: [navigation](The_PCI_slot_seems_like_it's_backwards,_what_gives.html#column-one), [search](The_PCI_slot_seems_like_it's_backwards,_what_gives.html#searchInput) 
PCI cards can have 3.3V or 5V signalling voltage, or both. The slot and edge-connector are keyed for this to prevent cards of the wrong voltage being inserted. The Soekris boards only support PCI cards with 3.3V signalling, and are keyed accordingly. (Note that the [net4501](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Net4501 "Net4501") has additional restrictions on the supply voltage to the card; many 3.3V cards can not be used in [net4501](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Net4501 "Net4501")).


The [net4801](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Net4801 "Net4801") in the standard case can only accept a card when the metal back-plate has been removed. Unfortunately, the 3.3V and 5V keys are the same distance from the side of the connector, so when the back-plate has been removed, a card of the wrong voltage can be physically inserted upside-down. Doing so can damage the PCI card and/or Soekris, so don't do it.


The part of the card where the backplate was, and the external connectors, should be positioned at the side of the Soekris board with the ethernet ports.


If the card cannot be inserted with a reasonable amount of force in that direction, do not install the card at all.


On the [net5501](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Net5501 "Net5501") in the standard case, PCI cards can be installed with the metal back-plate, but doing so requires unbolting the [net5501](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Net5501 "Net5501") from the case, assembling the two PC boards, and bolting it back in.





Retrieved from "[http://wiki.soekris.info/The\_PCI\_slot\_seems\_like\_it%27s\_backwards%2C\_what\_gives](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/The_PCI_slot_seems_like_it%27s_backwards%2C_what_gives)"
[Categories](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Hardware](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Category_Hardware "Category_Hardware") | [FAQ](https://web.archive.org/web/20180610231715/http://wiki.soekris.info/Category_FAQ "Category_FAQ")

 

