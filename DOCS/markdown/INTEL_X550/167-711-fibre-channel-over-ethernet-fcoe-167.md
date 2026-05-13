## 7.11 Fibre Channel over Ethernet (FCoE)

### 7.11.1 Introduction

Fibre Channel (FC) is the predominant protocol used in Storage Area Networks (SAN). Fibre Channel
over Ethernet (FCoE) is used to connect an Ethernet storage initiator and legacy FC storage targets.
The FC protocol is based on high reliability of the communication link between the initiator and the
storage target. It assumes an extremely low error rate of 10-12 and no packet drop. DCB extends
Ethernet through class-based flow control in such a way that FC-like no-drop is guaranteed as required
by FC. Doing so, FC protocol can be transposed to an Ethernet link by Layer 2 encapsulation that is
defined by the FCoE protocol. Figure 7-45 shows a connection between an FCoE initiator and legacy FC
targets.

                     Legacy FC Target

                                        FC

                                                FCoE gateway                    FCoE Initiator

                                                                       DCB
                                                          Ethernet
                     Legacy FC Target

                                        FC                            LAN
                                                      Ethernet       Network

Figure 7-45. Connecting an FCoE Initiator to FC Targets

Existing FC HBAs used to connect between an FC initiator and FC targets provide full offload of the FC
protocol to the initiator to maximize storage performance. To compete with this market, the X550
offloads the main data path of I/O Read and Write commands to the storage target.

#### 7.11.1.1 FC Terminology

Useful background on FC framing and its Ethernet encapsulation can be found in Section A.4. More
comprehensive material can be found in the FIBRE CHANNEL FRAMING AND SIGNALING-2 (FC-FS-2)
specification. Following are some of the most common terms used extensively in the sections that
describe the FCoE functionality.
 • FC Exchange — Complete FC read or FC write flow. It starts with a read or write request by the
   initiator (the host system) until it receives a completion indication from the target (the remote
   disk).
 • FC Sequence — An FC exchange is composed of multiple FC sequences. An FC sequence can be
   single or multiple frames that are sent by the initiator or the target. Also, each FC sequence has a
   unique sequence ID.

544                                                                                                      333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • FC Frame — FC frames are the smallest units sent between the initiator and the target. The FC-FS-
   2 specification defines the maximum frame size as 2112 bytes. Each FC frame includes an FC
   header and optional FC payload. It also may include extended headers and FC optional headers.
   Extended headers other than Virtual Fabric Tagging (VFT) are not expected in an FCoE network and
   FC optional headers are not used in most cases as well.
 • Data Frame — FC frames that carry read or write data.
 • FCP_RSP Frame — FC control frames are sent from the target to the initiator, which defines the
   completion of an FC read or write exchange.

### 7.11.2 FCoE Transmit Operation

Transmit FCoE offload is enabled by setting the TUCMD.FCoE bit in the transmit context descriptor. The
X550 supports the following offload capabilities: FC CRC calculation and insertion, FC padding insertion
and FC segmentation. These capabilities are described in the following sections.

#### 7.11.2.1 FCoE Transmit Cross Functionality

After setting the TUCMD.FCoE bit, hardware digests the packet’s content before it is sent to the wire. In
this case, software must enable hardware offload for additional tasks as follows:

Cross Function              Requirements

Ethernet CRC insertion      Software must enable Ethernet CRC insertion by setting the IFCS bit in the transmit data descriptor.
                            The Ethernet CRC covers the entire packet. Enabling FCoE offloading, hardware modifies the packet
                            content and must also adjust the Ethernet CRC.

VLAN header                 It is assumed that any FCoE has a VLAN header. In the case of double VLAN mode, the packet must
                            have the two VLAN headers.

SNAP packet                 The X550 does not provide FCoE offload for FCoE frame over SNAP.

Traffic rate control        FC traffic relies on a high quality link that guarantees no packet loss. It is expected that any lost
                            traffic protocols supported by the network are enabled by the X550 as well.
FC and PFC

Virtualization              It is expected that the VMM abstract the FCoE functionality to the VM(s). FCoE setting and FCoE
                            traffic is expected only by the VMM accessing the LAN via the PF.

TCP/IP and UDP/IP offload   FCoE traffic is L2 traffic (not over IP). Any setting of TCP/IP and UDP/IP offload capabilities are not
                            applicable and do not impact FCoE offload functions.

Transmit descriptors        Software must use the advanced transmit descriptor to activate either FC CRC offload or TSO
                            functionality.

#### 7.11.2.2 FC Padding Insertion

FC frames always consist of a whole number of four bytes. If user data is not composed of a whole
number of four bytes, the FC frames contain padding bytes with a zero value. The length of the padding
bytes can be any number between zero to three so together with the user data, the length of the FC
frames has a whole number of four bytes. The length of the padding bytes is indicated by software in
the Fill Bytes field in the FC header. This field is used by the receiving end node (target) to extract these
bytes. Hardware does not use this field to identify the required length of the padding bytes. Instead, it
checks the transmit buffer size indicated by the PAYLEN field in the transmit data descriptor. The length
of the padding bytes added by hardware equals:
    2’s complement {two LS bits of (PAYLEN minus MACLEN)}.

333369-009                                                                                                                          545
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

where PAYLEN is defined in the Tx data descriptor and MACLEN is defined in the Tx context descriptor.
The X550 auto-pads the frame with the required zero bytes when FCoE offload is enabled (TUCMD.FCoE
bit is set). In TSO, padding bytes are added only on the last frame since the MSS must be a whole
number of four bytes.

#### 7.11.2.3 SOF Placement

During a single send, the SOF field is taken as is from the FCoE header in the data buffer.
During TSO (both the TUCMD.FCoE bit in the transmit context descriptor and the DCMD.TSE bit in the
transmit data descriptor are set), the SOF field in the data buffer is replaced by hardware according to
the values of the SOF and ORIS bits in the transmit context descriptor. In this case the value of the SOF
field in the data buffer is ignored (for future expansion software should set it to zero). The SOF codes
that are inserted to the transmitted packets are stored in the TSOFF register. The TSOFF register
contains four SOF codes named as SOF0...SOF3 that are supported by the transmit FCoE offload. By
default these values are programmed to the following values: SOF0 = SOFi2; SOF1 = SOFi3; SOF2 =
SOFn2; SOF3 = SOFn3. The SOF flag and Orientation Start (ORIS) bit in the FCoEF field in the transmit
context descriptor define an index value. This index is used to extract the SOF code that is inserted to
the packet as listed in the Table 7-76. The ORIS bit defines if the TSO starts an FC sequence or if the
first frame on the FC sequence is already sent.

Table 7-76. SOF Codes in TSO
    SOF Bit in the         ORIS Bit in the           SOF Code in the First    SOF Code in Other        SOF Code in a Single
  Context Descriptor     Context Descriptor                Frame                   Frames                    Packet

# 1 (Class 3)           1 (sequence start)           SOF1 (SOFi3)              SOF3 (SOFn3)            SOF1 (SOFi3)

# 1 (Class 3)       0 (not a sequence start)         SOF3 (SOFn3)              SOF3 (SOFn3)            SOF3 (SOFn3)

# 0 (Class 2)           1 (sequence start)           SOF0 (SOFi2)              SOF2 (SOFn2)            SOF0 (SOFi2)

# 0 (Class 2)           0 (not a sequence)           SOF2 (SOFn2)              SOF2 (SOFn2)            SOF2 (SOFn2)

#### 7.11.2.4 EOF Insertion

The X550 automatically inserts the End of Frame field when the TUCMD.FCoE bit in the transmit context
descriptor is set.
The EOF and ORIE fields define the EOF that is inserted by hardware. In a single packet send, the EOF
field is defined completely by the EOF setting while in TSO mode, the EOF field is defined by the EOF
and the ORIE bits as listed in Table 7-77.

