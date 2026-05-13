## How VLAN priority works 

The VLAN priority is a 3-bit field called Priority Code Point (PCP) within a VLAN-tagged header and values are between 0 and 7. It is used for implementing QoS on bridges and switches. MikroTik devices by default are sending VLAN packets (locally generated or encapsulated) with a priority of 0. The RouterOS bridge forwards VLAN tagged packets unaltered, which means that received VLAN tagged packets with a certain VLAN priority will leave the bridge with the same VLAN priority. The only exception is when the bridge untags the packet, in this situation VLAN priority is not preserved due to the missing VLAN header. 

More details can be studied in the IEEE 802.1p specification.
