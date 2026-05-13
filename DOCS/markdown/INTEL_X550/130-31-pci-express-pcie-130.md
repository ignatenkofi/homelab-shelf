## 3.1 PCI Express (PCIe)

### 3.1.1 General Overview

The X550 supports Rev 3.0 of the PCIe base specification.
On top of the capabilities required by the PCIe specifications, The X550 supports optional functionality
as listed in this section:
 • All PCI functions are native PCIe functions.
 • Physical Layer:
     — Support for 2.5 GT/s, 5 GT/s, and 8 GT/s
     — Interface width of 1, 4 or 8 PCIe lanes (8 lanes are supported only in the X550-BT2, and only at

    5 GT/s or 2.5 GT/s speeds.)

     — Full swing and half swing signaling
     — Lane reversal
 • Transaction layer mechanisms:
     — 64-bit and 32-bit memory address spaces
     — Removal of I/O BAR (optional)
     — Relaxed ordering
     — Flow control update timeout mechanism
     — ID-based ordering (IDO)
     — Packet sizes: Maximum packet size: 512, Maximum read request size: 2 KB
     — Function-Level Reset (FLR)
     — TLP Processing Hints (TPH)
 • Reliability:
     — Advanced Error Reporting (AER)
     — End-to-End CRC (ECRC) generation and checking
     — Recovery from data poisoning
     — Completion Timeout
 • Power management:
     — Active state power management (L1 state)
     — Wake capability
     — Latency Tolerance Reporting (LTR)
 • DFT and DFM support for high-volume manufacturing.

333369-009                                                                                             65
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

 • The X550 supports the following Extended Capabilities:
     — Advanced Error Reporting (AER)
     — Device Serial Number
     — Alternative RID Interpretation (ARI)
     — Single Root I/O Virtualization (SR-IOV)
     — TPH Requester — Access Control Services (ACS)

### 3.1.2 Transaction Layer

#### 3.1.2.1 Transaction Types Accepted by the X550

Table 3-1 summarizes the transactions accepted by the device and their attributes.

Table 3-1.         Transaction Types Accepted by the Transaction Layer
                                                                              Hardware Should Keep Data from
          Transaction Type              FC Type         Tx Layer Reaction
                                                                                     Original Packet

Configuration Read Request                NPH             CPLH + CPLD             Requester ID, TAG, attribute

Configuration Write Request            NPH + NPD              CPLH                Requester ID, TAG, attribute

Memory Read Request                       NPH             CPLH + CPLD             Requester ID, TAG, attribute

Memory Write Request                     PH + PD                -                              -

IO Read Request                           NPH             CPLH + CPLD             Requester ID, TAG, attribute

IO Write Request                       NPH + NPD              CPLH                Requester ID, TAG, attribute

Read Completions                       CPLH + CPLD              -                              -

Message                                    PH                   -                              -

Flow Control Types Legend:
     CPLD — Completion Data Payload
     CPLH — Completion Headers
     NPD — Non-Posted Request Data Payload
     NPH — Non-Posted Request Headers
     PD — Posted Request Data Payload
     PH — Posted Request Headers

66                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

3.1.2.1.1              Size of Target Accesses

3.1.2.1.1.1             Memory Accesses

Rules for accesses to the CSR space (both memory BAR and MSI-X BAR):
Write accesses:
     — Zero-length writes have no internal impact (nothing written, no effect such as clear-by-write).
       The transaction is treated as a successful operation (no error event).
     — CSR writes are 32-bit or 64-bit only. Larger or partial CSR writes are handled as Completer
       Abort - data is dropped and an error is generated per PCIe rules.
 • Read accesses:
     — Partial reads with at least one byte disabled are handled as a full read. Any side effect of the full
       read (such as clear by read) is also applicable to partial reads. The completion on PCIe obeys
       the specification rules regarding the number of bytes reported in the completion.
     — Zero-length reads generate a completion, but the register is not accessed and undefined data is
       returned.
     — CSR reads are 32-bit or 64-bit only. Larger CSR read requests are handled as Completer Abort.
       The completion includes a CA status and an error is generated per PCIe rules.
     — Some 64-bit reads are handled atomically (i.e. not interleaved with any other requests). This
       applies mainly to reading counters, where all 64-bit need to be read simultaneously. Such
       registers are explicitly marked in their description.
Rules for accessing the Flash space in the memory BAR or the Expansion ROM BAR:
 • Write accesses:
     — Writes to Flash are 8-bit wide only.
     — Any larger write accesses are handled as Completer Abort - data is dropped and an error is
       generated per PCIe rules.
 • Read accesses:
     — Reads to Flash are 32-bit wide.
     — Partial reads with at least one byte disabled are handled internally as a full read. That is, any
       side effect of the full read (such as clear by read) is also applicable to partial reads. The
       completion on PCIe obeys the specification rules regarding the number of bytes reported in the
       completion.
     — Larger CSR read requests are handled as Completer Abort - the completion includes a CA status
       and an error is generated per PCIe rules.

333369-009                                                                                                67
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                       Interconnects

3.1.2.1.1.2                I/O Accesses

Rules for accesses to the I/O BAR:
 • Write accesses:
     — Write accesses are 32-bit wide.
     — Zero-length writes have no internal impact (nothing written, no effect such as clear-by-write).
       The transaction is treated as a successful operation (no error event).
     — Other accesses (partial writes, larger writes) are handled as Completer Abort - data is dropped
       and an error is generated per PCIe rules.
 • Read accesses:
     — Reads to the I/O BAR are 32-bit wide.
     — Partial reads with at least one byte disabled are handled internally as a full read. That is, any
       side effect of the full read (such as clear by read) is also applicable to partial reads. The
       completion on PCIe obeys the specification rules regarding the number of bytes reported in the
       completion.
     — Larger CSR read requests are handled as Completer Abort - the completion includes a CA status
       and an error is generated per PCIe rules.

3.1.2.1.1.3                Messages

MCTP messages may contain payload of up to 64 bytes.

3.1.2.1.2                  Support for Dynamic Changes

The X550 captures the Bus Number and Device Number per each Configuration Write Request.
However, dynamic change of Bus Number or Device Number is not supported. Rather, the PCIe link
should be quiescent prior to such a change, including reception of all completion for previous requests.

#### 3.1.2.2 Transaction Types Initiated by the X550

Table 3-2.       Transaction Types Initiated by the Transaction Layer
                Transaction Type                           Payload Size                        FC Type

 Configuration Read Request Completion                        DWord                          CPLH + CPLD

 Configuration Write Request Completion                          -                              CPLH

 IO Read Request Completion                                   DWord                          CPLH + CPLD

 IO Write Request Completion                                     -                              CPLH

 Read Request Completion                                   DWord/QWord                       CPLH + CPLD

 Memory Read Request                                             -                              NPH

 Memory Write Request                                 <= MAX_PAYLOAD_SIZE                      PH + PD

 Message                                                     64 bytes1                           PH

1. MCTP messages contain payload.

68                                                                                                         333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Configuration values:
 • Max Payload Size — The value of the Max Payload Size Supported field in the Device Capabilities
   Register is loaded from NVM.
     — Hardware default is 512.
     — System software then programs the actual value into the Max Payload Size field of the Device
       Control Register.
          • Non-ARI mode: If not all functions are programmed with the same value, the max payload
            size used for all functions is the minimum value programmed among all functions.
          • ARI mode: Max_Payload_Size is determined solely by the setting in Function 0.
 • Max Read Request Size — The X550 supports read requests of up to 2 KB.
     — The actual maximum size of a read request is defined as the minimum {2 KB, Max Read
       Request Size field in the Device Control Register}.
The number of outstanding memory read requests is bounded by the following:
 • The total number of outstanding requests is not more than 32 requests. These are shared by all
   sources for memory reads.

3.1.2.2.1              Data Alignment

