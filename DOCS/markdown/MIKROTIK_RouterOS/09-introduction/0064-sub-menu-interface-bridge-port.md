## Sub-menu: `/interface bridge port` 

Property Description 

519 

multicast-router (yes | no) Shows if a multicast router is detected on the port. Monitoring value appears only when `igmp-snooping` is enabled. 

```
[admin@MikroTik] > /interface bridge port monitor [find]
              interface: ether2          ether3          ether4
                 status: in-bridge       in-bridge       in-bridge
            port-number: 1               2               3
                   role: designated-port designated-port designated-port
              edge-port: no              yes             yes
    edge-port-discovery: yes             yes             yes
    point-to-point-port: yes             yes             yes
           external-fdb: no              no              no
           sending-rstp: yes             yes             yes
               learning: yes             yes             yes
             forwarding: yes             yes             yes
       multicast-router: yes             no              no
       hw-offload-group: switch1         switch1         switch1
```
