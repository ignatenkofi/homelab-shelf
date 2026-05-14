## PTP on VLAN Ports 

When PTP ports are also part of VLANs on your boundary clock device, you must add a bridge interface as an untagged port in the Bridge VLAN Table for every entry that includes a PTP port. 

This is necessary because the bridge interface functions as a bridge port towards the CPU. Therefore, it must be included in the VLAN table along with the PTP ports ensuring that packets can be correctly received from the physical port and forwarded to the CPU via the bridge. Let's continue with our previous configuration to make this clearer: 

```
# Create a new bridge interface
/interface/bridge/add name=bridge1
```

```
# Assign the ports that will be part of this bridge
/interface/bridge/port add bridge=bridge1 interface=sfp28-1 pvid=10
/interface/bridge/port add bridge=bridge1 interface=sfp28-2 pvid=20
```

```
# Create new entries for Bridge VLAN Table
```

```
/interface bridge vlan add bridge=bridge1 vlan-ids=10 untagged=bridge1,sfp28-1
```

```
/interface bridge vlan add bridge=bridge1 vlan-ids=20 untagged=bridge1,sfp28-2
```

**==> picture [13 x 13] intentionally omitted <==**

This applies to the IPv4 and L2-forwardable (01-1B-19-00-00-00) transport modes. The only exception is L2-non-forwardable (01-80-C2-00-000E), in which case there is no need to add a bridge interface as an untagged port in the Bridge VLAN Table. 

To check the default(auto) transport mode values for each profile, please refer to the "General Properties"  section.
