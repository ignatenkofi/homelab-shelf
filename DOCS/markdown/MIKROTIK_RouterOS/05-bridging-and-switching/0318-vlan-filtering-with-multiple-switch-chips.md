## VLAN filtering with multiple switch chips 

Consider the following scenario, you have a device with two or more switch chips and you have decided to use a single bridge and set up VLAN filtering (by using the `/interface ethernet switch` menu) on a hardware level to be able to reach wire-speed performance on your network. This is very relevant for RB2011 and RB3011 series devices. In this example, let's assume that you want to have a single trunk port and all other ports are access ports, for example, ether10 is our trunk port and ether1-ether9 are our access ports.
