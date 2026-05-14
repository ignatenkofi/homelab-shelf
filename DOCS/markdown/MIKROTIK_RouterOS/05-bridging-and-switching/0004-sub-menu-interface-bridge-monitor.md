## Sub-menu: `/interface bridge monitor` 

**==> picture [502 x 221] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge-id  (priority. Local bridge indetifier, which is in form of bridge-priority.bridge-MAC-address.<br>MAC address)<br>current-mac- Current MAC address of the bridge.<br>address  (MAC<br>address)<br>designated-port- Number of designated bridge ports.<br>count  (integer)<br>declared-vlan-ids (i VLANs decleared on the bridge interface via MVRP protocol.<br>nteger 1..4094)<br>fast-forward  (yes |  Whether bridge fast-forward is active.<br>no)<br>igmp-querier  (none  Shows a bridge port and source IP address from the detected IGMP querier. Only shows detected external IGMP querier,<br>| interface & IPv4  local bridge IGMP querier (including IGMP proxy and PIM) will not be displayed. Monitoring value appears only when  igmp-<br>address) snooping  is enabled.<br>**----- End of picture text -----**<br>

355 

**==> picture [502 x 325] intentionally omitted <==**

**----- Start of picture text -----**<br>
mld-querier  (none |  Shows a bridge port and source IPv6 address from the detected MLD querier. Only shows detected external MLD querier,<br>interface & IPv6  local bridge MLD querier will not be displayed. Monitoring value appears only when  igmp-snooping  is enabled and the<br>address) bridge has an active IPv6 address.<br>mst-config-digest  (i Computed hash of VLAN mappings to MST Instance IDs.<br>nteger)<br>multicast-router  (ye Shows if a multicast router is detected on the port. Monitoring value appears only when  igmp-snooping  is enabled.<br>s | no)<br>port-count  (integer) Number of the bridge ports.<br>regional-root- The regional root bridge ID, which is in form of bridge-priority.bridge-MAC-address. Only applies when MSTP is enabled.<br>bridge-id  (priority.<br>MAC address)<br>registered-vlan-ids ( VLANs registered on the bridge interface via MVRP protocol.<br>integer 1..4094)<br>root-bridge  (yes |  Shows whether the bridge is the root bridge of the spanning tree.<br>no)<br>root-bridge-id  (priori The root bridge ID, which is in form of bridge-priority.bridge-MAC-address.<br>ty.MAC address)<br>root-path-cost  (inte The total cost of the path to the root-bridge.<br>ger)<br>root-port  (name) Port to which the root bridge is connected to.<br>state  (enabled |  State of the bridge.<br>disabled)<br>**----- End of picture text -----**<br>

```
[admin@MikroTik] /interface/bridge monitor bridge1
                    state: enabled
      current-mac-address: 2C:C8:1B:FF:92:F4
                bridge-id: 0x1000.2C:C8:1B:FF:92:F4
              root-bridge: yes
           root-bridge-id: 0x1000.2C:C8:1B:FF:92:F4
  regional-root-bridge-id: 0x1000.2C:C8:1B:FF:92:F4
           root-path-cost: 0
                root-port: none
               port-count: 2
    designated-port-count: 2
        mst-config-digest: d2b171a8ad95f593c241fc33d419a88c
             fast-forward: no
         multicast-router: no
             igmp-querier: none
              mld-querier: none
        declared-vlan-ids: 1
      registered-vlan-ids: 1
```
