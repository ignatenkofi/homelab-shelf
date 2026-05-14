## QoS in Nv2 network 

1506 

QoS in Nv2 is implemented by means of variable number of priority queues. Queue is considered for transmission based on rule recommended by 802.1D2004 - only if all higher priority queues are empty. In practice this means that at first all frames from queue with higher priority will be sent, and only then next queue is considered. Therefore QoS policy must be designed with care so that higher priority queues do not make lower priority queues starve. 

QoS policy in Nv2 network is controlled by AP, clients adapt policy from AP. On AP QoS policy is configured with Nv2-queue-count and Nv2-qos parameters. Nv2-queue-count parameter specifies number of priority queues used. Mapping of frames to queues is controlled by Nv2-qos parameter.
