## 802.11 limitations for L2 bridging 

Historically 802.11 AP devices were supposed to be able to bridge frames between wired network segment and wireless, but station device was not supposed to do L2 bridging. 

Consider the following network: 

```
[X]---[AP]-(     )-[STA]---[Y]
```

where X-to-AP and STA-to-Y are ethernet links, but AP-to-STA are connected wirelessly. According to 802.11, AP can transparently bridge traffic between X and STA, but it is not possible to bridge traffic between AP and Y, or X and Y. 

802.11 standard specifies that frames between station and AP device must be transmitted in so called 3 address frame format, meaning that header of frame contains 3 MAC addresses. Frame transmitted from AP to station has the following addresses: 

destination address - address of station device, also radio receiver address radio transmitter address - address of AP 

source address - address of originator of particular frame 

Frame transmitted from station to AP has the following addresses: 

radio receiver address - address of AP 

source address - address of station device, also radio transmitter address destination address 

Considering that every frame must include radio transmitter and receiver address, it is clear that 3 address frame format is not suitable for transparent L2 bridging over station, because station can not send frame with source address different from its address - e.g. frame from Y, and at the same time AP can not format frame in a way that would include address of Y. 

802.11 includes additional frame format, so called 4 address frame format, intended for "wireless distribution system" (WDS) - a system to interconnect APs wirelessly. In this format additional address is added, producing header that contains the following addresses: 

radio receiver address radio transmitter address destination address source address 

1535 

This frame format includes all necessary information for transparent L2 bridging over wireless link. Unluckily 802.11 does not specify how WDS connections should be established and managed, therefore any usage of 4 address frame format (and WDS) is implementation specific. 

Different station modes attempt to solve shortcomings of standard station mode to provide support for L2 bridging.
