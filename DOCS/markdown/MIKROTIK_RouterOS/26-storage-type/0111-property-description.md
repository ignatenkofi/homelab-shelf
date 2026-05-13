## Property Description 

**==> picture [506 x 141] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>disabled  (yes | no; Default: no ) Whether an item is disabled<br>interface  (string; Default: ) Name of the interface which will be used<br>for led status. Applicable only if type is<br>interface specific.<br>modem-signal-treshold  (integer [-113..-51]; Default: ) Applicable if a type is  modem-signal<br>leds  (list of leds; Default: ) List of led names used for a status report.<br>For example, wireless signal strength will<br>require more than one led.<br>**----- End of picture text -----**<br>


1706 

type (align-down | align-left | align-right | align-up | ap-cap | fan-fault | flash-access | interface-activity | interface-receive | interface-speed | interface-speed-1G | interface-speed-25G | interface-status | interface-transmit | modem-signal | modem-technology | off | on | poe-fault | poe-out | wireless-signalstrength | wireless-status; Default: ) 

Type of the status: 

- align-down - light the led if the w60g device needs to be aligned downwards for the best signal quality align-left - light the led if the w60g device needs to be aligned to the left align-right - light the led if the w60g device needs to be aligned to the right align-up - light the led if the w60g device needs to be aligned upwards ap-cap - blink on CAP initializing with CAPsMAN, steady on once connected fan-fault - light the led when any of the devices controlled fans stop working flash-access - blink the led on flash access interface-activity - blink the led on interface (traffic) activity interface-receive - blink the led on interface received a traffic interface-speed - light the led when interface works in 10Gbit rate interface-speed-1G - light the led when interface works in 1Gbit rate interface-speed-25G - light the led when interface works in 25Gbit rate interface-speed-100G - light the led when interface works in 100Gbit rate interface-status - light the led on interface status change interface-transmit - blink the led on interface transmitted traffic modem-signal - blink the led on 3G modem signal (either USB or miniPCIe) modem-technology - turns on LEDs in order of modem technology generation: GSM; 3G; LTE; single led turns on only when LTE is active. off - turn off the led on - turn on the led poe-fault - light the led when PoE out budget is close to the maximum supported limit poe-out - light the led when interface PoE out turns on wireless-signal-strength - light the leds displaying wireless signal (requires more than one led) wireless-status - light the led on wireless status change.