Table 7-77. EOF Codes in TSO
  EOF Bits in the Context         ORIE Bit in the Context       Last Frame of a TSO or TSO
                                                                                                    Other frames of TSO
        Descriptor                     Descriptor                     in single frame

# 0 (not a sequence end)               EOF0 (EOFn)                      EOF0 (EOFn)

# 00 (EOFn)

# 1 (sequence end)                  EOF1 (EOFt)                      EOF0 (EOFn)

            Other                                X                           N/A                             N/A

546                                                                                                                333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.11.2.5 FC CRC Insertion

FC CRC calculation is one of the most CPU intensive tasks in large transactions. The X550 offloads the
FC CRC calculation when the FCoE bit is set in the TUCMD field within the transmit context descriptor.
The X550 calculates and adds the FC CRC before packet transmission but after the required FC padding
bytes are already added.
The CRC polynomial used by the FC protocol is the same one as used in FDDI and Ethernet as shown in
the following equation. While CRC bytes are transmitted in big endian byte ordering (MS byte first on
the wire):
    X32+X26+X23+X22+X16+X12+X11+X10+X8+X7+X5+X4+X2+X+1

The size of FCoE payload on which FC CRC is calculated is indicated in the context and data descriptors
as follows. Figure 7-46 specifies the FCoE frame and the relevant parameters to CRC calculation.

                               ==HEADLEN==                                ==FC Payload LEN==

                                       F
                                   r   O [opt.] FC                                                     C     F       C
               MAC         N     E e   S               FC (basic)       [opt.] FC Option Headers +     R
                           A     o d   - Extended                                                      C     O       R
             Addresses     L     C a   E                Header              Data & FC Padding                E
                                                                                                             -       C
                           V     F e
                                   H     Headers                                                       C     E
                                                                                                                     -
                                                                                                                     E
                                                                                                       F

                 ==MACLEN==                               ==FC CRC Calculation==

Figure 7-46. FCoE Frame and Relevant Transmit Descriptor Parameters

FC CRC Calculation Beginning:
FC CRC calculation starts after the FCoE header. It equals to byte offset of MACLEN + 4, while the
MACLEN field in the transmit context descriptor is the byte offset of the last DWord in the FCoE header
that contains the SOF flag.
FC CRC Calculation End:
FC CRC calculation ends at the end of the FC Payload LEN shown in Figure 7-46 (eight bytes before the
Ethernet CRC).

#### 7.11.2.6 Host Data Buffers Content for a Single Packet Send

 Table 7-78 lists the data prepared by software when transmit FCoE offload is enabled (the FCoE bit in
the TUCMD field is set in the transmit context descriptor).

Table 7-78. Transmit FCoE Packet Data Provided by Software (for TUCMD.FCoE = 1)
                                                                 FC Frame (provided by software)
 Ethernet MAC      VLAN     FCoE       [opt.] FC
   Addresses      Header   Header                                   FC Option
                                       Extended      FC Header                            [Opt.] Data & FC Padding
                                                                    Header(s)
                                       Headers

Listed below are fields in the transmitted FCoE frame that are not included in the data buffers (in host
memory) as shown in Table 7-78.
 • VLAN Header — The VLAN header could be part of the data buffer or in the transmit descriptor
   depending on VLE bit in the CMD field in the transmit descriptor.

333369-009                                                                                                               547
                                    Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

 • EOF — The EOF is defined by the EOF fields and ORIE bit in the context descriptor (more details in
   Section 7.2.3.2.3).
 • FC-CRC — The X550 calculates and inserts the FC CRC bytes.
 • FC-Padding — The X550 calculates the padding length and inserts these bytes as required (all
   zeros).
 • Ethernet CRC — Insertion should be enabled by the IFCS bit in transmit data descriptor.

#### 7.11.2.7 FC TSO

FCoE segmentation enables the FCoE software to initiate a transmission of multiple FCoE packets up to
a complete FC sequence with a single header in host memory (single instruction). It is activated by
using the advanced Tx context descriptor (DTYP equals 0010b) and setting both the TUCMD.FCoE in the
context descriptor and setting the DCMD.TSE bit in the transmit data descriptor. The X550 splits the
transmitted content to multiple packets as defined by the MSS field in the Tx context descriptor.
TSO Parameters:
 • The frame header includes the Ethernet MAC Addresses, VLAN Tag, FCoE header, and the FC
   header. The header size is defined by the HEADLEN and MACLEN in the context descriptor as
   illustrated in Figure 7-46.
 • The SOF and EOF fields are defined by the SOF, ORIS, EOF and ORIE fields in the context descriptor
   as described in Section 7.11.2.3 and Section 7.11.2.4.
 • MSS – the maximum segment size in the context descriptor that define the FC data (payload) size
   on each packet other than the last frame which can be smaller.

7.11.2.7.1             Host Data Buffers Content for TSO Offload

Figure 7-47 shows the data in host memory when FCoE TSO is activated. The TSO header is repeated
on all frames of the TSO. The header includes static and dynamic fields that are modified by hardware
from packet-to-packet. The payload size is reflected in all frames.

                       MAC Addresses ; VLAN ; FCoE Header ; [opt.] VFT ; FC (basic) Header

                  TSO FC Option
                                                  FC Payload / Data (including optional padding)
                 header Header(s)

                                     . .MSS. .                        . .MSS. .                    . .Residual. .

          TSO FC Option                           TSO                                           TSO
                              FC Data (1)                            FC Data (2)                              FC Data (3)
         header Header(s)                        header                                        header

Figure 7-47. FCoE TSO Provided by the FCoE Driver

FCoE Header:
The FCoE packet header must not span more than two buffers. For best bus use it is recommended that
the header be located in a single buffer (the first one).
 • Ethernet MAC Addresses are the source and destination Ethernet MAC Addresses
 • VLAN tag can be provided by the driver as part of the packet header or as part of the data
   descriptor.

548                                                                                                                         333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • FCoE header (shown in Figure 7-47) includes the FCoE Ethernet type, FCoE Version and SOF flag.
   Software should leave the SOF fields as zero while hardware inserts it according to the SOF and
   ORIS bits in the Tx context descriptor.
 • FC (basic) header as shown in Section A.4.2.3.
FCoE TSO — Payload:
 • FC option headers as described in Section A.4.2.5.
 • FC data to be segmented
 • The payload may or may not include the optional FC padding bytes. Hardware adds any required
   padding bytes not included in the data buffers according to the PAYLEN field in the data descriptor.
Modified fields between consecutive frames within TSO.
    SOF            The SOF flags are defined by the SOF bit and ORIS bit in the context descriptor (more
                   details in Section 7.11.2.3)
    F_CTL          Table 7-79 lists those fields in the F_CTL that are modified between consecutive frames
                   of a TSO (see Section A.4.2.3 for a complete description of the F_CTL field). If a TSO is
                   transmitted by a single packet all F_CTL fields are taken from the data buffer (as if it is
                   the last frame in the TSO).

        Table 7-79. F_CTL Codes in TSO
                                      Last Frame in TSO when the ORIE Bit in the Tx
                 F_CTL Bits                                                                          Any Other Frame
                                                Context Descriptor is Set

          Fill Bytes (1:0)            Taken from the F_CTL(1:0) in the data buffer. It      00b if not last frame on TSO or taken
                                      defines the length of the FC padding required to      from the F_CTL(1:0) in the data
                                      make the FC data a complete multiply of four bytes.   buffer if last frame in TSO (even if
                                                                                            ORIE bit is not set).

          Continue Sequence           Taken from the F_CTL(7:6) in the data buffer. The     00b
          Condition (7:6)             continue sequence condition is meaningful only if
                                      F_CTL(19) is set and F_CTL(16) is cleared.

          Sequence Initiative (16)    Taken from the F_CTL(16) in the data buffer. The      0b
                                      sequence initiative is meaningful only if F_CTL(19)
                                      is also set.

          End Sequence (19)           Taken from the F_CTL(19) in the data buffer. The      0b
                                      end sequence should be set to 1b by software only
                                      if the frame is the last one of a sequence.

    DF_CTL         Table 7-80 lists those fields in the DF_CTL that can be modified between consecutive
                   frames of a TSO. Note that the ESP Header Presence bit is not listed in this table. When
                   ESP Header is present, software must not use a TSO that spans across multiple
                   packets. If a TSO is transmitted by a single packet all DF_CTL fields are taken from the
                   data buffer (as if it is the first frame in the TSO).

        Table 7-80. DF_CTL Codes in TSO
                                                 1st Frame in TSO when ORIS Bit in the Tx
                    DF_CTL Fields                                                                         Any Other Frame
                                                         Context Descriptor is Set

          Device Header Indication (1:0)      Taken from the data buffer.                           00b

          Association Header Indication (4)   Taken from the data buffer.                           0b

          Network Header Indication (5)       Taken from the data buffer.                           0b

