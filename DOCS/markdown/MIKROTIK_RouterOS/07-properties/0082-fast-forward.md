## Fast Forward 

Fast Forward allows forwarding packets faster under special conditions. When Fast Forward is enabled, then the bridge can process packets even faster since it can skip multiple bridge-related checks, including MAC learning. Below you can find a list of conditions that MUST be met in order for Fast Forward to be active: 

- Bridge has `fast-forward` set to `yes` Bridge has only 2 running ports 

Both bridge ports support Fast Path, Fast Path is active on ports and globally on the bridge Bridge Hardware Offloading is disabled Bridge VLAN Filtering is disabled Bridge DHCP snooping is disabled `unknown-multicast-flood` is set to `yes unknown-unicast-flood` is set to `yes broadcast-flood` is set to `yes` MAC address for the bridge matches with a MAC address from one of the bridge slave ports `horizon` for both ports is set to `none` 

**==> picture [13 x 13] intentionally omitted <==**

Fast Forward disables MAC learning, this is by design to achieve faster packet forwarding. MAC learning prevents traffic from flooding multiple interfaces, but MAC learning is not needed when a packet can only be sent out through just one interface. 

**==> picture [13 x 13] intentionally omitted <==**

Fast Forward is disabled when hardware offloading is enabled. Hardware offloading can achieve full wire-speed performance when it is active since it will use the built-in switch chip (if such exists on your device), fast forward uses the CPU to forward packets. When comparing throughput results, you would get such results: Hardware offloading > Fast Forward > Fast Path > Slow Path. 

It is possible to check how many packets where processed by Fast Forward: 

```
[admin@MikroTik] /interface bridge settings> pr
              use-ip-firewall: no
     use-ip-firewall-for-vlan: no
    use-ip-firewall-for-pppoe: no
              allow-fast-path: yes
      bridge-fast-path-active: yes
     bridge-fast-path-packets: 0
       bridge-fast-path-bytes: 0
  bridge-fast-forward-packets: 16423
    bridge-fast-forward-bytes: 24864422
```

385 

**==> picture [13 x 13] intentionally omitted <==**

If packets are processed by Fast Path, then Fast Forward is not active. Packet count can be used as an indicator of whether Fast Forward is active or not. 

Since RouterOS 6.44 it is possible to monitor Fast Forward status, for example: 

```
[admin@MikroTik] /interface bridge monitor bridge1
                  state: enabled
    current-mac-address: B8:69:F4:C9:EE:D7
            root-bridge: yes
         root-bridge-id: 0x8000.B8:69:F4:C9:EE:D7
         root-path-cost: 0
              root-port: none
             port-count: 2
  designated-port-count: 2
           fast-forward: yes
```

**==> picture [13 x 13] intentionally omitted <==**

Disabling or enabling fast-forward will temporarily disable all bridge ports for settings to take effect. This must be taken into account whenever changing this property on production environments since it can cause all packets to be temporarily dropped.
