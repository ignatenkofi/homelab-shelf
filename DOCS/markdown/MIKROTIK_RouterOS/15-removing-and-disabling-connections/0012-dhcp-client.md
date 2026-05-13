## DHCP Client 

Summary 

```
/ip dhcp-client
```

883 

The DHCP (Dynamic Host Configuration Protocol) is used for the easy distribution of IP addresses in a network. The MikroTik RouterOS implementation includes both server and client parts and is compliant with RFC 2131. 

The MikroTik RouterOS DHCP client may be enabled on any Ethernet-like interface at a time. The client will accept an address, netmask, default gateway, and two DNS server addresses. The received IP address will be added to the interface with the respective netmask. The default gateway will be added to the routing table as a dynamic entry. Should the DHCP client be disabled or not renew an address, the dynamic default route will be removed. If there is already a default route installed prior to the DHCP client obtaining one, the route obtained by the DHCP client would be shown as invalid. 

RouterOS DHCP client asks for the following options: 

- option 1 - Subnet Mask, 

- option 3 - Gateway Addresses, option 6 - DNS Server Addresses, option 33 - Static Routes, option 42 - NTP Server Addresses, option 43 - Vendor Specific Information, option 121 - Classless Static Routes, option 138 - CAPWAP Access Controller Addresses.
