## Sub-menu: **`/snmp`** 

This sub menu allows to enable SNMP and to configure general settings. 

**==> picture [516 x 385] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>contact  (string; Default: ) "" Contact information<br>enabled  (yes | no;  Used to disable/enable SNMP service<br>Default:  no )<br>engine-id  (string;  For SNMP v3, used as part of the identifier. You can configure the suffix part of the engine id using this argument. If the<br>Default: ) "" SNMP client is not capable to detect set engine-id value then this prefix hex has to be used 0x80003a8c04<br>location  (string; Default:  "" Location information<br>)<br>trap-community  (string;  Which communities configured in the community menu to use when sending out the trap.<br>Default:  public )<br>trap-generators  (interface What action will generate traps:<br>s | start-trap; Default: )<br>interfaces - interface changes;<br>start-trap - SNMP server starting on the router<br>temp-exception - send trap when temperature reached 100c (or value configured for cpu-overtemp-temperature at<br>/system health )<br>trap-interfaces  (string | all List of interfaces that traps are going to be sent out.<br>; Default: )<br>trap-target  (list of IP/IPv6; IP (IPv4 or IPv6) addresses of SNMP data collectors that have to receive the trap<br>Default:  0.0.0.0 )<br>trap-version  (1|2|3;  A version of SNMP protocol to use for trap<br>Default: ) 1<br>src-address  (IPv4 or  Force the router to always use the same IP source address for all of the SNMP messages<br>IPv6 address; Default: ) ::<br>vrf  (VRF name; default  Set VRF on which service is listening for incoming connections<br>value:  main )<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

the engine-id field holds the suffix value of engine-id, usually, SNMP clients should be able to detect the value, as SNMP values, as read from the router. However, there is a possibility that this is not the case. In which case, the engine-ID value has to be set according to this rule: <engine-id prefix> + <hex-dump suffix>, so as an example, if you have set 1234 as suffix value you have to provide 80003a8c04 + 31323334, combined hex (the result) is 80003a8c0431323334 

1813
