## USB Power Reset 

USB power reset turns off USB port power for a specified time. It is useful when 3G/LTE modem needs to be restarted but there is no physical access to it. 

Available properties: 

duration (time; Default: "3s") - Time interval of how long power is turned off. 

For example, turn off USB port power for 10 seconds: 

```
/system routerboard usb power-reset duration=10s
```

RouterBoards with multiple USB buses also require a bus specified in order to do a USB power reset. Available properties: 

duration (time; Default: "3s") - Time interval of how long power is turned off. bus (integer; Default: 1) - USB bus where power reset is applied. 

**==> picture [13 x 13] intentionally omitted <==**

RB953GS : The miniPCIe slot closer to Ethernet ports on the RB953GS board is the one which is shared with USB port and has configurable US B port type, its USB bus number is 1. Depending on USB port type the power reset is done on USB port or miniPCIe slot. The other miniPCIe slot closer to SFP slots has independent bus - 2. 

**==> picture [13 x 13] intentionally omitted <==**

RB922UAG : The USB port has an independent bus - 1. The miniPCIe slot has an independent bus - 2. 

**==> picture [13 x 13] intentionally omitted <==**

CCR1072-1G-8S+ : The micro USB port has independent bus - 0. The USB Type-A port has independent bus - 1.
