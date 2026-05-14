## Setup Examples 

**==> picture [13 x 13] intentionally omitted <==**

- Make sure you have added all needed interfaces to the VLAN table when using secure `vlan-mode` . For routing functions to work properly on the same device through ports that use secure `vlan-mode` , you will need to allow access to the CPU from those ports, this can be done by adding the switchX-cpu interface itself to the VLAN table. Examples can be found in the Management port section. 

**==> picture [13 x 13] intentionally omitted <==**

- It is possible to use the built-in switch chip and the CPU at the same time to create a Switch-Router setup, where a device acts as a switch and as a router at the same time. You can find a configuration example in the Switch-Router guide. 

**==> picture [13 x 13] intentionally omitted <==**

When allowing access to the CPU, you are allowing access from a certain port to the actual router/switch, this is not always desirable. Make sure you implement proper firewall filter rules to secure your device when access to the CPU is allowed from a certain VLAN ID and port, use firewall filter rules to allow access to only certain services. 

**==> picture [13 x 13] intentionally omitted <==**

Devices with MT7621 , MT7531 , EN7523, RTL8367 , 88E6393X , 88E6191X, 88E6190 switch chips support HW offloaded vlan-filtering in RouterOS v7. VLAN-related configuration on the "/interface ethernet switch" menu is not available. 

**==> picture [13 x 13] intentionally omitted <==**

- For VLAN related matchers or VLAN related action parameters to work on 88E6393X switch chip, you need to enable vlan-filtering on the bridge interface and make sure that hardware offloading is enabled on those ports, otherwise, these parameters will not have any effect.. 

VLAN Example 1 (Trunk and Access Ports) 

493 

RouterBOARDs with Atheros switch chips can be used for 802.1Q Trunking. This feature in RouterOS v6 is supported by QCA8337, Atheros8316, Atheros8327, Atheros8227 and Atheros7240 switch chips. In this example, ether3 , ether4, and ether5 interfaces are access ports, while ether2 is a trunk port. VLAN IDs for each access port: ether3 - 200, ether4 - 300, ether5 - 400. 

**==> picture [504 x 323] intentionally omitted <==**

Switch together the required ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
add bridge=bridge1 interface=ether4 hw=yes
add bridge=bridge1 interface=ether5 hw=yes
```

**==> picture [13 x 13] intentionally omitted <==**

By default, the bridge interface is configured with `protocol-mode` set to `rstp` . For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features. 

Add VLAN table entries to allow frames with specific VLAN IDs between ports: 

```
/interface ethernet switch vlan
```

```
add ports=ether2,ether3 switch=switch1 vlan-id=200
add ports=ether2,ether4 switch=switch1 vlan-id=300
add ports=ether2,ether5 switch=switch1 vlan-id=400
```

Assign `vlan-mode` and `vlan-header` mode for each port and also `default-vlan-id` on ingress for each access port: 

494 

```
/interface ethernet switch port
```

```
set ether2 vlan-mode=secure vlan-header=add-if-missing
```

```
set ether3 vlan-mode=secure vlan-header=always-strip default-vlan-id=200
set ether4 vlan-mode=secure vlan-header=always-strip default-vlan-id=300
set ether5 vlan-mode=secure vlan-header=always-strip default-vlan-id=400
```

- Setting `vlan-mode=secure` ensures strict use of the VLAN table. Setting `vlan-header=always-strip` for access ports removes the VLAN header from the frame when it leaves the switch chip. Setting `vlan-header=add-if-missing` for trunk port adds VLAN header to untagged frames. 

`default-vlan-id` specifies what VLAN ID is added for untagged ingress traffic of the access port. 

**==> picture [13 x 13] intentionally omitted <==**

On QCA8337 and Atheros8327 switch chips, a default `vlan-header=leave-as-is` property should be used. The switch chip will determine which ports are access ports by using the `default-vlan-id` property. The `default-vlan-id` should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to.
