## Port isolation 

Port isolation provides the possibility to divide (isolate) certain parts of your network, this might be useful when you need to make sure that certain devices cannot access other devices, this can be done by isolating switch ports. Port isolation only works between ports that are members of the same switch. Switch port isolation is available on all switch chips since RouterOS v6.43. 

**==> picture [516 x 53] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>forwarding-override  (interface;  Forces ingress traffic to be forwarded to a specific interface. Multiple interfaces can be specified by separating<br>Default: ) them with a comma.<br>**----- End of picture text -----**<br>


**==> picture [13 x 13] intentionally omitted <==**

(R/M)STP will only work properly in PVLAN setups, (R/M)STP will not work properly in setups, where there are multiple isolated switch groups, because switch groups might not properly receive BPDUs and therefore fail to detect network loops. 

**==> picture [13 x 13] intentionally omitted <==**

The `forwarding-override` property affects ingress traffic only. Switch ports that do not have the `forwarding-override` specified can send packets through all switch ports. 

488 

**==> picture [13 x 13] intentionally omitted <==**

Switch chips with a VLAN table support ( QCA8337 , Atheros8327 , Atheros8316 , Atheros8227 and Atheros7240 ) can override the port isolation configuration when enabling a VLAN lookup on the switch port (the `vlan-mode` is set to `fallback` , `check` or `secure` ). If additional port isolation is needed between ports on the same VLAN, a switch rule with a new-dst-ports property can be implemented. Other devices without switch rule support cannot overcome this limitation.