333369-009                                                                                                                     549
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                              Inline Functions

      SEQ_CNT             SEQ_CNT in the first frame is taken from the SEQ_CNT field in the FC header in
                          the data buffers. On any other frame, the value of SEQ_CNT is increased by one
                          from its value in the previous frame. The SEQ_CNT wrap-to-zero after reaching a
                          value of 65,535.
      PARAM               The PARAM field in the first frame is taken from the PARAM field in the FC header
                          in the data buffers. If the FCoEF.PARINC bit is set in the transmit context
                          descriptor, the value of the PARAM becomes dynamic. In that case, the PARAM is
                          increased by hardware by the MSS value on each frame. Software should set the
                          FCoEF.PARINC bit when the PARAM field indicates the data offset (Relative Offset
                          Present bit in the F_CTL field is set).
      FC_CRC              Calculated and inserted on each frame as described in Section 7.11.2.5.
      FC_Padding          Calculated the number of required padding bytes and inserted them on the last
                          frame as described in Section 7.11.2.2.
      EOF                 The EOF flags are defined by the EOF field and the ORIE bit in the context
                          descriptor (more details in Section 7.11.2.4).

### 7.11.3 FCoE Receive Operation

The X550 can offload the following tasks from the CPU while processing FCoE receive traffic: FC CRC
check, receive coalescing and Direct Data placement (DDP). These offload options are described in the
sections that follow.
DDP functionality is not provided for control packets or data packets that do not meet DDP criteria
(described later in the sections that follow). In those cases, hardware posts the packets to the legacy
Rx queues as is (header and trailer are not stripped including SOF, EOF, FC padding and FC CRC bytes).
When DDP functionality is enabled, only the FC payload is posted to the user buffers. If the packet’s
header should be indicated to the legacy Rx queues, all bytes starting at the destination Ethernet MAC
Address until the FC header and optionally FC header(s) inclusive are posted to the legacy buffer.

#### 7.11.3.1 FCoE Receive Cross Functionality

FCoE receive offload capabilities coexist with other functions in the X550 are listed as follows:

Table 7-81. FCoE Receive Cross Functionality
Cross Function                 Requirements

Ethernet CRC check             There is no enforcement on save bad frames policy. In the case of save bad frames, packets with
                               bad Ethernet CRC are posted to the legacy receive queue even if DDP is enabled. FC payload of
                               bad packets are never posted directly to the user buffers.

Ethernet padding extraction    There is no enforcement on the Ethernet padding extraction. When DDP is enabled, hardware
                               posts the FC payload to the user buffers. When DDP is not enabled the entire packets are posted
                               to the legacy receive queues with or without the Ethernet padding according to the device
                               setting.

VLAN header                    It is assumed that any FCoE has a VLAN header. In the case of double VLAN mode, the packet
                               must have the two VLAN headers.

SNAP packet                    The X550 does not provide FCoE offload for FCoE frame over SNAP.

FC and PFC                     FC traffic relies on a high-quality link that guarantees no packet loss. It is expected that any lost
                               traffic protocols supported by the network is enabled by the X550 as well.

Virtualization                 It is expected that VM(s) generate FC write requests to the VMM. FCoE setting and FCoE traffic is
                               expected only by the VMM accessing the physical function.

550                                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-81. FCoE Receive Cross Functionality [continued]
Cross Function                       Requirements

TCP/IP and UDP/IP offload            FCoE traffic is L2 traffic (not over IP). Any setting of TCP/IP and UDP/IP offload capabilities are
                                     not applicable and do not impact FCoE offload functions.

Jumbo frames                         Maximum expected clear text FC frame size is 2140 bytes (FC header + FC payload + FC CRC).
                                     Adding optional FC crypto, plus FCoE encapsulation, packet might exceed the 2200 bytes. To
                                     enable FCoE traffic, jumbo packet reception should be enabled.

Receive descriptors in the           When FC CRC offload or DDP functionality are enabled, software must use the advanced
legacy Rx queues                     descriptors in the associated legacy Rx queues (SRRCTL.DESCTYPE = 001b). The legacy Rx
                                     buffers must be larger than the maximum expected packet size so any Rx packets span on a
                                     single buffer.

#### 7.11.3.2 FC Receive CRC Offload

FC CRC calculation is one of the most CPU intensive tasks in TSO transactions. The X550 offloads the
receive FC CRC integrity check while trashing the CRC bytes and FC padding bytes.
The X550 recognizes FCoE frames in the receive data path by their FCoE Ethernet type and the FCoE
version in the FCoE header. The Ethernet type that hardware associates with FCoE is defined in the
ETQF register by setting the FCoE bit with a specific Ethernet type value. The supported FCoE versions
by the Rx offload logic are defined by FCRXCTRL.FCOEVER. FCoE packets that do not match the
previously described Ethernet type and FCoE versions are ignored by the Rx FCoE logic.
The X550 reconstructs the FC CRC while processing the incoming bytes and compares it against the
received FC CRC. The frame is considered a good FC packet if the previous comparison matches and it
is considered as a bad FC packet otherwise.
The FC CRC integrity check is meaningful only if all the following conditions are met:
 • The received frame contains a correct Ethernet CRC
The length of the FC padding bytes that hardware trashes are defined in the Fill Bytes field in the FC
frame control (F_CTL). The Fill Bytes field can have any value between zero to three that makes the FC
frame a whole number of DWords. It is expected that the Fill Bytes field would be zero except for last
data frames within a sequence.

                      MAC              VLAN       FCoE                                                     Opt. FC
                                                             FC Header(s)             FC Data                            FC CRC
                    Addresses           Tag      Header                                                    Padding

                              FCoE Ethernet Type               F_CTL.Fill Bytes

                CRC polynomial: X 32 + X 26 + X 23 + X 22 + X 16 + X 12 + X 11 + X 10 + X 8 + X 7 + X 5 + X 4 + X 2 + X + 1

Figure 7-48. Relevant FCoE and FC Fields for CRC Receive Offload

333369-009                                                                                                                             551
                                          Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Inline Functions

#### 7.11.3.3 Large FC Receive

