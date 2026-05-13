## Vlan tag override 

Per-interface VLAN tag can be overridden on per-client basis by means of access-list and RADIUS attributes (for both - regular wireless and wireless controller). 

This way traffic can be separated between wireless clients even on the same interface, but must be used with care - only "interface VLAN" broadcast /multicast traffic will be sent out. If working broadcast/multicast is necessary for other (overridden) VLANs as well, multicast-helper can be used for now (this changes every multicast packet to unicast and then it is only sent to clients with matching VLAN ids).
