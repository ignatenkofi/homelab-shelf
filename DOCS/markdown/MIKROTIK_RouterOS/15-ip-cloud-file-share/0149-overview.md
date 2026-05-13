## Overview 

RouterOS supports OpenFlow 1.0 and 1.3 which allows communication between the OpenFlow controller and OpenFlow agent. OpenFlow is used to centralize management of network equipment in Software Define Networks (SDNs). 

Applications on OpenFlow controller have access to switch's data-path and can perform custom tasks, like flow steering, traffic monitoring etc. 

Controller sends flows to be added in the agent's flow table. Packet lookup, modification and forwarding is done based on flow table on the agent. 

RouterOS supports OpenFlow fastpath in simple setups where " goto table" flows are not used. 

OpenFlow feature overrides regular packet processing functionality - packets that are received on interfaces that are OpenFlow switch ports, will not pass through the regular networking stack unless OpenFlow controller sets up flows that enable this. Due to this care must be taken to not disable access to the device when configuring OpenFlow. 

OpenFlow support is available as standalone openflow package. 

Currently supported basic capabilities: 

OFPC_FLOW_STATS OFPC_TABLE_STATS OFPC_PORT_STATS OFPC_GROUP_STATS 

Currently unsupported basic capabilities: 

- OFPC_IP_REASM OFPC_QUEUE_STATS OFPC_PORT_BLOCKED 

Currently not supported configuration parameters and actions (version 1): 

OFPT_SET_ASYNC OFPAT_SET_NW_SRC OFPAT_SET_NW_DST OFPAT_SET_NW_TOS OFPAT_SET_TP_SRC OFPAT_SET_TP_DST OFPAT_ENQUEUE OFPAT_VENDOR 

Currently not supported configuration parameters and actions (version 1.3): 

OFPT_SET_ASYNC OFPAT_SET_NW_TTL OFPAT_DEC_NW_TTL OFPAT_COPY_TTL_OUT OFPAT_COPY_TTL_IN
