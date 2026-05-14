## 7.2 Transmit Functionality

### 7.2.1 Packet Transmission

Transmit packets are made up of data buffers in host memory that are indicated to hardware by pointer
and length pairs. These pointer and length pairs are named as transmit descriptors that are stored in
host memory as well.
Software prepares memory structures for transmission by assembling a list of descriptors. It then
indicates this list to hardware for updating the on-chip transmit tail pointer. Hardware transmits the
packet only after it has completely fetched all packet data from host memory and deposited it into the
on-chip transmit FIFO. This store and forward scheme enables hardware-based offloads such as TCP or
UDP checksum computation, and many other ones detailed in this document while avoiding any
potential PCIe under-runs.

#### 7.2.1.1 Transmit Storage in System Memory

A packet (or multiple packets in transmit segmentation) can be composed of one or multiple buffers.
Each buffer is indicated by a descriptor. Descriptors of a single packet are consecutive, while the first
one points to the first buffer and the last one points to the last buffer (see Figure 7-15). The following
rules must be kept:
 • Address alignment of the data buffers can be on any byte boundary.
 • Data buffers of any transmitted packet must include at least the 12 bytes of the source and
   destination Ethernet MAC Addresses as well as the 2 bytes of the Type/Len field.
 • A packet (or multiple packets in transmit segmentation) can span any number of buffers (and their
   descriptors) up to a limit of 40 minus WTHRESH minus 2 (see Section 7.2.3.3 for Tx Ring details
   and Section 7.2.3.5.1 for WTHRESH details). For best performance it is recommended to minimize
   the number of buffers as possible.

                                                          T x D a ta in h os t m em o ry

                                                                              ...
                                        T x B u ffe r 1    T x B u ffe r 2                     T x B u ffe r N
             T x D e sc rip to r 1
             T x D e sc rip to r 2
                     ...
            T x D e s crip to r N

Figure 7-15. Tx Packet in Host Memory

418                                                                                                                333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.2.1.2 Transmit Path in the X550

The transmit path in the X550 consists of the following stages:
 • Descriptor plane
     — The X550 maintains a set of 128 on-die descriptor queues. Each queue is associated with a
       single descriptor ring in system memory. See Section 7.2.3.3 for more details on the Tx
       descriptor rings. Each on-die descriptor queue contains up to 40 descriptors to achieve the
       desired performance.
     — A fetch mechanism loads Tx descriptors from the descriptor rings in system memory to the
       respective descriptor queues in the X550. A descriptor fetch arbiter determines the order in
       which descriptors are fetched into the various on-die descriptor queues. See Section 7.2.3.4 for
       more details on the fetch mechanism.
     — An arbitration scheme determines the order in which descriptors are processed and requests
       are generated for data reads. These requests load packet data from system memory into a set
       of Tx packet buffers. The arbitration mechanism varies with configuration and is described in
       Section 7.8.
     — Once a packet has been fetched into a packet buffer, status is (optionally) written back into
       system memory. See Section 7.2.3.5 for more details.
 • Packet plane (data plane)
     — Packet data is stored in up to eight packet buffers. The number and size of packet buffers vary
       with the mode of operation and is described in Section 7.2.1.2.2.
     — If more than a single packet buffer is enabled, an arbitration scheme determines the order in
       which packets are taken out of the packet buffers and sent to the MAC for transmission.The
       arbitration mechanism is described in Section 7.8.

7.2.1.2.1              Tx Queues Assignment

The X550 supports a total of 128 queues per LAN port. Each Tx queue is associated with a packet buffer
and the association varies with the operational mode. The following mechanisms impact the association
of the Tx queues. These are described briefly in this section, and in full details in separate sections:
 • Virtualization (VT) — In a virtualized environment, DMA resources are shared between more
   than one software entity (operating system and/or device driver). This is done through allocation of
   transmit descriptor queues to virtual partitions (VMM, IOVM, VMs, or VFs). Allocation of queues to
   virtual partitions is done in sets of queues of the same size, called queue pools, or pools. A pool is
   associated with a single virtual partition. Different queues in a pool can be associated with different
   packet buffers. For example, in a DCB system, each of the queues in a pool might belong to a
   different TC and therefore to a different packet buffer. The PFVFTE register contains a bit per VF.
   When the bit is set to 0b, packet transmission from the VF is disabled. When set to 1b, packet
   transmission from the VF is enabled.
 • DCB — DCB provides QoS through priority queues, priority flow control, and congestion
   management. Queues are classified into one of several (up to eight) Traffic Classes (TCs). Each TC
   is associated with a single unique packet buffer.
 • Transmit fanout — A single descriptor queue might be enough for a given functionality. For
   example, in a VT system, a single Tx queue can be allocated per VM. However, it is often the case
   that the data rate achieved through a single buffer is limited. This is especially true with 10 GbE,
   and traffic needs to be divided into several Tx queues to reach the desired data rate. Therefore,
   multiple queues might be provided for the same functionality.

333369-009                                                                                             419
                                 Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                                     Inline Functions

Table 7-28 lists the queuing schemes. Scheme selection is done via the MTQC register.

Table 7-28. Tx Queuing Schemes
      VT         DCB                          Queues Allocation                                    Packet Buffers Allocation

                           A single set of 64 queues is assigned to a single packet     A single packet buffer for all traffic
      No          No
                           buffer. Queues 64…127 should not be used.

                           Eight TCs mode – allocation of 32-32-16-16-8-8-8-8           A separate packet buffer is allocated to each TC
                           queues for TC0-TC1-…- TC7, respectively.                     (total of four or eight).
      No         Yes
                           Four TCs mode — allocation of 64-32-16-16 queues for
                           TC0-TC1-…- TC3, respectively.

                           32 pools x 4 queues, or                                      A single packet buffer for all traffic.
      Yes         No
                           64 pools x 2 queues

                           16 pools x 8 TCs, or                                         A separate packet buffer is allocated to each TC
      Yes        Yes                                                                    (total of four or eight).
                           32 pools x 4 TCs

Note:           Software can use any number of queues per each TC or per each pool within the allocated
                ranges previously described by disabling any unused queue.
Note:           Programming MTQC must be done only during the init phase, while software must also set
                RTTDCS.ARBDIS before configuring MTQC and then clear RTTDCS.ARBDIS afterwards.

Table 7-29. Queues, Pools, and TCs programming
                       Device Setting (MTQC)                                               Device Functionality

  DCB_ena                VT_Ena            NUM_TC_OR_Q              Total Number of Tx Queues                       TC & Pools

            0               0                      00                             64                                      -

       <> 0               <> 0                     00                                     Non valid configuration

            0               0                     <> 00                                   Non valid configuration

            1               0                      01                                                N/A

            1               0                      10                             128                               TC0 — TC3

            1               0                      11                             128                               TC0 — TC7

            0               1                      01                             128                                 64 pools

            0               1                      10                             128                                 32 pools

            0               1                      11                                                N/A

            1               1                      01                                                N/A

            1               1                      10                             128                         TC0 — TC3 & 32 pools

            1               1                      11                             128                         TC0 — TC7 & 16 pools

Allocating descriptor queues to VFs uses a consistent indexing over the different Tx queuing schemes.
The most significant bits of the queue index represent the VF index, and the least significant bits are
either the TC index or are used by software to dispatch traffic according to a Transmit Side Scaling
(TSS) algorithm — similar to RSS in the Rx path.
The Tx queue numbers associated with the TCs are listed in the following tables: Table 7-30 and
Table 7-31.

420                                                                                                                               333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-30. Tx Queues Indexing When VT-on
                                                            Allocation of Queue Index Bits According to
             VT Mode
                                         6             5                4              3         2         1               0

# 64 VFs + TSS                                                        VF or pool (63..0)                                     TSS

# 32 VFs + TSS or 4 TCs                                         VF or pool (31..0)                                TSS / TC

# 16 VFs + 8 TCs                                             VF (15..0)                                      TC

Table 7-31. Tx Queues Indexing When VT-off and DCB-on
          TC Mode                             TCn                              # of Qs               Queues Attached to TCn

                                              TC0                                  64                       0xxxxxx

                                              TC1                                  32                       10xxxxx

# 4 TCs

                                              TC2                                  16                       110xxxx

                                              TC3                                  16                       111xxxx

                                              TC0                                  32                       00xxxxx

                                              TC1                                  32                       01xxxxx

                                              TC2                                  16                       100xxxx

                                              TC3                                  16                       101xxxx

# 8 TCs

                                              TC4                                  8                        1100xxx

                                              TC5                                  8                        1101xxx

                                              TC6                                  8                        1110xxx

                                              TC7                                  8                        1111xxx

Note:   “x” refers to both 0 or 1, and is used by software to dispatch Tx flows via TSS algorithm.

7.2.1.2.2                Tx Packet Buffers

As previously described, the following modes exist for the X550 packet buffers:
 • A single 160 KB packet buffer that serves all Tx descriptor queues, leading to one single (or no) TC
   enabled, TC0
 • Four 40 KB packet buffers, one per enabled TC, leading to four TCs, TC0 to TC3
 • Eight 20 KB packet buffers, one per enabled TC, leading to eight TCs, TC0 to TC7
The size of the Tx packet buffer(s) is programmed via the TXPBSIZE registers, one register per TC.
Null-sized packet buffer corresponds to a disabled TC.
Note:        Setting the packet buffers’ size leads to a different partition of a shared internal memory and
             must be done during boot, prior to communicating, and followed by a software reset.

333369-009                                                                                                                       421
                                      Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                  Inline Functions

                                                   LAN Port 0 / 1
                Tx      Tx      Tx        Tx         Tx        Tx        Tx        Tx                      Tx
              queue   queue   queue      queue     queue     queue     queue     queue                    queue
                0       1       2          3         4         5         6         7                       127

                         Transmit descriptor rings (queues). Each queue has a cache of 40 descriptors

                                        The X550 has up to 8 packet buffers

                        The size of all of the packet buffers together is 160 KB.
                        The X550 can have any number of packet buffers less than or equal to 8.
                        The packet buffer size is specified for each packet buffer in the
                        TXPBSIZE registers.

Figure 7-16. Tx Packet Buffers

7.2.1.2.3             Tx Arbitration Schemes

There are basically four Tx arbitration schemes, one per each combination of the DCB and Virtualization
(VT) enabled/disabled modes. They are configured via the MTQC.MTQE register field.

