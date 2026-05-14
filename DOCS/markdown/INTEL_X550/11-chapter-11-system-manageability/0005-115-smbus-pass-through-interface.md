## 11.5 SMBus Pass-Through Interface

SMBus is the system management bus defined by Intel. It is used in personal computers and servers
for low-speed system management communications. This section describes how the SMBus interface
operates in legacy pass-through mode.

### 11.5.1 General

The SMBus sideband interface includes standard SMBus commands used for assigning a slave address
and gathering device information as well as Intel proprietary commands used specifically for the
pass-through interface.

### 11.5.2 Pass-Through Capabilities

This section details manageability capabilities the X550 provides while in SMBus mode. Pass-through
traffic is carried by the sideband interface as described in Section 11.1.
These services are not available in NC-SI mode.
When operating in SMBus mode, in addition to exposing a communication channel to the LAN for the
BMC, the X550 provides the following manageability services to the BMC:
 • ARP handling — The X550 can be programmed to auto-ARP replying for ARP request packets to
   reduce the traffic over the BMC interconnect.
 • Default configuration of filters by NVM — When working in SMBus mode, the default values of
   the manageability receive filters can be set according to the PT LAN and flex TCO NVM structures.

### 11.5.3 Port to SMBus Mapping

The X550 is presented on the SMBus manageability link as two different devices (for example, via two
different SMBus addresses on which each device is connected to a different LAN port). There is no
logical connection between the devices.
The fail-over between the LAN ports is done by the BMC (by sending/receiving packets through
different devices). The status report to the BMC, ARP handling, DHCP, and other pass-through
functionality are unique for each port and configured by the BMC.
If the number of enable ports changes, the port enable state is updated, and an alarm is set according
to the programmed notification method. Bit 6 in Status data byte 2 of all the currently-enabled
functions is set to indicate the change. The BMC can then detect the change in the configuration and do
a new ARP flow or try to discover if new ports where added or removed.

333369-009                                                                                          967
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                            System Manageability

### 11.5.4 Automatic Ethernet ARP Operation

The X550 can offload the Ethernet Address Resolution Protocol (ARP) for the BMC to reduce the
bandwidth required on the SMBus link.
Automatic Ethernet ARP parameters are loaded from the NVM when the X550 is powered up or
configured through the sideband management interface. The following parameters should be configured
to enable ARP operation:
 • ARP auto-reply enabled.
 • ARP IP Address (to filter ARP packets).
 • ARP MAC Addresses (for ARP responses).
These are all configurable over the sideband interface using the advanced version of the Receive Enable
command.
When an ARP request packet is received and ARP auto-reply is enabled, the X550 checks the targeted
IP Address (after the packet has passed L2 checks and ARP checks). If the targeted IP matches the IP
configuration for the X550, it replies with an ARP response.
The X550 responds to ARP request targeted to the ARP IP Address with the configured ARP MAC
Address. In case that there is no match, the X550 silently discards the packets. If the X550 is not
configured to do auto-ARP response, it can be configured to forward the ARP packets to the BMC (which
can respond to ARP requests).
When the external BMC uses the same IP and MAC Address of the OS, the ARP operation should be
coordinated with the host operating system.
Note:       If sharing the MAC and IP with the host operating system is possible, the X550 provides the
            ability to read the stem MAC Address, allowing the BMC to share the MAC Address. There is
            no mechanism however provided by the X550 to read the IP Address. The host OS (or an
            agent within) and BMC must coordinate the sharing of IP Addresses.

### 11.5.5 SMBus Transactions

This section gives a brief overview of the SMBus protocol. Following is an example for a format of a
typical SMBus transaction.

Table 11-6. Typical SMBus Transaction
 1           7          1    1           8           1             8             1   1

 S      Slave Address   Wr   A       Command         A            PEC            A   P

          1100 001      0    0       0000 0010        0     [Data Dependent]     0

The top row of the table identifies the bit length of the field in a decimal bit count. The middle row
(bordered) identifies the name of the fields used in the transaction. The last row appears only with
some transactions, and lists the value expected for the corresponding field. This value can be either
hexadecimal or binary.
The SMBus controller is a master for some transactions and a slave for others. The differences are
identified in this document.
Shorthand field names are listed in Table 11-7 and are fully defined in the SMBus specification.

968                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-7. Shorthand Field Names
Field Name     Definition

S              SMBus START Symbol

P              SMBus STOP Symbol

PEC            Packet Error Code

A              ACK (Acknowledge)

N              NACK (Not Acknowledge)

Rd             Read Operation (Read Value = 1b)

Wr             Write Operation (Write Value = 0b)

#### 11.5.5.1 SMBus Addressing

The SMBus is presented as up to two SMBus devices on the SMBus (two addresses). All pass-through
functionality is duplicated on the SMBus address, where each SMBus address is connected to a different
LAN port. Note that it is not permitted to configure multiple ports to the same SMBus address. When a
LAN function is disabled, the corresponding SMBus address is not presented to the BMC.
SMBus addresses (enabled from the NVM) can be re-assigned using the SMBus ARP protocol.
In addition to the SMBus address values, all parameters of the SMBus (SMBus channel selection,
address mode, and address enable) can be set only through NVM configuration. Note that the NVM is
read at the X550’s power up and resets.

#### 11.5.5.2 SMBus ARP Functionality

The X550 supports the SMBus ARP protocol as defined in the SMBus 2.0 specification. The X550 is a
persistent slave address device so its SMBus address is valid after power-up and loaded from the NVM.
The X550 supports all SMBus ARP commands defined in the SMBus specification both general and
directed.
SMBus ARP capability can be disabled through the NVM.

#### 11.5.5.3 SMBus ARP Flow

SMBus ARP flow is based on the status of two flags:
 • AV (Address Valid) — This flag is set when the X550 has a valid SMBus address.
 • AR (Address Resolved) — This flag is set when the X550 SMBus address is resolved (SMBus
   address was assigned by the SMBus ARP process).
These flags are internal X550 flags and are not exposed to external SMBus devices.
Since the X550 is a Persistent SMBus Address (PSA) device, the AV flag is always set, while the AR flag
is cleared after power up until the SMBus ARP process completes. Since AV is always set, the X550
always has a valid SMBus address.
When the SMBus master needs to start an SMBus ARP process, it resets (in terms of ARP functionality)
all devices on SMBus by issuing either Prepare to ARP or Reset Device commands. When the X550
accepts one of these commands, it clears its AR flag (if set from previous SMBus ARP process), but not
its AV flag (the current SMBus address remains valid until the end of the SMBus ARP process).

333369-009                                                                                          969
                                   Did this document help answer your questions?

                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                       System Manageability

Clearing the AR flag means that the X550 responds to SMBus ARP transactions that are issued by the
master. The SMBus master issues a Get UDID command (general or directed) to identify the devices on
the SMBus. The X550 always responds to the Directed command and to the General command only if its
AR flag is not set.
After the Get UDID, The master assigns the X550 SMBus address by issuing an Assign Address
command. The X550 checks whether the UDID matches its own UDID and if it matches, it switches its
SMBus address to the address assigned by the command (byte 17). After accepting the Assign Address
command, the AR flag is set and from this point (as long as the AR flag is set), the X550 does not
respond to the Get UDID General command. Note that all other commands are processed even if the AR
flag is set. If the address changed, from the one previously stored in the NVM, the X550 stores the
SMBus address that was assigned in the SMBus ARP process in the NVM, so at the next power up, it
returns to its assigned SMBus address. This process uses the NVM update flow described in
Section 3.4.2.1.
Figure 11-4 shows the X550 SMBus ARP flow.

970                                                                                              333369-009
                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

                                    Power-Up reset

                                Set AV flag; Clear AR flag
                                 Load SMB address from
                                         EPROM

                                      SMB packet       NO
                                       received

                                           Yes

                                       SMB ARP
             Process regular
                               NO       address
                command
                                         match

                                           Yes

                                       Prepare to              ACK the command
                                                         YES
                                         ARP ?                  and clear AR flag

                                           NO

                                         Reset                 ACK the command
                                                         YES
                                         device                 and clear AR flag

                                           NO

                                          Assign
                                         Address         YES   UDID match           NO     NACK packet
                                        command

                                                                                           ACK packet
                                           NO                            YES             Set slave address
                                                                                           Set AR flag.

                                       Get UDID
                                       command           YES    AR flag set         NO     Return UDID
                                        general

                                           NO                            YES               NACK packet

                                       Get UDID
                                       command                     YES                     Return UDID
                                        directed

                                           NO

                                     Illegal command
                                          handling

Figure 11-4. SMBus ARP Flow

333369-009                                                                                                   971
                                    Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

#### 11.5.5.4 SMBus ARP UDID Content

The UDID provides a mechanism to isolate each device for the purpose of address assignment. Each
device has a unique identifier. The 128-bit number is comprised of the following fields:

Table 11-8. UDID

# 1 Byte          1 Byte          2 Bytes        2 Bytes        2 Bytes        2 Bytes           2 Bytes           4 Bytes

    Device           Version/                                                    Subsystem         Subsystem           Vendor
                                     Vendor ID      Device ID       Interface
  Capabilities       Revision                                                    Vendor ID         Device ID          Specific ID

  See notes         See notes                                       0x0004/                                           See notes
                                      0x8086         0x1562                        0x0000            0x0000
  that follow       that follow                                     0x0024                                            that follow

       MSB                                                                                                               LSB

Where:

  Vendor ID:                    The device manufacturer’s ID as assigned by the SBS Implementers’ Forum or
                                the PCI SIG.
                                   Constant value: 0x8086
  Device ID:                    The device ID as assigned by the device manufacturer (identified by the Vendor
                                ID field).
                                   Constant value: 0x1562
  Interface:                    Identifies the protocol layer interfaces supported over the SMBus connection by
                                the device.
                                   Bits 3:0 = 0x4 indicates SMBus Version 2.0
                                   Bit 5 (ASF bit) = 1 in MCTP mode.
  Subsystem Fields:             These fields are not supported and return zeros.

Device Capabilities: Dynamic and Persistent Address, PEC Support bit:

        7                  6             5              4               3             2                 1                 0

                                                                                                                          PEC
            Address Type            Reserved (0)   Reserved (0)   Reserved (0)   Reserved (0)     Reserved (0)
                                                                                                                       Supported

       0b                  1b           0b             0b              0b            0b                 0b              0b/1b1

       MSB                                                                                                               LSB

1. The value is set according to the SMBus Transaction PEC bit in the NVM

Version/Revision: UDID Version 1, Silicon Revision:

        7                  6             5              4               3             2                 1                 0

 Reserved (0)      Reserved (0)                    UDID Version                                 Silicon Revision ID

       0b                  0b                         001b                                   See the following table

       MSB                                                                                                               LSB

972                                                                                                                     333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Silicon Revision ID:

             Silicon Version                     Revision ID

                    A0                                 000b

                    B0                                 001b

Vendor Specific ID: Four LSB bytes of the device Serial Number combined with the port number. The
Serial Number is taken from the NVM and is reflected in the PCI_SERL and PCI_SERH registers.

# 1 Byte                    1 Byte                        1 Byte                1 Byte

  Port Number, MAC Address,
                                 MAC Address, Byte 2           MAC Address, Byte 1   MAC Address, Byte 0
         Byte 3[6:0]

              MSB                                                                           LSB

#### 11.5.5.5 SMBus ARP and Multi-Port

The X550 responds as two SMBus devices having two sets of AR/AV flags (one for each port). The X550
responds two time to the SMBus ARP master, once each for each port. All SMBus addresses are taken
from the SMBus ARP address word of the NVM.
Note that the Unique Device Identifier (UDID) is different for the different ports in the Version ID field.
The X550 first responds as port 0, and only when an address is assigned, then starts responding as port
1 to the Get UDID command.

#### 11.5.5.6 Concurrent SMBus Transactions

The SMBus interface is single threaded. Thus, concurrent SMBus transactions are not permitted. Once a
transaction is started, it must be completed before additional transaction can be initiated.
A transaction is defined as:
 • All the SMBus commands used to receive a packet.
 • All the SMBus commands used to send a packet.
 • The read and write SMBus commands used as part of read parameters described in
   Section 11.5.11.2.
 • The single write SMBus commands described in Section 11.5.11.1.

### 11.5.6 SMBus Notification Methods

The X550 supports three methods of notifying the BMC that it has information that needs to be read by
the BMC:
 • SMBus alert - Refer to Section 11.5.6.1.
 • Asynchronous notify - Refer to Section 11.5.6.2.
 • Direct receive - refer to Section 11.5.6.3.
The notification method used by the X550 can be configured from the SMBus using the Receive Enable
command (Section 11.5.11.1.3). The default method is set by the NVM in the Notification Method field
in LAN Receive Enable 1 (Section 6.2.18.48).

333369-009                                                                                                 973
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

