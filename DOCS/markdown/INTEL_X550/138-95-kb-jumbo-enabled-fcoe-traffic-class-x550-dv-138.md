## 9.5 KB Jumbo Enabled                           FCoE Traffic Class                                X550 DV

                   No                                           No                                          5 KB

                   No                                          Yes                                          7 KB

                   Yes                                          No                                         21 KB

                   Yes                                         Yes                                          7 KB

333369-009                                                                                                                       133
                                      Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

3.7.4.3.5            Packet Buffer Size

When FC is enabled, the total size of a TC packet buffer must be large enough for the Low and high
thresholds. To avoid constant transmission of XOFF and XON frames it is recommended to add some
space for hysteresis type of behavior. The difference between the two thresholds is recommended to be
at least one frame size (when 9.5 KB jumbo frames are expected over the TC) and larger than a few
frames in other cases (4.5 KB for instance). If the available Rx buffer is large enough, it is
recommended to increase as much as possible the hysteresis budget. If the available Rx buffer is not
large enough it might be required to cut both the low threshold as well as the hysteresis budget.
 • For a PFC-enabled TC:
      — FCRTH = FCRTL + hysteresis budget = FCRTL + Max (MaxFrame(TC), 4.5 x 1024 B)
      — Rx Packet Buffer size = FCRTH + the X550 DV (see Section 3.7.4.3.3)
 • For a best effort TC:
      — Rx Packet Buffer size = FCRTL, as the same considerations than described in Section 3.7.4.3.4
        play here to avoid bubbles over PCIe
The total Rx Packet Buffer size available to a port for all its supported TCs is either 384 KB, 320 KB, or
256 KB, depending on the size allocated to the Flow Director table, 0 KB, 64 KB, or 128 KB,
respectively.
Table 3-46 assumes four PFC-enabled Traffic Classes are defined over the port, of which two are
allocated to FCoE traffic and two for other loss less traffic types like iSCSI, etc. The table lists the
recommended settings for the supported combinations. When less than 4 PFC-enabled TCs are defined,
and/or when less than 8 TCs are defined, it is recommended to refer to the setting rules described in
this section, in Section 3.7.4.3.3, and in Section 3.7.4.3.4. Note that reducing the number of TCs of a
port to what is really needed, helps increasing the port’s throughput.

Table 3-46. Some Recommended Rx Packet Buffer Settings
                                                                                         Packet Buffer Size of Any
 Flow Director   9.5 KB Jumbo    Packet Buffer Size of Any   Packet Buffer Size of Any
                                                                                              of the Other 2
   Table Size       Enabled       of the 4 Best Effort TCs      of the 2 FCoE TCs
                                                                                             PFC-Enabled TCs

       No             Yes                 33 KB                       62 KB                       61 KB
                                                                   FCRTL = 7 KB                FCRTL = 6 KB
                                                                  FCRTH = 37 KB               FCRTH = 37 KB

       No             Yes                 27 KB                       52 KB                       86 KB
                                                                   FCRTL = 7 KB               FCRTL = 21 KB
                                                                  FCRTH = 17 KB               FCRTH = 36 KB

       No             No                  32 KB                       64 KB                       63 KB
                                                                   FCRTL = 7 KB                FCRTL = 6 KB
                                                                  FCRTH = 37 KB               FCRTH = 36 KB

       No             Yes                 22 KB                       57 KB                       91 KB
                                                                   FCRTL = 7 KB               FCRTL = 21 KB
                                                                  FCRTH = 12 KB               FCRTH = 31 KB

    64 KB           No                  25 KB                       54 KB                       53 KB

                                                                   FCRTL = 7 KB                FCRTL = 6 KB
                                                                  FCRTH = 29 KB               FCRTH = 29 KB

    64 KB           Yes                 19 KB                       44 KB                       78 KB

                                                                   FCRTL = 6 KB               FCRTL = 20 KB
                                                                   FCRTH = 9 KB               FCRTH = 28 KB

    64 KB           No                  24 KB                       56 KB                       55 KB

                                                                   FCRTL = 7 KB                FCRTL = 6 KB
                                                                  FCRTH = 29 KB               FCRTH = 28 KB