7.2.1.2.3.1           DCB-on/VT-on

When both DCB and virtualization are enabled, queues are allocated to the packet buffers in a fixed
manner, the same number of queues per each TC. Two DCB modes are supported, four TCs or eight TCs
mode, according to coherent configuration made in registers TXPBSIZE and MTQC.

Descriptor Plane Arbiters and Schedulers:
 • Rate-Scheduler — Once a frame has been fetched out from a rate-limited queue, the next time
   another frame could be fetched from that queue is regulated by the rate-scheduler. In the
   meantime, the queue is considered as if it was empty (such as switched-off) for the subsequent
   arbitration layers.
 • VM Weighted Round Robin Arbiter — Descriptors are fetched out from queues attached to the
   same TC in a frame-by-frame weighted round-robin manner, while taking into account any
   limitation as previously described. Weights or credits allocated to each queue are configured via the
   RTTDT1C register. Bandwidth unused by one queue is reallocated to the other queues within the TC,
   proportionally to their relative bandwidth shares. TC bandwidth limitation is distributed across all
   the queues attached to the TC, proportionally to their relative bandwidth shares. Details on

422                                                                                                                   333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

    weighted round-robin arbiter between the queues can be found in Section 7.6.2.3. It is assumed
    traffic is dispatched across the queues attached to a same TC in a straightforward manner,
    according to the VF to which it belongs.
 • TC Weighted Strict Priority Arbiter — Descriptors are fetched out from queues attached to
   different TCs in a frame-by-frame weighted strict-priority manner. Weights or credits allocated to
   each TC are configured via RTTDT2C registers. Bandwidth unused by one TC is reallocated to the
   others, proportionally to their relative bandwidth shares. Link bandwidth limitation is distributed
   across all the TCs, proportionally to their relative bandwidth shares. Details on weighted strict-
   priority arbiter between the TCs can be found at Section 7.6.2.3. It is assumed (each) driver
   dispatches traffic across the TCs according to the 802.1p User Priority field inserted by the
   operating system and according to a user priority-to-TC Tx mapping table.

Packet Plane Arbiters:
 • TC Weighted Strict Priority Arbiter — Packets are fetched out from the different packet buffers
   in a frame-by-frame weighted strict-priority manner. Weights or credits allocated to each TC (such
   as to each packet buffer) are configured via RTTPT2C registers, with the same allocation done at
   the descriptor plane. Bandwidth unused by one TC and link bandwidth limitation is distributed over
   the TCs as in the descriptor plane. Details on weighted strict-priority arbiter between the TCs can be
   found in Section 7.6.2.3.
 • Priority Flow Control packets are inserted with strict priority over any other packets.
 • Manageability packets are inserted with strict priority over data packets from the same TC, with
   respect to the bandwidth allocated to the concerned TC. TCs that belong to manageability packets
   are controlled by MNGTXMAP.MAP.

                                                      Start
                                                                                 Replenish all VMs credits
                                                                                 Saturated to twice T1[VM].Refill
                                                                                 For all the VMs:
                                                                                 T1[VM].Credits :=
                                             VM := first VM in the TC;             Min( (T1[VM].Credits + T1[VM].Refill), 2 x T1[VM].Refill)

             Decrement T1[VM].Credits                             N          All VMs in that TC                 Y
                                                                               are either empty
                                                                             or have no credits?
                          Y

          Next data read request                                                 Cyclic VM ++
          was sent (from this VM)?
                                     N
                                                 VM is empty?
                                                                         Y
                                                              N

              Select VM for next               T1[VM].Credits > 0?
                                                                                                 WRR Arbiters
              data read request         Y                                    N

Figure 7-17. Transmit Architecture DCB-on/VT-on — Eight TCs Mode

Note:        Replicating TC arbiters before and after the packet buffers is required to provide arbitration
             whether PCI bandwidth is smaller or greater than the link bandwidth, respectively.

333369-009                                                                                                                                     423
                                            Did this document help answer your questions?

                                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                                             Inline Functions

7.2.1.2.3.2             DCB-on/VT-off

When DCB is enabled and virtualization disabled, queues are allocated to the packet buffers in a fixed
manner according to the number of TCs. Two DCB modes are supported, four TCs or eight TCs mode,
according to coherent configuration made in registers TXPBSIZE and MTQC. In Figure 7-18, eight TCs
mode is shown.
 • The unique difference with the DCB-on/VT-on arbitration scheme previously described is that the
   VM weighted round-robin arbiters are degenerated into simple frame-by-frame round-robin arbiters
   across the queues attached to the same TC. It is assumed driver dispatches traffic across the
   queues attached to a same TC according to hashing performed on MAC destination addresses. This
   is aimed to minimize crosstalk between rate-limited and non-rate-limited flows.

                                                                  Descriptor
                                                                 Fetch Arbiter

                                          D    D             D                       D     D            D    Descriptor
                                          Q
                                          0
                                               Q
                                               1
                                                     … 31Q            …              Q
                                                                                    120
                                                                                           Q
                                                                                           121
                                                                                                 … 127Q       Queues

                    Rate‐Limiter

                      VM Arbiters,                                    …                   Round‐Robin       Data read
                                              Round‐Robin
                       one per TC                                                                            request      Data

                    Descriptor Plane                                Weighted
                       TC Arbiter                                 Strict Priority

                                                    PB                                           PB            Packet
                                                                                                  7

# 0 Buffers

                      Packet Plane        T raffi c C l as s 0      Weighted         T raffi c C l as s 7
                       TC Arbiter                                 Strict Priority

                                                                                     Flow Control per TC
                                                                      MAC           Manageability packets

Figure 7-18. Transmit Architecture DCB-on/VT-off — Eight TCs Mode

7.2.1.2.3.3             DCB-off/VT-on

When DCB is disabled and virtualization enabled, all the 128 queues are allocated to a single packet
buffer PB(0). Queues are grouped into 32 or 64 pools of 4 or 2 queues, respectively. The number of
queue pools corresponds to the number of VFs exposed. Queues are attached to pools according to
consecutive indexes
      — For the 32 pools case, queues 0, 1, 2, 3 are attached to VF0, queues 4, 5, 6, 7 are attached to
        VF1, and so forth up to VF31.
      — For the 64 pools case, queues 0 and 1 are attached to VF0, queues 2 and 3 are attached to VF1,
        and so forth up to VF63.

424                                                                                                                              333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Descriptor Plane Arbiters:
 • Descriptor Queues Round Robin Arbiter — Descriptors are fetched out from the internal
   descriptor queues attached to the same pool in a frame-by-frame round-robin manner. It is
   assumed driver dispatches traffic across the queues of a same pool according to some Transmit
   Side Scaling (TSS) algorithm similarly to what is done by hardware in the Rx path with RSS.
 • VM Weighted Round Robin Arbiter — Descriptors are fetched out from queues attached to
   different pools in a frame-by-frame weighted round-robin manner. Weights or credits allocated to a
   pool are those allocated for the lowest queue of the pool via the RTTDT1C register. Bandwidth
   unused by one pool is reallocated to the others proportionally to their relative bandwidth shares.
   Link bandwidth limitation is distributed across all the pools, proportionally to their relative
   bandwidth shares. Details on weighted round-robin arbiter between the pools can be found in
   Section 7.6.2.3.

Packet Plane Arbiter:
 • Manageability packets are inserted with strict priority over data packets.

                                                        Descriptor
                                                       Fetch Arbiter

                D     D           D      D     D           D                        D      D            D    Descriptor
                Q
                0
                      Q
                      1
                          …       Q
                                  3
                                         Q
                                         4
                                               Q
                                               5
                                                   …       Q
                                                           7         …              Q
                                                                                   124
                                                                                           Q
                                                                                          125
                                                                                                 … 127
                                                                                                    Q
                                                                                                              Queues

                     Pool 0                   Pool 1                                     Pool 31
                                                                     …                                      Queues Arbiters,
                    Round-Robin              Round-Robin                               Round-Robin
                                                                                                              one per VF
                                                                                                Data read
                                                        Weighted                                 request          Data
               VM Arbiter                              Round-Robin

                                                               PB        Packet

# 0 Buffer

                                                       Strict Priority

                                                                            Manageability packets
                                                           MAC
Figure 7-19. Transmit Architecture DCB-off/VT-on — 32 VFs

333369-009                                                                                                                     425
                                      Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

7.2.1.2.3.4           DCB-off/VT-off

When both DCB and virtualization features are disabled, a single set of up to 64 queues is allocated to a
single packet buffer PB(0).

Descriptor Plane Arbiter:
 • Descriptor Queues Round Robin Arbiter — Descriptors are fetched out from the internal
   descriptor queues in a frame-by-frame round-robin manner. It is assumed driver dispatches traffic
   across the queues according to some TSS algorithm similarly to what is done by hardware in the Rx
   path with RSS.

Packet Plane Arbiter:
 • Manageability packets are inserted with strict priority over data packets.

                                            Descriptor
                                           Fetch Arbiter

                                       D     D             D   Descriptor
                                       Q
                                       0
                                             Q
                                             1
                                                  … 63Q         Queues

                                                                                 Data read
                                                                                  request         Data
                      Queues Arbiter       Round-Robin

                                                 PB          Packet

# 0 Buffer

                                           Strict Priority

                                                                Manageability packets
                                              MAC
Figure 7-20. Transmit Architecture DCB-off/VT-off

426                                                                                                               333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.2.2 Transmit Contexts

The X550 provides hardware checksum offload and TCP segmentation facilities. These features enable
TCP and UDP packet types to be handled more efficiently by performing additional work in hardware,
thus reducing the software overhead associated with preparing these packets for transmission. Part of
the parameters used to control these features are handled through contexts.
A context refers to a set of parameters providing a particular offload functionality. These parameters
are loaded by unique descriptors named transmit context descriptors. A transmit context descriptor is
identified by the DTYP field (described later in this section) equals to 0x2.
The X550 supports two contexts for each of its 128 transmit queues. The IDX bit contains an index to
one of these two contexts. Each advanced data descriptor that uses any of the advanced offloading
features must refer to a context by the IDX field.
Contexts can be initialized with a transmit context descriptor and then used for a series of related
transmit data descriptors. Software can use these contexts as long lived ones, while one of the two
contexts is used for checksum offload and the other one for transmit segmentation detailed in the
following sections. The contexts should be modified when new offload parameters are required.

### 7.2.3 Transmit Descriptors