Note:     The SMBus notification method used must be the same for all ports.
The following events cause the X550 to send a notification event to the BMC:
 • Receiving a LAN packet that is designated to the BMC.
 • The firmware was reset and requires re-initialization.
 • Receiving a Request Status command from the BMC initiates a status response.
 • The X550 is configured to notify the BMC upon status changes (by setting the EN_STA bit in the
   Receive Enable Command) and one of the following events happen:
      — TCO Command Aborted
      — Link Status changed
      — Power state change
      — Thermal Sensor Event
There can be cases where the BMC is hung and not responding to the SMBus notification. The X550 has
a time-out value (defined in the NVM) to avoid hanging while waiting for the notification response. If
the BMC does not respond until the time out expires, the notification is de-asserted and all pending data
is silently discarded.
Note that the SMBus notification time-out value can only be set in the NVM. The BMC cannot modify this
value.

#### 11.5.6.1 SMBus Alert and Alert Response Method

The SMBus Alert# (SMBALERT_N) signal is an additional SMBus signal that acts as an asynchronous
interrupt signal to an external SMBus master. The X550 asserts this signal each time it has a message
that it needs the BMC to read and if the chosen notification method is the SMBus alert method. Note
that the SMBus alert method is an open-drain signal which means that other devices besides the X550
can be connected on the same alert pin. As a result, the BMC needs a mechanism to distinguish
between the alert sources.
The BMC can respond to the alert by issuing an ARA Cycle command to detect the alert source device.
The X550 responds to the ARA cycle with its own SMBus slave address (if it was the SMBus alert
source) and de-asserts the alert when the ARA cycle is completes. Following the ARA cycle, the BMC
issues a read command to retrieve the X550 message.
Some BMCs do not implement the ARA cycle transaction. These BMCs respond to an alert by issuing a
Read command to the X550 (0xC0/0xD0 or 0xDE). The X550 always responds to a Read command,
even if it is not the source of the notification. The default response is a status transaction. If the X550 is
the source of the SMBus Alert, it replies the read transaction and then de-asserts the alert after the
command byte of the read transaction.
Note:     In SMBus Alert mode, the SMBALERT_N pin is used for notification. Each port generate alerts
          on events that are independent of each other. If two ports have events to notify, the second
          alert is asserted only after the first event is handled. Hence, if an ARA cycle is not sent, a read
          status transaction should be done to all the ports in event of an ALERT_N assertion.
The ARA cycle is an SMBus receive byte transaction to SMBus Address 0001-100b. Note that the ARA
transaction does not support PEC. The ARA transaction format is as follows:

974                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

 1                  7                      1            1                             8                         1   1     1

 S      Alert Response Address             Rd           A                Slave Device Address                       A     P

                0001 100                   1            0        Manageability Slave SMBus Address              0   1

If the BMC does not react to the alert in the delay defined by the SMBus Notification Timeout NVM field
(Section 6.2.17.3), the ALERT pin is de-asserted and the Rx packet indication in the status word is
cleared (and packet is dropped)

#### 11.5.6.2 Asynchronous Notify Method

When configured using the asynchronous notify method, the X550 acts as a SMBus master and notifies
the BMC of one of the events listed in Section 11.5.6 by issuing a modified form of the write word
transaction. The asynchronous notify transaction SMBus address and data payload is configured using
the Receive Enable command (Section 11.5.11.1.3) or using the NVM defaults. Note that the
asynchronous notify is not protected by a PEC byte.

 1              7                 1   1                       7                1      1                8            1                8         1   1

                                                Sending Device
 S     Target Address         Wr      A                                               A           Data Byte Low     A         Data Byte High   A   P
                                                   Address

                                               MNG Slave SMBus
      BMC Slave Address           0   0                                        0      0             Interface       0          Alert Value     0
                                                   Address

The target address and data byte low/high are taken from the Receive Enable command or NVM
configuration (Section 6.2.18.48 and Section 6.2.18.49).
If the BMC does not read the status in the delay defined by the SMBus Notification Timeout NVM field
(Section 6.2.17.3), the Rx packet indication in the status word is cleared (and packet is dropped).

#### 11.5.6.3 Direct Receive Method

If configured, the X550 has the capability to send a message it needs to transfer to the external BMC as
a master over the SMBus instead of alerting the BMC and waiting for it to read the message.
The message format follows. Note that the command that is used is the same command that is used by
the external BMC in the Block Read command. The opcode that the X550 puts in the data is also the
same as it put in the Block Read command of the same functionality. The rules for the F and L flags
(bits) are also the same as in the Block Read command.

 1                  7                 1         1            1       1                        6                 1

 S           Target Address           Wr        A            F       L                Command                   A   ...

                                                            First   Last       Receive TCO Command
        BMC Slave Address             0         0                                                               0
                                                            Flag    Flag             01 0000b

          8                   1                     8                      1              1                8              1      1

      Byte Count              A           Data Byte 1                      A    ...       A           Data Byte N         A      P

          N                   0                                            0              0                               0

333369-009                                                                                                                                         975
                                           Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                          System Manageability

### 11.5.7 Receive Pass-Through Flow

The X550 is used as a channel for receiving packets from the network link and passing them to the
external BMC. The BMC configures the X550 to pass these specific packets to the BMC. Once a full
packet is received from the link and identified as a manageability packet that should be transferred to
the BMC, the X550 starts the receive TCO flow to the BMC.
The X550 uses the SMBus notification method to notify the BMC that it has data to deliver. Since the
packet size might be larger than the maximum SMBus fragment size, the packet is divided into
fragments, where the X550 uses the maximum fragment size allowed in each fragment (configured via
the NVM). The last fragment of the packet transfer is always the status of the packet. As a result, the
packet is transferred in at least two fragments. The data of the packet is transferred as part of the
receive TCO LAN packet transaction.
When SMBus alert is selected as the BMC notification method, the X550 notifies the BMC on each
fragment of a multi-fragment packet. When asynchronous notify is selected as the BMC notification
method, the X550 notifies the BMC only on the first fragment of a received packet. It is the BMC's
responsibility to read the full packet including all the fragments.
Any timeout on the SMBus notification results in discarding the entire packet. Any NACK by the BMC
causes the fragment to be re-transmitted to the BMC on the next Receive Packet command.
The maximum size of the received packet is limited by the X550 to 1536 bytes. Packets larger than
1536 bytes are silently discarded. Any packet smaller than 1536 bytes is processed.

### 11.5.8 Transmit Pass-Through Flow

The X550 is used as the channel for transmitting packets from the external BMC to the network link.
The network packet is transferred from the BMC over the SMBus and then, when fully received by the
X550, is transmitted over the network link.
Each SMBus address is connected to a different LAN port. When a packet is received during a SMBus
transaction using SMBus address #0, it is transmitted to the network using LAN port #0; it is
transmitted through LAN port #1 if received on SMBus address #1, etc.
The X550 supports packets up to an Ethernet packet length of 1536 bytes. Since SMBus transactions
can only be up to 240 bytes in length, packets might need to be transferred over the SMBus in more
than one fragment. This is achieved using the F and L bits in the command number of the transmit TCO
packet Block Write command. When the F bit is set, it is the first fragment of the packet. When the L bit
is set, it is the last fragment of the packet. When both bits are set, the entire packet is in one fragment.
The packet is sent over the network link only after all its fragments are received correctly over the
SMBus. The maximum SMBus fragment size is defined within the NVM and cannot be changed by the
BMC.
The minimum packet length defined by the 802.3 specification is 64 bytes. The X550 pads packets that
are less than 64 bytes to meet the specification requirements (there is no need for the external BMC to
pad packets less than 64 bytes). If the packet sent by the BMC is larger than 1536 bytes, the X550
silently discards the packet.
The X550 calculates the L2 CRC on the transmitted packet and adds its four bytes at the end of the
packet. Any other packet field (such as XSUM or VLAN) must be calculated and inserted by the BMC
(the X550 does not change any field in the transmitted packet, other than adding padding and CRC
bytes).

976                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

If the network link is down when the X550 has received the last fragment of the packet from the BMC,
it silently discards the packet. Note that any link down event during the transfer of any packet over the
SMBus does not stop the operation since the X550 waits for the last fragment to end to see whether the
network link is up again.

#### 11.5.8.1 Transmit Errors in Sequence Handling

Once a packet is transferred over the SMBus from the BMC to the X550, the F and L flags should follow
specific rules. The F flag defines the first fragment of the packet; the L flag that the transaction contains
the last fragment of the packet. Table 11-9 lists the different flag options in transmit packet
transactions.

Table 11-9. Flag Options During Transmit Packet Transactions
   Previous         Current                                             Action/Notes

Last             First        Accept both.

Last             Not First    Error for the current transaction. Current transaction is discarded and an abort status is
                              asserted.

Not Last         First        Error in previous transaction. Previous transaction (until previous First) is discarded. Current
                              packet is processed.
                              No abort status is asserted.

Not Last         Not First    Process the current transaction.

Note:        Since every other Block Write command in TCO protocol has both F and L flags on, they cause
             flushing any pending transmit fragments that were previously received. When running the
             TCO transmit flow, no other Block Write transactions are allowed in between the fragments.

#### 11.5.8.2 TCO Command Aborted Flow

The X550 indicates to the BMC an error or an abort condition by setting the TCO Abort bit in the general
status. The X550 might also be configured to send a notification to the BMC (see
Section 11.5.11.1.3.3).
Following is a list of possible error and abort conditions:
 • Any error in the SMBus protocol (NACK, SMBus timeouts, etc.).
 • If the BMC does not respond until the notification timeout (programmed in the EEPROM) expires.
 • Any error in compatibility between required protocols to specific functionality (for example, Rx
   Enable command with a byte count not equal to 1/14, as defined in the command specification).
 • If the X550 does not have space to store the transmitted packet from the BMC (in its internal buffer
   space) before sending it to the link, the packet is discarded and the external BMC is notified via the
   Abort bit.
 • Error in the F/L bit sequence during multi-fragment transactions.
 • An internal reset to the X550's firmware.

333369-009                                                                                                                       977
                                  Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                             System Manageability

### 11.5.9 SMBus Link State Control

While in SMBus mode, the default setting of the link is defined by the Enable All PHYs in D3 N bit in
Common Firmware Parameters NVM word.
When a channel is enabled through NVM setting or through the RCV_EN option of the Receive Enable
Command, the link is established (if not already required for other purposes).
If the channel is disabled by clearing of the RCV_EN option, the link may move back to the default
defined by the Enable All PHYs in D3 N if not needed for other purposes.
Note:     When the link is taken down due to RCV_EN being cleared the transmit traffic from BMC is
          also stopped.
Note:     Before transitioning to D3 it is the responsibility of the driver to request the PHY to be active
          for wake-up activities.

### 11.5.10 SMBus ARP Transactions

All SMBus ARP transactions include the PEC byte.

#### 11.5.10.1 Prepare to ARP

This command clears the Address Resolved flag (set to false). It does not affect the status or validity of
the dynamic SMBus address and is used to inform all devices that the ARP master is starting the ARP
process:

 1           7            1    1              8             1              8              1   1

 S      Slave Address     Wr   A          Command           A             PEC             A   P

          1100 001        0    0          0000 0001         0    [Data Dependent Value]   0

#### 11.5.10.2 Reset Device (General)

This command clears the Address Resolved flag (set to false). It does not affect the status or validity of
the dynamic SMBus address.

 1           7            1    1              8             1              8              1   1

 S      Slave Address     Wr   A          Command           A             PEC             A   P

          1100 001        0    0          0000 0010         0    [Data Dependent Value]   0

978                                                                                                    333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.5.10.3 Reset Device (Directed)

The Command field is NACKed if bits 7:1 do not match the current SMBus address. This command
clears the Address Resolved flag (set to false) and does not affect the status or validity of the dynamic
SMBus address.

 1                7           1         1                    8                 1                    8                     1   1

 S       Slave Address        Wr        A                 Command              A                    PEC                   A   P

             1100 001         0         0      Targeted Slave Address | 0      0         [Data Dependent Value]           0

#### 11.5.10.4 Assign Address

This command assigns SMBus address. The address and command bytes are always acknowledged.
The transaction is aborted (NACKed) immediately if any of the UDID bytes is different from the X550
UDID bytes. If successful, the manageability system internally updates the SMBus address. This
command also sets the Address Resolved flag (set to true).

 1            7           1       1                   8              1                 8                  1

 S     Slave Address     Wr       A             Command              A          Byte Count                A    ···

         1100 001         0       0             0000 0100            0          0001 0001                 0

          8               1                    8                 1             8                1                    8            1

        Data 1            A                  Data 2              A           Data 3             A                Data 4           A   ···

  UDID Byte 15 (MSB)      0            UDID Byte 14              0        UDID Byte 13          0             UDID Byte 12        0

          8               1                    8                 1             8                1                    8            1

        Data 5            A                  Data 6              A           Data 7             A                Data 8           A   ···

     UDID Byte 11         0            UDID Byte 10              0         UDID Byte 9          0             UDID Byte 8         0

          8               1                    8                 1             8                1

        Data 9            A                 Data 10              A           Data 11            A       ···

     UDID Byte 7          0             UDID Byte 6              0         UDID Byte 5          0

          8               1                    8                 1             8                1                    8            1

       Data 12            A                 Data 13              A           Data 14            A               Data 15           A   ···

     UDID Byte 4          0             UDID Byte 3              0         UDID Byte 2          0             UDID Byte 1         0

          8               1                    8                 1             8                1         1

       Data 16            A                 Data 17              A            PEC               A         P

                                                                         [Data Dependent
  UDID Byte 0 (LSB)       0           Assigned Address           0                              0
                                                                              Value]

