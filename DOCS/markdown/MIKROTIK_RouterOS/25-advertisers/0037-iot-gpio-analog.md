## /iot gpio analog 

note please check on a product page whether your hardware supports analog input or not.: 

In the "analog" setting you can measure voltages on the analog input/ADC input pins: 

```
[admin@device] /iot gpio analog> print
 # NAME                                                                                     VALUE       OFFSET
 0 pin2                                                                                       0mV          0mV
 1 pin3                                                                                      32mV          0mV
```

"OFFSET" can be used to manually compensate voltage drop on the wires. "VALUE" is measured with:
