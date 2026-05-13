## Enable Layer 3 Hardware Offloading 

```
# Enable full hardware routing on LAN ports
```

```
:foreach i in=[/interface/list/member/find where list=LAN] do={
```

```
    /interface/ethernet/switch/port set [/interface/list/member/get $i interface] l3-hw-offloading=yes
}
```

- `# Disable full hardware routing on WAN or Management ports` 

```
:foreach i in=[/interface/list/member/find where list=WAN or list=MGMT] do={
```

```
    /interface/ethernet/switch/port set [/interface/list/member/get $i interface] l3-hw-offloading=no
}
```

```
# Activate Layer 3 Hardware Offloading on the switch chip
/interface/ethernet/switch/set 0 l3-hw-offloading=yes
```

Results: 

Within the same VLAN (e.g., sfp1-sfp4), traffic is forwarded by the hardware on Layer 2 (L2HW). 

Inter-VLAN traffic (e.g. sfp1-sfp5) is routed by the hardware on Layer 3 (L3HW). 

- Traffic from/to the WAN port gets processed by the CPU/Firewall first. Then Fasttrack connections get offloaded to the hardware (HardwareAccelerated L4 Stateful Firewall). NAT applies both on CPU- and HW-processed packets. Traffic to the management port is protected by the Firewall.