Requests must never specify an address/length combination that causes a memory space access to
cross a 4 KB boundary. The X550 therefore breaks requests into 4 KB-aligned requests (if needed). This
does not place any requirement on software. However, if software allocates a buffer across a 4 KB
boundary, hardware issues multiple requests for the buffer. Software should consider aligning buffers to
a 4 KB boundary in cases where it improves performance. The maximum size of a read request is
defined as the minimum {2 KB bytes, Max_Read_Request_Size}
The general rules for packet alignment are as follows. Note that these apply to all the X550 requests
(read/write):
 • The length of a single request does not exceed the PCIe limit of MAX_PAYLOAD_SIZE for write and
   MAX_READ_REQ for read.
 • The length of a single request does not exceed the X550 internal limitations.
 • A single request does not span across different memory pages as noted by the 4 KB boundary
   alignment previously mentioned.
If a request can be sent as a single PCIe packet and still meet the general rules for packet alignment, it
is not broken at the cache line boundary but rather sent as a single packet. However, if any of the three
general rules require that the request is broken into two or more packets, the request is broken at the
cache line boundary.
For requests with data payload, if the payload size is larger than (MAX_PAYLOAD_SIZE -
CACHELINE_SIZE), the request is broken into multiple TLPs staring at the first cache line boundary
following the (MAX_PAYLOAD_SIZE - CACHELINE_SIZE) bytes. For example, if MAX_PAYLOAD_SIZE =
256 bytes and CACHELINE_SIZE = 64 bytes, a 1 KB request starting at address 0x...10 is broken into
TLPs such that the first TLP contains 240 bytes of payload (since 240B + 10h = 256B is on cache line
boundary).
The system cache line size is controlled by the PCI_CNF2.CACHELINE_SIZE bit, loaded from the NVM.
Note that the Cache Line Size Register in the PCI configuration space is not related to the
PCI_CNF2.CACHELINE_SIZE and is solely for software use.

333369-009                                                                                              69
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                             Interconnects

#### 3.1.2.3 Messages

3.1.2.3.1              Received Messages

Message packets are special packets that carry a message code. The upstream device transmits special
messages to the X550 by using this mechanism. The transaction layer decodes the message code and
responds to the message accordingly.

Table 3-3.     Supported Messages in the X550 — as a Receiver
  Message
                  Routing r2r1r0                          Message                              X550 Later Response
 Code [7:0]

0x14          100b                       PM_Active_State_NAK                        Accepted

0x19          011b                       PME_Turn_Off                               Accepted

0x40, 0x41,   100b                       Ignored messages (used to be hot-plug      Silently drop
0x43, 0x44,                              messages)
0x45, 0x47,
0x48

0x50          100b                       Slot power limit support (has one DWord    Silently drop.
                                         data)

0x7E          000b, 010b, 011b, 100b     Vendor defined type 0                      Drop and handle as an Unsupported
                                                                                    request.

0x7F          100b                       Vendor defined type 1                      Silently drop.

0x7F          010b, 011b, 000b           Vendor defined type 1                      Send to MCTP reassembly if Vendor ID =
                                                                                    0x1AB4 (DMTF) and VDM code = 0000b
                                                                                    (MCTP). Otherwise, silently drop.

0x00          011b                       Unlock                                     Silently drop.

3.1.2.3.2              Transmitted Messages

The transaction layer is also responsible for transmitting specific messages to report internal/external
events (such as interrupts and PMEs).

Table 3-4.     Supported Messages in the X550 — as a Transmitter
  Message
                 Routing r2r1r0                                             Message
 Code [7:0]

0x20          100b                     Assert INT A

0x21          100b                     Assert INT B

0x22          100b                     Assert INT C

0x23          100b                     Assert INT D

0x24          100b                     De- Assert INT A

0x25          100b                     De- Assert INT B

0x26          100b                     De- Assert INT C

0x27          100b                     De- Assert INT D

0x30          000b                     ERR_COR

0x31          000b                     ERR_NONFATAL

0x33          000b                     ERR_FATAL

0x18          000b                     PM_PME

70                                                                                                              333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-4.          Supported Messages in the X550 — as a Transmitter [continued]
  Message
                     Routing r2r1r0                                                Message
 Code [7:0]

 0x1B           101b                        PME_TO_Ack

 0x10           100b                        LTR

 0x7F           000b, 010b, 011b            VDM

3.1.2.3.3                 Vendor Defined Messages (VDM)

The following vendor defined messages are supported:
 • DMTF MCTP

3.1.2.3.3.1                 MCTP VDMs

MCTP VDMs are supported as both master and target. The following header fields are involved (see
Figure 3-5):
 • Fmt — Set to 11b to indicate 4 DWord header with data.
 • Type
        — [4:3] Set to 10b to indicate a message.
        — [2:0] Routing r2r1r0 = 000b, 010b or 011b.
 • Traffic Class — Set to 000b.
 • TLP Digest — Set to 0b (no ECRC) or 1 (ECRC) according to the PCI_CAPSUP.ECRC_MCTP_GEN bit.
 • Error Present - Set to 0.
 • Attributes[1:0] — Set to 01 (no snoop).
 • Tag field — Indicates this is an MCTP packet and the size of padding to DWord alignment added.
 • Message code = 0x7F (Type 1 VDM).
 • Destination ID — captures the target B/D/F for Route by ID. Otherwise, reserved.
 • Vendor ID = 0x1AB4 (DMTF).

Table 3-5.          MCTP Over PCIe Header Format
 FMT         Type                R    TC          R   A    R   T   T   E   Attr     AT       Length
 011         10r2r1r01                000             tt       H   D   P   [1:0]    00       00_000x_xxxx
                                                      r2       2   2   2   2

 PCI Requester ID                                                  PCI Tag Field                   Message Code
                                                                                                   Vendor Defined = 0111_1111b
                                                                   R       Pad      MCTP VDM
                                                                           Len      code - 0000b

 PCI Target ID (For Route by ID messages,                          Vendor ID = 0x1AB4 (DMTF)
 otherwise = Reserved)

1. r2r1r0 =
   000b: Route to Root Complex
   010b: Route by ID
   011b: Broadcast from Root Complex
2. TD = 0, EP = 0, IC = 0,TH = 0, Attr[2:0] = 0 for sent packets and is ignored for received packets.

333369-009                                                                                                                   71
                                      Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

#### 3.1.2.4 Transaction Attributes

3.1.2.4.1            Traffic Class (TC) and Virtual Channels (VC)

The X550 only supports TC = 0 and VC = 0 (default).

3.1.2.4.2            TLP Processing Hints (TPH)

The X550 supports the TPH capability defined in the PCI Express specification. It does not support
Extended TPH requests.
Existence of a TLP Processing Hint (TPH) is indicated on the PCIe link by setting the TH bit in the TLP
header. Using the PCIe TLP Steering Tag (ST) and Processing Hints (PH) fields, The X550 can provide
hints to the root complex about the destination (socket ID) and about data access patterns (locality in
Cache) when executing DMA memory writes or read operations.
The X550 exposes a PCIe TPH capability structure (See Section 9.2.4.5) with no steering table.
See Section 7.5 for details on the usage of TPH.

#### 3.1.2.5 Ordering Rules

The X550 meets the PCIe ordering rules by following the PCI simple device model:
1. Deadlock Avoidance — The X550 meets the PCIe ordering rules that prevent deadlocks:
     a. Posted writes overtake stalled read requests. This applies to both target and master directions.
        For example, if master read requests are stalled due to lack of credits, master posted writes are
        allowed to proceed. On the target side, it is acceptable to timeout on stalled read requests to
        allow later posted writes to proceed.
     b. Target posted writes overtake stalled target configuration writes.
     c. Completions overtake stalled read requests. This applies to both target and master directions.
        For example, if master read requests are stalled due to lack of credits, completions generated
        by the X550 are allowed to proceed.
