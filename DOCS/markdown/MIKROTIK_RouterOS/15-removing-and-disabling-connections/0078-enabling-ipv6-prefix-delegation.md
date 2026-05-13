## Enabling IPv6 Prefix delegation 

Let's consider that we already have a running DHCP server. 

To enable IPv6 prefix delegation, first, we need to create an address pool: 

```
/ipv6 pool add name=myPool prefix=2001:db8:7501::/60 prefix-length=62
```

Notice that prefix-length is 62 bits, which means that clients will receive /62 prefixes from the /60 pool. 

The next step is to enable DHCP-PD: 

```
/ipv6 dhcp-server add name=myServer prefix-pool=myPool interface=local
```

To test our server we will set up wide-dhcpv6 on an ubuntu machine: 

install wide-dhcpv6-client edit "/etc/wide-dhcpv6/dhcp6c.conf" as above 

**==> picture [13 x 13] intentionally omitted <==**

You can use also RouterOS as a DHCP-PD client. 

```
interface eth2{
send ia-pd 0;
};
id-assoc pd {
prefix-interface eth3{
sla-id 1;
sla-len 2;
};
};
```
