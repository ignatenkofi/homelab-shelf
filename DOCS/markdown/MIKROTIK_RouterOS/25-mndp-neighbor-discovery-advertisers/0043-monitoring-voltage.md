## Monitoring voltage 

Last but not least - is to "monitor voltage" using the analog pins.  You need a script that will read/monitor voltage on schedule and then send the data via e- mail, MQTT or HTTPS (fetch). 

Create a script, as shown below. In this example, we will be using MQTT publish (but you can create a similar script with "/tool e-mail .." to use e-mail notifications): 

:local broker "name" 

:local topic "topic" 

:local message "{\"voltage(mV)\":$[/iot gpio analog get pin3 value]}" /iot mqtt publish broker=$broker topic=$topic message=$message 

The script will read/measure the voltage on pin3 and publish the data to the MQTT broker. 

Do not forget to set up MQTT broker (/iot mqtt brokers add ..) and alter a few script lines beforehand: 

:local broker "name" 

The broker's "name" should be changed accordingly (you can check all created brokers and their names using CLI command /iot mqtt brokers print). 

:local topic "topic" 

The topic should be changed as well. The topic itself is configured on the server-side, so make sure that the correct topic is used. 

Save the script and name it, for example, "voltagepublish". To automate the process, you can use the scheduler. 

```
[admin@device] /system scheduler> add name=run-45s interval=45s on-event="voltagepublish"
```

The schedule configuration shown above will run the script every 45 seconds. 

1597