2. Descriptor/Data Ordering — The X550 ensures that a Rx descriptor is written back on PCIe only
   after the data that the descriptor relates to is written to the PCIe link.MSI and MSI-X Ordering
   Rules. System software might change the MSI or MSI-X tables during run-time. Software expects
   that interrupt messages issued after the table has been updated are using the updated contents of
   the tables.
     a. Since software does not know when the tables are actually updated in the X550, a common
        scheme is to issue a read request to the MSI or MSI-X table (a PCI configuration read for MSI
        and a memory read for MSI-X). Software expects that any message issued following the
        completion of the read request, is using the updated contents of the tables.
     b. Once an MSI or MSI-X message is issued using the updated contents of the interrupt tables, any
        consecutive MSI or MSI-X message does not use the contents of the tables prior to the change.
3. The X550 meets the rules relating to independence between target and master accesses:
     a. The acceptance of a target posted request does not depend upon the transmission of any TLP.
     b. The acceptance of a target non-posted request does not depend upon the transmission of a
        non-posted request.
     c. Accepting a completion does not depend upon the transmission of any TLP.

72                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

3.1.2.5.1                Relaxed Ordering

The X550 takes advantage of the relaxed ordering rules in PCIe. By setting the relaxed ordering bit in
the packet header, the X550 enables the system to optimize performance in the following cases:
1. Relaxed ordering for descriptor and data reads — When the X550 masters a read transaction, its
   split completion has no ordering relationship with the writes from the CPUs (same direction). It
   should be allowed to bypass the writes from the CPUs.
2. Relaxed ordering for receiving data writes — When the X550 masters receive data writes, it also
   enables them to bypass each other in the path to system memory because software does not
   process this data until their associated descriptor writes are done.
3. The X550 cannot relax ordering for receive descriptor writes or an MSI write.
Relaxed ordering is enabled in the X550 by clearing the CTRL_EXT.RO_DIS bit. Relaxed ordering is
further controlled through the Enable Relaxed Ordering bit in the PCIe Device Control Register
(Section 9.2.3.6.5).

3.1.2.5.2                ID-Based Ordering (IDO)

ID-based ordering was introduced in the PCIe rev. 2.1 specification. When enabled, the X550 sets IDO
in all applicable TLPs defined in the PCIe specification.
This capability allows a supporting root complex to relax ordering rules for TLPs sent by different
requesters.
IDO is enabled when all of the following conditions are met:
 • The NVM PCI_CAPSUP.IDO Enable bit is set (Section 6.2.6.12 and Section 8.2.2.5.11).
 • The PCIe IDO Request Enable bit (for requests) or the IDO Completion Enable bit (for completions)
   in Device Control 2 Register is set (Section 9.2.3.6.11).

#### 3.1.2.6 Flow Control

3.1.2.6.1                Flow Control Rules

The X550 only implements the default Virtual Channel (VC0). A single set of credits is maintained for
VC0.

Table 3-6.      Flow Control Credits Allocation
             Credit Type                         Operations                       Number of Credits (Dual Port)

Posted Request Header (PH)          Target write                           16 credit units to support tail write at wire
                                    Message (one unit)                     speed.

Posted Request Data (PD)            Target Write (Length/16 bytes = one)   max{MAX_PAYLOAD_SIZE/16, 32}.
                                    Message (one unit)

Non-Posted Request Header (NPH)     Target read (one unit)                 Four credit units (to enable concurrent target
                                    Configuration read (one unit)          accesses to both LAN ports).
                                    Configuration write (one unit)

Non-Posted Request Data (NPD)       Configuration write (one unit)         Four credit units.

Completion Header (CPLH)            Read completion (N/A)                  Infinite (accepted immediately).

Completion Data (CPLD)              Read completion (N/A)                  Infinite (accepted immediately).

333369-009                                                                                                                  73
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

Rules for FC updates:
 • UpdateFC packets are sent immediately when a resource becomes available.
 • The X550 follows the PCIe recommendations for frequency of UpdateFC FCPs.
 • Specific rules apply in L0 or L0s link states. See PCIe specification.

3.1.2.6.2            Flow Control Timeout Mechanism

The X550 implements the optional flow control update timeout mechanism. See the PCIe specification.

#### 3.1.2.7 End-to-End CRC (ECRC)

The X550 supports ECRC as defined in the PCIe specification. The following functionality is provided:
 • Inserting ECRC in all transmitted TLPs:
     — The X550 indicates support for inserting ECRC in the ECRC Generation Capable bit of the PCIe
       configuration registers. This bit is loaded from the ECRC Generation NVM bit.
     — Inserting ECRC is enabled by the ECRC Generation Enable bit of the PCIe configuration
       registers. VFs follow the behavior of their PF.
         • ECRC is not added to MCTP messages (per MCTP specification) unless the
           PCI_CAPSUP.ECRC_MCTP_GEN bit is set.
 • ECRC is checked on all incoming TLPs. A packet received with an ECRC error is dropped. Note that
   for completions, a completion timeout occurs later (if enabled).
     — The X550 indicates support for ECRC checking in the ECRC Check Capable bit of the PCIe
       configuration registers. This bit is loaded from the ECRC Check NVM bit.
     — Checking of ECRC is enabled by the ECRC Check Enable bit of the PCIe configuration registers.
       ECRC checking is done if enabled by at least one physical function (enablement is not done via
       VFs).
 • ECRC errors are reported on all physical functions (PFs) enabled for ECRC checking.
 • System software can configure ECRC independently per each physical function.

### 3.1.3 Link Layer

#### 3.1.3.1 ACK/NAK Scheme

The X550 supports two alternative schemes for ACK/NAK rate:
 • NAKs are sent as soon as identified.
 • ACKs are sent per Section 3.5.3.1 (Table 3-7, Table 3-8, and Table 3-9) in the PCIe Base
   Specification.

74                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

#### 3.1.3.2 Supported DLLPs

The following DLLPs are supported by the X550 as a receiver:
 • ACK
 • NAK
 • PM_Request_Ack
 • InitFC1-P
 • InitFC1-NP
 • InitFC1-Cpl
 • InitFC2-P
 • InitFC2-NP
 • InitFC2-Cpl
 • UpdateFC-P
 • UpdateFC-NP
 • UpdateFC-Cpl
The following DLLPs are supported by the X550 as a transmitter:
 • ACK
 • NAK
 • PM_Enter_L1
 • PM_Enter_L23
 • InitFC1-P
 • InitFC1-NP
 • InitFC1-Cpl
 • InitFC2-P
 • InitFC2-NP
 • InitFC2-Cpl
 • UpdateFC-P
 • UpdateFC-NP
Note:        UpdateFC-Cpl is not sent because of the infinite FC-Cpl allocation.

#### 3.1.3.3 Transmit End Data Bit (EDB) Nullifying — End Bad

A TLP may be signaled as EDB or poisoned if during its transmission from the device, an internal
memory error is detected that may corrupt the TLP payload.

333369-009                                                                                         75
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

### 3.1.4 Physical Layer

#### 3.1.4.1 Link Speed

The X550 supports PCIe 2.1 and PCIe 3.0.
The following configuration controls link speed:
 • PCIe Supported Link Speeds bit — Indicates the link speeds supported by the X550.
 • PCIe Current Link Speed bit — Indicates the negotiated link speed.
 • PCIe Target Link Speed bit — used to set the target compliance mode speed when software is
   using the Enter Compliance bit to force a link into compliance mode. The default value is loaded
   from the highest link speed supported defined by the above Supported Link Speeds.
The X550 does not initiate a hardware autonomous speed change.
The X550 supports entering compliance mode at the speed indicated in the Target Link Speed field in
the PCIe Link Control 2 register (Section 9.2.3.6.13). Compliance mode functionality is controlled via
the PCIe Link Control 2 register.

#### 3.1.4.2 Link Width

