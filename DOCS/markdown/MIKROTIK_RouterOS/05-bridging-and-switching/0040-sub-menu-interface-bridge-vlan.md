## Sub-menu: `/interface bridge vlan` 

All ports that are members of static VLANs or dynamic untagged VLANs created by the port `pvid` setting are treated as "fixed." Meaning the registrar disregards all MRP messages and remains registered (IN) for those VLANs. 

When VLAN is neither manually configured nor created by the port `pvid` setting, incoming registrations on a bridge port can dynamically designate that specific port as a tagged VLAN member. The `mvrp-forbidden` feature allows creating a list of ports that are restricted from registering into a specific VLAN ID. 

VLANs that are static or dynamic will be declared by the applicants unless this functionality is disabled by the port's `mvrp-applicant-state` , or by VLAN's `mvrp-forbidden` setting. 

**==> picture [502 x 327] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mvrp-forbidden  (interfaces;  Ports that ignore all MRP messages and remains Not Registered (MT), as well as disables applicant from<br>Default: ) declaring specific VLAN ID.<br>Sub-menu: /interface bridge vlan mvrp<br>The MVRP attributes menu can be used to see internal MVRP attribute states, as specified in the IEEE 802.1Q-2011.<br>Property Description<br>applicant- The Applicant state machine that declares attributes. Its state can be VO, VP, VN, AN, AA, QA, LA, AO, QO, AP, QP, or LO. Each<br>state state consists of two letters.<br>The first letter indicates the state:<br>V—Very anxious;<br>A—Anxious;<br>Q—Quiet;<br>L—Leaving.<br>The second letter indicates the membership state:<br>A - Active member;<br>P - Passive member;<br>O - Observer;<br>N - New.<br>For example, VP indicates "Very anxious, Passive member."<br>**----- End of picture text -----**<br>

384 

registrarThe Registrar state machine that records the registration state of attributes declared by other participants. Its state can be IN, LV, or state MT: 

IN—Registered; LV—Previously registered, but now being timed out; MT—Not registered. 

```
[admin@Mikrotik] /interface/bridge/vlan/mvrp print where vlan-id=10
Columns: BRIDGE, PORT, VLAN-ID, REGISTRAR-STATE, APPLICANT-STATE, LAST-EVENT
 #  BRIDGE    PORT           VLAN-ID  REGISTRAR-STATE  APPLICANT-STATE  LAST-EVENT
 1  bridge67  sfp-sfpplus1        10  IN               Quiet Active     JoinIn
 9  bridge67  sfp-sfpplus5        10  MT               Quiet Active     JoinEmpty
17  bridge67  sfp-sfpplus9        10  MT               Quiet Active     JoinEmpty
25  bridge67  sfp-sfpplus13       10  IN               Quiet Active     JoinIn
```
