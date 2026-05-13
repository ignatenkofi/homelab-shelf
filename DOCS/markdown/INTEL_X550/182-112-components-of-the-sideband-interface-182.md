## 11.2 Components of the Sideband Interface

There are two components to a sideband interface:
 • Physical Layer
 • Logical Layer

### 11.2.1 Physical Layer

This is the electrical connection between the X550 and BMC.

#### 11.2.1.1 SMBus

The SMBus physical layer is defined by the SMBus specification. The interface is made up of two
connections: Data and Clock. There is also an optional third connection: the Alert line. This line is used
by the X550 to notify the BMC that there is data available for reading. Refer to the SMBus specification
for details.
The SMBus can run at three speeds: 100 KHz (standard SMBus), or 400 KHz (I2C fast mode) or 1 MHz
(I2C fast mode plus).The speed used is selected by the SMBus Connection Speed in SMBus Notification
Timeout and Flags NVM word.

11.2.1.1.1                PEC Support

SMBus transactions can be protected by using Packet Error Code (PEC). Packet Error Checking,
whenever applicable, is implemented by appending a PEC byte at the end of each message transfer. The
PEC byte is a CRC8 calculation on all the message bytes.
PEC is added in transmit and expected in receive for the following SMBus packets:
 • ARP packets.
 • MCTP over SMBus transactions.
For ARA cycles and legacy SMBus transactions, a PEC is not expected.
Table 11-1 describes the behavior of the device in each PEC configured mode for transactions directly
handled by the hardware upon reception of packets with or without PEC.

Table 11-1. SMBus PEC Modes1
                                                                           Target PEC Mode
  SMBus Transaction
                             X550 PEC Mode
 (Relative to the X550)
                                                           PEC Enabled                          PEC Disabled

                                 Enabled        (A) Target ACKs the PEC byte.         (A) Target NACKs the PEC byte.
      Master Write2
                                                (A) Target receives stop before       (A) PEC byte is not expected.
                                 Disabled
                                                expected PEC byte.

                                                (A) Target ACKs last data byte; PEC   (A) Target NACKs last data byte; No
                                 Enabled
                                                byte is NACKed.                       PEC byte is written by Slave.
                 3
      Slave Write
                                                (A) Target ACKs last data byte; PEC   (A) Target NACKs last data byte
                                 Disabled
                                                byte is 0xFF.                         and generates Stop after that.

333369-009                                                                                                              949
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                      System Manageability

Table 11-1. SMBus PEC Modes1 [continued]
                                                                                  Target PEC Mode
  SMBus Transaction
                                 X550 PEC Mode
 (Relative to the X550)
                                                                  PEC Enabled                         PEC Disabled

                                                        (A) Target sends PEC byte; PEC      (A) Target does not send PEC byte
                                      Enabled
                                                        byte is ACKed by Slave.             and generates Stop after that.
                      4
         Slave Read
                                                        (R) Target sends PEC byte; PEC      (A) Target does not send PEC byte
                                     Disabled
                                                        byte is NACKed by Slave.            and generates Stop after that.

1.   (A) - Accept Transaction (R) - Reject Transaction
2.   Used in Legacy SMBus writes commands (Direct receive) and in MCTP over SMBus (Transmitted transactions).
3.   Used in Legacy SMBus Read commands.
4.   Used in Legacy SMBus mode (Alert/Async-Notify) and in MCTP over SMBus (Received transactions).

Note:        In SMBus ARP and MCTP, the specification indicates that PEC must be used. However, if PEC is
             not used by the master, the transaction is still accepted and processed by the device.
The PEC behavior is controlled by the SMBus Transaction PEC bit in the SMBus Notification Timeout and
Flags NVM word: If this bit is set, PEC is added for master SMBus write transactions. a PEC is added to
slave read transactions and can be received in slave write transaction. If this bit is cleared, PEC is not
added to master write or slave read transactions, a slave write transaction with PEC is dropped. This bit
should be set for MCTP mode and should be cleared in legacy SMBus mode.

