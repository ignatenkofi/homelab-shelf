## `/ip ipsec identity` 

```
add generate-policy=port-strict mode-config=ike2-gre peer=ike2 policy-template-group=ike2-gre secret=test
```

The server side is now configured and listening to all IKEv2 requests. Please make sure the firewall is not blocking UDP/4500 port. 

The last step is to create the GRE interface itself. This can also be done later when an IPsec connection is established from the client-side. 

```
/interface gre
```

```
add local-address=192.168.99.1 name=gre-tunnel1 remote-address=192.168.99.2
```

Configure IP address and route to remote network through GRE interface. 

```
/ip address
add address=172.16.1.1/30 interface=gre-tunnel1
/ip route
add dst-network=10.1.202.0/24 gateway=172.16.1.2
```
