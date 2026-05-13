## PTP with IGMP Snooping 

If IGMP snooping is enabled on your bridge and VLANs are configured as shown in the previous example, you must manually add static Multicast Database (MDB) entries for each VLAN containing PTP ports that use IPv4 (224.0.1.129) as their transport modes. This ensures proper forwarding of PTP multicast traffic. 

```
/interface bridge/mdb add group=224.0.1.129 bridge=bridge1 ports=bridge1 vid=10
/interface bridge/mdb add group=224.0.1.129 bridge=bridge1 ports=bridge1 vid=20
```

**==> picture [13 x 13] intentionally omitted <==**

Static MDB entries in PTP setup are only required when IGMP snooping is enabled alongside VLANs.