#### 7.2.3.1 Introduction

The X550 supports legacy descriptors and advanced descriptors.
Legacy descriptors are intended to support legacy drivers, to enable fast platform power up and to
facilitate debug. The legacy descriptors are recognized as such based on DEXT bit (see the sections that
follow). Legacy descriptors are not supported together with DCB, virtualization, and IPsec. These
modes are recognized by a dedicated enable bit for each.
In addition, the X550 supports two types of advanced transmit descriptors:
1. Advanced transmit context descriptor, DTYP = 0010b
2. Advanced transmit data descriptor, DTYP = 0011b
Note:        DTYP = 0000b and 0001b are reserved values.
The transmit data descriptor (both legacy and advanced) points to a block of packet data to be
transmitted. The advanced transmit context descriptor does not point to packet data. It contains
control/context information that is loaded into on-chip registers that affect the processing of packets for
transmission. The following sections describe the descriptor formats.

#### 7.2.3.2 Transmit Descriptors Formats

7.2.3.2.1              Notations

This section defines the structure of descriptors that contain fields carried over the network. At the
moment, the only relevant field is the VLAN Tag field.
The rule for VLAN tag is to use network ordering (also called big endian). It appears in the following
manner in the descriptor:

333369-009                                                                                               427
                                 Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                                      Inline Functions

Table 7-32. VLAN Tag
          Byte address N + 1 -> first byte on the wire                          Byte address N -> second byte on the wire
Bit 7                                first on the wire <- Bit 0         Bit 7 -> last on the wire                               Bit 0

        PRI (3 bits)          DEI              VID (4 bits)                                          VID (8 bits)

7.2.3.2.2                     Legacy Transmit Descriptor Format

To select legacy mode operation, bit 29 (TDESC.DEXT) should be set to 0b. In this case, the descriptor
format is defined as listed in Table 7-33. Address and length must be supplied by software on all
descriptors. Bits in the command byte are optional, as are the CSO, and CSS fields.

Table 7-33. Transmit Descriptor (TDESC) Layout — Legacy Mode
           63                       48    47         40   39     36   35   32   31         24   23         16   15                 0

# 0 Buffer Address [63:0]

    8 VLAN                    CSS            Rsvd      STA          CMD             CSO              Length

Table 7-34. Transmit Descriptor Write-Back Format — Legacy Mode
           63                       48    47         40   39     36   35   32   31         24   23         16   15                 0

# 0 Reserved                                                          Reserved

    8 VLAN                    CSS            Rsvd      STA          CMD             CSO              Length

Buffer Address (64) and Length (16)
      The buffer address is a byte-aligned address. Length (TDESC.LENGTH) specifies the length in bytes
      to be fetched from the buffer address provided. The maximum length associated with a single
      descriptor is 15.5 KB while the total frame size must meet the maximum supported frame size.
      There is no limitation for the minimum buffer size.
      Note:        Descriptors with zero length (null descriptors) transfer no data. Null descriptors might
                   appear only between packets and must have their EOP bits set.
Checksum Offset and Start — CSO (8) and CSS (8)
      A Checksum Offset (TDESC.CSO) field indicates where, relative to the start of the packet, to insert
      a TCP checksum if this mode is enabled. A Checksum Start (TDESC.CSS) field indicates where to
      begin computing the checksum. Note that CSO and CSS are meaningful only in the first descriptor
      of a packet.
      Both CSO and CSS are in units of bytes. These must both be in the range of data provided to the
      device in the descriptor. This means for short packets that are padded by software, CSO and CSS
      must be in the range of the un-padded data length, not the eventual padded length (64 bytes).
      CSO must be set to the location of TCP or UDP checksum in the packet. CSS must be set to the
      beginning of the IP header or the L4 (TCP/UDP) header. Checksum calculation is not done if CSO or
      CSS are out of range. This occurs if (CSS > length) OR (CSO > length - 1).
      For the 802.1Q header, the offset values depend on the VLAN insertion enable bit — the VLE bit. If
      they are not set (VLAN tagging included in the packet buffers), the offset values should include the
      VLAN tagging. If these bits are set (VLAN tagging is taken from the packet descriptor), the offset
      values should exclude the VLAN tagging.

428                                                                                                                       333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

    Hardware does not add the 802.1q EtherType or the VLAN field following the 802.1Q EtherType to
    the checksum. So for VLAN packets, software can compute the values to back out only on the
    encapsulated packet rather than on the added fields.
    Note:         UDP checksum calculation is not supported by the legacy descriptor because the legacy
                  descriptor does not support the translation of a checksum result of 0x0000 to 0xFFFF
                  needed to differentiate between an UDP packet with a checksum of zero and an UDP
                  packet without checksum.
        Because the CSO field is eight bits wide, it puts a limit on the location of the checksum to 255
        bytes from the beginning of the packet.
    Note:         CSO must be larger than CSS.
    Software must compute an offsetting entry to back out the bytes of the header that should not be
    included in the TCP checksum and store it in the position where the hardware computed checksum
    is to be inserted.
    Hardware adds the checksum at the byte offset indicated by the CSO field. Checksum calculations
    are for the entire packet starting at the byte indicated by the CSS field. The byte offset is counted
    from the first byte of the packet fetched from host memory.
Command Byte — CMD (8)
    The CMD byte stores the applicable command and has the fields listed in Table 7-35.

    Table 7-35. Transmit Command (TDESC.CMD) Layout
             7                 6              5              4               3              2               1              0

         RSV                  VLE           DEXT            RSV             RS              IC            IFCS            EOP

    RSV (bit 7)
        Reserved.
    VLE (bit 6) - VLAN Packet Enable
        When set to 1b, VLE indicates that the packet is a VLAN packet and hardware adds the VLAN
        header to the Tx packet. The VLAN EtherType is taken from DMATXCTL.VT and the 802.1q VLAN
        tag is taken from the VLAN field in the Tx descriptor. See Section 7.4.5 for details about double
        VLAN.

        Table 7-36. VLAN Tag Insertion Decision Table for VLAN Mode Enabled
                 VLE                                                        Action

# 0 Send generic Ethernet packet.

# 1 Send 802.1Q packet; the Ethernet Type field comes from the VET field of the VLNCTRL register and the

                            VLAN data comes from the VLAN field of the Tx descriptor.

         Note:         This table is relevant only if PFVMVIR.VLANA = 00b (use descriptor command) for the queue.

    DEXT (bit 5) - Descriptor Extension
        Zero for legacy mode.
    RSV (bit 4)
        Reserved.

333369-009                                                                                                                         429
                                         Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                    Inline Functions

      RS (bit 3) - Report Status
          RS signals hardware to report the DMA completion status indication as well as triggering ITR.
          Hardware indicates a DMA completion by setting the DD bit in the transmit descriptor when
          TDWBAL[n].HEAD_WB_EN = 0b or by Head Write-back if HEAD_WB_EN = 1b (see
          Section 7.2.3.5.2). The RS bit is permitted only on descriptors that has the EOP bit set (last
          descriptor of a packet).
          Note:     Software should not set the RS bit when TXDCTL.WTHRESH is greater than zero.
                    Instead, the hardware reports the DMA completion according to the WTHRESH rules
                    (explained in Section 7.2.3.5.1). This note is relevant only for descriptor write back
                    while in head write-back mode. WTRESH must also be set to zero.
                    When TXDCTL.WTHRESH = zero, software must set the RS bit on the last descriptor
                    of every packet.
                    There are some exceptions for descriptor completion indication in head write-back
                    mode. For more details see Section 7.2.3.5.2.
      IC (bit 2) - Insert Checksum
          Hardware inserts a checksum at the offset indicated by the CSO field if the Insert Checksum bit
          (IC) is set.
      IFCS (bit 1) - Insert FCS
          When set, hardware appends the MAC FCS at the end of the packet. When cleared, software
          should calculate the FCS for proper CRC check. There are several cases in which software must
          set IFCS as follows:
           • Transmitting a short packet while padding is enabled by the HLREG0.TXPADEN bit.
           • Checksum offload is enabled by the IC bit in the TDESC.CMD.
           • VLAN header insertion enabled by the VLE bit in the TDESC.CMD or by the PFVMVIR.VLANA
             fields.
           • E-tag insertion enabled by the PFVMVIR.TAGA fields.
           • TSO or TCP/IP checksum offload using a context descriptor.
           • IPsec offload is requested.
          Note:     TSO and IPsec offload are relevant only to advanced Tx descriptors.
      EOP (bit 0) - End of Packet
          A packet can be composed of multiple buffers (each of them indicated by its own descriptor).
          When EOP is set, it indicates the last descriptor making up the packet.
          Note:     VLE, IFCS, and IC fields should be set in the first descriptor of a packet. The RS bit
                    can be set only on the last descriptor of a packet. The DEXT bit must be set to zero
                    for all descriptors. The EOF bit is meaningful in all descriptors.
STA (4) — Transmitted Status
DD (bit 0) — Descriptor Done Status
      This bit provides a status indication that the DMA of the buffer has completed. Software might re-
      use descriptors with the DD bit set and any other descriptors processed by the hardware before this
      one. The other bits in the STA field are reserved.

430                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Rsvd — Reserved (4)
VLAN (16)
    The VLAN field is used to provide the 802.1q/802.1ac tagging information. The VLAN field is
    qualified on the first descriptor of each packet when the VLE bit is set to 1b. The VLAN field is
    provided in network order and is meaningful in the first descriptor of a packet. See
    Section 7.2.3.2.1 for more details.

    Table 7-37. VLAN Field (TDESC.VLAN) Layout
     15                    13    12         11                                                                                          0

                PRI              DEI                                                       VLAN

7.2.3.2.3                  Advanced Transmit Context Descriptor

          63
                      55        48     47        42    41            32     31                        16    15        9   8              0
               56

                                                                                                                               IPLEN/

    0 TUNNELLEN         OUTERIPLEN        FCoEF           IPsec SA Index                     VLAN              MACLEN

                                                                                                                              HEADLEN

                                                                                 D
                                                                 I
                                                            RS                   E

    8 MSS                     L4LEN                D Reserved          RSV      DTYP         TUCMD          IPsec ESP_LEN

                                                            V                    X
                                                                 X must be
                                                                     0x3F        T

                                                            39   3               2   28       23 2
    63                          48     47             40           35     30                         19               9   8              0
                                                            37   6               9    24       0

