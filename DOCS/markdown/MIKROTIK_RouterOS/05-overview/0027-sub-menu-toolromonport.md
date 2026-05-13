## Sub-menu: `/tool/romon/port` 

Property Description 

233 

comment (string; Default: ) Short description of the entry. cost (integer: 0..4294967295; Default: 100 ) Changes the port's cost. disabled (yes | no; Default: no ) Changes whether the entry is disabled. interface (name; Default: ) Interface name or interface-list used for RoMON. secrets (string; Default: ) List of individual port secrets used for RoMON message hashing. 

**==> picture [13 x 13] intentionally omitted <==**

A default entry with the interface-list "all" is preconfigured. This means that when the RoMON service is enabled, all interfaces are allowed to participate in the RoMON network by default. This default entry cannot be removed or enabled/disabled, but you can still modify its `cost` , set it to `forbid` participation, or configure `secrets` .