134                                                                                                     333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-46. Some Recommended Rx Packet Buffer Settings [continued]
                                                                                                     Packet Buffer Size of Any
  Flow Director     9.5 KB Jumbo       Packet Buffer Size of Any      Packet Buffer Size of Any
                                                                                                          of the Other 2
    Table Size         Enabled          of the 4 Best Effort TCs         of the 2 FCoE TCs
                                                                                                         PFC-Enabled TCs

    64 KB               Yes                      14 KB                        49 KB                           83 KB

                                                                             FCRTL = 3 KB                   FCRTL = 18 KB
                                                                             FCRTH = 4 KB                   FCRTH = 23 KB

     128 KB                No                      17 KB                         46 KB                          45 KB
                                                                              FCRTL = 7 KB                   FCRTL = 6 KB
                                                                             FCRTH = 21 KB                  FCRTH = 21 KB

     128 KB                No                      16 KB                         48 KB                          47 KB
                                                                              FCRTL = 7 KB                   FCRTL = 6 KB
                                                                             FCRTH = 21 KB                  FCRTH = 20 KB

Notes:
 1. In some of the cases above, it has been necessary to get compromised on the rules for hysteresis and FCRTL to fit the size
    available for Rx packet buffer.
 2. In some other cases, after having applied all the rules there was an exceeding available Rx packet buffer left which has been
    used to extend the hysteresis budgets.
 3. In all cases, FCRTH rule has been applied as is, since compromising on it is not allowed and extending it provides no
    performance benefits.

#### 3.7.4.4 Link FC in DCB Mode

When operating in DCB mode, PFC is the preferred method of getting the best use of the link for all TCs.
When connecting to switches that do no support (or enable) PFC, the X550 can also throttle the traffic
according to incoming link FC notifications. Following is the required device setting and functionality.
 • The X550 should be set to legacy link FC by setting MFLCN.RFCE.
 • Receive XOFF pauses transmission in all TCs.
 • Crossing the Rx buffer high threshold on any TC generates XOFF transmission. Each TC can have its
   own threshold configured by the FCRTH[n] registers.
 • Crossing the Rx buffer Low threshold on any TC generates XON transmission. This behavior is
   undesired. Therefore, software should not enable XON in this mode by clearing FCRTL[n].XONE bits
   in all TC.
 • The FCTTV of all TCs must be set to the same value.

### 3.7.5 Inter Packet Gap (IPG) Control and Pacing

The X550 supports transmission pacing by extending the IPG (the gap between consecutive packets).
The pacing mode enables the average data rate to be slowed in systems that cannot support the full
link rate (10 GbE, 1 GbE or 100 Mb/s). As listed in Table 3-47, the pacing modes work by stretching the
IPG in proportion to the data sent. In this case the data sent is measured from the end of preamble to
the last byte of the packet. No allowance is made for the preamble or default IPG when using pacing
mode.

Example 1:
    Consider a 64-byte frame. To achieve a 1 GbE data rate when link rate is 10 GbE and packet length
    is 64 bytes (16 DWords), add an additional IPG of 144 DWords (nine times the packet size to reach

# 1 GbE). When added to the default IPG gives an IPG of 147 DWords.

333369-009                                                                                                                     135
                                      Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

Example 2:
      Consider a 65-byte frame. To achieve a 1 GbE data rate when link rate is 10 GbE and packet length
      is 65 bytes (17 DWords when rounded up) add an additional IPG of 153 DWords (nine times the
      packet duration in DWords). When added to the default IPG gives an IPG of 156 DWords. Note that
      in this case, where the packet length counted in DWords is not an integer, count any fraction of a
      DWord as an entire DWord for computing the additional IPG.
Table 3-47 lists the pacing configurations supported by the X550 at link rates of 10 GbE. When
operating at lower link speeds the pacing speed is proportional to the link speed.

Table 3-47. Pacing Speeds at 10 GbE Link Speed
         Pacing Speeds (Gb/s)              Delay Inserted into IPG                    Register Value

# 10 (LAN)                              None                                  0000b

            9.294196 (WAN)                  1 byte for 13 transmitted                      1111b

                 9.0                       1 DWord for 9 transmitted                       1001b

                 8.0                       1 DWord for 4 transmitted                       1000b

                 7.0                       3 DWords for 7 transmitted                      0111b

                 6.0                       2 DWords for 3 transmitted                      0110b

                 5.0                       1 DWords for 1 transmitted                      0101b

                 4.0                       3 DWords for 2 transmitted                      0100b

                 3.0                       7 DWords for 3 transmitted                      0011b

                 2.0                       4 DWords for 1 transmitted                      0010b

                 1.0                       9 DWords for 1 transmitted                      0001b

# 10 None                                 Default

Pacing is configured in the PACE field of the Pause and Pace (PAP) register.

136                                                                                                    333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

Chapter 4                         Initialization
