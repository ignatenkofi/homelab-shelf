## 7.7 Time SYNC (IEEE1588 and 802.1AS)

### 7.7.1 Overview

IEEE 1588 addresses the clock synchronization requirements of measurement and control systems. The
protocol supports system-wide synchronization accuracy in the sub-microsecond range with minimal
network and local clock computing resources. The protocol is spatially localized and allows simple
systems to be installed and operate.
The IEEE802.1AS standard specifies the protocol used to ensure that synchronization requirements are
met for time sensitive applications, such as audio and video, across Bridged and Virtual Bridged Local
Area Networks consisting of LAN media where the transmission delays are almost fixed and
symmetrical; for example, IEEE 802.3 full duplex links. This includes the maintenance of synchronized
time during normal operation and following addition, removal, or failure of network components and
network re-configuration. It specifies the use of IEEE 1588 specifications where applicable.
Note:     The time sync mechanism activation is possible in full-duplex mode only and is not supported
          at 100 Mb/s link speed.
Note:     The clock used for Time Sync is a 80 MHz clock, so the limit of the accuracy of all Time Sync
          operations is 12.5 ns.

### 7.7.2 Flow and Hardware/Software Responsibilities

The operation of a Precision Time Protocol (PTP) enabled network is divided into two stages:
initialization and time synchronization.
At the initialization stage, every master-enabled node starts by sending sync packets that include the
clock parameters of its clock. Upon receipt of a sync packet, a node compares the received clock
parameters to its own and if the received parameters are better, then this node moves to a slave state
and stops sending sync packets. While in slave state, the node continuously compares the incoming
packet to its currently chosen master and if the new clock parameters are better, than the master
selection is transferred to this master clock. Eventually the best master clock is chosen. Every node has
a defined time-out interval that if no sync packet was received from its chosen master clock it moves
back to a master state and starts sending sync packets until a new best master clock (PTP) is chosen.
The time synchronization stage is different to master and slave nodes. If a node is in a master state it
should periodically send a sync packet that is time stamped by hardware on the Tx path (as close as
possible to the PHY). After the sync packet, a Follow_Up packet is sent that includes the value of the
time stamp kept from the sync packet. In addition, the master should time stamp Delay_Req packets
on its Rx path and return to the slave that sent the time stamp value using a Delay_Response packet. A
node in a slave state should time stamp every incoming sync packet and if it came from its selected
master, software uses this value for time offset calculation. In addition, it should periodically send
Delay_Req packets to calculate the path delay from its master. Every sent Delay_Req packet sent by
the slave is time stamped and kept. With the value received from the master with Delay_Response
packet, the slave can now calculate the path delay from the master to the slave. The synchronization
protocol flow and the offset calculation are shown in Figure 7-36.

492                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                             Master                        Slave
                             T0                                 T0 + delta T

                             T1
                                             Sync                           Master to Slave
                                                                T2        Transmission delay
                                        Follow_U
                                                p(T1)

                                                                T3
                                                  q                        Slave to Master
                             T4            Dely_Re                       Transmission delay
                                                 (T3)
                                        Follow_Up

                                     Delay_R                             T1, T2, T3 and T4
                                            esponse
                                                   (T4)                  are sampled by the HW

                   Calculated delta T = [(T2-T1)-(T4-T3)]/2 // assuming symmetric transmission delays
                   Toffset = - delta T // offset at the Slave

Figure 7-36. Sync Flow and Offset Calculation

Hardware responsibilities are:
1. Identify the packets that require time stamping.
2. Time stamp the packets on both Rx and Tx paths.
3. Store the time stamp value for software.
4. Keep the system time in hardware and give a time adjustment service to software.
5. Maintain auxiliary features related to the system time.
Software responsibilities are:
1. Manageability controller protocol execution, which means defining the node state (master or slave)
   and selection of the master clock if in slave state.
2. Generate PTP packets, consume PTP packets.
3. Calculate the time offset and adjust the system time using a hardware mechanism for that.
4. Enable configuration and usage of the auxiliary features.

                                        Action                                                 Responsibility   Node Role

Generate a sync packet with time stamp notification in the descriptor.                            Software       Master

Time stamp the packet and store the value in registers (T1).                                     Hardware        Master

Time stamp incoming sync packet, store the value in register                                     Hardware         Slave

Read the time stamp from register put in a Follow_Up packet and send.                             Software       Master

Once received, the Follow_Up store T2 from registers and T1 from Follow_up packet.                Software        Slave

Generate a Delay_Req packet with time stamp notification in the descriptor.                       Software        Slave

Time stamp the packet and store the value in registers (T3).                                     Hardware         Slave

Time stamp incoming Delay_Req packet, store the value in register                                Hardware        Master

333369-009                                                                                                                  493
                                      Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                               Inline Functions

                                       Action                                              Responsibility       Node Role

Read the time stamp from register and send back to slave using a Delay_Response               Software            Master
packet.

Once received, the Delay_Response packet calculate offset using T1, T2, T3 and T4             Software            Slave
values.

#### 7.7.2.1 Time Sync Indications in Rx and Tx Packet Descriptors

Some indications need to be transferred between software and hardware regarding PTP packets. On the
Tx path, software should set the 1588 bit in the Tx packet descriptor (bit 9). On the Rx path, hardware
has two indications to transfer to software, one is to indicate that this packet is a PTP packet (whether
time stamp is taken or not). This is also for other types of PTP packets needed for management of the
protocol and this bit is set only for the L2 type of packets (the PTP packet is identified according to its
EtherType). PTP packets have the L2 Packet bit in the packet type field set (bit 11 in the receive
descriptor) and the EtherType matches the filter number set by software in the ETQF registers to filter
PTP packets. The UDP type of PTP packets do not need such indication since the port number (319 for
event and 320 all the rest PTP packets) directs the packets toward the time sync application. The
second indication is RDESC.STATUS.TS (bit 16) to indicate to software that time stamp was taken for
this packet. Software needs to access the time stamp registers to get the time stamp values.

### 7.7.3 Hardware Time Sync Elements

All time sync hardware elements are reset to their initial values (as defined in Section 8.2.2.21) upon
Master reset. Upon change in link speed some of the time sync parameters should be changed
accordingly.

#### 7.7.3.1 System Time Structure and Mode of Operation

The SYSTIME is a 96 bit register is composed of: SYSTIMR, SYSTIMEL and SYSTIMEH registers: The
SYSTIMR register holds the sub-nanosecond fraction, the SYSTIMEL register holds the nanosecond
fraction and the SYSTIMEH register holds the sec fraction of the time (note that the upper two bits of
the SYSTIMEL register are always zero while the max value of this register is 999,999,999 decimal).
 • Initial Setting — Setting the initial time is done by direct write access to the SYSTIME register.
   Software should set first the SYSTIMEL and then set the SYSTIMEH. Setting the SYSTIMR is
   meaningless while it represents sub-nanosecond units.
 • Run Time — During run time the SYSTIME timer value in the SYSTIMEH, SYSTIMEL and SYSTIMR
   registers, is updated periodically each 12.5 ns clock cycle according to the following formula:
      — Define: INC_TIME == 12.5 ns +/- TIMINCA.Incvalue * 2-32 ns. Add or subtract the
        TIMEINCA.INCVALUE is defined by TIMINCA.ISGN (where 0b means Add and 1b means
        Subtract)
      — Then: SYSTIME = SYSTIME + INC_TIME
 • Reading the SYSTIME register by software is done by the following sequence:
      — Read the SYSTIMEL register.
      — Read the SYSTIMEH register.

