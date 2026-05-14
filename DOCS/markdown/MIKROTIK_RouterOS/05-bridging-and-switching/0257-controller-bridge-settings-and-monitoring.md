## Controller Bridge settings and monitoring 

This section describes the Controller Bridge settings and monitoring options. 

Sub-menu: `/interface bridge port-controller` 

**==> picture [502 x 112] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>bridge  (name; Default:  n The bridge interface where ports will be extended. The CB will only enable when  bridge  and  switch properties are<br>one ) specified, otherwise, it will be in a disabled state.<br>cascade-ports  (interface Interfaces that will act as cascade ports. A bonding interface with 802.3ad or balance-xor  mode  is also supported.<br>s; Default:  none )<br>switch  (name; Default:  n The switch that will act as the CB and ensure the control and network traffic. The CB will only enable when  bridge  and<br>one ) switch  properties are specified, otherwise, it will be in a disabled state.<br>**----- End of picture text -----**<br>

After CB and PE devices are configured and connected, each PE device will be automatically visible on the device menu, use `print` and `monitor` commands to see more details. 

```
[admin@Controller] > interface bridge port-controller device print
```

```
Flags: I - inactive
```

```
 0   name="pe1" pe-mac=64:D1:54:EB:AE:BC descr="MikroTik RouterOS 6.48beta35 (testing) CRS328-24P-4S+"
control-ports=pe1-sfpplus1,pe1-sfpplus2
```

```
 1   name="pe2" pe-mac=64:D1:54:C7:3A:58 descr="MikroTik RouterOS 6.48beta35 (testing) CRS326-24G-2S+"
control-ports=pe2-sfpplus1
```

```
[admin@Controller] > interface bridge port-controller device monitor pe2
```

```
                 name: pe2
```

```
               status: active
```

```
  connected-via-ports: sfp-sfpplus1==pe1-sfpplus1,pe1-sfpplus2==pe2-sfpplus1
   connected-via-devs: controller,pe1
```

Sub-menu: `/interface bridge port-controller device` 

**==> picture [300 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>connected-via-devs  (name) Shows the connected devices in the path from PE to CB.<br>connected-via-ports  (name) Shows the connection path from PE to CB.<br>control-ports  (interfaces) PE device control ports.<br>descr  (name) Short PE device description.<br>name  (name) Automatically assigned PE device name.<br>pe-mac  (MAC address) PE device MAC address.<br>**----- End of picture text -----**<br>

541 

status (active | inactive) PE device status. 

Additionally, each PE device interface can be monitored on the port menu, use `print` and `monitor` commands to see more details. 

```
[admin@Controller] > interface bridge port-controller port print where !disabled
Flags: I - inactive, X - disabled, R - running, U - upstream-port, C - cascade-port
 #    NAME                                   DEVICE
 0 I  pe1-ether1                             pe1
 1 R  pe1-ether2                             pe1
 2 R  pe1-ether3                             pe1
 3 R  pe1-ether4                             pe1
 4  U pe1-sfpplus1                           pe1
 5 RC pe1-sfpplus2                           pe1
 6 I  pe2-ether1                             pe2
 7 R  pe2-ether2                             pe2
 8 R  pe2-ether3                             pe2
 9 R  pe2-ether4                             pe2
10  U pe2-sfpplus1                           pe2
[admin@Controller] > interface bridge port-controller port monitor [find where !disabled]
           name: pe1-ether1 pe1-ether2 pe1-ether3 pe1-ether4 pe1-sfpplus1 pe1-sfpplus2 pe2-ether1 pe2-ether2
pe2-ether3 pe2-ether4 pe2-sfpplus1
         status: unknown    link-ok    link-ok    link-ok    no-link      link-ok      unknown    link-ok
link-ok    link-ok    no-link
           rate:            1Gbps      1Gbps      1Gbps      10Gbps       10Gbps                  1Gbps
1Gbps      1Gbps      10Gbps
    port-status: not-added  ok         ok         ok         ok           ok           not-added  ok
ok         ok         ok
           pcid:            457        458        459        480          481                     509
510        511        532
```

Sub-menu: `/interface bridge port-controller port` 

**==> picture [290 x 137] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>device  (name) Automatically assigned PE device name.<br>name  (name) Automatically assigned PE port name.<br>pcid  (integer) Automatically assigned port identifier.<br>port-status  (dev-inactive | not-added | ok) PE port status.<br>rate  (bps) Data rate of the connection.<br>status  (link-ok | no-link | unknown) PE port link status.<br>**----- End of picture text -----**<br>

The Controller Bridge can monitor the PoE-out related information from Port Extenders on the port poe menu, use `print` and `monitor` commands to see more details. For more information regarding PoE-out, please visit the PoE-out manual. 

```
[admin@Controller] > interface bridge port-controller port poe print
 # NAME                                    DEVICE
 0 pe1-ether1                              pe1
 1 pe1-ether2                              pe1
 2 pe1-ether3                              pe1
 3 pe1-ether4                              pe1
 4 pe1-ether5                              pe1
 5 pe1-ether6                              pe1
 6 pe1-ether7                              pe1
...
[admin@Controller] > interface bridge port-controller port poe monitor pe1-ether2,pe1-ether3
               name: pe1-ether2 pe1-ether3
     poe-out-status: powered-on powered-on
    poe-out-voltage: 52.8V      52.9V
    poe-out-current: 123mA      95mA
      poe-out-power: 6.4W       5W
```

542
