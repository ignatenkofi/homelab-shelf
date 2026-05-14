## Bandwidth Test Client 

```
Sub-menu: /tool bandwidth-test
```

**==> picture [496 x 309] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>address  (IP address |  IP address of host<br>IPv6 prefix[%interface];<br>Default:)<br>direction (both | receive |  Direction of data flow<br>transmit; Default: receive )<br>duration  (time; Default: ) Duration of the test<br>interval  (time: 20ms..5s;  Delay between reports (in seconds)<br>Default: 1s )<br>local-tx-speed  (integer 0.. Transfer test maximum speed (bits per second)<br>18446744073709551615;<br>Default: )<br>local-udp-tx-size  (integer:  Local transmit packet size in bytes<br>28..64000)<br>password  (string; Default: "" Password for the remote user<br>)<br>protocol  (udp | tcp; Default: Protocol to use<br>udp )<br>random-data  (yes | no;  If random-data is set to yes, the payload of the bandwidth test packets will have incompressible random data stream<br>Default: no ) so that links that use data compression will not distort the results (this is CPU intensive and random-data should be<br>set to no for low speed CPUs)<br>**----- End of picture text -----**<br>

1756 

remote-tx-speed (integer Receive test maximum speed (bits per second) 0.. 18446744073709551615; Default: ) remote-udp-tx-size (integer Remote transmit packet size in bytes : 28..64000) connection-count (integer Number of TCP connections to use 1..255; Default:) user (string; Default: "" ) Remote user