494                                                                                                                333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • Dynamic update of SYSTIME registers is done by using the TIMADJ registers by the following
   flow:
     — Write the TADJL value and its SIGN to the TIMADJ register (the SIGN bit indicates if the TADJL
       value should be added or subtracted).
     — Following the write access to the TIMADJ register, the hardware repeats the following two steps
       at each 12.5 ns clock as long as the Tadjust > 0.
          • SYSTIME = SYSTIME + INC_TIME +/- 1 ns. Add or subtract 1 ns is defined by
            TIMADJ.Sign (where ‘0’ means Add and ‘1’ means Subtract).
          • TADJL = TADJL - 1 ns
     — As shown above, the time adjustment might take multiple clocks. Software might write a new
       value to the TIMADJ register before the hardware completed the previous adjustment. In such a
       case, the new value written by software, overrides the above equation. If such a race is not
       desired, the software could check that the previous adjustment is completed by one of the
       following methods:
          • Wait enough time before accessing the TIMADJ register which guarantees that the previous
            update procedure is completed.
          • Poll the matched TSICR.TADJ flag which is set by the hardware each time the update
            procedure is completed.

#### 7.7.3.2 Time Stamping Mechanism

The time stamping logic is located as close as possible to the PHY. Figure 7-37 shows the exact point in
time where the time value is captured by the hardware relative to the packet content. This is to reduce
delay uncertainties originated from implementation differences. As the time stamp is sampled at a very
late phase in the data path, the X550 does not insert it to the transferred packet. Instead, the X550
supports the two-step operation as follows for Tx and Rx.
Note:        As the time stamping logic is located at the MAC/PHY interface, there is no timestamping of
             packets when MAC loopback is activated.

Figure 7-37. Time Stamp Point

333369-009                                                                                            495
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

7.7.3.2.1            Single Tx Time Stamping

The time stamp logic is activated if enabled by the TSYNCTXCTL.EN bit and the time stamp bit in the
packet descriptor is set. In this case, hardware captures the packet's transmission time in the TXSTMPL
and TXSTMPH registers. Software is responsible to read the transmission time and append it in the
Folow_Up packet as shown in Figure 7-36.

7.7.3.2.2            Single Rx Time Stamping

On the Rx, this logic parses the traversing frame. If it is matching the message type defined in RXMTRL
register and the TSYNCRXCTL.TYPE field, and timestamping is enabled by the TSYNCRXCTL.EN bit the
reception time stamp is stored in the RXSTMPL and RXSTMPH registers. In addition, the TS status bits
is reported in the Rx descriptor to identify that a time stamp was taken for this packet (stored in the
RXSTMPL and RXSTMPH registers).
Note:     The time stamp values are locked in the RXSTMPL and RXSTMPH registers until software
          accesses them. As long as software does not read these registers, hardware does not capture
          the time stamp of further Rx packets. To avoid potential deadlocks, it is recommended that
          software read the Rx time stamp registers at some time after sync or Delay_Req packets are
          expected. It would overcome erroneous cases on which the hardware latches a packet
          reception time while the packet's content was not posted properly to the software. Master
          software must not initiate consecutive sync requests before the previous response is
          received.
Note:     If TSYNCRXCTL.TYPE = 4 (sample time stamp of all packets), the timestamps are not locked
          in the RXSTMPL and RXSTMPH registers, and each new packet timestamp is stored in these
          registers.

7.7.3.2.3            Multiple Rx Time Stamping

Packets that are identified to be time stamped by hardware are also indicated by the TS or TSIP flags in
the receive descriptors. If the TS flag is set, the packet reception time is sampled by the hardware in
the RXSTMPL/H registers (see Single Rx Time Stamping above). These registers are locked till the
software reads its value. If the TSIP flag is set, the packet reception time is posted to the packet buffer
in host memory. For more information about posting the time stamp in the receive buffer refer to
Section 7.1.6.2.

### 7.7.4 Hardware Time Sync Elements