IPLEN/HEADLEN (9)
    IPLEN (for IP packets)
          This field holds the value of the IP header length for the IP checksum offload feature. If an
          offload is requested, IPLEN must be greater than or equal to 20, and less than or equal to 511.
          For IP tunnel packets (IPv4-IPv6) IPLEN must be defined as the length of the two IP headers.
          The hardware is able to offload the L4 checksum calculation while software should provide the
          IPv4 checksum. For IPsec packets, it is the sum of IP header length plus IPsec header length.
    HEADLEN (for FCoE packets)
          This field indicates the size (in bytes) of the FCoE frame header. The frame header includes the
          MAC header, optional VLAN and FCoE header(s) as shown in Figure 7-46. HEADLEN is
          meaningful only if transmit FCoE offload is enabled by setting the FCoE bit in the TUCMD field.
          HEADLEN that matches Figure 7-46 equals 56 for packets without FC extended headers.
MACLEN (7)
    For non-FCoE packets: This field indicates the length of the MAC header. When an offload is
    requested, one of the TSE bits (in the advanced transmit data descriptor) or IXSM bit or TXSM bit
    are set, MACLEN must be larger than or equal to 14, and less than or equal to 127. This field should
    include only the part of the L2 header supplied by the driver and not the parts added by hardware.
    The following table lists the value of MACLEN in the different cases.

                     Regular VLAN                                  Extended tag                                  MACLEN

                By hardware or none                                      None                                      14

                By hardware or none                                      VLAN                                      18

333369-009                                                                                                                              431
                                            Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                     Inline Functions

                Regular VLAN                          Extended tag                           MACLEN

              By hardware or none                         E-tag                                 22

                    By software                           None                                  18

                    By software                           VLAN                                  22

                    By software                           E-tag                                 26

      For FCoE packets: This field is a byte offset to the last DWord of the FCoE header (supplied by the
      driver) that includes the SOF flag. The FC frame header starts four bytes after the MACLEN as
      shown in Figure 7-46. The MACLEN that matches Figure 7-46 equals 28.
VLAN (16)
      This field contains the 802.1Q VLAN tag to be inserted in the packet during transmission. This VLAN
      tag is inserted when a packet using this context has its DCMD.VLE bit is set. This field should
      include the entire 16-bit VLAN field including DEI and priority fields as listed in Table 7-37.
      Note:     The VLAN field is provided in network order. See Section 7.2.3.2.1.
IPsec SA IDX (10)
      If an IPsec offload is requested for the packet (IPSEC bit is set in the advanced Tx data descriptor),
      indicates the index in the SA table where the IPsec KEY and SALT are stored for that flow.
FCoEF (6)
      EOF (bits 1:0)
          End of frame delimiter index (see Section 7.11.2.4 for details).
      ORIE (bit 4)
          Orientation relative to the last frame in an FC sequence (see Section 7.11.2.4 for details).
      SOF (bit 2)
          Start of frame delimiter index (see Section 7.11.2.3 for details).
      ORIS (bit 5)
          Orientation relative to the first frame in an FC sequence (see Section 7.11.2.3 for details).
      PARINC (bit 3)
          When this bit is set, hardware relates to the PARAM field in the FC header as relative offset. In
          this case, hardware increments the PARAM field in TSO by an MSS value on each transmitted
          packet of the TSO. Software should set the PARINC bit when it sets the Relative Offset Present
          bit in the F_CTL.
OUTERIPLEN (8)
      This field holds the value of the outer IP header length.
TUNNELLEN (8)
      This field holds the length value of the tunnel headers including the inner L2 header.
IPS_ESP_LEN(9)
      Size of the ESP trailer and ESP ICV appended by software. Meaningful only if the IPSEC_TYPE bit is
      set in the TUCMD field and to single send packets for which the IPSEC bit is set in their advanced Tx
      data descriptor.

432                                                                                                      333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

TUCMD (11)
    RSV (bit 10-7)
          Reserved.
    FCoE (bit 6)
          This bit defines the context descriptor and the associated data descriptors as FCoE frame type.
          See Section 7.11.2 for a description of the offload provided by the hardware while transmitting
          a single frame and TSO.
    Reserved (bit 5:4)
          Reserved.
    L4T (bit 3:2)
          L4 Packet TYPE (00: UDP; 01: TCP; 10: SCTP; 11: RSV). Should be set to 11b for FCoE packets.
    IPV4(bit 1)
          IP Packet Type: When 1b, IPv4; when 0b, IPv6.
DTYP (4)
    This field is always 0010b for this type of descriptor.
RSV(1)
    Reserved.
DEXT (1)
    Descriptor Extension (one for advanced mode).
Reserved (6)
    Reserved.
IDX (1)
    The context descriptor is posted to a context table in hardware. There are two context tables per
    queue. The IDX is the index of the context tables.
    Note:       Because the X550 supports only two context descriptors per queue, the two MS bits are
                reserved and should be set to 0b.
RSV(1)
    Reserved.
L4LEN(8)
    This field holds the layer 4 header length. If TSE is set, this field must be greater than or equal to 8
    and less than or equal to 64. Otherwise, this field is ignored. Note that for UDP segmentation the L4
    header size equals 8 and for TCP segmentation (with no TCP options) it equals 20.
MSS (16)
    This field controls the Maximum Segment Size. This specifies the maximum protocol payload
    segment sent per frame, not including any header. MSS is ignored when DCMD.TSE is not set.

333369-009                                                                                               433
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                   Inline Functions

7.2.3.2.3.1              TCP/UDP Segmentation

The total length of each frame (or segment) excluding Ethernet CRC as follows. Note that the last
packet of a TCP segmentation might be shorter.
      MACLEN + 4(if VLE set) + [4, 8, 14, or 16] + OUTERIPLEN + TUNNELLEN + IPLEN + L4LEN + MSS + [PADLEN
      + 18] (if ESP packet)

PADLEN ranges from zero to three in Tx and is the content of the ESP Padding Length field that is
computed when offloading ESP in cipher blocks of 16 bytes (AES-128) with respect to the following
alignment formula:
      [L4LEN + MSS + PADLEN + 2] modulo(4) = 0

For a single send the IPS_ESP_LEN equals to PADLEN + 18.
Note:       The headers lengths must meet the following: MACLEN + IPLEN + L4LEN <= 512

7.2.3.2.3.2              FCoE Segmentation

The total length of each frame (or segment) excluding Ethernet CRC is equal to:
      MACLEN + 4(if VLE set) + [4, 8, 14, or 16] + 8 (FC CRC + EOF)

Note:       For FCoE packets, the maximum segment size defines the FC payload size in all packets but
            the last one, which can be smaller.
The context descriptor requires valid data only in the fields used by the specific offload options. Table 7-
38 lists the required valid fields according to the different offload options.

434                                                                                                    333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-38. Valid Fields by Offload Option

                                                                        OUTERIPLEN/TUNNELLEN

                                                                                                                                                                                                                          CC (data descriptor)
                                                                                               IPLEN/HEADLEN

                                                                                                                                                               IPSECTYPE
                                                                                                                                                  Encryption

                                                                                                                                                                                                             QCNTLEN
                                                                                                                                                                                      ESP_LEN
                                                               MACLEN

                                                                                                                                                                            SAIDX
                                                                                                                 L4LEN
                                         FCoEF

                                                      VLAN
                    Context

                                                                                                                                  IPV4
                                  FCoE

                                                                                                                                                                                                  MSS
                                                                                                                                          L4T
                    Fields ->

                      VLAN
                                                      yes                                                                                                                                                    yes
                    insertion

                   IPv4 XSUM      n/a    n/a                   yes                             yes                                    1                                                                      yes                  0

                    L4 XSUM       n/a    n/a                   yes                             yes                                        yes                                                                yes                  0

                    TCP/UDP
                                  n/a    n/a                   yes                             yes               yes              yes     yes                                                     yes        yes                  0
                      Seg

                                                                                                                                           Yes
                    FCoE CRC      yes    yes                   yes                             yes               n/a              n/a             n/a          n/a          n/a       n/a                    yes                  1
Required Offload

                                                                                                                                          (11)

                                                                                                                                           Yes
                    FCoE Seg      yes    yes                   yes                             yes               n/a              n/a             n/a          n/a          n/a       n/a         yes        yes                  1
                                                                                                                                          (11)

                    IPsec ESP     n/a    n/a                   yes                             yes                                yes             yes          yes          yes       yes                    yes                  1

                    IPsec AH      n/a    n/a                   yes                             yes                                yes             yes          yes          yes       yes                    yes                  1

                        Tunnel
                                  n/a    n/a                   yes      yes                    yes                                        yes                                                                                     1
                        XSUM

                   Tunnel Seg     n/a    n/a                   yes      yes                    yes               yes              yes     yes                                                     yes        yes                  1

                    Tx switch     n/a    n/a                   yes                             yes               yes              yes     yes     n/a          n/a          n/a       n/a                    yes                  1

Note:                      All fields that are not used in the context descriptor must be set to zero.

7.2.3.2.4                                Advanced Transmit Data Descriptor

Table 7-39. Advanced Transmit Data Descriptor Read Format
                   63                            46     45         40                 39               38 36             35 32    31      24     23 20           19              18      17             16       15                              0

# 0 Address[63:0]

  8                          PAYLEN                          POPTS                    CC                       IDX        STA         DCMD       DTYP                      MAC                  TUNNEL                 DTALEN

Table 7-40. Advanced Transmit Data Descriptor Write-back Format
                    63                                                                           36              35       32     31                                                                                                              0

    0 RSV

    8 RSV                                                                       STA                                                     RSV

Address (64)
                   This field holds the physical address of a data buffer in host memory, which contains a portion of a
                   transmit packet. This field is meaningful in all descriptors.

333369-009                                                                                                                                                                                                                                       435
                                                              Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                    Inline Functions

DTALEN (16)
      This field holds the length in bytes of data buffer at the address pointed to by this specific
      descriptor. This field is meaningful in all descriptors. The maximum length is 16 KB with no
      limitations on the minimum size. Refer to the comment on descriptors with zero length described in
      the sections that follow.
TUNNEL (2)
      Tunnel Type (bit 0):
          0 = VXLAN
          1 = NVGRE
      OUTERIPCS (bit 1) - Outer IP checksum enable
          Indicates this is a tunnel packet and that the OUTERIPLEN/TUNNELLEN parameters in the
          context descriptor are valid.
