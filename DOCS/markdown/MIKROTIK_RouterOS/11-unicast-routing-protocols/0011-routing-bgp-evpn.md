## `/routing bgp evpn` 

See EVPN documentation. 

**==> picture [516 x 288] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  (string;  Name of the entry<br>Default: )<br>instance  (name) BGP instance this EVPN is assigned to.<br>export  - a group of parameters associated with the route export<br>.route- List of route targets that will be added to EVPN routes when exporting.<br>targets  (Iist<br>of RTs)<br>import  - a group of parameters associated with the route import<br>.route- List of route targets that will be used to import EVPN routes.<br>targets  (Iist<br>of RTs)<br>rd  (string) Specifies the value that gets attached to route so that receiving routers can distinguish advertisements that may otherwise look the<br>same. Used to distinguish between tenants using overlapping IP ranges. Also can be used to simplify convergence and redundancy<br>within Virtual Network. RDs form MLAG pairs should be unique, too.<br>vni  (range of  Range of Virtual Network Identifiers.<br>integers[0..<br>4294967295])<br>vrf  (name)<br>**----- End of picture text -----**<br>

958