The X550 supports a maximum link width of x8, x4, or x1.The maximum link width is loaded into the
Max Link Width field of the PCIe Capability register (LCAP[11:6]). Hardware default is the x4 link for the
X550-AT2, and x8 link for the X550-BT2.
During link configuration, the platform and the X550 negotiate on a common link width. The link width
must be one of the supported PCIe link widths (x1, x4, x8), such that:
 • If Maximum Link Width = x8, the X550 negotiates to either x8, x4 or x1.
 • If Maximum Link Width = x4, the X550 negotiates to either x4 or x1
 • If Maximum Link Width = x1, the X550 only negotiates to x1
When negotiating for x4, or x1 link, the X550 may negotiate the link to reside starting from physical
lane 0 or starting from physical lane 4.
The X550 does not initiate a hardware autonomous link width change.
When operating in x8 link width the X550 does not support Gen3 link speed (8GT/s).
The x8 link width is available only in the X550-BT2.

#### 3.1.4.3 Lane Configurations

The X550 supports lane reversal and degraded modes.
The following general rules determine how the device reacts in different cases of lanes configuration:
 • If lane 0 is found valid, the X550 does not initiate lane reversal. The link partner (LP) may initiate
   lane reversal (to end up with an optimal lane width) and the X550 consents with the lane reversal.
 • If lane 0 is found invalid, the X550 initiates lane reversal. Lane reversal succeeds if the link partner
   supports link reversal.
 • If the lanes at both ends of the port (i.e. lanes 0 & 7 for x8, lanes 0 & 3 for x4, lane 0 for x1) are
   invalid, a link is not established.

76                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Note:        Some of the configurations or transitions assume lane reversal is done by the link partner. If
             the link partner does not support a specific transition, the respective configuration is not
             provided on that system.
Figure 3-1, Figure 3-2, and Figure 3-3 depict the initial link width configuration and link degradation
options. In Figure 3-1 and Figure 3-2, the upper part of the Figure describes link options where the Link
Partner (LP) and the X550 (NIC) are aligned. The bottom part of the Figure describes link options where
the Link Partner and the X550 are reversed in order.
 • Figure 3-1 applies when either the Link partner or the X550 is physically set to x8.
 • Figure 3-2 applies when either the Link partner or the X550 is physically set to x4 and both are not
   physically set x8.
 • Figure 3-3 applies when both the Link partner or the X550 is physically set to x1.

333369-009                                                                                               77
                                 Did this document help answer your questions?

                                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                                            Interconnects

                  Initial Configuration
               LP 0 1 2 3 4 5 6 7
              NIC 0 1 2 3 4 5 6 7

                                                                                                                          Degradation:
                  Case 1: all lanes valid
                           LP     0         1     2       3        4       5       6       7
                          NIC     0         1     2       3        4       5       6       7

                  Case 2: at least 1 of physical Lanes 4‐7 is defect
                           LP     0       1        2      3        4       5       6       7
                          NIC     0       1        2      3        4       5       6       7

                  Case 3: (At least 1 of physical Lanes 1‐3 is defect and LP doesn’t initiate lane reversal) or (At least 1 of
                  physical Lanes 1‐3 is defect and at least 1 of physical Lanes 4‐7 is defect)
                           LP     0       1        2      3        4       5      6        7
                          NIC     0       1        2      3        4       5      6        7

                  Case 4: (At least 1 of physical Lanes 1‐3 is defect and LP initiates lane reversal) or (Physical lane 0 is
                  defect and physical lanes 4‐7 are valid)
                           LP    7        6       5       4       3       2        1       0
                          NIC    0        1       2       3       4       5        6       7

                  Case 5: Physical lane 0 is defect and at least one of physical lanes 4‐6 are defect
                           LP    7        6       5       4       3       2        1       0
                          NIC    0        1       2       3       4       5        6       7

                  Initial Configuration
               LP 7 6 5 4 3 2 1 0
              NIC 0 1 2 3 4 5 6 7

                                                                                                                          Degradation:
                  Case 1: all lanes valid
                           LP     7         6     5       4        3       2       1       0
                          NIC     0         1     2       3        4       5       6       7

                  Case 2: at least one of physical Lanes 0‐3 is defect
                           LP     7       6       5       4       3        2       1       0
                          NIC     0       1       2       3       4        5       6       7

                  Case 3: (At least 1 of physical Lanes 4‐6 is defect and LP doesn’t initiate lane reversal) or (At least 1 of
                  physical Lanes 4‐6 is defect and at least 1 of physical Lanes 0‐3 is defect)
                           LP     7       6        5      4        3       2      1        0
                          NIC     0       1        2      3        4       5      6        7

                  Case 4: (At least 1 of physical Lanes 4‐6 is defect and LP initiates lane reversal) or (Physical lane 7 is
                  defect and physical lanes 0‐3 are valid)
                           LP    0        1       2       3       4       5        6       7
                          NIC    0        1       2       3       4       5        6       7

                  Case 5: Physical lane 7 is defect and at least one of physical lanes 1‐3 are defect
                           LP    0        1       2       3       4       5        6       7
                          NIC    0        1       2       3       4       5        6       7

Figure 3-1.    Link Width Configurations for a x8 Port

78                                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

                    Initial Configuration
                 LP 0 1 2 3
                NIC 0 1 2 3

                                                                                  Degradation:
                     Case 1: all lanes valid
                              LP 0 1 2 3
                             NIC 0 1 2 3

                     Case 2: at least 1 of physical Lanes 1‐3 is defect
                              LP 0 1 2 3
                             NIC 0 1 2 3

                     Case 3: Physical lane 0 is defect
                              LP 3 2 1 0
                             NIC 0 1 2 3

                    Initial Configuration
                 LP 3 2 1 0
                NIC 0 1 2 3

                                                                                  Degradation:
                     Case 1: all lanes valid
                              LP 3 2 1 0
                             NIC 0 1 2 3

                     Case 2: at least one of physical Lanes 0‐2 is defect
                              LP 3 2 1 0
                             NIC 0 1 2 3

                     Case 3: Physical lane 3 is defect
                              LP 0 1 2 3
                             NIC 0 1 2 3

Figure 3-2.    Link Width Configurations for a x4 Port

333369-009                                                                                       79
                                  Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                  Interconnects

                        Initial Configuration
                     LP 0
                    NIC 0

                        Case 1: all lanes valid
                                 LP 0
                                NIC 0

Figure 3-3.   Link Width Configurations for a x1 Port

#### 3.1.4.4 Receiver Framing Requirements

This section applies to Gen3 operation only and lists the optional capabilities defined in Section
4.2.2.3.3 (Receiver Framing Requirements) of the PCIe base specification.
The device implements the optional Gen3 receiver framing error checks other than:
 • TLP Token length=0
 • Mixed order sets across lanes

### 3.1.5 Error Events and Error Reporting

#### 3.1.5.1 General Description

PCIe defines three error reporting paradigms: the baseline capability, the Advanced Error Reporting
(AER) capability, and a proprietary mechanism. The baseline error reporting capabilities are required of
all PCIe devices and define the minimum error reporting requirements. The AER capability is defined for
more robust error reporting and is implemented with a specific PCIe capability structure. Both
mechanisms are supported by the X550. The proprietary error reporting mechanism used for error
better handled by the software device driver using internal CSRs is described in Section 3.1.5.8.
The SERR# Enable and the Parity Error bits from the Legacy Command register also take part in the
error reporting and logging mechanism.
In a multi-function device, PCIe errors that are not related to any specific function within the device are
logged in the corresponding status and logging registers of all functions in that device. Figure 3-4
shows, in detail, the flow of error reporting in the X550.