MAC (2)
      This field is meaningful on the first descriptor of the packet(s).
      Reserved (bit 0)
          Reserved.
      1588 (bit 1)
          IEEE1588 time stamp packet.
DTYP (4)
      0011b for advanced data descriptor. DTYP should be valid in all descriptors of the packet(s).
DCMD (8)
      TSE (bit 7) - Transmit Segmentation Enable
          This bit indicates a TCP or FCoE segmentation request. When TSE is set in the first descriptor of
          a TCP or FCoE packet, hardware must use the corresponding context descriptor to perform
          segmentation.
          Note:       It is recommended that HLREG0.TXPADEN be enabled when TSE is used since the last
                      frame can be shorter than 60 bytes — resulting in a bad frame.
      VLE (bit 6) - VLAN Packet Enable
          This bit indicates that the packet is a VLAN packet (hardware must add the VLAN EtherType and
          an 802.1q VLAN tag to the packet).
      DEXT (bit 5) - Descriptor Extension
          This bit must be one to indicate advanced descriptor format (as opposed to legacy).
      Rsv (bit 4)
          Reserved.
      RS (bit 3) - Report Status
          See the description in the legacy transmit descriptor in Section 7.2.3.2.2.
      Rsv (bit 2)
          Reserved.

436                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

    IFCS (bit 1) - Insert FCS
          When this bit is set, the hardware appends the MAC FCS at the end of the packet. When
          cleared, software should calculate the FCS for proper CRC check. There are several cases in
          which software must set IFCS as follows:
           • Transmitting a short packet while padding is enabled by the HLREG0.TXPADEN bit.
           • Checksum offload is enabled by the either IC, TXSM or IXSM bits in the TDESC.DCMD.
           • VLAN header insertion enabled by the VLE bit in the TDESC.DCMD.
           • FC CRC (FCoE) offload is enabled by the FCoE bit in the transmit context descriptor.
           • TCP or FCoE segmentation offload enabled by the TSE bit in the TDESC.DCMD.
    EOP (bit 0) - End of Packet
          A packet might be composed of multiple buffers (each of them is indicated by its own
          descriptor). When EOP is set, it indicates the last descriptor making up the packet. In transmit
          segmentation (explained later on in this section) the EOP flag indicates the last descriptor of the
          last packet of the segmented transmission.
          Note:       TSE, VLE, and IFCS fields should be set in the first descriptor of the packet(s). The RS
                      bit can be set only on the last descriptor of the packet. The EOP bit is valid in all
                      descriptors. The DEXT bit must be set to 1b for all descriptors.
                      Descriptors with zero length, transfer no data. If the RS bit in the command byte is
                      set, the DD field in the status word is not written when hardware processes them.
STA (4)
    Rsv (bit 3:1)
          Reserved.
    DD (bit 0) - Descriptor Done
          The DD bit provides a status indication that the DMA of the buffer has completed. Software
          might re-use descriptors with the DD bit set, and any other descriptors processed by hardware
          before this one. In TSO, the buffers that include the TSO header are used multiple times during
          transmission and special considerations should be made as described in Section 7.2.4.2.2.
IDX (3)
    This field holds the index into the hardware context table to indicate which of the two per-queue
    contexts should be used for this request. If no offload is required and the CC bit is cleared, this field
    is not relevant and no context needs to be initiated before the packet is sent. See Table 7-38 for
    details of which packets requires a context reference. This field is relevant only on the first
    descriptor of the packet(s).
CC (1)
    Check Context bit — When set, a Tx context descriptor indicated by IDX index should be used for
    this packet(s). The CC bit should be set in the following cases:
     1. Non-zero QCNTLEN field is required (defined in the context descriptor).
     2. Any FCoE offload is required.
     3. Tx switching is enabled (including anti-spoof checks).

333369-009                                                                                                 437
                                   Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                   Inline Functions

POPTS (6)
      Rsv (bit 5:2)
          Reserved.
      TXSM (bit 1) - Insert TCP/UDP Checksum
          When set to 1b, the L4 checksum must be inserted. In this case, TUCMD.LP4 indicates whether
          the checksum is TCP or UDP or SCTP. When DCMD.TSE is set, TXSM must be set to 1b. If this
          bit is set, the packet should at least contain a TCP header.
      IXSM (bit 0) - Insert IP Checksum
          This field indicates that IP checksum must be inserted. In IPv6 mode, it must be reset to 0b. If
          DCMD.TSE and TUCMD.IPV4 are set, IXSM must be set to 1b. If this bit is set, the packet should
          at least contain an IP header.
          This field is relevant only on the first descriptor of the packet(s).
PAYLEN (18)
      PAYLEN indicates the size (in byte units) of the data buffer(s) in host memory for transmission.
      In a single-send packet, PAYLEN defines the entire packet size fetched from host memory. It does
      not include the fields that hardware adds such as: optional VLAN tagging, the FCoE trailer
      containing the FC CRC and EOF (For FCoE packets) and Ethernet CRC or Ethernet padding.
      When IPsec offload is enabled, the PAYLEN field does not include the ESP trailer added by hardware.
      In TSO (regardless if it is transmitted on a single or multiple packets), the PAYLEN defines the
      protocol payload size fetched from host memory.
       • In TCP or UDP segmentation offload, PAYLEN defines the TCP/UDP payload size.
       • In FCoE TSO offload, the PAYLEN field defines the FC payload size. It includes the FC option
         headers (if present) and the FC data payload but excludes the FCoE trailer containing the FC
         CRC and EOF.
      This field is relevant only on the first descriptor of the packet(s). The minimum transmitted packet
      size excluding VLAN padding and CRC bytes is 17 and the PAYLEN size should meet this limitation.
      On a single-packet send, the maximum size of the PAYLEN is dictated by the maximum allowed
      packet size which is 15.5 KB. On TSO, the maximum PAYLEN can be up to 218-1.
Note:       When a packet spreads over multiple descriptors, all of the descriptor fields are valid only on
            the first descriptor of the packet, except for RS and EOP bits, which are set on the last
            descriptor of the packet.

438                                                                                                    333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.2.3.3 Transmit Descriptor Ring

The transmit descriptor ring structure (shown in Figure 7-21) uses a contiguous memory space. A set of
four registers (described later in this section) maintain the transmit descriptor ring in the host memory.
Hardware maintains internal circular queues of 64 descriptors per queue to hold the descriptors that
were fetched from the software ring.
Descriptors handled to hardware should not be manipulated by software until hardware completes its
processing. It is indicated by advancing the head pointer beyond these descriptors.

                               Base
                                                                          descriptor currently
                                             Descriptors                  processed by HW
                               Head         Owned by SW

                  Transmit                   Descriptors                  Last descriptor
                    Queue                   Owned by HW                   added by SW

                                Tail
                                             Descriptors
                                            Owned by SW
                      Base + Length

Figure 7-21. Transmit Descriptor Ring Structure

The transmit descriptor ring is defined by the following registers:
 • Transmit Descriptor Base Address register (TDBA 0-127) — This register indicates the start
   address of the descriptor ring buffer in the host memory; this 64-bit address is aligned on a 128-
   byte boundary and is stored in two consecutive 32-bit registers. Hardware ignores the lower 7 bits.
 • Transmit Descriptor Length register (TDLEN 0-127) — This register determines the number of
   bytes allocated to the circular buffer. This value must be 0 modulo 128.
 • Transmit Descriptor Head register (TDH 0-127) — This register holds a value that is an offset
   from the base and indicates the in-progress descriptor. There can be up to 64 K minus 8 descriptors
   in the circular buffer. The transmit queue consists of the descriptors between the head and tail
   pointers. Transmission starts with the descriptor pointer by the head registers. When the DMA
   engine processes a descriptor, it might optionally write back the completed descriptor and then
   advance the head pointer. It then processes the next descriptor up to the point that the head
   pointer reaches the tail. Head equals tail means that the transmit queue in host memory is empty.
   Reading this register indicates the hardware progress to the software. All descriptors behind the
   head pointer and in front of tail register are owned by the software. The other descriptors are
   owned by the hardware and should not be modified by the software.

333369-009                                                                                             439
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

 • Transmit Descriptor Tail register (TDT 0-127) — This register holds a value, which is an offset
   from the base, and indicates the location beyond the last descriptor hardware can process.
   Software adds new descriptors to the ring by writing descriptors in the circular buffer pointed by the
   tail pointer. The new descriptor(s) are indicated to hardware by updating the tail pointer one
   descriptor above the last added descriptor. Note that a single packet or TSO might be composed of
   multiple descriptors. The transmit tail pointer should never point to the middle of a packet or TSO,
   which might cause undesired software/hardware races.
Software might detect which packets have already been processed by hardware using the following:
 • Read the TDH head register to determine which packets (those logically before the head) have been
   transferred to the on-chip FIFO or transmitted. This method is not recommended as races between
   the internal update of the head register and the actual write back of descriptors can occur.
 • When head write back is enabled (TDWBAL[n].HEAD_WB_EN = 1b) software might read the image
   of the head pointer in host memory at the address defined by TDWBAH[n]/TDWBAL[n] pair.
   Hardware updates the head image in host memory by completed descriptors as described in
   Section 7.2.3.5.2.
 • When head write back is not enabled (TDWBAL[n].HEAD_WB_EN = 0b), software might track the
   DD bits in the descriptor ring. Descriptor write back is controlled by the RS bit and the WTHRESH
   setting as well as interrupt assertion.
 • Issue an interrupt. An interrupt condition is generated each time a packet was transmitted or
   received and a descriptor was write back or transmit queue goes empty (EICR.RTxQ[0-19]). This
   interrupt can either be enabled or masked.
All of the registers controlling the descriptor rings behavior should be set before transmit is enabled.

#### 7.2.3.4 Transmit Descriptor Fetching

The X550 fetches new descriptors as required for packet transmission depending on its on-die
descriptor buffer state:
 • Fetch — The on-chip descriptor buffer is empty or contains less descriptors than a complete
   packet.
      — A fetch starts as soon as any descriptors are made available (host writes to the tail pointer).
      — A request is issued for any available descriptors up to the size of the on-die buffer.
      — Once the sum of on-die descriptors and requested descriptors is more than required for a single
        packet, the buffer transitions to the pre-fetch state.
      — If several on-chip descriptor queues are empty simultaneously, queues are served in round
        robin arbitration except the queues indicated as strict priority, which are served first.
 • Pre-Fetch — The on-chip descriptor buffer becomes almost empty while there are enough
   descriptors in the host memory.
      — The on-chip descriptor buffer is defined as almost empty if it contains less descriptors than the
        threshold defined by TXDCTL[n].PTHRESH.
      — The transmit descriptor contains enough descriptors if it includes more ready descriptors than
        the threshold defined by TXDCTL[n].HTHRESH.
      — In pre-fetch mode, descriptors are fetched only after there are no other DMA activity of greater
        priority as: transmit descriptor fetch; status write-backs or packet data transfers).
      — A request is issued for any available descriptors up to the capacity of the on-die buffer.

