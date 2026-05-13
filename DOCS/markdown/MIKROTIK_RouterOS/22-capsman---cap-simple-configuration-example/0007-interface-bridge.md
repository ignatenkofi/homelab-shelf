## `/interface bridge` 

```
add name=bridgeLocal vlan-filtering=yes
/interface wifi
set [ find default-name=wifi1 ] configuration.manager=capsman disabled=no
set [ find default-name=wifi2 ] configuration.manager=capsman disabled=no
/interface bridge port
```

```
add bridge=bridgeLocal comment=defconf interface=ether1
add bridge=bridgeLocal comment=defconf interface=ether2
add bridge=bridgeLocal comment=defconf interface=ether3
add bridge=bridgeLocal comment=defconf interface=ether4
add bridge=bridgeLocal comment=defconf interface=ether5
add bridge=bridgeLocal interface=wifi1 pvid=10
add bridge=bridgeLocal interface=wifi21 pvid=20
add bridge=bridgeLocal interface=wifi2 pvid=10
add bridge=bridgeLocal interface=wifi22 pvid=20
/interface bridge vlan
```

```
add bridge=bridgeLocal tagged=ether1 untagged=wifi1,wifi2 vlan-ids=10
add bridge=bridgeLocal tagged=ether1 untagged=wifi21,wifi22 vlan-ids=20
/interface wifi cap
```

```
set discovery-interfaces=bridgeLocal enabled=yes slaves-static=yes
```

**==> picture [13 x 13] intentionally omitted <==**

Check the dynamically created interface and assign the PVID to the appropriate one 

Additionally, the configuration below has to be added to the CAPsMAN configuration : 

```
/interface wifi datapath
```

```
add bridge=br name=DP_AC
/interface wifi configuration
```

```
add datapath=DP_AC name=MAIN_AC security=Security_MAIN ssid=MAIN_Network
```

```
add datapath=DP_AC name=GUEST_AC security=Security_GUEST ssid=GUEST_Network
```

```
/interface wifi provisioning
```

```
add action=create-dynamic-enabled master-configuration=MAIN_AC slave-configurations=GUEST_AC supported-
bands=5ghz-ac
```

```
add action=create-dynamic-enabled master-configuration=MAIN_AC slave-configurations=GUEST_AC supported-
bands=2ghz-n
```

**==> picture [13 x 13] intentionally omitted <==**

Passing datapaths "MAIN/GUEST" from the start of the example to "wifi-qcom-ac" CAP would be misconfiguration, make sure to use datapath without "vlan-id" specified to such devices.
