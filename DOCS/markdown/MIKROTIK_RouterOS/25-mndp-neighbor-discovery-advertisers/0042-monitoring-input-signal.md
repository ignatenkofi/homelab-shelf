## Monitoring input signal 

Another scenario is to "monitor input signal" using the digital input pins. You need a script that will initiate e-mail notification or MQTT/HTTPS (fetch) publish whenever the "INPUT" value changes for the pin with the direction="input" (whenever the RouterOS device receives a signal "0 or 1" from another device connected to the pin). 

E-mail notification script: 

/tool e-mail send to=config@mydomain.com subject="$[/system identity get name]" body="$[/iot gpio digital get pin5 input]" 

After creating a script, apply/set it to the "input" pin: 

1595 

```
[admin@device] /iot gpio digital> set pin5 script=script1
[admin@device] /iot gpio digital> print
Flags: X - disabled
```

```
 #   NAME                     DIRECTION OUTPUT INPUT SCRIPT
 0   pin5                     input     0      0     script1
 1   pin4                     output    0            script1
 2   pin6                     output    0
```

In the example above, the e-mail notification script is named "script1". 

As a result, whenever the input value changes (from 0 to 1 or from 1 to 0), the script automatically initiates an e-mail notification that will display the input value in the e-mail body. 

Do not forget to change the script line and configure the e-mail settings (/tool e-mail) accordingly: 

/tool e-mail send to="config@mydomain.com" subject="$[/system identity get name]"  body="$[/iot gpio digital get pin5 input]" 

Configure the actual e-mail address that you use. You can also change the subject and the body for the mail as you see fit. 

MQTT publish script: 

:local broker "name" 

:local topic "topic" 

:local message "{\"inputVALUE\":$[/iot gpio digital get pin5 input]}" /iot mqtt publish broker=$broker topic=$topic message=$message 

This script works the same way as the "e-mail notification" script, only when the input value changes the script initiates MQTT publish (instead of e-mail notification) and sends the input value received on the pin in the JSON format. Do not forget to set up MQTT broker (/iot mqtt brokers add ..) and alter a few script lines beforehand: 

:local broker "name" 

The broker's "name" should be changed accordingly (you can check all created brokers and their names using CLI command /iot mqtt brokers print). 

:local topic "topic" 

The topic should be changed as well. The topic itself is configured on the server-side, so make sure that the correct topic is used. 

Do not forget to apply/set the script to pin5 (/iot gpio digital set pin5 script=script_name), as shown in the "email notification" example above. 

If the mechanical switch is used to send the signal to the GPIO pin, it is suggested to use the following script instead (in case the script is initiated more than once when the signal is received on the pin): 

:global gpioscriptrunning; 

if (!$gpioscriptrunning) do={:set $gpioscriptrunning true; :log info "script started - GPIO changed"; :do {if ([/iot gpio digital get pin5 input] = "0") do={/tool e-mail send to="config@mydomain.com" subject="$[/system identity get name]" body="pin5 received logical 0"} else {/tool e-mail send to="config@mydomain.com" subject="$[/system identity get name]"  body="pin5 received logical 1"}; :delay 1s; :set $gpioscriptrunning false} on-error={:set $gpioscriptrunning false; :log info "e-mail error, resetting script state..."}} 

1596 

If the GPIO pin state changes more than once within mili/microseconds - the script above is going to make sure that e-mail notification is not sent more than once.
