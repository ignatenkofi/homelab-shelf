## 11.3 Packet Filtering

Since both the host operating system and BMC use the X550 to send and receive Ethernet traffic, there
needs to be a mechanism by which incoming Ethernet packets can be identified as those that should be
sent to the BMC rather than the host operating system.
There are two different types of filtering available. The first is filtering based upon the MAC Address.
With this filtering, the BMC has at least one dedicated MAC Address and incoming Ethernet traffic with
the matching MAC Address(es) are passed to the BMC. This is the simplest filtering mechanism to utilize
and it allows an BMC to receive all types traffic (including, but not limited to, IPMI, NFS, HTTP etc).
The other mechanism available utilizes a highly configurable mechanism by which packets can be
filtered using a wide range of parameters. Using this method, the BMC can share a MAC Address (and
IP Address, if desired) with the host OS and receive only specific Ethernet traffic. This method is useful
if the BMC is only interested in specific traffic, such as IPMI packets.

### 11.3.1 Manageability Receive Filtering

This section describes the manageability receive packet filtering flow. Packet reception by the X550 can
generate one of the following results:
 • Discarded.
 • Sent to host memory.
 • Sent to the external BMC.
 • Sent to both the BMC and host memory.
The decisions regarding forwarding of packets to the host and to the BMC are separate and are
configured through two sets of registers. However, the BMC may define some types of traffic as
exclusive. This traffic is forwarded only to the BMC, even if it passes the filtering process of the host.
These types of traffic are defined using the MNGONLY register (Section 8.2.2.19.8).
An example of packets that might be necessary to send exclusively to the BMC might be specific TCP/
UDP ports of a shared MAC Address or a MAC Address dedicated to the BMC. If the BMC configures the
manageability filters to send these ports to the BMC, it should configure the settings to not send them
to the host, otherwise, these ports are received and handled by the host operating system.
The BMC controls the types of packets that it receives by programming receive manageability filters.
The following filters are accessible to the BMC:

Table 11-2. Filters Accessible to BMC
                 Filters                                            Functionality                              When Reset

Filters Enable                            General configuration of the manageability filters                 LAN_PWR_GOOD

Manageability Only                        Enables routing of packets exclusively to the manageability.       LAN_PWR_GOOD

Manageability Decision Filters [7:0]      Configuration of manageability decision filters                    LAN_PWR_GOOD

MAC Address [3:0]                         Four unicast MAC manageability addresses                           LAN_PWR_GOOD

VLAN Filters [7:0]                        Eight VLAN tag values                                              LAN_PWR_GOOD

UDP/TCP Port Filters [15:0]               16 destination port values                                         LAN_PWR_GOOD

Flexible 128 bytes TCO Filter             Length and values for one flex TCO filter                          LAN_PWR_GOOD

IPv4 and IPv6 Address Filters [3:0]       IP Address for manageability filtering                             LAN_PWR_GOOD

952                                                                                                                 333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

All filtering capabilities are available on both the NC-SI and legacy SMBus interfaces. However, in NC-SI
mode, to program part of the capabilities, the Intel OEM commands described in Section 11.6.3 should
be used.
All filters are reset only on Internal Power On Reset. Register filters that enable filters or functionality
are also reset by firmware reset in NC-SI mode. These registers can be loaded from the NVM following
a reset in SMBus mode. See Section 6.2.16.3 for description of their location in the NVM map.
The high-level structure of manageability filtering is done using two steps.
1. The packet is parsed and fields in the header are compared to programmed filters.
2. A set of decision filters are applied to the result of the first step.
Some general rules apply:
 • Fragmented packets are passed to manageability but not parsed beyond the IP header.
 • Packets with L2 errors (CRC, alignment, etc.) are not forwarded to the BMC.
 • Packets longer than 2KB are filtered out.
 • The filtering relates only to the outer L3/L4 header. In tunneled packets, the inner L2, L3 and L4
   header parameters are not considered for manageability filtering.
The following sections describe the manageability filtering, followed by the final filtering rules.
The filtering rules are created by programming the decision filters as described in Section 11.3.4.

### 11.3.2 L2 Filters

#### 11.3.2.1 MAC and VLAN Filters

The manageability MAC filters allow comparison of the Destination MAC Address to one of 4 filters
defined in the MMAH and MMAL registers.
The VLAN filters allow comparison of the 12-bit VLAN tag to one of 8 filters defined in the MAVTV
registers.