#### 11.2.1.2 NC-SI

The X550 uses the DMTF standard Sideband Interface. This interface consists of 6 lines for transmission
and reception of Ethernet packets and two optional lines for arbitration among more than one physical
network controller.
The physical layer of NC-SI is very similar to the RMII interface, although not an exact duplicate. Refer
to the NC-SI specification for details of the differences.

#### 11.2.1.3 PCIe

The X550 uses the VDMs (Vendor Defined Messages) over PCIe defined in the DMTF MCTP specification
to convey pass-through traffic or NC-SI control traffic. See Section 3.1 for details of the PCIe interface.

### 11.2.2 Logical Layer

#### 11.2.2.1 Legacy SMBus

The protocol layer for SMBus consists of commands the BMC issues to configure filtering for the X550
management traffic and the reading and writing of Ethernet frames over the SMBus interface. There is
no industry standard protocol for sideband traffic over SMBus. The protocol layer for SMBus on the
X550 is Intel proprietary. The Legacy SMBus protocol is described in Section 11.5.

950                                                                                                                333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.2.2.2 NC-SI

The DMTF also defines the protocol layer for the NC-SI interface. NC-SI compliant devices are required
to implement a minimum set of commands. The specification also provides a mechanism for vendors to
add additional capabilities through the use of OEM commands. Intel OEM NC-SI commands for the X550
are discussed in Section 11.6.3. For information on base NC-SI commands, see the NC-SI specification.
NC-SI traffic can run on top of three different Physical layers:
1. NC-SI Physical layer as described in Section 11.2.1.2.
2. MCTP over PCIe.This protocol allows control and pass-through traffic over PCIe of a NIC or a LOM
   device. The NC-SI over MCTP protocol is slightly different than the standard NC-SI as it includes
   additional NC-SI commands. This mode is usually paired with an MCTP over SMBus, where this
   mode is used in S0 states and the SMBus interface is used in Sx state.The MCTP protocol and the
   differences from standard NC-SI is described in Section 11.7.
3. MCTP over SMBus. As described above, this layer is paired with the MCTP over PCIe to support Sx
   modes.
The X550 exposes one NC-SI package with up to two channels, one per port.
If the number of ports available changes, the package moves to initialization required state and should
be re-enumerated. If the transition occurs while one of the ports is in Keep PHY link up state, the
transition is delayed until the Keep PHY link up state is cleared.
The X550 implements a type C NC-SI interface (Single package, common bus buffers and shared Rx
queue) as described in section 5.2 of the NC-SI specification.

11.2.2.2.1             Package ID Setting

The package ID can be set either from the Package ID field in the NC-SI Configuration 1 NVM word
(Section 6.2.17.5), or from an SDP pin. If set from SDP, the Package ID is {0,SDP0_0 value, 0}. The
mode used is set by the NC-SI Package ID from SDP field in the NC-SI Configuration 2 NVM word
(Section 6.2.17.6). Note that when the package ID is set from the SDP pin, SDP0_0 should be set as
input is ESDP.SDP0_IODIR field.
The internal channel ID matches the lowest numbered PCIe function number through which this port is
exposed to the host.

11.2.2.2.2             Channel ID Mapping

The mapping of the channels to physical ports is according to the NC-SI Channel to Port Mapping NVM
word (Section 6.2.17.17) if the Table Valid bit is set. If this bit is not set, the following algorithm should
be used:
  CHANNEL_ID = 0
  If (FACTPS. LAN_FUNCTION_SEL == 0 ) // no swap
     For (x = 0 to 1) {
         PORT = x;
         If (FACTPS.LANx_VALID) NC-SI_Channel[PORT] = CHANNEL_ID++;
     }
  Else // swap
     For (x = 0 to 1) {
         PORT = 1 - x;
         If (FACTPS.LANx_VALID) NC-SI_Channel[PORT] = CHANNEL_ID++;
     }

333369-009                                                                                                 951
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                          System Manageability
