## Overview 

The MACsec (Media Access Control Security) protocol is a standard security technology employed in Ethernet networks to ensure the confidentiality, integrity, and authenticity of data transmitted over the physical medium. MACsec is defined by IEEE standard 802.1AE. 

MACsec utilizes GCM-AES-128 encryption over Ethernet and secures all LAN traffic, including DHCP, ARP, LLDP, and higher-layer protocols. 

**==> picture [13 x 13] intentionally omitted <==**

RouterOS MACsec implementation is in the early stage, it does not support dynamic key management via Dot1x (manual key configuration is required) and hardware-accelerated encryption (maximum throughput is highly limited by the device CPU).