333369-009                                                                                                                                  979
                                            Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                                System Manageability

#### 11.5.10.5 Get UDID (General and Directed)

The general get UDID SMBus transaction supports a constant command value of 0x03 and, if directed,
supports a Dynamic command value equal to the dynamic SMBus address.
If the SMBus address has been resolved (Address Resolved flag set to true), the manageability system
does not acknowledge (NACK) this transaction. If it’s a General command, the manageability system
always acknowledges (ACKs) as a directed transaction.
This command does not affect the status or validity of the dynamic SMBus address or the Address
Resolved flag.

  S     Slave Address         Wr       A             Command          A       S       ···

             1100 001             0     0            See Below        0

         7              1         1                        8                  1

  Slave Address         Rd        A                  Byte Count               A       ···

      1100 001          1         0                  0001 0001                0

             8               1                   8                1           8                 1               8          1

         Data 1              A                 Data 2             A         Data 3              A             Data 4       A    ···

 UDID Byte 15 (MSB)           0             UDID Byte 14          0    UDID Byte 13             0          UDID Byte 12    0

             8               1                   8                1           8                 1               8          1

         Data 5              A                 Data 6             A         Data 7              A             Data 8       A    ···

      UDID Byte 11            0             UDID Byte 10          0       UDID Byte 9           0          UDID Byte 8     0

             8               1                   8                1           8                 1

         Data 9              A                Data 10             A         Data 11             A    ···

      UDID Byte 7             0             UDID Byte 6           0       UDID Byte 5           0

             8               1                   8                1           8                 1               8          1

        Data 12               A               Data 13             A         Data 14             A            Data 15       A    ···

      UDID Byte 4             0             UDID Byte 3           0       UDID Byte 2           0          UDID Byte 1     0

             8               1                   8                1           8                 1     1

        Data 16               A               Data 17             A          PEC               ~Ã     P

                                                                      [Data Dependent
  UDID Byte 0 (LSB)           0       Device Slave Address        0                             1
                                                                           Value]

The Get UDID command depends on whether this is a Directed or General command.
The General Get UDID SMBus transaction supports a constant command value of 0x03.

980                                                                                                                       333369-009
                                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

The Directed Get UDID SMBus transaction supports a Dynamic command value equal to the dynamic
SMBus address with the LSB bit set.
Note:        Bit 0 (LSB) of Data byte 17 is always 1b.

### 11.5.11 SMBus Pass-Through Transactions

This section details commands (both read and write) that the X550 SMBus interface supports for pass-
through.

#### 11.5.11.1 Write SMBus Transactions

This section details the commands that the BMC can send to the X550 over the SMBus interface. The
SMBus write transactions table lists the different SMBus write transactions supported by the X550.

                                                                                                           Section
               TCO Command                    Transaction             Command             Fragmentation
                                                                                                           Number

                                                                      First: 0x84
Transmit Packet                               Block Write            Middle: 0x04             Multiple    11.5.11.1.1
                                                                      Last: 0x44

Transmit Packet                               Block Write            Single: 0xC4              Single     11.5.11.1.1

Request Status                                Block Write            Single: 0xDD              Single     11.5.11.1.2

Receive Enable                                Block Write            Single: 0xCA              Single     11.5.11.1.3

Force TCO                                     Block Write            Single: 0xCF              Single     11.5.11.1.4

Management Control                            Block Write            Single: 0xC1              Single     11.5.11.1.5

Update MNG RCV Filter Parameters              Block Write            Single: 0xCC              Single     11.5.11.1.6

Set Common Filters                            Block Write            Single: 0xC2              Single     11.5.11.1.7

Clear All Filters                             Block Write            Single: 0xC3              Single     11.5.11.1.8

Set Thermal Sensor Configuration              Block Write      Single: 0xCB (index = 1)        Single     11.5.11.1.9

Perform Thermal Sensor Action                 Block Write       Single: 0xCB(index = 2)        Single     11.5.11.1.10

11.5.11.1.1                Transmit Packet Command

The Transmit Packet command behavior is detailed in Section 11.5.8. The Transmit Packet fragments
have the following format.
The payload length is limited to the maximum payload length set in the NVM. If the overall packet
length is bigger than 1536 bytes, the packet is silently discarded.

          Function              Command    Byte Count           Data 1         …          Data N

Transmit first fragment            0x84        N            Packet data MSB     …     Packet data LSB

Transmit middle fragment           0x04

Transmit last fragment             0x44

Transmit single fragment           0xC4

333369-009                                                                                                         981
                                     Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                              System Manageability

11.5.11.1.2                 Request Status Command

An external BMC can initiate a request to read the X550 manageability status by sending a Request
Status command. When received, the X550 initiates a notification to an external BMC when status is
ready. After this, the external controller is able to read the status, by issuing a read status command
(see Section 11.5.11.2.2).
The format is as follows:

      Function         Command       Byte Count             Data 1

Request Status          0xDD               1                    0

11.5.11.1.3                 Receive Enable Command

The Receive Enable command is a single fragment command used to configure the X550. This
command has two formats: short, 1-byte legacy format (providing backward compatibility with
previous components) and long, 14-byte advanced format (allowing greater configuration capabilities).
The Receive Enable command format is as follows:

                            Byte
 Function        CMD                Data 1       Data 2     …       Data 7   Data 8      …   Data 11     Data 12      Data 13     Data 14
                           Count

Legacy           0xCA        1      Receive         -       …         -          -       …       -            -           -           -
Receive                             Control
Enable                               Byte

Advanced                   14                     MAC                MAC     IP Addr          IP Addr       BMC       I/F Data      Alert
Receive                  (0x0E)                   Addr               Addr      MSB              LSB        SMBus        Byte        Value
Enable                                            MSB                LSB                                    Addr                    Byte

      Field       Bit(s)                                                     Description

RCV_EN              0        Receive TCO Enable.
                              0b = Disable receive TCO packets.
                              1b = Enable Receive TCO packets.
                             Setting this bit enables all manageability receive filtering operations. Enabling specific filters is done via
                             the NVM or through special configuration commands.
                             Note: When the RCV_EN bit is cleared, all receive TCO functionality is disabled, not just the packets
                                      that are directed to the BMC (also auto ARP packets).

RCV_ALL             1        Receive All Enable.
                              0b = Disable receiving all packets.
                              1b = Enable receiving all packets.
                             Forwards all packets received over the wire that passed L2 filtering to the external BMC. This flag has no
                             effect if bit 0 (Enable TCO packets) is disabled.

EN_STA              2        Enable Status Reporting.
                              0b = Disable status reporting.
                              1b = Enable status reporting.

982                                                                                                                              333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

     Field      Bit(s)                                                 Description

EN_ARP_RES        3      Enable ARP Response.
                           0b = Disable the X550 ARP response — The X550 treats ARP packets as any other packet, for
                                 example, packet is forwarded to the BMC if it passed other (non-ARP) filtering.
                           1b = Enable the X550 ARP response — The X550 automatically responds to all received ARP requests
                                 that match the IP Address programmed by the BMC. The BMC IP Address is provided as part of
                                 the Receive Enable message (bytes 8:11). If a short version of the command is used, the X550
                                 uses IP Address configured in the most recent long version of the command in which the
                                 EN_ARP_RES bit was set. If no such previous long command exists, the X550 uses the IP
                                 Address configured in the NVM as ARP Response IPv4 Address in the pass-through LAN
                                 configuration structure.
                         If the CBDM bit is set, the X550 uses the BMC dedicated MAC Address in ARP response packets. If the
                         CBDM bit is not set, the BMC uses the host MAC Address.
                         When the ARP offload feature is activated, the X550 uses the following registers to filter the ARP traffic
                         addressed to the BMC. BMC should not modify these registers:
                         Manageability Decision Filter – MDEF6 (and corresponding bit 6 in Management Only traffic Register –
                         MNGONLY).
                         IPv4 address - MIPAF4[3]

NM               5:4     Notification Method. Define the notification method the X550 uses.
                          00b = SMBUS Alert.
                          01b = Asynchronous notify.
                          10b = Direct receive.
                          11b = Not supported.
                         Changing the notification method in any port updates the notification method of all ports.

Reserved          6      Reserved. Must be set to 1b.

CBDM              7      Configure the BMC Dedicated MAC Address.
                         Note: This bit should be 0b when the RCV_EN bit (bit 0) is not set.
                           0b = The X550 shares the MAC Address for MNG traffic with the host MAC Address, which is specified
                                 in NVM words 0x0-0x2.
                           1b = The X550 uses the BMC dedicated MAC Address as a filter for incoming receive packets.
                         The BMC MAC Address is set in bytes 2-7 in this command.
                         If a short version of the command is used, the X550 uses the MAC Address configured in the most
                         recent long version of the command in which the CBDM bit was set.
                         When the dedicated MAC Address feature is activated, the X550 uses the following registers to filter in
                         all the traffic addressed to the BMC MAC. BMC should not modify these registers:
                         Manageability Decision Filter – MDEF7 (and corresponding bit 7 in Management Only traffic Register –
                         MNGONLY)
                         Manageability MAC Address Low – MMAL[3]
                         Manageability MAC Address High – MMAH[3]
                         When the dedicated MAC Address feature is cleared, these registers are not programmed and the BMC
                         may use other filters to enforce MAC filtering using the Update Management Receive Filter Parameters
                         command.

11.5.11.1.3.1            Management MAC Address (Data Bytes 7:2)

Ignored if the CBDM bit is not set. This MAC Address is used to configure the dedicated MAC Address. In
addition, it is used in the ARP response packet when the EN_ARP_RES bit is set. This MAC Address is
also used when CBDM bit is set in subsequent short versions of this command.

11.5.11.1.3.2            Management IP Address (Data Bytes 11:8)

This IP Address is used to filter ARP request packets.

11.5.11.1.3.3            Asynchronous Notification SMBus Address (Data Byte 12)

This address is used for the asynchronous notification SMBus transaction and for direct receive. The
SMBus address is stored in bit 7:1 of this byte. Bit 0 is always 0b.

333369-009                                                                                                                      983
                                    Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                          System Manageability

11.5.11.1.3.4                Interface Data (Data Byte 13)

Interface data byte used in asynchronous notification.

11.5.11.1.3.5                Alert Value Data (Data Byte 14)

Alert Value data byte used in asynchronous notification.

11.5.11.1.4              Force TCO Command

This command causes the X550 to perform a TCO reset, TCO isolate, or firmware reset.
TCO Reset:
      The Force TCO reset clears the data path (Rx/Tx) of the X550 to enable the BMC to transmit/receive
      packets through the X550 by assertion of a global reset. Force TCO reset is asserted only to the
      port related to the SMBus address the command. This command should only be used when the BMC
      is unable to transmit receive and suspects that the X550 is inoperable. The command also causes
      the LAN device driver to unload. It is recommended to perform a system restart to resume normal
      operation.
Firmware Reset:
      This command causes re-initialization of all the embedded controller functions and re-load of
      related NVM words. A firmware reset is achieved by setting the GSCR.SET_FWRST Aux bit.
The X550 considers the Force TCO reset command as an indication that the operating system is hung.
The Force TCO command format is as follows:

      Function       Command       Byte Count             Data 1

 Force TCO Reset        0xCF            1              TCO Mode

Where TCO Mode is:

        Field          Bit(s)                                             Description

 DO_TCO_RST              0      Perform TCO Reset.
                                 0b = Do nothing.
                                 1b = Perform TCO reset.

 DO_TCO_ISOLATE1         1      Do TCO Isolate
                                 0b = Enable PCIe write access to LAN port.
                                 1b = Isolate Host PCIe write operation to the port
                                Note: Should be used for debug only.

 RESET_MGMT              2      Reset manageability; re-load manageability NVM words.
                                 0b = Do nothing.
                                 1b = Issue firmware reset to manageability.
                                Setting this bit generates a one-time firmware reset. Following the reset, management related
                                data from NVM is loaded.

 Reserved               7:3     Reserved (set to 0x00).

1. TCO Isolate Host Write operation enabled in NVM.

Note:       Only one of the fields should be set in a given command. Setting more than one field may
            yield unexpected results.

984                                                                                                                  333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.5.11.1.5             Management Control

This command is used to set generic manageability parameters. The parameters list is shown in
Table 11-10. The command is 0xC1 stating that it is a Management Control command. The first data
byte is the parameter number and the data afterwards (length and content) are parameter specific as
shown in Management Control Command Parameters/Content.
Note:        If the parameter that the BMC sets is not supported by the X550. The X550 does not NACK
             the transaction. After the transaction ends, the X550 discards the data and asserts a
             transaction abort status.