#### 11.3.2.2 EtherType Filters

Manageability L2 EtherType filters allow filtering of received packets based on the Layer 2 EtherType
field. The L2 type field of incoming packets is compared against the EtherType filters programmed in
the Manageability EtherType Filter (METF; up to 4 filters); the result is incorporated into decision filters.
Each Manageability EtherType filter can be configured as pass (positive) or reject (negative) using a
polarity bit. For the reverse polarity mode to be effective and block certain type of packets, the
EtherType filter should be part of all the enabled decision filters.
An examples for usage of L2 EtherType filters is to determine the destination of 802.1X control packets.
The 802.1X protocol is executed at different times in either the management controller or by the Host.
L2 EtherType filters are used to route these packets to the proper agent.

333369-009                                                                                               953
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                         System Manageability

In addition to the flexible EtherType filters, the X550 supports 2 fixed EtherType filters used to block
NC-SI control traffic (0x88F8) and flow control traffic (0x8808) from reaching the manageability
interface. The NC-SI EtherType is used for communication between the management controller on the
NC-SI link and the X550. Packets coming from the network are not expected to carry this EtherType
and such packets are blocked to prevent attacks on the management controller. Flow control packets
should be consumed by the MAC and as such are not expected to be forwarded to the management
interface.

### 11.3.3 L3/L4 Filtering

The manageability filtering stage combines checks done at previous stages with additional L3/L4 checks
to make a the decision on whether to route a packet to the BMC. The following sections describe the
manageability filtering done at layers L3/L4 and final filtering rules.
Note:      The L3 filters do not match tunneled fields (L3, L4 or ARP).

#### 11.3.3.1 ARP Filtering

ARP filtering — The X550 supports filtering of ARP request packets (initiated externally) and ARP
responses (to requests initiated by the BMC).
In legacy SMBus mode, the ARP filters can be used as part of the ARP offload described in
Section 11.5.4. ARP offload is not specifically available when using NC-SI. However, the general filtering
mechanism is utilized to filter incoming ARP traffic as requested using the Enable Broadcast Filtering
NC-SI command.
To limit the reception of ARP packets to the ARP packets dedicated to this station (ARP target IP = BMC
IP), the ARP request/response filter can be bind to specific IP Address, by setting both the ARP
Request/Response and the IP AND bits in an MDEF filter, as the IP bit is set also if there is a match on
the target IP (the TPA field in the ARP packet) of an ARP request or an ARP response.
Note:      If the OR section of the MDEF is all cleared and one of the IPv4 address are set, ARP packets
           matching the IP Address pass the filter. If these packets should be dropped, an OR EtherType
           filter with a a value of 0x0800 (IPv4) should be added.

#### 11.3.3.2 Neighbor Discovery Filtering and MLD

The X550 supports filtering of the following ICMPv6 packets.
Neighbor Discovery packets:
      0x86 (134d) - Router Advertisement.
      0x87 (135d) - Neighbor Solicitation.
      0x88 (136d) - Neighbor Advertisement.
      0x89 (137d) - Redirect.
MLD packets:
      0x82 (130d) - MLD Query
      0x83 (131d) - MLDv1 Report
      0x84 (132d) - MLD Done
      0x8F (143d) - MLDv2 Report

954                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

The Neighbor Discovery packets has dedicated enables for each type in the decision filters. For MLD, a
single enable controls the forwarding of all the MLD packets. This means that either all the MLD packets
types are selected for reception or none of them.

#### 11.3.3.3 RMCP Filtering

The X550 supports filtering by fixed destination port numbers, port 0x26F and port 0x298. These ports
are IANA reserved for RMCP.
In SMBus mode, there are filters that can be enabled for these ports. When using NC-SI, they are not
specifically available. However, the general filtering mechanism can be utilized to filter incoming ARP
traffic.

#### 11.3.3.4 Flexible Port Filtering

The X550 implements 16 flex destination port filters. The X550 directs packets whose L4 destination
port matches to the BMC. The BMC must ensure that only valid entries are enabled in the decision
filters.

#### 11.3.3.5 IP Address Filtering

The X550 supports filtering by destination IP Address using IPv4 and IPv6 address filters. These are
dedicated to manageability. The X550 provides four IPv6 address filters or three IPv6 addresses and
four IPv4 address filters.
The IPv4 match rises also for ARP packets for which the Target IP matches the IP Address in the MIPAF4
register.

