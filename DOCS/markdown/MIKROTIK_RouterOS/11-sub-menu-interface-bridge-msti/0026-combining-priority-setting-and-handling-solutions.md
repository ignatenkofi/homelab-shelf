## Combining priority setting and handling solutions 

Complex networks and different situations can be handled by combining different approaches of carrying priority information to ensure QoS and optimize the use of resources, based on the "building blocks" described above. Several suggestions: 

The fewer number of filter rules in the whole network, the better (faster). Try classifying packets only when necessary, prefer to do that on fast routers as most probably connection tracking will be required. 

- Use DSCP to carry priority information in IP packets forwarded in your network, this way you can use it when needed. 

- Use VLANs where necessary, as they also carry priority information, make sure Ethernet bridges and switches in the way are not clearing priority information in the VLAN tag. 

Remember that QoS does not improve the throughput of links, it just treats different packets differently, and also that WMM traffic over the wireless link will discriminate regular traffic in the air.