Large FC receive includes two types of offloads. The X550 can save a data copy by posting the received
FC payload directly to the kernel storage cache or the user application space (in the remainder of the
document there is no difference between the two cases and it is named as user buffers). When the
packet’s payload are posted directly to the user buffers their headers can be posted to the legacy
receive queues. The X550 saves CPU cycles by reducing the data copy and also minimize CPU
processing by posting only the packet’s headers that are required for software.
Figure 7-49 shows the mapping of received FCoE frames to the legacy Rx queue and the user buffers.
Figure 7-50 shows a top level overview of the large FC receive flow. The remaining sections detail the
large FC receive functionality as follows:
 • Enabling large FC receive — Section 7.11.3.3.1
 • FC read exchange flow — Section 7.11.3.3.2
 • FC write exchange flow — Section 7.11.3.3.3
 • FCoE receive filtering (Frame types and rules) — Section 7.11.3.3.5, Section 7.11.3.3.10 and
   Section 7.11.3.3.12
 • User descriptors — Section 7.11.3.3.9
 • Header posting to the legacy receive queues and FC exceptions — Section 7.11.3.3.13 and
   Section 7.11.3.3.14
 • Interrupts — Section 7.11.3.3.15

             (16) x Legacy Rx Queues
                                                                     (2048) x FC Contexts
               used for FCoE Traffic
          Descriptors         Data
                                 . .Buffers
                                     .                        (2048) x “User Descriptors”
           Address                                           Lists and their “User Buffers”
            Status        Rx Buff: FCoE Frame
                           Header of the first
           Address          frame (optional)
            Status                                                     Buffer          FC Data
                                                                                      First Frame    Example:
           Address                                                       0                            First FC
            Status               ...                                                        ...        Read
                                                         Address       Buffer           FC Data
           Address        Rx Buffer: FCoE Frame                                                      Sequence
            Status                                       Address         1              Frame N
                           Header of the last
           Address           frame in the FC                                            FC Data
                                                         Address       Buffer
            Status              Sequence                                               Frame N+1
                                                           ...           2                            Example:
           Address               ...                                                                 Proceeding
            Status                                       Address        ...                           FC read
           Address               Rx Buffer                                                           Sequences
                                                                       Buffer           FC Data
            Status                                                       N             Last Frame
                                Required headers are posted in the
                DDP status                                                      . .DDP. .
                                   legacy Rx queue. The OX_ID
                 indication
                               indicates the associated FC Context

Figure 7-49. Large FC Reception to User Buffers and Legacy Rx Queue

552                                                                                                               333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

              New Frame is received                                                                      1

             Identify Legacy Rx Queue                            Indicate the frame to      Fail    FC filtering
                                                                   Legacy Rx queue                      (1)

                                                                                                             OK
                      Check                     Indicate packet to legacy
                                 Bad CRC
                     Ethernet                  Rx queues in case of Save            Post FC data to user buffer at “user
                      CRC                          Bad Frame setting                 buffer Offset”. If data exceeds the
                                                                                       buffer limits update the “User
                                                                                   Descriptor PTR” and fetch a new “User
                                                                                                 Descriptor”.
                                                                                    Then update the “User Buffer offset”

                            OK               Note (1) Check Legit frames for             Update SEQ_CNT and SEQ_ID
                                             large FCoE receive (FCoE
          Packet parsing: Identify FCoE      receive filtering): Allowed SOF
           header and FC frame length        values; The Frame Contains FC
                                                                                                   FCoE Header     No
                                             Data; no ESP option header;
                                             Valid Context in the OX_ID entry                      Required (2)
                      Check
                                 Bad CRC     in the context table; Match the
                      FCoE                                                                                   Yes
                      CRC                    source address entry in the
                                             context table “Abort Sequence         Post FCoE frame header to legacy Rx
                            OK                                                     queue with DDP status indication. The
                                             Condition” is inactive and in order
                 Fetch FC context            reception.                              The OX_ID in the frame’s header
             according to OX_ID value        Note (2) Examples for required          points to the “User descriptor list”
                                             headers of: Last packet in FC
                                             sequence. First packet in FC            Initiate an Rx interrupt according to
                        1                    sequence that includes FC option                FCoE interrupt policy
                                             headers.

                                                                                            End Frame processing

Figure 7-50. FCoE Large Receive Flow Diagram

7.11.3.3.1                  Enabling Large FC Receive

Large FC receive offload is enabled per each outstanding read or write exchange by programming the
FCoE context table with the flow parameters. Setting the FC context for read or write exchange is done
at run time. It is expected that a read context is programmed before the read request is initiated to the
remote target and write context is programmed before the target sends the ready indication to the
initiator. Unless the FC context is invalidated, software must not modify it in the middle of a transaction
(see Section 7.11.3.3.5 for details on context invalidation). For more details on FCoE initialization flow
see Section 4.6.9.

7.11.3.3.2                  FC Read Exchange Flow

Figure 7-51 shows an example of an FC (class 3) read request. This flow is detailed in this section.
1. The software checks if the read request can use large FC receive offload depending on FC context
   resources and some criteria as listed in Section 7.11.3.3.5. Section 7.11.3.3.12 describes a
   proposed software flow to manage the FC contexts.
2. If the previous conditions are not met, software can still initiate the FC read request according the
   flow described in Figure 7-51 while the received frames are posted to the legacy receive queues.

333369-009                                                                                                                   553
                                        Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                            Inline Functions

      • If the previous conditions are met, software locks the relevant user buffers (the target buffers
        for the FC read request) and program the FC context table. It then initiates the FC read request
        according the flow shown in Figure 7-51. The payload of the received frames is posted directly
        to the user buffers. Some of the packet’s headers (only the required ones) are posted to the
        legacy receive queues. The FC header in the packet’s header contains the OX_ID field. This field
        indicates to software its context and its user buffer list. During nominal operation, all packets’
        headers except packets with FC optional headers are trashed by the hardware minimizing
        software overhead.
3. The target sends the FCP_RSP frame type indicating the completion of the read exchange. As a
   response, the hardware invalidates the FC read context (if it was used) and indicates the number of
   bytes posted directly to the user buffers in the receive descriptor (see Section 7.11.3.3.13).
   Software indicates the read completion to the application.

                      Initiator     FC Seq. ‘x': CMND packet = FC Read Request             Target

                                    FC Seq. ‘i’: First DATA packet in the sequence
                                    FC Seq. ‘i’: DATA packet 2                              First FC
                                                  ...                                      Sequence
                                    FC Seq. ‘i’: Last DATA packet in the sequence               ‘i’

                                                 ...

                                    FC Seq. ‘m’: First DATA packet in the sequence          Last FC
                                                 ...                                         Data
                                    FC Seq. ‘m’: Last DATA packet in the sequence          Sequence
                                                                                              ‘m’

                                    FC Seq. ‘n’: RSP packet = Read completion           FC Sequence
                                                                                             ‘n’

Figure 7-51. Example for FC Class 3 Read Exchange Flow

7.11.3.3.3           FC Write Exchange Flow

Figure 7-52 shows an example of an FC (class 3) write request (on which the Seq_CNT starts from zero
on each new sequence). This flow is detailed in the sections that follow.
1. The host (originator) sends an FC write request to the target (responder).
2. Software in the target checks if the write request can use large FC receive offload depending on FC
   context resources and some criteria as listed in Section 7.11.3.3.5.
3. If the previous conditions are met, software can use DDP for this FC write exchange.
4. The target software locks the relevant user buffers (the target buffers for the FC write request) and
   program the FC context table. It then initiates the FC ready indication to the host.
5. As a response, the host sends the data frames to be written to the target. The frames are received
   in the target. If DDP is used, the FC payload is posted directly to the user buffers while “most” (see
   additional details below) packet’s headers are trashed minimizing software overhead.
6. The host marks the last data frame it was requested to send by setting the Sequence Initiative bit
   in the F_CTL field.

554                                                                                                             333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7. The target identifies the last data frame and invalidates the DDP context. As indicated above,
   during nominal operation, “most” packet’s headers are trashed. Only headers that have meaningful
   content are posted to host memory as: Headers of packets with FC optional headers and the header
   of the last packet in a sequence with active sequence initiative bit are posted to the legacy receive
   queues. The hardware indicates the number of bytes posted directly to the user buffers in the
   receive descriptor (see Section 7.11.3.3.13). Note that the FC header contains the RX_ID field that
   can be used by software to identifies its associated DDP context and user buffer list.
