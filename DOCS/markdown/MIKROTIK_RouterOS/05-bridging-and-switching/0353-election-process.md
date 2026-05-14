## Election process 

The election process in MSTP can be divided into two sections, intra-region and inter-region. For MSTP to work properly there will always need to be a regional root, that is the root bridge inside a region, and a CIST root, that is the root bridge between regions. A regional root is the root bridge inside a region, regional root bridge will be needed to properly set up load balancing for VLAN groups inside a region. CIST root will be used to configure which ports will be alternate/backup ports (inactive) and which ports will be root ports (active). 

**==> picture [13 x 13] intentionally omitted <==**

Between regions, there is no load balancing per VLAN group, root port election process, and port blocking between MSTP regions is done the same way as in (R)STP. If CIST has blocked a port that is inside an MSTP region to prevent traffic loops between MSTP regions, then this port can still be active for IST to do load balancing per VLAN group inside an MSTP region. 

The following parameters are involved in electing a regional root bridge or root ports inside a MSTP region: 

**==> picture [511 x 141] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>priority  (integer: 0..65535 decimal format or 0x0000-0xffff  /interface bridge msti, MST Instance priority, used to elect a regional root inside an<br>hex format; Default: 32768 / 0x8000 ) MSTP region.<br>internal-path-cost  (integer: 1..200000000; Default: ) /interface bridge port, path cost to the regional root for unknown VLAN IDs (MSTI0),<br>used on a root port inside an MSTP region.<br>priority  (integer: 0..240; Default: 128 ) /interface bridge port mst-override, MST port priority for a defined MST Instance, used<br>on a bridge port on the regional root bridge.<br>internal-path-cost  (integer: 1..200000000; Default: ) /interface bridge port mst-override, MST port path cost for a defined MST Instance,<br>used on a non-root bridge port inside an MSTP region.<br>**----- End of picture text -----**<br>

615 

The following parameters are involved in electing a CIST root bridge or CIST root ports: 

**==> picture [511 x 112] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>priority  (integer: 0..65535 decimal format or 0x0000-0xffff hex format;  /interface bridge, CIST bridge priority, used to elect a CIST root bridge.<br>Default: 32768 / 0x8000 )<br>priority  (integer: 0..240; Default: 128 ) /interface bridge port, CIST port priority, used on a CIST root bridge to elect<br>CIST root ports.<br>path-cost  (integer: 1..200000000; Default: ) /interface bridge port, CIST port path cost, used on a CIST non-root bridge<br>port to elect CIST root ports.<br>**----- End of picture text -----**<br>

**==> picture [13 x 13] intentionally omitted <==**

The sequence of parameters in which MSTP checks to elect root bridge/ports is the same as in (R)STP, you can read more about it in the (R) STP Election Process section.
