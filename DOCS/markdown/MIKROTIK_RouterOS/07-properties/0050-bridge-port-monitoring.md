## Bridge Port Monitoring 

To monitor the current status of bridge ports, use the `monitor` command. 

Sub-menu: `/interface bridge port monitor` 

**==> picture [502 x 602] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>actual-path- Shows the actual port path-cost. Either manually applied or automatically determined based on the interface speed and the  port-<br>cost  (integer: cost-mode  setting.<br>1..<br>200000000)<br>declared- VLANs declared by the intrface via MVRP Protocol.<br>vlan-ids (inte<br>ger 1..4094)<br>designated- Shows the designated bridge identifier, as determined from the port's priority vector.<br>bridge-id  (pri<br>ority.MAC<br>address)<br>designated- Shows the designated root-path-cost, as determined from the port's priority vector.<br>cost  (integer)<br>designated- Shows the designated internal-root-path-cost, as determined from the port's priority vector.<br>internal-cost  (<br>integer)<br>designated-m Shows the designated message age, as determined from the port's priority vector.<br>essage-age  (<br>time)<br>designated- Shows the designated max age, as determined from the port's priority vector. The BPDU packet can pass as many bridges as<br>max-age  (tim specified in the  max-message-age  parameter.<br>e)<br>designated- Shows the designated port identifier, as determined from the port's priority vector.<br>port-id  (priority<br>.integer)<br>designated- Shows the designated remaining hops, as determined from the port's priority vector. Number of hops that a packet is allowed to<br>remaining- traverse before reaching its destination.<br>hops  (integer)<br>discard- Counter, registring how often port transitions into discarding state.<br>transitions  (in<br>teger)<br>edge-port  (ye Whether the port is an edge port or not.<br>s | no)<br>edge-port- Whether the port is set to automatically detect edge ports.<br>discovery  (ye<br>s | no)<br>external-fdb  ( Whether the registration table is used instead of a forwarding database.<br>yes | no)<br>forwarding  (y Shows if the port is not blocked by (R/M)STP.<br>es | no)<br>forward- Counter, registring how often port transitions into forwarding state<br>transitions  (in<br>teger)<br>**----- End of picture text -----**<br>


365 

**==> picture [502 x 677] intentionally omitted <==**

**----- Start of picture text -----**<br>
hw-offload- Switch chip used by the port.<br>group  (switchX<br>)<br>interface  (na Interface name.<br>me)<br>last- Last topology change timer, records time since the last change.<br>topology-<br>change  (time)<br>learning  (yes Shows whether the port is capable of learning MAC addresses.<br>| no)<br>multicast- Shows if a multicast router is detected on the port. Monitoring value appears only when igmp-snooping is enabled.<br>router  (yes |<br>no)<br>registered-vl VLANs where the interface is registred via MVRP Protocol.<br>an-ids (integ<br>er 1..4094)<br>port-id  (priority In Spanning Tree Protocol each port has a unique Port Identifier. Priority[hex] + port number.<br>.integer)<br>point-to- Whether the port is connected to a bridge port using full-duplex (yes) or half-duplex (no).<br>point-port  (ye<br>s | no)<br>role  (designa (R/M)STP algorithm assigned port role:<br>ted | root-<br>port |  disabled-port  - disabled or inactive port.<br>alternate |  root-port  - port that is facing towards the root bridge and has the best (lowest cost) path to the root bridge. Only one root<br>backup |  port is elected per bridge (except the root bridge itself).<br>disabled) alternative-port  - port that is facing towards the root bridge, but is not going to forward traffic. Port provides a backup<br>path to the root bridge if the current root port fails.<br>designated-port  - port that is facing away from the root bridge and forwards traffic away from the root bridge to<br>downstream devices.<br>backup-port  - port that is facing away from the root bridge, but is going to forward traffic. Port that serves as a backup for a<br>designated port on the same segment.<br>In RouterOS, the  role  monitoring property displays RSTP roles, such as  alternate-port  and  backup-port , even when STP<br>mode is enabled. While this is technically incorrect, it does not affect the operation of STP. This is because STP treats all blocked<br>ports the same, without differentiating their purpose (e.g., as potential backup paths). The displayed roles are simply a reflection of<br>RSTP functionality and have no practical impact when STP is in use. See more details on STP and RSTP page.<br>root-path- The total cost of the path to the root-bridge.<br>cost  (integer)<br>sending-rstp  ( Whether the port is using RSTP or MSTP BPDU types. A port will transit to STP type when RSTP/MSTP enabled port receives an<br>yes | no) STP BPDU. This settings  does not  indicate whether the BDPUs are actually sent.<br>status  (in- Port status:<br>bridge |<br>inactive) in-bridge  - port is enabled<br>inactive  - port is disabled.<br>tx-rx-bpdu  (in Sent/recived bpdu messages counter.<br>teger)<br>tx-rx-tc  (integ Topology change messages transmitted/recived.<br>er)<br>topology- Topology change counter.<br>changes  (int<br>eger)<br>**----- End of picture text -----**<br>


366 

```
[admin@MikroTik] /interface/bridge/port monitor [find interface=ether1]
                  interface: ether1
                     status: in-bridge
                    port-id: 0x80.1
                       role: root-port
                  edge-port: no
        edge-port-discovery: yes
        point-to-point-port: yes
               external-fdb: no
               sending-rstp: yes
                   learning: yes
                 forwarding: yes
           actual-path-cost: 20000
    internal-root-path-cost: 20000
       designated-bridge-id: 0x1000.2C:C8:1B:FF:92:F4
   designated-internal-cost: 0
         designated-port-id: 0x80.1
  designated-remaining-hops: 20
                 tx-rx-bpdu: 3/63
        discard-transitions: 0
        forward-transitions: 1
                   tx-rx-tc: 2/0
           topology-changes: 1
       last-topology-change: 2m5s
           multicast-router: no
           hw-offload-group: switch1
          declared-vlan-ids: 1
        registered-vlan-ids: 1
```
