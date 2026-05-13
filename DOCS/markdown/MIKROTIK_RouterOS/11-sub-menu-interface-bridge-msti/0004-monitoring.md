## Monitoring 

Similarly to (R)STP, it is also possible to monitor MSTP status. By monitoring the bridge interface itself it is possible to see the current CIST root bridge and the current regional root bridge for MSTI0, it is also possible to see the computed hash of MST Instance identifiers and VLAN mappings, this is useful when making sure that certain bridges are in the same MSTP region. Below you can find an example of monitoring an MSTP bridge: 

616 

```
/interface bridge monitor bridge
                    state: enabled
      current-mac-address: 6C:3B:6B:7B:F0:AA
                bridge-id: 0x8000.6C:3B:6B:7B:F0:AA
              root-bridge: no
           root-bridge-id: 0x1000.64:D1:54:24:23:72
  regional-root-bridge-id: 0x4000.6C:3B:6B:7B:F0:AA
           root-path-cost: 10
                root-port: ether4
               port-count: 5
    designated-port-count: 3
        mst-config-digest: 74edbeefdbf82cf63a70cf60e43a56f3
             fast-forward: no
         multicast-router: yes
             igmp-querier: none
              mld-querier: none
        declared-vlan-ids: 1
      registered-vlan-ids: 1
```

In MSTP it is possible to monitor the MST Instance, this is useful to determine the current regional root bridge for a certain MST Instance and VLAN group, below you can find an example to monitor an MST Instance: 

```
/interface bridge msti monitor 1
                    state: enabled
               identifier: 2
      current-mac-address: 6C:3B:6B:7B:F0:AA
                bridge-id: 0x8000.6C:3B:6B:7B:F0:AA
              root-bridge: no
           root-bridge-id: 0.00:00:00:00:00:00
  regional-root-bridge-id: 0x1002.6C:3B:6B:7B:F9:08
           root-path-cost: 0
                root-port: ether2
               port-count: 5
    designated-port-count: 1
```

It is also possible to monitor a certain MST Override entry, this is useful to determine the port role for a certain MST Instance when configuring root ports and alternate/backup ports in an MSTP region, below you can find an example to monitor an MST Override entry: 

```
/interface bridge port mst-override monitor 1
                      port: ether3
                    status: active
                identifier: 2
                   port-id: 0x80.1
                      role: alternate-port
                  learning: no
                forwarding: no
   internal-root-path-cost: 15
         designated-bridge: 0x1002.6C:3B:6B:7B:F9:08
  designated-internal-cost: 0
        designated-port-id: 0x80.1
 designated-remaining-hops: 20
                tx-rx-bpdu: 3/7991
       discard-transitions: 0
       forward-transitions: 1
                  tx-rx-tc: 2/2
          topology-changes: 1
```