#### 11.3.3.6 Checksum Filtering

If bit MANC.EN_XSUM_FILTER is set, the X550 directs packets to the BMC only if they match all other
filters previously described as well as pass L3/L4 checksum (if it exists).
The X550 may be instructed to directs packets to the BMC only if they pass L3/L4 checksum (if they
exist) in addition to matching other filters previously described.
Enabling the XSUM filter when using the SMBus interface is accomplished by setting the Enable XSUM
Filtering to Manageability bit (MANC.EN_XSUM_FILTER). This is done using the Update Management
Receive Filter Parameters command (see Section 11.5.11.1.6), or using Set Common Filters Receive
Control Bytes (data 2:4, command 0xC2) (see Section 11.5.11.1.7).
To enable the XSUM filtering when using NC-SI, use the Enable Checksum Offloading command (see
Section 11.6.3.15).

333369-009                                                                                           955
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                          System Manageability

### 11.3.4 Flexible 128 Byte Filter

The X550 provides one flex TCO filter. This filter looks for a pattern match within the first 128 bytes of
the packet.
Flex filters are temporarily disabled when read from or written to by the host. Any packet received
during a read or write operation is dropped. Filter operation resumes once the read or write access
completes.

#### 11.3.4.1 Flexible Filter Structure

The filter is composed of the following fields:
 • Flexible Filter Length — This field indicates the number of bytes in the packet header that should
   be inspected. The field also indicates the minimal length of packets inspected by the filter. Packet
   below that length are not inspected. Valid values for this field are: 8*n, where n=1…16.
 • Data — This is a set of up to 128 bytes comprised of values that header bytes of packets are tested
   against.
 • Mask — This is a set of 128 bits corresponding to the 128 data bytes that indicate for each
   corresponding byte if is tested against its corresponding byte. The general filter is 128 bytes that
   the BMC configures; all of these bytes may not be needed or used for the filtering, so the mask is
   used to indicate which of the 128 bytes are used for the filter.
Each filter tests the first 128 bytes (or less) of a packet, where not all bytes must necessarily be tested.

#### 11.3.4.2 TCO Filter Programming

Programming each filter is done using the following commands (NC-SI or SMBus) in a sequential
manner:
1. Filter Mask and Length — This command configures the following fields:
      a. Mask — A set of 16 bytes containing the 128 bits of the mask. Bit 0 of the first byte corresponds
         to the first byte on the wire.
      b. Length — A 1-byte field indicating the length.
2. Filter Data — The filter data is divided into groups of bytes. as described below:

                   Group                           Test Bytes

                    0x0                               0-29

                    0x1                               30-59

                    0x2                               60-89

                    0x3                              90-119

                    0x4                              120-127

      Each group of bytes need to be configured using a separate command, where the group number is
      given as a parameter. The command has the following parameters:
       • Group number — A 1-byte field indicating the current group addressed.
       • Data bytes — Up to 30 bytes of test-bytes for the current group.

956                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

### 11.3.5 Configuring Manageability Filters

There are a number of pre-defined filters that are available for the BMC to enable, such as ARPs and
IPMI ports 298h 26Fh. These are generally enabled by setting the appropriate bit within the MANC
register using specific commands.
For more advanced filtering needs, the BMC has the ability to configure a number of configurable filters.
It is a two-step process to use these filters. They must first be configured and then enabled.

#### 11.3.5.1 Manageability Decision Filters

Manageability decision filters (MDEF) are a set of eight filters, each with the same structure. The
filtering rule for each decision filter is programmed by the BMC and defines which of the L2, VLAN,
EtherType and L2/L3 filters participate in decision making. Any packet that passes at least one rule is
directed to manageability and possibly to the host.
The inputs to each decision filter are:
 • Packet passed a valid management L2 exact address filter.
 • Packet is a broadcast packet.
 • Packet has a VLAN header and it passed a valid manageability VLAN filter.
 • Packet matched one of the valid IPv4 or IPv6 manageability address filters.
 • Packet is a multicast packet.
 • Packet passed ARP filtering (request or response).
 • Packet passed neighbor solicitation filtering.
 • Packet passed MLD filtering.
 • Packet passed 0x298/0x26F port filter.
 • Packet passed a valid flex port filter.
 • Packet passed a valid flex TCO filter.
 • Packet passed or failed an L2 EtherType filter.
 • Packet passed or failed Flow Control or NC-SI L2 EtherType Discard filter.
