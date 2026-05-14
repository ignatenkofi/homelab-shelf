## Modem Access Technology example 

These LED trigger examples turn on LEDs in order of modem technology generation: GSM; 3G; LTE. 

1 LED: led1 turns on when LTE is active; 

```
/system leds add interface=lte1 leds=led1 modem-type=modem-technology
```

2 LEDs: led1 - 3G; led2 - LTE; 

```
/system leds
add interface=lte1 leds=led1,led2 modem-type=modem-technology
```

3 LEDs: led1 - GSM; led2 - 3G; led3 - LTE 

```
/system leds add interface=lte1 leds=led1,led2,led3 modem-type=modem-technology
```

1710
