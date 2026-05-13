## Port Stats 

Example `[admin@Mikrotik] /interface/ethernet/switch/qos/port> print stats where name=ether2 name:     ether2 tx-packet:      2 887 tx-byte:  3 938 897 drop-packet:      1 799 drop-byte:  2 526 144 tx-queue0-packet:         50 tx-queue1-packet:      1 871 tx-queue3-packet:        774 tx-queue5-packet:        192 tx-queue0-byte:      3 924 tx-queue1-byte:  2 468 585 tx-queue3-byte:  1 174 932 tx-queue5-byte:    291 456 drop-queue1-packet:      1 799 drop-queue1-byte:  2 526 144` 

**==> picture [516 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name Port name.<br>tx-packet The total number of packets transmitted via this port.<br>tx-byte The total number of bytes transmitted via this port.<br>**----- End of picture text -----**<br>


470 

**==> picture [516 x 167] intentionally omitted <==**

**----- Start of picture text -----**<br>
drop-packet The total number of packets should have been transmitted via this port but were dropped due to a lack of resources (e.<br>g., queue buffers) or QoS Enforcement.<br>drop-byte The total number of bytes should have been transmitted via this port but were dropped.<br>tx-queue0-packet  ..  tx-queue7- The number of packets transmitted via this port from the respective queue.<br>packet<br>tx-queue0-byte  ..  tx-queue7- The number of bytes transmitted via this port from the respective queue.<br>byte<br>drop-queue0-packet  ..  drop- The number of packets dropped from the respective queue (or not enqueued at all due to lack of resources).<br>queue7-packet<br>drop-queue0-byte  ..  drop- The number of bytes dropped from the respective queue.<br>queue7-byte<br>**----- End of picture text -----**<br>
