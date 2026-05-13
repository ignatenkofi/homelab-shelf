## Overview 

Overview 

Nv2 protocol implementation status Compatibility and coexistence with other wireless protocols How Nv2 compares with Nstreme and 802.11 

Nv2 vs 802.11 

Nv2 vs Nstreme 

Configuring Nv2 Migrating to Nv2 Nv2 AP Synchronization Configuration example QoS in Nv2 network Nv2-qos=default Nv2-qos=frame-priority Security in Nv2 network 

Nv2 protocol is a proprietary wireless protocol developed by MikroTik for use with Atheros 802.11 wireless chips. Nv2 is based on TDMA (Time Division Multiple Access) media access technology instead of CSMA (Carrier Sense Multiple Access) media access technology used in regular 802.11 devices. 

TDMA media access technology solves hidden node problem and improves media usage, thus improving throughput and latency, especially in PtMP networks. 

Nv2 is supported for Atheros 802.11n chips and legacy 802.11a/b/g chips starting from AR5212, but not supported on older AR5211 and AR5210 chips. This means that both - 11n and legacy devices can participate in the same network and it is not required to upgrade hardware to implement Nv2 in network. 

Media access in Nv2 network is controlled by Nv2 Access Point. Nv2 AP divides time into fixed size "periods" which are dynamically divided into downlink (data sent from AP to clients) and uplink (data sent from clients to AP) portions, based on the queue state on AP and clients. Uplink time is further divided between connected clients based on their requirements for bandwidth. At the beginning of each period, AP broadcasts a schedule that tells clients when they should transmit and the amount of time they can use. 

In order to allow new clients to connect, Nv2 AP periodically assigns uplink time for "unspecified" client - this time interval is then used by a fresh client to initiate registration to AP. Then AP estimates propagation delay between AP and client and starts periodically scheduling uplink time for this client in order to complete registration and receive data from client. 

Nv2 implements dynamic rate selection on a per-client basis and ARQ for data transmissions. This enables reliable communications across Nv2 links. 

For QoS Nv2 implements variable number of priority queues with built-in default QoS scheduler that can be accompanied with fine-grained QoS policy based on firewall rules or priority information propagated across network using VLAN priority or MPLS EXP bits. 

Nv2 protocol limit is 511 clients per interface.
