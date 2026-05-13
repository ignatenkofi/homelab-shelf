## Introduction 

The Group Management Protocol allows any of the interfaces to become a receiver for the multicast stream. It allows testing the multicast routing and switching setups without using dedicated IGMP or MLD clients. The option is available since RouterOS v7.4 and it supports IGMP v1, v2, v3 and MLD v1, v2 protocols. 

Interfaces are using IGMP v3 and MLD v2 by default. In case IGMP v1, v2 or MLD v1 queries are received, the interfaces will fall back to the appropriate version. Once Group Management Protocol is created on the interface, it will send an unsolicited membership report (join) packet and respond to query messages. If the configuration is removed or disabled, the interface will send a leave message.
