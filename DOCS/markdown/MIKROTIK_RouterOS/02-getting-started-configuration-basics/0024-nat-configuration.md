## NAT Configuration 

At this point, PC is not yet able to access the Internet, because locally used addresses are not routable over the Internet. Remote hosts simply do not know how to correctly reply to your local address. 

The solution for this problem is to change the source address for outgoing packets to routers public IP. This can be done with the NAT rule: 

```
/ip firewall nat
  add chain=srcnat out-interface=ether1 action=masquerade
```

23 

**==> picture [13 x 13] intentionally omitted <==**

If the public interface is PPPoE, LTE, or any other type, the 'out-interface' should be set to that interface. 

Another benefit of such a setup is that NATed clients behind the router are not directly connected to the Internet, that way additional protection against attacks from outside mostly is not required.
