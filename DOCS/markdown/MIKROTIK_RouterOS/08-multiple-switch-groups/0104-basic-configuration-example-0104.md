## Basic Configuration Example 

In this example, we define just one QoS level - VoIP (IP Telephony) on top of the standard "Best Effort" class. Let's imagine that we have a CRS326-24G2S+ device where: 

all ports are bridged and using vlan-filtering ; sfp-sfpplus1 is a VLAN trunk connected to another switch; ether1-ether9 are dedicated ports for IP phones; ether10-ether24 are standard ports for host connection; 

First, we need to define QoS profiles. Defined `dscp` and `pcp` values that will be used in forwarded packets on egress: 

```
/interface ethernet switch qos profile
add dscp=46 name=voip pcp=5 traffic-class=5
```

Port-based QoS profile assignment on dedicated ports for IP phones applies to ingress traffic. Other Ethernet ports will use the default `profile` (where `ds cp=0` and `pcp=0` ): `/interface ethernet switch qos port set ether1 profile=voip set ether2 profile=voip set ether3 profile=voip set ether4 profile=voip set ether5 profile=voip set ether6 profile=voip set ether7 profile=voip set ether8 profile=voip set ether9 profile=voip` The trunk port receives both types of QoS traffic. We need to create VLAN priority mapping with the QoS profile and enable `trust-l2` to differentiate them: `/interface ethernet switch qos map vlan add pcp=5 profile=voip /interface ethernet switch qos port set sfp-sfpplus1 trust-l2=trust` Finally, enable QoS hardware offloading for the above settings to start working: `/interface ethernet switch set switch1 qos-hw-offloading=yes` 

It is possible to verify the port QoS settings with `print` command: 

460 

```
[admin@MikroTik] /interface/ethernet/switch/qos/port print
Columns: NAME, SWITCH, PROFILE, MAP, TRUST-L2, TRUST-L3
 # NAME          SWITCH   PROFILE  MAP      TRUST-L2  TRUST-L3  TX-MANAGER
 0 ether1        switch1  voip     default  ignore    ignore    default
 1 ether2        switch1  voip     default  ignore    ignore    default
 2 ether3        switch1  voip     default  ignore    ignore    default
 3 ether4        switch1  voip     default  ignore    ignore    default
 4 ether5        switch1  voip     default  ignore    ignore    default
 5 ether6        switch1  voip     default  ignore    ignore    default
 6 ether7        switch1  voip     default  ignore    ignore    default
 7 ether8        switch1  voip     default  ignore    ignore    default
 8 ether9        switch1  voip     default  ignore    ignore    default
 9 ether10       switch1  default  default  ignore    ignore    default
10 ether11       switch1  default  default  ignore    ignore    default
11 ether12       switch1  default  default  ignore    ignore    default
12 ether13       switch1  default  default  ignore    ignore    default
13 ether14       switch1  default  default  ignore    ignore    default
14 ether15       switch1  default  default  ignore    ignore    default
15 ether16       switch1  default  default  ignore    ignore    default
16 ether17       switch1  default  default  ignore    ignore    default
17 ether18       switch1  default  default  ignore    ignore    default
18 ether19       switch1  default  default  ignore    ignore    default
19 ether20       switch1  default  default  ignore    ignore    default
20 ether21       switch1  default  default  ignore    ignore    default
21 ether22       switch1  default  default  ignore    ignore    default
22 ether23       switch1  default  default  ignore    ignore    default
23 ether24       switch1  default  default  ignore    ignore    default
24 sfp-sfpplus1  switch1  default  default  trust     ignore    default
25 sfp-sfpplus2  switch1  default  default  ignore    ignore    default
26 switch1-cpu   switch1
```

Now incoming packets on ports ether1-ether9 are marked with a Priority Code Point (PCP) value of 5 and a Differentiated Services Code Point (DSCP) value of 46, and incoming packets on ports ether10-ether24 are marked with PCP and DSCP values of 0. When packets are incoming to sfp-sfpplus1 port, any packets with a PCP value of 5 will retain their PCP value of 5 and DSCP value of 46, while all other packets will be marked with PCP and DSCP values of 0.