The Management Control command format is as follows:

        Function        Command      Byte Count            Data 1                 Data 2            …          Data N

Management Control          0xC1           N         Parameter Number                    Parameter Dependent

Table 11-10. Management Control Command Parameters/Content
    Parameter           #                                             Parameter Data

Keep PHY Link Up       0x00   A single byte parameter.
                              Data 2:
                               Bit 0: Set to indicate that the PHY link for this port should be kept up throughout system resets.
                                       This is useful when the server is reset and the BMC needs to keep connectivity for a
                                       manageability session.
                               Bit [7:1] Reserved.
                               0b = Disabled.
                               1b = Enabled.

11.5.11.1.6             Update Management Receive Filter Parameters

This command is used to set the manageability receive filters parameters. The command is 0xCC. The
first data byte is the parameter number and the data that follows (length and content) are parameter
specific as listed in management RCV filter parameters.
If the parameter that the BMC sets is not supported by the X550, the X550 does not NACK the
transaction. After the transaction ends, the X550 discards the data and asserts a transaction abort
status.
The update management RCV receive filter parameters command format is as follows:

        Function        Command      Byte Count            Data 1                 Data 2            …          Data N

Update Manageability
                            0xCC           N         Parameter Number                    Parameter Dependent
Filter Parameters

Table 11-11 lists the different parameters and their content.

333369-009                                                                                                                     985
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

Table 11-11. Management Receive Filter Parameters
       Parameter            Number                                          Parameter Data

Filters Enables              0x1       Defines the generic filters configuration. The structure of this parameter is four bytes as
                                       the Manageability Control (MANC) register (see Table 11-12).
                                       Note: The general filter enable is in the Receive Enable command that enables receive
                                                filtering.

MNGONLY configuration        0xF       This parameter defines which of the packets types identified as manageability packets in
                                       the receive path is never directed to the host memory.
                                         Data 2:5 = MNGONLY register bytes (see Section 8.2.2.19.8) - Data 2 is the MSB.

Flex Filter 0 Enable Mask    0x10      Flex Filter 0 Mask.
and Length                               Data 17:2 = Mask. Bit 0 in data 2 is the first bit of the mask.
                                         Data 19:18 = Reserved. Should be set to 00b.
                                         Date 20 =     Flexible filter length.

Flex Filter 0 Data           0x11      Data 2 — Group of flex filter’s bytes:
                                        0x0 = bytes 0-29
                                        0x1 = bytes 30-59
                                        0x2 = bytes 60-89
                                        0x3 = bytes 90-119
                                        0x4 = bytes 120-127
                                        Data 3:32 = Flex filter data bytes. Data 3 is LSB.
                                       Group's length is not a mandatory 30 bytes; it might vary according to filter's length and
                                       must NOT be padded by zeros.

Decision Filters             0x61      This command is obsolete and should not be used anymore. Use 0x68 instead.

VLAN Filters                 0x62      3 bytes are required to load the VLAN tag filters.
                                        Data 2 = VLAN filter number.
                                        Data 3 = MSB of VLAN filter.
                                        Data 4 = LSB of VLAN filter.

Flex Port Filters            0x63      3 to 4 bytes are required to load the manageability flex port filters.
                                        Data 2 = Flex port filter number.
                                        Data 3 = MSB of flex port filter.
                                        Data 4 = LSB of flex port filter.

IPv4 Filters                 0x64      5 bytes are required to load the IPv4 address filter.
                                        Data 2 = IPv4 address filter number (3:0).
                                        Data 3 = LSB of IPv4 address filter.
                                        …
                                        Data 6 = MSB of IPv4 address filter.

IPv6 Filters                 0x65      17 bytes are required to load the IPv6 address filter.
                                        Data 2 = IPv6 address filter number (3:0).
                                        Data 3 = LSB of IPv6 address filter.
                                        …
                                        Data 18 = MSB of IPv6 address filter.

MAC Filters                  0x66      7 bytes are required to load the MAC Address filters.
                                        Data 2 = MAC Address filters pair number (3:0).
                                        Data 3 = MSB of MAC Address.
                                        …
                                        Data 8 = LSB of MAC Address.

986                                                                                                                    333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-11. Management Receive Filter Parameters [continued]
         Parameter            Number                                         Parameter Data

EtherType Filters              0x67      5 bytes to load EtherType Filters (METF)
                                          Data 2 = METF filter index (valid values are 0, 1, 2, 3).
                                          Data 3 = MSB of METF.
                                          ...
                                          Data 6 = LSB of METF.

Extended Decision Filter       0x68      9 bytes to load the extended decision filters (MDEF_EXT & MDEF)
                                          Data 2 — MDEF filter index (valid values are 0...5).
                                          Data 3 — MSB of MDEF_EXT (DecisionFilter1).
                                          ...
                                          Data 6 — LSB of MDEF_EXT (DecisionFilter1).
                                          Data 7 — MSB of MDEF (DecisionFilter0).
                                          ...
                                          Data 10 — LSB of MDEF (DecisionFilter0).
                                         The command overwrites any previously stored value.

Table 11-12. Filter Enable Parameters
  Bit               Name                                                   Description

  16:0     Reserved             Reserved.

# 17 RCV_TCO_EN           Receive TCO Packets Enabled

                                When this bit is set it enables the receive flow to the manageability block.
                                This bit should be set only if at least one of EN_BMC2OS or EN_BMC2NET bits are set.
                                This bit is usually set using the receive enable command (see Section 11.5.11.1.3).

# 18 Reserved             Reserved.

 22:19     Reserved             Reserved.

# 23 Enable Xsum          When this bit is set, only packets that pass the L3 and L4 checksum are send to the manageability

           Filtering to MNG     block.

# 24 EN_IPV4_FILTER       Enable IPv4 address Filters

                                 0b = These bits store a single IPv6 filter.
                                 1b = The last 128 bits of the MIPAF register are used to store 4 IPv4 addresses for IPv4 filtering.

# 25 FIXED_NET_TYPE       Fixed Net Type

                                 0b = Both tagged and un-tagged packets can be forwarded to the manageability engine.
                                 1b = Only packets matching the net type defined by the NET_TYPE field passes to manageability.

# 26 NET_TYPE             Net Type

                                 0b = Pass only un-tagged packets.
                                 1b = Pass only VLAN tagged packets.
                                Valid only if FIXED_NET_TYPE is set.

 31:27     Reserved             Reserved.

11.5.11.1.7                Set Common Filters Command

The Set Common Filters command is a single fragment command capable of configuring the most
common filters.
Note:        If this command is used, all the other commands that programs forwarding filters should not
             be used (apart from the Clear All Filters command). When this command is received, an
             implied Clear All Filters command is done before the application of this command.

333369-009                                                                                                                       987
                                       Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                             System Manageability

The Set Common Filters command has two possible formats:
IPv4 Format:

                                                                                       Data
                                 Byte
  Function         Command
                                Count
                                             1            2:4           5:10             11           12          13         14:17

Set Common          0xC2         17        Opcode      Receive          MAC           BMC Alert   Interface   Alert Value     IPv4
Filters                                     =0       Control (see      Address         Address    Data Byte      Byte        Address
                                                     Table 11-13)

IPv6 Format:

                                                                                       Data
                                 Byte
  Function         Command
                                Count
                                             1            2:4           5:10             11           12          13         14:29

Set Common          0xC2         29        Opcode      Receive          MAC           BMC Alert   Interface   Alert Value     IPv6
Filters                                     =0       Control (see      Address         Address    Data Byte      Byte        Address
                                                     Table 11-13)

Table 11-13. Set Common Filters Receive Control Bytes
 Byte        Bit                Field                                                   Description

      1      0       RCV_EN                         Receive TCO Packets Enabled.
                                                     1b = Enables the receive flow to the manageability block.
                                                    This bit should be set only if at least one of EN_BMC2O or EN_BMC2NET bits are
                                                    set.

# 1 EN_STA                         Enable Status Reporting.

                                                     0b = Disable status reporting.
                                                     1b = Enable status reporting.

# 2 Auto ARP                       Automatically respond to ARP packets.

                                                    Ignored in IPv6 mode. If this bit is set, broadcast ARP packets are handled by the
                                                    X550 and ARP requests to the IP Address set in the command are responded.
                                                    Mutually exclusive to Configure ARP/ Neighborhood Filter bit.
                                                    If this bit is set, the IP Address must be valid and contain the IP Address of the
                                                    MC.
                                                    This bit is ignored if RCV_EN is cleared.
                                                    When set, ARP requests to the BMC IP defined below (unicast or Broadcast) are
                                                    sent to the internal firmware for processing. ARP response are dropped.

# 3 Enable Xsum Filtering to       When this bit is set, only packets that pass the L3 and L4 checksum are send to

                     MNG                            the manageability block.
                                                    This bit is ignored if RCV_EN is cleared.

             5:4     Reserved

             7:6     Notification Method            Notification Method. Define the notification method the X550 uses.
                                                     00b = SMBUS Alert.
                                                     01b = Asynchronous notify.
                                                     10b = Direct receive.
                                                     11b = Not supported.

988                                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-13. Set Common Filters Receive Control Bytes [continued]
  Byte       Bit              Field                                                 Description

   2         8     CBDM                       Configure the BMC Dedicated MAC Address.
                                                0b = The X550 shares the MAC Address for MNG traffic with the host MAC
                                                      Address, which is specified in RAH/RAL[0] registers
                                                1b = The X550 uses the BMC dedicated MAC Address as a filter for incoming
                                                      receive packets.
                                              The BMC MAC Address is set in bytes 5-10 in this command.
                                              This bit is ignored if RCV_EN is cleared.
                                              If this bit is cleared, at least one of bits 9,10 or 11 must be set. If only bit 9 is set,
                                              the IP Address should be different than the address used by the host.

# 9 Configure IP Address       Automatically configure an IP Address Filter. If this bit is set, only packets

                   Filter                     matching this IP Address and the MAC Address defined by the CBDM bit are
                                              forwarded. This bit is ignored if RCV_EN is cleared.

# 10 Configure RMCP 26Fh        Automatically configure standard IPMI port 26Fh filters. If this bit is set, only

                   Filter                     packets matching this port and the MAC Address defined by the CBDM bit are
                                              forwarded. If the Configure IP Address Filter bit is set, only packets matching the
                                              IP Address and this port are forwarded. The other port enable bit (11) may add
                                              additional forwarding condition.
                                              This bit is ignored if RCV_EN is cleared.

# 11 Configure RMCP 298h        Automatically configure standard IPMI port 298h filter. If this bit is set, only

                   Filter                     packets matching this port and the MAC Address defined by the CBDM bit are
                                              forwarded. If the Configure IP Address Filter bit is set, only packets matching the
                                              IP Address and this port are forwarded. The other port enable bit (10) may add
                                              additional forwarding condition.
                                              This bit is ignored if RCV_EN is cleared.

# 12 Configure ARP/             Automatically Configure filters to allow this traffic to BMC (mutually exclusive to

                   Neighborhood Filter        Auto ARP bit). If this bit is set, broadcast or unicast ARP packets are forwarded to
                                              BMC. These packets may be sent to the host also.
                                              In IPv4 mode, setting this bit allows forwarding of broadcast or unicast ARP
                                              request and response. If IP Address is set, only request or response to this
                                              address is forwarded.
                                              In IPv6 mode, setting this bit allows forwarding of all types of neighbor discovery
                                              and MLD ICMPv6 packet types:
                                                0x86 (134d) - Router Advertisement.
                                                0x87 (135d) - Neighbor Solicitation.
                                                0x88 (136d) - Neighbor Advertisement.
                                                0x89 (137d) - Redirect
                                                0x82 (130d) - MLD Query
                                                0x83 (131d) - MLDv1 Report
                                                0x84 (132d) - MLD Done
                                                0x8F (143d) - MLDv2 Report
                                              This bit is ignored if RCV_EN is cleared.

# 13 Configure DHCP port 44h    Automatically configure DHCP port 44 filter to BMC. If this bit is set, broadcast

                   Filter (DHCP server        packets matching this port are forwarded. Otherwise, this port is not added to the
                   packets)                   broadcast filtering option.
                                              This bit is ignored if RCV_EN is cleared or in IPv6 mode.

          15:14    Reserved

   3         16    Disable Host ARP           Configure ARP Requests and Network Neighborhood packets not to go to host. This
                                              bit should be cleared in regular operation. Ignored if both bit 12 and bit 2 are
                                              cleared or if RCV_EN is cleared.

# 17 Disable Host DHCP          Configure DHCP packets (port 44h) not to go to host. This bit should be cleared in

                                              regular operation. Ignored if bit 13 is cleared, RCV_EN is cleared, or in IPv6 mode.

          24:18    Reserved

333369-009                                                                                                                           989
                                      Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                             System Manageability

11.5.11.1.8                 Clear all Filters Command