8. The target may repeat Step 4, which is followed by Step 5 until the entire requested data is
   transferred.
9. The target sends the FCP_RSP frame indicating to the initiator the completion of the write
   exchange.

                  Initiator    CMND packet = FC Write Request: FC Seq. ‘k', Seq_CNT = 0    Target

                               XFER_RDY: FC Seq. ‘x’, Seq_CNT = 0

                               Data: FC Seq. ‘i’, Seq_CNT = 0
                                                                                           First Data
                               Data: FC Seq. ‘i’, Seq_CNT = 1
                                                                                           Sequence
                                                  ...                                       (N data
                               Data: FC Seq. ‘i’, Seq_CNT = N-1, Sequence Initiative = 1    packets)

                               XFER_RDY: FC Seq. ‘y’, Seq_CNT = 0

                               Data: FC Seq. ‘j’, Seq_CNT = 0                                 Data
                                                  ...                                      Sequence
                               Data: FC Seq. ‘j’, Seq_CNT = M-1, Sequence Initiative = 1    (M data
                                                                                            packets)

                               RSP: FC Seq. ‘z’, Seq_CNT = 0

Figure 7-52. Example for FC Class 3 Write Exchange Flow

7.11.3.3.4              EOF and SOF Flags identification

As part of the DDP functionality, hardware identifies the SOF and EOF flags in the received packets. The
flags identification is based on a setting of the RSOFF and REOFF registers. These registers are identical
to the TSOFF and TEOFF registers and should be programmed by software to the same values.

7.11.3.3.5              FCoE Receive Filtering

Received FCoE frames are associated to one of the legacy receive queues according to the scheme
described in Section 7.1.3. When the legacy receive queue is enabled, large FC receive functionality is
enabled as well if a matched FC receive context is defined. The data is posted to the user buffers that
are pointed to by the FC receive context. Some of the headers of these frames that are required for the
data processing are posted to the legacy receive queue (see Section 7.11.3.3.13).

333369-009                                                                                              555
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

FCoE frames that carry FC class 3 or class 2 data can be posted to large receive buffers if they meet the
following conditions:
 • The FC context table contains valid context that matches the exchange ID in the received frame.
   Hardware checks the RX_ID for write data packets sent by the initiator. These packets are identified
   by the Exchange Context bit in the F_CTL header equals zero (originator of exchange). Hardware
   checks the OX_ID for read response data packets sent by the target. These packets are identified
   by the Exchange Context bit in the F_CTL header equals one (responder of exchange).
 • The FC frame source address match the source MAC Address field in the in the same valid exchange
   ID context.
 • Frames are identified as FCoE frame type according to the Ethernet type in the FCoE header. The
   Ethernet type that hardware associates with FCoE is defined in the ETQF registers by setting the
   FCoE bit with a specific Ethernet type value.
 • The FC frame carry class 2 or class 3 content as defined by the SOF flag. The SOF in the FCoE
   header equals SOFi2 or SOFn2 or SOFi3 or SOFn3.
 • The FCoE version in the received frame is equal or lower than FCRXCTRL.FCOEVER.
 • The frame contains data content (with data payload) as defined in the Routing Control field (R_CTL)
   in the FC header:
      — R_CTL.Information (least significant four bits) equals 0x1 (solicited data).
      — R_CTL.Routing (most significant four bits) equals 0x0 (device data).
      — Frames that do not contain device data are not posted to the user buffers. Still these frames are
        compared against the expected SEQ_ID and SEQ_CNT in the FC context and update these
        parameters as described in Section 7.11.3.3.5.
 • The FC frame does not include ESP header (bit 6 in the DF_CTL field within the FC header is
   cleared). Frames that include ESP option headers are posted to the legacy receive queue. For good
   use of hardware resources, software should not program the large FC receive context table with
   flows that carry an ESP header.
 • The FC frame does not include FC extended headers. For good use of hardware resources, software
   should not program the large FC receive context table with flows that carry extended headers.
 • The first packet received to a new context is identified as the first FC frame in the exchange. This
   packet is expected to have the SOFi2 or SOFi3 codes. The SEQ_ID on the first packet may have any
   value.
 • The frame is received in order as defined in Section 7.11.3.3.7 and does not carry any exception
   errors as defined in Section 7.11.3.3.14.
 • The first frame on each FC sequence is identified by the SOFi2 or SOFi3 codes in the SOF field in the
   FCoE header. It is expected that the SEQ_ID is changed for any new sequence.
 • The last frame on each FC sequence is identified by an active End Sequence flag in the F_CTL field
   in the FC header. It is expected to receive the EOFt code in the EOF field; however, hardware does
   not check this rule.
Other frames (that do not meet the previous conditions) are posted to the legacy receive queues
according to the generic Rx filtering rules.

556                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.11.3.3.6                DDP Context

Hardware can provide DDP offload for up to 2048 concurrent outstanding FC read or write exchanges.
Each exchange has an associated FC context in hardware. Contexts are identified by the exchange ID
(OX_ID for FC read and RX_ID for FC write). The exchange ID is a 16-bit field so that a system could
theoretically generate up to 64 K concurrent outstanding FC read requests and 64 K concurrent
outstanding FC write requests. Hardware contains 2048 contexts for the 2048 concurrent outstanding
exchanges. Using exchange ID values between 0 to 2047, software can benefit from the DDP offload.
Each entry in the DDP table can be used to offload either a read exchange (as the initiator) or a write
exchange (as the target).
Mapping an exchange to a DDP context is done by the exchange ID. The 11 LS bits of the exchange ID
is the DDP context Index. In addition, read DDP context is defined by the 11 LS bits of the OX_ID and
write DDP context is defined by the 11 LS bits of the RX_ID. Therefore, if a specific OX_ID is offloaded
by read DDP, the same number of RX_ID can't be offloaded by write DDP at the same time.
The FC context is a set of parameters used to identify a frame and its user buffers in host memory. The
context parameters are split into two categories (according to the internal hardware implementation):
DMA context (FCPTRL, FCPTRH, FCBUFF and FCDMARW registers) and filter context (FCFLT, FCPARAM,
SMAC, FCD_ID, and FCFLTRW registers) as listed in Table 7-82 and shown in Figure 7-53.
Software should program both the DMA context and filter context making the context usable. During
reception, hardware updates some of the parameters if the packet matches all criteria detailed in
Section 7.11.3.3.5. Initialization values and the updated ones are listed in this section.

Table 7-82. Large FC Context Table
                              DMA Context                                                 Filter Context
 Exchange         (FCPTRL, FCPTRH, FCBUFF, FCDMARW)                                 (FCFL, FCFLTRW, FCBUFF)
    ID
                      DMA Flags               User Descriptor        Filter Flags             In Order Reception

# 0 Valid, First, Last, Count    Size, Offset, Pointer   Valid, First     Seq_ID, Seq_CNT, PARAM,SMAC1, D_ID2

# 1 Valid, First, Last, Count    Size, Offset, Pointer   Valid, First    Seq_ID, Seq_CNT, PARAM, SMAC1, D_ID2

# 2 Valid, First, Last, Count    Size, Offset, Pointer   Valid, First    Seq_ID, Seq_CNT, PARAM, SMAC1, D_ID2

     ...                   ...                                           ...

    2047        Valid, First, Last, Count    Size, Offset, Pointer   Valid, First    Seq_ID, Seq_CNT, PARAM, SMAC1, D_ID2

1. If FCRXCTRL.SMAC_EN is set
2. If FCRXCTRL.DID_EN is set

Note:        The WRCONTX field differentiating read and write exchanges is not part of the filter. Thus
             software should not request a DDP offload of a read flow if a write flow with the same
             Exchange ID may be received and vice versa.

333369-009                                                                                                              557
                                        Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Inline Functions

                Large FC Receive Context                         User Descriptor List                    User Buffers
                 (Host memory buffer)
                                                                                                            Buffer 0
                 Context Valid                                   User Buffer 0 Address
                 User Descriptor PTR
                                                                 User Buffer 1 Address                      Buffer 1
                 User Buffer Offsets
                 Buffer Size                                     User Buffer 2 Address
                 First and Null Flags                                                                       Buffer 2
                                                                           ...
                                                                                                             ...
                                                           Last User Buffer Address + Size
                                                                                                            Buffer N

Figure 7-53. Large FC Receive Context Related to the User Buffers

Table 7-83. FCoE DMA and Filter Contexts
               Width                                                           Initialization
      Field                              Description                                                   Updates by Hardware
               (Bits)                                                              Value

DMA              1      DMA context is valid.                              1                    Cleared when context is invalidated.
Context                                                                                         See Section 7.11.3.3.10 and
Valid1                                                                                          Section 7.11.3.3.11

Filter           1      Filter Context is valid.                           1
Context
Valid

Filter First     1      The first received frame that matches an           0                    Hardware sets this bit when the filter
                        active context in the filter unit is marked by                          unit recognizes the first packet that
                        the filter. This marking is used by the DMA                             matches a valid context.
                        unit as an indication that reception to this
                        context has been started. The DMA context
                        does not accept packets from the filter unit
                        unless it received successfully the packet that
                        was marked as the first one (see the section
                        on exception handling in
                        Section 7.11.3.3.14).

DMA First        1                                                         0                    Hardware sets this bit when the DMA
                                                                                                unit received packet that matches a
                                                                                                valid context and marked as first by
                                                                                                the filter unit.

DMA Last         1                                                         0                    Hardware sets this bit when the DMA
                                                                                                unit received packet that matches a
                                                                                                valid context and marked as last by
                                                                                                the filter unit.

Buffer           8      Defines the number of remaining user buffers       Number of the        During reception, hardware
Count                   in the list. A value of 0x00 means 1024            allocated user       decrements the buffer count as each
                        buffers                                            buffers.             of them completes.

Buffer Size      2      Defines the user buffer size used in this          Buffer Size          Static Parameter
                        context.
                          00b = 4 KB
                          01b = 8 KB
                          10b = 16 KB
                          11b = 64 KB.
                        All buffers except the first one and the last
                        one are full size. The address of all buffers is
                        aligned to the buffer size in the context. The
                        first buffer can start at a non-zero offset. The
                        size of the last buffer can be smaller than the
                        buffer size as defined by the last buffer size
                        parameter.

User Buffer     16      Byte offset within the current buffer to which     Beginning of the     Next received packet offset.
Offset                  the next packet should be posted.                  first buffer.

558                                                                                                                        333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-83. FCoE DMA and Filter Contexts [continued]
               Width                                                         Initialization
    Field                                Description                                                    Updates by Hardware
               (Bits)                                                            Value

 Last User       16     Size of the last user buffer in byte units.      Last user buffer        Static Parameter
 Buffer Size                                                             size.

 User             8     The user buffers are indicated by a list of      Beginning of the        Hardware increments the user
 Descriptor             pointers named as user descriptors (see          user descriptor list.   descriptor PTR by eight (the size of
 PTR                    Section 7.11.3.3.9 for a description of the                              the user descriptor) when it
                        user descriptors). The user descriptor PTR in                            completes a buffer and requires the
                        the FC context is a pointer to the user                                  next one.
                        descriptor list.

 SEQ_ID           8     The sequence ID identifies the received          0                       Hardware updates the SEQ_ID in the
                        sequence number. An FC read or write                                     context table according to the value
                        exchange can be composed of multiple                                     of the SEQ_ID in the incoming frame.
                        sequences depending on the target
                        implementation. The SEQ_ID has a different
                        value for each sequence and does not
                        necessarily increment sequentially. Hardware
                        uses the SEQ_CNT and SEC_ID for checking
                        in-order reception as described in
                        Section 7.11.3.3.7.

 SEQ__CNT        16     SEQ_CNT is an index of the expected FC           Read context: 0         For each in-order reception, hardware
                        frames within a sequence or within the entire    Write context:          sets SEQ_CNT in the context to the
                        exchange. Hardware uses the SEQ_CNT and          SEQ_CNT + 1 of          value of the received SEQ_CNT + 1.
                        SEC_ID for checking in-order reception as        the last packet of
                        described in Section 7.11.3.3.7.                 the same
                                                                         exchange received
                                                                         from the initiator.

 PARAM           32     The PARAM field in the FC header may             Read context: 0         Hardware increments the PARAM by
                        indicate the data offset within the FC IO        Write context: the      the size of the FC payload if it is used
                        exchange. It is indicated as an offset by the    expected received       as an offset. The FC payload size
                        Relative Offset Present bit in the F_CTL field   value                   equals the packet size minus the
                        in the FC header. In this case, the PARAM                                length of its header and trailer. While
                        field indicates the expected value of the next                           the header for this purpose includes
                        received packet.                                                         all bytes starting at the Ethernet
                                                                                                 destination address up to and
                                                                                                 including the basic FC header, the
                                                                                                 trailer includes the FC CRC, FC
                                                                                                 padding, EOF including the three
                                                                                                 reserved bytes, and the Ethernet
                                                                                                 CRC.

 SMAC            48     Source MAC Address of the FCoE sender.           Source MAC              Static Parameter
                        Used to match the source MAC Address of the
                        incoming FCoE packets.
                        The comparison of the SMAC field is enabled
                        by the FCRXCTRL.SMAC_EN bit

 D_ID            24     The D_ID field is configured with the FC         D_ID                    Static Parameter
                        Destination Identification address of the FCoE
                        receiver and is used to match D_ID value of
                        the incoming FCoE packets.
                        The comparison of the D_ID field is enabled
                        by the FCRXCTRL.DID_EN bit

 WRCONTX          1     Write DDP Context. This bit should be set to     WRCONTX                 Static Parameter
                        1 for write exchange context aimed for target
                        (responder) usage. This bit should be set to 0
                        for read exchange context aimed for initiator
                        (originator) usage.

1. During programming time, software should enable first the DMA context. When software disables a context it should invalidate first
   the filter context. See more details on context invalidation in Section 7.11.3.3.10.

333369-009                                                                                                                            559
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

7.11.3.3.7            In Order Reception Checking

Hardware checks in-order reception by SEQ_ID, SEQ_CNT and PARAM fields. These parameters should
meet the expected values (as follows) to pass in-order reception’s criteria.
 • PARAM — When the PARAM field is used as an offset (as indicated by the Relative Offset Present
   bit in the F_CTL field in the FC header), the PARAM field in the received packet should be the same
   as the PARAM field in the FC context. Software should initialize this parameter to the expected
   received value (equals to zero in read exchanges).
 • SEQ_ID, SEQ_CNT — SEQ_ID identifies the FC sequence and SEQ_CNT is the FC frame index
   within the entire exchange or within the sequence (according to specific vendor preference).
   SEQ_CNT in the received packet could be either the same as the SEQ_CNT in the FC context or it
   could start from zero for new SEQ_ID, which is different than the SEQ_ID in the context. Software
   should initialize SEQ_CNT to the expected received value (equals zero in read exchanges). SEQ_ID
   on the first packet is always assumed to be a new value even if by chance it equals to the initial
   value in the context.

7.11.3.3.8            Accessing the Large FC Receive Context

