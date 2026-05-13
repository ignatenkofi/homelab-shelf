## Discovery and control protocols 

Before frame forwarding on extended ports is possible, Controlling Bridge and Port Extender must discover each other and exchange with essential information. 

CB and PE enabled devices are using a neighbor discovery protocol LLDP with specific Port Extension TLV. This allows CB and PE devices to advertise their support on cascade and control ports. 

**==> picture [13 x 12] intentionally omitted <==**

CB and PE configuration can override the neighbor discovery settings, for example, if a cascade port is not included in a neighbor discovery interface list, the LLDP messages will be still sent. 

Once LLDP messages are exchanged between CB and PE, a Control and Status Protocol (CSP) over an Edge Control Protocol (ECP) will initiate. The CSP is used between CB and PE to assert control and receive status information from the associated PE - it assigns unique IDs for extended ports, controls data-path settings (e.g. port VLAN membership) and sends port status information (e.g. interface stats, PoE-out monitoring). The ECP provides a reliable and sequenced frame delivery (encoded with EtherType 0x8940). 

**==> picture [13 x 13] intentionally omitted <==**

The current CB implementation does not support any failover techniques. Once the CB device becomes unavailable, the PE devices will lose all the control and data forwarding rules.
