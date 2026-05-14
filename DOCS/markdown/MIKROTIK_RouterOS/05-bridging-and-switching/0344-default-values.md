## Default values 

When creating a bridge or adding a port to the bridge the following are the default values that are assigned by RouterOS: 

Default bridge priority: 32768 / 0x8000 Default bridge port path cost: based on interface speed Default bridge port priority: 0x80 

- BPDU message age increment: 1 

- HelloTime: 2 Default max message age: 20 

The bridge interface setting `port-cost-mode` changes the port `path-cost` and `internal-path-cost` mode for bridged ports, utilizing automatic values based on interface speed. This setting does not impact bridged ports with manually configured `path-cost` or `internal-path-cost` properties. Below are examples illustrating the path-costs corresponding to specific data rates (with proportionate calculations for intermediate rates): 

610 

**==> picture [123 x 174] intentionally omitted <==**

**----- Start of picture text -----**<br>
Data rate Long Short<br>10 Mbps 2,000,000 100<br>100 Mbps 200,000 19<br>1 Gbps 20,000 4<br>10 Gbps 2,000 2<br>25 Gbps 800 1<br>40 Gbps 500 1<br>50 Gbps  400 1<br>100 Gbps 200 1<br>**----- End of picture text -----**<br>

For bonded interfaces, the highest `path-cost` among all bonded member ports is applied, this value remains unaffected by the total link speed of the bonding. For virtual interfaces (such as VLAN, EoIP, VXLAN), as well as wifi, wireless, and 60GHz interfaces, a `path-cost` of 20,000 is assigned for long mode, and 10 for short mode. For dynamically bridged interfaces (e.g. wifi, wireless, PPP, VPLS), the `path-cost` defaults to 20,000 for long mode and 10 for short mode. However, this can be manually overridden by the service that dynamically adds interfaces to bridge, for instance, by using the CAPsMAN `d atapath.bridge-cost` setting. RouterOS versions prior to 7.13 does not change port path cost based on the link speed, for 10M, 100M, 1000M, and 10000M link speeds the default path cost value when a port is added to a bridge was always 10 . 

The age of a BPDU is determined by how many bridges have the BPDU passed times the message age since RouterOS uses 1 as the message age increment, then the BPDU packet can pass as many bridges as specified in the `max-message-age` parameter. By default this value is set to 20 , this means that after the 20th bridge the BPDU packet will be discarded and the next bridge will become a root bridge, note that if `max-message-age=20` is set, then it is hard to predict which ports will be the designated port on the 21st bridge and may result in traffic not being able to be forwarded properly. 

**==> picture [13 x 13] intentionally omitted <==**

In case bridge filter rules are used, make sure you allow packets with DST-MAC address 01:80:C2:00:00:00 since these packets carry BPDUs that are crucial for STP to work properly.
