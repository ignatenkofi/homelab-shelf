## Configuring Nv2 

wireless-protocol setting controls which wireless protocol selects and uses. Note that the meaning of this setting depends on the interface role (either it is AP or client) that depends on interface mode setting. Find possible values of wireless-protocol and their meaning in table below. 

**==> picture [516 x 151] intentionally omitted <==**

**----- Start of picture text -----**<br>
value AP client<br>unspecified establish nstreme or 802.11  connect to nstreme or 802.11 network based on old  nstreme  setting<br>network based on old  nstreme<br>setting<br>any same as  unspecified scan for all matching networks, no matter what protocol, connect using protocol of chosen network<br>802.11 establish 802.11 network connect to 802.11 networks only<br>nstreme establish Nstreme network connect to Nstreme networks only<br>Nv2 establish Nv2 network connect to Nv2 networks only<br>**----- End of picture text -----**<br>

1504 

**==> picture [516 x 77] intentionally omitted <==**

**----- Start of picture text -----**<br>
Nv2- establish Nv2 network scan for Nv2 networks, if suitable network found - connect, otherwise scan for Nstreme networks, if<br>nstreme- suitable network found - connect, otherwise scan for 802.11 network and if suitable network found -<br>802.11 connect.<br>Nv2- establish Nv2 network scan for Nv2 networks, if suitable network found - connect, otherwise scan for Nstreme networks and<br>nstreme if suitable network found - connect<br>**----- End of picture text -----**<br>

Note that wireless-protocol values Nv2-nstreme-802.11 and Nv2-nstreme DO NOT specify some hybrid or special kind of protocol - these values are implemented to simplify client configuration when protocol of network that client must connect to can change. Using these values can help in migrating network to Nv2 protocol. 

Most of Nv2 settings are significant only to Nv2 AP - Nv2 client automatically adapts necessary settings from AP. The following settings are relevant to Nv2 AP: 

- Nv2-queue-count - specifies how many priority queues are used in Nv2 network. For more details see QoS in Nv2 network Nv2-qos - controls frame to priority queue mapping policy. For more details see QoS in Nv2 network 

- Nv2-cell-radius - specifies distance to farthest client in Nv2 network in km. This setting affects the size of contention time slot that AP allocates for clients to initiate connection and also size of time slots used for estimating distance to client. If this setting is too small, clients that are farther away may have trouble connecting and/or disconnect with "ranging timeout" error. Although during normal operation the effect of this setting should be negligible, in order to maintain maximum performance, it is advised to not increase this setting if not necessary, so AP is not reserving time that is actually never used, but instead allocates it for actual data transfer. 

- tdma-period-size - specifies size in ms of time periods that Nv2 AP uses for media access scheduling. Smaller period can potentially decrease latency (because AP can assign time for client sooner), but will increase protocol overhead and therefore decrease throughput. On the other hand - increasing period will increase throughput but also increase latency. It may be required to increase this value for especially long links to get acceptable throughput. This necessity can be caused by the fact that there is "propagation gap" between downlink (from AP to clients) and uplink (from clients to AP) data during which no data transfer is happening. This gap is necessary because client must receive last frame from AP - this happens after propagation delay after AP's transmission, and only then client can transmit - as a result frame from client arrives at AP after propagation delay after client's transmission (so the gap is propagation delay times two). The longer the distance, the bigger is necessary propagation gap in every period. If propagation gap takes significant portion of period, actual throughput may become unacceptable and period size should get increased at the expense of increased latency. Basically value of this setting must be carefully chosen to maximize throughput but also to keep latency at acceptable levels. 

Nv2-mode - specifies to use dynamic or fixed downlink/uplink ratio. Default value is "dynamic-downlink"; 

"sync-master" - works as nv2-mode=fixed-downlink (so uses nv2-downlink-ratio), but allows slaves to sync to this master; "sync-slave" - tries to sync to master (or already synced slave) and adapt period-size and downlink ratio settings from master. 

Nv2-downlink-ratio - specifies the Nv2 downlink ratio. Uplink ratio is automatically calculated from the downlink-ratio value. When using dynamicdownlink mode the downlink-ratio is also used when link get fully saturated. Minimum value is 20 and maximum 80. Default value is 50. 

The follwing settings are significant on both - Nv2 AP and Nv2 client: 

- Nv2-security - specifies Nv2 security mode, for more details see Security in Nv2 network 

- Nv2-preshared-key - specifies preshared key to be used, for more details see Security in Nv2 network 

- nv2-sync-secret - specifies secret key for use in the Nv2 synchronization. Secret should match on Master and Slave devices in order to establish the synced state.
