## Configuration 

Allowing or forbidding BFD sessions can be done from the `/routing bfd configuration` menu. For example: 

```
/routing bfd configuration
add interfaces=sfp12 forbid-bfd=yes
add interfaces=static
```

Configuration entries are order sensitive, which means that in the example above we are forbidding BFD sessions explicitly on the "sfp12" interface and allowing on the rest of the interfaces belonging to the "static" interface list. 

To be able to filter multi-hop sessions, `addresses` or `address-list` properties can be used to match the destination, as well as the appropriate VRF, if a session is not running in the "main" VRF. 

```
/ip firewall address-list
add address=10.155.255.183 list=bgp_allow_bfd
add address=10.155.255.217 list=bgp_allow_bfd
```

```
/routing bfd configuration
add addresses=111.111.0.0/16 vrf=vrf1
add address-list=bgp_allow_bfd
```

Everything else that is not explicitly listed in the configuration by default is forbidden. 

1017