440                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

     — If several on-chip descriptor queues are in this situation simultaneously, queues are served in
       round robin arbitration except the queues indicated as strict priority which are served first.
 • Idle — Requests are not issued. This is the state reached when none of the previous states apply.
Note:        Software must update the Tail register on packet boundaries. That is, the last valid descriptor
             might not be a context descriptor and must have the EOP bit set.

7.2.3.4.1               Transmit Descriptor Fetch and Write-back Settings

This section describes the settings of transmit descriptor thresholds. It relates to fetch thresholds
described above as well as the write-back threshold (WTHRESH) when operating in descriptor
write-back mode, which is described in Section 7.2.3.5.1.
 • Transmit descriptor fetch setting is programmed in the TXDCTL[n] register per queue. The default
   settings of PTHRESH, HTHRESH and WTHRESH are zero’s.
 • To reduce transmission latency, it is recommended to set the PTHRESH value as high as possible
   while the HTHRESH and WTHRESH as low as possible (down to zero).
 • To minimize PCIe overhead the PTHRESH should be set as low as possible while HTHRESH and
   WTHRESH should be set as high as possible.
 • The sum of PTHRESH plus WTHRESH must not be greater than the on-chip descriptor buffer size.
 • Some practical rules:
     — CPU cache line optimization — Assume ‘N’ equals the CPU cache line divided by 16 (descriptor
       size). Then, to align descriptors pre-fetch to CPU cache line (in most cases), it is advised to set
       PTHRESH to the on-chip descriptor buffer size minus ‘N’ and HTHRESH to ‘N’. To align descriptor
       write back to the CPU cache line it is advised to set WTHRESH to either 'N' or even 2 times 'N'.
       Note that partial cache line writes might significantly degrade performance. Therefore, it is
       highly recommended to follow this advice.
     — Minimizing PCIe overhead — As an example, setting PTHRESH to the on-chip descriptor buffer
       size minus 16 and HTHRESH to 16 minimizes the PCIe request and header overhead to ~20%
       of the bandwidth required for the descriptor fetch.
     — Minimizing transmission latency from tail update — Setting PTHRESH to the on-chip descriptor
       buffer size minus ‘N’ (‘N’ previously defined) while HTHRESH and WTHRESH to zero.
     — Threshold settings in DCB mode — Note that only values of PTHRESH equals on-chip descriptor
       buffer size minus 8 and HTHRESH equals 4 were thoroughly tested.
Note:        As previously described, device setting is a trade-off between overhead (translated to
             performance) and latencies. It is expected that some level of optimization is done at software
             driver development phase. Customers who want better performance might need to adjust the
             threshold values according to the previous guidelines while optimizing to specific platform and
             targets.

#### 7.2.3.5 Transmit Write Back

The X550 periodically updates software on its progress in processing transmit buffers. Two methods are
described for doing so:
 • Updating by writing back into the Tx descriptor.
 • Update by writing to the head pointer in system memory.

333369-009                                                                                               441
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

7.2.3.5.1            Tx Descriptor Write Back

When the TXDCTL[n].WTHRESH equals zero, descriptors are written back for those descriptors with the
RS bit set. When the TXDCTL[n].WTHRESH value is greater than zero, descriptors are accumulated until
the number of accumulated descriptors equals the TXDCTL[n].WTHRESH value, then these descriptors
are written back. Accumulated descriptor write back enables better use of the PCIe bus and memory
bandwidth.
Any descriptor write back includes the full 16 bytes of the descriptor.
Descriptors are written back in one of three cases:
 • TXDCTL[n].WTHRESH = 0 and a descriptor that has RS set is ready to be written back.
 • TXDCTL[n].WTHRESH > 0 and TXDCTL[n].WTHRESH descriptors have accumulated.
 • TXDCTL[n].WTHRESH > 0 and the corresponding EITR counter has reached zero. The timer
   expiration flushes any accumulated descriptors and sets an interrupt event (TXDW).
An additional mode in which transmit descriptors are not written back at all and the head pointer of the
descriptor ring is written instead is described in the following section.

7.2.3.5.2            Tx Head Pointer Write Back

In legacy hardware, transmit requests are completed by writing the DD bit to the transmit descriptor
ring. This causes cache trash since both the driver and hardware are writing to the descriptor ring in
host memory. Instead of writing the DD bits to signal that a transmit request is complete, hardware can
write the contents of the descriptor queue head to host memory. The driver reads that memory location
to determine which transmit requests are complete. To improve the performance of this feature, the
driver needs to program TPH registers to configure which CPU processes each Tx queue.
The head pointer is reflected in a memory location that is allocated by software for each queue.
Rules for head pointer write back:
 • Head write back occurs if TDWBAL[n].HEAD_WB_EN is set for this queue, and the RS bit is set in
   the Tx descriptor, following its corresponding data upload into packet buffer.
      — If the head write-back feature is enabled, software must set WTHRESH to 0x0 while only
        descriptors with the RS bit set, generate header write back.
      — Note that the head pointer write back does not hold transmission. Instead, if packets with the
        RS bit are transmitted fast enough, it might happen that the header pointer write back is not
        updated for each and every packet. In addition, it might happen that the head pointer write
        back might be updated up to descriptors that do not have the RS bit set. In such cases,
        hardware might report a completion of a descriptor that might not be the last descriptor in a
        TSO or even the last descriptor in a single packet.
The driver has control of this feature per queue through the TDWBAL and TDWBAH registers.
The low register's LSB hold the control bits.
 • The HEAD_WB_EN bit enables activation of tail write back. In this case, no descriptor write back is
   executed.
 • The 30 upper bits of this register hold the lowest 32 bits of the head write-back address, assuming
   that the two last bits are zero.
The high register holds the high part of the 64-bit address.
Note:     Hardware writes a full DWord when writing this value, so software should reserve enough
          space for each head value and make sure the TDBAL value is DWord-aligned.

442                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.2.4 TCP and UDP Segmentation

Hardware TCP segmentation is one of the offloading options supported by the Windows* and Linux*
TCP/IP stack. This is often referred to as Large Send offloading or TSO. This feature enables the TCP/IP
stack to pass to the network device driver a message to be transmitted that is bigger than the
Maximum Transmission Unit (MTU) of the medium. It is then the responsibility of the device driver and
hardware to divide the TCP message into MTU size frames that have appropriate layer 2 (Ethernet), 3
(IP), and 4 (TCP) headers. These headers must include sequence number, checksum fields, options and
flag values as required. Note that some of these values (such as the checksum values) are unique for
each packet of the TCP message, and other fields such as the source IP Address is constant for all
packets associated with the TCP message.
Similar to TCP segmentation, the X550 also provides a capability to offload UDP segmentation. Note
that current UDP segmentation offload is not supported by any standard operating system.
Note:        CRC appending (HLREG0.TXCRCEN) must be enabled in TCP / UDP segmentation mode
             because CRC is inserted by hardware.
             Padding (HLREG0.TXPADEN) must be enabled in TCP / UDP segmentation mode, since the
             last frame might be shorter than 60 bytes — resulting in a bad frame if TXPADEN is disabled.
The offloading of these mechanisms to the device driver and the X550 saves significant CPU cycles. The
device driver shares the additional tasks to support these options with the X550.

#### 7.2.4.1 Assumptions and Restrictions