All time sync hardware is initialized as defined in the registers section upon MAC reset. The time sync
logic is enabled if the TSAUXC.Disable systime flag is cleared.
The 1588 logic includes multiple registers larger than 32 bits which are indicated as xxxL (Low portion -
LS) and xxxH (High portion - MS). When software accesses these registers (either read or write) it
should access first the xxxL register (LS) and only then the xxxH register (MS). Accessing the xxxH
might impact the hardware functionality which should be triggered only after both portions of the
register are valid.

496                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.7.4.1 Target Time

The two target time registers TRGTTIMEL0/H0 and TRGTTIMEL1/H1 enable generating a time triggered
event to external hardware using one of the SDP pins according to the setup defined in the TSSDP and
TSAUXC registers. Each target time register is structured the same as the SYSTIMEL/H registers. If the
value of SYSTIMEL/H is equal or larger than the value of the TRGTTIMEL/H registers, a change in level
or a pulse is generated on the matched SDP outputs.

7.7.4.1.1              SYSTIM Synchronized Level Change Generation on SDP Pins

To generate a level change on one of the SDP pins when System Time (SYSTIM) reaches a pre-defined
value, the driver should do the following:
1. Select a specific SDP pin by setting the TSSDP.TS_SDPx_EN flag to 1b (where ‘x’ is 0, 1, 2 or 3).
2. Assign a target time register to the selected SDP by setting the TSSDP.TS_SDPx_SEL field to 00b or
   01b if level change should occur based on TRGTTIMEL0/H0 or TRGTTIMEL1/H1, respectively.
3. Define the selected SDPx pin as output, by setting the appropriate SDPx_IODIR bit in the ESDP
   register (where ‘x’ is 0, 1, 2, or 3).
4. Define that this SDP is used for TimeSync function by setting the appropriate SDPx_NATIVE bit in
   the ESDP register (while ‘x’ is 0, 1, 2, or 3). If used with SDP1, clear ESDP.SDP1_FUNCTION field.
5. Program the target time TRGTTIMELx/Hx to the required event time (where ‘x’ is 0 or 1).
6. Program the TRGTTIMELx/Hx to “Level Change” mode by setting the TSAUXC.PLSG0 bit to 0b and
   TSAUXC.EN_TTx bit to 1b (where ‘x’ is 0 or 1).
7. To make this a one time operation, the TSAUXC.DIS_TS_CLEAR field should be cleared.
8. When the SYSTIMEL/H registers become equal or larger than the selected TRGTTIML/H registers,
   the selected SDP changes its output level.

7.7.4.1.2              SYSTIM Synchronized Pulse Generation on SDP Pins

An output pulse can be generated by using one of the target time registers to define the beginning of
the pulse and the other target time registers to define the pulse completion time. To generate a pulse
on one of the SDP pins when System Time (SYSTIM) reaches a pre-defined value, the driver should do
the following:
1. Select a specific SDP pin by setting the TSSDP.TS_SDPx_EN flag to 1b (where ‘x’ is 0, 1, 2 or 3).
2. Set TSSDP.TS_SDPx_SEL field to 00b to define that the TRGTTIMEL0/H0 register defines the start of
   pulse time, and the TRGTTIMEL1/H1 register defines the end of pulse time.
3. Define the selected SDPx pin as output, by setting the appropriate SDPx_IODIR bit in the ESDP
   register (where ‘x’ is 0, 1, 2, or 3).
4. Define that this SDP is used for TimeSync function by setting the appropriate SDPx_NATIVE bit in
   the ESDP register (where ‘x’ is 0, 1, 2, or 3). If used with SDP1, clear ESDP.SDP1_FUNCTION field.
5. Program the target time TRGTTIMELx/Hx to the required event time (while ‘x’ is 0b or 1b).
6. TRGTTIMEL0/H0 should be set to a lower value than TRGTTIMEL1/H1.
7. Program the TRGTTIMEL0/H0 defined by the TSSDP.TS_SDPx_SEL to “Start of Pulse” mode by
   setting the TSAUXC.PLSG0 bit to 1b and TSAUXC.EN_TT0 bit to 1b (where ‘x’ defines the SDP
   used). The TRGTTIMEL1/H1 register should be set to indicate the end of the pulse and
   TSAUXC.EN_TT1 bit should be set to 1b.

333369-009                                                                                         497
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

8. To make this a one time operation, the TSAUXC.DIS_TS_CLEAR field should be cleared.
9. When the SYSTIMEL/H registers becomes equal or larger than the TRGTTIMEL0/H0 registers the
   selected SDP changes its level. Then, when the SYSTIMEL/H registers becomes equal or larger than
   TRGTTIMEL0/H1 registers (that define the trailing edge of the pulse), the selected SDP changes its
   level back.

7.7.4.1.3             Synchronized Output Clock on SDP Pins

The X550 supports driving a programmable Clock on the SDP pins (up to two output clocks). The output
clocks generated are synchronized to the global System time registers (SYSTIM). The Target Time
registers (TRGTTIMEL0/H0 or TRGTTIMEL2/H1) can be used for the clock output generation. To start an
clock output on one of the SDP pins when System Time (SYSTIM) reaches a pre-defined value, the
driver should do the following:
1. Select a specific SDP pin by setting the TSSDP.TS_SDPx_EN flag to 1b (where ‘x’ is 0, 1, 2 or 3).
2. Select the target time register for a selected SDP, by setting the TSSDP.TS_SDPx_SEL field to 10b
   or 11b if output clock should occur based on TRGTTIMEL0/H0 or TRGTTIMEL2/H1 respectively.
3. Program the matched FREQOUT0/1 register to define clock half cycle time.
4. Define the selected SDPx pin as output, by setting the appropriate SDPx_IODIR bit in the ESDP
   register (where ‘x’ is 0, 1, 2, or 3).
5. Define that this SDP is used for TimeSync function by setting the appropriate SDPx_NATIVE bit in
   the ESDP register (where ‘x’ is 0, 1, 2, or 3). If used with SDP1, clear ESDP.SDP1_FUNCTION field.
6. If the output clock should start at a specific time, the TSAUXC.ST0/1 flag should be set to 1b and
   the matched TRGTTIMELx/Hx should be set to the required start time.
7. Enable the clock operation by setting the relevant TSAUXC.EN_CLK0/1 bit to 1b.
An interrupt can be generated from the clock output generated by the device by setting the relevant
TSAUXC.EN_TT0/1 bit to 1b and by setting the TSAUXC.DIS_TS_CLEAR to allow it to work continuously.
The clock out drives initially a logical ‘0’ level on the selected SDP. If the TSAUXC.ST0/1 flag is cleared,
it happens instantly when setting the TSAUXC.EN_CLK0/1 bit. Otherwise it happens when SYSTIM is
equal or larger than the TRGTTIM. Since then, the hardware repeats endlessly the following two steps:
1. Increment the used TRGTTIMELx/Hx by FREQOUT.
2. When SYSTIM is equal or larger than the TRGTTIM, the SDP reverts its output level.
Note:     When clearing TSAUXC.EN_CLK0/1 while TSAUXC.EN_TT0/1 was set to generate interrupts,
          clear the matching TSAUXC.EN_TT0/1 too to avoid one unexpected toggle.

#### 7.7.4.2 Time Stamp Events

Upon a change in the input level of one of the SDP pins that was configured to detect Time stamp
events using the TSSDP register or upon a setting of one of the TSAUXC.SAMP_AUTx fields, a time
stamp of the system time is captured into one of the two auxiliary time stamp registers (AUXSTMPL0/
H0 or AUXSTMPL1/H1). Software enables the timestamp of input event as follows:
1. Define the sampled SDP on AUX time ‘x’ (‘x’ = 0b or 1b) by setting the TSSDP.AUXx_SDP_SEL field
   while setting the matched TSSDP.AUXx_TS_SDP_EN bit to 1b.
2. Set also the TSAUXC.EN_TSx bit (‘x’ = 0b or 1b) to 1b to enable “timestamping”.

498                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Following a transition on the selected SDP, the hardware does the following:
1. The SYSTIM registers (low and high) are latched to the selected AUXSTMP registers (low and high).
2. The selected AUTT0 or AUTT1 flags are set in the TSICR and TSAUXC registers. If the AUTT
   interrupt is enabled by the TSIM register, and the 1588 interrupts are enabled by the TIMESYNC
   flag in the ICR register, an interrupt is asserted as well. After the hardware reports that an event
   time was latched, the software should read the latched time in the selected AUXSTMP registers.
   Software should read first the Low register and only then the High register. Reading the high
   register clears the relevant TSAUC.AUTTx field and releases the registers to sample a new event.
The software device driver may initiate a sampling of the current time by setting one of the
TSAUXC.SAMP_AUTx fields. When one of these bits is written the hardware The SYSTIM registers (low
and high) are latched to the selected AUXSTMP registers (low and high) and the selected AUTT0 or
AUTT1 flags are set in the TSAUXC register. Once the device driver reads the selected AUXSTMP
registers as described above, the hardware clears the relevant TSAUXC.AUTTx field and releases the
registers to sample a new event.

### 7.7.5 Time Sync Interrupts

Time Sync related interrupts can be generated by programming the TSICR and TSIM registers. The
TSICR register logs the interrupt cause and the TSIM register enables masking specific TSICR bits.
Occurrence of a Time Sync interrupt sets the ICR.TIME_SYNC interrupt bit.

### 7.7.6 PTP Packet Structure

The time sync implementation supports both the 1588 V1 and V2 PTP frame formats. The V1 structure
can come only as UDP payload over IPv4 while the V2 can come over L2 with its EtherType or as a UDP
payload over IPv4 or IPv6. The 802.1AS uses only the layer 2 V2 format. Note that PTP frame structure
over UDP is not supported in the X550 for IP tunneling packets.

     Offset in Bytes                        V1 Fields                                   V2 Fields

             Bits                       76543210                                      76543210

              0                                                        transportSpecific1           messageType
                                            versionPTP

# 1 Reserved                  versionPTP

              2
                                        versionNetwork                                messageLength
              3

333369-009                                                                                                        499
                                 Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                       Inline Functions

      Offset in Bytes                     V1 Fields                                        V2 Fields

            Bits                        76543210                                        76543210

# 4 SubdomainNumber

# 5 Reserved

             6
                                                                                             flags
             7

             8

             9

             10

             11
                                          Subdomain                                     Correction Field
             12

             13

             14

             15

             16

             17
                                                                                           reserved
             18

             19

             20                          messageType

# 21 Source communication technology

             22

             23

             24
                                         Sourceuuid                                      Source Port ID
             25

             26

             27

             28
                                         sourceportid
             29

             30
                                          sequenceId                                      sequenceId
             31

             32                             control                                         control

             33                            reserved                                    logMessagePeriod

             34
                                             falgs                                            n/a
             35

1. Should all be zero.

Note:       Only the fields with the bold italic format colored red are of interest to hardware.

         Ethernet (L2)             VLAN (Optional)                PTP EtherType                      PTP message

         Ethernet (L2)                 IP (L3)                        UDP                            PTP message

500                                                                                                           333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

When a PTP packet is recognized (by EtherType or UDP port address) on the Rx side, the version should
be checked if it is V1, then the control field at offset 32 should be compared to message field in the
RXMTRL register described in Section 8.2.2.21.2. Otherwise, the byte at offset 0 should be used for
comparison to the rest of the needed field are at the same location and size for both V1 and V2.

                       Enumeration                                                  Value

PTP_SYNC_MESSAGE                                                                      0

PTP_DELAY_REQ_MESSAGE                                                                 1

PTP_FOLLOWUP_MESSAGE                                                                  2

PTP_DELAY_RESP_MESSAGE                                                                3

PTP_MANAGEMENT_MESSAGE                                                                4

reserved                                                                            5–255

                        MessageId                                Message Type               Value (hex)

PTP_SYNC_MESSAGE                                                     Event                      0

PTP_DELAY_REQ_MESSAGE                                                Event                      1

PTP_PATH_DELAY_REQ_MESSAGE                                           Event                      2

PTP_PATH_DELAY_RESP_MESSAGE                                          Event                      3

Unused                                                                                          4-7

PTP_FOLLOWUP_MESSAGE                                                 General                    8

PTP_DELAY_RESP_MESSAGE                                               General                    9

PTP_PATH_DELAY_FOLLOWUP_MESSAGE                                      General                    A

PTP_ANNOUNCE_MESSAGE                                                 General                    B

PTP_SIGNALLING_MESSAGE                                               General                    C

PTP_MANAGEMENT_MESSAGE                                               General                    D

Unused                                                                                          E-F

If V2 mode is configured in TSAUXC register (Section 8.2.2.21.13), time stamp should be taken on
PTP_PATH_DELAY_REQ_MESSAGE and PTP_PATH_DELAY_RESP_MESSAGE for any value in the
message field in the RXMTRL register described at Section 8.2.2.21.2.
Note:        A PTP over UDP packet encapsulated in a VXLAN or NVGRE tunnel is still identified as a PTP
             packet.

333369-009                                                                                                501
                                    Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                                        Inline Functions

#### 7.7.6.1 Time Sync Packets Identification Configuration

Table 7-61 summarize the setting needed to identify Time Sync packets.

Table 7-61. Enabling Receive Timestamp
      Functionality           Register               Field                             Setting Options

Enable receive timestamp    TSYNCRXCTL      En                     En = 1b (must be set in all the following options).
in register

Sampled V1 Control value    RXMTRL          CTRLT                  The CTRLT defines the recognized V1 Control field. This
                                                                   field must be defined if V1 packets recognition is
                                                                   required.
                                                                     0x0 = PTP_SYNC_MESSAGE

Sampled V2 MessageType      RXMTRL          MSGT                   The MSGT defines the recognized V2 MessageType field.
value                                                              This field must be defined if V2 packets recognition is
                                                                   required.
                                                                    0x0 = Sync

Enable all packets for      TSYNCRXCTL      Type                   Type equals to 100b enables sampling all packets. Useful
timestamp                                                          only when posting the timestamp to the packet buffer in
                                                                   host memory, enabled per queue by the
                                                                   SRRCTL[n].Timestamp.

Enable L2 1588 packets      TSYNCRXCTL      Type                   Type equals to 000b or 010b enable V2 packets with
for timestamp sampling                                             MessageType equals to MSGT
                                                                   Type equals to 101b enable all V2 packets with Message
                                                                   Type bit 3 zero (means any event packets)

                            ETQF[n]         EType Filter enable    The EType on one of the enabled ETQF registers (Filter
                                            IEEE_1588_TIME_STAMP   enable is ‘1’) should be set to the 1588 EtherType
                                                                   (equals to 0x88F7) and IEEE_1588_TIME_STAMP field
                                                                   should be set.

Enable 1588 packets over    TSYNCRXCTL      Type                   Type equals to 001b enables V1 packets with Control
UDP for timestamp                                                  field equals to CTRLT parameter
sampling                                                           Type equals to 010b enables V2 packets with
                                                                   MessageType fields equals to MSGT parameter
                                                                   Type equals to 101b enables all V2 packets with
                                                                   MessageType bit 3 zero (which means any event
                                                                   packets)

                            RXMTRL          UDPT                   Defines the UDP port to use for V1 detection

Define specific receive     ETQF[n]         Rx Queue               Setting the “Queue Enable” on the same ETQF register
queue for the L2 1588                       Queue Enable           as above, the receive queue is defined by the Rx Queue
packets                                                            field.

502                                                                                                               333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions
