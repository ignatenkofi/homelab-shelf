## Controlling relays 

One of the scenarios for the GPIO implementation is "controlling other relays" using digital output pins. Basically, sending "0" or "1" signal to the unit that is connected to the pin. To automate the process, you can use a scheduler, which will run the script at specific times. 

For example, you can add the first script (a single line shown below) and name it "output=0": 

/iot gpio digital set pin4 output=0 

Then add a second script (a single line shown below) and name it "output=1": 

/iot gpio digital set pin4 output=1 

Having both scripts, you can configure a schedule: 

```
[admin@device] /system scheduler> add name=run-30s interval=30s on-event="output=0"
```

The schedule configuration shown above will run the script with the name "output=0", every 30 seconds. 

```
[admin@device] /system scheduler> add name=run-45s interval=45s on-event="output=1"
```

The schedule configuration shown above will run the script with the name "output=1", every 45 seconds. 

As a result, the device will automatically send a signal to the 4th pin (digital output pin) with output value=0 every 30 seconds and a signal with output value=1 every 45 seconds. 

You can change the scheduled time as you see fit (depending on the requirements).
