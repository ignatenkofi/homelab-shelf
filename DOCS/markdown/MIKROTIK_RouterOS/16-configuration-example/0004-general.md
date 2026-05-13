## General 

```
Sub Menu:/openflow
```

This menu lists the configuration of OpenFlow clients. 

**==> picture [516 x 176] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>certificate  (name) Name of the certificate from certificate list. Used together with  verify-peer  parameter.<br>controllers  (list of [protocol/address/port]) Configuration of the connection to the controller. Supported protocols are  tcp  and  tls . Example: tcp/1.2.3.4<br>/6654<br>datapath-id  (number/mac) Datapath ID consisting of two parts (integer number [0..65535] and MAC address) separated with slash.<br>name (string) Reference name of the entry<br>passive-port (disabled | integer [1..65535])<br>verify-peer (if-cert-present | none |  Verify peer's identity using certificates<br>required)<br>version (1 | 1.3 | default) Version of the OpenFlow standard to be used.<br>**----- End of picture text -----**<br>


Read-Only Parameters 

**==> picture [254 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>openflow-fast-path-bytes  (integer) Amount of bytes set to fastpath<br>openflow-fast-path-packets  (integer) Number of packets sent to fastpath<br>**----- End of picture text -----**<br>
