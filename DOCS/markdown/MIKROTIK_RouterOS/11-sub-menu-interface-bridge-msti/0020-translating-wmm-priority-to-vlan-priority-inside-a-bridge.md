## Translating WMM priority to VLAN priority inside a bridge 

When a wireless packet is received with an already set WMM priority, the RouterOS bridge does not automatically translate it to a VLAN header. It means, that received wireless packets with WMM priority that get VLAN tagged by the bridge will be forwarded with a VLAN priority of 0. However, we can use a bridge filter rule with `from-ingress` setting to keep the priority in VLAN packets. For example, we would like to forward wireless packets over ether2 with a VLAN 10 header and keep the already set WMM priority (set by the wireless client). 

```
/interface bridge
```

```
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=wlan2 pvid=10
/interface bridge vlan
add bridge=bridge1 tagged=ether2 vlan-ids=10
```

```
# translates WMM priority to VLAN priority
/interface bridge filter
```

```
add action=set-priority chain=forward new-priority=from-ingress out-interface=ether2
```

The same situation applies when wireless packets are VLAN tagged by the wireless interface using the `vlan-mode=use-tag` and `vlan-id` settings. You still need to use the same bridge filter rule to translate WMM priority to VLAN priority: 

626 

```
/interface wireless
set [ find default-name=wlan2 ] vlan-mode=use-tag vlan-id=10
```

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2
add bridge=bridge1 interface=wlan2
```

```
 # translates WMM priority to VLAN priority
/interface bridge filter
```

```
add action=set-priority chain=forward new-priority=from-ingress out-interface=ether2
```

**==> picture [13 x 13] intentionally omitted <==**

The same principles apply in the other direction. RouterOS does not automatically translate VLAN priority to WMM priority. The same rule `newpriority=from-ingress` can be used to translate VLAN priority to WMM priority. 

**==> picture [13 x 13] intentionally omitted <==**

The RouterOS bridge forwards VLAN tagged packets unaltered, which means that received VLAN tagged packets with a certain VLAN priority will leave the bridge with the same VLAN priority. The only exception is when the bridge untags the packet, in this situation VLAN priority is not preserved due to the missing VLAN header.
