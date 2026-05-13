## Setup Procedure 

To get IPsec to work with automatic keying using IKE-ISAKMP you will have to configure policy, peer, and proposal (optional) entries. 

**==> picture [13 x 13] intentionally omitted <==**

IPsec is very sensitive to time changes. If both ends of the IPsec tunnel are not synchronizing time equally(for example, different NTP servers not updating time with the same timestamp), tunnels will break and will have to be established again.
