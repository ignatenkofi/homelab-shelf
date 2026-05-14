## IPv4 RAW Rules 

Raw IPv4 rules will perform the following actions: 

add disabled "accept" rule - can be used to quickly disable RAW filtering without disabling all RAW rules; 

- accept DHCP discovery - most of the DHCP packets are not seen by an IP firewall, but some of them are, so make sure that they are accepted; drop packets that use bogon IPs; 

- drop from invalid SRC and DST IPs; 

- drop globally unroutable IPs coming from WAN; 

drop packets with source-address not equal to 192.168.88.0/24 (default IP range) coming from LAN; 

- drop packets coming from WAN to be forwarded to 192.168.88.0/24 network, this will protect from attacks if the attacker knows the internal network; 

- drop bad ICMP, UDP, and TCP; 

accept everything else coming from WAN and LAN; 

- accept local traffic between router interfaces; 

- drop everything else, to make sure that any newly added interface (like PPPoE connection to service provider) is protected against accidental misconfiguration. 

```
/ip firewall raw
```

```
add action=accept chain=prerouting comment="defconf: enable for transparent firewall" disabled=yes
add action=accept chain=prerouting comment="defconf: accept DHCP discover" dst-address=255.255.255.255 dst-
port=67 in-interface-list=LAN protocol=udp src-address=0.0.0.0 src-port=68
```

```
add action=drop chain=prerouting comment="defconf: drop bogon IP's" src-address-list=bad_ipv4
add action=drop chain=prerouting comment="defconf: drop bogon IP's" dst-address-list=bad_ipv4
add action=drop chain=prerouting comment="defconf: drop bogon IP's" src-address-list=bad_src_ipv4
add action=drop chain=prerouting comment="defconf: drop bogon IP's" dst-address-list=bad_dst_ipv4
add action=drop chain=prerouting comment="defconf: drop non global from WAN" src-address-list=not_global_ipv4
in-interface-list=WAN
```

```
add action=drop chain=prerouting comment="defconf: drop forward to local lan from WAN" in-interface-list=WAN
dst-address=192.168.88.0/24
```

```
add action=drop chain=prerouting comment="defconf: drop local if not from default IP range" in-interface-
list=LAN src-address=!192.168.88.0/24
```

```
add action=drop chain=prerouting comment="defconf: drop bad UDP" port=0 protocol=udp
add action=jump chain=prerouting comment="defconf: jump to ICMP chain" jump-target=icmp4 protocol=icmp
add action=jump chain=prerouting comment="defconf: jump to TCP chain" jump-target=bad_tcp protocol=tcp
add action=accept chain=prerouting comment="defconf: accept everything else from LAN" in-interface-list=LAN
add action=accept chain=prerouting comment="defconf: accept everything else from WAN" in-interface-list=WAN
add action=accept chain=prerouting comment="defconf: accept local traffic between router interfaces" src-
address-type=local
```

```
add action=drop chain=prerouting comment="defconf: drop the rest"
```

Notice that we used some optional chains, the first TCP chain to drop TCP packets known to be invalid. 

737
