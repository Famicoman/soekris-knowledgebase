# Tuning net5501 freebsd

The VIA VT6105M chips used in net5501s have don't have very good interrupt mitigation, but this can be circumvented by turning on polling. See the ifconfig documentation. 

Categories: [Net5501](Category_Net5501.md "Category_Net5501")