## Site 2 (client) configuration 

1211 

Similarly to server configuration, start off by creating a new Phase 1 profile and Phase 2 proposal configurations. Since this site will be the initiator, we can use a more specific profile configuration to control which exact encryption parameters are used, just make sure they overlap with what is configured on the server-side. 

```
/ip ipsec profile
add dh-group=ecp256 enc-algorithm=aes-256 name=ike2-gre
/ip ipsec proposal
add auth-algorithms=null enc-algorithms=aes-128-gcm name=ike2-gre pfs-group=none
```

Next, create a new mode config entry with responder=no. This will make sure the peer requests IP and split-network configuration from the server. 

```
/ip ipsec mode-config
add name=ike2-gre responder=no
```

It is also advised to create a new policy group to separate this configuration from any existing or future IPsec configuration. 

```
/ip ipsec policy group
add name=ike2-gre
```

Create a new policy template on the client-side as well. 

```
/ip ipsec policy
```

```
add dst-address=192.168.99.1/32 group=ike2-gre proposal=ike2-gre src-address=192.168.99.2/32 template=yes
```

Move on to peer configuration. Now we can specify the DNS name for the server under the address parameter. Obviously, you can use an IP address as well. 

```
/ip ipsec peer
```

```
add address=n.mynetname.net exchange-mode=ike2 name=p1.ez profile=ike2-gre
```

Lastly, create an identity for our newly created peers. 

```
/ip ipsec identity
```

```
add generate-policy=port-strict mode-config=ike2-gre peer=p1.ez policy-template-group=ike2-gre secret=test
```

If everything was done properly, there should be a new dynamic policy present. 

```
/ip ipsec policy print
Flags: T - template, X - disabled, D - dynamic, I - invalid, A - active, * - default
```

```
0 T * group=default src-address=::/0 dst-address=::/0 protocol=all proposal=default template=yes
```

```
1 T group=ike2-gre src-address=192.168.99.2/32 dst-address=192.168.99.1/32 protocol=all proposal=ike2-gre
template=yes
```

```
2 DA src-address=192.168.99.2/32 src-port=any dst-address=192.168.99.1/32 dst-port=any protocol=all
action=encrypt level=unique ipsec-protocols=esp
```

```
tunnel=yes sa-src-address=192.168.90.1 sa-dst-address=(current IP of n.mynetname.net) proposal=ike2-gre ph2-
count=1
```

A secure tunnel is now established between both sites which will encrypt all traffic between 192.168.99.2 <=> 192.168.99.1 addresses. We can use these addresses to create a GRE tunnel. 

```
/interface gre
```

```
add local-address=192.168.99.2 name=gre-tunnel1 remote-address=192.168.99.1
```

Configure IP address and route to remote network through GRE interface. 

1212 

```
/ip address
add address=172.16.1.2/30 interface=gre-tunnel1
/ip route
add dst-network=10.1.101.0/24 gateway=172.16.1.1
```
