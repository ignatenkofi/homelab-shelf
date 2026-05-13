## Configuration for SW3: 

```
/interface bridge
add name=bridge priority=0x3000
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2
add bridge=bridge interface=ether3
```

Configuration for SW4: 

613 

```
/interface bridge
add name=bridge priority=0x4000
/interface bridge port
add bridge=bridge interface=ether1
add bridge=bridge interface=ether2 path-cost=20
add bridge=bridge interface=ether3
```

In this example, SW1 is the root bridge since it has the lowest bridge priority. SW2 and SW3 have ether1,ether2 connected to the root bridge, and ether3 is connected to SW4 . When all switches are working properly, the traffic will be flowing from ServerA through SW1_ether2, through SW2, and through SW4 to ServerB. In the case of SW1 failure, the SW2 becomes the root bridge because of the next lowest priority, indicated by the dotted line in the diagram. Below is a list of ports and their role for each switch: 

root-port - SW2_ether2, SW3_ether2, SW4_ether1 

- alternate-port - SW2_ether1, SW3_ether1, SW4_ether2 

- designated-port - SW1_ether1, SW1_ether2, SW1_ether3, SW1_ether4, SW1_ether5, SW2_ether3, SW2_ether3, SW4_ether3 

**==> picture [13 x 13] intentionally omitted <==**

Note: By the 802.1Q recommendations, you should use bridge priorities in steps of 4096. To set a recommended priority it is more convenient to use hexadecimal notation, for example, 0 is 0x0000, 4096 is 0x1000, 8192 is 0x2000, and so on (0..F).
