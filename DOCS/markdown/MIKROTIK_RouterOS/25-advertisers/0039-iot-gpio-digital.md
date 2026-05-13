## /iot gpio digital 

In the "digital" section you can send/receive a logical 0 or 1 signal using the digital output/input pins (output pins are "open drain"): 

```
[admin@device] /iot gpio digital> print
Flags: X - disabled
 #   NAME                                        DIRECTION OUTPUT INPUT
SCRIPT
 0   pin5                                        input     0      0
 1   pin4                                        output    0
 2   pin6                                        output    0
```

"DIRECTION" for the pin can be either "input" (a pin that can receive the signal) or "output" (a pin that can send the signal). 

**==> picture [13 x 13] intentionally omitted <==**

KNOT pin's "DIRECTION" for pin4 and pin6 can not be changed. Both pins are meant to be used only as "output" pins. 

When the pin's direction is set to "output", you can configure the "OUTPUT" value. Changing the "OUTPUT" value sends the signal to the pin. 

```
[admin@device] /iot gpio digital> set pin4 output=
Output ::= 0 | 1
```

```
[admin@device] /iot gpio digital> set pin4 output=1
[admin@device] /iot gpio digital> print
Flags: X - disabled
 #   NAME                                        DIRECTION OUTPUT INPUT
SCRIPT
 0   pin5                                        input     0      0
 1   pin4                                        output    1
 2   pin6                                        output    0
```

The "script" field allows you to configure a script, that will be initiated whenever the "INPUT" or "OUTPUT" value changes (from 0 to 1 or from 1 to 0). 

1594 

```
[admin@device] /iot gpio digital> set pin4 script=script1
[admin@device] /iot gpio digital> set pin5 script="/system .."
[admin@device] /iot gpio digital> print
Flags: X - disabled
 #   NAME                                        DIRECTION OUTPUT INPUT
SCRIPT
 0   pin5                                        input     0      0     /system
..
 1   pin4                                        output    1
script1
 2   pin6                                        output    0
```