The Clear all Filters command is a single fragment command capable of clearing all the receive filters
currently programmed for manageability traffic.

      Function          Command          Byte Count           Data

Clear all Filters           0xC3             1                    0x00

11.5.11.1.9                 Set Thermal Sensor Configuration

This command sets the thermal sensor configuration for threshold Index in direction Direction, where
the threshold is measured in “unit types”, and the Actions field describes the actions to activate upon
crossing of the threshold in the requested direction according to Table 11-39.
Direction is encoded as follows:
      0 = High Going
      1 = Low Going

                                                                                        Data
                                    Byte
  Function          Command
                                   Count
                                                 1            2             3           4:5         6:9      10:13        14

Set Thermal          0xCB           14         Sub        Index          Direction    Threshold    Actions   Actions   Hysteresis
Sensor                                       Opcode                                                “Going    “Going
Configuration                                 (0x1)                                                 High”     Low”

11.5.11.1.10                Perform Thermal Sensor Action

This command executes actions immediately.
The Actions field describes the actions to activate according to Table 11-39.

             Function                    Command      Byte Count             Data 1               Data 2:5

Perform Thermal Sensor Action              0xCB           5              Sub Opcode (0x2)         Actions

990                                                                                                                    333369-009
                                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.5.11.2 Read SMBus Transactions

This section details the pass-through read transactions that the BMC can send to the X550 over SMBus.
SMBus read transactions lists the different SMBus read transactions supported by the X550. All the read
transactions are compatible with SMBus read block protocol format.

Table 11-14. SMBus Read Transactions
                                                  Write                                                            Section
      TCO Command             Transaction                       Read Command          Opcode        Fragments
                                                Command1                                                           Number

                                                                                     First: 0x90
 Receive TCO Packet            Block Read           N/A           0xD0 or 0xC0      Middle: 0x10      Multiple    11.5.11.2.1
                                                                                    Last2: 0x50

                                                                 0xD0 or 0xC0 or
 Read Status                   Block Read           N/A                             Single: 0xDD      Single      11.5.11.2.2
                                                                      0xDE

 Get System MAC Address        Block Read           N/A               0xD4          Single: 0xD4      Single      11.5.11.2.3

 Read Management
                               Block Read          0xC1               0xD1          Single: 0xD1      Single      11.5.11.2.4
 Parameters

 Read Management RCV
                               Block Read          0xCC               0xCD          Single: 0xCD      Single      11.5.11.2.5
 Filter Parameters

 Get Controller Information    Block Read          0xD5               0xD5          Single: 0xD5      Single      11.5.11.2.6

 Get Common filters            Block Read          0xD3               0xD3          Single: 0xD3      Single      11.5.11.2.7

 Read Receive Enable
                               Block Read           N/A               0xDA          Single: 0xDA      Single      11.5.11.2.8
 Configuration

 Get Thermal Sensor
                               Block Read    0xCB (index = 0)   0xDB (index = 0)    Single: 0xDB      Single      11.5.11.2.9
 Capabilities

 Get Thermal Sensor
                               Block Read    0xCB (index = 1)   0xDB (index = 1)    Single: 0xDB      Single     11.5.11.2.10
 Configuration

 Get Thermal Sensor Status     Block Read    0xCB (index = 2)   0xDB (index = 2)    Single: 0xDB      Single     11.5.11.2.11

1. In some commands, a preliminary write command is sent to ask the firmware to prepare the data for the upcoming read command.
   This column describes the opcode used for the write command.
2. The last fragment of the receive packet is the packet status.

0xC0 or 0xD0 commands are used for more than one payload. If BMC issues these read commands,
and the X550 has no pending data to transfer, it always returns as default opcode 0xDD with the X550
status and does not NACK the transaction.
If an SMBus quick read command is received, it is handled as a X550 Request Status command (See
Section 11.5.11.1.2 for details).

333369-009                                                                                                                 991
                                     Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                System Manageability

11.5.11.2.1               Receive TCO LAN Packet Transaction

The BMC uses this command to read packets received on the LAN and its status. When the X550 has a
packet to deliver to the BMC, it asserts the SMBus notification for the BMC to read the data (or direct
receive). Upon receiving notification of the arrival of a LAN receive packet, the BMC begins issuing a
Receive TCO packet command using the block read protocol.
A packet can be transmitted to the BMC in at least two fragments (at least one for the packet data and
one for the packet status). As a result, BMC should follow the F and L bit of the opcode.
The opcode can have these values:
 • 0x90 — First Fragment
 • 0x10 — Middle Fragment
 • 0x50 — Indicates the last fragment of the packet, which contains packet status.
If a notification timeout is defined (in the NVM - Section 6.2.17.3) and the BMC does not finish reading
the whole packet within the timeout period, since the packet has arrived, the packet is silently
discarded. The time spent in ARA cycle or in reading the packet is not counted by the timeout counter.
Following is the receive TCO packet format and the data format returned from the X550.

       Function                Command

Receive TCO Packet            0xC0 or 0xD0

          Function               Byte Count   Data 1 (Opcode)          Data 2          …          Data N

Receive TCO First Fragment                         0x90
                                      N                            Packet Data Byte    …     Packet Data Byte
Receive TCO Middle Fragment                        0x10

Receive TCO Last Fragment          9 (0x9)         0x50                     See Section 11.5.11.2.1.1

11.5.11.2.1.1             Receive TCO LAN Status Payload Transaction

This transaction is the last transaction that the X550 issues when a packet received from the LAN is
transferred to the BMC. The transaction contains the status of the received packet.
The format of the status transaction is as follows:

                                                Data 1          Data 2 – Data 17
         Function              Byte Count
                                               (Opcode)          (Status Data)

Receive TCO Long Status          9 (0x9)         0x50              See Below

The status is 8 bytes where byte 0 (bits 7:0) is set in Data 2 of the status and byte 7 in Data 9 of the
status. Table 11-15 lists the content of the status data.

992                                                                                                         333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-15. TCO LAN Packet Status Data
       Name              Bit(s)                                              Description

Packet Length            13:0     Packet length including CRC, only 14 LSB bits.

Reserved                 15:14    Reserved.

Packet status            31:16    See Table 11-16.

VLAN                     47:32    The two bytes of the VLAN header tag.

MNG status               63:48    See Table 11-17. This field should be ignored if Receive is not enabled.

Table 11-16.           Packet Status Info
        Field            Bit(s)                                              Description

CRC stripped               0      Insertion of CRC is needed.

VP                         1      VLAN Stripped (indicates if the VLAN is part of the packet, or was removed).

LAN#                      3:2     Indicates the source port of the packet:
                                   00b = Port 0
                                   01b = Port 1
                                   10b = Reserved
                                   11b = Reserved

Reserved                 15:4     Reserved.

Table 11-17.           MNG Status
                Name                 Bits                                          Description

 Pass MNG VLAN Filter Index           2:0     Indicates which of the VLAN filters match the packet.

 MNG VLAN Address Match                3      Set when the MNG packet matches one of the MNG VLAN filters.

Decision Filter index                 7:4     Indicates which of the decision filters match the packet.
                                              Allows for up to 16 filters, although only 8 are currently supported.

Decision Filter match                  8      Set when there is a match to one of the Decision filters.

Reserved                             15:9     Reserved.

11.5.11.2.2                Read Status Command

The BMC should use this command after receiving a notification from the X550 (such as SMBus Alert).
The X550 also sends a notification to the BMC in either of the following two cases:
 • The BMC asserts a request for reading the status.
 • The X550 detects a change in one of the Status Data 1 bits (and was set to send status to the BMC
   on status change) in the Receive Enable command.
Note:        Commands 0xC0/0xD0 are for backward compatibility and can be used for other payloads.
             The X550 defines these commands in the opcode as well as which payload this transaction is.
             When the 0XDE command is set, the X550 always returns opcode 0XDD with the X550 status.
             The BMC reads the event causing the notification, using the Read Status command as follows.
             The X550 response to one of the commands (0xC0 or 0xD0) in a given time as defined in the
             SMBus Notification Timeout and Flags word in the NVM.

333369-009                                                                                                            993
                                       Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                              System Manageability

          Function                      Command

 Read Status                      0XC0 or 0XD0 or 0XDE

                                                            Data 1               Data 2                    Data 3
           Function                 Byte Count
                                                           (Opcode)          (Status Data 1)           (Status Data 2)

 Receive TCO Partial Status                3                 0XDD                             See Below

This command can also be executed using the I2C quick read format as follows:

   1             7            1        1               8              1             8              1             8             1      1

 Start    Slave Address       Rd       Ack        Byte Count          Ack     Status Data 1       Ack       Status Data 2     Ack   Stop

                              1        0          0000 0002           0                            0                           1

Table 11-18 lists the status data byte 1 parameters.

Table 11-18.          Status Data Byte 1
   Bit                Name                                                          Description

   1:0     Power State                     00b = Dr state
                                           01b = D0u state
                                           10b = D0 state
                                           11b = D3 state

# 2 Reserved

# 3 Initialization Indication       0b = An NVM reload event has not occurred since the last Read Status cycle.

                                           1b = An NVM reload event has occurred since the last Read Status cycle1.

    4 PHY Link Forced Up              Contains the value of the PHY_Link_Up bit. When set, indicates that the PHY link is configured

                                           to keep the link up.

# 5 Link Status Indication          0b = LAN link down.

                                           1b = LAN link up.

    6 TCO Command Aborted             0b = A TCO command abort event did not occur since the last read status cycle.

                                           1b = A TCO command abort event occurred since the last read status cycle.

    7 LAN Port                        LAN port. Defines the port that sent status.

1. This indication is asserted when the X550 manageability block reloads the NVM and its internal database is updated to the NVM
   default values. This is an indication that the external BMC should reconfigure the X550, if other values other than the NVM default
   should be configured.

Status data byte 2 is used by the BMC to indicate whether the LAN device driver is alive and running,
and for thermal events.
The LAN device driver valid indication is a bit set by the LAN device driver during initialization; the bit is
cleared when the LAN device driver enters a Dx state or is cleared by the hardware on a PCI reset.
Table 11-19 lists status data byte 2.

994                                                                                                                           333369-009
                                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-19. Status Data Byte 2
  Bit                 Name                                                        Description

# 0 Thermal Sensor event       0b = No thermal event

                                         1b = Thermal event asserted.

  2:1         Reserved                   Reserved.

# 3 Driver Valid Indication    0b = LAN driver is not alive.

                                         1b = LAN driver is alive.

  5:4         Reserved                   Reserved.

# 6 Configuration Change       0 = No change.

                                         1 = Number of enabled ports changed.

# 7 Reserved                   Reserved.

Table 11-20 lists the possible values of bits 2 and 1 and what the BMC can assume from the bits.

Table 11-20. Status Data Byte 2 (Bits 2 and 1)
   Previous            Current                                                  Description

  Don’t Care             00b        Interrupt is not pending (OK).

        00b              01b        New interrupt is asserted (OK).

        10b              01b        New interrupt is asserted (OK).

        11b              01b        Interrupt is waiting for reading (OK).

        01b              01b        Interrupt is waiting for reading by the driver for more than one read cycle (not OK).
                                    Possible drive hang state.

  Don’t Care             11b        Previous interrupt was read and current interrupt is pending (OK).

  Don’t Care             10b        Interrupt is not pending (OK).

BMC reads should consider the time it takes for the LAN device driver to deal with the interrupt (in s).
Note that excessive reads by the BMC can give false indications.

11.5.11.2.3                    Get System MAC Address

The Get System MAC Address returns the system MAC Address over to the SMBus. This command is a
single-fragment Read Block transaction that returns the following the MAC Address configured in RAL0,
RAH0 registers.
Get system MAC Address format:

              Function                  Command

Get system MAC Address                      0xD4

Data returned from the X550:

          Function               Byte Count        Data 1 (Opcode)            Data 2            …          Data 7

Get system MAC Address                  7                0xD4            MAC Address MSB        …    MAC Address LSB

333369-009                                                                                                                  995
                                             Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

11.5.11.2.4            Read Management Parameters

To read the management parameters the BMC should execute two SMBus transactions. The first
transaction is a block write that sets the parameter that the BMC wants to read. The second transaction
is block read that reads the parameter.
Block write transaction:

           Function          Command        Byte Count            Data 1

Management control request      0xC1              1          Parameter number

Following the block write the BMC should issue a block read that reads the parameter that was set in
the Block Write command:

           Function          Command

Read management parameter       0xD1

Data returned:

           Function          Byte Count       Data 1 (Opcode)              Data 2            Data 3      …     Data N

Read management parameter          N                  0xD1           Parameter number          Parameter dependent

The returned data is in the same format of the BMC command.
The returned data is as follows:

      Parameter        #                                              Parameter Data

Keep PHY Link Up      0x00   A single byte parameter.
                             Data 2:
                              Bit [0] =   Set to indicate that the PHY link for this port should be kept up. When set, sets the
                                          keep_PHY_link_up bit. When cleared, clears the keep_PHY_link_up bit.
                              Bit [7:1] = Reserved.

