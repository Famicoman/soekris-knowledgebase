# Master/Slave

On the net4801 and net5501, you can change a comBIOS setting to select whether the CF module is set to master or slave. This is done by using the cable-select pin. If a PATA hard-drive is attached, it should be jumpered to use cable-select rather than forcing it to be primary or slave (cable-select for the hard drive is set to the opposite of the CF).

Some CF have a problem with this. Quoting from [a soekris-tech post from Søren Kristensen](https://web.archive.org/web/20180610231614/http://marc.info/?l=soekris-tech&m=111559192823339&w=2):

"The net4801 do that by setting the pin status during post and then issueing a hard reset by pulsing the ATA RESET pin to get the devices to reinitialize and sample the cable select pin. Unfortunate some CF module do not sample the cable select pin when hard reset, and although the CF specs are not specific on that, good practice is to reset everything when reset.... On the net4801, the cable select pin to the CF module is pulled high until programmed to it's final value, and some CF modules apperently only sample that pin during power up and therefore always defaulting to slave.

Solutions:

CF modules that to not correctly sample the cable select pin during hard reset should not be used on a net4801. I will make the cable select pin defauling to low on power up on next revision, that way those CF modules can still be used, but will then always be master instead of slave.

As usual, Sandisk always work...."

The way this is handled gives a method that can be used by people wishing to use both a SATA and PATA hard drive: if the PATA drive is jumpered to force it to a particular setting (e.g. master), and the comBIOS setting for CF is set the same way, the SATA drive will appear as the other (e.g. slave). If this is done, a CF module cannot be used at the same time. 