The structure of each decision filter is shown in Figure 11-2. A boxed number indicates that the input is
conditioned by a mask bit defined in the MDEF register and MDEF_EXT register for this rule. Decision
filter rules are as follows:
 • At least one bit must be set in a register. If all bits are cleared (MDEF/MDEF_EXT = 0x0000), the
   decision filter is disabled and ignored.
 • All enabled AND filters must match for the decision filter to match. An AND filter not enabled in the
   MDEF/MDEF_EXT registers is ignored. If an AND filter is preceded by a OR filter, at least one of the
   enabled OR inputs must match for the filter to pass.
 • If no OR filter is enabled in the register, the OR filters are ignored in the decision (the filter might
   still match).
 • If one or more OR filters are enabled in the register, at least one of the enabled OR filters must
   match for the decision filter to match.

333369-009                                                                                                957
                                 Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                        System Manageability

                      L2 EtherType 3           1.7

                      L2 EtherType 0           1.4

                           Flex TCO        1.24

                         Flex Port 15      1.23

                          Flex Port 0          1.8

                          Port 0x26F       0.31

                          Port 0x298       0.30            OR
                  Neighbor Discovery         0.29,
                   (134/135/136/137)       1.25- 1.27

                       ARP Request         0.27

                      ARP Response         0.28

                           Broadcast       0.25

                 L2 unicast address 0      0.21
                                                                             NC-SI L2 EtherType

                 L2 unicast address 3          0.24

                          Reserved        1.28                                    MANC[1]
                               MLD      1.29
                      L2 EtherType 0                 1.0

                      L2 EtherType 3                 1.3

                      IPv4 address 0             0.13

                      IPv4 address 3             0.16       OR
                      IPv6 address 0             0.17
                                                                       AND

                      IPv6 address 3             0.20                                                     AND
                             VLAN 0              0.5

                             VLAN 7             0.12

                           Broadcast                 0.4

                 L2 unicast address 3                0.3

                 L2 unicast address 0                                             MANC[0]
                                                     0.0

                            Multicast            0.26                         Flow Control L2 EtherType

Figure 11-2. Manageability Decision Filters

A decision filter (for any of the 8 filters) defines which of the above inputs is enabled as part of a
filtering rule. The BMC programs two 32-bit registers per rule (MDEF[7:0] & MDEF_EXT[7:0]) with the
settings as described in Section 8.2.2.19.9 and Section 8.2.2.19.5. A set bit enables its corresponding
filter to participate in the filtering decision.
In addition to the controls described above, the MDEF_EXT.APPLY_TO_HOST_TRAFFIC and
MDEF_EXT.APPLY_TO_NETWORK_TRAFFIC bits defines which traffic is compared to this filter. At least
one of these bits must be set for the filter to be valid.
If the MDEF_EXT.APPLY_TO_HOST_TRAFFIC bit is set, the traffic from the host is candidate for this
filter. If the MDEF_EXT.APPLY_TO_NETWORK_TRAFFIC bit is set, the traffic from the network is
candidate for this filter. If both bits are set, this filter is applied to all traffic.

958                                                                                                               333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.3.5.2 Exclusive Traffic

The decisions regarding forwarding of packets to the host for LAN traffic or to the LAN for host traffic
are independent from the management decision filters. However, the BMC may define some types of
traffic as exclusive. The behavior for such traffic is defined by the using the bits corresponding to the
decision filter in the MNGONLY register (one bit per each of the eight decision rules) and the
MDEF_EXT.APPLY_TO_HOST_TRAFFIC and MDEF_EXT.APPLY_TO_NETWORK_TRAFFIC bits.
Table 11-3 describes the behavior in each case. If one or more filters match the traffic and at least one
of the filters is set as exclusive, the traffic is treated as exclusive.

Table 11-3. Exclusive Traffic Behavior
                                                  Filter Matches                                      Filter Does Not Match
 Traffic Source
                              MNGONLY = 0                           MNGONLY = 1                                 N/A

From network        Traffic is forwarded to the           Traffic is forwarded only to          Traffic is forwarded to the host
                    manageability.                        manageability.                        according to host filtering
                    Traffic is forwarded to the host
                    according to host filtering

From host           Traffic is forwarded to the           Traffic is forwarded only to          Traffic is forwarded to the LAN
                    manageability and to the LAN          manageability.

