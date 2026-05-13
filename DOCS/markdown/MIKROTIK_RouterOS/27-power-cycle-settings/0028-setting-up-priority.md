## Setting up priority 

Example of how to set priorities from CLI: 

**==> picture [13 x 13] intentionally omitted <==**

- /interface ethernet poe set ether2 poe-priority=10 /interface ethernet poe set ether3 poe-priority=13 /interface ethernet poe set ether4 poe-priority=11 /interface ethernet poe set ether5 poe-priority=14 

What will happen when power budget will go over total PoE-Out limit - first if the overload is detected, ether5 will be turned off (lowest priority), then recheck is done and if the still total limit overload is detected next port in priority will be turned off, in this example, ether3 will be turned off. Both of these ports will be reached every few seconds to check if it is possible to turn PoE-Out on for these ports. Power up will happen in reverse order as the power was cut.
