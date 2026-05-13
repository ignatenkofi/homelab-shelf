## ARP and Tying It All Together 

Even though IP packets are addressed using IP addresses, hardware addresses must be used to actually transport data from one host to another. 

This brings us to Address Resolution Protocol (ARP) which is used for mapping the IP address of the host to the hardware address (MAC). ARP protocol is referenced in RFC 826. 

Each network device has a table of currently used ARP entries. Normally the table is built dynamically, but to increase network security, it can be partially or completely built statically by means of adding static entries. 

**==> picture [13 x 13] intentionally omitted <==**

Address Resolution Protocol is a thing of the past. IPv6 completely eliminates use of the ARP. 

When a host on the local area network wants to send an IP packet to another host in this network, it must look for the Ethernet MAC address of destination host in its ARP cache. If the destination host’s MAC address is not in the ARP table, then the ARP request is sent to find the device with a corresponding IP address. ARP sends a broadcast request message to all devices on the LAN by asking the devices with the specified IP address to reply with its MAC address. A device that recognizes the IP address as its own returns ARP response with its own MAC address: 

153 

**==> picture [450 x 320] intentionally omitted <==**

Let's make a simple configuration and take a closer look at processes when Host A tries to ping Host C. 

At first, we add IP addresses on Host A: 

```
/ip address add address=10.155.101.225 interface=ether1
```
