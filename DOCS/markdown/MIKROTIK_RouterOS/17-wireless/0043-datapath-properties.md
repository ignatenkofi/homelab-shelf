## Datapath properties 

Parameters relating to forwarding packets to and from wireless client devices. 

**==> picture [516 x 122] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (bridge interface) Bridge interface to add interface to, as a bridge port.<br>Virtual ('slave') interfaces are by default added to the same bridge, if any, as the corresponding master interface. Master<br>interfaces are not by default added to any bridge.<br>bridge-cost  (integer;  Bridge port cost to use when adding as bridge port.<br>default:  10 )<br>bridge-horizon  (none integ|  Bridge horizon to use when adding as bridge port.<br>er; default:  none )<br>**----- End of picture text -----**<br>

1352 

**==> picture [516 x 372] intentionally omitted <==**

**----- Start of picture text -----**<br>
client-isolation   (no | yes;  Determines whether client devices connecting to this interface are (by default) isolated from others or not.<br>default:  no ) This policy can be overridden on a per-client basis using access list rules, so a an AP can have a mixture of isolated and<br>non-isolated clients.<br>Traffic from an isolated client will not be forwarded to other clients and unicast traffic from a non-isolated client will not be<br>forwarded to an isolated one.<br>interface-list  (interface list;  List to which add the interface as a member.<br>default:  no )<br>traffic-processing  (on-cap |<br>on-capsman | on-capsman- This setting is only available starting with  7.21beta2  version.<br>secure)<br>on-cap , will make it so that the CAP itself is responsible for handling all WiFi traffic (same as any standalone AP<br>would);<br>on-capsman , will make it so that the CAP's WiFi traffic is forwarded to a pseudo-tunnel to the CAPSMAN and the<br>CAPsMAN becomes responsible for CAP's traffic handling;<br>on-capsman-secure , will make it so that the CAP's WiFi traffic is forwarded to an encrypted pseudo-tunnel to the<br>CAPSMAN and the CAPsMAN becomes responsible for CAP's traffic handling.<br>When using  traffic-processing=on-capsman  setting, be aware, that since all the CAP's WiFi traffic now<br>gets handled by the CAPsMAN (gets pushed into the CAPsMAN), it will increase CAPSMAN's resource<br>consumption (CPU and RAM usage).<br>vlan-id  (none | integer 1.. Default VLAN ID to assign to client devices connecting to this interface (only relevant to interfaces in AP mode).<br>4095; default:  none ) When a client is assigned a VLAN ID, traffic coming from the client is automatically tagged with the ID and only packets<br>tagged with with this ID are forwarded to the client.<br>802.11ac chipsets do not support this type of VLAN tagging , but they can be configured as VLAN access ports<br>in bridge settings.<br>**----- End of picture text -----**<br>