Wrong parameter       0xFE   Returned by the X550 only. This parameter is returned on read transaction, if in the previous
request                      read command the BMC sets a parameter that is not supported by the X550.

The X550 is not       0xFF   Returned by the X550 only, on read parameters command when the data that should have been
ready                        read is not ready. This parameter has no data. The BMC should retry the read transaction.
                             This value is also returned if the byte count is illegal or if the read command is not preceded by a
                             write command.

The parameter that is returned might not be the parameter requested by the BMC. The BMC should
verify the parameter number (default parameter to be returned is 0x1).
If the parameter number is 0xFF, it means that the data that was requested from the X550 is not ready
yet, or that the adequate write command was not given.The BMC should retry the read transaction or
send the write transaction.
It is responsibility of the BMC to follow the procedure previously defined. When the BMC sends a Block
Read command (as previously described) that is not preceded by a Block Write command with
bytecount=1, the X550 sets the parameter number in the read block transaction to be 0xFF.

996                                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.5.11.2.5                 Read Management Receive Filter Parameters

To read the management receive filter parameters, the BMC should execute two SMBus transactions.
The first transaction is a block write that sets the parameter that the BMC wants to read. The second
transaction is block read that read the parameter.
Block write transaction:

       Function             Command       Byte Count            Data 1                Data 2

Update MNG RCV filter
                              0xCC           1 or 2       Parameter number         Parameter data
parameters

The different parameters supported for this command are the same as the parameters supported for
update Management receive filter parameters.
Following the block write the BMC should issue a block read that reads the parameter that was set in
the Block Write command:

                 Function                 Command

Request MNG RCV filter parameters            0xCD

Data returned from the X550:

     Function             Byte Count     Data 1 (Opcode)             Data 2           Data 3    …    Data N

Read MNG RCV filter
                              N                   0xCD          Parameter number        Parameter dependent
parameters

The parameter that is returned might not be the parameter requested by the BMC. The BMC should
verify the parameter number (default parameter to be returned is 0x1).
If the parameter number is 0xFF, it means that the data that was requested from the X550 is not ready
yet, or that the adequate write command was not given. The BMC should retry the read transaction or
send the write transaction.
It is BMC responsibility to follow the procedure previously defined. When the BMC sends a Block Read
command (as previously described) that is not preceded by a Block Write command with bytecount=1,
the X550 sets the parameter number in the read block transaction to be 0xFF.

       Parameter                   #                                          Parameter Data

Filters Enable                    0x01    None.

MNGONLY Configuration             0x0F    None.

Flex Filter Enable Mask           0x10    None.
and Length

Flex Filter Data                  0x11    Data 2 — Group of Flex Filter’s Bytes:
                                           0x0 = bytes 0-29
                                           0x1 = bytes 30-59
                                           0x2 = bytes 60-89
                                           0x3 = bytes 90-119
                                           0x4 = bytes 120-127

Decision Filters                  0x61    This command is obsolete. Use 0x68 instead.

VLAN Filters                      0x62    One byte to define the accessed VLAN tag filter (MAVTV)
                                          Data 2 — VLAN Filter number

333369-009                                                                                                    997
                                         Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                    System Manageability

       Parameter            #                                           Parameter Data

Flex Ports Filters         0x63    One byte to define the accessed manageability flex port filter (MFUTP).
                                   Data 2 — Flex Port Filter number

IPv4 Filter                0x64    One byte to define the accessed IPv4 address filter (MIPAF4)
                                   Data 2 — IPv4 address filter number

IPv6 Filters               0x65    One byte to define the accessed IPv6 address filter (MIPAF6)
                                   Data 2 — Pv6 address filter number

MAC Filters                0x66    One byte to define the accessed MAC Address filters pair (MMAL, MMAH)
                                   Data 2 — MAC Address filters pair number (0-3)

EtherType Filters          0x67    1 byte to define EtherType filters (METF)
                                   Data 2 — METF filter index (valid values are 0 - 3)

Extended Decision Filter   0x68    1 byte to define the extended decisions filters (MDEF_EXT & MDEF)
                                   Data 2 — MDEF filter index (valid values are 0 - 5)

Wrong parameter request    0xFE    Returned by the X550 only. This parameter is returned on read transaction, if in the
                                   previous read command the BMC sets a parameter that is not supported by the X550.

The X550 is not ready      0xFF    Returned by the X550 only, on read parameters command when the data that should have
                                   been read is not ready. This parameter has no data.
                                   This value is also returned if the byte count is illegal or if the read command is not
                                   preceded by a write command.

998                                                                                                             333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.5.11.2.6              Get Controller Information Command

The BMC uses this command to get the controller identification. Each parameter is returned using a
different opcode
To read the controller information, the BMC should execute two SMBus transactions. The first
transaction is a block write that sets the parameter that the BMC wants to read. The second transaction
is block read that read the parameter.
Block write transaction:

          Function              Command       Byte Count      Data 1 (Opcode)

Get Controller Information       0xD5              1         Parameter number

Following the block write the BMC should issue a block read that reads the parameter that was set in
the Block Write command:

          Function              Command

Get Controller Information       0xD5

Data returned from the X550:

     Function         Command         Byte Count         Data 2 (Opcode)                 Data 3 -n

Get Controller                                                                    See Table 11-21 for the
                         0xD5       Per Table 11-21       Per Table 11-21
Information                                                                        data for each opcode

Table 11-21. Get Controller Information Data
              Byte
 Opcode                                 Description                                                    Notes
             Count

  0x00           5    Data 4:3: Generic device ID.                          This is the hardware default value, not any value
                      Data 5: Silicon Revision (RevID)                      programmed via NVM.

  0x0B           4    Data 4:3 NVM Image version

  0x0C           6    Data 6:3: Firmware ROM Internal version

  0x0D           6    Data 6:3: Firmware Flash Internal version

  0x0E           4    Data 4:3: PXE firmware version                        MajorVersion.MinorVersion.Build.SubBuild

  0x0F           4    Data 4:3: iSCSI firmware version

  0x10           4    Data 4:3: uEFI firmware version

  0x16           4    Data 4:3: FCoE Boot firmware version

  0x17           6    Data 6:3: Firmware Mini Loader Internal version

  0xFE           2    Wrong parameter request                               Returned by the X550 only. This parameter is returned
                                                                            on read transaction, if in the previous read command the
                                                                            BMC sets a parameter that is not supported by the X550.

  0xFF           2    The X550 is not ready                                 Returned by the X550 only, on read parameters
                                                                            command when the data that should have been read is
                                                                            not ready. This parameter has no data. The BMC should
                                                                            retry the read transaction.
                                                                            This value is also returned if the byte count is illegal or if
                                                                            the read command is not preceded by a write command.
                                                                            This value is returned also if opcode 0x00 is received
                                                                            while device is in Dr state.

333369-009                                                                                                                             999
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

11.5.11.2.7              Get Common Filters Command

The BMC uses this command to get the common filters setting. This data can be configured when using
Set Common Filters command. The first transaction is a block write that alerts that the BMC wants to
read the filters configuration. The second transaction is block read that read the configuration.
Block write transaction:

       Function          Command     Byte count                   Data

Get Common Filters         0xD3                1                  0x00

Following the block write the BMC should issue a block read that reads the filter settings:

       Function           Command

Get Common filters          0xD3

Data returned from the X550:
IPv4 Format:

                                                                                 Data
                             Byte
  Function    Command
                            Count
                                       1               2:4               5:10      11          12           13         14:17

Get Common                                           Receive
                                                                      MAC       BMC Alert   Interface   Alert Value     IPv4
Filters           0xD3       18        0           Control (See
                                                                     Address     Address    Data Byte      Byte        Address
                                                   Table 11-13)

IPv6 Format:

                                                                                 Data
                             Byte
  Function    Command
                            Count
                                       1               2:4               5:10      11          12           13         14:29

Get Common                                           Receive
                                                                      MAC       BMC Alert   Interface   Alert Value     IPv6
Filters           0xD3       30        0           Control (see
                                                                     Address     Address    Data Byte      Byte        Address
                                                   Table 11-13)

If case of error the following answers may be returned:

       Function          Command    Byte Count               Data 1

Get Common Filters        0xD3             1                  0xFF

This response is by the X550, on read common filter command when the data that should have been
read is not ready. This parameter has no data. The BMC should retry the read transaction.
This value is also returned if the byte count is illegal, if the read command is not preceded by a write
command, or if the filters were not previously configured with a Set Common Filters command
(Section 11.5.11.1.7).

1000                                                                                                                  333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.5.11.2.8                Read Receive Enable Configuration

The BMC uses this command to read the receive configuration data. This data can be configured when
using Receive Enable command or through the NVM.
Read Receive Enable Configuration command format (SMBus Read Block) is as follows:

      Function              Command

Read Receive Enable             0xDA

Data returned from the X550:

                                                                                  Data
                  Byte
  Function
                 Count        1
                                              2      3          …       8            9      …     12         13          14         15
                           (Opcode)

Read Receive                            Receive     MAC                MAC                                  BMC                    Alert

    15 IP Addr       IP Addr                I/F Data

Enable                          0xDA    Control     Addr         …     Addr                 …              SMBus                   Value
                 (0x0F)                                                             MSB           LSB                    Byte
                                         Byte       MSB                LSB                                  Addr                   Byte

The detailed description of each field is specified in the receive enable command description in
Section 11.5.11.1.3.

11.5.11.2.9                Get Thermal Sensor Capabilities Command

The BMC can use this function to read the thermal sensor capabilities. It uses a write command to set
the needed index and then a read block command to read the data.
The write command is:

              Function                 Command      Byte Count          Sub Opcode

Get Thermal Capabilities Request         0xCB               1                 0x0

The read command is:

              Function                 Command

Get Thermal Capabilities Request         0xDB

The data returned from the X550 is:

                                                    Data 2                                                 Data 5:6
                           Byte      Data 1                           Data 3           Data 4                                   Data 7
     Function                                        (Sub                                                 (Number of
                          Count     (Opcode)                         (Version)       (Unit Types)                             (Accuracy)
                                                   Opcode)                                                Thresholds)

Get Thermal Sensor
                           26          0xDB          0x0                1           See Table 11-40        See below
Capabilities

                                                                 Data 13:16          Data 17:20        Data 21:24
                                                                                                                           Data 25:26
   Data 8        Data 9     Data 10    Data 11    Data 12        (Valid High         (Valid Low          (Valid
                                                                                                                           (Tjunction
 (Hysteresis)     (M)         (B)       (K1)       (K2)            Going               Going           Immediate
                                                                                                                              Max)
                                                                  Actions)            Actions)          Actions)

  See below                       See below                     See Table 11-39     See Table 11-39   See Table 11-39         See below

333369-009                                                                                                                            1001
                                        Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

 • Version should always be 1.
 • Unit Types describes the unit types measured according to the encoding in Table 11-40.
 • Accuracy describes the accuracy of the reported measurements as follows:
       — 7:4: Max deviation of actual value above measurement in “unit types”.
       — 3:0: Max deviation of actual value below measurement in “unit types”.
 • Max hysteresis — Defines the max hysteresis value allowed in the implementation. A value of zero
   means hysteresis is not supported.
 • Number of thresholds describes the number of up and down thresholds as follows:
       — 15:12: Reserved
       — 11:8: Max Number of mixed thresholds.
       — 7:4: Max number of up thresholds.
       — 3:0: Max number of down thresholds.
 • Valid Actions “High Going” thresholds — Describes the actions that can be activated by the device
   as described in Table 11-39 when a high going threshold is crossed or the upper hysteresis of a
   “High Going” Threshold is crossed.
 • Valid Actions “Low going” thresholds — Describes the actions that can be activated by the device as
   described in Table 11-39 when a low going threshold is crossed or the lower hysteresis of a “Low
   Going” Threshold is crossed.
 • Valid Actions “Immediate” — Describes the actions that can be activated by the device as described
   in Table 11-39 using a “Perform Thermal Sensor Action” command.
 • M, B, K1, K2 — Parameters used to translate the raw data read to a meaningful value according to
   the following formula:
          Y = (MX + (B * 10K1)) *10K2
       where X is the measured value, and Y is the value presented to the user.
       Note:    This formula is compliant with the definition of section 36.3 “Sensor Reading Conversion
                Formula” in IPMI 2.0
 • Tjunction Max - The maximal junction temperature supported (105 °C)

1002                                                                                                 333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.5.11.2.10             Get Thermal Sensor Configuration Command

The BMC can use this function to read the thermal sensor configuration for a given threshold. It uses a
write command to set the needed index and then a read block command to read the data.
The write command is:

              Function                Command        Byte Count      Sub Opcode          Data 1

Get Thermal Configuration Request          0xCB             2              0x1            Index

The read command is:

              Function                Command

Get Thermal Configuration Request          0xDB

The data returned from the X550 is:

                                                   Data 2
                       Byte     Data 1                           Data 3            Data 4:5               Data 6:9
     Function                                       (Sub
                      Count    (Opcode)                         (Index)          (Threshold)       (Action “Going High”)
                                                  Opcode)

