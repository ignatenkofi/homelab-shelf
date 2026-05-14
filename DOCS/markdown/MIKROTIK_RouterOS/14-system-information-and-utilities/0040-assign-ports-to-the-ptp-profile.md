## Assign Ports to the PTP Profile 

As the final step, assign the ports that will participate in PTP. For example, lets include few sfp28 interfaces.  SFP28-12 is connected to the grandmaster clock, while SFP28-1 and SFP28-2 are connected to an ordinary clock/slave: 

```
/system ptp port add interface=sfp28-1 ptp=ptp1
/system ptp port add interface=sfp28-2 ptp=ptp1
/system ptp port add interface=sfp28-12 ptp=ptp1
```
