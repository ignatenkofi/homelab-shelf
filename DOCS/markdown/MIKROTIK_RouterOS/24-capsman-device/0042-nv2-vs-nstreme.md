## Nv2 vs Nstreme 

The key differences between Nv2 and Nstreme: 

Reduced polling overhead - instead of polling each client, Nv2 AP broadcasts an uplink schedule that assigns time to multiple clients, this can be considered "group polling" - no time is wasted for polling each client individually, leaving more time for actual data transmission. This improves throughput, especially in PtMP configurations. 

- Reduced propagation delay overhead - Nv2 must not poll each client individually, this allows to create uplink schedule based on estimated distance (propagation delay) to clients such that media usage is most effective. This improves throughput, especially in PtMP configurations. More control over latency - reduced overhead, adjustable period size and QoS features allows for more control over latency in the network.
