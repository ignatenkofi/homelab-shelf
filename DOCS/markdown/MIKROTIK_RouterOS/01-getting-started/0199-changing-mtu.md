## Changing MTU 

VMware ESXi supports MTU of up to 9000 bytes. To get the benefit of that, you have to adjust your ESXi installation to allow a higher MTU. Virtual Ethernet interface added after the MTU change will be properly allowed by the ESXi server to pass jumbo frames. Interfaces added prior to MTU change on the ESXi server will be barred by the ESXi server (it will still report the old MTU as the maximum possible size). If you have this, you have to re-add interfaces to the virtual guests. 

Example. There are 2 interfaces added to the ESXi guest, auto-detected MTU on the interfaces show MTU size as it was at the time when the interface was added: 

```
[admin@chr-vm] > interface ethernet print
```

```
Flags: X - disabled, R - running, S - slave
```

```
 #    NAME           MTU MAC-ADDRESS       ARP
```

```
 0 R  ether1        9000 00:0C:29:35:37:5C enabled
```

```
 1 R  ether2        1500 00:0C:29:35:37:66 enabled
```
