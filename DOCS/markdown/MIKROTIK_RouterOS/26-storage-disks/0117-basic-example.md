## Basic example 

LED control via CLI commands for scripting purposes: 

```
#add led entry with specific type "on" or "off" to leds menu
/system leds add leds=led1 type=off
#to control led
/system leds set [find where leds="led1"] type=on
or
/system leds set [find where leds="led1"] type=off
```

Enable the User ACT LED to show current CAP status on an RB951 

```
/system leds
add leds=user-led type=ap-cap
```