Any traffic matching any of the configurable filters (see Section 11.3.5.1) can be used as filters to pass
traffic to the host.

Table 11-4. MNGONLY Register Description and Usage
 Bits       Description                                                     Default

# 0 Decision Filter 0   Determines if packets that have passed decision filter 0 are sent exclusively to the manageability path.

# 1 Decision Filter 1   Determines if packets that have passed decision filter 1 are sent exclusively to the manageability path.

# 2 Decision Filter 2   Determines if packets that have passed decision filter 2 are sent exclusively to the manageability path.

# 3 Decision Filter 3   Determines if packets that have passed decision filter 3 are sent exclusively to the manageability path.

# 4 Decision Filter 4   Determines if packets that have passed decision filter 4 are sent exclusively to the manageability path.

# 5 Unicast and         NC-SI mode:

        Mixed                Determines if unicast and mixed packets are sent exclusively to the manageability path.
                            SMBus mode:
                             Determines if packets that have passed decision filter 5 are sent exclusively to the manageability path.

# 6 Global Multicast    NC-SI mode:

                             Determines if multicast packets are sent exclusively to the manageability path.
                            SMBus mode:
                             Determines if packets that have passed decision filter 6 are sent exclusively to the manageability path.

# 7 Broadcast           NC-SI mode:

                             Determines if broadcast packets are sent exclusively to the manageability path.
                            SMBus mode:
                             Determines if ARP packets are sent exclusively to the manageability path.

 31:8   Reserved            Reserved.

When using the SMBus interface, the BMC enables these filters by issuing the Update Management
Receive Filter Parameters command (see Section 11.5.11.1.6) with the parameter of 0x0F.
The MNGONLY register is also configurable when using NC-SI using the Set Intel Filters — Manageability
Only Command (see Section 11.6.3.7.2).

333369-009                                                                                                                         959
                                        Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

All manageability filters are controlled by the BMC only and not by the LAN device driver.

#### 11.3.5.3 Global Controls

On top of the MDEF filters, the MANC register contains some global controls applied to all the packets to
be candidate for manageability filtering:
 • Receive Enable bits:
       — The RCV_TCO_EN field controls the reception of manageability traffic. It should be set only if
         one of the following bits is set also.
       — The EN_BMC2OS bit controls the reception of manageability traffic from the host.
       — The EN_BMC2NET bit controls the reception of manageability traffic from the network.
 • VLAN filtering:
      To support the NC-SI VLAN modes the following controls are provided:
       — The FIXED_NET_TYPE field controls if only VLAN tagged or VLAN un-tagged traffic is received. If
         this bit is cleared both types are received. If it is set, only the type described by the NET_TYPE
         field is accepted.
       — If set, the NET_TYPE field indicates that only VLAN tagged traffic is received, if cleared only
         packets without VLAN is accepted. This field is validated by the FIXED_NET_TYPE field.
      Both fields relates to the inner VLAN.

### 11.3.6 Filtering Programming Interfaces

The X550 provides multiple options to program the forwarding filters, depending on the interface used
and the level of flexibility needed. Table 11-5 describes the different options and points to the
description of the relevant commands.
Table 11-5. Filtering Programming Interfaces
      Interface     Flexible/Abstract                                          Description

                                          The regular NC-SI commands can be used to allow forwarding based on a dedicated
                    Abstract (dedicated   MAC Address. The list of supported commands can be found in Section 11.6.2.1. When
                      MAC Address)        using these commands, one of the two other modes can be used to add finer grain
                                          filtering.
 NC-SI (over RMII
  or over MCTP)                           This interface described in most of the subsections of Section 11.6.3.4. It uses the
                                          packet reduction commands to reduce the forwarding scope of the filters set by the
                         Flexible
                                          regular NC-SI commands and the packet addition commands to add new packet types to
                                          the forwarding rules.

                                          The Set Common filter command (Section 11.5.11.1.7) can be used to set the most
                         Abstract         common filters. When using this commands the flexible filtering interface should not be
                                          used. When sending this command, all previous filtering requests are cleared.
       SMBus
                                          The Update MNG RCV Filter Parameters (Section 11.5.11.1.6) can be used to define the
                         Flexible
                                          exact filtering rules to be applied.

960                                                                                                                   333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

### 11.3.7 Possible Configurations

This section describes ways of using management filters. Actual usage may vary.

#### 11.3.7.1 Dedicated MAC Packet Filtering

 • Select one of the eight rules for dedicated MAC filtering.
 • Load Host MAC Address to one of the management MAC Address filters and set the appropriate bit
   in field 3:0 of the MDEF register.
 • Set other bits to qualify which packets are allowed to pass through. For example:
     — Set bit 5 in MDEF to qualify with the first manageability VLAN.
     — Set relevant bits 13 to 20 in MDEF to qualify with a match to one of the IP Addresses.
     — Set any L3/L4 bits (bits 27 to 31 in MDEF and bits 16 to 23 in MDEF_EXT) to qualify with any of
       a set of L3/L4 filters.

#### 11.3.7.2 Broadcast Packet Filtering

 • Select one of the eight rules for broadcast filtering.
 • Set bit 25 in MDEF of the decision rule to enforce broadcast filtering.
 • Set other bits to qualify which broadcast packets are allowed to pass through. For example:
     — Set bit 5 in MDEF to qualify with the first manageability VLAN.
     — Set relevant bits 13 to 20 in MDEF to qualify with a match to one of the IP Addresses.
     — Set any L3/L4 bits (bits 27 to 31 in MDEF, and bits 16 to 23 in MDEF_EXT) to qualify with any of
       a set of L3/L4 filters.

#### 11.3.7.3 VLAN Packet Filtering

 • Select one of the eight rules for VLAN filtering.
 • Set bit 5 to 12 in MDEF to qualify with the relevant manageability VLANs.
 • Set other bits to qualify which VLAN packets are allowed to pass through. For example:
     — Set any L3/L4 bits (bits 27 to 31 in MDEF, and bits 16 to 23 in MDEF_EXT) to qualify with any of
       a set of L3/L4 filters.

#### 11.3.7.4 IPv6 Filtering

IPv6 filtering is done using the following IPv6-specific filters:
 • IP Unicast filtering — requires filtering for Link Local address and a Global address. Filtering setup
   might depend on whether the MAC Address is shared with the host or dedicated to manageability:
     — Dedicated MAC Address (for example, dynamic address allocation with DHCP does not support
       multiple IP Addresses for one MAC Address). In this case, filtering can be done at L2 using two
       dedicated unicast MAC filters.

333369-009                                                                                             961
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                          System Manageability

      — Shared MAC Address (for example, static address allocation sharing addresses with host). In
        this case, filtering needs to be done at L3, requiring two IPv6 address filters, one per address.
 • A neighbor Discovery filter — The X550 supports IPv6 neighbor Discovery protocol. Since the
   protocol relies on multicast packets, the X550 supports filtering of these packets. IPv6 multicast
   addresses are translated into corresponding Ethernet multicast addresses in the form of 33-33-xx-
   xx-xx-xx, where the last 32 bits of address are taken from the last 32 bits of the IPv6 multicast
   address. As a result, two direct MAC filters can be used to filter IPv6 solicited-node multicast
   packets as well as IPv6 all node multicast packets.

#### 11.3.7.5 Receive Filtering with Shared IP

When using the Legacy SMBus interface, it is possible to share the host MAC and IP Address with the
BMC. This functionality is also available when using base NC-SI using Intel OEM commands.
When the BMC shares the MAC and IP Address with the host, receive filtering is based on identifying
specific flows through port allocation. The following setting might be used when using the legacy SMBus
interface:
 • Select one of the eight rules.
 • Set a manageability dedicated MAC filter to the host MAC Address and set the matching bit (0-3) in
   the MDEF register.
 • If VLAN is used for management, load one or more management VLAN filters and set the matching
   bit (5-12) in the MDEF register.
ARP filter/neighbor Discovery filter is enabled when the BMC is responsible for handling the ARP
protocol. Set bit 27 or bit 28 in the MDEF register for this functionality.

### 11.3.8 Determining Manageability MAC Address

If the BMC wishes to use a dedicated MAC Address or configure the automatic ARP response mechanism
(only available in SMBus mode), it may be beneficial for the BMC to be able to determine the MAC
Address used by the host.
Both the NC-SI and SMBus interfaces provide an Intel OEM command to read the System MAC Address.
A possible use for this is that the MAC Address programmed at manufacturing time does not increment
by one each time, but rather by two. In this way, the BMC can read the System MAC Address and add
one to it and be guaranteed of a unique MAC Address.
Determining the IP Address being used by the host is beyond the scope of this document.

962                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability
