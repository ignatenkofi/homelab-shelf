## PCP based traffic scheduling 

By default, CRS1xx/CRS2xx series devices will ignore the PCP/CoS/802.1p value and forward packets based on FIFO (First-In-First-Out) manner. When the device's internal queue is not full, then packets are in a FIFO manner, but as soon as a queue is filled, then higher-priority traffic will be sent out first. Let's consider a scenario when ether1 and ether2 are forwarding data to ether3 , but when ether3 is congested, then packets are going to be scheduled, we can configure the switch to hold lowest priority packets until all higher priority packets are sent out, this is a very common scenario for VoIP type setups, where some traffic needs to be prioritized. 

To achieve such a behavior, switch together ether1 , ether2 , and ether3 ports: 

```
/interface bridge
add name=bridge1
/interface bridge port
```

```
add bridge=bridge1 interface=ether1 hw=yes
add bridge=bridge1 interface=ether2 hw=yes
add bridge=bridge1 interface=ether3 hw=yes
```
