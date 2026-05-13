## Modem Signal Strength example 

The whole modem-signal strength range is [-113..-51] and the modem-signal-threshold increases the weakest signal limit to -91 so the signal range for LED indication is [-91..-51]. That range is divided into equal parts depending on number of LEDs configured for modem-signal LED trigger. The first LED turns on when signal is above -91 and the last LED turns on when signal reaches -51. 

```
/system leds
```

```
add interface=lte1 leds=led1,led2,led3,led4,led5 modem-signal-treshold=-91 type=modem-signal
```

1709
