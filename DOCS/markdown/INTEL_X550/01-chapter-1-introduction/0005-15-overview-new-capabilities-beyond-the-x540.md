## 1.5 Overview: New Capabilities Beyond the X540

### 1.5.1 NBASE-T Support

Support for 2.5GBASE-T and 5GBASE-T is added to the X550.

### 1.5.2 Filtering Capabilities

#### 1.5.2.1 Flow Director Improvements

Two new modes, based on cloud tenant ID or on MAC, VLAN are added to the X550 to allow support of
the features described below. Also supported is a better definition of the packet which are candidate to
the flow director filtering and the ability to drop candidate packets that do not match any filter.

1.5.2.2               802.1BR Support
The X550 supports the IEEE 802.1BR specification. It allows forwarding to pools based on unicast or
multicast E-tags and allow insertion and removal of the E-tag using a per pool policy.
To allow L2 filtering on top of the E-tag forwarding, the flow director may be configured to MAC, VLAN
filtering and non matching packets may be dropped.

#### 1.5.2.3 VXLAN and NVGRE Support

The X550 supports detection and off-loading of NVGRE and VXLAN packets. It provides transmit and
receive checksum off-load on both inner and outer IP headers and on TCP header. It also allows
forwarding to a specific VM within a tenant using a new flow director mode.
In the regular IP mode of the flow director, VXLAN and NVGRE flows can be differentiated from regular
IP packets and filtering based on the inner IP/L4 header is supported.

### 1.5.3 IEEE 1588 Improvements

The X550 improves the support for IEEE 1588 by adding the following features:
 • Sampling based on a fixed clock, allowing operation independent from the link speed.
 • Clock representation is divided to seconds, nanoseconds and sub-nano parts - allowing easier
   handling by software.
 • Enabling of sub-ns periodic corrections.
 • Gradual time adjustment of frequency corrections preventing single large correction. An interrupt is
   provided when the adjustment is done.
 • Support for two different target times for SDP toggling.
 • Each SDP can be associated with any 1588 functionality.
 • Allow timestamp to be received in register or embedded in packet.

333369-009                                                                                            43
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                   Introduction

### 1.5.4 Manageability

#### 1.5.4.1 DMTF MCTP Protocol Over PCIe

The X550 enables reporting and controlling all information exposed in a LOM device via NC-SI using the
MCTP protocol over PCIe in addition to SMBus. The MCTP interface over PCIe is used by the MC to
control the NIC and for pass-through traffic. In addition, the MCTP over SMBus interface can also be
used for pass-through traffic. For more information, refer to Section 11.7.

#### 1.5.4.2 NVM Structures

Management related NVM structures were updated. For further information see Chapter 6, “Non-
Volatile Memory Map”.

#### 1.5.4.3 Simplified SMBus TCO Status and Filter Setting

The TCO status in an SMBus received packet was reduced to 8 bytes and most of the information was
removed to keep only the information relevant to the MCs. See Section 11.5.11.2.1.1 for details.
In addition, a generic command was added to enable the setting of most common filtering options
independently of the actual filters implementation. See Section 11.5.11.1.7 and Section 11.5.11.1.8 for
details.

#### 1.5.4.4 Diagnostic Commands

A command was added to the legacy SMBus interface to enable querying the identity of the X550 and
the firmware versions currently running on the X550. See Section 11.5.11.2.6 for details. This
command is the SMBus counterpart of the NC-SI command described in Section 11.6.3.13.2.
