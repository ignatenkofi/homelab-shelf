## Advertisers 

In this menu, it is possible to set up the Bluetooth chip to broadcast advertising packets. You can check and set advertiser settings with the commands: 

```
/iot bluetooth advertisers print
Flags: X - DISABLED
Columns: DEVICE, MIN-INTERVAL, MAX-INTERVAL, OWN-ADDRESS-TYPE, CHANNEL-MAP, AD-SIZE
#   DEVICE  MIN-INTERVAL  MAX-INTERVAL  OWN-ADDRESS-TYPE  CHANNEL-MAP  AD-SIZE
0 X bt1     1280ms        2560ms        random-static              37        0
                                                                   38
                                                                   39
/iot bluetooth advertisers set
```

Configurable settings are shown below: 

Property Description ad-structures (string; Default: ) Choose a pre-configured structure for the advertisement packets. For more information see the "AD structures" section. 

1556 

**==> picture [516 x 197] intentionally omitted <==**

**----- Start of picture text -----**<br>
channel-map  (37 | 38 | 39; Default: 37, 38, 39) Channels used for advertising.<br>disabled  (yes | no; Default:  yes ) An option to disable or enable the Bluetooth chip to broadcast advertising packets.<br>max-interval  (integer:20..10240; Default:  2560  The maximal interval for broadcasting advertising packets.<br>ms )<br>min-interval  (integer:20..10240; Default:  1280 ms ) The minimal interval for broadcasting advertising packets.<br>own-address-type  (public | random-static | rpa- The MAC address that is going to be used in the advertising packet's payload:<br>fallback-to-public | rpa-fallback-to-random;<br>Default:  random-static ) public →  To use the IEEE registered, permanent address.<br>random-static →  To use user-configurable address (will be changed on the next power-cycle).<br>rpa-fallback-to-public → To use Resolvable Random Private Address (RPA) that can only be<br>resolved if the receiver has our Identity Resolving Key (IRK). If RPA can not be generated, the<br>public address will be used instead.<br>rpa-fallback-to-random → Same as "rpa-fallback-to-public" but if RPA can not be generated, the<br>random-static address will be used instead.<br>**----- End of picture text -----**<br>

note : Advertising packets will be broadcasted each min-interval <=  <= X max-interval milliseconds.
