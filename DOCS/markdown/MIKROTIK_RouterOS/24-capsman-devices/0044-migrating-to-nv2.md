## Migrating to Nv2 

Using wireless-protocol setting aids in migration or evaluating Nv2 protocol in existing networks really simple and reduce downtime as much as possible. These are the recommended steps: 

- upgrade AP to version that supports Nv2, but do not enable Nv2 on AP yet. upgrade clients to version that supports Nv2 

- configure all clients with wireless-protocol=Nv2-nstreme-802.11 . Clients will still connect to AP using protocol that was used previously, because 

- AP is not changed over to Nv2 yet 

- configure Nv2 related settings on AP 

- if it is necessary to use data encryption and secure authentication, configure Nv2 security related settings on AP and clients (refer to Security in Nv2 network). 

- set wireless-protocol=Nv2 on AP. This will make AP to change to Nv2 protocol. Clients should now connect using Nv2 protocol. in case of some trouble you can easily switch back to previous protocol by simply changing it back to whatever was used before on AP. fine tune Nv2 related settings to get acceptable latency and throughput 

- implement QoS policy for maximum performance. 

The basic troubleshooting guide: 

1505 

clients have trouble connecting or disconnect with "ranging timeout" error - check that Nv2-cell-radius setting is set appropriately unexpectedly low throughput on long distance links although signal and rate is fine - try to increase tdma-period-size setting
