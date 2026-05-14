## Monitoring 

You can check the STP status of a bridge by using the `/interface bridge monitor` command, for example: 

608 

```
interface/bridge/monitor bridge1
                    state: enabled
      current-mac-address: 74:4D:28:6F:31:10
                bridge-id: 0x8000.74:4D:28:6F:31:10
              root-bridge: no
           root-bridge-id: 0.74:4D:28:11:70:6B
  regional-root-bridge-id: 0.74:4D:28:11:70:6B
           root-path-cost: 0
                root-port: combo1
               port-count: 2
    designated-port-count: 0
        mst-config-digest: 4e22fbb9ede77faa45ec995c4ffa8085
             fast-forward: no
         multicast-router: yes
             igmp-querier: none
              mld-querier: none
        declared-vlan-ids: 1
      registered-vlan-ids: 1
```

Note that the root bridge doesn't have any root ports, only designated ports. 

You can check the STP status of a bridge port by using the `/interface bridge port monitor` command, for example: 

```
/interface bridge port monitor [find interface=sfp-sfpplus2]
                  interface: combo1
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
           actual-path-cost: 2000
    internal-root-path-cost: 2000
       designated-bridge-id: 0.74:4D:28:11:70:6B
   designated-internal-cost: 0
         designated-port-id: 0x80.1
  designated-remaining-hops: 20
                 bpdu-tx-rx: 3/7791
        discard-transitions: 0
        forward-transitions: 1
                   tc-tx-rx: 2/2
           topology-changes: 1
       last-topology-change: 4h19m43s
           multicast-router: no
           hw-offload-group: switch1
          declared-vlan-ids: 1
                             100
        registered-vlan-ids: 1
                             100
                             200-203
```

Note that `root-bridge-id` consists of the bridge priority and the bridge's MAC address, for non-root bridges the root bridge will be shown as `designate d-bridge` . 

**==> picture [13 x 12] intentionally omitted <==**

When using bridges that are set to use 802.1Q as EtherType, they will send out BPDUs to 01:80:C2:00:00:00, which are used by MSTP, RSTP, and STP. When using 802.1ad as bridge VLAN protocol, the BPDUs are not compatible with 802.1Q bridges and they are sent to 01:80:C2:00: 00:08. (R/M)STP will not function properly if there are different bridge VLAN protocols across the Layer2 network. 

STP and RSTP 

609 

STP and Rapid STP are used widely across many networks, but almost all networks have switched over to using only RSTP because of its benefits. STP is a very old protocol and has a convergence time (the time needed to fully learn network topology changes and to continue properly forwarding traffic) of up to 50 seconds. RSTP has a lot of smaller convergence time, a few seconds or even a few milliseconds. It is recommended to use RSTP instead of STP since it is a lot faster and is also backward compatible with STP. One of the reasons why RSTP is faster is because of reduced possible port states, below is a list of possible STP port states: 

- Forwarding - port participates in traffic forwarding and is learning MAC addresses, and is receiving BPDUs. Listening - port does not participate in traffic forwarding and is not learning MAC addresses, is receiving BPDUs. Learning - port does not participate in traffic forwarding but is learning MAC addresses. 

- Blocking - port is blocked since it is causing loops but is receiving BPDUs. Disabled - port is disabled or inactive. 

In RSTP the disabled, listening, and blocking port states are replaced with just one state called the Discarding state: 

Forwarding - port participates in traffic forwarding and is learning MAC addresses, is receiving BPDUs (forwarding=yes). Learning - port does not participate in traffic forwarding but is learning MAC addresses (learning=yes). 

Discarding - port does not participate in traffic forwarding and is not learning MAC addresses, is receiving BPDUs (forwarding=no). 

In STP ports are primarily categorized by states (e.g., Forwarding, Listening, Learning, Blocking, Disabled). Port behavior is determined dynamically based on the spanning tree algorithm but without explicitly assigning roles. The logic of forwarding or blocking traffic is derived from the calculation of Root Bridge, Root Ports, and Designated Ports, but these are considered part of the spanning tree topology rather than formalized port roles. RSTP explicitly defined port roles and introduces the concept of backup paths, which are explicitly represented through the Alternate Port and Backup Port roles. These roles did not exist in STP because STP treated blocked ports generically, without distinguishing their function as potential backups. 

Here is a breakdown of the port roles for RSTP protocols: 

Root Port - port that is facing towards the root bridge and has the best (lowest cost) path to the root bridge. Only one root port is elected per bridge (except the root bridge itself). 

- Designated Port - port that is facing away from the root bridge and forwards traffic away from the root bridge to downstream devices. Alternate Port - port that is facing towards the root bridge, but is not going to forward traffic. Port provides a backup path to the root bridge if the current root port fails. 

- Backup Port - port that is facing away from the root bridge, but is not going to forward traffic. Port that serves as a backup for a designated port on the same segment. 

Disabled Port - disabled or inactive port. 

In STP connectivity between bridges is determined by sending and receiving BPDUs between neighbor bridges. Designated ports are sending BPDUs to root ports. If a BPDU is not received 3 times the HelloTime in a row, then the connection is considered as unavailable and network topology convergence will commence. IT is possible to reduce STP convergence time in certain scenarios by reducing the `forward-delay` timer, which is responsible for how long can the port be in the learning/listening state. 

In RouterOS, it is possible to specify which bridge ports are edge ports. Edge ports are ports that are not supposed to receive any BPDUs, this is beneficial since this allows STP to skip the learning and the listening state and directly go to the forwarding state. This feature is sometimes called PortFast · You can leave this parameter to the default value, which is auto , but you can also manually specify it, you can set a port as an edge port manually for ports that should not have any more bridges behind it, usually these are access ports. 

Additionally, bridge port `point-to-point` , specifies if a bridge port is connected to a bridge using a point-to-point link for faster convergence in case of failure. By setting this property to `yes` , you are forcing the link to be a point-to-point link, which will skip the checking mechanism, which detects and waits for BPDUs from other devices from this single link, by setting this property to `no` , you are implying that a link can receive BPDUs from multiple devices. By setting the property to `yes` , you are significantly improving (R/M)STP convergence time. In general, you should only set this property to `no` , if it is possible that another device can be connected between a link, this is mostly relevant to Wireless mediums and Ethernet hubs. If the Ethernet link is full-duplex, `auto` enables point-to-point functionality. This property has no effect when `protocol-mode` is set to `none` .