80                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

                                                         Error Sources
                                                      (Associated with Port)

                                                                                                                               Device Status ::
                                                        Uncorrectable Error Severity

                                                                                         Status Reporting - Not Gated
                                                                                                                          Correctable Error Detected              Status ::
                                                                                                                                                            Signaled Target Abort
                                                      Uncorrectable Error Status                                             Device Status ::
                               Correctable Error Status                                                                  Non-Fatal Error Detected                Status ::
                                                                                                                            Device Status ::               Received Target Abort
                                                                                                                          Fatal Error Detected                   Status ::
                                                                                                                                                           Received Master Abort
                                                                                                                              Device Status ::
                             Correctable Error Mask         Uncorrectable Error Mask                                    Unsupported Request Detected             Status ::
                                                                                                                                                           Detected Parity Error

                          Device Control ::
                                                                                                                                                 Root Error Status
        Correctable Error Reporting Enable
                              Device Control ::
        Unsupported Request Reporting Enable
                          Device Control ::                                                                                                               Report Error Command ::
          Non-Fatal Error Reporting Enable                                                                                                       Correctable Error Reporting Enable
                           Device Control ::                                                                                                               Report Error Command ::         Interrupt
               Fatal Error Reporting Enable                                                                                                         Non-Fatal Error Reporting Enable

                                                                                                                                                           Report Error Command ::
                                                                                                                                                        Fatal Error Reporting Enable
                                   Command::
                                 SERR# Enable

                                      Command::                                                      Status::                                                                      Status::
                           Parity Error Response                                                     Master Data Parity Error                                                      Signaled System Error
                                               Bridge Control::
                                                                                                                                                             Root Control::
                                                SERR Enable
                                                                                                                                   System Error on Correctable Error Enable

  Rcv                                                                                                                                                        Root Control::
  Msg               Error Message
                                                                                                                                     System Error on Non-Fatal Error Enable                      System
                     Processing                                                                                                                               Root Control::                      Error
                                                                                                                                          System Error on Fatal Error Enable

                                                                                                                                                                     Secondary Status::
                                                                                                                                                                     Received System Error
                                                                                       Secondary Status::                                                            Either Implementation
                                                                                       Detected Parity Error                                                         Acceptable – the unqualified
                                                                                                                                                                     version is more like PCI P2P
                                                                                       Secondary Status::
                                                                                                                                                                     bridge spec
                                                                                       Received Target Abort
                        Secondary Side Error Sources                                   Secondary Status::
                                                                                       Received Target Abort
                                                                                       Secondary Status::
                                                                                                                                         Bridge Control::
                                                                                       Signaled Master Abort                                                                           Secondary Status::
                                                                                                                                         Parity Error Response Enable
                                                                                                                                                                                       Master Data Parity
                                                                                                                                                                                       Error

Figure 3-4.           Error Reporting Mechanism

333369-009                                                                                                                                                                                                  81
                                                      Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                          Interconnects

#### 3.1.5.2 Error Events

Table 3-7 lists the error events identified by the X550 and the response in terms of logging, reporting,
and actions taken. Refer to the PCIe specification for the effect on the PCI Status register.

Table 3-7.         Response and Reporting of PCIe Error Events
     Error Name                   Error Events             Default Severity                       Action

Physical Layer Errors

Receiver Error          •   8b/10b decode errors.        Correctable           TLP to initiate NAK, drop data.
                        •   Packet Framing Error.        Send ERR_CORR         DLLP to drop.

Data Link Errors

Bad TLP                 •   Bad CRC.                     Correctable           TLP to initiate NAK, drop data.
                        •   Illegal EDB.                 Send ERR_CORR
                        •   Wrong sequence number.

Bad DLLP                •   Bad CRC.                     Correctable           DLLP to drop.
                                                         Send ERR_CORR

Replay Timer            •   REPLAY_TIMER expiration.     Correctable           Follow LL rules.
Timeout                                                  Send ERR_CORR

REPLAY NUM              •   REPLAY NUM rollover.         Correctable           Follow LL rules.
Rollover                                                 Send ERR_CORR

Data Link Layer         •   Violations of flow control   Uncorrectable
Protocol Error              initialization protocol.     Send ERR_FATAL

TLP Errors

Poisoned TLP            •   TLP with error forwarding.   Uncorrectable         If completion TLP:
Received                                                 ERR_NONFATAL          Error is non-fatal (default case):
                                                         Log Header             • Send error message if advisory.
                                                                                • Retry the request once and send
                                                                                    advisory error message on each failure.
                                                                                • If fails, send uncorrectable error
                                                                                    message.
                                                                               Error is defined as fatal:
                                                                                • Send uncorrectable error message.

ECRC Check failed       •   Failed ECRC check.           Uncorrectable         Error is non-fatal (default case):
                                                         ERR_NONFATAL           • Send error message if advisory.
                                                         Log Header            Error is defined as fatal:
                                                                                • Send uncorrectable error message.

Unsupported             •   Receipt of TLP with          Uncorrectable         Send completion with UR.
Request (UR)                unsupported request type.    ERR_NONFATAL
                        •   Receipt of an unsupported    Log header
                            vendor defined type 0
                            message.
                        •   Invalid message code.
                        •   Wrong function number.
                        •   Received TLP outside BAR
                            address range.
                        •   Receipt of a Request TLP
                            during D3hot, other than
                            Configuration and Message
                            requests.

Completion Timeout      •   Completion timeout timer     Uncorrectable         Error is non-fatal (default case):
                            expired.                     ERR_NONFATAL           • Send error message if advisory.
                                                                               Error is defined as fatal:
                                                                                • Send uncorrectable error message.

82                                                                                                               333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-7.        Response and Reporting of PCIe Error Events [continued]
    Error Name                  Error Events                    Default Severity                          Action

Completer Abort       •   Received target access with        Uncorrectable.            Send completion with CA.
                          illegal data size per              ERR_NONFATAL
                          Section 3.1.2.1.1.
                                                             Log header

Unexpected            •   Received completion without a      Uncorrectable             Discard TLP.
Completion                request for it (Tag, ID, etc.).    ERR_NONFATAL
                                                             Log Header

Receiver Overflow     •   Received TLP beyond                Uncorrectable             Receiver behavior is undefined.
                          allocated credits.                 ERR_FATAL

Flow Control          •   Minimum initial flow control       Uncorrectable.            Receiver behavior is undefined.
Protocol Error            advertisements.                    ERR_FATAL
                      •   Flow control update for infinite
                          credit advertisement.

Malformed TLP (MP)    •   Data payload exceed                Uncorrectable             Drop the packet, free FC credits.
                          Max_Payload_Size.                  ERR_FATAL
                      •   Received TLP data size does        Log Header
                          not match length field.
                      •   TD field value does not
                          correspond with the observed
                          size.
                      •   PM messages that do not use
                          TC0.
                      •   Usage of unsupported VC.
                      •   Target request crosses a 4KB
                          boundary.

Completion with                                              No Action (already done   Free FC credits.
Unsuccessful                                                 by originator of
Completion Status                                            completion)

#### 3.1.5.3 Completion Timeout Mechanism

The X550 supports completion timeout as defined in the PCIe specification.
The X550 controls the following aspects of completion timeout:
 • Disabling or enabling completion timeout.
     — The PCIe Completion Timeout Disable Supported bit in the Device Capabilities 2 Register
       (Section 9.2.3.6.10) is hardwired to 1b to indicate that disabling completion timeout is
       supported
     — The PCIe Completion Timeout Disable bit in Device Control 2 Register controls whether
       completion timeout is enabled
 • A programmable range of timeout values.
     — The X550 supports all four ranges as programmed in the Completion Timeout Ranges
       Supported field of the Device Capabilities 2 Register. The actual completion timeout value is
       written in the Completion Timeout Value field of Device Control 2 Register (Section 9.2.3.6.10)
The following sequence takes place when completion timeout is detected:
 • The appropriate message is sent on PCIe as described in Table 3-7.
 • The affected queue or client takes action based on the nature of the original request.
 • An interrupt is issued to the respective PF.

333369-009                                                                                                                 83
                                     Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

#### 3.1.5.4 Error Forwarding (TLP Poisoning)

If a TLP is received with an error-forwarding trailer, the packet is dropped and is not delivered to its
destination. The X550 then reacts as listed in Table 3-7.
The following sequence takes place when a poisoned TLP is received:
 • The appropriate message is sent on PCIe as described in Table 3-7.
 • An interrupt is issued.
 • If the TLP is a completion, a completion timeout follows at some later time. Processing continues as
   described in Section 3.1.5.3.
System logic is expected to trigger a system-level interrupt to signal the operating system of the
problem. Operating systems can then stop the process associated with the transaction, re-allocate
memory to a different area instead of the faulty area, etc.

#### 3.1.5.5 Completion with Unsuccessful Completion Status

A completion arriving with unsuccessful completion status (either UR or CA) is dropped and not
delivered to its destination. A completion timeout follows at some later time. Processing continues as
described in Section 3.1.5.3.

#### 3.1.5.6 Error Pollution

Error pollution can occur if error conditions for a given transaction are not isolated to the error's first
occurrence. If the PHY detects and reports a receiver error, to avoid having this error propagate and
cause subsequent errors at the upper layers, the same packet is not signaled at the data link or
transaction layers. Similarly, when the data link layer detects an error, subsequent errors that occur for
the same packet are not signaled at the transaction layer.

#### 3.1.5.7 Blocking on Upper Address

The PCI_UPADD register blocks master accesses from being sent out on PCIe if the TLP address
exceeds some upper limit. Bits [31:1] correspond to bits [63:33] in the PCIe address space,
respectively.
When a bit is set in GLPCI_UPADD[31:1], any transaction in which the corresponding bit in its address
is set, is blocked and not sent over PCIe. If all register bits are cleared, there is no effect (in other
words, no TLPs are blocked by this mechanism).
The PCI_UPADD register is loaded from NVM with a value allowing all addresses to pass. The software
device driver should override this value with a system dependent value.
Processing a blocked transaction:
 • Write transaction
     — The transaction is dropped.
     — Set the “Exceeded upper address limit (write requests)” event in the PCIe errors register (see
       Section 3.1.5.8).
     — An interrupt is issued as described in Section 3.1.5.8.

84                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

 • Read transaction
     — The transaction is dropped.
     — Set the “Exceeded upper address limit (read requests)” event in the PCIe errors register (see
       Section 3.1.5.8).
     — The originating internal client is notified.
     — The affected queue or client takes action based on the nature of the original request. An
       interrupt is issued to the respective PF.

#### 3.1.5.8 Proprietary Error Reporting

The PCIe specification defines how to report errors to system software. There are, however, error
events that the device driver should be aware of or that the device driver is in better position to handle
and recover from. This section describes the mechanism to report PCIe related errors to device drivers.
Several CSRs are dedicated to this functionality, with a separate bit allocated per error type (see
Table 3-8):
 • The “PCIe Errors Reported” register (PCI_PCIERR - RO) indicates which errors are reported using
   this mechanism. It is shared by all PFs. It is loaded from NVM. All non-reserved errors are enabled.
 • The “PCIe Interrupt Cause” register (PCI_ICAUSE - RW1C) indicates pending errors for errors set in
   the PCIe Errors Reported register. It is dedicated per PF.
 • The “PCIe Interrupt Enable” register (PCI_IENA - RW) determines if an interrupt should be issued to
   the respective PCI function on an error event. It is dedicated per PF.
Reporting an error to the PF driver involves the following steps:
 • The device checks if the respective bit is set in the PCIe Errors Reported register. If cleared, done.
   Else, continue
 • The respective bit is set in the “PCIe Interrupt Cause” register
 • If the respective bit is set in the “PCIe Interrupt Enable” register, an interrupt is issued to the PCI
   function. The PCI_EXCEPTION cause is used (see the EICR register - Section 8.2.2.6.1).

Table 3-8.      PCIe Errors Reported to Device Software
      Error Event         Index               Description and Comments                     Function Association

Exceeded upper address      00     See Section 3.1.5.7                               Sent to PF
limit (read requests)

Exceeded upper address      01     See Section 3.1.5.7                               Sent to PF
limit (write requests)

Reserved                    02     Reserved entries                                  N/A

Poisoned TLP received       03     See Section 3.1.5.4                               Sent to PF

Reserved                   04-05   Reserved entries                                  N/A

ECRC error detected         06     ECRC check failed on a received TLP. See          Sent to all PFs
                                   Section 3.1.5.7

Unsupported Request -       07     Request causes an Unsupported Request due to      Sent to PF
Request Type                       receipt of TLP with unsupported Request Type

Unsupported Request -       08     Request causes an Unsupported Request due to      Sent to PF unless r[2:0] =
Vendor Message                     receipt of an Unsupported Vendor Defined Type 0   Broadcast from Root Complex, in
                                   Message                                           which case sent to all PFs

333369-009                                                                                                             85
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               Interconnects

Table 3-8.       PCIe Errors Reported to Device Software [continued]
      Error Event          Index                 Description and Comments                         Function Association

Unsupported Request -        09      Request causes an Unsupported Request due to           Sent to PF
Message Code                         receipt of an invalid Message Code

Unsupported Request -        10      Request causes an Unsupported Request due to           Sent to all PFs
Function Number                      receipt of a not-supported Function Number

Unsupported Request -        11      Request causes an Unsupported Request due to           Sent to PF
Address Range                        receipt of a not-supported Address Range

Unsupported Request -        12      Request causes an Unsupported Request due to           Sent to PF
D3hot                                receipt of a Request TLP during D3hot, other than
                                     Configuration and Message requests

Completer abort - target     13      Received Target Access with illegal data size per      Sent to PF
size                                 Section 3.1.2.1.1 (CA)

Reserved                   14 - 31   Reserved entries                                       N/A

### 3.1.6 Performance and Statistics Counters

The X550 incorporates counters to track the behavior and performance of the PCIe interconnect. The
X550 implements several types of counters:
 • Transaction layer event counters — Section 3.1.6.1
 • Link and Physical layer event counters — Section 3.1.6.2
 • Bandwidth counters — Section 3.1.6.3
 • Latency counters — Section 3.1.6.4
General characteristics of the counters:
 • Software can reset, stop, or start the counters.
 • The counters are shared by all PCI functions (“Service” mode of sharing).
Part of the registers that manage the operation of the performance counters are accessed via the
PCI_LCBADD and PCI_LCBDATA register pair.
Reading a register via the PCI_LCBADD/PCI_LCBDATA pair is done as follows:
 • Write the following values into the PCI_LCBADD register.
     — ADDRESS — The 18-bit register address. See below for the specific address per each register.
     — BLOCK_ID — Defines the sub-unit where the register resides. Use the value 0x7F to access
       registers mentioned in this section.
     — LOCK — Use if need to gain access in case of multiple agents accessing the PCI_LCBADD/
       PCI_LCBDATA registers.
 • Read the PCI_LCBDATA register.
     Note:      Although PCI_LCBDATA is a 32-bit register, the registers that maintain the actual count
                are read as atomic 64-bit reads. The PCI_LCBADD contains the address of the low DW,
                and reading PCI_LCBDATA returns a 64-bit value.

86                                                                                                               333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Writing a register via the PCI_LCBADD/PCI_LCBDATA pair is done as follows:
 • Write the following values into the PCI_LCBADD register.
     — ADDRESS — The 18-bit register address. See below for the specific address per each register.
     — BLOCK_ID — Defines the sub-unit where the register resides. For actual values, consult the text
       below.
     — LOCK — Use if need to gain access in case of multiple agents accessing the PCI_LCBADD/
       PCI_LCBDATA registers.
 • Write to the PCI_LCBDATA register.

#### 3.1.6.1 Event Counters - Transaction Layer

Counters operate in one of the following modes:
 • Count Mode — The counter increments when the respective event occurred
 • Leaky Bucket Mode — The counter increments only when the rate of events exceeded a certain
   value. See Section 3.1.6.1.2 for more details.
The list of events supported by the X550 are listed in Table 3-9.

Table 3-9.        PCIe Statistic Events Encoding
                                 Event
             Events             Mapping                                         Description
                                 (Hex)

Cycles                           0x00       Increment on each PCIe clock tick

                                               Transaction Layer Events

