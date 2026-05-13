## Sub-menu: `/interface bridge port` 

The port menu enables control over the applicant and registrar settings on a per-port basis. 

**==> picture [502 x 158] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>mvrp-applicant-state  (non-participant | normal-participant; Default:  n MVRP applicant options:<br>ormal-participant )<br>non-participant  - port does not send any MRP messages;<br>normal-participant  - port participates normally in MRP exchanges.<br>mvrp-registrar-state  (fixed | normal; Default:  normal ) MVRP registrar options:<br>fixed  - port ignores all MRP messages, and remains Registered (IN) in<br>all configured vlans.<br>normal  - port receives MRP messages and handles them according to<br>the standard.<br>**----- End of picture text -----**<br>


To monitor the currently declared and registered VLAN IDs, use the `monitor` command. 

383 

```
[admin@MikroTik] > interface/bridge/port monitor [find interface=sfp-sfpplus1]
            interface: sfp-sfpplus1
               status: in-bridge
          port-number: 1
                 role: designated-port
            edge-port: no
  edge-port-discovery: yes
  point-to-point-port: yes
         external-fdb: no
         sending-rstp: yes
             learning: yes
           forwarding: yes
     actual-path-cost: 2000
     hw-offload-group: switch1
    declared-vlan-ids: 1,10,20-21
  registered-vlan-ids: 1,10,20,30-33
```