The X550 supports a large number of FC contexts while each context contains about 16 bytes. To save
consumed memory space, the FC context is accessed by indirect mapping. This section describes how
the DMA and filter contexts are accessed. The DMA context is consist of the FCPTRL, FCPTRH and
FCBUFF registers while read and write accesses are controlled by the FCDMARW register. The filter
context is consist of the FCFLT register while read and write accesses are controlled by the FCFLTRW
register.
 • Indirect DMA Context Programming — Software should program the FCPTRL, FCPTRH and
   FCBUFF registers by the required setting. It then programs the FCDMARW register with the
   following content:
      — FCOESEL should be set by the required context index (OX_ID or RX_ID values)
      — The WE bit is set to 1b for write access while the RE bit is set to 0b. LASTSIZE should be set to
        the relevant value for the context
 • Indirect DMA Context Read — Software should program the FCDMARW register as follows and
   then read the context on the FCPTRL, FCPTRH, FCBUFF and FCDMARW registers
      — FCOESEL should be set by the required context index (OX_ID or RX_ID values).
      — RE bit should be set to 1b for read access while WE, and LASTSIZE fields are set to 0b.
        LASTSIZE should be set to 0b. It is ignored by hardware when the RE bit is set to 1b. When
        reading FCDMARW the LASTSIZE field reflects the context content.
      The FC context may handle up to 1024 user buffers in a DDP request.
 • Direct DMA Context Access — Software can access the FCoE DMA context directly for reading or
   programming through the FCDDC registers, each 4 consecutive DWs represent a separate FCoE
   Context:
      — DW[4*n]: FCPTRL[n]
      — DW[4*n+1]: FCPTRH[n]
      — DW[4*n+2]: FCBUFF[n]
      — DW[4*n+3]: FCDMARW[n]

560                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • Indirect Filter Context Programming — Software should program the FCFLT register by the
   required setting. It then programs the FCFLTRW register with the following content:
     — FCOESEL should be set by the required context index (OX_ID or RX_ID values).
     — WE bit is set to 1b for a write access while RE bit is set to 0b.
 • Direct Filter Context Access — Software can access the FCoE Filter Context directly for reading
   or programming through the FCDFC, FCDFCD registers. FCDFCD has a DW per context while FCDFC
   is structured such that each 4 consecutive DWs represent a separate FCoE context:
     — FCDFC:
           • DW[4*n]: FCFLT[n]
           • DW[4*n+1]: FCPARAM[n]
           • DW[4*n+2]: FCSMAC[n]
           • DW[4*n+3]: FCFLTRW[n]
     — FCDFCD:
           • DW[n]: FC D_ID
 • Indirect Filter Context Read — Software should program the FCFLTRW register as follows and
   then read the context on the FCFLT register:
     — FCOESEL should be set by the required context index (OX_ID or RX_ID values).
     — RE bit should be set to 1b for a read access while WE bit is set to 0b.
     Software should access the FCoE context either through the direct access type or indirect access
     type. Software mixing the access type accesses results in un-defined outcome.

7.11.3.3.9                User Descriptor Structure and User Descriptor List

The buffers in host memory could be either user application memory or storage cache named as user
buffers. In both cases the buffers must be locked (against software) and converted to physical memory
up front.
The user descriptor list is a contiguous list of pointers to the user buffers. The buffers are aligned to
their size as defined in the FC context. The first buffer can start a non-zero offset as the software
defines it in the FC context. All other buffers start at a zero offset. The last buffer can be smaller than
the full size as defined in the FC context.

Table 7-84. FC User Descriptor
63                                                                                                                                  0

User buffer address defined in byte units. N LS bits must be set to zero while N equals 12 for a 4 KB buffer size, 13 for 8 KB buffer
size, 14 for 16 KB buffer size and 16 for 64 KB buffer size.

333369-009                                                                                                                        561
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

7.11.3.3.10          Invalidating FC Read Context

During nominal activity, hardware invalidates autonomously the FC contexts. The target indicates a
completion of an FC read by sending the FCP_RSP frame. Hardware identifies the FCP_RSP frame and
invalidates the FC context that matches the OX_ID in the incoming frame. The FCP_RSP frame is posted
to the legacy Rx queues with appropriate status indication. Hardware identifies the FCP_RSP frame by
the following criteria:
 • The frame is identified as FCoE frame by its Ethernet type
 • R_CTL.Information (least significant four bits) equals 0x7 (command status)
 • R_CTL.Routing (most significant four bits) equals 0x0 (device data)
Context that is invalidated autonomously by hardware is indicated by setting the FCSTAT field in the
receive descriptor to 10b. When software gets this indication it can unlock the user buffers instantly and
re-use the context for a new FC exchange.
In some erroneous cases software might invalidate a context before a read exchange completes (such
as a time out event). In such cases, software should clear the Filter Context Valid bit and then the DMA
Context Valid bit. Hardware invalidates the context at a packet's boundaries. Therefore, after software
clears the DMA Context Valid bit, software should either poll it until it is granted (cleared) by hardware
or optionally software could wait ~100 s (guaranteed time for any associated DMA cycles to
complete). In addition, software should also ensure that the receive packet buffer does not contain any
residual packets of the same flow. See Section 4.6.7.1.1 for the required software flow. Only then the
software can unlock the user buffers and re-use the context for a new FC exchange.
Note:     While RXCTRL.RXEN is in the disabled state, frames from the DDP filter logic may be dropped
          silently by the device. Therefore, prior to clearing RXCTRL.RXEN bit, any outstanding or active
          DDP context should be invalidated and those associated DDP I/O read requests retried.

7.11.3.3.11          Invalidating FC Write Context

During nominal activity, hardware invalidates autonomously the FC contexts. The initiator indicates a
completion of a granted portion of an FC write by sending a data frame with active sequence initiative
flag. After receiving this type of frame, hardware invalidates the matched FC context. The header of this
frame is posted to the legacy Rx queues with appropriate status indication. Hardware identifies this
frame by the following criteria:
 • The frame is identified as FCoE frame by its Ethernet type
 • R_CTL — Information (least significant four bits) equals 0x1 (solicited data).
 • R_CTL — Routing (most significant four bits) equals 0x0 (device data).
 • F_CTL — Sequence initiative equals 1b indicating transfer initiative to the target.
 • F_CTL — End sequence equals 1b, indicating last frame in a sequence.
Context that is invalidated autonomously by hardware is indicated by setting the FCSTAT field in the
receive descriptor to 10b. When software gets this indication, it can unlock the user buffers instantly
and re-use the context for a new FC exchange. If the FC write is not complete, software can re-use the
same context for the completion of the exchange. It can also define a new user buffer list and indicate
it to hardware by programming the DMA context. It then can enable the filter context by setting the
Re-Validation bit the WE bit and the FCOESEL field in the FCFLTRW register.
Software can also invalidate a context in case of a time out event or other reasons. Software
invalidation flow is described in Section 7.11.3.3.10.

562                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.11.3.3.12              OX_ID and RX_ID Pool Management

As previously indicated, hardware enables Large FC receive offload for up to 2048 concurrent
outstanding read or write requests. In some cases more than 2048 concurrent outstanding requests are
generated by the FCoE stack. Therefore, software might need to manage two separate queues for the
requests: one queue for those FC requested supported by the large FC receive offload and another one
for those requests that do not gain the large FC receive offload. Software should claim an entry in the
context table, and its associated OX_ID or RX_ID for the duration of the read or write requests,
respectively. Once a request completes and its context is invalidated, software can re-use its context
entry for a new request.
Table 7-85 defines an example for an OX_ID list that can be used for new FC read requests managed by
software at initialization time and during run time. Similarly, this table could be helpful for write
requests and their RX_ID or shared pool for both read and write requests.

