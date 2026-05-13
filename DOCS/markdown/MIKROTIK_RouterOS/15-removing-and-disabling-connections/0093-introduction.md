## Introduction 

Domain Name System (DNS) usually refers to the Phonebook of the Internet. In other words, DNS is a database that links strings (known as hostnames), such as www.mikrotik.com to a specific IP address, such as 159.148.147.196. 

A MikroTik router with a DNS feature enabled can be set as a DNS cache for any DNS-compliant client. Moreover, the MikroTik router can be specified as a primary DNS server under its DHCP server settings. When the remote requests are enabled, the MikroTik router responds to TCP and UDP DNS requests on port 53. 

When both static and dynamic servers are set, static server entries are preferred, however, it does not indicate that a static server will always be used (for example, previously query was received from a dynamic server, but static was added later, then a dynamic entry will be preferred). 

**==> picture [13 x 13] intentionally omitted <==**

When DNS server allow-remote-requests are used make sure that you limit access to your server over TCP and UDP protocol port 53 only for known hosts. 

There are several options on how you can manage DNS functionality on your LAN - use public DNS, use the router as a cache, or do not interfere with DNS configuration. Let us take as an example the following setup: Internet service provider (ISP) → Gateway (GW) → Local area network (LAN). The GW is RouterOS based device with the default configuration: 

- You do not configure any DNS servers on the "GW" DHCP server network configuration - the device will forward the DNS server IP address configuration received from `ISP` to `LAN` devices; 

- You configure DNS servers on the "GW" DHCP server network configuration - the device will give configured DNS servers to `LAN` devices (also " /ip dns set allow-remote-requests=yes" must be enabled); 

- "dns-none" configured under DNS servers on "GW" DHCP server network configuration - the device will not forward any of the dynamic DNS servers to `LAN` devices;