Bad Request TLPs                 0x10       Number of bad TLPs arriving to the transaction layer.These include:
                                             • Request caused UR
                                             • Request caused CA
                                             • Malformed TLP

Bad Completions                  0x11       Number of bad Completions received. These include:
                                             • Unexpected Completion
                                             • UR status
                                             • CA status

Completion Timeout               0x12       Number of completion timeout events

Poisoned TLP                     0x13       Number of TLPs received with poisoned data

ECRC Check                       0x14       Number of TLPs that foil ECRC check

                                                   Link Layer Events

Retry Buffer Timeout             0x31       Number of replay events that happen due to timeout (does not count replay
                                            initiated due to NACK)

Retry Buffer Replay Roll-Over    0x32       Increment when a replay is initiated for more than 3 times

                                                 Physical Layer Events

Receive Error                    0x50       Increment when one of the following occurs:
                                            1. Decoder error occurred during training in the PHY. It is reported only when
                                            training ends.
                                            2. Decoder error occurred during link-up or till the end of the current packet (in
                                            case the link failed). This error is masked when entering/exiting EI.

Surprise Link Down               0x51       Increment when link is unpredictably down (Not because of reset or DFT)

333369-009                                                                                                                       87
                                  Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                Interconnects

3.1.6.1.1           Count Mode

The following CSR fields control operation of the Count mode:
 • Four 32-bit counters PCI_GSCN_0_3 track events and increment on each occurrence of an event.
     — The four 32-bit counters can also operate in a two 64-bit mode to count long intervals or large
       payloads.
         • Registers PCI_GSCN_0_3[0] and PCI_GSCN_0_3[1] form the first 64-bit counter. Registers
           PCI_GSCN_0_3[2] and PCI_GSCN_0_3[3] form the second 64-bit counter.
         • The PCI_GSCL_1.GIO_64_BIT_EN selects between 32-bit and 64-bit modes.
 • The PCI_GSCL_1.GIO_COUNT_EN_[3:0] bits enable each of the 4 counters.
     — The enable bits for the two 64-bit counters are PCI_GSCL_1.GIO_COUNT_ EN_0 and
       PCI_GSCL_1.GIO_COUNT_ EN_2, respectively.
 • The PCI_GSCL_1.GIO_COUNT_START bit starts event counting of enabled counters.
 • The PCI_GSCL_1.GIO_COUNT_STOP bit stops event counting of running counters.
 • The PCI_GSCL_1.GIO_COUNT_RESET bit resets the event counters.
 • The PCI_GSCL_2 associates an event with each of the 4 counters.
     — In 64-bit mode, the GIO_EVENT_NUM_[2,0] fields are used.

3.1.6.1.2           Leaky Bucket Mode

Each of the counters can be configured independently to operate in a leaky bucket mode. When in leaky
bucket mode, the following functionality is provided:
 • One of four 16-bit Leaky Bucket Counters (LBC) is enabled via the LBC_ENABLE_[3:0] bits in the
   PCIe Statistic Control register #1.
 • The LBC is controlled by the GIO_COUNT_START, GIO_COUNT_STOP, GIO_COUNT_RESET bits in
   the PCIe Statistic Control register #1.
 • The LBC increments every time the respective event occurs.
 • The LBC is decremented every T s as defined in the LBC_TIMER_N field in the PCIe Statistic
   Control registers #5...#8 (PCI_GSCL_5_8).
 • When an event occurs and the value of the LBC meets or exceeds the threshold defined in the
   LBC_THRESHOLD_N field in the PCIe Statistic Control registers #5...#8 (PCI_GSCL_5_8), the
   respective statistics counter increments, and the LBC counter is cleared to zero.

#### 3.1.6.2 Event Counters - Link and Physical Layers

This section describes the performance events for the Link and Physical layers and how to manage the
counters associated with these events.
Note:    Before using LCB performance counters, the clock gating should be disabled by setting the
         PCIE_CLKGATE_DIS field in the PCI_GLBL_CNF register.
The registers responsible for the Link and Physical layers counters are accessed via the PCI_LCBADD
and PCI_LCBDATA register pair.
Two events can be counted concurrently. The event counters include two sets of registers, each
managing one event counter. Such pairs are documents as <register_name>[1:0].

88                                                                                                333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

The following procedures manage the operation of the event counters (when writing to part of the
register, make sure other fields are written with their existing values):
 • Resetting the counters configuration:
     — Set the XPPERFCON.GRST bit.
     — Clear the XPPERFCON.GRST bit (otherwise the logic stays in reset).
 • Setting an event:
     — Write 0x0...0 to the XPPMCL[1:0] registers
     — Set the XPPMR[1:0].CENS field to 0x1
     — Set the XPPMR[1:0].CNTMD field to 0x1
     — Set the XPPMER[1:0].XPRSCA field to 0x1
     — Set the event according to Table 3-10.
 • Starting a count:
     — Set the XPPERFCON.GCE bit.
 • Stopping a count:
     — Clear the XPPERFCON.GCE bit.
 • Reading the count (note: reading the counter clears their values):
     — Read the respective XPPMDH[1:0] and XPPMDL[1:0] register pair in a single 64-bit aligned
       access.
Table 3-10 defines the Link and Physical Layer events.

Table 3-10. Link and Physical Layer Performance Events
           Event                                        Description                                    Register Field

Uncorrectable Errors         Counts the total number of Uncorrectable Errors.                   XPPMER[1:0].CNTUCERR

Correctable Errors           Counts the total number of Correctable Errors.                     XPPMER[1:0].CNTCERR

Tx L0s state utilization     Counts the number of entries to L0s on the Tx lanes.               XPPMER[1:0].TXL0SU

Rx L0s state utilization     Counts the number of entries to L0s on the Rx lanes.               XPPMER[1:0].RXL0SU

Link Utilization             Counts clocks that a port is receiving data.                       XPPMER[1:0].LNKUTIL
                             If one counter counts receiver errors and another counter counts
                             Link Utilization, a bit error rate can be calculated.

Recovery State Utilization   Counts the number of entries to Recovery state.                    XPPMER[1:0].RECOVERY

ASPM L1 state utilization    Counts the number of entries to ASPM L1 state (i.e. initiated by   XPPMER[1:0].L1
                             the device).

SW L1 state utilization      Counts the number of entries to L1 state initiated by software.    XPPMER[1:0].SWL1

Tx and Rx L0s utilization    Counts number of events where both Tx and Rx are in L0s state.     XPPMER[1:0].RXL0STXL0SU

NAK DLLP received            Counts number of received NAK DLLPs.                               XPPMER[1:0].NAKDLLP

333369-009                                                                                                                89
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               Interconnects

#### 3.1.6.3 Bandwidth Counters

The bandwidth counters measure total payload bytes transferred over the PCIe link. Counting is
provided per each traffic type (posted, non-posted, completions) per direction (upstream,
downstream).
The mechanisms described above hold for the bandwidth counters with the following differences:
 • Setting an event:
       — Set the XPPMR[1:0].CENS field to 0x1.
       — Set the XPPMR[1:0].EGS field to 0x2.
       — Set the XPPMR[1:0].FCCSEL field to the desired traffic type (posted, non-posted, completions,
         or all).
       — Set the XPPPMER[1:0].TXRXSEL field to desired values.
       — Set the XPPPMER[1:0].XPRSCA field to 0x1.
       — Set the XPPERFCON.GCE field to 0x1.
Registers fields used exclusively by the bandwidth counters:
 • XPPMR[1:0].FCCSEL — Selects the desired traffic type (posted, non-posted, completions, or all).
 • XPPMER[1:0].TXRXSEL — Selects between monitoring downstream traffic, upstream traffic, or
   both.

3.1.6.3.1                Register Map

The register fields that control the Link and Physical Layer events are as follows:

Table 3-11. XP PM Compare Low Bits Register (XPPMCL[1:0]) (0x3288, 0x328C)
     Field      Bit(s)      Init.                                            Description

