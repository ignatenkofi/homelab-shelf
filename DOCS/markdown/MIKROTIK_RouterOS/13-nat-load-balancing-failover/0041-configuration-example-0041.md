## Configuration example 

Let's assume that the router has two links - ether1 max bandwidth is 10Mbps and ether2 max bandwidth is 5Mbps. The first link has more bandwidth so we set it as a primary link: 

```
/interface bonding add mode=balance-tlb slaves=ether1,ether2 primary=ether1
```

**==> picture [481 x 301] intentionally omitted <==**

No additional configuration is required for the switch. The image above illustrates how balance-tlb mode works. As you can see router can communicate to all the clients connected to the switch with a total bandwidth of both links (15Mbps). But as you already know, balance-tlb is not balancing incoming traffic. In our example, clients can communicate to the router with a total bandwidth of primary link which is 10Mbps in our configuration.
