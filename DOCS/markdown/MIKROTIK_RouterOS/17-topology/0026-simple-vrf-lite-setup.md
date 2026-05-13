## Simple VRF-Lite setup 

Let's consider a setup where we need two customer VRFs that require access to the internet: 

```
/ip address
add address=172.16.1.2/24 interface=public
add address=192.168.1.1/24 interface=ether1
add address=192.168.2.1/24 interface=ether2
/ip route
add gateway=172.16.1.1
# add VRF configuration
/ip vrf
add name=cust_a interface=ether1 place-before 0
add name=cust_b interface=ether2 place-before 0
# add vrf routes
/ip route
add gateway=172.16.1.1@main routing-table=cust_a
add gateway=172.16.1.1@main routing-table=cust_b
# masquerade local source
/ip firewall nat add chain=srcnat out-interface=public action=masquerade
```

It might be necessary to ensure that packets coming in the "public" interface can actually reach the correct VRF. 

This can be solved by marking new connections originated by the VRF customers and steering the traffic by routing marks of incoming packets on the "public" interface. 

1039 

```
# mark new customer connections
/ip firewall mangle
```

```
add action=mark-connection chain=prerouting connection-state=new new-connection-mark=\
    cust_a_conn src-address=192.168.1.0/24 passthrough=no
```

```
add action=mark-connection chain=prerouting connection-state=new new-connection-mark=\
    cust_b_conn src-address=192.168.2.0/24 passthrough=no
```

```
# mark routing
/ip firewall mangle
add action=mark-routing chain=prerouting connection-mark=cust_a_conn \
    in-interface=public new-routing-mark=cust_a
add action=mark-routing chain=prerouting connection-mark=cust_b_conn \
    in-interface=public new-routing-mark=cust_b
```
