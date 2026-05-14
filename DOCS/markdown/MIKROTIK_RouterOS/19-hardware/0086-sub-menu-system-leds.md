## Sub-menu: `/system leds` 

RouterOS allows configuring each LED's activity the way that the user wishes. It is possible to configure the LEDs to display wireless strength, blink the LEDs on interface traffic activity, and many other options. 

For example, default led configuration on Groove 

```
[admin@MikroTik] /system leds> print
Flags: X - disabled
# TYPE INTERFACE LEDS
0 wireless-signal-strength led1
led2
led3
led4
led5
1 interface-activity ether1 user-led
```

**==> picture [13 x 13] intentionally omitted <==**

Not all boards have the necessary hardware capabilities to support this feature. 

**==> picture [13 x 13] intentionally omitted <==**

RB Groove uses five LEDs for wireless strength and one for ethernet activity monitoring.
