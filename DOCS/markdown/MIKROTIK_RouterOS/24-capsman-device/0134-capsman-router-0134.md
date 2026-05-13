## CAPsMAN router: 

Setup Bridge VLAN filtering to limit interfaces to appropriate VLANs 

```
/interface bridge
add name=bridge1 vlan-filtering=yes
/interface bridge port
add bridge=bridge1 interface=ether1 pvid=10
add bridge=bridge1 interface=ether2 pvid=20
/interface bridge vlan
add bridge=bridge1 tagged=bridge1 untagged=ether1 vlan-ids=10
add bridge=bridge1 tagged=bridge1 untagged=ether2 vlan-ids=20
```

**==> picture [13 x 13] intentionally omitted <==**

CAPsMAN will attach CAP interfaces to the bridge and automatically will add appropriate entries to the bridge VLAN table 

Note: CAPsMAN will attach CAP interfaces to the bridge and automatically will add appropriate entries to the bridge VLAN table. This feature is available starting with RouterOS v6.43 

Create appropriate CAP configurations for each VLAN 

1547 

```
/caps-man configuration
```

```
add country=latvia datapath.bridge=bridge1 datapath.vlan-id=10 datapath.vlan-mode=use-tag name=Config_WORK
security.authentication-types=wpa-psk,wpa2-psk \
```

```
    security.passphrase=secret_work_password ssid=WiFi_WORK
```

```
add country=latvia datapath.bridge=bridge1 datapath.vlan-id=20 datapath.vlan-mode=use-tag name=Config_GUEST
security.authentication-types=wpa-psk,wpa2-psk \
```

```
    security.passphrase=secret_guest_password ssid=WiFi_GUEST
```

We are going to create a single CAPsMAN provisioning rule to create the WiFi_WORK and the WiFi_GUEST SSIDs on a single device, each 

connect CAP is going to create these SSIDs automatically 

```
/caps-man provisioning
```

```
add action=create-dynamic-enabled master-configuration=Config_WORK slave-configurations=Config_GUEST
```

**==> picture [13 x 13] intentionally omitted <==**

You can create even more Virtual APs by adding multiple slave-configurations. That requires multiple CAPsMAN configurations that were created earlier. 

For security reasons, limit the CAPsMAN to interfaces. to which CAPs are going to be connected 

```
/caps-man manager interface
set [ find default=yes ] forbid=yes
add disabled=no interface=ether3
add disabled=no interface=ether4
```

Enable the CAPsMAN manager 

```
/caps-man manager
set enabled=yes
```

Setup DHCP Server for each VLAN 

```
/interface vlan
add interface=bridge1 name=VLAN10 vlan-id=10
add interface=bridge1 name=VLAN20 vlan-id=20
/ip address
add address=192.168.10.1/24 interface=VLAN10
add address=192.168.20.1/24 interface=VLAN20
/ip pool
add name=dhcp_pool10 ranges=192.168.10.2-192.168.10.254
add name=dhcp_pool20 ranges=192.168.20.2-192.168.20.254
/ip dhcp-server
add address-pool=dhcp_pool10 disabled=no interface=VLAN10 name=dhcp10
add address-pool=dhcp_pool20 disabled=no interface=VLAN20 name=dhcp20
/ip dhcp-server network
add address=192.168.10.0/24 dns-server=8.8.8.8 gateway=192.168.10.1
add address=192.168.20.0/24 dns-server=8.8.8.8 gateway=192.168.20.1
```
