## Overview 

A queue is a collection of data packets collectively waiting to be transmitted by a network device using a pre-defined structure methodology. Queuing works almost on the same methodology used at banks or supermarkets, where the customer is treated according to its arrival. 

Queues are used to: 

limit data rate for certain IP addresses, subnets, protocols, ports, etc.; 

- limit peer-to-peer traffic; 

- packet prioritization; 

- configure traffic bursts for traffic acceleration; 

- apply different time-based limits; 

share available traffic among users equally, or depending on the load of the channel 

Queue implementation in MikroTik RouterOS is based on Hierarchical Token Bucket (HTB). HTB allows the creation of a hierarchical queue structure and determines relations between queues. These hierarchical structures can be attached at two different places, the Packet Flow diagram illustrates both input and postrouting chains. 

There are two different ways how to configure queues in RouterOS: 

- /queue simple menu - designed to ease the configuration of simple, every day queuing tasks (such as single client upload/download limitation, p2p traffic limitation, etc.). 

- /queue tree menu - for implementing advanced queuing tasks (such as global prioritization policy, and user group limitations). Requires marked packet flows from /ip firewall mangle facility. 

RouterOS provides a possibility to configure queue in 8 levels -  the first level is an interface queue from the "/queue interface" menu and the other 7 are lower-level queues that can be created in Queue Simple and/or Queue Tree.
