## Nv2-qos=frame-priority 

In this mode QoS queue is selected based on frame priority field. Note that frame priority field is not some field in headers and therefore it is valid only while packet is processed by given device. Frame priority field must be set either explicitly by firewall rules or implicitly from ingress priority by frame forwarding process, for example, from MPLS EXP bits. For more information on frame priority field see: 

EXP bit and MPLS Queuing 

WMM and VLAN priority 

Queue is selected based on frame priority according to 802.1D recommended user priority to traffic class mapping. Mapping depends on number of available queues ( Nv2-queue-count parameter). For example, if number of queues is 4, mapping is as follows (pay attention how this mapping resembles mapping used by WMM): 

priority 0,3 -> queue 0 priority 1,2 -> queue 1 priority 4,5 -> queue 2 priority 6,7 -> queue 3 

If number of queues is 2 (default), mapping is as follows: 

priority 0,1,2,3 -> queue 0 priority 4,5,6,7 -> queue 1 

If number of queues is 8 (maximum possible), mapping is as follows: 

priority 1 -> queue 0 priority 2 -> queue 1 priority 0 -> queue 2 priority 3 -> queue 3 priority 4 -> queue 4 priority 5 -> queue 5 priority 6 -> queue 6 priority 7 -> queue 7 

For other mappings, discussion on rationale for these mappings and recommended practices please see 802.1D-2004.