CMPL             31:0     0xFF...F    PM Compare Low Value
                                      Low order bits [31:0] for PM compare register[1:0].

Table 3-12. XP PM Data Low Bits Register (XPPMDL[1:0]) (0x32E8, 0x32F0)
     Field      Bit(s)      Init.                                            Description

CNTL             31:0     0x00...00   PM Data Counter Low Value
                                      Low order bits [31:0] for PM data counter[1:0].

Note:    XPPMDL must be read together with the respective XPPMDH register as a single 64-bit aligned read. The registers are
         simultaneously cleared on read.

Table 3-13. XP PM Data High Bits Register (XPPMDH[1:0]) (0x32EC, 0x32F4)
     Field      Bit(s)      Init.                                            Description

CNTH             3:0        0x0       PM Data Counter High Value
                                      High order bits [35:32] for PM data counter[1:0].

RSVD             31:4      0x0...0    Reserved.

Note:    XPPMDH must be read together with the respective XPPMDL register as a single 64-bit aligned read. The registers are
         simultaneously cleared on read.

90                                                                                                                   333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-14. XP PM Response Control Register (XPPMR[1:0]) (0x3294, 0x3298)
     Field    Bit(s)     Init.                                              Description

RSVD           10:0      0x0      Reserved.

CENS           13:11     00b      Counter Enable Source

CNTMD          15:14     00b      Count Mode

EGS            20:19     00b      Event Group Selection

RSVD           31:21     0x0      Reserved.

Table 3-15. XP PM Resource Events Register (XPPMER[1:0]) (0x32AC, 0x32B0)
      Field     Bit(s)    Init.                                              Description

TXRXSEL          1:0       00b     Tx/Rx Select
                                   This field selects the traffic direction to monitor:
                                    1xb = Transmit
                                    x1b = Receive (from PCIe bus)
                                    11b = Either Transmit or Receive direction.

FCCSEL           4:2      000b     Flow Control Class Select
                                   This field selects which flow class for resource event
                                    xx1b = Posted
                                    x1xb = Non-Posted
                                    1xxb = Completion
                                   Note: Setting to 111b counts posted, non-posted, and completion traffic combined.

RSVD            12:5       0x0     Reserved.

LNKUTIL         16:13      0x0     Link Utilization
                                   Set to 0x1 to enable.

XPRSCA          20:17      0x0     XP Resource Assignment
                                    0001b = Set
                                    All other values are reserved.

RXL0SU           21        0b      Rx L0s State Utilization Event
                                    0b = Disabled
                                    1b = Enabled

TXL0SU           22        0b      Tx L0s State Utilization Event
                                    0b = Disabled
                                    1b = Enabled

CNTCERR          23        0b      Count Correctable Errors
                                    0b = Disabled
                                    1b = Enabled

CNTUCERR         24        0b      Count Uncorrectable Errors
                                    0b = Disabled
                                    1b = Enabled

RECOVERY         25        0b      Recovery State Utilization
                                    0b = Disabled
                                    1b = Enabled

L1               26        0b      ASPM L1 State Utilization
                                    0b = Disabled
                                    1b = Enabled

SWL1             27        0b      SW L1 State Utilization
                                    0b = Disabled
                                    1b = Enabled

333369-009                                                                                                             91
                                  Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                   Interconnects

Table 3-15. XP PM Resource Events Register (XPPMER[1:0]) (0x32AC, 0x32B0) [continued]
      Field       Bit(s)       Init.                                             Description

RXL0STXL0SU         28          0b        Tx and Rx L0s Utilization
                                           0b = Disabled
                                           1b = Enabled

NAKDLLP             29          0b        NAK DLLP Received
                                           0b = Disabled
                                           1b = Enabled

RSVD              31:30         0x0       Reserved.

Table 3-16. Performance Monitor Local Control Register (XPPERFCON) (0x32C4)
     Field       Bit(s)       Init.                                             Description

GRST               0           0b        Global Reset

GCE                1           0b        Global Count Enable

RSVD              31:2         0x0       Reserved.

#### 3.1.6.4 Latency Counter

The latency counter measures the min, max, or average read latency.
Note:         Completion Timeout events are ignored when the latency counter is enabled.
The latency counters are managed via a set of register fields described below (see also Table 3-17,
Table 3-18, and Table 3-19). Each of the following sources of traffic has its separate set of registers and
counters:
     0x0 — Rx LAN descriptor fetch
     0x1 — Tx LAN descriptor fetch
     0x4 — Internal cache load
     0x5 — Internal management engine read
     0x6 — Tx LAN packet fetch
The registers are accessed via the PCI_LCBADD and PCI_LCBDATA registers.
The register fields that control the latency counter operation are:

Table 3-17. NPQ Control Register - NPQC (0x00000)
      Field        Bit(s)       Init.                                             Description

Reserved               3:0       0x4       Reserved.

PERFMNTRAVG            7:4       0x1       Performance Monitor Average Rate
                                           This field sets the averaging rate for all latency average monitors. See definition of
                                           NPQRTDLY1.ARTDLY (Table 3-18).
                                           This field divided by 16 is the weight W in an exponential moving average. The possible
                                           values are 1, 2, 4 or 8, which correspond to averaging rates of 0.0625, 0.125, 0.25 or
                                           0.5, respectively.

PERFMNTREN             8            0b     Performance Monitor Enable
                                           This bit should set to enable latency counters.
                                           Clearing this bit clears the latency counters.

92                                                                                                                      333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-17. NPQ Control Register - NPQC (0x00000) [continued]
     Field         Bit(s)     Init.                                            Description

RTMNTREN              9         0b       Latency Counting Enable
                                         This bit should set to enable latency counters. When set, completion timeout events are
                                         ignored.

Reserved           31:10       0x0       Reserved.

Table 3-18. NPQ Round-Trip Delay 1 Register - NPQRTDLY1 (0x00030; RO)
    Field        Bit(s)     Init.                                             Description

ARTDLY           15:0       0x0        Average Read Requests Round-trip Delay
                                       Captures the average read latency experienced since the last counter reset.
                                       Latency is measured from time the read request starts until the time the completion starts
                                       to arrive. Average is calculated as exponential moving average. That is, the new average
                                       M(n) at sample n equals:
                                         M(n) = (W/16) * new_sample + (16-W)/16*M(n-1)
                                       where W is defined in the NPQC.PERFMNTRAVG field.

Reserved         31:16      0x0        Reserved.

Table 3-19. NPQ Round-Trip Delay 2 Register - NPQRTDLY2 (0x00034; RO)
    Field        Bit(s)     Init.                                             Description

MINRTDLY         15:0       0x0        Minimal Read Requests Round-Trip Delay
                                       Captures the minimal read latency experienced since the last counter reset.
                                       Latency is measured from time the read request starts until the time the completion starts
                                       to arrive.

MAXRTDLY         31:16      0x0        Maximal Read Requests Round-Trip Delay
                                       Captures the maximal read latency experienced since the last counter reset.
                                       Latency is measured from time the read request starts until the time the completion starts
                                       to arrive.

Latencies are measured in cycle counts, where a cycle duration is per Table 3-20.

Table 3-20. Resolution of the Latency Counters
                                          Setting of the
                                                                      PCIe Operational Link
   PCIe Operation Speed             PCI_CLKCTL.PCI_CLK_DYN                                              Cycle Duration (ns)
                                                                             Width
                                                Bit

           Gen1 (2.5G)                          0b                               x                                8

           Gen2 (5.0G)                          0b                               x                                4

           Gen3 (8.0G)                          0b                               x                                2

           Gen1 (2.5G)                          1b                            8 lanes                            16

           Gen2 (5.0G)                          1b                            8 lanes                             8

           Gen1 (2.5G)                          1b                          1 or 4 lanes                         32

           Gen2 (5.0G)                          1b                          1 or 4 lanes                         16

           Gen3 (8.0G)                          1b                          1 or 4 lanes                          8

333369-009                                                                                                                          93
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects
