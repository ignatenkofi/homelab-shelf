## 15.5 KB. Further restrictions per queue are described in Section 7.1.4.

4. CRC errors before the Start Frame Delimiter (SFD) are ignored. All packets must have a valid SFD
   to be recognized by the device (even bad packets).

333369-009                                                                                             363
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                               Inline Functions

#### 7.1.1.2 CRC Strip

The X550 potentially strips the L2 CRC on incoming packets.
CRC strip is enabled by the HLREG0.RXCRCSTRP bit. When set, CRC is stripped from all received
packets.
The global CRC strip bit (HLREG0.RXCRCSTRP) must be set in the following cases were the packet
changes before being handled to the driver:
 • RSC is enabled in any queue.
 • VLAN is hidden (PFQDE.HIDE_VLAN = 1) in any queue.
 • E-tag is removed in any queue (PFQDE.STRIP_TAG is set)
 • L2 tags are stripped from packets (PFQDE.STRIP_TAG = 1) in any queue.
 • IPsec is enabled.
 • Time stamp is added to the packets in any TC (any bit of TSYNCRXCTL.TSIP_UT_EN or
   TSYNCRXCTL.TSIP_UP_EN is set).
 • Short received packets are padded (RDRXCTL.PSP is set).

### 7.1.2 Packet Filtering

A received packet goes through up to three stages of filtering as depicted in Figure 7-1. The figure
describes a switch-like structure that is used in virtualization mode to route packets between the
network port (top of drawing) and one of many virtual ports (bottom of drawing), where each virtual
port might be associated with a Virtual Machine (VM), a Virtual Machine Monitor (VMM), or the like. The
three stages are:
1. First stage — Admission Control: Ensure that the packet should be received by the port. This is
   done by a set of L2 filters and is described in detail in this section.
2. Second stage — Pooling: This stage is specific to virtualization environments and defines the
   virtual ports (called pools in this document) that are the targets for the Rx packet. A packet can be
   associated with any number of ports/pools and the selection process is described in Section 7.1.3.2.
   In non virtualization mode, this stage is skipped and all the queues used in the next stage are
   considered as part of the same default pool.
      Note:   A pool is equivalent to a VSI as defined in IEEE 802.1Qbg specification.
      Note:   FCoE packets are not expected in virtual machines, and thus bypasses the pooling
              mechanism.
3. Third stage — Queueing: A receive packet that successfully passed the Rx filters is associated
   with one of many receive descriptor queues as described in Section 7.1.3.

364                                                                                                333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                                                   L2 Filters

                                                  Pool Select

                                                  Queue Select

Figure 7-1.    Stages in Packet Filtering - Virtualization Mode

The receive packet filtering role is to determine which of the incoming packets are allowed to pass to
the local machine and which of the incoming packets should be dropped since they are not targeted to
the local machine. Received packets that are targeted for the local machine can be destined to the host,
to a manageability controller, or to both. This section describes how host filtering is done, and the
interaction with management filtering.
As depicted in Figure 7-2, host filtering is done in two stages:
1. Packets are filtered by L2 filters (Ethernet MAC Address, unicast/multicast/broadcast). See
   Section 7.1.2.1.
2. Packets are filtered by VLAN if a VLAN tag is present. See Section 7.1.2.2.
A packet is not forwarded to the host if any of the following occurs:
 • The packet does not pass L2 filters, as described in Section 7.1.2.1.
 • The packet does not pass VLAN filtering, as described in Section 7.1.2.2.
 • The packet passes manageability filtering and the manageability filters determine that the packet
   should not pass to the host (see MNGONLY register and Section 11.3.5.2).

333369-009                                                                                           365
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

                                                     Receive Packet

                                                         Filter
                                              Fail

                                                          L2
                                                              Pass

                                                         VLAN
                                                         Filter

                                                                             MNG
                                                                             Filter
                                             Fail

                                                              Pass

                                                                      Pass

                                                                      MNGONLY

                                                                             To MNG
                                   Discard              To Host
                                   Packets

Figure 7-2.   Rx Filtering Flow Chart

#### 7.1.2.1 L2 Filtering

A packet passes successfully through L2 Ethernet MAC Address filtering if any of the following
conditions are met:
 • Unicast packet filtering — Promiscuous unicast filtering is enabled (FCTRL.UPE = 1b) or the
   packet passes unicast MAC filters (host).
 • Multicast packet filtering — Promiscuous multicast filtering is enabled (FCTRL.MPE = 1b) or the
   packet matches one of the multicast filters.
 • Broadcast packet filtering to host — Promiscuous multicast filtering is enabled (FCTRL.MPE =
   1b) or Broadcast Accept Mode is enabled (FCTRL.BAM = 1b).

7.1.2.1.1            Unicast Filter

The Ethernet MAC Address is checked against the 128 host unicast addresses and 4 KB hash-based
unicast address filters (if enabled). The host unicast addresses are controlled by the host interface. The
destination address of an incoming packet must exactly match one of the pre-configured host address
filters. These addresses can be unicast or multicast. Those filters are configured through Receive
Address Low (RAL), Receive Address High (RAH), In addition, there are 4 KB unicast hash filters used
for host defined by the PFUTA registers. The unicast hash filters are useful mainly for virtualization
settings in those cases that more than 128 filters might be required.
Promiscuous Unicast — Receive all unicasts. Promiscuous unicast mode is usually used when the LAN
device is used as a sniffer.

366                                                                                                                  333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.1.2.1.2              Multicast Filter (Partial)

The 12-bit portion of the incoming packet multicast address must be set in the multicast filter address
table (MTA) to pass the partial multicast filter. The bits (out of 48 bits of the destination address) used
to index the MTA table can be selected by the MO field in the MCSTCTRL register.
Promiscuous Multicast — Receive all multicasts. Promiscuous multicast mode is usually used when the
LAN device is used as a sniffer.

#### 7.1.2.2 VLAN Filtering

The X550 provides exact VLAN filtering as follows:
 • Host VLAN filters are programmed by the VFTA[n] registers.
 • A VLAN match might relate to the DEI bit in the VLAN header. It is enabled for host filtering only by
   the VLNCTRL.DEIEN while the expected value is defined by the VLNCTRL.DEI.
If double VLAN is enabled (see Section 7.4.5), filtering is done on the second (internal) VLAN tag. All
the filtering functions of the X550 ignore the first (external) VLAN in this mode.
A receive packet that passes MAC Address filtering successfully is subjected to VLAN header filtering as
illustrated in Figure 7-3:
1. If the packet does not have a VLAN header, it passes to the next filtering stage.
2. Else, if VLAN filters are not enabled (VLNCTRL.VFE = 0b), the packet is forwarded to the next
   filtering stage.
3. Else, if the packet matches an enabled VLAN filter and DEI checking (if enabled), the packet is
   forwarded to the next filtering stage.
4. Otherwise, the packet is dropped.

                                                        MAC Address Filtering

                                                   NO        Packet has
                                                            VLAN header
                                                                                VLNCTRL.VFE
                                                                   YES             is set

                                                  NO         Host VLAN
                                                               filtering
                                                             is enabled
                                                                                Match to a valid
                                                                   YES             VFTA[n]

                                                  YES     Pass host VLAN
                                                              filtering

                                                                    NO

                                                        FAIL - Discard Packet
                       Pass – to Host Filtering

Figure 7-3.    VLAN Filtering

333369-009                                                                                              367
                                    Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                  Inline Functions

#### 7.1.2.3 E-tag Filtering

If the PFVTCTL.POOLING_MODE is E-tag (01b), special L2 filtering rules are applied to tagged packets.
 • If the tag matches one of the RAH registers used for tag filtering (RAH.ADTYPE = 1), it is
   considered as a packet that passed L2.
 • If the FCTRL.TPE bit is set (Tag Promiscuous Enable), all the tagged packets pass L2 filtering.
 • Otherwise, packets with E-tag (if PFVTCTL.POOLING_MODEis E-tag (01b)) are dropped.
Note:     E-tag packets are not expected when double VLAN are use, thus PFVTCTL.POOLING_MODE
          should be cleared if CTRL_EXT.EXTENDED_VLAN is set.

#### 7.1.2.4 Manageability/Host Filtering

The host and manageability filtering process are mostly independent. Each entity defines which packet
it should receive. The only exception is that the manageability filters can define a packet as exclusive
and thus prevent it from reaching the host. See Section 11.3.5.2 for details. Figure 7-4 describes this
flow.

                               MNG Filtering
                                                                Host Filtering

                                                Exclusive to
                                                   MNG
                                               (MNGONLY)?      YES

                               Packet to MNG                    Packet to Host

Figure 7-4.   Manageability/Host Filtering

368                                                                                                   333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.1.3 Rx Queues Assignment

The following filters/mechanisms determine the destination of a received packet. These filters are
described briefly while more detailed descriptions are provided in the following sections:
 • Virtualization — In a virtual environment, DMA resources are shared between more than one
   software entity (operating system and/or device driver). This is done by allocating receive
   descriptor queues to virtual partitions (VMM, IOVM, VMs, or VFs). Allocating queues to virtual
   partitions is done in sets, each with the same number of queues, called queue pools, or pools.
   Virtualization assigns to each received packet one or more pool indices. Packets are routed to a pool
   based on their pool index and other considerations such as DCB and RSS. See Section 7.1.3.2 for
   more on routing for virtualization.
 • DCB — Data Center Bridging (DCB) provides QoS through priority queues, priority flow control, and
   congestion management. Packets are classified into one of several (up to eight) Traffic Classes
   (TCs). Each TC is associated with a single unique packet buffer. Packets that reside in a specific
   packet buffer are then routed to one of a set of Rx queues based on their TC value and other
   considerations such as RSS and virtualization. See Section 7.6 for details on DCB.
     — DCB is enabled via the DCB_ENA bit
 • Receive Side Scaling (RSS) — RSS distributes packet processing between several processor
   cores by assigning packets into different descriptor queues. RSS assigns to each received packet an
   RSS index. Packets are routed to one queue from a set of Rx queues based on their RSS index and
   other considerations such as DCB and virtualization. See Section 7.1.3.7 for details.
 • L2 EtherType Filters — These filters identify packets by their L2 EtherType and assigns them to
   receive queues. Examples of possible uses are LLDP packets, and 802.1X packets. See
   Section 7.1.3.3 for details. The X550 incorporates eight EtherType filters.
 • FCoE Redirection Table — FCoE packets that match the L2 filters might be directed to a single
   legacy Rx queue or multiple queues to ease multi-core processing. See Section 7.1.3.4 for details.
   See also Section 7.11.3.3 for Large FC receive and direct data placement. Up to 64 queues (any 64
   of the 128 queues) can be allocated for FCoE traffic by the FCoE redirection table defined by
   FCRETA[n] registers.
 • Flow Director Filters — These filters that provide up to additional 32 K filters. See Section 7.1.3.6
   for details.
 • TCP SYN Filters — The X550 might route TCP packets with their SYN flag set into a separate
   queue. SYN packets are often used in SYN attacks to load the system with numerous requests for
   new connections. By filtering such packets to a separate queue, security software can monitor and
   act on SYN attacks. See Section 7.1.3.5 for details.
A received packet is allocated to a queue based on the above criteria and the following order:
 • Queue by L2 EtherType filters (if match)
 • Queue by FCoE redirection table (relevant for FCoE packets)
 • Queue by SYN filter (if match)
 • Queue by flow director filters
 • Queue (in case of virtualization, within a pool) by DCB and/or RSS as described in Section 7.1.3.1
   and Section 7.1.3.2.
 • Send to queue zero.

333369-009                                                                                           369
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

#### 7.1.3.1 Queuing in a Non-virtualized Environment

Table 7-1 lists the queuing schemes for packets that do not match any special filters (L2 EtherType,
FCoE redirection, SYN and flow director filters). Table 7-2 illustrates the queue indexing. Selecting a
scheme is done via the Multiple Receive Queues Enable (MRQE) field in MRQC register.

Table 7-1.        Rx Queuing Schemes Supported (No Virtualization)
         DCB                    RSS                       DCB/RSS Queues                               Special Filters1

          No                    No            1 queue                                                      Supported
                                              Rx queue 0

          No                    Yes           64 RSS queues                                                Supported

         Yes                    No            8 TCs x 1 queue                                              Supported

# 4 TCs x 1 queue

                                              Assign Rx queue 0 of each TC

         Yes                    Yes           8 TCs x 16 RSS                                               Supported

# 4 TCs x 32 RSS

1. Special filters include: L2 filters; FCoE redirection; SYN filter. When possible it is recommended to assign Rx queues not used by
   the DCB / RSS queues.

Table 7-2.        Queue Indexing Illustration in Non-virtualization Mode
   MRQC.MRQE              Queue Index Bits              6           5           4           3          2            1          0

       0000b                  Default only                                                  0

       0001b                      RSS                                                           RSS

       0101b                 DCB(4) + RSS                     TC                                      RSS1

       0011b                    DCB(4)                        TC                                       0

       0100b                 DCB(8) + RSS                          TC                                        RSS1

       0010b                    DCB(8)                             TC                                         0

1. The number of bits used for each TC is set according to the RQTC.RQTCx fields

A received packet is assigned to a queue according to the ordering shown in Figure 7-5:
 • DCB and RSS filters — Packets that do not meet any of the previous filtering conditions described in
   Section 7.1.3 are assigned to one of 128 queues as listed in Table 7-1. The following modes are
   supported:
      — No DCB, No RSS — Queue 0 is used for all packets.
      — RSS only — A set of 64 queues is allocated for RSS. The queue is identified through the RSS
        index. Note that it is possible to use a subset of these queues.
      — DCB only — A single queue is allocated per TC to a total of eight queues (if the number of TCs
        is eight), or to a total of four queues (if the number of TCs is four). The queue is identified
        through the TC index.
      — DCB with RSS — A packet is assigned to one of 128 queues (8 TCs x 16 RSS or 4 TCs x 32
        RSS) through the DCB traffic class of the packet and the RSS index. The TC index is used as the
        MS bits of the Rx queue index, and the LS bits are defined by the RSS index. The number of
        queues used for each TC are set according to the RQTC.RQTCx fields

370                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

When operating in conjunction with DCB, the number of RSS queues can vary per DCB TC. Each TC can
be configured to a different number of RSS queues (1/2/4/8/16/32 queues). The output of the RSS
redirection table is masked accordingly to generate an RSS index of the right width. When configured to
less than the maximum number of queues, the respective MS bits of the RSS index are set to zero. The
number of RSS queues per TC is configured in the RQTC register.
 • Example — Assume a 4 TCs x 32 RSS configuration and that the number of RSS queues for TC=3 is
   set to 4. The queue numbers for TC=3 are 64, 65, 66, and 67 (decimal).
Figure 7-5 depicts the flow of allocation of Rx queues by the various queue filters previously described:

                                                   Rx Packet

                                                   Match L2      Yes      Rx queue is defined by
                                                    filters                the L2 Ethertype filter
                  Note: Filter Match in this flow
                  diagram means that Rx packets
                                                            No
                  match filters that assigns Rx queue
                  for these packets                              Yes
                                                    Match FCoE                Rx queue is defined
                                                       filters                by the FCoE filters

                                                         No

                                                  Match SYN      Yes          Rx queue is defined
                                                     filter                    by the SYN filter

                                                         No
                                                    Match        Yes       Rx queue is defined by
                                                 Flow Director
                                                                           the Flow Director filters
                                                    filters
                                                         No

                   If(Packet match RSS criteria and RSS enabled) RSS Index = RSS queue
                   If(DCB Enabled)                               TC Index = RX User                    Rx Queue
                                                                 Priority to TC Mapping                Assigned
                   Queue num = TC Index | RSS Index

Figure 7-5.    Rx Queuing Flow (Non-virtualized)

#### 7.1.3.2 Queuing in a Virtualized Environment

The 128 Rx queues are allocated to a pre-configured number of queue sets, called pools. In non-IOV
mode, system software allocates the pools to the VMM or to VMs. In IOV mode, each pool may be
associated with a VF.
Incoming packets are associated with pools based on their L2 characteristics as described in
Section 7.8.3. This section describes the following stage, where an Rx queue is assigned to each
replication of the Rx packet as determined by its pools association.
Table 7-3 lists the queuing schemes supported with virtualization. Table 7-4 lists the queue indexing.

333369-009                                                                                                        371
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

Table 7-3.          Rx Queuing Schemes Supported with Virtualization
          DCB                   RSS                       DCB/RSS Queues                               Special Filters1

          No                    No            16 pools x 1 queue                                           Supported
                                              32 pools x 1 queue
                                              64 pools x 1 queue
                                               - Rx queue 0 of each pool

          No                    Yes           32 pools x 4 RSS                                             Supported
                                              64 pools x 2 RSS

          Yes                   No            16 pools x 8 TCs                                             Supported
                                              32 pools x 4 TCs

          Yes                   Yes           N/A                                                             N/A

1. Special filters include: L2 filters; FCoE redirection; SYN filter. When possible it is recommended to assign Rx queues not used by
   the DCB / RSS queues.

Table 7-4.          Queue Indexing Illustration in Virtualization Mode
   MRQC.MRQE              Queue Index Bits              6           5           4           3          2            1          0

        1000b                                                                     Pool Index                                    0

        1011b                VT(64) + RSS                                         Pool Index                                   RSS

                                                                                                                  VF
      1001b/1111b     VT(64) + RSS + Mega Pool                             Pool Index                           Index/         RSS
                                                                                                                 RSS1

        1010b                VT(32) + RSS                                  Pool Index                                    RSS

         N/A                 VT(16) + RSS                                            Not Supported

        1101b              VT(32) + DCB(4)                                 Pool Index                                     TC

        1100b              VT(16) + DCB(8)                           Pool Index                                     TC

1. When MRQC.MRQE = 0xF, VF index for pools 0-59, part of RSS for pool 60, 62 and pools 61 and 63 are disabled.When MRQC.MRQE
   = 0x0, VF index for pools 0-61, part of RSS for pool 62 and pool 63 is disabled.

Selecting a scheme is done in the following manner:
 • Non-IOV mode
        — Select one of the above schemes via the Multiple Receive Queues Enable field in the MRQC
          register.
 • IOV mode
        — Determine the number of pools: the number must support the value configured by the
          operating system in the PCIe NumVFs field (see Section 9.2.4.4.5). Therefore, the number of
          pools is min. of {16, 32, 64} that is still >= NumVFs.
        — Determine DCB mode via the DCB_ENA bit in MTQC register.

372                                                                                                                       333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

A received packet is assigned to an absolute queue index according to the ordering shown in
Figure 7-6). It is software responsibility to define a queue that belongs to the matched pool:
 • DCB and RSS filters — The supported modes are listed in Table 7-3 and detailed as follows. The
   associated queue indexes are listed in Table 7-4.
     — No DCB, No RSS — A single queue is used as default queue of the pool with either 16, 32, or
       64 pools enabled. In a 64 pools setting, queues '2xN'...'2xN+1' are allocated to pool 'N'; In a 32
       pools setting, queues '4xN'...'4xN+3' are allocated to pool 'N'. The queues not used as default
       may be directed to by other filters.
     — RSS only — All 128 queues are allocated to pools. Configurations supported:
          • 32 pools with 4 RSS queues each
          • 64 pools with 2 RSS queues each.
          • 63 pools. The first 62 with 2 queues each and the last one with 4 RSS queues.In this mode
            the last pool is 62 and pool 63 is disabled.
          • 62 pools. The first 60 with 2 queues each and the last two with 4 RSS queues each. In this
            mode the last two pools are 60 and 62 and pools 61/63 are disabled.
             Note:      It is possible to use a subset of the RSS queues in each pool. The LS bits of the
                        queue indexes are defined by the RSS index, and the pool index is used as the MS
                        bits.See description below.
             Note:      In the 62 and 63 pools modes, the pools with 4 queues should be assigned to the
                        PF and can not be assigned to a VF.
     — DCB only — All 128 queues are allocated to pools. Two configurations are supported: 16 pools
       with 8 TCs each or 32 pools with 4 TCs each. The LS bits of the queue indexes are defined by
       the TC index, and the pool index is used as the MS bits.
     — DCB and RSS — All 128 queues are allocated to pools. One configuration is supported: 16
       pools with 4 TCs each TC with 2 RSS queues. The LS bit of the queue indexes is defined by the
       RSS index, the next 2 bits of the queue indexes are defined by the TC index, and the pool index
       is used as the MS bits.
When operating in conjunction with RSS, the number of RSS queues can vary per pool as defined by the
PSRTYPE[n].RQPL. Each pool can be configured to a different number of RSS queues (1/2/4- queues)
up to the maximum possible queues in the selected mode of operation. The output of the RSS
redirection table is masked accordingly to generate an RSS index of the right width. When configured to
less than the maximum number of queues, the respective MS bits of the RSS index are set to zero.

333369-009                                                                                            373
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

                                                         Rx Packet

                                                          Match L2      Yes   Rx queue is defined by the
                                                           filters                L2 Ethertype filter

                                                                No

                                                         Match FCoE     Yes   Rx queue is defined by the
                                                            filters                 FCoE filters
              Note: Filter Match in this flow diagram
              means that Rx packets match filters that          No
              assigns Rx queue for these packets
                                                         Match SYN      Yes   Rx queue is defined by the
                                                            filter                   SYN filter

                                                                No

                                                         VT pool list   Yes
                                                                                    Discard packet
                                                           empty

                                                                No
                                                        Match
                                                                        Yes   Rx queue is defined by the
                                                     Flow Director
                                                                                 Flow Director filters
                                                        filters
                                                               No
              If(Packet match RSS criteria and RSS enabled) Queue Index = RSS queue
                                                                                                           Rx Queue
              If(DCB Enabled and VLAN header present)       Queue Index = RX User Priority to TC
                                                                                                           Assigned
                                                                           Mapping
              Queue num = VT Pool Index | Queue Index

Figure 7-6.   Rx Queuing Flow (Virtualization Case)

#### 7.1.3.3 L2 EtherType Filters

These filters identify packets by their L2 EtherType, 802.1Q user priority and optionally assign them to
a receive queue. The following possible usages have been identified at this time:
 • DCB LLDP packets — Identifies DCB control packets
 • IEEE 802.1X packets — Extensible Authentication Protocol (EAPOL) over LAN
 • Time sync packets (such as IEEE 1588) — Identifies Sync or Delay_Req packets
 • FCoE packets (possibly two UP values)
 • The L2 type filters should not be set to IP packet type as this might cause unexpected results
The X550 incorporates eight EtherType filters defined by a set of two registers per filter: ETQF[n] and
ETQS[n].
The L2 packet type is defined by comparing the EtherType field in the Rx packet with the
ETQF[n].ETYPE (regardless of the pool and UP matching). The Packet Type field in the Rx descriptor
captures the filter number that matched with the L2 EtherType. See Section 7.1.5.2.2 for a description
of the Packet Type field.

374                                                                                                                   333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

The following flow is used by the EtherType filters:
1. If the ETQF.FILTER_ENABLE bit is cleared, the filter is disabled and the following steps are ignored.
2. Receive packet matches any ETQF filters if the EtherType field in the packet matches the ETYPE
   field of the filter. Note that the following steps are ignored if the packet does not match the ETQF
   filters.
    Note:      EtherType Filters should not be configured in a way that may cause a packet to match
               multiple filters.
3. Packets that match any ETQF filters are candidate for the host. If the packet also matches the
   manageability filters, it is directed to the host as well regardless of the MNGONLY register setting.
4. If the ETQF.FCOE field is set, the packet is identified as an FCoE packet.
5. If the ETQF.IEEE_1588_TIME_STAMP field is set, the packet is identified as an IEEE 1588 packet.
6. If the ETQS.QUEUE_ENABLE bit is cleared, the filter completed its action on the packet. Else, the
   filter is also used for queuing purposes as described in the sections that follow.
7. If the ETQF.POOL_ENABLE field is set, the Pool field of the filter determines the target pool for the
   packet. The packet can still be mirrored to other pools as described in Section 7.8.3. See the
   sections that follow for more details on the use of the Pool field.
8. The ETQS.RX_QUEUE field determines the destination queue for the packet. In case of a mirrored
   packet, only the copy of the packet that is targeted to the pool defined by the Pool field in the ETQF
   register is routed according to the Rx Queue field.
Setting the ETQF[n] registers is described as follows:
 • The FILTER_ENABLE bit enables identification of Rx packets by EtherType according to this filter. If
   this bit is cleared, the filter is ignored.
 • The ETYPE field contains the 16-bit EtherType compared against all L2 type fields in the Rx packet.
 • The FCOE bit indicates that the EtherType defined in the EType field is an FCoE EType. Packets that
   match this filter are identified as FCoE packets.
 • The IEEE_1588_TIME_STAMP bit indicates that the EtherType defined in the EType field is identified
   as IEEE 1588 EType. Packets that match this filter are time stamped according to the IEEE 1588
   specification.
 • The Pool field defines the target pool for a packet that matches the filter.
     — It applies only in virtualization modes. The pool index is meaningful only if the POOL_ENABLE
       bit is set.
     — If the POOL_ENABLE bit is set, the QUEUE_ENABLE bit in the ETQS register must be set as well.
       In this case, the RX_QUEUE field in the ETQS must be part of the pool number defined in the
       ETQF.
Setting the ETQS[n] registers is described as follows:
 • The QUEUE_ENABLE bit enables routing of the Rx packet that match the filter to Rx queue as
   defined by the RX_QUEUE field.
 • The RX_QUEUE field contains the destination queue (one of 128 queues) for the packet.

333369-009                                                                                            375
                                 Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                    Inline Functions

Special considerations for virtualization modes:
 • Packets that match an EtherType filter are diverted from their original pool (as defined by the VLAN
   and Ethernet MAC Address filters) to the pool defined in the Pool field in the ETQF registers.
 • The same applies for multicast packets. A single copy is posted to the pool defined by the filter.
 • Mirroring rules
      — A packet sent to a pool by an ETQF filter, is still candidate to mirroring using the standard
        mirroring rules.
      — The EtherType filter does not take part in the decision on the destination of the mirrored packet.

#### 7.1.3.4 FCoE Redirection Table

The FCoE redirection table is a mechanism to distribute received FCoE packets into several descriptor
queues. Software might assign each queue to a different processor, sharing the load of packet
processing among multiple processors. The FCoE redirection table assigns Rx queues to packets that
are identified as FCoE in the ETQF[n] registers but not assigned to queues in the ETQS[n] registers.
Figure 7-7 illustrates the computing of the assigned Rx queue index by the FCoE redirection table.
 • The receive packet is parsed and the OX_ID is extracted for the filtering to Rx LAN queue (named
   as EX_ID).
 • The six LS bits of the OX_ID are used as an address to the redirection table (FCRETA[n] register
   index).
 • The FCoE redirection table is enabled by the FCRECTL.ENA bit. If enabled, the content of the
   selected FCRETA[n] register is the assigned Rx queue index.
 • FCoE Packets with SNAP header are routed according to FCRETA[0].TABLE_ENTRY.
 • If the FCoE redirection table is disabled, FCoE packets are assigned to queue 0.

                     Rx OX_ID                                      Redirection Table

    0 FCRETA[0].TABLE_ENTRY

    1 FCRETA[1].TABLE_ENTRY

                     16                                  ...   ...

    6 LS bits       31    FCRETA[31].TABLE_ENTRY

    32 FCRETA[0].TABLE_ENTRY_HIGH

    11 LS bits                          ...   ...

    63 FCRETA[31].TABLE_ENTRY_HIGH

                                                                                7
                      Flow ID
                                                                        Assigned Rx Queue
                                                                              Index
Figure 7-7.    FCoE Redirection Table

376                                                                                                     333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.1.3.5 SYN Packet Filters

The X550 might route TCP packets whose SYN flag is set into a separate queue. SYN packets are used
in SYN attacks to load the system with numerous requests for new connections. By filtering such
packets to a separate queue, security software can monitor and act on SYN attacks.
The following rules apply:
 • A single SYN filter is provided.
The SYN filter is configured via the SYNQF register as follows:
 • The QUEUE_ENABLE bit enables SYN filtering capability.
 • The RX_QUEUE field contains the destination queue for the packet (one of 128 queues). In case of
   mirroring (in virtualization mode), only the original copy of the packet is routed according to this
   filter.

#### 7.1.3.6 Flow Director Filters

The flow director filters identify specific flows or sets of flows and routes them to specific queues. The
flow director filters are programmed by FDIRCTRL and all other FDIR registers. The X550 shares the Rx
packet buffer for the storage of these filters.
The X550 supports three different modes of flow director (set in the FDIRCTRL.FILTERMODE field -
Section 8.2.2.15.1):
 • IP filtering (000b)
 • MAC, VLAN filtering (001b)
 • Cloud: NVGRE or VXLAN filtering (010b)
Table 7-5 describes the packets that are candidate to compared to the flow director filters according to
the different modes:

Table 7-5.       Candidate for Flow Director per Mode
                          IP packets
                                                                                                       Other IP packets
        Mode            TCP/UDP/SCTP         Non IP Packets      NVGRE Packets        VXLAN packets
                                                                                                       or Fragmented IP
                        (Not Tunneled)

 00 - IP                    Candidate         Not Candidate          Candidate            Candidate      Not Candidate
 (L4 fields unmasked)                                               (inner IP)1          (inner IP)1

 00 - IP                    Candidate         Not Candidate         Candidate            Candidate       Candidate2’3
 (L4 fields masked)                                                 (inner IP)2          (inner IP)2

 01 - MAC VLAN              Candidate           Candidate            Candidate           Candidate        Candidate

 10 - Cloud               Not Candidate       Not Candidate          Candidate           Candidate       Not Candidate

1. Only if a known L4 header is present (TCP/UDP/SCTP).
2. VXLAN and NVGRE packets without inner IP header (e.g. tunneled ARP) are not candidate in IP mode.
3. IP in IP packets are not candidate in IP mode.

Basic rules for the flow director filters are:
In VT mode, the Pool field in FDIRCMD must be valid. If the packet is replicated, only the copy that goes
to the pool that matches the Pool field is impacted by the filter.The flow director filters cover the
following fields:

333369-009                                                                                                               377
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

Table 7-6.        Lookup Fields for Flow Director per Mode
       Mode                                                          Lookup Fields

 00 - IP             •   VLAN header
                     •   Source IP and destination IP Addresses
                     •   Source port and destination port numbers
                     •   IPv4 / IPv61 and UDP / TCP or SCTP protocol match
                     •   Flexible 2-byte tuple anywhere in the first 64 bytes of the packet
                     •   Target pool number (relevant only for VT mode)

 01 - MAC VLAN       •   MAC
                     •   VLAN
                     •   Flexible 2-byte tuple anywhere in the first 64 bytes of the packet
                     •   Target pool number (relevant only for VT mode)

 10 - Cloud          •   Tunnel type - NVGRE or VXLAN
                     •   TNI (NVGRE) / VNI (VXLAN)
                     •   Inner MAC
                     •   Inner VLAN
                     •   Flexible 2-byte tuple anywhere in the first 64 bytes of the packet
                     •   Target pool number (relevant only for VT mode)

1. IPv6 extended headers are parsed by the X550, enabling TCP layer header recognition. Still the IPv6 extended header fields are
   not taken into account for the queue classification by Flow Director filter. This rule do not apply for security headers and
   fragmentation header. Packets with fragmentation header miss this filter. Packets with security extended headers are parsed only
   up to these headers and therefore can match only filters that do not require fields from the L4 protocol.

The X550 supports two types of filtering modes (static setting by the FDIRCTRL.PERFECT_MATCH bit):
 • Perfect Match Filters — The hardware checks a match between the masked fields of the received
   packets and the programmed filters. Masked fields should be programmed as zeros in the filter
   context. The X550 supports up to 8 K - 1 perfect match filters.
 • Signature Filters — The hardware checks a match between a hash-based signature of the masked
   fields of the received packet. The X550 supports up to 32 K - 1 signature filters. This mode can be
   used only when the filtering mode is IPMODE (FDIRCTRL.FILTERMODE = 000b).
      Note:      The Perfect Match fields and Signature field are denoted as Flow ID fields.
The X550 supports masking / range for the previously described fields. These masks are defined
globally for all filters in the FDIR…M registers.
 • The following fields can be masked per bit enabling power of two ranges up to complete enable /
   disable of the fields: IPv4 addresses and L4 port numbers.
 • The following fields can be masked per byte enabling lower granularity ranges up to complete
   enable / disable of the fields: IPv6 addresses; Inner MAC; Outer MAC; TNI/VNI field.
      Note:      In perfect match filters the destination IPv6 address can only be compared as a whole
                 (with no range support) to the IP6AT filters. A match to any of the IP6AT filter is
                 considered as an IPv6 destination match.
 • The following fields can be either enabled or disabled completely for the match functionality: VLAN
   ID tag; Outer VLAN Priority + DEI bit (the user priority is taken from the outermost tag with UP bits
   if an inner VLAN exists; otherwise it is ignored. Inner or outer VLAN tag; Flexible 2-byte tuple and
   target pool. Target pool can be enabled by software only when VT is enabled as well.

378                                                                                                                    333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Flow director filters have the following functionality in virtualization mode:
 • Flow director filters are programmed by the registers in the PF described in Section 7.1.3.6.13 and
   Section 7.1.3.6.14.
 • Flow director filters can be utilized in virtualization mode to filter on MAC-VLAN by setting
   FDIRCTRL.FILTERMODE = MACVLANMODE (001b). MACVLANMODE is only used in flow director
   perfect match mode.

7.1.3.6.1              Flow Director Filters Actions

Flow director filters might have one of the following actions programmed per filter in the FDIRCMD
register:
 • Drop packet or pass to host as defined by the Drop bit.
     — Matched packets to a flow director filter is directed to the assigned Rx queue only if the packet
       does not match the L2 filters for queue assignment nor the SYN filter for queue assignment.
     — Packets that match a filter are directed to the Rx queue defined in the filter context as
       programmed by the FDIRCMD.RX_QUEUE. The RX_QUEUE field is an absolute receive queue
       index. In a non-VT setting, it can be programmed to any value. In VT mode, the software
       should set the RX_QUEUE to an index that belongs to the matched pool.
     — Packets that match drop filters are directed to the Rx queue defined per all filters in the
       FDIRCTRL.DROP_QUEUE. The X550 drops these packets if software does not enable the specific
       Rx queue.

7.1.3.6.2              Flow Director Default Action

A default drop action may be applied by the flow director for packets that are candidate to flow director
as defined in Table 7-5. If the FDIRCTRL.DROP_NO_MATCH bit is set, any packet candidate for flow
director that does not match any of the filters is sent to the queue defined in the
FDIRCTRL.DROP_QUEUE field.

7.1.3.6.3              Flow Director Filters Status Reporting

Shared status indications for all packets:
 • The X550 increments the FDIRMATCH counter for packets that match a flow director filter. It also
   increments the FDIRMISS counter for packets that do not match any flow director filter.
 • The Flow Director Filter Match (FLM) bit in the Extended Status field of the Rx descriptor is set for
   packets that match a flow director filter.
 • The flow ID parameters are reported in the Flow Director Filter ID field in the Rx descriptor if
   enabled by the FDIRCTRL.REPORT_STATUS. When the Report-Status bit is set, the RXCSUM.PCSD
   bit should be set as well. This field is indicated for all packets that match or do not match the flow
   director filters.
     — For packets that do not match a flow director filter, if the FDIRCTRL.REPORT_STATUS_ALWAYS
       is set, the Flow Director Filter ID field can be used by software for future programming of a
       matched filter, otherwise, the RSS hash value is reported. Table 7-7 describes the value of the
       RSS_TYPE field in the receive descriptor in the different cases.

333369-009                                                                                            379
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                  Inline Functions

Table 7-7.       RSS Type Values According to Flow Director Match
      REPORT_STATUS         REPORT_STATUS_ALWAYS         Packet matches a Flow
                                                                                        RSS Type Field Value
       (FDIRCTRL[5])            (FDIRCTRL[7])                Director Entry

             0                          0                          X                           RSS Type

             1                          0                          0                           RSS Type

             1                          0                          1                              0xF

             0                          1                          X                      illegal configuration

             1                          1                          X                              0xF

For packets that match a flow director filter, the Flow Director Filter ID field can be used by software to
identify the flow of the Rx packet. Too long linked list exception (linked list and too long terms are
illustrated in Figure 7-8):
 • The maximum recommended linked list length is programmed in the FDIRCTRL.MAX_LENGTH field
 • The length exception is reported in the FDIRERR field in the Rx descriptor
 • Packets that do not match any flow director filter, reports this exception if the length of the existing
   linked list is above the maximum recommended length. Software can use it to avoid further
   programming of additional filters to this linked list before other filters are removed.
 • Packets that match a pass filter report this exception if the distance of the matched filter from the
   beginning of the linked list is higher than the above recommended length.
 • Packets that match a drop filter are posted to the Rx queue programmed in the filter context
   instead of the global FDIRCTRL.DROP_QUEUE. The drop exception is reported in addition to the
   length exception (in the same field in the Rx descriptor).
Collision exception:
 • Packets that matches a collided filter report this exception in the FDIRERR field in the Rx descriptor.
 • Collision events for signature-based filters should be rare. Still it might happen because multiple
   flows can have the same hash and signature values. Software might leave the setting as is while
   the collided flows are handled according to the actions of the first programmed flow. Only one flow
   (out of the collided ones) might remain in the flow director filters. To clear the collision indication in
   the programmed filter, software should remove the filter and then re-program it once again.
 • Collision events for a perfect match filter should never happen. A collision error might indicate a
   programming fault that software might decide to fix.

7.1.3.6.4              Flow Director Filters Block Diagram

Figure 7-8 shows a block diagram of the flow director filters. Received flows are identified to buckets by
a hash function on the relevant tuples as defined by the FDIR...M registers. Each bucket is organized in
a linked list indicated by the hash lookup table. Buckets can have a variable length while the last filter in
each bucket is indicated as a last. There is no upper limit for a linked list length during programming.
However, a received packet that matches a filter that exceeds the FDIRCTRL.MAX_LENGTH are reported
to software (see Section 7.1.3.6.6).

380                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

            Logic AND of Rx Packet tuples with
             the Flexible filters Mask registers                                   Flow ID Fields in “Perfect Match mode”

                                  ~350                    Hash (Signature)
                                                                                   Flow ID Field in “Signature mode”
                                                            15 bit output

                          Hash
                       15 bit output
                                                    Hash-Index = 0      Hash-Index = 1            Hash-Index = N       Hash-Index = N+1

                         15 bit address               Flow ID fields     Flow ID fields            Flow ID fields        Flow ID fields
                                                       Filter Action      Filter Action     ...     Filter Action         Filter Action   ...
      Addr

# 0 Bucket Valid First Filter PTR                Collision flag     Collision flag            Collision flag        Collision flag

                                                     Next Filter PTR    Next Filter PTR           Next Filter PTR       Next Filter PTR

# 1 Bucket Valid First Filter PTR

# 2 Bucket Valid First Filter PTR

                                                                                     Bucket 0 (linked list 0)
       ...           ...                                                                                                    ‘too long’
       M Bucket Valid First Filter PTR               Hash-Index = 0     Hash-Index = 1                                      Linked list
       ...                  ...                       Flow ID fields     Flow ID fields
      32K Bucket Valid First Filter PTR                Filter Action      Filter Action
                                                      Collision flag     Collision flag           Max recommended linked list length
                                                     Next Filter PTR    Next Filter PTR               (FDIRCTRL.Max-Length)

                Hash Lookup Table                         Bucket M (linked list M)
                    Shares the Rx
             packet buffer memory space                         Flexible Filters table - Shares the Rx packet buffer memory space

Figure 7-8.          Flow Director Filters Block Diagram

7.1.3.6.5                      Rx Packet Buffer Allocation

Flow director filters can consume zero space (when disabled) up to ~256 KB of memory. As shown in
Figure 7-8, flow director filters share the same memory with the Rx packet buffer. By setting the
PBALLOC field in the FDIRCTRL register, the software can enable and allocate memory for the flow
director filters. The memory allocated to received traffic is the remaining part of the Rx packet buffer.

Table 7-8.           Rx Packet Buffer Allocation
                                                                                           Supported Flow Director Filters
                          Effective Rx
                       Packet Buffer Size           Flow Director
 PBALLOC (2)                                                                         Signature                              Perfect Match
                         (see following            Filters Memory
                             note)
                                                                             Filters         Bucket Hash            Filters           Bucket Hash

       00
 Flow Director is             384 KB                      0                    0                   N/A                  0                  N/A
    disabled

       01                     320 KB                   64 KB             8 K -1 filters           13 bit        2 K -1 filters            11 bit

       10                     256 KB                   128 KB           16 K -1 filters           14 bit        4 K -1 filters            12 bit

333369-009                                                                                                                                         381
                                            Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Inline Functions

Table 7-8.        Rx Packet Buffer Allocation [continued]
                                                                                     Supported Flow Director Filters
                      Effective Rx
                   Packet Buffer Size         Flow Director
 PBALLOC (2)                                                                  Signature                         Perfect Match
                     (see following          Filters Memory
                         note)
                                                                      Filters         Bucket Hash          Filters       Bucket Hash

       11                 128 KB                 256 KB            32 K -1 filters        15 bit        8 K -1 filters       13 bit

Notes:
    • It is the user’s responsibility to ensure that sufficient buffer space is left for reception of traffic. The required buffer space
       for receive traffic depends on the number of traffic classes, and flow control upper and lower threshold values. If flow
       director is enabled (PBALLOC > 0), software should set the RXPBSIZE[n] registers according to the total remaining part of
       the Rx packet buffer for reception of traffic.
    • When allocating 256 KB to the Flow Director table, it is likely that the 128 KB packet buffer left is too small to permit
       operating the port in DCB enabled mode.
    • Refer to Section 3.7.4.3.2 through Section 3.7.4.3.5 for recommended setting of the Rx packet buffer sizes and flow
       control thresholds.

7.1.3.6.6                  Flow Director Filtering Reception Flow

 • Rx packet is digested by the filter unit which parse the packet extracting the relevant tuples for the
   filtering functionality.
 • The X550 calculates a 15-bit hash value out of the masked tuples (logic mask of the tuples and the
   relevant mask registers) using the hash function described in Section 7.1.3.6.16.
 • The address in the hash lookup table points to the selected linked list of flow director filters.
 • The X550 checks the Bucket Valid flag. If it is inactive, the packet does not match any filter.
   Otherwise, Bucket Valid flag is active, proceed for the next steps.
 • The X550 checks the linked list until it reaches the last filter in the linked list or until a matched
   filter is found.
 • Case 1: Matched filter is found:
      — Increment the FDIRMATCH statistic counter.
      — Process the filter's actions (queue assignment) according to queue assignment priority.
        Meaning, the actions defined in this filter takes place only if the packet did not match any L2
        filter or SYN filter that assigns an Rx queue to the packet.
      — Rx queue assignment according to the filter context takes place if QUEUE_EN is set.
      — If the DROP bit is set in the filter context, the packet is sent to the queue pointed by the
        FDIRCTRL.DROP_QUEUE field.
      — Post the packet to host including the flow director filter match indications as described in
        Section 7.1.3.6.3.
 • Case 2: Matched filter is not found:
      — Increment the FDIRMISS statistic counter.
      — Post the packet to host including the flow director filter miss indications as described in
        Section 7.1.3.6.3.

382                                                                                                                         333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.1.3.6.7              Add Filter Flow

The software programs the filters parameters in the registers described in Section 7.1.3.6.13 and
Section 7.1.3.6.14 while keeping the FDIRCMD.FILTER_UPDATE bit inactive. As a result, the X550
checks the bucket valid indication in the hash lookup table (that matches the FDIRHASH.HASH) for the
presence of an existing linked list. Following are the two programming flows for the case a link list
exists or for the case a new list is required.
 • Case 1: Add a filter to existing linked list:
    The X550 checks the linked list until it reaches the last filter in the list or until a matched filter is
    found. The following cases may occur:
     — Matched filter is found (equal flow ID) with the same action parameters — The programming is
       discarded silently. This is a successful case since the programmed flow is treated as requested.
     — Matched filter is found (equal flow ID) with different action parameters — The X550 keeps the
       old setting of the filter while setting the Collision flag in the filter context (see Section 7.1.3.6.3
       for software handling of collision during packet reception).
     — Matched filter is found (equal flow ID) with different action parameters and the Collision flag is
       already set — The programming is discarded silently. Software gets the same indications as the
       previous case.
     — Matched filter is not found (no collision) — The X550 checks for a free space in the flow director
       filters table.
     — No space case — Discard programming; increment the FADD counter in the FDIRFSTAT register
       and assert the flow director interrupt. Following this interrupt software should read the
       FDIRFSTAT register and FDIRFREE.FREE field, for checking the interrupt cause.
     — Free space is found — Good programming case: Add the new filter at the end of the linked list
       while indicating it as the last one. Program the Next Filter PTR field and then clear the Last flag
       in the filter that was previously the last one.
 • Case 2: Create a new linked list:
    The X550 looks for an empty space in the flow director filters table:
     — Handle no empty space the same as in Case 1.
     — Good programming case: Add the new filter while indicating it as the last one in the linked list.
       Then, program the hash lookup table entry by setting the Valid flag and the First Filter PTR
       pointing to the new programmed filter.
Additional successful add flow indications:
 • Increment the ADD statistic counter in the FDIRUSTAT register.
 • Reduce the FREE counter in the FDIRFREE register, and then indicate the number of free filters. If
   the FREE counter crosses the FULL_THRESH value in the FDIRCTRL register, assert the flow director
   filter interrupt. Following this interrupt software should read the FDIRFSTAT register and
   FDIRFREE.FREE field, for checking the interrupt cause.
 • Compare the length of the new linked list with MAXLEN in the FDIRLEN register. If the new linked
   list is longer than MAXLEN, update the FDIRLEN by the new flow.

333369-009                                                                                                  383
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                   Inline Functions

7.1.3.6.8             Update Filter Flow

In some applications, it is useful to update the filter parameters, such as the destination Rx queue.
Programing filter parameters is described in Section 7.1.3.6.7.
Setting the FILTER_UPDATE bit in the FDIRCMD register has the following result:
 • Case 1: Matched filter does not exist in the filter table — Setting the FILTER_UPDATE bit has no
   impact and the command is treated as add filter.
 • Case 2: Matched filter already exists in the filter table — Setting the FILTER_UPDATE bit enables
   filter parameter’s update while keeping the collision indication as is.
When updating an existing filter the software device driver should program the same filter (i.e. the
same FDIRHASH.HASH and the same FDIRHASH.SIGNATURE_SW_INDEX) while keeping the
FDIRCMD.FILTER_UPDATE = 1

7.1.3.6.9             Remove Filter Flow

Software programs the filter Hash and Signature/Software-Index in the FDIRHASH register. It then
should set the FDIRCMD.CMD field to Remove Flow. Software might use a single 64-bit access to the
two registers for atomic operation. As a result, the X550 follows these steps:
1. Check if such a filter exists in the flow director filters table.
2. If there is no flow, increment the FREMOVE counter in the FDIRFSTAT register and skip the next
   steps.
3. If the requested filter is the only filter in the linked list, invalidate its entry in the hash lookup table
   by clearing the Valid bit.
4. Else, if the requested filter is the last filter in the linked list, invalidate the entry by setting the Last
   flag in the previous filter in the linked list.
5. Else, invalidate its entry by programming the Next Filter PTR in the previous filter in the linked list,
   pointing it to the filter that was linked to the removed filter.
Additional indications for successful filter removal:
1. Increment the remove statistic counter in the FDIRUSTAT register.
2. Increment the FREE counter in the FDIRFREE register.

7.1.3.6.10            Remove All Flow Director Filters

In some cases there is a need to clear the entire flow director table. It might be useful in some
applications that might cause the flow director table becoming too occupied. Then, software might clear
the entire table enabling its re-programming with new active flows.
Following are steps required to clear the flow director table:
 • Poll the FDIRCMD.CMD until it is zero indicating any previous pending commands to the flow
   director table is completed (at worst case the FDIRCMD.CMD should be found cleared on the second
   read cycle). Note that software must not initiate any additional commands (add/remove/query)
   before this step starts and until this flow completes.
 • Clear the FDIRFREE register (set FREE field to zero).
 • Set FDIRCMD.CLEARHT to 1b and then clear it back to 0b.
 • Clear the FDIRHASH register to zero.

384                                                                                                    333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • Re-write FDIRCTRL by its previous value while clearing the INIT_DONE flag.
 • Poll the INIT_DONE flag until it is set to 1b by hardware.
 • Clear the following statistic registers: FDIRUSTAT, FDIRFSTAT, FDIRMATCH, FDIRMISS, FDIRLEN
   (note that some of these registers are read clear and some are read write).

7.1.3.6.11                 Flow Director Filters Initializing Flow

Following a device reset, the flow director is enabled by programming the FDIRCTRL register, as
follows:
 • Set PBALLOC to non-zero value according to the required buffer allocation to reception and flow
   director filter (see Section 7.1.3.6.5). All other fields in the register should be valid as well
   (according to required setting), as the FDIRCTRL register is expected to be programmed by a single
   cycle.
 • Poll the INIT_DONE flag until it is set to 1b by hardware (expected initialization flow should take
   about 55 s at 10 Gb/s and 550 s at 1 Gb/s.
Note:        The value of the FDIRCTRL.PERFECT_MATCH and FDIRCTRL.FILTERMODE should be modified
             only when no filters are set (at init time).

7.1.3.6.12                 Query Filter Flow

Software might query specific filter settings and bucket length using the Query command.
 • Program the filter HASH and SIGNATURE_SW_INDEX in the FDIRHASH register, and set the CMD
   field in the FDIRCMD register to 11b (Query Command). A single 64-bit access can be used for this
   step.
 • As a result, the X550 provides the query result in the FDIRHASH, FDIRCMD and FDIRLEN registers
   (described in the sections as follows).
 • Hardware indicates query completion by clearing the FDIRCMD.CMD field. The following table lists
   the query result.

Table 7-9.        Query Filter Flow
                                 FDIRHASH ->        FDIRCMD ->          FDIRLEN ->           FDIRCMD ->            FDIRCMD ->
       Query Outcome
                                 Bucket Valid        Filter Valid      Bucket Length        Filter ID Fields       Filter Action

 Empty Bucket                           0                 0          N/A                          N/A                    N/A

 Valid Bucket, Matched Filter           1                 0          Bucket linked list           N/A                    N/A
 Not Found                                                           length

 Found Signature Filter                 1                 1          Filter index within           0             Filter's parameters1
                                                                     the linked list

 Found Perfect Match Filter             1                 1          Filter index within   Filter's parameters   Filter's parameters
                                                                     the linked list

1. The pool parameter is not returned as part of the filter action in signature mode.

333369-009                                                                                                                         385
                                       Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                Inline Functions

7.1.3.6.13              Signature Filter Registers

The signature flow director filter is programmed by setting the FDIRHASH and FDIRCMD registers.
These registers are located in consecutive 8-byte aligned addresses. Software should use a 64-bit
register to set these two registers in a single atomic operation. Table 7-10 lists the recommended
setting.

Table 7-10. Signature Match Filter Parameters
                                           Filter Bucket Parameters — FDIRHASH

                        15-bit hash function used to define a bucket of filters. This parameter is part of the flow director filter ID
          Hash
                        that can be reported in the Rx descriptor. It is shared for signature and perfect match filters.

          Valid         Should be set to 1b. It is shared for signature and perfect match filters.

                                                      Flow ID — FDIRHASH

                        15-bit hash function used as the flow matching field. This parameter is also part of the flow director filter
        Signature
                        ID that can be reported in the Rx descriptor.

        FDIRCMD — Programming Command and Filter action — See Section 8.2.2.15.8 for all fields descriptions.

7.1.3.6.14              Perfect Match Filter Registers

Perfect match filters are programmed by the following registers: FDIRSIPv6[n], FDIRVLAN, FDIRPORT,
FDIRIPDA, FDIRIPSA, FDIRHASH, FDIRCMD. Setting the FDIRCMD register, generates the actual
programming of the filter. Therefore, write access to this register must be the last cycle after all other
registers contain a valid content. Table 7-11 lists the recommended setting.
Note:       Software filter programming must be an atomic operation. In a multi-core environment,
            software must ensure that all registers are programmed in a sequence with no possible
            interference by other cores.

Table 7-11. Perfect Match Filter Parameters
                               Filter Bucket Parameters and Software Index — FDIRHASH

Hash                      See Section 7.1.3.6.13.

Valid                     See Section 7.1.3.6.13.

Software-Index            16-bit index provided by software at filter programming used by software to identify the matched flow.
                          This parameter is also part of the flow director filter ID that can be reported in the Rx descriptor.

FDIRCMD — Programming Command and Filter Action Set

                                    IP Mode                            MAC, VLAN Mode                        Cloud Modes
                               FILTERMODE = 000b                     FILTERMODE = 001b                   FILTERMODE = 010b

IPV6DMATCH                Should be set for IPv6 filters         Should be cleared
                          only and only if the destination
                          address should be compared to
                          one of the IPAT filters.

L4TYPE                    Defines if the filter is for TCP,      Should be cleared
                          UDP or SCTP flows.                     FDIRM.L4P should be set

IPV6                      Defines if the filter is for IPv4 or   Should be cleared
                          IPv6 addresses.                        FDIRM.L3P should be set
                                                                 FDIRM.DIPV6 should be set

386                                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-11. Perfect Match Filter Parameters [continued]
TUNNEL_FILTER            Defines if the filter is a VXLAN    Should be cleared.
                         and NVGRE tunneled packet
                         filter. If set, the parameters of
                         the L3 and L4 header relates to
                         the tunneled (inner) header.

POOL                     Pool to which the packet is directed (relevant only in virtualization modes).

Flow ID — Perfect Match Flow ID Parameters are Listed in the Following Registers and Fields

                                  IP Mode                          MAC, VLAN Mode                        Cloud Mode
                             FILTERMODE = 000b                   FILTERMODE = 001b                   FILTERMODE = 010b

FDIRSIPv6[0…2].IP6SA     Three LS DWord of the source        {FDIRSIPv6_0[31:0],                FDIRSIPv6_2[31:0] holds the
                         IPv6. Meaningful for IPv6 flows     FDIRSIPv6_1[15:0]} holds the       32 bits of the TNI/VNI field.
                         depending on the                    destination MAC Address value      {FDIRSIPv6_0[31:0],
                         FDIRIP6M.SIPM setting.              FDIRSIPv6_1[31:16], and            FDIRSIPv6_1[15:0]} holds the
                                                             FDIRSIPv6_2[31:0] are              destination MAC Address value
                                                             reserved and should be set to
                                                                                                FDIRSIPv6_1[31] holds the
                                                             0x0. The FDIRIP6M.SIPM field
                                                                                                cloud mode (0 = NVGRE, 1 =
                                                             should be set to 0x0xFC0F
                                                                                                VXLAN).
                                                                                                FDIRSIPv6_1[30:16] are
                                                                                                reserved and should be set to
                                                                                                0x0.
                                                                                                To mask one of the fields the
                                                                                                matching bits in FDIRIP6M.SIPM
                                                                                                should be set:
                                                                                                 • Bits [15:12] control the
                                                                                                    masking of the TNI/VNI
                                                                                                    field. All the 32 bits of the
                                                                                                    key can be used for
                                                                                                    filtering.
                                                                                                 • Bit [11] controls the
                                                                                                    masking of the cloud mode
                                                                                                    and should be cleared for
                                                                                                    normal operation
                                                                                                 • Bits [3:0] and Bit [10]
                                                                                                    should be set.
                                                                                                 • Bits [9:4] control the
                                                                                                    masking of the inner MAC
                                                                                                    Address.

FDIRVLAN.VLAN            VLAN fields are meaningful depending on the FDIRM.VLANID and           Inner VLAN fields are
                         FDIRM.VLANP setting. The VLAN field should be stored in Little         meaningful depending on the
                         endian format.                                                         FDIRM.VLANID and
                                                                                                FDIRM.VLANP setting.The VLAN
                                                                                                field should be stored in Little
                                                                                                endian format.

FDIRVLAN.FLEX            Flexible 2-byte field at offset FDIRCTRL.FLEX_OFFSET. Meaningful depending on FDIRM.FLEX setting.

FDIRPORT.Source          L4 source port. Meaningful for      Reserved - Should be zero.
                         TCP, UDP and SCTP packets           FDIRM.L4P should be set.
                         depending on the
                                                             FDIRTCPM.SportM, FDIRUDPM.SportM and FDIRSCTPM.SportM
                         FDIRTCPM.SportM,
                                                             should be set.
                         FDIRUDPM.SportM and
                         FDIRSCTPM.SportM setting.

FDIRPORT.Destination     L4 destination port. Meaningful     Reserved - Should be zero.
                         for TCP, UDP and SCTP packets       FDIRM.L4P should be set.
                         depending on the
                                                             FDIRTCPM.DportM, FDIRUDPM.DportM and FDIRSCTPM.DportM
                         FDIRTCPM.DportM,
                                                             should be set.
                         FDIRUDPM.DportM and
                         FDIRSCTPM.DPORTM setting.

333369-009                                                                                                                    387
                                   Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                      Inline Functions

Table 7-11. Perfect Match Filter Parameters [continued]
FDIRIPDA.IP4DA         IPv4 destination address.       Reserved - Should be zero.
                       Meaningful depending on the     All bits in FDIRDIP4M.IPM should be set.
                       FDIRDIP4M.IPM setting.

FDIRIPSA.IP4SA         IPv4 source address or LS       Reserved - Should be zero.
                       DWord of the source IPv6        All bits in FDIRDSIP4M.IPM should be set.
                       address. Meaningful for IPv4
                                                       FDIRIP6M.SIPM[3:0] should be set.
                       flows depending on the
                       FDIRSIP4M.IPM setting and for
                       IPv6 flows depending on the
                       FDIRIP6M.SIPM setting.

7.1.3.6.15           Multiple CPU Cores Considerations

Perfect match filters programming and any query cycles require access to multiple registers. To avoid
races between multiple cores, software might need to use one of the following programming methods:
 • Use a software-based semaphore between the multiple cores for gaining control over the relevant
   CSR registers for complete programming or query cycles.
 • Manage all programming and queries of the flow director filters by a single core.
Programming signature filters requires only the FDIRHASH and FDIRCMD registers. These two registers
are located in 8-byte aligned adjacent addresses. Software could use an 8-byte register for the
programming of these registers in a single atomic operation, which avoids the need for any semaphore
between multiple cores.

7.1.3.6.16           Flow Director Hash Function

The X550 supports programmable 16-bit hash functions based on two 32-bit keys, one for the lookup
table identifying a bucket of filters and another one for the signature (FDIRHKEY and FDIRSKEY). The
hash function is described in the sections that follows. In some cases, a smaller hash value than 16 bits
is required. In such cases, the LS bits of the hash value are used.
  For (i=0 to 350) {if (Ext_K[i]) then Hash[15: 0] = Hash[15: 0] XOR Ext_S[15+i: i]}

While using the following notations:
      'XOR'                 Bitwise XOR of two equal length strings
      If (xxx)              Equals ‘true’ if xxx = ‘1’ and equals ‘false’ if xxx = ‘0’
      S[335:0]              The input bit string of the flow director tuples: 42 bytes listed in Table 7-12
                            AND-logic with the filters masks.
      Ext_S[n]              S[14:0] | S[335:0] | S[335:321] // concatenated
      K[31:0]               The hash key as defined by the FDIRHKEY or FDIRSKEY registers.
      Tmp_K[11*32-1:0]      (Temp Key) equals K[31:0] | K[31:0]... // concatenated Key 11 times
      Ext_K[350:0]          (Extended Key) equals T_K[351:1]
The input bit stream for the hash calculation is listed in Table 7-12 while byte 0 is the MSByte (first on
the wire) of the VLAN, byte 2 is the MSByte of the source IP (IPv6 case) and so on.

388                                                                                                       333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-12. Input Bit Stream for Hash Calculation
                                                                            Field
      Bytes/Mode
                                     IP                     MAC, VLAN                              Cloud Mode

       Bytes 0…1          VLAN tag (always the outer VLAN)                     Inner VLAN Tag

       Bytes 2…5          Source IP (16 bytes for    Zero
                          IPv6; source IP for IPv4
      Bytes 6...11        | 12 bytes of zero's)      MAC                       Inner MAC

      Bytes 12...13                                  Zero                      8 bits of zeros | bit of tunnel_type | 7 bits of zeros

      Bytes 14...17                                  Zero                      VNI/TNI

                          Signature Mode: Destination IP (16 bytes for IPv6; destination IP for IPv4 | 12 bytes of zero's)
      Bytes 18…33         Exact Mode: Destination IP (7 zero bits |IP6AT match indication | 120 zero bits; destination IP for IPv4 |
                          12 bytes of zero's)1

         34...37          L4 source port number | L4 destination port number

         38...39          Flexible bytes

           40             00b | pool number (as defined by FDIRCMD.Pool)

                          [7:5] 000b
                          [4] FDIRCMD.TUNNEL_FILTER (should be zero in MAC, VLAN mode).
           41             [3] 0b
                          [2] IPv6/IPv4 type (FDIRCMD.IPV6)
                          [1:0] L4 type (FDIRCMD.L4TYPE)

1. In VXLAN and NVGRE packets, the IP Addresses used are of the tunneled header in other packets the outer IP header is used.

#### 7.1.3.7 RSS

RSS is a mechanism to distribute received packets into several descriptor queues. Software can then
assign each queue to a different processor, therefore sharing the load of packet processing among
several processors.
As described in Section 7.1, the X550 uses RSS as one ingredient in its packet assignment policy (the
others are the various filters, DCB and virtualization). The RSS output is an RSS index. The X550 global
assignment uses these bits (or only some of the LSBs) as part of the queue number.
Figure 7-9 and Figure 7-10 show the process of computing an RSS output:
 1. The receive packet is parsed into the header fields used by the hash operation (such as IP
    Addresses, TCP port, etc.)
 2. A hash calculation is performed. The X550 supports a single hash function, as defined by Microsoft*
    (MSFT) RSS. The X550 therefore does not indicate to the device driver which hash function is used.
    The 32-bit result is fed into the RSS Hash field in the packet receive descriptor.
 3. The X550 supports two modes of RSS defined by the MRQC.MULTIPLE_RSS bit. When set to 0b a
    single RSS key and redirection table are supported. In this mode (usually used when virtualization
    is not enabled) the nine LSBs of the hash result are used as an index into a 512-entry redirection
    table. Each entry provides up to 6-bit RSS output index (Figure 7-9).
    For SRIOV or VMDQ enabled modes (set by MRQC.MULTIPLE_RSS set to 1b), The X550 supports up
    to 64 (one per pool) RSS keys and redirection tables (both can be controlled and programmed at
    the VF space). In this mode the 6 LSBs of the hash result are used as an index into a 64-entry
    redirection table. Each entry provides up to 2-bit RSS output index (Figure 7-10).

333369-009                                                                                                                         389
                                      Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

When RSS is enabled, the X550 provides software with the following information as required by
Microsoft* RSS and provided for device driver assist:
 • A DWord result of the MSFT RSS hash function application to the packet header, to be used by the
   stack for flow classification, is written into the receive packet descriptor. A 4-bit RSS Type field
   conveys the hash function used for the specific packet.
 • Packets to which the RSS function cannot be applied (for example non IP packets) return an RSS
   Hash result of zero, an RSS Type of zero and an RSS output index of zero.

7.1.3.7.1           Enabling RSS

 • RSS is enabled in the MRQC register.
 • RSS enabling cannot be done dynamically and must be preceded by a software reset.
 • RSS status field in the descriptor write-back is enabled when the RXCSUM.PCSD bit is set (fragment
   checksum is disabled). RSS is therefore mutually exclusive with UDP fragmentation checksum
   offload.
 • Support for RSS is not provided when legacy receive descriptor format is used.

7.1.3.7.2           Disabling RSS

 • Disabling RSS on the fly is not allowed, and the X550 must be reset after RSS is disabled.
 • When RSS is disabled, packets are assigned an RSS output index = zero.

                     Parsed receive packet

                                                      Redirection Table
                          RSS hash
                                                           512 x 6

    9 LS

                                           bits
                           32                                                 0

                                                            6

                                                                                       RSS Disable or (RSS
                       Packet Descriptor
                                                                                        & not decodable)

                                                                     6

                                                                RSS output index

Figure 7-9.   RSS Block Diagram (MULTIPLE_RSS = 0b)

390                                                                                                               333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                       Parsed receive packet

# 64 Redirection

                                                           Tables
                                                            64 x 2     6
                                                                                Pool Number
                            RSS hash

    6 LS

                                             bits
                             32                                            0

                                                         2

                                                                                   RSS Disable or (RSS
                         Packet Descriptor
                                                                                    & not decodable)

                                                                  2

                                                             RSS output index

Figure 7-10. RSS Block Diagram (MULTIPLE_RSS = 1b)

7.1.3.7.3              RSS Hash Function

This section provides a verification suite used to validate that the hash function is computed according
to MSFT nomenclature.
The X550’s hash function follows the MSFT definition. A single hash function is defined with several
variations for the following cases:
 • TcpIPv4 — The X550 parses the packet to identify an IPv4 packet containing a TCP segment per
   the criteria described below. If the packet is not an IPv4 packet containing a TCP segment, RSS is
   not done for the packet.
 • IPv4 — The X550 parses the packet to identify an IPv4 packet. If the packet is not an IPv4 packet,
   RSS is not done for the packet.
 • TcpIPv6 — The X550 parses the packet to identify an IPv6 packet containing a TCP segment per
   the criteria described below. If the packet is not an IPv6 packet containing a TCP segment, RSS is
   not done for the packet.
 • IPv6 — The X550 parses the packet to identify an IPv6 packet. If the packet is not an IPv6 packet,
   RSS is not done for the packet.
Tunneled IP to IP packets are considered for the RSS functionality as IP packets. The RSS logic ignores
the L4 header while using the outer (first) IP header for the RSS hash.
For NVGRE and VXLAN packets the inner header (IP and TCP/UDP) is used for RSS computations.
The following additional cases are not part of the MSFT RSS specification but are supported RSS modes:
 • UdpIPV4 — The X550 parses the packet to identify a packet with UDP over IPv4.
 • UdpIPV6 — The X550 parses the packet to identify a packet with UDP over IPv6.

333369-009                                                                                               391
                                   Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

A packet is identified as containing a TCP segment if all of the following conditions are met:
 • The transport layer protocol is TCP (not UDP, ICMP, IGMP, etc.).
 • The TCP segment can be parsed (such as IPv4 options or IPv6 extensions can be parsed, packet not
   encrypted, etc.).
 • The packet is not fragmented (even if the fragment contains a complete L4 header).
Note:      IPv6 extended headers are parsed by the X550, enabling TCP layer header recognition. Still
           the IPv6 extended header fields are not taken into account for the queue classification by RSS
           filter. This rule do not apply for security headers and fragmentation header. Packets with
           fragmentation header miss this filter. Packets with security extended headers are parsed only
           up to these headers and therefore can match only filters that do not require fields from the L4
           protocol.
Bits[31:16] of the Multiple Receive Queues Command (MRQC), for single RSS and VFMRQC for multiple
RSS, registers enable each of the above hash function variations (several might be set at a given time).
If several functions are enabled at the same time, priority is defined as follows (skip functions that are
not enabled):
 • IPv4 packet:
      — Try using the TcpIPv4 function
      — Try using UdpIPv4 function
      — Try using the IPv4 function
 • IPv6 packet:
      — Try using the TcpIPv6 function.
      — Try using UdpIPv6 function.
      — Try using the IPv6 function
The following combinations are currently supported:
 • Any combination of IPv4, TcpIPv4, and UdpIPv4.
      And/or:
 • Any combination of either IPv6, TcpIPv6, and UdpIPv6.
When a packet cannot be parsed by the previous rules, it is assigned an RSS output index = zero. The
32-bit tag (normally a result of the hash function) equals zero.
The 32-bit result of the hash computation is written into the packet descriptor and also provides an
index into the redirection table.
The following notation is used to describe the following hash functions:
 • Ordering is little endian in both bytes and bits. For example, the IP Address 161.142.100.80
   translates into 0xa18e6450 in the signature.
 • A “^” denotes bit-wise XOR operation of same-width vectors.
 • @x-y denotes bytes x through y (including both of them) of the incoming packet, where byte 0 is
   the first byte of the IP header. In other words, we consider all byte-offsets as offsets into a packet
   where the framing layer header has been stripped out. Therefore, the source IPv4 address is
   referred to as @12-15, while the destination v4 address is referred to as @16-19.
 • @x-y, @v-w denotes concatenation of bytes x-y, followed by bytes v-w, preserving the order in
   which they occurred in the packet.

392                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

All hash function variations (IPv4 and IPv6) follow the same general structure. Specific details for each
variation are described in the following section. The hash uses a random secret key of length 320 bits
(40 bytes); the key is stored in the RSS Random Key Register RSSRK for single RSS and
VFRSSRK[63:0] for multiple RSS.
The algorithm works by examining each bit of the hash input from left to right. Our nomenclature
defines left and right for a byte-array as follows: Given an array K with k bytes, our nomenclature
assumes that the array is laid out as follows:
 • K[0] K[1] K[2] … K[k-1]
K[0] is the left-most byte, and the MSB of K[0] is the left-most bit. K[k-1] is the right-most byte, and
the LSB of K[k-1] is the right-most bit.
ComputeHash(input[], N)
  For hash-input input[] of length N bytes (8N bits) and a random secret key K of 320 bits
  Result = 0;
  For each bit b in input[] {
  if (b == 1) then Result ^= (left-most 32 bits of K);
  shift K left 1 bit position;
  }
  return Result;

7.1.3.7.3.1             Pseudo-code Examples

The following four pseudo-code examples are intended to help clarify exactly how the hash is to be
performed in four cases, IPv4 with and without ability to parse the TCP header, and IPv6 with and
without a TCP header.

Hash for IPv4 with TCP:
    Concatenate SourceAddress, DestinationAddress, SourcePort, DestinationPort into one single byte-
    array, preserving the order in which they occurred in the packet: Input[12] = @12-15, @16-19,
    @20-21, @22-23.
      Result = ComputeHash(Input, 12);

Hash for IPv4 with UDP:
    Concatenate SourceAddress, DestinationAddress, SourcePort, DestinationPort into one single byte-
    array, preserving the order in which they occurred in the packet: Input[12] = @12-15, @16-19,
    @20-21, @22-23.
      Result = ComputeHash(Input, 12);

Hash for IPv4 without TCP:
    Concatenate SourceAddress and DestinationAddress into one single byte-array
      Input[8] = @12-15, @16-19
      Result = ComputeHash(Input, 8)

Hash for IPv6 with TCP:
    Similar to previous:
      Input[36] = @8-23, @24-39, @40-41, @42-43
      Result = ComputeHash(Input, 36)

333369-009                                                                                            393
                                 Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Inline Functions

Hash for IPv6 with UDP:
      Similar to previous:
        Input[36] = @8-23, @24-39, @40-41, @42-43
        Result = ComputeHash(Input, 36)

Hash for IPv6 without TCPL:
        Input[32] = @8-23, @24-39
        Result = ComputeHash(Input, 32)

7.1.3.7.4                    Redirection Tables

The redirection table used for single RSS mode (RETA - Section 8.2.2.8.18 and ERETA -
Section 8.2.2.8.24) is a 512-entry structure, indexed by the nine LSBs of the hash function output.
The redirection tables used for multiple RSS mode (VFRETA - Section 8.3.2.3.12) are 64-entry
structures indexed by the six LSBs of the hash function output. The table to use is defined by the pool
to which the packet is sent.
System software might update the redirection tables during run time. Such updates of the table are not
synchronized with the arrival time of received packets. Therefore, it is not guaranteed that a table
update takes effect on a specific packet boundary.

7.1.3.7.5                    RSS Verification Suite

Assume that the random key byte-stream is:
  0x6d, 0x5a, 0x56, 0xda, 0x25, 0x5b, 0x0e, 0xc2,
  0x41, 0x67, 0x25, 0x3d, 0x43, 0xa3, 0x8f, 0xb0,
  0xd0, 0xca, 0x2b, 0xcb, 0xae, 0x7b, 0x30, 0xb4,
  0x77, 0xcb, 0x2d, 0xa3, 0x80, 0x30, 0xf2, 0x0c,
  0x6a, 0x42, 0xb7, 0x3b, 0xbe, 0xac, 0x01, 0xfa

Table 7-13. IPv4
  Destination Address/Port          Source Address/Port                    IPv4 only                 IPv4 with TCP

      161.142.100.80:1766            66.9.149.187:2794                  0x323e8fc2                    0x51ccc178

        65.69.140.83:4739            199.92.111.2:14230                0xd718262a                     0xc626b0ea

      12.22.207.184:38024            24.19.198.95:12898                0xd2d0a5de                     0x5c2b394a

       209.142.163.6:2217            38.27.205.30:48228                0x82989176                      0xafc7327f

       202.188.127.2:1303           153.39.163.191:44251               0x5d1809c5                     0x10e828a2

Note:       The IPv6 address tuples are only for verification purposes, and may not make sense as a
            tuple.

Table 7-14. IPv6
      Destination Address/Port                 Source Address/Port                      IPv6 only        IPv6 with TCP

      3ffe:2501:200:3::1 (1766)             3ffe:2501:200:1fff::7 (2794)                0x2cc18cd5         0x40207d3d

            ff02::1 (4739)             3ffe:501:8::260:97ff:fe40:efab (14230)           0x0f0c461c         0xdde51bbf

 fe80::200:f8ff:fe21:67cf (38024)    3ffe:1900:4545:3:200:f8ff:fe21:67cf (44251)       0x4b61e985           0x02d1feef

394                                                                                                            333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.1.4 Receive Data Storage in System Memory

The X550 posts receive packets into data buffers in system memory.
The following controls are provided for the data buffers:
 • The SRRCTL[n].BSIZEPACKET field defines the size of the data buffer pointed by each descriptor.
   The maximum packet size that can be posted to a queue can be limited using the RXDCTL[n].RLPML
   field. This filter enables software to use smaller buffers than the size defined by the
   SRRCTL[n].BSIZEPACKET.
    Note:      The packet size compared to RXDCTL[n].RLPML does not include any parts stripped by
               the device like CRC VLAN or other tags but include additional Timestamp appended to the
               packet.
 • The SRRCTL[n].BSIZEHEADER field defines the size of the header buffer pointed by each descriptor
   (advanced descriptors only).
 • Each queue is provided with a separate SRRCTL register.
Receive memory buffer addresses are word (2 x byte) aligned (both data and headers).
The internal receive buffers are described in Section 7.6.3.1.

### 7.1.5 Receive Descriptors

#### 7.1.5.1 Legacy Receive Descriptor Format

A receive descriptor is a data structure that contains the receive data buffer address and fields for
hardware to store packet information. Upon receipt of a packet for this device, hardware stores the
packet data into the indicated buffer and writes the length, status and errors to the receive descriptor.
If SRRCTL[n].DESCTYPE = zero, the X550 uses the Legacy Rx descriptor as listed in Table 7-15. The
shaded areas indicate fields that are modified by hardware upon packet reception (so-called descriptor
write-back).
Legacy descriptors should not be used when advanced features are enabled: SCTP, Virtualization, DCB,
IPsec, FCoE, Time stamp in Packet, tunnel packets checksum or RSC. Packets that match these cases
might be dropped from queues that use legacy receive descriptors.
Refer to Table 7-15 and the field descriptions that follow.

Table 7-15. Legacy Receive Descriptor (RDESC) Layout
         63                   48    47            40   39            32   31               16   15            0

# 0 Buffer Address [63:0]

    8 VLAN Tag                Errors             Status         Fragment Checksum         Length

Buffer Address (64-bit offset 0, 1st line)
    Physical address in host memory of the received packet buffer.
Length Field (16-bit offset 0, 2nd line)
    The length indicated in this field covers the data written to a receive buffer including CRC bytes (if
    any). Software must read multiple descriptors to determine the complete length for packets that
    span multiple receive buffers.

333369-009                                                                                                    395
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

Fragment Checksum (16-bit offset 16, 2nd line)
      This field is used to provide the fragment checksum value. This field is equal to the unadjusted 16-
      bit ones complement of the packet. Checksum calculation starts at the L4 layer (after the IP
      header) until the end of the packet excluding the CRC bytes. To use the fragment checksum assist
      to offload L4 checksum verification, software might need to back out some of the bytes in the
      packet. For more details see Section 7.1.6.5.
      The fragment checksum is always reported in the descriptor with the EOP bit set.
Status Field (8-bit offset 32, 2nd line)
      Status information indicates whether the descriptor has been used and whether the referenced
      buffer is the last one for the packet. Error status information is listed in Table 7-17.

      Table 7-16. Receive Status (RDESC.STATUS) Layout
           7               6              5                 4            3                2               1                0

           PIF         IPCS             L4CS           UDPCS             VP           Reserved          EOP                DD

      End of Packet (EOP) and Descriptor Done (DD)
          Refer to the following table:

               DD     EOP                                                 Description

                 0     0       Software setting of the descriptor when it hands it to the hardware.

                 0     1       Reserved (invalid option).

                 1     0       A completion status indication for non-last descriptor of a packet that spans across multiple
                               descriptors. It means that the hardware is done with the descriptor and its buffers while only the
                               length is valid on this descriptor.

                 1     1       A completion status indication of the entire packet. Software might take ownership of its
                               descriptors while all fields in the descriptor are valid.

      VP (VLAN Packet)
          When set, the VP field indicates that the incoming packet's type is a VLAN (802.1q, matching
          the VLNCTRL.VET). If the RXDCTL.VME bit is set as well, an active VP field also means that the
          VLAN has been stripped from the packet to the receive descriptor. For a further description of
          802.1q VLANs, see Section 7.4.
      IPCS (IPv4 Checksum), L4CS (L4 Checksum), UDPCS (UDP Checksum)
          These bits are described in the following table.
          Note:      Switched packets from a local VM that do not use the Tx IP checksum offload by
                     hardware have the IPCS equal to zero; switched packets from a local VM that do not
                     use the Tx L4 checksum offload by hardware have the L4CS and UDPCS equal to zero.

            L4CS     UDPCS      IPCS                                           Functionality

                 0     0          0        Hardware does not provide checksum offload.

                 0     0          1        Hardware provides IPv4 checksum offload. Pass/fail indication is provided in the Error
                                           field – IPE.

                 1     0         1/0       Hardware provides IPv4 checksum offload if IPCS is active along with TCP checksum
                                           offload. Pass/fail indication is provided in the Error field – IPE and TCPE.

                 1     1         1/0       Hardware provides IPv4 checksum offload if IPCS is active along with UDP checksum
                                           offload. Pass/fail indication is provided in the Error field – IPE and TCPE.

396                                                                                                                   333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

          IPv6 packets do not have the IPCS bit set, but might have the L4CS bit and UDPCS bit set if the
          X550 recognizes the transport header.
    PIF (Non Unicast Address)
          The PIF bit is set on packets with a non-unicast destination Ethernet MAC Address — multicast
          and broadcast.
Error Field (8-bit offset 40, 2nd line)
    Table 7-17 and the following text describes the possible errors reported by the hardware.

    Table 7-17. Receive Errors (RDESC.ERRORS) Layout
             7          6             5           4            3            2            1            0

           IPE         TCPE       Reserved     Reserved     Reserved     Reserved     Reserved       RXE

    IPE (IPv4 Checksum Error)
          The IP checksum error is valid only when the IPCS bit in the Status field is set (indicating that
          the hardware validated the IP checksum). This bit is meaningful only on the last descriptor of a
          packet while the EOP bit is set as well. Packets with IP error are posted to host memory
          regardless of the store bad packet setting (FCTRL.SBP).
    TCPE (TCP/UDP Checksum Error)
          The TCP/UDP checksum error is valid only when the L4CS bit in the Status field is set (indicating
          that the hardware validated the L4 checksum). This bit is meaningful only on the last descriptor
          of a packet while the EOP bit is set as well. Packets with a TCP/UDP error are posted to host
          memory regardless of the store bad packet setting (FCTRL.SBP).
          IPv4/UDP packets that carry a null UDP checksum field are reported with L4CS = 0 and TCPE =

# 0 (valid packet with no checksum).

          IPv6/UDP packets that carry a null UDP checksum field are reported with L4CS = 1 and TPCE =

# 1 (UDP checksum is mandatory over IPv6).

    RXE
          The RXE error bit is an indication for any MAC error. It is a logic OR function of the following
          errors:
           • CRC or symbol error might be a result of receiving a /V/ symbol on the TBI interface, /FE/
             symbol on the GMII/XGMII interface, RX_ER assertion on GMII interface, bad EOP or loss of
             sync during packet reception.
           • Undersize frames shorter than 64 bytes.
           • Oversize frames larger than the MFS definition in the MAXFRS register.
           • Length error in 802.3 packet format. Length field is not checked in presence of a VLAN or
             E-Tag.
          Packets with an RXE error are posted to host memory only when store bad packet bit
          (FCTRL.SBP) is set.

333369-009                                                                                                   397
                                 Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                          Inline Functions

VLAN Tag Field (16-bit offset 48, 2nd line)
      If the RXDCTL.VME is set and the received packet type is 802.1q (as defined by VLNCTRL.VET), the
      VLAN header is stripped from the packet data storage. In this case the 16 bits of the VLAN tag,
      priority tag and DEI from the received packet are posted to the VLAN Tag field in the receive
      descriptor. Otherwise, the VLAN Tag field contains 0x0000.

      Table 7-18. VLAN Tag Field Layout (for 802.1q Packet)
      15         13   12    11                                             0

           PRI        DEI                    VLAN

      Priority and DEI are part of 802.1Q specifications. The VLAN field is provided in network order.

#### 7.1.5.2 Advanced Receive Descriptors

7.1.5.2.1                   Advanced Receive Descriptors — Read Format

Table 7-19 lists the advanced receive descriptor programming by the software. The
SRRCTL[n].DESCTYPE should be set to a value other than 000b when using the advanced descriptor
format.

Table 7-19. Descriptor Read Format
           63                                                                                                  1     0

# 0 Packet Buffer Address [63:1]

# 8 Header Buffer Address [63:1]                                            DD

Packet Buffer Address (64)
      The physical address in host memory of the packet buffer.
Header Buffer Address (64)
      The physical address in host memory of the header buffer with the lowest bit being Descriptor Done
      (DD). When a packet spans in multiple descriptors, only the header buffer of the first descriptor is
      used. In subsequent descriptors, only the data buffer is used.
      During the programming phase, software must set the DD bit to zero (see the description of the DD
      bit in this section). This means that header buffer addresses are always word aligned.
Note:        The X550 does not support null descriptors meaning packet or header addresses are zero.

398                                                                                                           333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.1.5.2.2                   Advanced Receive Descriptors — Write-Back Format

When the X550 writes back the descriptors, it uses the format listed in Table 7-20. The advanced
descriptor writeback format is used when SRRCTL[n]. DESCTYPE is set to a value other than 000b.

Table 7-20. Descriptor Write-Back Format
      63   ...      . . . . . 48 47 . ..        . . . 32    31     30   .   . . . 21 20        .17 16 .        . . . . . . 4 3.. . . . 0
      RSS Hash / Fragment Checksum / FCoE_PARAM

    0 SPH          HDR_LEN          RSCCNT            Packet Type         RSS Type

                 / Flow Director Filters ID

    8 VLAN Tag                 PKT_LEN                   Extended Error                        Extended Status / NEXTP

      63   ...       . . . . . 48 47 . .. .       . . 32   31    .....      . . . . . . 20    19   ...          . . . . . . . . . . . . .. 0

RSS Type (4-bit offset 0, 1st line)
     The X550 must identify the packet type and then choose the appropriate RSS hash function to be
     used on the packet. The RSS type reports the packet type that was used for the RSS hash function.

           RSS Type                                                         Description

     0x0                   No hash computation done for this packet

     0x1                   HASH_TCP_IPv4

     0x2                   HASH_IPv4

     0x3                   HASH_TCP_IPv6

     0x4                   Reserved

     0x5                   HASH_IPv6

     0x6                   Reserved

     0x7                   HASH_UDP_IPv4

     0x8                   HASH_UDP_IPv6

     0x9 – 0xE             Reserved

     0xF                   Packet reports flow director filters status (set if flow director match, even if packet is forwarded by
                           another filter).

Packet Type (13-bit at offset 4, 1st line)
     The Packet Type field reports the packet type identified by the hardware as follows. Note that some
     of the fields in the receive descriptor are valid for specific packet types.

                                                                                  Bit 11 = 1 (L2 packet matching one of the ETQF
      Bit Index                            Bit 11 = 0
                                                                                                      filters)

# 0 IPV4 — IPv4 header present

                                                                                  EtherType — ETQF register index that matches the

# 1 IPV4O — IPv4 with options                                   packet. Special types are defined for 802.1X,

                                                                                  and FCoE.

# 2 IPV6 — IPv6 header present

# 3 IPV6E- IPv6 with extensions

                                                                                  Reserved.

    4 TCP — TCP header present

333369-009                                                                                                                               399
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

                                                                               Bit 11 = 1 (L2 packet matching one of the ETQF
       Bit Index                           Bit 11 = 0
                                                                                                   filters)

    5 UDP — UDP header present

    6 SCTP — SCTP header

                     If bit 12 = 0 - Reserved
                     If bit 12 = 1:

# 7 Reserved.

                       0b = NVGRE
                       1b = XLAN

# 8 IPsec ESP – IPsec encapsulation

# 9 IPsec AH – IPsec encapsulation

# 10 Reserved                                                  Reserved.

          11         0b = non L2 packet                                        1b = L2 packet

                     NVGRE or VXLAN Tunnel Packet. If this bit is set, bit 7

# 12 Reserved.

                     indicates the tunnel type.

      Note:        UDP, TCP and IPv6 indications are not set in any IPv4 fragmented packet.
                   In virtualization mode, packets might be received from other local VMs. The X550 does
                   not check the L5 header for these packets and does not report NFS header. If such
                   packets carry IP tunneling (IPv4 — IPv6), they are reported as IPV4E. The packets
                   received from local VM are indicated by the LB bit in the status field. To be identified, the
                   CC bit in the transmit descriptor must be set and if it is a tunnel packet, the
                   TUNNEL.OUTERIPCS must be set also. If bit 12 (Tunnel Packet) is set, all the L3/L4
                   indications (IPV4, IPV4O, IPV6, IPV6E, TCP, UDP, SCTP) reflects the inner header status.
RSC Packet Count- RSCCNT (4-bit offset 17, 1st line)
      The RSCCNT field is valid only for RSC descriptors while in non-RSC it equals zero. RSCCNT minus
      one indicates the number of coalesced packets that start in this descriptor. RSCCNT might count up
      to 14 packets. Once 14 packets are coalesced in a single buffer, RSC is closed enabling accurate
      coalesced packet count. If the RSCCNTBP bit in RDRXCTL is set, coalescing might proceed beyond
      the 14 packets per buffer while RSCCNT stops incrementing beyond 0xF.
      Note:        Software can identify RSC descriptors by checking the RSCCNT field for non-zero value.
HDR_LEN (10-bit offset 21, 1st line)
      The HDR_LEN reflects the size of the packet header in byte units (if the header is decoded by the
      hardware). This field is meaningful only in the first descriptor of a packet and should be ignored in
      any subsequent descriptors. Header split is explained in Section 7.1.6 while the packet types for
      this functionality are enabled by the PSRTYPE[n] registers.
Split Header — SPH (1-bit offset 31, 1st line)
      When set to 1b, indicates that the hardware has found the length of the header. If set to 0b, the
      header buffer may be used only in split always mode. If the received header size is greater or equal
      to 1024 bytes, the SPH bit is not set and header split functionality is not supported. The SPH bit is
      meaningful in all the descriptors of a packet. See additional details on SPH, PKT_LEN and HDR_LEN
      as a function of split modes in Table 7-25.

400                                                                                                                  333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                                                                                         Header Length
                                     Packet Type                                     (Includes All Fields Up     Header Split
                                                                                     to the Field Specified)

     Un-recognized EtherType only with/without SNAP and with/without VLAN, or       VLAN header(s) if present.       No
     packets that match the L2 filters (MTQF) other than FCoE with/without VLAN.    Else, EtherType field

     FCoE packet without ESP option header.                                         FC header including FC          N/A1
                                                                                    options

     FCoE packet with ESP option header.                                            FC header excluding FC          N/A1
                                                                                    options

     Pv4 only or fragmented IPv4 with any payload including IPv4-IPv6 tunneling.    IPv4 header                    Enabled

     Non-fragmented IPv4, TCP / UDP / SCTP.                                         L4 header                      Enabled

     IPv4-IPv6, only or fragmented IPv4-IPv6 at IPv6 header with any payload.       IPv6 header (up to the         Enabled
                                                                                    fragment extension header
                                                                                    if exist)

     IPv4-IPv6,TCP / UDP / SCTP.                                                    L4 header                      Enabled

     VXLAN or NVGRE.                                                                Cloud Header/L2 Header         Enabled2

    1. Header split is not permitted in queues that might receive FCoE packets.
    2. If cloud split modes used (PSRTYPE15 or PSRTYPE16 are set). If not, according to internal header.

RSS Hash or FCOE_PARAM or Flow Director Filters ID (32-bit offset 32, 1st line) / Fragment Checksum
(16-bit offset 48, 1st line)
    This field has multiplexed functionality according to the received packet type (reported on the
    Packet Type field in this descriptor) and device setting.
    FCoE_PARAM
         For FCoE packets that matches a valid DDP context, this field holds the PARAM field in the DDP
         context after processing the received packet. If the Relative Offset Present bit in the F_CTL was
         set in the data frames, the PARAM field indicates the size in bytes of the entire exchange
         inclusive the frame reported by this descriptor. This field is valid for FCoE packets for which the
         FCSTAT field is non zero.
    Fragment Checksum
         For fragmented UDP/IP packets, this field holds the UDP fragment checksum (described in
         Section 7.1.6.5) if both the RXCSUM.PCSD bit is cleared and RXCSUM.IPPCSE bit is set. This
         field is meaningful only for UDP packets where the UDPV bit in the Extended Status word is set.
         When Fragment Checksum is reported, bits 47:32 are invalid.
         The checksum does not include any padding or timestamp added by the device.
    RSS Hash / Flow Director Filters ID
         For non-FCoE packets, if the RXCSUM.PCSD bit is set, this field holds the RSS hash value or flow
         director filters ID.
          • If the FDIRCTRL.REPORT_STATUS bit is set, the flow director filters ID is reported;
          • If the RSS Type is non zero, the RSS hash is reported.
          • Otherwise, the value is not valid.

333369-009                                                                                                                   401
                                     Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                          Inline Functions

           Table 7-21. Checksum Enable/Disable
                RXCSUM.PCSD                    0 (Checksum Enable)                                            1 (Checksum Disable)

                                 Fragment Checksum and IP Identification are              RSS Hash value is reported in the Rx Descriptor.
                                 reported in the Rx Descriptor.

      RSS Hash
           The RSS hash value is required for RSS functionality as described in Section 7.1.3.7. Note that
           the RSS hash is meaningful only for ‘RSS Type’ in the range 0x1 to 0x8.
      Flow Director Filters ID
           The flow director filters ID is reported only when the received packet matches a flow directory
           filter (see Section 7.1.3.6). The flow director filter ID field has a different structure for
           signature-based filters and perfect match filters as follows:

                             Filter Type                   31          30            29       28              16   15          13      12             0

            Hash-based Flow Director Filter ID             Rsv                   Bucket Hash                                   Signature

            Perfect Match Flow Director Filter ID                      Rsv                         Hash                  Rsv            SW-Index

           Bucket Hash — A hash value that identifies a flow director bucket. When the Flow Director table
           is smaller than 32 K filters the bucket hash is smaller than 15 bits. In this case the upper bit(s)
           are set to zero.
           Signature — A hash value used to identify flow within a bucket.
           SW-Index — The SW-Index that is taken from the filter context, programmed by software. It is
           meaningful only when the FLM bit in the Extended Status is set as well.
           Rsv — Reserved.
Extended Status / NEXTP (20-bit offset 0, 2nd line)
      Status information indicates whether the descriptor has been used and whether the referenced
      buffer is the last one for the packet. Table 7-22 lists the Extended Status word in the last descriptor
      of a packet (EOP bit is set). Table 7-23 lists the Extended Status word in any descriptor but the last
      one of a packet (EOP bit is cleared).

      Table 7-22. Receive Status (RDESC.STATUS) Layout of Last Descriptor
           19           18             17           16           15              14                13              12           11             10

           BMC          LB            SECP          TS           TSIP                              Rsv                          Rsv           UDPV

                                                    IPCS         L4I         UDPCS
        VEXT        OUTERIPCS          PIF                                                         VP              FLM          EOP            DD
                                                 FCEOFs                 FCSTAT

            9            8                 7         6            5              4                  3              2               1              0

      Table 7-23. Receive Status (RDESC.STATUS) Layout of Non-Last Descriptor
      19                                                                                  4             3:2                1                  0

                              Next Descriptor Pointer — NEXTP                                           Rsv             EOP = 0b              DD

402                                                                                                                                         333369-009
                                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

    Rsv (14:11)
        Reserved at zero.
    FLM(2)
        Flow director filter match indication is set for packets that match these filters.
    VP(3), PIF (7)
        These bits are described in the legacy descriptor format in Section 7.1.5. The VP bit is not set
        even if a VLAN tag is present if the PFQDE.HIDE_VLAN bit is set for the queue.
    EOP (1) and DD (0)
        End of Packet and Done bits are listed in the following table:

             DD       EOP                                                 Description

    0 X      Software setting of the descriptor when it hands it to hardware.

              1        0      A completion status indication for a non last descriptor of a packet (or multiple packets in the case
                              of RSC) that spans across multiple descriptors. In a single packet case the DD bit indicates that
                              the hardware is done with the descriptor and its buffers. In the case of RSC, the DD bit indicates
                              that the hardware is done with the descriptor but might still use its buffers (for the coalesced
                              header) until the last descriptor of the RSC completes.
                              Only the Length fields are valid on this descriptor. In the RSC case, the next descriptor pointer
                              and RSCCNT are valid as well.

              1        1      A completion status indication of the entire packet (or the multiple packets in the case of RSC)
                              and software might take ownership of its descriptors.
                              All fields in the descriptor are valid (reported by the hardware).

    UDPCS (4), L4I (5) / FCSTAT (5:4)
        This field has multiplexed functionality for FCoE and non-FCoE packets. Hardware identifies
        FCoE packets in the filter unit and indicates it in the Packet Type field in the Rx descriptor. For
        non-FCoE packets this field is UDPCS and L4I. The UDPCS (UDP checksum) is set (together with
        L4CS bit) when hardware provides UDP checksum offload. The L4I (L4 Integrity) is set when
        hardware provides any L4 offload as: UDP checksum, TCP checksum or SCTP CRC offload. For
        FCoE packets, this field represents the FCSTAT (FCoE Status) as follows:

             FCSTAT                                                    Meaning

# 00 No match to any active FC context

# 01 FCoE frame matches an active FC context with no DDP. The entire frame is posted to the receive buffer

                      indicated by this descriptor.

# 10 FCP_RSP frame received that invalidates an FC read context or last data packet in a sequence with

                      sequence initiative set that invalidates an FC write context.

# 11 FCoE frame matches an active FC context and found liable for DDP by the filter unit. The packet's data was

                      posted directly to the user buffers if no errors were found by the DMA unit as reported in the FCERR field.
                      If any error is found by the DMA unit the entire packet is posted to the legacy queues.

    IPCS(6), FCEOFs (6)
        This bit has multiplexed functionality for FCoE and non-FCoE packets. The hardware identifies
        FCoE packets in the filter unit and indicates it in the Packet Type field in the Rx descriptor.
        For non-FCoE packets it is IPCS as described in Legacy Rx descriptor (in Section 7.1.5).
        For FCoE packets, this bit and the FCEOFe bit in the Extended Error field indicates the received
        EOF code as follows:

333369-009                                                                                                                       403
                                   Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                                        Inline Functions

           FCEOFe     FCEOFs                   Description and Digested Meaning and Device Behavior

                 0       0      EOFn. Nominal operation, DDP is enabled.

                 0       1      EOFt. Nominal operation (end of sequence), DDP is enabled.

                 1       0      Unexpected EOFn-EOFt or SOFi-SOFn. No DDP while filter context is updated by the packet.

                 1       1      EOFa, EOFni or un-recognized EOF / SOF. No DDP while filter context is invalidated.

      OUTERIPCS(8)
         Indicates that a checksum was done on the outer IP header of an NVGRE or VXLAN packet.
      VEXT (9)
         Outer-VLAN is found on a double VLAN packet. This bit is valid only when
         CTRL_EXT.EXTENDED_VLAN is set. See more details in Section 7.4.5.
      UDPV (10)
         The UDP Checksum Valid bit indicates that the incoming packet contains a valid (non-zero
         value) checksum field in an incoming fragmented (non-tunneled) UDP IPv4 packet. It means
         that the Fragment Checksum field in the receive descriptor contains the UDP checksum as
         described in Section 7.1.6.5. When this field is cleared in the first fragment that contains the
         UDP header, it means that the packet does not contain a valid UDP checksum and the checksum
         field in the Rx descriptor should be ignored. This field is always cleared in incoming fragments
         that do not contain the UDP header.
      TSIP (15)
         Timestamp in packet. The Timestamp In Packet bit is set to indicate that the received packet
         arrival time was captured by the hardware and the timestamp was placed in the receive buffer.
         For more details see Section 7.7 and Section 7.1.6.2.
      TS (16)
         The Time Stamp bit is set when the device recognized a time sync packet. In such a case the
         hardware captures its arrival time and stores it in the Time Stamp register. For more details see
         Section 7.7.
      SECP (17)
         Security Processing bit indicates that the hardware identified the security encapsulation and
         processed it as configured.
         IPsec processing — This bit is set only if a matched SA was found. Note that hardware does not
         process packets with an IPv4 option or IPv6 extension header and the SECP bit is not set. This
         bit is not set for IPv4 packets shorter than 70 bytes, IPv6 ESP packets shorter than 90 bytes, or
         IPv6 AH packets shorter than 94 bytes (all excluding CRC). Note that these packet sizes are
         never expected and set the length error indication in the SECERR field.
      LB (18)
         This bit provides a loopback status indication which means that this packet is sent by a local VM
         (VM to VM switch indication).
      BMC (19)
         Packet received from BMC. The BMC bit is set to indicate the packet was sent by the local BMC.
         Bit is cleared if packet arrives from the network. For more details see Section 11.4.2.2.

404                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

    NEXTP (19:4)
        Large receive might be composed of multiple packets and packets might span in multiple
        buffers (descriptors). These buffers are not guaranteed to be consecutive while the NEXTP field
        is a pointer to the next descriptor that belongs to the same RSC. The NEXTP field is defined in
        descriptor unit (the same as the head and tail registers). The NEXTP field is valid for any
        descriptor of a large receive (the EOP bit is not set) except the last one. It is valid even in
        consecutive descriptors of the same packet. In the last descriptor (on which the EOP bit is set),
        NEXTP is not indicated but rather all other status fields previously described in this section.
Extended Error (12-bit offset 21, 2nd line)
    Table 7-24 and the following text describe the possible errors reported by hardware.

    Table 7-24. Receive Errors (RDESC.ERRORS) Layout
         11            10             9             8:7             6              5:4             3                 2:0

         IPE
                       L4E          RXE           SECERR       OUTERIPER           Rsv            HBO        FCERR / FDIRERR
       FCEOFe

    FCERR (2:0)
        Defines error cases for FCoE packets. Note that hardware indicates FCoE packet recognition on
        the Packet Type field in the Rx descriptor. Packets with FCERR are posted to host memory
        regardless of the store bad packet setting in the Filter Control register. This field must be
        ignored when FCSTAT is 00b.

          FCERR Code                                                    Meaning

                000     No exception errors found

                001     Bad FC CRC. Hardware does not check any other FC fields in the packet.

                010     One of the following error indications found by the filter unit (hardware auto-invalidates a matched DDP
                        filter context if exists):
                          1. Received non-zero abort sequence condition in the F_CTL field in FC read packet.
                          2. Received EOFa or EOFni or any un-recognized EOF or SOF flags.

                011     The DMA unit gets FCoE packets that match a DDP context while it missed the packet that was marked
                        as first by the filter unit. Filter context parameters might be updated while DMA context parameters are
                        left intact (see error code 101b).

                100     One of the following cases:
                         1. Unsupported FCoE version. FCSTAT equals to 00b.
                         2. Out of order reception (SEQ_CNT does not match expected value) of a packet that matches an
                            active DDP context. The filter unit might set the FCSTAT to 01b, or 10b.

                101     No DMA resources due to one of the following cases listed while the hardware auto-invalidates the DDP
                        DMA context. Software should invalidate the filter context before it can reuse it.
                         1. Last buffer exhausted (no space in the user buffers).
                         2. Legacy receive queue is not enabled or no legacy receive descriptor.
                         3. Some cases of a missed packet as described in FCERR code 011b and 110b.

                110     Filter context valid and DMA context invalid. Indicates that some packet(s) were lost by the DMA
                        context due to lack of legacy receive descriptors or were missed by the Rx packet buffer.
                         1. This error code might also be received in some cases of a missed packet as described in FCERR
                             code 011b.

                111     Reserved

333369-009                                                                                                                   405
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

      FDIRERR (2:0)
         This field is relevant for non-FCoE packets when the flow director filters are enabled.
         FDIRErr(0) - Length — If the flow director filter matches the Length bit, this indicates that the
         distance of the matched filter from the hash table exceeds the FDIRCTRL.Max-Length. If there
         is no matched filter, the Length bit is set if the flow director linked list of the matched hash
         value exceeds the FDIRCTRL.Max-Length.
         FDIRErr(1) - Drop — The Drop bit indicates that a received packet matched a flow director filter
         with a drop action. In the case of perfect mode filtering, it is expected to find the drop
         indication only when the linked list in the flow director bucket exceeds the permitted Max-
         Length. In this case, the packet is not dropped. Instead, it is posted to the Rx queue (indicated
         in the filter context) for software handling of the Max-Length exception. In the case of hash
         mode filtering, it is expected that the drop queue is always a valid queue so all packets that
         match the drop filter are visible to software.
         FDIRErr(2) - Coll — A matched flow director filter with a collision indication was found. The
         collision indicates that software attempted to step over this filter with a different action that
         was already programmed.
      HBO (3)
         The Header Buffer Overflow bit is set if the packet header (calculated by hardware) is bigger
         than the header buffer (defined by SSRCTL.BSIZEHEADER). HBO reporting might be used by
         software to allocate bigger buffers for the headers. It is meaningful only if the SPH bit in the
         receive descriptor is set as well. The HDR_LEN field is valid even when the HBO bit is set.
         Packets with HBO error are posted to host memory regardless of the store bad packet setting
         (FCTRL.SBP). Packet DMA to its buffers when the HBO bit is set, depends on the device settings
         as follows:

                SRRCTL.DESCTYPE                                            DMA Functionality

          Header Split (010b)            The header is posted with the rest of the packet data to the packet buffer.

          Always Split Mode (101b)       The header buffer is used as part of the data buffers and contains the first
                                         SRRCTL.BSIZEHEADER bytes of the packet.

      Rsv (5:4)
         Reserved at zero.
      OUTERIPER (6)
         Indicates an error was found in the checksum of an outer IP header of a VXLAN or NVGRE
         packet or that the UDP checksum of the outer UDP header in a VXLAN packet was not zero.
      SECERR (8:7)
         Security error indication for IPsec. This field is meaningful only if the SECP bit in the extended
         status is set.

           SECERR                                               IPsec Error Reporting

# 00 No errors found while an active SA found or no security processing.

# 01 Invalid IPsec Protocol: IPsec protocol field (ESP or AH) in the received IP header does not match expected

                       one stored in the SA table.

406                                                                                                                     333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

             SECERR                                              IPsec Error Reporting

# 10 Length error: ESP packet is not 4-bytes aligned or AH/ESP header is truncated (for example, a 28-byte

                        IPv4 packet with IPv4 header + ESP header that contains only SPI and SN) or AH Length field in the AH
                        header is different than 0x07 for IPv4 or 0x08 for IPv6 or the entire packet size excluding CRC is shorter
                        than 70 bytes for IPv4 or 90 bytes for IPv6 ESP or 94 bytes for IPv6 AH.

# 11 Authentication failed: Bad signature.

    RXE (9)
        RXE is described in the legacy descriptor format in Section 7.1.5.
    L4E (10)
        L4 integrity error is valid only when the L4I bit in the Status field is set. It is active if L4
        processing fails (TCP checksum or UDP checksum or SCTP CRC). Packets with L4 integrity error
        are posted to host memory regardless of the store bad packet setting (FCTRL.SBP). In case of
        VXLAN or NVGRE packets, this relates to the internal L4 header.
    FCEOFe(11) / IPE(11)
        This bit has multiplexed functionality. FCoE packets are indicated as such in the Packet Type
        field in the Rx descriptor.

                          Non-FCoE Packet                                                    FCoE Packet

     IPE (IPv4 checksum error) is described in Section 7.1.5. In     FC EOF Exception (FCEOFe). This bit indicates unexpected
     case of VXLAN or NVGRE packets, this relates to the internal    EOF or SOF flags. The specific error is defined by the FCEOF
     IP header.                                                      bit in the extended status previously described.

PKT_LEN (16-bit offset 32, 2nd line)
    PKT_LEN holds the number of bytes posted to the packet buffer. The length covers the data written
    to a receive buffer including posted CRC bytes (if any). Software must read multiple descriptors to
    determine the complete length for packets that span multiple receive buffers. If SRRCTL.DESCTYPE
    = 2 (advanced descriptor header splitting) and the buffer is not split because the header is bigger
    than the allocated header buffer, this field reflects the size of the data written to the data buffer
    (header + data).
    When short packets are padded, the PKT_LEN does not include the padding, so that the software
    device driver can detect the location of a potential time stamp in the packet.
    When a time stamp is added (TSIP bit is set), the PKT_LEN includes the timestamp size (+8).
VLAN Tag (16-bit offset 48, 2nd line)
    This field is described in the legacy descriptor format in Section 7.1.5. The VLAN tag is set to
    0x0000 even if a VLAN tag is present if the PFQDE.HIDE_VLAN bit is set for the queue.

#### 7.1.5.3 Receive Descriptor Fetching

The X550 implements a fetch-by-demand mechanism for descriptor fetch. Descriptors are not fetched
in advance, but rather fetched after a packet is received. Such a strategy eliminates the need to store
descriptors on-die for each and every descriptor queue in anticipation for packet arrival.

333369-009                                                                                                                      407
                                     Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                          Inline Functions

#### 7.1.5.4 Receive Descriptor Write-Back

The X550 writes back the receive descriptor immediately following the packet write into system
memory. It is therefore possible for a single descriptor to be written at a time into memory. However, if
aggregation occurs during descriptor fetch (see Section 7.1.5.3), the descriptors fetched in the
aggregated operation are written back in a single write-back operation. In Receive Coalescing (RSC), all
the descriptors except the last one are written back when they are completed. This does not have to be
on packet boundaries but rather when the next descriptor of the same RSC is fetched. See
Section 7.10.5.1 for more on RSC.
Note:     Software can determine if a packet has been received only by checking the receive descriptor
          DD bit in memory. Checking through DD bits (and not by checking the receive head pointer in
          RDH/RDL registers) eliminates a potential race condition: all descriptor data is posted
          internally prior to incrementing the head register and a read of the head register could
          potentially pass the descriptor waiting inside the X550.

#### 7.1.5.5 Receive Descriptor Queue Structure

Figure 7-11 shows the structure of each of the receive descriptor rings. Note that each ring uses a
contiguous memory space.

                                               Circular Buffer Queues

                       Base

                                                                        Head

                                                                                          Receive
                                                                                          Queue

                                                                        Tail

                      Base + Size

Figure 7-11. Receive Descriptor Ring Structure

Software inserts receive descriptors by advancing the tail pointer(s) to refer to the address of the entry
just beyond the last valid descriptor. This is accomplished by writing the descriptor tail register(s) with
the offset of the entry beyond the last valid descriptor. The X550 adjusts its internal tail pointer(s)
accordingly. As packets arrive, they are stored in memory and the internal head pointer(s) is increased
by the X550.

408                                                                                                           333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

When RSC is not enabled, the visible (external) head pointer(s) reflect the internal ones. On any
receive queue that enables RSC, updating the external head pointer might be delayed until interrupt
assertion. When the head pointer(s) is equal to the tail pointer(s), the queue(s) is empty. The X550
stops storing packets in system memory until software advances the tail pointer(s), making more
receive buffers available.

                                                        Software writes a                  Head
                                                        descriptor to the
                Base +2                                                                                         First Descriptor added
                                                        memory ring and
            Base +1

# 1 Head &Tail         moves the tail

        Base                           Together                                                          Tail
     Base + size

                                                 Software writes another
                                               descriptor to the memory ring
                                                                                           Head
                              Head                                                                   oldest first to
                                      oldest first to                                                 be added
                                       be added
     3                                                                         4                            Second
                                          newest latest                                                   descriptor to
                                           to be added                                                     be added
                                          Tail                                                       newest latest
      The tail moves down after the newest                                                           to be added
    descriptor was inserted between the old tail                                              Tail
         location and the new tail location                                        Previous Head     Head moves towards the tail and
                       Head                                                           location        frees-up the buffer to the SW.
                                     Data from the packet represented by
                                      this descriptor is stored in memory

     5                                                                         6                        Data from the packet represented by
                                                                                                         this descriptor is stored in memory

                                            Tail
         Original Head location                                                                       Tail
                                  Previous Head location

                                        Head moves towards the tail and
     7                                   frees-up the buffer to the SW         8
                                                                                                                Head and
                                                                                                                  Tail
                                                                                                                Together
                                            Tail

Figure 7-12. Descriptors and Memory Rings

The X550 writes back used descriptors just prior to advancing the head pointer(s). Head and tail
pointers wrap back to base when the number of descriptors corresponding to the size of the descriptor
ring have been processed.
The receive descriptor head and tail pointers reference to 16-byte blocks of memory. Shaded boxes in
Figure 7-12 represent descriptors that have stored incoming packets but have not yet been recognized
by software. Software can determine if a receive buffer is valid by reading descriptors in memory rather
than by I/O reads. Any descriptor with a DD bit set has been used by the hardware, and is ready to be
processed by software.
Note:         The head pointer points to the next descriptor that is to be written back. At the completion of
              the descriptor write-back operation, this pointer is increased by the number of descriptors
              written back. Hardware owns all descriptors between [head... tail]. Any descriptor not in this
              range is owned by software.

333369-009                                                                                                                                     409
                                           Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

The receive descriptor rings are described by the following registers:
 • Receive Descriptor Base Address registers (RDBA) — This register indicates the start of the
   descriptor ring buffer; this 64-bit address is aligned on a 128-byte boundary and is stored in two
   consecutive 32-bit registers. Hardware ignores the lower 7 bits.
 • Receive Descriptor Length registers (RDLEN) — This register determines the number of bytes
   allocated to the circular buffer. This value must be a multiple of 128 (the maximum cache line size).
   Since each descriptor is 16 bytes in length, the total number of receive descriptors is always a
   multiple of 8.
 • Receive Descriptor Head registers (RDH) — This register holds a value that is an offset from
   the base, and indicates the in-progress descriptor. There can be up to 64K-8 descriptors in the
   circular buffer. Hardware maintains a shadow copy that includes those descriptors completed but
   not yet stored in memory.
      Software can determine if a packet has been received by either of two methods: reading the DD bit
      in the receive descriptor field or by performing a Programmed I/O read of the Receive Descriptor
      Head register. Checking the descriptor DD bit in memory eliminates a potential race condition. All
      descriptor data is written to the I/O bus prior to incrementing the head register, but a read of the
      head register could pass the data write in systems performing I/O write buffering. Updates to
      receive descriptors use the same I/O write path and follow all data writes. Consequently, they are
      not subject to the race.
 • Receive Descriptor Tail registers (RDT) — This register holds a value that is an offset from the
   base, and identifies the location beyond the last descriptor hardware can process. This is the
   location where software writes the first new descriptor.
If software statically allocates buffers, and uses a memory read to check for completed descriptors, it
simply has to zero the status byte in the descriptor to make it ready for re-use by hardware. This is not
a hardware requirement, but is necessary for performing an in-memory scan. This is relevant only to
legacy descriptors.
All the registers controlling the descriptor rings behavior should be set before receive is enabled, apart
from the tail registers which are used during the regular flow of data.

7.1.5.5.1              Low Receive Descriptors Threshold

As previously described, the size of the receive queues is measured by the number of receive
descriptors. During run time, software processes descriptors and upon completion of descriptors,
increments the Receive Descriptor Tail registers. At the same time, the hardware may post new
received packets incrementing the Receive Descriptor Head registers for each used descriptor.
The number of usable (free) descriptors for the hardware is the distance between the Tail and Head
registers. When the tail reaches the head, there are no free descriptors and further packets might be
either dropped or block the receive FIFO. To avoid this situation, the X550 might generate a low latency
interrupt (associated to the relevant Rx queue) once there are less equal free descriptors than specified
by a low level threshold. The threshold is defined in 64 descriptors granularity per queue in the
SRRCTL[n].RDMTS field.

410                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.1.6 Receive Offloads

#### 7.1.6.1 Header Splitting

7.1.6.1.1                  Purpose

This feature consists of splitting a packet header to a different memory space. This helps the host to
fetch headers only for processing: headers are posted through a regular snoop transaction to be
processed by the host CPU. It is recommended to perform this transaction with TPH enabled (see
Section 7.5).
The X550’s support for header split is controlled by the DESCTYPE field of the Split Receive Control
registers (SRRCTL). The following modes exist in both split and non-split modes:
 • 000b: Legacy mode — Legacy descriptors are used, headers and payloads are not split.
 • 001b: Advanced mode, no split — Advanced descriptors are in use, header and payload are not
   split.
 • 010b: Advanced mode, header split — Advanced descriptors are in use, header and payload are
   split to different buffers.
 • 101b: Advanced mode, split always — Advanced descriptors are in use, header and payload are
   split to different buffers. If no split is done, the first part of the packet is stored in the header buffer.
The X550 uses packet splitting when the SRRCTL[n].DESCTYPE is greater than one.

7.1.6.1.2                  Description

                     63                                    32    31                               0

# 0 Packet Buffer address

# 8 Header Buffer address

                                                Packet Header

                          Header                                                      Header
                                                                                      Buffer

                                               Packet Payload
                                                                                      Data
                          Payload                                                     Buffer

                                                                                    Host memory

Figure 7-13. Header Splitting Diagram

The physical address of each buffer is written in the Buffer Addresses fields:
 • The packet buffer address includes the address of the buffer assigned to the packet data.
 • The header buffer address includes the address of the buffer that contains the header information.
   The receive DMA module stores the header portion of the received packets into this buffer.

333369-009                                                                                                   411
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Inline Functions

The sizes of these buffers are statically defined in the SRRCTL[n] registers:
 • The BSIZEPACKET field defines the size of the buffer for the received packet.
 • The BSIZEHEADER field defines the size of the buffer for the received header. If header split is
   enabled, this field must be configured to a non-zero value. The X550 only writes the header portion
   into the header buffer. The header size is determined by the options enabled in the PSRTYPE
   registers.
When header split is selected, the packet is split only on selected types of packets. A bit exists for each
option in PSRTYPE[n] registers, so several options can be used in conjunction. If one or more bits are
set, the splitting is performed for the corresponding packet type. See Section 8.2.2.8.17 for details on
the possible header types supported. In virtualization mode, a separate PSRTYPE register is provided
per pool up to the number of pools enabled. In non-virtualization mode, only PSRTYPE[0] is used.
Rules regarding header split:
 • Packets that have headers bigger than 1023 bytes are not split.
 • The header of a fragmented IPv6 packet is defined until the Fragment extension header.
 • Header split must not be used in a queue used for a FCoE large receive.
 • An IP in IP packet (such as any combination of IPv4 and IPv6 tunneling) is not split. Not relevant for
   NVGRE and VXLAN packets
 • Packet header cannot span across buffers, therefore, the size of the header buffer must be larger
   than any expected header size. In case of header split mode (SRRCTL.DESCTYPE = 010b), a packet
   with a header larger than the header buffer is not split.
 • If an IPsec header is present in the receive packet, the following rules apply:
        — IPsec packets handled in the X550 always include IPsec header in a split done at IP boundary.
        — IPsec packets handled in software must never do header split.
Table 7-25 lists the behavior of the X550 in the different modes.

Table 7-25. Behavior in Header Split Modes
                                                                                                  Header and Payload
 DESCTYPE              Condition            SPH   HBO1       PKT_LEN2             HDR_LEN2
                                                                                                        DMA3

                                             0     0                                            Header + Payload (+
                                                         Min (packet length,
               1. Header can't be decoded                                            0x0        TimeStamp) (+ Padding) ->
                                                             buffer size)
                                                                                                Packet Buffer

               2. Header <=                  1     0                                            Header -> Header Buffer
                                                         Min (payload length,
               BSIZEHEADER and Payload                                            Header size   Payload (+ TimeStamp) (+
                                                              buffer size)
               >0                                                                               Padding) -> Packet Buffer
Split
               3. Header <=                  1     0
                                                                                                Header (+ TimeStamp) (+
               BSIZEHEADER and Payload                            0               Header size
                                                                                                Padding) -> Header Buffer4
               = 0 (Header only packet)

                                             1     1                                            Header + Payload (+
                                                         Min (packet length,
               4. Header > BSIZEHEADER                                           Header size5   TimeStamp) -> Packet
                                                             buffer size)
                                                                                                Buffer

412                                                                                                             333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-25. Behavior in Header Split Modes [continued]
                                                                                                         Header and Payload
     DESCTYPE            Condition             SPH    HBO1         PKT_LEN2            HDR_LEN2
                                                                                                               DMA3

 Split –         1. Header can't be decoded     0        0                                            Header + Payload (+
 always use      and packet length <=                                  0x0            Packet length   TimeStamp) (+ Padding) ->
 header          BSIZEHEADER                                                                          Header Buffer
 buffer
                 2. Header cannot be            0        0     Min (packet length –                   Header + Payload (+
                 decoded and packet length                     BSIZEHEADER, data      BSIZEHEADER     TimeStamp) -> Header +
                 > BSIZEHEADER                                      buffer size)                      Packet Buffers5

                                                1        0                                            Header -> Header Buffer
                 3. Header <=                                  Min (payload length,
                                                                                       Header Size    Payload (+ TimeStamp) (+
                 BSIZEHEADER                                     data buffer size)
                                                                                                      Padding) -> Packet Buffer

                                                1        1     Min (packet length –                   Header + Payload (+
                 4. Header > BSIZEHEADER                       BSIZEHEADER, data      Header Size6    TimeStamp) -> Header +
                                                                    buffer size)                      Packet Buffer

1. HBO is set to 1b if the header size is bigger than BSIZEHEADER and zero otherwise.
2. PKT_LEN and HDR_LEN includes optionally added time stamp if TSIP bit is set and does not include padding added by the device.
3. Partial means up to BSIZEHEADER.
4. Even if there is no payload at all and there is a timestamp in the packet - the timestamp is considered as an 8 bytes payload and
   is written to the packet buffer.
5. If the packet spans more than one descriptor, only the header buffer of the first descriptor is used.
6. HDR_LEN does not reflect the actual data size stored in the header buffer. It reflects the header size determined by the parser.

#### 7.1.6.2 Receive Packet Timestamp in Buffer

The X550 supports adding an optional tailored header appended to the end of the packet in the receive
buffer. The tailored header includes a 64-bit timestamp composed of the packet reception time
measured in the SYSTIMEL (Low DW) and SYSTIMEH (High DW) registers (See Section 7.7.3.2 for
further information on SYSTIMEL/H operation). The timestamp starts right at the end of the packet
(after the last byte). It is sent as {SYSTIMEH, SYSTEML} - most significant byte first (closest to
packet).
PKT_LEN and HDR_LEN includes optionally added time stamp.
When the TSAUXC.DISABLE_SYSTIME bit is cleared and the TSYNCRXCTL.TSIP_UP_EN is set for the UP
in the packet (or TSYNCRXCTL.TSIP_UT_EN for un-tagged packets), packets received that meet the
TSYNCRXCTL.TYPE are time-stamped. A packet that was time stamped is reported as follows:
 • Place a 64-bit timestamp, indicating the time a packet was received by the MAC, appended at the
   end of the received packet within the receive buffer.
 • Set the TSIP bit in the RDESC.STATUS field of the last receive descriptor.
Notes:        Even if TSYNCRXCTL.TYPE=100b (timestamp all packets), FCoE DDP packets do not have a
              timestamp.
              When packets are coalesced, the timestamp reflects the reception time of the last coalesced
              fragment, unless the packet is a pure ACK packet, in which case, the timestamp is of the first
              packet.

333369-009                                                                                                                      413
                                       Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Inline Functions

#### 7.1.6.3 Receive Checksum Offloading

The X550 supports the offloading of three receive checksum calculations: the fragment checksum, the
IPv4 header checksum, and the TCP/UDP checksum.
For supported packet/frame types, the entire checksum calculation can be offloaded to the X550. The
X550 calculates the IPv4 checksum and indicates a pass/fail indication to software via the IPv4
Checksum Error bit (RDESC.IPE) in the ERROR field of the receive descriptor. Similarly, the X550
calculates the TCP or UDP checksum and indicates a pass/fail condition to software via the TCP/UDP
Checksum Error bit (RDESC.TCPE). For NVGRE or VXLAN packets, the IPE and TCPE bits relates to the
inner IP/TCP header. The outer IPv4 checksum is also checked and a pass/fail indication is indicated to
software via the Outer IPv4 Checksum Error bit (OUTERIPER). These error bits are valid when the
respective status bits indicate the checksum was calculated for the packet (RDESC.IPCS, RDESC.L4CS,
and RDESC.OUTERIPCS respectively).
Similarly, if RFCTL.IPV6_DIS and RFCTL.IP6XSUM_DIS are cleared to zero, the X550 calculates the TCP
or UDP checksum for IPv6 packets. It then indicates a pass/fail condition in the TCP/UDP Checksum
Error bit (RDESC.TCPE).
Note:      Only Ethernet II frames are supported (no checksum support for SNAP packets).

Table 7-26. Supported Receive Checksum Capabilities
                                                          Hardware IP Checksum            Hardware TCP/UDP Checksum
                    Packet Type
                                                               Calculation                        Calculation

IP header’s protocol field contains a protocol # other
                                                                    Yes                                 No
than TCP or UDP.

IPv4 + TCP/UDP packets.                                             Yes                                 Yes

IPv6 + TCP/UDP packets.                                           No (N/A)                              Yes

IPv4 packet has IP options (IP header is longer than
                                                                    Yes                                 Yes
20 bytes).

IPv6 packet with next header options:
 • Hop-by-hop options.                                            No (N/A)                              Yes
 • Destinations options (without home address).                   No (N/A)                              Yes
 • Destinations options (with home address).                      No (N/A)                              No
 • Routing (with segment left 0).                                 No (N/A)                              Yes
 • Routing (with segment left > 0).                               No (N/A)                              No
 • Fragment.                                                      No (N/A)                              No

Packet has TCP or UDP options.                                      Yes                                 Yes

IPv4 tunnels:
 • IPv4 packet in an IPv4 tunnel.                           Yes (outer IPv4 only)                       No
 • IPv6 packet in an IPv4 tunnel.                                Yes (IPv4)                             No

IPv6 tunnels:
 • IPv4 packet in an IPv6 tunnel.                                    No                                 No
 • IPv6 packet in an IPv6 tunnel.                                 No (N/A)                              No

Packet is an IPv4 fragment.                                         Yes                         UDP checksum assist

Packet is greater than 1522 bytes.                                  Yes                                 Yes

Packet has 802.3ac tag.                                             Yes                                 Yes

414                                                                                                            333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-26. Supported Receive Checksum Capabilities [continued]
                                                                   Hardware IP Checksum               Hardware TCP/UDP Checksum
                       Packet Type
                                                                        Calculation                           Calculation

 NVGRE:
  • Inner IPv4 packet                                                Yes (Inner and outer)                              Yes
  • Inner IPv6 packet                                                     Yes (outer)                                   Yes

 VXLAN:
  • Inner IPv4 packet                                                Yes (Inner and outer)                    Yes (inner only)1
  • Inner IPv6 packet                                                     Yes (outer)                         Yes (inner only)

1. The outer UDP header of VXLAN packets do not use a checksum.

#### 7.1.6.4 SCTP Receive Offload

If a receive packet is identified as SCTP, the X550 checks the CRC32 checksum of this packet and
identifies this packet as SCTP. Software is notified of the CRC check via the L4I and L4E bits in the
Extended Status field and Extended Error field in the Rx descriptor. The detection of an SCTP packet is
indicated via the SCTP bit in the Packet Type field of the Rx descriptor. SCTP CRC uses the CRC32c
polynomial as follows (0x11EDC6F41):
     X32+X28+X27+X26+X25+X23+X22+X20+X19+X18+X14+X13+X11+X10+X9+X8+X6+X0

The checker assumes the following SCTP packet format.

Table 7-27. SCTP Header
                                            1   1   1    1   1     1   1   1    1   1   2    2    2   2   2   2     2    2    2    2   3   3
 0   1    2    3   4   5   6   7   8   9    0   1   2    3   4     5   6   7    8   9   0    1    2   3   4   5     6    7    8    9   0   1

                           Source Port                                                           Destination Port

                                                             Verification Tag

                                                        CRC Checksum (CRC32c)

                                                                 Chunks 1..n

#### 7.1.6.5 Receive UDP Fragmentation Checksum

The X550 might provide a receive fragmented UDP checksum offload for IPv4 non-tunneled packets.
The RXCSUM.PCSD bit should be cleared and the RXCSUM.IPPCSE bit should be set to enable this
mode.
The following table lists the outcome descriptor fields for the following incoming packets types.

         Incoming Packet Type                    Fragment Checksum                           UDPV                       UDPCS / L4CS

 Non-IP packet                                               0                                   0                             0

 IPv6 packet                                                                                                      Depends on transport
                                                             0                                   0                UDP: 1 / 1
 Non fragmented IPv4 packet
                                                                                                                  TCP: 0 / 1

 Fragmented IPv4 with protocol =           The unadjusted 1’s complement            1 if the UDP header
 UDP, first fragment (UDP protocol         checksum of the IP payload if            checksum is valid (not
 present)                                  Checksum in packet header is             0)                                        0/0
                                           different than zero and zero
                                           otherwise.

 Fragmented IPv4, when not first           The unadjusted 1’s complement
                                                                                                 1                            0/0
 fragment                                  checksum of the IP payload

333369-009                                                                                                                                 415
                                         Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                       Inline Functions

      Incoming Packet Type                  Fragment Checksum                   UDPV               UDPCS / L4CS

Fragmented IPv4 with protocol =      The unadjusted 1’s complement      1 if the UDP header
UDP, first fragment (UDP protocol    checksum of the inner IP payload   checksum is valid (not
                                                                                                        1/0
present) within a VXLAN or NVGRE                                        0)
packet.

Fragmented IPv4 when not first       The unadjusted 1’s complement
fragment within a VXLAN or NVGRE     checksum of the inner IP payload              0                    1/0
packet.

Note:      When the driver computes the 16-bit ones complement sum on the incoming packets of the
           UDP fragments, it should expect a value of 0xFFFF.

### 7.1.7 Receive Statistics

#### 7.1.7.1 General Rules

 • All Statistics registers are cleared on read. In addition, they stick at 0xFF...F when the maximum
   value is reached.
 • For the receive statistics it should be noted that a packet is indicated as received if it passes the
   device filters and is placed into the packet buffer memory. A packet does not have to be DMA'ed to
   host memory to be counted as received.
 • Due to divergent paths between interrupt-generation and logging of relevant statistics counts, it
   might be possible to generate an interrupt to the system for a noteworthy event prior to the
   associated statistics count actually being increased. This is extremely unlikely due to expected
   delays associated with the system interrupt-collection and ISR delay, but might be an explanation
   for interrupt statistics values that do not quite make sense. Hardware guarantees that any event
   noteworthy of inclusion in a statistics count is reflected in the appropriate count within 1 s; a small
   time-delay prior to reading the statistics might be required to avoid a potential mismatch between
   and interrupt and its cause.
 • If RSC is enabled, statistics are collected before RSC is applied to the packets.
 • All byte (octet) counters composed of 2 registers can be fetched by two consecutive 32-bit accesses
   while reading the Low 32-bit register first or a single 64-bit access.
 • All receive statistic counters count the packets and bytes before coalescing by the RSC logic or FCoE
   DDP logic.
 • All receive statistic counters in the Filter unit (listed below) might count packets that might be
   dropped by the packet buffer or receive DMA. Same comment is valid for the byte counters
   associated with these packet counters: PRC64, PRC127, PRC255, PRC511, PRC1023, PRC1522,
   BPRC, MPRC, GPRC, RXNFGPC, RUC, ROC.

416                                                                                                        333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.1.7.2 Receive Statistics Hierarchy

The following diagram describes the relations between the packet flow and the different statistic
counters.

                                                 Total Packet Received
                                                          TPR

                                                                                   Error packets
                                                         Errors                     ILLERRC
                                                                                    CRCERRS

                                                       L2 filtering

                                                                                  Flow control packets
                                                 Flow control detection                XONRXC
                                                                                      XOFFRXC

                                                                                     Missed packet
                                                    Packet buffer full
                                                                                         MPC

                            BMC 2 OS             Good packets received
                                                        GPRC

                                                                               Manageability only packets
                                                 Manageability filtering
                         BMC 2 OS traffic                                            MNGPRC
                           B2OSPC

                                                     VMDQ switch
                                                                           Packets dropped by Switch
                                                   Pool/Storm control

                                                        Queues                      Drop of queues

                                            Packet Received by host from BMC
                                                       B2OGPRC

Figure 7-14. Receive Flow Statistics

333369-009                                                                                                  417
                                   Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                               Inline Functions
