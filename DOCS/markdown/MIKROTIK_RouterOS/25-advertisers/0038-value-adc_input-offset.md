## `value = adc_input + offset` 

- , where adc_input is the voltage on the pin. 

- "OFFSET" configuration example is shown below: 

1593 

```
[admin@device] /iot gpio analog> set pin2 offset
```

```
Offset ::= [-]Num[mV]
  Num ::= -2147483648..2147483647    (integer number)
```

```
[admin@device] /iot gpio analog> set pin2 offset 2
[admin@device] /iot gpio analog> print
 # NAME                                                                                           VALUE
OFFSET
 0 pin2
2mV          2mV
 1 pin3
0mV          0mV
```
