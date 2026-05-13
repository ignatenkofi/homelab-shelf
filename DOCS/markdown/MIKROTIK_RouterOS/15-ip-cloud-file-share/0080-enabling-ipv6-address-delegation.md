## Enabling IPv6 Address delegation 

Address delegation on DHCPv6 server side works almost in the exact same way as when you configure prefix server. Only difference is that you must specify in configuration address-pool instead of prefix-pool and the pool used for this server must be defined to use /128 prefix-length. Of course, you can create server which only assigns static addresses and skip using the pool. 

```
[admin@MikroTik] > ipv6/pool/print detail
Flags: D - dynamic
 0   name="myAddressPool" prefix=2001:db8:7501::/120 prefix-length=128
[admin@MikroTik] > /ipv6/dhcp-server/print detail
Flags: D - dynamic; X - disabled, I - invalid
 0    name="myDHCP" interface=ether2 prefix-pool=static-only
      address-pool=myAddressPool lease-time=3d rapid-commit=yes use-radius=no
      preference=255 dhcp-option="" route-distance=1 use-reconfigure=no
      address-lists="" duid="0x00030001b813f4840556"
```

This configuration is already enough to work with DHCPv6 clients such as, for example, RouterOS client. 

```
[admin@MikroTik] > ipv6/dhcp-client/print detail
Flags: D - dynamic; X - disabled, I - invalid
 0    interface=ether2 status=bound duid="0x00030001b123f48407f0"
      dhcp-server-v6=fe80::ba69:f4af:fe14:558 request=address
      add-default-route=no use-peer-dns=yes allow-reconfigure=no
      dhcp-options="" pool-name="" pool-prefix-length=64 prefix-hint=::/0
      prefix-address-lists="" dhcp-options=""
      address=2001:db8:7501::, 2d23h59m51s
```

However, usually end-devices as computers do not know if their network is managed by DHCP server or not. That is why DHCPv6 server configuration is combined with SLAAC functionality. You can even avoid using SLAAC in order to advertise prefix for local network device, all you need to do is advertise "managed-address-configuration" option to your network devices. 

910 

```
[admin@MikroTik] > ipv6/nd/print detail
Flags: X - disabled, I - invalid; * - default
```

```
 0    interface=ether2 ra-interval=3m20s-10m ra-delay=3s mtu=unspecified
      reachable-time=unspecified retransmit-interval=unspecified
      ra-lifetime=30m ra-preference=medium hop-limit=unspecified
      advertise-mac-address=yes advertise-dns=yes
      managed-address-configuration=yes other-configuration=no
[admin@MikroTik] > ipv6/nd/prefix/print detail
Flags: X - disabled, I - invalid; D - dynamic
 0    prefix=::/64 6to4-interface=none interface=ether2 on-link=yes
      autonomous=yes valid-lifetime=4w2d preferred-lifetime=1w
```

Now, for example, your computer which will be connected to router ether2 interface will receive advertisement message from RouterOS ND configuration stating that this network is using "managed-address-configuration" which normally on end user devices will enable DHCPv6 client requesting IPv6 address. 

Full configuration backup from the server with several comments is provided here. 

```
#Address pool to be used for 'bridge', must have prefix-length 128
/ipv6 pool
add name=myLocalLan prefix=2001:db8::/100 prefix-length=128
#DHCPv6 server with spcified 'address' pool
/ipv6 dhcp-server
add address-pool=myLocalLan interface=bridge name=myLocalServer prefix-pool=""
#We must 'advertise' that this is managed network so LAN devices use DHCPv6 clients
#RFC 4861, RFC 4862, RFC 8415 'M - Managed address configuration'
/ipv6 nd
add interface=bridge managed-address-configuration=yes
#We must enable advertising on our 'bridge' interface
#We can even add interface without specified prefix, because we here need only
#to advertise 'option' that tells this is managed network
/ipv6 nd prefix
add interface=bridge
```