Get Thermal Sensor                                                           The programmed       The programmed actions as
                         15         0xDB            0x1           Index
Configuration                                                                    threshold         described in Table 11-39

         Data 10:13                   Data 14                 Data 15
    (Action “Going Low”)             (Direction)            (Hysteresis)

   The programmed actions as
                                      See below              See below
    described in Table 11-39

The threshold and the Hysteresis are measured in “unit types”.
Note:        If the Max hysteresis reported in the Thermal Sensor capabilities is zero, the Hysteresis value
             is ignored.
The Actions Going High field describes the actions to activate upon crossing of the threshold for “Going
High” thresholds or when crossing the hysteresis for “Going Low” thresholds according to Table 11-39.
The Actions Going Low field describes the actions to activate upon crossing of the threshold for “Going
Low” thresholds or when crossing the hysteresis for “Going High” thresholds according to Table 11-39.
Direction is encoded as follows:
    0 = High Going
    1 = Low Going
If the opcode is 0xFF, it means that the data that was requested from the X550 is not ready yet, or that
the adequate write command was not given. The BMC should retry the read transaction or send the
write transaction.

333369-009                                                                                                                 1003
                                     Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                         System Manageability

11.5.11.2.11             Get Thermal Sensor Status Command

The BMC can use this function to read the thermal sensor status. It uses a write command to set the
needed index and then a read block command to read the data.
The write command is:

              Function                Command        Byte Count       Sub Opcode

Get Thermal Sensor Status Request          0xCB             1             0x2

The read command is:

              Function                Command

Get Thermal Sensor Status Request          0xDB

The data returned from the X550 is:

                                                   Data 2                                                       Data 9:10
                      Byte      Data 1                              Data 3:4              Data 5:8
       Function                                     (Sub                                                     (Threshold Cross
                     Count     (Opcode)                         (Measured Value)       (Active Actions)
                                                  Opcode)                                                         Event)

Get Thermal Sensor                                                                    The currently active
                                                                The value measured
Status                   10         0xDB            0x2                               actions as described      See below
                                                                  in “unit types”
                                                                                         in Table 11-39

“Threshold cross events” is a bitmap that describes which events were crossed since the last read of the
status or since the activation of the thermal sensor (the latest of the two). Bit ‘n’ in the bitmap
represent threshold index ‘n’ as configured in the Set Thermal Sensor Configuration command
(Section 11.5.11.1.9)
If the opcode is 0xFF, it means that the data that was requested from the X550 is not ready yet, or that
the adequate write command was not given. The BMC should retry the read transaction or send the
write transaction.

1004                                                                                                                333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

### 11.5.12 Example Configuration Steps

This section provides sample configuration settings for common filtering configurations. Three examples
are presented. The examples are in pseudo code format, with the name of the SMBus command
followed by the parameters for that command and an explanation.

#### 11.5.12.1 Example 1 - Shared MAC, RMCP Only Ports

This example is the most basic configuration. The MAC Address filtering is shared with the host
operating system and only traffic directed the RMCP ports (26Fh & 298h) is filtered. For this example,
the BMC must issue gratuitous ARPs because no filter is enabled to pass ARP requests to the BMC.

11.5.12.1.1            Example 1 Pseudo Code

Step 1: Disable existing filtering
  Receive Enable[00]

    Utilizing the simple form of the Receive Enable command, this prevents any packets from reaching
    the BMC by disabling filtering:
    Receive Enable Control 00h:
      • Bit 0 [0] – Disable Receiving of packets
Step 2: Configure MDEF[0]
  Update Manageability Filter Parameters [68, 0, C0000000, 00000000]

    Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
    (parameter 68h). This updates MDEF[0], as indicated by the 2nd parameter (0).
    MDEF[0] value of C0000000h:
      • Bit 30 [1] – port 298h
      • Bit 31 [1] – port 26Fh
    MDEF_EXT[0] value of 0000000h:
Step 3: Configure MNGONLY
  Update Manageability Filter Parameters [F, 0, 00000001]

    Use the Update Manageability Filter Parameters command to update Manageability Only
    (MNGONLY) (parameter 0xF) so that port 298h and 26Fh would not be sent to the host.
      • Bit [0] - MDEF[0] is exclusive to the BMC.
Step 4: - Enable Filtering
  Receive Enable [05]

    Using the simple form of the Receive Enable command:
    Receive Enable Control 05h:
      • Bit 0 [1] – Enable Receiving of packets
      • Bit 2 [1] – Enable status reporting (such as link lost)
      • Bit 5:4 [00] – Notification method = SMB Alert

333369-009                                                                                         1005
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                         System Manageability

       • Bit 7 [0] – Use shared MAC
The resulting MDEF filters are as follows:

Table 11-22. Example 1 MDEF Results
                                                         Manageability Decision Filter (MDEF)

                    Filter                   0      1        2       3         4       5        6        7

L2 Unicast Address[3:0]           AND

Broadcast                         AND

Manageability VLAN[7:0]           AND

IPv6 Address[3:0]                 AND

IPv4 Address[3:0]                 AND

L2 Unicast Address[3:0]           OR

Broadcast                         OR

Multicast                         AND

ARP Request                       OR

ARP Response                      OR

Neighbor Discovery                OR

Port 0x298                        OR         X

Port 0x26F                        OR         X

Flex Port 7:0                     OR

Flex TCO                          OR

1006                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.5.12.2 Example 2 - Dedicated MAC, Auto ARP Response and

                      RMCP Port Filtering
This example shows a common configuration; the BMC has a dedicated MAC and IP Address. Automatic
ARP responses are enabled as well as RMCP port filtering. By enabling Automatic ARP responses the
BMC is not required to send the gratuitous ARPs as it did in Example 1.
For demonstration purposes, the dedicated MAC Address is calculated by reading the System MAC
Address and adding 1 do it, assume the System MAC is AABBCCDC. The IP Address for this example is
1.2.3.4. Additionally, the XSUM filtering is enabled.
Note that not all Intel Ethernet Controllers support automatic ARP responses, refer to product-specific
documentation.

11.5.12.2.1            Example 2 - Pseudo Code

Step 1: Disable existing filtering
  Receive Enable[00]

    Utilizing the simple form of the Receive Enable command, this prevents any packets from reaching
    the BMC by disabling filtering:
    Receive Enable Control 00h:
      • Bit 0 [0] – Disable Receiving of packets
Step 2: Read System MAC Address
  Get System MAC Address []

    Reads the System MAC Address. Assume returned AABBCCDC for this example.
Step 3: Configure XSUM Filter
  Update Manageability Filter Parameters [01, 00800000]

    Use the Update Manageability Filter Parameters command to update Filters Enable settings
    (parameter 1). This set the Manageability Control (MANC) Register.
    MANC Register 00800000h:
      • Bit 23 [1] - XSUM Filter enable
    Note that some of the following configuration steps manipulate the MANC register indirectly, this
    command sets all bits except XSUM to 0. It is important to either do this step before the others, or
    to read the value of the MANC and then write it back with only bit 32 changed. Also note that the
    XSUM enable bit may differ between Ethernet Controllers, refer to product specific documentation.
Step 4: Configure MDEF[0]
  Update Manageability Filter Parameters [68, 0, C0000000, 00000000]

    Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
    (parameter 68h). This updates MDEF[0], as indicated by the 2nd parameter (0).
    MDEF value of 00000C00h:
      • Bit 30 [1] – port 298h
      • Bit 31 [1] – port 26Fh
    MDEF_EXT[0] value of 0000000h:

333369-009                                                                                          1007
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                            System Manageability

Step 5: Configure MDEF[1]
  Update Manageability Filter Parameters [68, 1, 10000000, 00000000]

       Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
       (parameter 61h). This updates MDEF[1], as indicated by the 2nd parameter (1).
       MDEF value of 10000000:
        • Bit 28 [1] – ARP Requests
       MDEF_EXT[1] value of 0000000h:
       When Enabling Automatic ARP responses, the ARP requests still go into the manageability filtering
       system and as such need to be designated as also needing to be sent to the host. For this reason a
       separate MDEF is created with only ARP request filtering enabled.
       Refer to the next step for more details.
Step 6: Configure Manageability only
  Update Manageability Filter Parameters [F, 0, 00000001]

       Use the Update Manageability Filter Parameters command to update Manageability Only
       (MNGONLY) (parameter 0xF) so that port 298h and 26Fh would not be sent to the host.
        • Bit [0] - MDEF[0] is exclusive to the BMC.
       This allows ARP requests to be passed to both manageability and to the host. Specified separate
       MDEF filter for ARP requests. If ARP requests had been added to MDEF[0] and then MDEF[0]
       specified in Management Only configuration, not only would RMCP traffic (ports 26Fh and 298h) be
       sent only to the BMC, ARP requests would have also been sent to the BMC only.
Step 7: Enable Filtering
  Receive Enable [8D, AABBCCDD, 01020304, 00, 00, 00]

       Using the advanced version Receive Enable command, the first parameter:
       Receive Enable Control 8Dh:
        • Bit 0 [1] – Enable Receiving of packets
        • Bit 2 [1] – Enable status reporting (such as link lost)
        • Bit 3 [1] – Enable Automatic ARP Responses
        • Bit 5:4 [00] – Notification method = SMB Alert
        • Bit 7 [1] - Use dedicated MAC
       Second parameter is the MAC Address (AABBCCDD).
       Third Parameter is the IP Address(01020304).
The last three parameters are zero when the notification method is SMB Alert.
The resulting MDEF filters are as follows:

1008                                                                                                  333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-23. Example 2 MDEF Results
                                                           Manageability Decision Filter (MDEF)

                    Filter                    0       1        2       3         4       5        6   7

L2 Unicast Address[3:0]              AND

Broadcast                            AND

Manageability VLAN[7:0]              AND

IPv6 Address[3:0]                    AND

IPv4 Address[3:0]                    AND

L2 Unicast Address[3:0]              OR

Broadcast                            OR

Multicast                            AND

ARP Request                          OR               X

ARP Response                         OR

Neighbor Discovery                   OR

Port 0x298                           OR       X

Port 0x26F                           OR       X

Flex Port 7:0                        OR

Flex TCO                             OR

333369-009                                                                                            1009
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                            System Manageability

#### 11.5.12.3 Example 3 - Dedicated MAC & IP Address

This example provided the BMC with a dedicated MAC and IP Address and allows it to receive ARP
requests. The BMC is then responsible for responding to ARP requests.
For demonstration purposes, the dedicated MAC Address is calculated by reading the System MAC
Address and adding 1 do it, assume the System MAC is AABBCCDC. The IP Address for this example is
1.2.3.4. For this example, the Receive Enable command is used to configure the MAC Address filter.
For the BMC to be able to receive ARP Requests, it needs to specify a filter for this. That filter must be
included in the Manageability To Host filtering so that the host OS may also receive ARP Requests.

11.5.12.3.1             Example 3 - Pseudo Code

Step 1: Disable existing filtering
  Receive Enable[00]

       Utilizing the simple form of the Receive Enable command, this prevents any packets from reaching
       the BMC by disabling filtering:
       Receive Enable Control 00h:
        • Bit 0 [0] – Disable Receiving of packets
Step 2: Read System MAC Address
  Get System MAC Address []

       Reads the System MAC Address. Assume returned AABBCCDC for this example.
Step 3: Configure IP Address Filter
  Update Manageability Filter Parameters [64, 00, 01020304]

       Use the Update Manageability Filter Parameters to configure an IPv4 filter.
       The 1st parameter (64h) specifies that we are configuring an IPv4 filter.
       The 2nd parameter (00h) indicates which IPv4 filter is being configured, in this case filter 0.
       The 3rd parameter is the IP Address – 1.2.3.4.
Step 4: Configure MAC Address Filter
  Update Manageability Filter Parameters [66, 00, AABBCCDD]

       Use the Update Manageability Filter Parameters to configure a MAC Address filter.
       The 1st parameter (66h) specifies that we are configuring a MAC Address filter.
       The 2nd parameter (00h) indicates which MAC Address filter is being configured, in this case filter
       0.
       The 3rd parameter is the MAC Address - AABBCCDD
Step 5: Configure MDEF[0] for IP and MAC Filtering
  Update Manageability Filter Parameters [68, 0, 00002001, 00000000]

       Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
       (parameter 68h). This updates MDEF[0], as indicated by the 2nd parameter (0).

1010                                                                                                  333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

    MDEF value of 00002001:
      • Bit 0 [1] – MAC[0] Address Filtering
      • Bit 13 [1] – IP[0] Address Filtering
    MDEF_EXT[0] value of 0000000h:
Step 6: Configure MDEF[1]
  Update Manageability Filter Parameters [68, 1, 10000000]

    Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
    (parameter 68h). This updates MDEF[1], as indicated by the 2nd parameter (1).
    MDEF value of 10000000:
      • Bit 28 [1] – ARP Requests
    MDEF_EXT[1] value of 0000000h:
Step 7: Configure the Management to Host Filter
  Update Manageability Filter Parameters [F, 0, 00000001]

    Use the Update Manageability Filter Parameters command to update Manageability Only
    (MNGONLY) (parameter 0xF) so that the dedicated MAC/IP traffic would not be sent to the Host.
    Note that given the host does not program this address in it’s L2 filtering, this step is not a must,
    unless the host chooses to work in promiscuous mode.
      • Bit [0] - MDEF[0] is exclusive to the BMC.
Step 8: Enable Filtering
  Receive Enable [05]

    Using the simple form of the Receive Enable command:
    Receive Enable Control 05h:
      • Bit 0 [1] – Enable Receiving of packets
      • Bit 2 [1] – Enable status reporting (such as link lost)
      • Bit 5:4 [00] – Notification method = SMB Alert
The resulting MDEF filters are as follows:

333369-009                                                                                            1011
                                 Did this document help answer your questions?

                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                       System Manageability

Table 11-24. Example 3 MDEF Results
                                                       Manageability Decision Filter (MDEF)

                    Filter                0       1        2       3         4       5        6        7

L2 Unicast Address[3:0]         AND     0001

Broadcast                       AND

Manageability VLAN[7:0]         AND

IPv6 Address[3:0]               AND

IPv4 Address[3:0]               AND     0001

L2 Unicast Address[3:0]         OR

Broadcast                       OR

Multicast                       AND

ARP Request                     OR                X

ARP Response                    OR

Neighbor Discovery              OR

Port 0x298                      OR

Port 0x26F                      OR

Flex Port 7:0                   OR

Flex TCO                        OR

1012                                                                                              333369-009
                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.5.12.4 Example 4 - Dedicated MAC and VLAN Tag

This example shows an alternate configuration; the BMC has a dedicated MAC and IP Address, along
with a VLAN tag of 32h is required for traffic to be sent to the BMC. This means that all traffic with VLAN
a matching tag is sent to the BMC.
For demonstration purposes, the dedicated MAC Address is calculated by reading the System MAC
Address and adding 1 do it, assume the System MAC is AABBCCDC. The IP Address for this example is
1.2.3.4 and the VLAN tag is 0032h.
Additionally, the XSUM filtering is enabled.

11.5.12.4.1            Example 4 - Pseudo Code

Step 1: Disable existing filtering
  Receive Enable[00]

    Utilizing the simple form of the Receive Enable command, this prevents any packets from reaching
    the BMC by disabling filtering:
    Receive Enable Control 00h:
      • Bit 0 [0] – Disable Receiving of packets
Step 2: - Read System MAC Address
  Get System MAC Address []

    Reads the System MAC Address. Assume returned AABBCCDC for this example.
Step 3: Configure XSUM Filter
  Update Manageability Filter Parameters [01, 00800000]

    Use the Update Manageability Filter Parameters command to update Filters Enable settings
    (parameter 1). This set the Manageability Control (MANC) Register.
    MANC Register 00800000h:
      • Bit 23 [1] – XSUM Filter enable
    Note that some of the following configuration steps manipulate the MANC register indirectly, this
    command sets all bits except XSUM to 0. It is important to either do this step before the others, or
    to read the value of the MANC and then write it back with only bit 32 changed. Also note that the
    XSUM enable bit may differ between Ethernet Controllers, refer to product specific documentation.
Step 4: Configure VLAN 0 Filter
  Update Manageability Filter Parameters [62, 0, 0032]

    Use the Update Manageability Filter Parameters command to configure VLAN filters. Parameter 62h
    indicates update to VLAN Filter, the 2nd parameter indicates which VLAN filter (0 in this case), the
    last parameter is the VLAN ID (0032h).
Step 5: Configure MDEF[0]
  Update Manageability Filter Parameters [68, 0, 00000020, 00000000]

    Use the Update Manageability Filter Parameters command to update Decision Filters (MDEF)
    (parameter 68h). This updates MDEF[0], as indicated by the 2nd parameter (0).

333369-009                                                                                             1013
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

       MDEF value of 00000020:
        • Bit 5 [1] – VLAN[0] AND
       MDEF_EXT[0] value of 0000000h:
Step 6: Enable Filtering
  Receive Enable [85, AABBCCDD, 01020304, 00, 00, 00]

       Using the advanced version Receive Enable command, the first parameter:
       Receive Enable Control 85h:
 • Bit 0 [1] – Enable Receiving of packets
 • Bit 2 [1] – Enable status reporting (such as link lost)
 • Bit 5:4 [00] – Notification method = SMB Alert
 • Bit 7 [1] – Use Dedicated MAC
       Second parameter is the MAC Address: AABBCCDD.
       Third Parameter is the IP Address: 01020304.
       The last three parameters are zero when the notification method is SMBus Alert.
The resulting MDEF filters are as follows:

Table 11-25. Example 4 MDEF Results
                                                           Manageability Decision Filter (MDEF)

                    Filter                    0       1        2       3         4       5        6        7

L2 Unicast Address[3:0]              AND                                                                 0001

Broadcast                            AND

Manageability VLAN[7:0]              AND      X

IPv6 Address[3:0]                    AND

IPv4 Address[3:0]                    AND

L2 Unicast Address[3:0]              OR

Broadcast                            OR

Multicast                            AND

ARP Request                          OR

ARP Response                         OR

Neighbor Discovery                   OR

Port 0x298                           OR

Port 0x26F                           OR

Flex Port 7:0                        OR

Flex TCO                             OR

1014                                                                                                  333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

### 11.5.13 SMBus Troubleshooting

This section outlines the most common issues found while working with pass-through using the SMBus
sideband interface.

#### 11.5.13.1 TCO Alert Line Stays Asserted After a Power Cycle

After the X550 resets, all its ports indicates a status change. If the BMC only reads status from one port
(slave address), the other one continues to assert the TCO alert line.
Ideally, the BMC should use the ARA transaction (see Section 11.5.10) to determine which slave
asserted the TCO alert. Many customers only wish to use one port for manageability thus using ARA
might not be optimal.
An alternate to using ARA is to configure part of the ports to not report status and to set its SMBus
timeout period. In this case, the SMBus timeout period determines how long a port asserts the TCO
alert line awaiting a status read from a BMC; by default this value is zero (indicates an infinite timeout).
The SMBus configuration section of the NVM has a SMBus Notification Timeout (ms) field that can be set
to a recommended value of 0xFF (for this issue). Note that this timeout value is for all slave addresses.
Along with setting the SMBus Notification Timeout to 0xFF, it is recommended that the other ports be
configured in the NVM to disable status alerting. This is accomplished by having the Enable Status
Reporting bit set to 0b for the desired ports in the LAN configuration section of the NVM.
The third solution for this issue is to have the BMC hard-code the slave addresses to always read from
all ports. As with the previous solution, it is recommend that the other ports have status reporting
disabled.

#### 11.5.13.2 When SMBus Commands are Always NACK'd

There are several reasons why all commands sent to the X550 from a BMC could be NACK'd. The
following are most common:
 • Invalid NVM Image — The image itself might be invalid or it could be a valid image and is not a
   pass-through image, as such SMBus connectivity is disabled.
 • The BMC is not using the correct SMBus address — Many BMC vendors hard-code the SMBus
   address(es) into their firmware. If the incorrect values are hard-coded, the X550 does not respond.
     — The SMBus address(es) can be dynamically set using the SMBus ARP mechanism.
 • The BMC is using the incorrect SMBus interface — The NVM might be configured to use one physical
   SMBus port; however, the BMC is physically connected to a different one.
 • Bus Interference — The bus connecting the BMC and the X550 might be unstable.

#### 11.5.13.3 SMBus Clock Speed is 16.6666 KHz

This can happen when the SMBus connecting the BMC and the X550 is also tied into another device
(such as an ICH) that has a maximum clock speed of 16.6666 KHz. The solution is to not connect the
SMBus between the X550 and the BMC to this device.

333369-009                                                                                             1015
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                         System Manageability

#### 11.5.13.4 A Network Based Host Application is Not Receiving Any

                    Network Packets
Reports have been received about an application not receiving any network packets. The application in
question was NFS under Linux. The problem was that the application was using the RMPC/RMCP+ IANA
reserved port 0x26F (623) and the system was also configured for a shared MAC and IP Address with
the OS and BMC.
The management control to host configuration, in this situation, was setup not to send RMCP traffic to
the OS (this is typically the correct configuration). This means that no traffic send to port 623 was being
routed.
The solution in this case is to configure the problematic application NOT to use the reserved port 0x26F.

#### 11.5.13.5 Unable to Transmit Packets from the BMC

If the BMC has been transmitting and receiving data without issue for a period of time, and then begins
to receive NACKs from the X550 when it attempts to write a packet, the problem is most likely due to
the fact that the buffers internal to the X550 are full of data that has been received from the network
but has yet to be read by the BMC.
Being an embedded device, the X550 has limited buffers that are shared for receiving and transmitting
data. If a BMC does not keep the incoming data read, the X550 can be filled up This prevents the BMC
form transmitting more data, resulting in NACKs.
If this situation occurs, the recommended solution is to have the BMC issue a Receive Enable command
to disable more incoming data, read all the data from the X550, and then use the Receive Enable
command to enable incoming data.

#### 11.5.13.6 SMBus Fragment Size

The SMBus specification indicates a maximum SMBus transaction size of 32 bytes. Most of the data
passed between the X550 and the BMC over the SMBus is RMCP/RMCP+ traffic, which by its very nature
(UDP traffic) is significantly larger than 32 bytes in length. Multiple SMBus transactions may therefore
be required to move data from the X550 to the BMC or to send a data from the BMC to the X550.
Recognizing this bottleneck, the X550 handles up to 240 bytes of data in a single transaction. This is a
configurable setting in the NVM. The default value in the NVM images is 32, per the SMBus
specification. If performance is an issue, increase this size.
During initialization, firmware within the X550 allocates buffers based upon the SMBus fragment size
setting within the NVM. The X550 firmware has a finite amount of RAM for its use: the larger the SMBus
fragment size, the fewer buffers it can allocate. Because this is true, BMC implementations must take
care to send data over the SMBus efficiently.
For example, the X550 firmware has 3 KB of RAM it can use for buffering SMBus fragments. If the
SMBus fragment size is 32 bytes, the firmware could allocate 96 buffers of size 32 bytes each. As a
result, the BMC could then send a large packet of data (such as KVM) that is 800 bytes in size in 25
fragments of size 32 bytes apiece.
However, this might not be the most efficient way because the BMC must break the 800 bytes of data
into 25 fragments and send each one at a time.
If the SMBus fragment size is changed to 240 bytes, the X550 firmware can create 12 buffers of 240
bytes each to receive SMBus fragments. The BMC can now send that same 800 bytes of KVM data in
only four fragments, which is much more efficient.

1016                                                                                               333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

The problem of changing the SMBus fragment size in the NVM is if the BMC does not also reflect this
change. If a programmer changes the SMBus fragment size in the X550 to 240 bytes, and then wants
to send 800 bytes of KVM data, the BMC can still only send the data in 32 byte fragments. As a result,
firmware runs out of memory.
This is because firmware created the 12 buffers of 240 bytes each for fragments; however, the BMC is
only sending fragments of size 32 bytes. This results in a memory waste of 208 bytes per fragment.
Then when the BMC attempts to send more than 12 fragments in a single transaction, the X550 NACKs
the SMBus transaction due to not enough memory to store the KVM data.
In summary, if a programmer increases the size of the SMBus fragment size in the NVM (recommended
for efficiency purposes) take care to ensure that the BMC implementation reflects this change and uses
that fragment size to its fullest when sending SMBus fragments.

#### 11.5.13.7 Losing Link

Normal behavior for the Ethernet Controller when the system powers down or performs a reset is for
the link to temporarily go down and then back up again to re-negotiate the link speed. This behavior
can have adverse affects on manageability.
For example if there is an active FTP or Serial Over LAN session to the BMC, this connection may be
lost. To avoid this possible situation, the BMC can use the Management Control command detailed in
Section 11.5.11.1.5 to ensure the link stays active at all times.
This command is available when using the NC-SI sideband interface as well.
Care should be taken with this command. If the driver negotiates the maximum link speed, the link
speed remains the same when the system powers down or resets. This may have undesirable power
consumption consequences. Currently, when using NC-SI, the BMC can re-negotiate the link speed.
That functionality is not available when using the SMBus interface.

#### 11.5.13.8 Enable Checksum Filtering

If Checksum filtering is enabled, the BMC does not need to perform the task of checking this checksum
for incoming packets. Only packets that have a valid Checksum is passed to the BMC. All others are
silently discarded.
This is a way to offload some work from the BMC.

#### 11.5.13.9 Still Having Problems?

If problems still exist, contact your field representative. Be prepared to provide the following:
 • A SMBus trace if possible
 • A dump of the NVM image. This should be taken from the actual X550, rather than the NVM image
   provided by Intel. Parts of the NVM image are changed after writing (such as the physical NVM
   size).

333369-009                                                                                          1017
                                 Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                    System Manageability
