## MAC-based traffic shaping using internal Priority 

568 

The scheme where MAC-based traffic shaping is done according to internal Priority would be following: [MAC address] -> [QoS Group] -> [Priority] -> [Queue] -> [Shaper]; 

In this example, unlimited traffic will have priority 0 and limited traffic will have priority 1 with a bandwidth limit of 10Mbit. Note that CRS has a maximum of 8 queues per port. 

Create a group of ports for switching: 

```
/interface bridge
add name=bridge1
/interface bridge port
add bridge=bridge1 interface=ether6 hw=yes
add bridge=bridge1 interface=ether7 hw=yes
add bridge=bridge1 interface=ether8 hw=yes
```