The following assumptions apply to the TCP / UDP segmentation implementation in the X550:
 • To limit the internal cache dimensions, software is required to spread the header onto a maximum
   four descriptors, while still allowed to mix header and data in the last header buffer. This limitation
   stands for up to Layer 4 header included, and for IPv4 or IPv6 independently.
 • The maximum size of a single TSO can be as large as defined by the PAYLEN field in the Tx data
   descriptor (such as up to 256 KB).
 • The RS bit operation is not changed. Interrupts are set after data in the buffers pointed to by
   individual descriptors is transferred (DMA'ed) to hardware.
 • SNAP packets are not supported for segmentation.
 • IP in IP tunneled packets are not supported for offloading under TSO operation. VXLAN and NVGRE
   tunneled packets can be segmented.
 • Software must enable the Ethernet CRC offload in the HLREG0.TXCRCEN register since CRC must
   be inserted by hardware after the checksum has been calculated.
 • Software must initialize the appropriate checksum fields in the packet’s header.

#### 7.2.4.2 Transmission Process

The transmission process involves the following:
 • The protocol stack receives from an application a block of data that is to be transmitted.
 • The protocol stack calculates the number of packets required to transmit this block based on the
   MTU size of the media and required packet headers.

333369-009                                                                                             443
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

 • The stack interfaces with the device driver and passes the block down with the appropriate header
   information: Ethernet, IP and TCP / UDP headers.
 • The stack interfaces with the device driver and commands the driver to send the individual packet.
   The device driver sets up the interface to the hardware (via descriptors) for the TCP / UDP
   segmentation.
 • The hardware transfers (DMA's) the packet data and performs the Ethernet packet segmentation
   and transmission based on offset and payload length parameters in the TCP/IP or UDP/IP context
   descriptor including:
      — Packet encapsulation
      — Header generation and field updates including IPv4/IPv6 and TCP/UDP checksum generation.
 • The driver returns ownership of the block of data to the NOS when the hardware has completed the
   DMA transfer of the entire data block.

7.2.4.2.1            TCP and UDP Segmentation Data Fetch Control

To perform TCP / UDP segmentation in the X550, the DMA must be able to fit at least one packet of the
segmented payload into available space in the on-chip packet buffer. The DMA does various
comparisons between the remaining payload and the packet buffer available space, fetching additional
payload and sending additional packets as space permits.
The X550 enables interleaving between different TSO requests at an Ethernet packet level. In other
words, the X550 might fetch part of a TSO from a queue, equivalent to one or more Ethernet packets,
then transition to another queue and fetch the equivalent of one or more packets (TSO or not), then
move to another queue (or the first queue), etc. The X550 decides on the order of data fetched based
on its QoS requirements (such as bandwidth allocation and priority).
To enable interleaving between descriptor queues at the Ethernet frame resolution inside TSO requests,
the frame header pointed by the so called header descriptors are re-read from system memory for
every TSO segment (once per packet), storing in an internal cache only the header’s descriptors instead
of the header’s content.

7.2.4.2.2            TCP and UDP Segmentation Write-back Modes

TCP / UDP segmentation mode uses the buffers that contain the header of the packet multiple times
(once for each transmitted segment). Software should guarantee that the header buffers are available
throughout the entire TSO transmission. Therefore, software should not re-use any descriptors of the
TSO header during the TSO transmission.

#### 7.2.4.3 TCP and UDP Segmentation Performance

Performance improvements for a hardware implementation of TCP / UDP segmentation offload include:
 • The stack does not need to partition the block to fit the MTU size, saving CPU cycles.
 • The stack only computes one Ethernet, IP, and TCP / UDP header per segment, saving CPU cycles.
 • The stack interfaces with the device driver only once per block transfer, instead of once per frame.
 • Larger PCI bursts are used, which improves bus efficiency (such as lowering transaction overhead).
 • Interrupts are easily reduced to one per TCP / UDP message instead of one per packet.
 • Fewer I/O accesses are required to command the hardware.

444                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.2.4.4 Packet Format

 A TCP / UDP message can be as large as 256 KB and is generally fragmented across multiple pages in
host memory. The X550 partitions the data packet into standard Ethernet frames prior to transmission.
The X550 supports calculating the Ethernet, IP, TCP, and UDP headers, including checksum, on a frame-
by-frame basis. For tunneled packets (NVGRE, VXLAN), The X550 also supports updating the outer IPv4
header.

Table 7-41. TCP/IP and UDP/IP Packet Format Sent by Host
                                Pseudo Header                                                 Data

                     Optional tunnel
     Ethernet                                IPv4/IPv6         TCP/UDP             DATA (full TCP/UDP message)
                         header

Table 7-42. Packets Format Sent by Device
    Pseudo                                                         Pseudo
                  Data (first                                                Data (Next
   Header                              FCS               ...      Header                       FCS               ...
                    MSS)                                                       MSS)
  (updated)                                                      (updated)

Frame formats supported by the X550 include:
 • Ethernet 802.3
 • IEEE 802.1Q VLAN (Ethernet 802.3ac)
 • Ethernet Type 2
 • NVGRE (see frame format in Section A.2.5.1)
 • VXLAN (see frame format in Section A.2.5.2)
 • IPv4 headers with options
 • IPv6 headers with extensions
 • TCP with options
 • UDP with options
VLAN tag insertion can be handled by hardware.
Note:        UDP (unlike TCP) is not a reliable protocol and fragmentation is not supported at the UDP
             level. UDP messages that are larger than the MTU size of the given network medium are
             normally fragmented at the IP layer. This is different from TCP, where large TCP messages can
             be fragmented at either the IP or TCP layers depending on the software implementation.
             The X550 has the ability to segment UDP traffic (in addition to TCP traffic); however, because
             UDP packets are generally fragmented at the IP layer, the X550's segmentation capability
             might not be used in practice for UDP.

#### 7.2.4.5 TCP and UDP Segmentation Indication

Software indicates a TCP/UDP segmentation transmission context to the hardware by setting up a
TCP/IP or UDP/IP context transmit descriptor (see Section 7.2.3). The purpose of this descriptor is to
provide information to the hardware to be used during the TCP / UDP segmentation offload process.

333369-009                                                                                                             445
                                       Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

Setting the TSE bit in the DCMD field to one (in the data descriptor) indicates that this descriptor refers
to the segmentation context (as opposed to the normal checksum offloading context). This causes the
checksum offloading, packet length, header length, and maximum segment size parameters to be
loaded from the descriptor into the device.
The TCP/UDP segmentation prototype header is taken from the packet data itself. Software must
identity the type of packet that is being sent (IPv4/IPv6, TCP/UDP, other), calculate appropriate
checksum off loading values for the desired checksums, and then calculate the length of the header
that is pre-appended. The header can be up to 240 bytes in length.
Once the TCP/UDP segmentation context has been set, the next descriptor provides the initial data to
transfer. This first descriptor(s) must point to a packet of the type indicated. Furthermore, the data it
points to might need to be modified by software as it serves as the prototype header for all packets
within the TC /UDP segmentation context. The following sections describe the supported packet types
and the various updates that are performed by hardware. This should be used as a guide to determine
what must be modified in the original packet header to make it a suitable prototype header.
The following summarizes the fields considered by the driver for modification in constructing the
prototype header.
IP Header
      For IPv4 headers:
       • Identification field should be set as appropriate for first packet of send (if not already).
       • Header checksums of inner and outer IP headers should be zeroed out unless some adjustment
         is needed by the driver.
TCP Header
       • Sequence number should be set as appropriate for first packet of send (if not already).
       • PSH, and FIN flags should be set as appropriate for LAST packet of send.
       • TCP checksum should be set to the partial pseudo-header checksum as follows (there is a more
         detailed discussion of this in Section 7.2.4.6:

      Table 7-43. TCP Partial Pseudo-header Checksum for IPv4
                                                        IP Source Address

                                                     IP Destination Address

           Zero           Layer 4 Protocol ID                                            Zero

      Table 7-44. TCP Partial Pseudo-header Checksum for IPv6
                                                      IPv6 Source Address

                                                  IPv6 Final Destination Address

                                                              Zero

                                           Zero                                                        Next Header

UDP Header
       • Checksum should be set as in TCP header, as previously explained.
The following sections describe the updating process performed by the hardware for each frame sent
using the TCP segmentation capability.

446                                                                                                               333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.2.4.6 Transmit Checksum Offloading with TCP and UDP

                       Segmentation
The X550 supports checksum offloading as a component of the TCP/UDP segmentation off-load feature
and as stand-alone capability. Section 7.2.5 describes the interface for controlling the checksum
off-loading feature. This section describes the feature as it relates to TCP/UDP segmentation.
The X550 supports IP and TCP header options in the checksum computation for packets that are
derived from the TCP segmentation feature.
Two specific types of checksum are supported by the hardware in the context of the TCP/UDP
segmentation off-load feature:
 • IPv4 checksum
 • TCP/UDP checksum
Each packet that is sent via the TCP/UDP segmentation off-load feature optionally includes the IPv4
checksum and/or the TCP/UDP checksum.
All checksum calculations use a 16-bit wide one's complement checksum. The checksum word is
calculated on the outgoing data.
Refer to Table 7-45 for the list of supported transmit checksums per packet type.

#### 7.2.4.7 IP/TCP/UDP Header Updating

IP/TCP and IP/UDP header is updated for each outgoing frame based on the header prototype that
hardware DMA's from the first descriptor(s). The checksum fields and other header information are
later updated on a frame-by-frame basis. The updating process is performed concurrently with the
packet data fetch.
The following sections define what fields are modified by hardware during the TCP/UDP segmentation
process by the X550.

7.2.4.7.1               TCP/IP/UDP Header for the First Frame

The hardware makes the following changes to the headers of the first packet that is derived from each
TCP segmentation context.
Tunnel Header
When tunnel offload is enabled (Tunnel bit set in the descriptor) the outer IPv4 header is updated as
follows:
 • IP Total Length = OUTERIPLEN + TUNNELLEN + IPLEN + L4LEN + MSS
 • Calculates the Outer IP Checksum
IPv4 Header
 • IP Total Length = MSS + L4LEN + IPLEN
 • Calculates the IP Checksum
IPv6 Header
 • Payload Length = MSS + L4LEN + IPV6_HDR_extension1

 1. IPV6_HDR_extension is calculated as IPLEN — 40 bytes.

333369-009                                                                                            447
                                    Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                   Inline Functions

TCP Header
 • Sequence Number: The value is the sequence number of the first TCP byte in this frame.
 • The flag values of the first frame are set by logic AND function between the flag word in the pseudo
   header and the DTXTCPFLGL.TCP_FLG_FIRST_SEG. The default values of the
   DTXTCPFLGL.TCP_FLG_FIRST_SEG are set. The flags in a TSO that ends up as a single segment are
   taken from the in the pseudo header in the Tx data buffers as is.
 • Calculates the TCP checksum.
UDP Header
 • Calculates the UDP checksum.

7.2.4.7.2               TCP/IP Header for the Subsequent Frames

The hardware makes the following changes to the headers for subsequent packets that are derived as
part of a TCP segmentation context:
      Number of bytes left for transmission = PAYLEN — (N * MSS)

Where N is the number of frames that have been transmitted.
Tunnel Header
      When tunnel offload is enabled (Tunnel bit set in the descriptor) the outer IPv4 header is updated
      as follows:
       • IP Identification: increased from last value (wrap around based on 16-bit width)
       • IP Total Length = OUTERIPLEN + TUNNELLEN + IPLEN + L4LEN + MSS
       • Calculates the Outer IP Checksum
IPv4 Header
       • IP Identification: increased from last value (wrap around)
       • IP Total Length = MSS + L4LEN + IPLEN
       • Calculate the IP Checksum
IPv6 Header
       • Payload Length = MSS + L4LEN + IPV6_HDR_extension1
TCP Header
       • Sequence Number update: Add previous TCP payload size to the previous sequence number
         value. This is equivalent to adding the MSS to the previous sequence number.
       • The flag values of the subsequent frames are set by logic AND function between the flag word
         in the pseudo header with the DTXTCPFLGL.TCP_FLG_MID_SEG. The default values of the
         DTXTCPFLGL.TCP_FLG_MID_SEG are set.
       • Calculate the TCP checksum
UDP Header
       • Calculates the UDP checksum.

448                                                                                                    333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.2.4.7.3               TCP/IP Header for the Last Frame

Hardware makes the following changes to the headers for the last frame of a TCP segmentation
context:
    Last frame payload bytes = PAYLEN — (N * MSS)

Tunnel Header
    When tunnel offload is enabled (Tunnel bit set in the descriptor) the outer IPv4 header is updated
    as follows:
      • IP Identification: increased from last value (wrap around based on 16-bit width)
      • IP Total Length = OUTERIPLEN + TUNNELLEN + IPLEN + L4LEN + last frame payload bytes.
      • Calculates the Outer IP Checksum
IPv4 Header
      • IP Total length = last frame payload bytes + L4LEN + IPLEN
      • IP identification: increased from last value (wrap around based on 16-bit width)
      • Calculate the IP checksum
IPv6 Header
      • Payload length = last frame payload bytes + L4LEN + IPV6_HDR_extension1
TCP Header
      • Sequence number update: Add previous TCP payload size to the previous sequence number
        value. This is equivalent to adding the MSS to the previous sequence number.
      • The flag values of the last frames are set by logic AND function between the flag word in the
        pseudo header and the DTXTCPFLGH.TCP_FLG_LST_SEG. The default values of the
        DTXTCPFLGH.TCP_FLG_LST_SEG are set. The flags in a TSO that ends up as a single segment
        are taken from the in the pseudo header in the Tx data buffers as is.
      • Calculate the TCP checksum
UDP Header
      • Calculates the UDP checksum.

 1. IPV6_HDR_extension is calculated as IPLEN — 40 bytes.

333369-009                                                                                          449
                                    Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

### 7.2.5 Transmit Checksum Offloading in

                  Non-Segmentation Mode
The previous section on TCP/UDP segmentation offload describes the IP/TCP/UDP checksum offloading
mechanism used in conjunction with segmentation. The same underlying mechanism can also be
applied as a stand-alone checksum offloading. The main difference in a single packet send is that only
the checksum fields in the IP/TCP/UDP headers are calculated and updated by hardware.
Before taking advantage of the X550's enhanced checksum offload capability, a checksum context must
be initialized. For a single packet send, DCMD.TSE should be set to zero (in the data descriptor). For
additional details on contexts, refer to Section 7.2.3.3.
Enabling checksum offload, software must also enable Ethernet CRC offload by the HLREG0.TXCRCEN
since CRC must be inserted by hardware after the checksum has been calculated.
Each checksum operates independently. Insertion of the IP and TCP/UDP checksum for each packet are
enabled through the transmit data descriptor POPTS.TXSM and POPTS.IXSM fields, respectively.

#### 7.2.5.1 IP Checksum

Three fields in the transmit context descriptor set the context of the IP checksum offloading feature:
 • TUCMD.IPV4
 • IPLEN
 • MACLEN
TUCMD.IPV4=1 specifies that the packet type for this context is IPv4, and that the IP header checksum
should be inserted. TUCMD.IPV4=0 indicates that the packet type is IPv6 (or some other protocol) and
that the IP header checksum should not be inserted.
MACLEN specifies the byte offset from the start of the DMA'ed data to the first byte to be included in the
checksum, the start of the IP header. The minimal allowed value for this field is 14. Note that the
maximum value for this field is 127. This is adequate for typical applications.
Note:      The MACLEN+IPLEN value must be less than the total DMA length for a packet. If this is not
           the case, the results are unpredictable.
IPLEN specifies the IP header length. Maximum allowed value for this field is 511 bytes.
MACLEN+IPLEN specify where the IP checksum should stop. The sum of MACLEN+IPLEN must be
smaller equals to the first 638 (127+511) bytes of the packet and obviously must be smaller or equal to
the total length of a given packet. If this is not the case, the result is unpredictable.
For IP tunnel packets (IPv4-IPv6), IPLEN must be defined as the length of the two IP headers.
Hardware is able to offload the L4 checksum calculation while software should provide the IPv4
checksum.
For NVGRE and VXLAN tunneled packet as defined by the Tunnel bit in the descriptor, Outer IPv4
checksum is controlled by OUTERIPCS bit and is determined by MACLEN and OUTERIPLEN similar to the
above description. Inner IPv4 checksum is controlled by TUCMD.IPv4 and offset determination should
be adjusted by hardware such that MACLEN should be replaced by (MACLEN+OUTIPLEN+TUNNELLEN)
The 16-bit IPv4 header checksum is placed at the two bytes starting at MACLEN+10.

450                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.2.5.2 TCP and UDP Checksum

Three to five fields in the transmit context descriptor set the context of the TCP/UDP checksum
offloading feature:
 • MACLEN
 • OUTERIPLEN (optional)
 • TUNNELLEN (optional)
 • IPLEN
 • TUCMD.L4T
TUCMD.L4T=01b specifies that the packet type is TCP, and that the 16-bit TCP header checksum should
be inserted at byte offset MACLEN+IPLEN+16. TUCMD.L4T=00b indicates that the packet is UDP and
that the 16-bit checksum should be inserted starting at byte offset MACLEN+IPLEN+6. If Tunnel bit is
set, the checksum is inserted at MACLEN+OUTERIPLEN+TUNNELLEN+IPLEN+6.
MACLEN+(OUTERIPLEN+TUNNELLEN)+IPLEN specifies the byte offset from the start of the DMA'ed
data to the first byte to be included in the checksum, the start of the UDP/TCP header. See MACLEN
table in Section 7.2.3.2.3 for its relevant values.
Note:        The MACLEN+(OUTERIPLEN+TUNNELLEN)+IPLEN+L4LEN value must be less than the total
             DMA length for a packet. If this is not the case, the results are unpredictable.
The TCP/UDP checksum always continues to the last byte of the DMA data.
Note:        For non-TSO, software still needs to calculate a full checksum for the TCP/UDP pseudo-
             header. This checksum of the pseudo-header should be placed in the packet data buffer at the
             appropriate offset for the checksum calculation.

#### 7.2.5.3 SCTP CRC Offloading

For SCTP packets, a CRC32 checksum offload is provided.
Three fields in the transmit context descriptor set the context of the STCP checksum offloading feature:
 • MACLEN
 • IPLEN
 • TUCMD.L4T
TUCMD.L4T=10b specifies that the packet type is SCTP, and that the 32-bit STCP CRC should be
inserted at byte offset MACLEN+IPLEN+8.
IPLEN+MACLEN specifies the byte offset from the start of the DMA'ed data to the first byte to be
included in the checksum, the start of the STCP header. The minimal allowed value for this sum is 26.
See MACLEN table in Section 7.2.3.2.3 for its relevant values.
The SCTP CRC calculation always continues to the last byte of the DMA data.
The SCTP total L3 payload size (PAYLEN - IPLEN - MACLEN) should be a multiple of four bytes (SCTP
padding not supported).
Note:        TSO is not available for SCTP packets.
Note:        The CRC field of the SCTP header must be set by driver to zero prior to requesting a CRC
             calculation offload.

333369-009                                                                                              451
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                             Inline Functions

#### 7.2.5.4 Checksum Supported per Packet Types

Table 7-45 lists which checksums are supported per packet type.
Note:       TSO is not supported for packet types for which IP checksum and TCP/UDP checksum cannot
            be calculated.

Table 7-45. Checksums Supported by Packet Type
                                                             Hardware IP                     Hardware TCP/UDP/SCTP
                    Packet Type
                                                         Checksum Calculation                 Checksum Calculation

 IPv4 packets                                                       Yes                                  Yes

 IPv6 packets                                                     No (n/a)                               Yes

 IPv6 packet with next header options:
  • Hop-by-hop options                                            No (n/a)                               Yes
  • Destinations options                                          No (n/a)                               Yes
  • Routing (with len 0)                                          No (n/a)                               Yes
  • Routing (with len >0)                                         No (n/a)                               No
  • Fragment                                                      No (n/a)                               No
  • Home option                                                   No (n/a)                               No
  • Security option (AH/ESP)                                      No (n/a)                               Yes

 IPv4 tunnels:
  • IPv4 packet in an IPv4 tunnel                                   No                                   No
  • IPv6 packet in an IPv4 tunnel                                   No                                   Yes

 IPv6 tunnels:
  • IPv4 packet in an IPv6 tunnel                                   No                                    No
  • IPv6 packet in an IPv6 tunnel                                   No                                    No

 Packet is an IPv4 fragment                                         Yes                                   No

 Packet has 802.3ac tag                                             Yes                                  Yes

 IPv4 packet has IPsec header without IP options                    Yes                                  Yes

 Packet has TCP or UDP options                                      Yes                                  Yes

 IP header’s protocol field contains protocol # other
                                                                    Yes                                   No
 than TCP, UDP, or SCTP

 NVGRE:
  • Inner IPv4 packet                                     Yes (Inner and outer)                          Yes
  • Inner IPv6 packet                                          Yes (outer)                               Yes

 VXLAN:
  • Inner IPv4 packet                                     Yes (Inner and outer)                    Yes (inner only)1
  • Inner IPv6 packet                                          Yes (outer)                         Yes (inner only)

1. The outer UDP header of VXLAN packets do not use a checksum.

452                                                                                                                333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.2.6 Transmit Statistics

#### 7.2.6.1 General Notes

 • All Statistics registers are cleared on read. In addition, they stick at 0xFF...F when the maximum
   value is reached.
 • Due to divergent paths between interrupt-generation and logging of relevant statistics counts, it
   might be possible to generate an interrupt to the system for a noteworthy event prior to the
   associated statistics count actually being increased. This is extremely unlikely due to expected
   delays associated with the system interrupt-collection and ISR delay, but might be an explanation
   for interrupt statistics values that do not quite make sense. Hardware guarantees that any event
   noteworthy of inclusion in a statistics count is reflected in the appropriate count within 1 s; a small
   time-delay prior to reading the statistics might be required to avoid a potential mismatch between
   and interrupt and its cause.
 • If TSO is enabled, statistics are collected after segmentation.
 • All byte (octet) counters composed of 2 registers can be fetched by two consecutive 32-bit accesses
   while reading the Low 32-bit register first or a single 64-bit access.

#### 7.2.6.2 Transmit Statistics Hierarchy

Figure 7-22 describes the relations between the packet flow and the different statistic counters.

333369-009                                                                                              453
                                 Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

                                       TPT

                                   MAC errors
                               (excessive collisions          MAC drops
                                   Link down)

                                                          Flow control packets
                               Flow control packets            XONTXC
                                                              XOFFTXC

                           GPTC (Only if Tx is enabled)

                              Manageability Muxing            OS to BMC packets
                                     Out                          O2BGPTC

                              Manageability Muxing           Manageability packets
                                     In                          MNGPTC

                               Packets Sent to BMC
                                    O2BSPC
                              Packets Sent from host
                                    TXDGPC

                                                          Security Errors (anti spoof)
                                 Switch Security
                                                                    SSVPC

Figure 7-22. Transmit Flow Statistics

454                                                                                                               333369-009
                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions
