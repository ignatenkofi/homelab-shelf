## RouterOS server configuration 

Before configuring IPsec, it is required to set up certificates. It is possible to use a separate Certificate Authority for certificate management, however in this example, self-signed certificates are generated in RouterOS System/Certificates menu. Some certificate requirements should be met to connect various devices to the server: 

Common name should contain IP or DNS name of the server; SAN (subject alternative name) should have IP or DNS of the server; EKU (extended key usage) tls-server and tls-client are required. 

Considering all requirements above, generate CA and server certificates: 

```
/certificate
add common-name=ca name=ca
sign ca ca-crl-host=2.2.2.2
add common-name=2.2.2.2 subject-alt-name=IP:2.2.2.2 key-usage=tls-server name=server1
sign server1 ca=ca
```

Now that valid certificates are created on the router, add a new Phase 1 profile and Phase 2 proposal entries with pfs-group=none: 

```
/ip ipsec profile
add name=ike2
/ip ipsec proposal
add name=ike2 pfs-group=none
```

Mode config is used for address distribution from IP/Pools: 

1213 

```
/ip pool
add name=ike2-pool ranges=192.168.77.2-192.168.77.254
/ip ipsec mode-config
```

```
add address-pool=ike2-pool address-prefix-length=32 name=ike2-conf
```

Since that the policy template must be adjusted to allow only specific network policies, it is advised to create a separate policy group and template. 

```
/ip ipsec policy group
add name=ike2-policies
/ip ipsec policy
```

```
add dst-address=192.168.77.0/24 group=ike2-policies proposal=ike2 src-address=0.0.0.0/0 template=yes
```

Create a new IPsec peer entry that will listen to all incoming IKEv2 requests.
