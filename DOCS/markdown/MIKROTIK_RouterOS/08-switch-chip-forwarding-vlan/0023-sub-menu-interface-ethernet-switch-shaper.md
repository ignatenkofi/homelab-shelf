## Sub-menu: `/interface ethernet switch shaper` 

**==> picture [507 x 118] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>burst  (integer; Default: 100k ) Maximum data rate which can be transmitted while the burst is allowed.<br>disabled  (yes | no; Default: no ) Enables or disables traffic shaper entry.<br>meter-unit  (bit | packet; Default: bit ) Measuring units for traffic shaper rate.<br>port  (port) Physical port for traffic shaper.<br>rate  (integer; Default: 1M ) Maximum data rate limit.<br>**----- End of picture text -----**<br>


426 

target (port | queueX | wrr-groupX; Three levels of shapers are supported on each port (including CPU port): Default: port ) 

Port level - Entry applies to the port of the switch-chip. WRR group level - Entry applies to one of the 2 Weighted Round Robin queue groups (wrr-group0, wrr-group1) on the port. 

Queue level - Entry applies to one of the 8 queues (queue0 - queue7) on the port.
