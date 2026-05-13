## Explanation of attributes: 

Root path cost, all bridges have a Root Path Cost. The root bridge has a root path cost of 0. For all other Bridges, it is the sum of the Port Path Costs on the least-cost path to the Root Bridge. You can modify the local port path cost under " `/interface bridge port` ". 

The bridge identifier is a combination of "bridge priority" and "bridge MAC", configurable under " `/interface bridge` " 

Bridge port ID is a combination of "unique ID" and "bridge port priority", the unique ID is automatically assigned to the bridge port upon adding it to the bridge, it cannot be edited. It can be seen in WinBox under the "Bridge Port" "Port Number" column, or with " `/interface bridge port monitor` ", as " `port-number` ". 

611 

**==> picture [13 x 13] intentionally omitted <==**

Make sure you are using path cost and priority on the right ports. For example, setting path cost on ports that are in a root bridge has no effect, only port priority affects them. Root path cost affects ports that are facing towards the root bridge and port priority affects ports that are facing away from the root bridge. And bridge identifier doesn’t impact the device's own root port election, instead, it affects the root port election for downstream devices. 

**==> picture [13 x 13] intentionally omitted <==**

In RouterOS it is possible to set any value for bridge priority between 0 and 65535, the IEEE 802.1W standard states that the bridge priority must be in steps of 4096. This can cause incompatibility issues between devices that do not support such values. To avoid incompatibility issues, it is recommended to use only these priorities: 0, 4096, 8192, 12288, 16384, 20480, 24576, 28672, 32768, 36864, 40960, 45056, 49152, 53248, 57344, 61440.
