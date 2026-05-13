## Quick setup 

in this example, CRS317 and CRS309 devices are used as MLAG peers and any device with two SFP+ interfaces can be used as an LACP client. The SFP+1 interface is used on both peer nodes to create `peer-port` , and it is used for ICCP, see a network scheme below. 

**==> picture [504 x 367] intentionally omitted <==**

Below are configuration commands to create a regular LACP bonding in RouterOS for the Client device. To speed up LACP link establishment, use a 1- second LACPDU transmission rate: 

```
/interface bonding
add mode=802.3ad name=bond1 slaves=sfp-sfpplus1,sfp-sfpplus2 lacp-rate=1sec
```

Next, configure bonding interfaces for MLAG on Peer1 and Peer2 devices, use a matching `mlag-id` setting on both peer devices, and set the 1-second LACPDU transmission rate: 

778 

```
# Peer1
/interface bonding
```

```
add mlag-id=10 mode=802.3ad name=client-bond slaves=sfp-sfpplus2 lacp-rate=1sec
```

```
# Peer2
/interface bonding
add mlag-id=10 mode=802.3ad name=client-bond slaves=sfp-sfpplus2 lacp-rate=1sec
```

Set up the bridge interface with `vlan-filtering` enabled. In this example, we want both MLAG nodes to act as the root bridge, so we assign a better (lower) bridge priority using `priority=0x1000` . Make sure both MLAG nodes use the same priority value. 

Optionally, you can set `frame-types=admit-only-vlan-tagged` on the bridge interface to disables the default untagged VLAN 1 ( `pvid=1` ). 

```
# Peer1
/interface bridge
add name=bridge1 vlan-filtering=yes priority=0x1000 frame-types=admit-only-vlan-tagged
```

```
# Peer2
/interface bridge
add name=bridge1 vlan-filtering=yes priority=0x1000 frame-types=admit-only-vlan-tagged
```

Next, add the necessary interfaces to the bridge. In this example, only the peer port (sfp-sfpplus1) and the client-bond interface need to be added. 

For the peer port, we disable the default untagged VLAN 1 ( `pvid=1` ) by configuring it to accept only VLAN-tagged traffic ( `frame-types=admit-onlyvlan-tagged` ). 

For the client-bond interface, we want untagged traffic to belong to VLAN 10, so we set `pvid=10` on that interface. 

```
# Peer1
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus1 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=client-bond pvid=10
```

```
# Peer2
/interface bridge port
add bridge=bridge1 interface=sfp-sfpplus1 frame-types=admit-only-vlan-tagged
add bridge=bridge1 interface=client-bond pvid=10
```

**==> picture [13 x 13] intentionally omitted <==**

The MLAG supports STP, RSTP or MSTP protocol. Use the same STP priority and the same STP configuration (e.g. path-cost, priority, edge) on dual-connected bridge ports on both nodes. 

**==> picture [13 x 13] intentionally omitted <==**

If the dual-connected bond interface is not connected to any other RSTP/MSTP bridges or switches, you can set `edge=yes` on that interface on both MLAG nodes. 

This setting allows the bond port to quickly enter the forwarding state, which helps reduce packet loss when one side of the MLAG becomes available again. 

In this example, client-bond interfaces uses VLAN 10 for untagged traffic (set with `pvid=10` ), and we also want to allow tagged VLAN 20. To make sure traffic for both VLANs can pass between the MLAG devices, we need to add the peer ports as tagged members of VLANs 10 and 20 on both MLAG nodes. It is important to include the peer ports in all VLANs that are used on other bridge ports, this includes the untagged and tagged VLANs. Below are configuration commands for both peer devices: 

779 

```
# Peer1
/interface bridge vlan
add bridge=bridge1 tagged=sfp-sfpplus1 vlan-ids=10
add bridge=bridge1 tagged=sfp-sfpplus1,client-bond vlan-ids=20
```

```
# Peer2
/interface bridge vlan
add bridge=bridge1 tagged=sfp-sfpplus1 vlan-ids=10
add bridge=bridge1 tagged=sfp-sfpplus1,client-bond vlan-ids=20
```

**==> picture [13 x 13] intentionally omitted <==**

All VLANs used for bridge slave ports must be also configured as tagged VLANs for peer-port, so that peer-port is a member of those VLANs and can forward data. 

Last, specify `bridge` and `peer-port` to enable MLAG. To control which device becomes the primary MLAG node, set a lower `priority` value on the preferred device. In this example, we want Peer1 to be the primary, so we set its `priority=50` . Peer2 keeps the default priority of 128, making it the secondary. Below are configuration commands for both peer devices: 

```
# Peer1
/interface bridge mlag
set bridge=bridge1 peer-port=sfp-sfpplus1 priority=50
# Peer2
/interface bridge mlag
set bridge=bridge1 peer-port=sfp-sfpplus1
```

Additionally, check MLAG status on peer devices and make sure that Client LACP has both interfaces active. 

```
# Peer1
[admin@Peer1] > /interface/bridge/mlag/monitor
       status: connected
    system-id: 74:4D:28:11:70:6B
  active-role: primary
# Peer2
[admin@Peer2] > /interface/bridge/mlag/monitor
       status: connected
    system-id: 74:4D:28:11:70:6B
  active-role: secondary
# Client
[admin@Client] > /interface bonding monitor bond1
                    mode: 802.3ad
            active-ports: sfp-sfpplus1,sfp-sfpplus2
          inactive-ports:
          lacp-system-id: 74:4D:28:7B:7F:96
    lacp-system-priority: 65535
  lacp-partner-system-id: 74:4D:28:11:70:6C
```
