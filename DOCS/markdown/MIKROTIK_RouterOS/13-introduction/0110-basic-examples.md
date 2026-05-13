## Basic examples 

Check port usage, as only one instance can use the serial port simultaneously: 

```
[admin@MikroTik] /port print
Flags: I - inactive
 #   DEVICE NAME                     CHANNELS USED-BY                   BAUD-RATE
 0          serial0                         1 Serial Console            auto
```

In case there is one port and it is used by the console, release it from the console menu: 

```
[admin@MikroTik] > /system console print
Flags: X - disabled, U - used, F - free
 #   PORT
TERM
 0 U serial0                                                                    vt102
```

```
[admin@MikroTik] > /system console disable 0
```

Adjust port settings specifically for your device (leave "auto" for LtAP mini): 

```
[admin@MikroTik] /port> set 0 baud-rate=4800 parity=odd
[admin@MikroTik] /port> print detail
Flags: I - inactive
 0   name="usb1" used-by="" channels=1 baud-rate=4800 data-bits=8 parity=odd stop-bits=1 flow-control=none
```
