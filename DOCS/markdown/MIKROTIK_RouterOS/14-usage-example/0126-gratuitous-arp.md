## Gratuitous ARP 

It is possible to create Gratuitous ARP requests in RouterOS. To do so you must use the Traffic-Generator tool, below is an example of how to generate a Gratuitous ARP request to update the ARP table on a remote device: 

```
/tool traffic-generator inject interface=ether2 \
```
