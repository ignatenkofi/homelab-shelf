## Dante 

Starting from RouterOS v7.15, all MikroTik QoS-Capable devices are compatible with Dante . 

Dante hardware use the following DSCP / Diffserv priority values for traffic prioritization. 

**==> picture [244 x 88] intentionally omitted <==**

**----- Start of picture text -----**<br>
Dante Priority Usage DSCP Label DSCP Value<br>High Time critical PTP events CS7 56<br>Medium Audio, PTP EF 46<br>Low (reserved) CS1 8<br>None Other traffic BE 0<br>**----- End of picture text -----**<br>


The example assumes that the switch is using its default configuration, which includes a default "bridge" interface and all Ethernet interfaces added as bridge ports, and any of these interfaces could be used for Dante. 

First, create QoS Profiles to match Dante traffic classes, there is already a pre-existing "default" profile that corresponds to Dante's None priority. 

```
/interface/ethernet/switch/qos/profile
add name=dante-ptp dscp=56 pcp=7 traffic-class=7
add name=dante-audio dscp=46 pcp=5 traffic-class=5
add name=dante-low dscp=8 pcp=1 traffic-class=0
```

Then, create a QoS mapping to match QoS profiles based on DSCP values. 

461 

```
/interface/ethernet/switch/qos/map/ip
add dscp=56 profile=dante-ptp
add dscp=46 profile=dante-audio
add dscp=8 profile=dante-low
```

Configure hardware queues to enforce QoS on Dante traffic. 

```
/interface/ethernet/switch/qos/tx-manager/queue
set [find where traffic-class>=2] schedule=strict-priority
set [find where traffic-class<2] schedule=low-priority-group weight=1
```

Dante's High and Medium priority traffic is scheduled in strict order. The devices transmits time-critical PTP packets until queue7 gets empty, then proceed with audio (queue5). Low and other traffic gets transmitted only when PTP and audio queues are empty. Since Dante does not define priority order between Low and Other traffic (usually, CS1 has lower priority than Best Effort), and the Low traffic class is reserved for future use anyway, we treat both traffic types equally by putting both into the same group with the same weight. Feel free to change the CS1/BE traffic scheduling according to the requirements if some Dante hardware in your network uses the low-priority traffic class. 

The next step is to enable trust mode for incoming Layer3 packets (IP DSCP field): 

```
/interface/ethernet/switch/qos/port
set [find] trust-l3=keep
```

Finally, enable QoS hardware offloading for the above settings to start working: 

```
/interface ethernet switch
set switch1 qos-hw-offloading=yes
```

When using Dante in multicast mode, it is beneficial to enable IGMP snooping on the switch. This feature directs traffic only to ports with subscribed devices, preventing unnecessary flooding. Additionally, enabling an IGMP querier (if not already enabled on another device in the same LAN), adjusting query intervals, and activating fast-leave can further optimize multicast performance.
