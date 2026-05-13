## USB Port Type 

RB912UAG and RB953GS have partially shared USB port and miniPCIe slot. Due to hardware restrictions it is possible to use only one at the time for 3G /LTE modem. 

```
[admin@MikroTik] > /system routerboard usb set type=
USB-type-A  mini-PCIe
```

Available properties: 

type (USB-type-A | mini-PCIe; Default: "USB-type-A") - Type of enabled port. 

1752 

**==> picture [13 x 13] intentionally omitted <==**

RB953GS: The miniPCIe slot closer to Ethernet ports on the RB953GS board is the one which is shared with USB port and has configurable US B port type, its USB bus number is 1. Depending on USB port type the power reset is done on USB port or miniPCIe slot. The other miniPCIe slot closer to SFP slots has independent bus - 2.