Table 7-85. Software OX_ID Table
 Init State of                  Updated State                       Updated State                          Updated State
                  Run-Time                         Run-Time                             Run-Time
  the OX_ID                     of the OX_ID                        of the OX_ID                           of the OX_ID
                   Events                           Events                               Events
     Table                          Table                               Table                                  Table

# 0 Software is         50         The following FC         50         Software is using

                 using 50                       read requests are                   additional 50 OX_ID

# 1 OX_ID values        51         completed (and           51         values supported by

                 supported by                   released by                         large FC receive.
     ...         large FC            ...        software) in the         ...                                    ...
                                                                                    The following FC
                 receive.                       following order:                    read requests are
     ...                             ...        44, 21, 9, 0.            ...                                   2046
                                                                                    completed (and
     ...                             ...                                 ...        released by                2047
                                                                                    software) in the
     ...                            2046                                2046        following order: 75,        44
                                                                                    10, 38.
     ...                            2047                                2047        Ordering between            21
                                                                                    software requests
     ...                                                                 44         and releases does            9
                                                                                    not matter in this
     ...                                                                 21                                      0
                                                                                    example.
     ...                                                                  9                                     75

     2046                                                                 0                                     10

     2047                                                                                                       38

Note:        Software is aware of which read requests can be offloaded by the large FC receive and use
             OX_IDs in the hardware range (0 to 2047) only for those ones.

7.11.3.3.13              Packets and Headers Indication in the Legacy Receive
                         Queue

The following packets or packet’s headers are posted to the legacy receive queues:
 • All FCoE frames that are not offloaded by the DDP logic
 • Any packet with exception errors as described in Section 7.11.3.3.14
 • Headers of packets posted to the user buffers by the DDP logic that contain meaningful data (as
   detailed in Section 7.11.3.3.2 and Section 7.11.3.3.3)
There are a few new fields in the receive descriptor dedicated to FCoE described in Section 7.1.5.2.2:
 • Packet Type — FCoE packets are identified by their Ethernet type that is programmed in the ETQF
   registers.

333369-009                                                                                                            563
                                   Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                Inline Functions

 • FCoE_PARAM — Reflects the value of the PARAM field in the DDP context.
 • FCSTAT — FCoE DDP context indication.
 • FCERR — FCoE Error indication. DDP offload is provided only when no errors are found.
 • FCEOFs and FCEOFe — Status indication on the EOF and SOF flags in the Rx packet.

7.11.3.3.14               Exception Handling

Table 7-86 lists the exception errors related to FC receive functionality. Packets with any of the following
exception errors are posted to the legacy receive queues with no DDP unless specified differently. In
these cases, the exception error is indicated in the Extended Error field in the receive descriptor. The
exceptions are listed in priority order in the table with highest priority first. Other than the EOF
exception, any high priority exception hides all other ones with a lower priority.

Table 7-86. Exception Error Table
              Event Description                                                Actions and Indications

Unsupported FCoE version (Rx Version >              The packet is identified as an FCoE packet type. DDP context parameters are
FCRXCTRL.FCOEVER)                                   left intact. Speculative CRC check is done. The packet is posted to legacy Rx
                                                    queue (unless CRC is incorrect and FCRXCTRL.SAVBAD is not set). If the packet
                                                    matches the FCoE redirection table, the packet is posted to Rx queue index
                                                    defined by its OX_ID.
                                                      RDESC.STATUS.FCSTAT = 00b.
                                                      RDESC.ERRORS.FCERR = 100b.

Rx packet with ESP option header.                   If it matches the DDP context, auto invalidate the filter context while keeping
                                                    the parameters intact. Note that this exception is not expected since software
                                                    should not enable a context to an exchange that uses ESP encapsulation.
                                                      RDESC.STATUS.FCSTAT = 00b / 01b / 10b.
                                                      RDESC.ERRORS.FCERR = 000b.

Received EOFa or EOFni or any unrecognized          If it matches the DDP context, auto invalidate the filter context while keeping
EOF or SOF flags.                                   the parameters intact.
                                                      RDESC.STATUS.FCSTAT = 00b / 01b / 10b.
                                                      RDESC.ERRORS.FCERR = 010b (even if no DDP match).
                                                      RDESC.ERRORS.FCEOFe = 1b.
                                                      RDESC.STATUS.FCEOFs = 1b.

Received non-zero abort sequence condition in       If it matches the DDP context, auto invalidate the filter context while keeping
FC read exchange.                                   the parameters intact.
                                                      RDESC.STATUS.FCSTAT = 00b / 01b / 10b.
                                                      RDESC.ERRORS.FCERR = 010b (even if no DDP match).

Out of order reception of packet that matches a     Auto invalidate the filter context while keeping the parameters intact.
DDP context1.                                        RDESC.STATUS.FCSTAT = 01b.
                                                     RDESC.ERRORS.FCERR = 100b.

Received unexpected EOF / SOF:                      No DDP while filter context is updated (if matched and other parameters are in
1) New sequence ID and SOF is not SOFi.             order).
2) Last packet in a sequence and EOF is not          RDESC.STATUS.FCSTAT = 00b / 01b / 10b.
EOFt.                                                RDESC.ERRORS.FCERR = 000b.
                                                     RDESC.ERRORS.FCEOFe = 1b.
                                                     RDESC.STATUS.FCEOFs = 0b.

The DMA unit gets FCoE packets while it missed      Filter context parameters are updated while DMA context parameters are left
the packet that was marked as first by the filter   intact.
unit2.                                                RDESC.STATUS.FCSTAT = 01b / 10b / 11b.
                                                      RDESC.ERRORS.FCERR = 011b or 101b.

Last user buffer is exhausted (not enough space     The filter context is updated while DMA context is auto invalidated.
for the FC payload).                                 RDESC.STATUS.FCSTAT = 01b / 10b / 11b.
                                                     RDESC.ERRORS.FCERR = 101b.

564                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-86. Exception Error Table [continued]
               Event Description                                              Actions and Indications

 Legacy receive queue is not enabled or no legacy   The entire packet is dropped. Auto invalidates the DMA context while the filter
 receive descriptor.                                context remains active and continues to be updated regularly. Once legacy
                                                    descriptors become valid again, packets are posted to the legacy queues with
                                                    the following indication.
                                                     RDESC.STATUS.FCSTAT = 01b / 10b / 11b.
                                                     RDESC.ERRORS.FCERR = 101b.

 Packet missed (lost) by the Rx packet buffer.      The entire packet is dropped (by the Rx packet buffer). Auto invalidate the DMA
 Normally a case when flow control is not enabled   context while the filter context remains active and continues to be updated
 or flow control does not work properly.            regularly. Once the Rx packet buffer gets free, further Rx packets are posted to
                                                    the legacy queues with the following indication.
                                                     RDESC.STATUS.FCSTAT = 01b / 10b / 11b.
                                                     RDESC.ERRORS.FCERR = 110b.
                                                    Note that software might ignore this error when FCSTAT equals 00b.

1. Out of order might be one of the following cases. SEQ_CNT does not meet expected value. The PARAM field in the Rx packet does
   not match the DDP context. SEQ_ID keeps the same value as the previous packet in a new sequence identified by the presence of
   SOFi code in the SOF field. The SOFi is not found in the first FC frame in a context.
2. Lost sync between Filter and DMA contexts could be a result of context invalidation by software together with misbehaved target
   that sends packet with no host request.

7.11.3.3.15               FC Exchange Completion Interrupt

One of the performance indicators of an initiator is measured by the number of I/O operations per
second it can generate. The number of FC exchanges per second is affected mainly by the CPU
overhead associated with the FC exchange processing and software latencies. The number of
concurrent outstanding FC exchanges supported by large FC receive is limited by hardware resources.
Reducing the latency associated with processing completions increases the number of FC exchanges per
second that the system supports.
