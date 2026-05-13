## Sub-menu: `/interface/ethernet/switch` 

**==> picture [516 x 151] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mirror-target  (cpu |  Selects a single mirroring target port. Packets from  mirror-egress  and  mirror-ingress  ( /interface/ethernet<br>name | none; Default: no /switch/port ) and mirror ( /interface/ethernet/switch/rule ) will be sent to the selected port.<br>ne )<br>rspan  (no | yes; Default: Enables Remote Switch Port Analyzer (RSPAN) feature on  mirror-target . Traffic marked for ingress or egress mirroring<br>no ) is carried over a specified remote analyzer VLAN -  rspan-egress-vlan-id  and  rspan-ingress-vlan-id .<br>rspan-egress-vlan-id  (int Selects the VLAN ID for marked egress traffic. Only applies when  rspan  is enabled.<br>eger: 1..4095; Default: ) 1<br>rspan-ingress-vlan-id  (int Selects the VLAN ID for marked ingress traffic. Only applies when  rspan  is enabled.<br>eger: 1..4095; Default: ) 1<br>**----- End of picture text -----**<br>
