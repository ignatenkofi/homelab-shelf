## Dynamic Public IP 

Dynamic address configuration is the easiest option. Simply set up a DHCP client on the public interface. The DHCP client will obtain information from your Internet Service Provider (ISP), such as an IP address, DNS servers, NTP servers, and default route, making the setup process straightforward for you. 

```
/ip dhcp-client add disabled=no interface=ether1
```

After adding the client you should see the assigned address and status should be bound 

21 

```
[admin@MikroTik] > ip dhcp-client print
Columns: INTERFACE, USE-PEER-DNS, ADD-DEFAULT-ROUTE, STATUS, ADDRESS
# INTERFACE  USE-PEER-DNS  ADD-DEFAULT-ROUTE  STATUS  ADDRESS
0 ether1     yes           yes                bound   1.2.3.100/24
```
