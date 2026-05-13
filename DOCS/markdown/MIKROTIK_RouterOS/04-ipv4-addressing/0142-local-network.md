## Local Network 

- IP address : Mostly can stay at the default 192.168.88.1 unless your router is behind another router. To avoid IP conflict, change to 192.168.89.1 or similar 

- Netmask : In most situations can leave 255.255.255.0 

- Bridge all LAN ports : Allows your devices to communicate to each other, even if, say, your TV is connected via Ethernet LAN cable, but your PC is connected via WiFi. 

- DHCP server : Normally, you would want automatic IP address configuration in your home network, so leave the DHCP settings ON and on their defaults. 

- NAT : Turn this off ONLY if your ISP has provided a public IP address for both the router and also the local network. If not, leave NAT on. UPnP : This option enables automatic port forwarding ("opening ports to the local network" as some call it) for supported programs and devices, like your NAS disks and peer-to-peer utilities. Use with care, as this option can sometimes expose internal devices to the internet without your knowledge. Enable only if specifically needed.
