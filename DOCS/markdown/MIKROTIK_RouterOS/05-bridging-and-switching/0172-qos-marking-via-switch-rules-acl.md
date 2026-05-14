## QoS Marking via Switch Rules (ACL) 

Starting from RouterOS v7.15 , it is possible to assign QoS profiles via Switch Rules (ACL). 

Sub-menu: `/interface/ethernet/switch/rule` 

**==> picture [516 x 112] intentionally omitted <==**

**----- Start of picture text -----**<br>
New/Changed  Description<br>Properties<br>new-qos-profile  (name) The name of the QoS profile to assign to the matched packets.<br>keep-qos-fields  (yes | no;  Should the original values of QoS fields (PCP, DSCP) be kept (yes), or replace them with the ones from the assigned QoS<br>Default: no ) profile (no)? Relevant only if  new-qos-profile  is set.<br>new-vlan-priority  (0..7) Deprecated and should be replaced with the respective  new-qos-profile . Kept for backward compatibility. Relevant only if<br>qos-hw-offloading=no.<br>**----- End of picture text -----**<br>

The following example assigns a QoS profile based on the source MAC address.
