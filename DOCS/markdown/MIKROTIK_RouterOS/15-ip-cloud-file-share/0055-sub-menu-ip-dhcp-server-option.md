## Sub-menu: `/ip dhcp-server option` 

With the help of the DHCP Option list, it is possible to define additional custom options for DHCP Server to advertise. Option precedence is as follows: 

radius, lease, server, network. 

This is the order in which the client option request will be filled in. 

According to the DHCP protocol, a parameter is returned to the DHCP client only if it requests this parameter, specifying the respective code in the DHCP request Parameter-List (code 55) attribute. If the code is not included in the Parameter-List attribute, the DHCP server will not send it to the DHCP client, but since RouterOS v7.1rc5 it is possible to force the DHCP option from the server-side even if the DHCP-client does not request such parameter: 

900 

```
ip/dhcp-server/option/set force=yes
```
