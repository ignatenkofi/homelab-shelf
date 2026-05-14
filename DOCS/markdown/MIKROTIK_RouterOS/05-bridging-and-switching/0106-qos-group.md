## QoS Group 

The global QoS group table is used for VLAN-based, Protocol-based, and MAC-based QoS group assignment configuration. 

Sub-menu: `/interface ethernet switch qos-group` 

**==> picture [507 x 176] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>dei  (0..1; Default: none ) The new value of DEI for the QoS group.<br>disabled  (yes | no; Default: no ) Enables or disables protocol QoS group entry.<br>drop-precedence  (drop | green | red | yellow;  Drop precedence is an internal QoS attribute used for packet enqueuing or dropping.<br>Default: green )<br>dscp  (0..63; Default: none ) The new value of DSCP for the QoS group.<br>name  (string value; Default: groupX ) Name of the QoS group.<br>pcp  (0..7; Default: none ) The new value of PCP for the QoS group.<br>priority  (0..15; Default: 0 ) Internal priority is a local significance of priority for classifying traffic to different egress queues on a<br>port. (1 is highest, 15 is lowest)<br>**----- End of picture text -----**<br>

427
