## Port Extender settings 

This section describes the Port Extender settings. 

Sub-menu: `/interface bridge port-extender` 

**==> picture [502 x 112] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>control-ports  (interfaces;  Interfaces that will either connect to the CB (upstream port) or connect other PE devices in series (cascade port). A<br>Default:  none ) bonding interface with 802.3ad or balance-xor  mode  is also supported.<br>excluded-ports  (interfaces Interfaces that will not be extended.<br>; Default:  none )<br>switch  (name; Default:  no The switch that will act as the extender and ensure the control and network traffic. The PE will only enable when this<br>ne ) property is specified, otherwise, it will be in a disabled state.<br>**----- End of picture text -----**<br>
