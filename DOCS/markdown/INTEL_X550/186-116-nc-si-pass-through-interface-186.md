## 11.6 NC-SI Pass-Through Interface

The Network Controller Sideband Interface (NC-SI) is a DMTF industry standard protocol for the
sideband interface. NC-SI uses a modified version of the industry standard RMII interface for the
physical layer as well as defining a new logical layer.
The NC-SI specification supported by the X550 can be found at:
       http://www.dmtf.org/sites/default/files/standards/documents/DSP0222_1.0.1.pdf

### 11.6.1 Overview

#### 11.6.1.1 Terminology

The terminology in this document is taken from the NC-SI specification.

Table 11-26. NC-SI Terminology
                 Term                                                     Definition

Frame Versus Packet            Frame is used in reference to Ethernet, whereas packet is used everywhere else.

External Network Interface     The interface of the network controller that provides connectivity to the external network
                               infrastructure (port).

Internal Host Interface        The interface of the network controller that provides connectivity to the host OS running on
                               the platform.

Management Controller (BMC)    An intelligent entity comprising of HW/FW/SW, that resides within a platform and is
                               responsible for some or all management functions associated with the platform (BMC, service
                               processor, etc.).

Network Controller (NC)        The component within a system that is responsible for providing connectivity to the external
                               Ethernet network world.

Remote Media                   The capability to allow remote media devices to appear as if they were attached locally to the
                               host.

Network Controller Sideband    The interface of the network controller that provides connectivity to a management controller.
Interface                      It can be shorten to sideband interface as appropriate in the context.

Interface                      This refers to the entire physical interface, such as both the transmit and receive interface
                               between the management controller and the network controller.

Integrated Controller          The term integrated controller refers to a network controller device that supports two or more
                               channels for NC-SI that share a common NC-SI physical interface. For example, a network
                               controller that has two or more physical network ports and a single NC-SI bus connection.

Multi-Drop                     Multi-drop commonly refers to the case where multiple physical communication devices share
                               an electrically common bus and a single device acts as the master of the bus and
                               communicates with multiple slave or target devices. In NC-SI, a management controller
                               serves the role as the master, and the network controllers are the target devices.

Point-to-Point                 Point-to-point commonly refers to the case where only two physical communication devices
                               are interconnected via a physical communication medium. The devices might be in a master/
                               slave relationship, or could be peers. In NC-SI, point-to-point operation refers to the situation
                               where only a single management controller and single network controller package are used on
                               the bus in a master/slave relationship where the management controller is the master.

Channel                        The control logic and data paths supporting NC-SI pass-through operation on a single network
                               interface (port). A network controller that has multiple network interface ports can support an
                               equivalent number of NC-SI channels.

1018                                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-26. NC-SI Terminology [continued]
              Term                                                           Definition

Package                            One or more NC-SI channels in a network controller that share a common set of electrical
                                   buffers and common buffer control for the NC-SI bus. Typically, there is a single, logical NC-SI
                                   package for a single physical network controller package (chip or module). However, the
                                   specification allows a single physical chip or module to hold multiple NC-SI logical packages.

Control Traffic/Messages/Packets   Command, response and notification packets transmitted between BMC and the X550 for the
                                   purpose of managing NC-SI.

Pass-Through Traffic/Messages/     Non-control packets passed between the external network and the BMC through the X550.
Packets

Channel Arbitration                Refer to operations where more than one of the network controller channels can be enabled to
                                   transmit pass-through packets to the BMC at the same time, where arbitration of access to
                                   the RXD, CRS_DV, and RX_ER signal lines is accomplished either by software of hardware
                                   means.

Logically Enabled/Disabled NC      Refers to the state of the network controller wherein pass-through traffic is able/unable to
                                   flow through the sideband interface to and from the management controller, as a result of
                                   issuing Enable/Disable Channel command.

NC RX                              Defined as the direction of ingress traffic on the external network controller interface

NC TX                              Defined as the direction of egress traffic on the external network controller interface

NC-SI RX                           Defined as the direction of ingress traffic on the sideband enhanced NC-SI Interface with
                                   respect to the network controller.

NC-SI TX                           Defined as the direction of egress traffic on the sideband enhanced NC-SI Interface with
                                   respect to the network controller.

#### 11.6.1.2 System Topology

In NC-SI each physical endpoint (NC package) can have several logical slaves (NC channels).
NC-SI defines that one management controller and up to four network controller packages can be
connected to the same NC-SI link.
Figure 11-5 shows an example topology for a single BMC and a single NC package. In this example, the
NC package has two NC channels.

                                                  Management Controller
                                                         (MC)

                                                                  NC-SI Link

                                                        NC Package
                                                      Package ID = 0x0
                                              NC Channel           NC Channel

                                                Internal            Internal
                                             ChannelID=0x0       ChannelID=0x1

                                                  LAN0                LAN1

Figure 11-5. Single NC Package, Two NC Channels

333369-009                                                                                                                     1019
                                    Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                               System Manageability

Figure 11-6 shows an example topology for a single BMC and two NC packages. In this example, one
NC package has two NC channels and the other has only one NC channel. Scenarios in which the NC-SI
lines are shared by multiple NCs (Figure 11-6) mandate an arbitration mechanism. The arbitration
mechanism is described in Section 11.6.7.1.

                                                   Management Controller
                                                          (MC)

                                                                NC-SI Link

                                  NC Package                                 NC Package
                                Package ID = 0x0                           Package ID = 0x1
                          NC Channel       NC Channel                         NC Channel

                            Internal        Internal                           Internal
                         ChannelID=0x0   ChannelID=0x1                      ChannelID=0x0

                            LAN0              LAN1                               LAN

Figure 11-6. Two NC Packages (Left, with Two NC Channels and Right, with One NC Channel)

Note:      Channel numbers should match PCI function numbers. If more than one function is defined
           on a port, the function with the lowest value associated with this port is used (it is assumed
           that the first function numbers are assigned to different ports). The association of functions to
           ports is reflected in the PFGEN_PORTNUM registers.

#### 11.6.1.3 Data Transport

Since NC-SI is based upon the RMII transport layer, data is transferred in the form of Ethernet frames.
NC-SI defines two types of transmitted frames:
 • Control frames:
       — Configures and control the interface
       — Identified by a unique EtherType in their L2 header
 • Pass-through frames:
       — Actual LAN pass-through frames transferred from/to the BMC
       — Identified as not being a control frame
       — Attributed to a specific NC channel by their source MAC Address (as configured in the NC by the
         BMC)

1020                                                                                                     333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.1.3.1             Control Frames

NC-SI control frames are identified by a unique NC-SI EtherType (0x88F8).
Control frames are used in a single-threaded operation, meaning commands are generated only by the
BMC and can only be sent one at a time. Each command from the BMC is followed by a single response
from the NC (command-response flow), after which the BMC is allowed to send a new command.
The only exception to the command-response flow is the Asynchronous Event Notification (AEN). These
control frames are sent unsolicited from the NC to the BMC.
AEN functionality by the NC must be disabled by default, until activated by the BMC using the Enable
AEN commands.
To be considered a valid command, a control frame must:
 • Comply with the NC-SI header format.
 • Be targeted to a valid channel in the package via the Package ID and Channel ID fields. For
   example, to target a NC channel with package ID of 0x2 and internal channel ID of 0x5, the BMC
   must set the channel ID inside the control frame to 0x45. The channel ID is composed of three bits
   of package ID and five bits of internal channel ID.
 • Contain a correct payload checksum (if used).
 • Meet any other condition defined by NC-SI.
There are also commands (such as select package) targeted to the package as a whole. These
commands must use an internal channel ID of 0x1F.
For details, refer to the NC-SI specification.

11.6.1.3.2             NC-SI Frames Receive Flow

Figure 11-7 shows the flow for frames received on the NC from the BMC.

                                                                        NC-SI frame
                                                                      received from MC

                                                                       EtherType ==
                           Process as NC-SI Control Frame   Yes
                                                                     NC-SI EtherType?

                                                                             No

                                                                   Source MAC address ==
                             Send to LAN with matching
                                                            Yes   previously configured MAC
                              configured MAC address
                                                                           address?

                                                                             No

                                                                  Drop frame (belongs to a
                                                                     different Package)

Figure 11-7. NC-SI Frames Receive Flow for the NC

333369-009                                                                                        1021
                                    Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                           System Manageability

### 11.6.2 NC-SI Standard Support

#### 11.6.2.1 Supported Features

The X550 supports all the mandatory features of the NC-SI specification (rev 1.0.1). Table 11-27 lists
the supported commands.

Table 11-28 lists optional features supported.

Table 11-27. Supported NC-SI Commands
                                                                               Supported over MCTP          Supported over MCTP
 Command                                           Supported over RMII
                                                                                with Pass-Through           without Pass-Through

 Clear initial state                                         Yes                          Yes                          Yes

 Get Version ID                                              Yes                          Yes                          Yes

 Get Parameters                                              Yes                          Yes                          Yes

 Get Controller Packet Statistics                       Yes, partially               Yes, partially               Yes, partially

 Get Link Status                                             Yes                          Yes                          Yes

 Enable Channel                                              Yes                          Yes                          Yes

 Disable Channel                                             Yes                          Yes                          Yes

 Reset Channel                                               Yes                          Yes                          Yes

 Enable VLAN                                                Yes1’2                       Yes1                          No3

 Disable VLAN                                                Yes                          Yes                          No3

 Enable Broadcast Filter                                     Yes                          Yes                          No3

 Disable Broadcast Filter                                    Yes                          Yes                          No3

 Set MAC Address4                                            Yes                          Yes                          No3

 Get NC-SI Statistics                                   Yes, partially               Yes, partially               Yes, partially

 Set NC-SI Flow-Control                                      Yes                          No                           No3

 Set Link Command                                            Yes                          Yes                          Yes

 Enable Global multicast Filter                              Yes                          Yes                          No3

 Disable Global multicast Filter                             Yes                          Yes                          No3

 Get Capabilities                                            Yes                          Yes                          Yes

 Set VLAN Filters                                            Yes                          Yes                          No3

 AEN Enable                                                  Yes                          Yes                          Yes

 Get NC-SI Pass-Through Statistics                      Yes, partially               Yes, partially                    No3

 Select Package                                              Yes                          Yes                          Yes

 Deselect Package                                            Yes                          Yes                          Yes

 Enable Channel Network Tx5                                  Yes                          Yes                          No

 Disable Channel Network Tx                                  Yes                          Yes                          No
                  6
 OEM Command                                                 Yes                          Yes                          Yes

1. In cases that one of the LAN devices is assigned for the sole use of the manageability and its LAN PCI-E function is disabled, using
   the NC-SI Set Link command while advertising multiple speeds and enabling auto-negotiation, results in the lowest possible speed
   chosen. To enable link of higher a speed, the BMC should not advertise speeds that are below the desired link speed. When doing
   it, changing the power state of the LAN device has no effect and the link speed is not re-negotiated.
2. The X550 does not support filtering of User priority/DEI Bits of VLAN.

1022                                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

3. In MCTP without pass-through mode, only control commands are supported and not pass-through traffic - thus many of the regular
   NC-SI commands are not supported or are supported in a limited manner, only to allow control and status reporting for the device.
4. Set MAC Address command fails with a 0x002 (Parameter Is Invalid, Unsupported, or Out-of-Range) reason code if received on a
   Tx enabled port with a unicast MAC Address already configured on another Tx enabled port.
5. Enable Channel Network TX command fails with a 0x002 (Parameter Is Invalid, Unsupported, or Out-of-Range) reason code if
   received on a port configured with an unicast MAC address equal to the MAC address of another Tx enabled port.
6. See Section 11.6.3 for details.

Table 11-28. Optional NC-SI Features Support
                Feature                 Implement                                           Details

 AENs                                        Yes         The Driver state AEN may be emitted up to 1 minute after actual driver
                                                         change if the driver was taken down unexpectedly.
                                                         A “Re-configuration Required” AEN is sent before a firmware reset
                                                         initiated due to a firmware code update

 Get Controller Packet Statistics       Yes, partially   Supports the following counters1:
 command                                                  2-8, 13-162
                                                         The statistics are cleared between reads.

 Get NC-SI statistics                        Yes         Supports all counters

 Get NC-SI Pass-Through Statistics      Yes, partially   Support the following counters3:
                                                           14, 2, 65, 7

 VLAN Modes                             Yes, partially   Support only modes 1, 3.

 Buffering Capabilities                      Yes         8 Kb 6

 MAC Address Filters                         Yes         Supports 2 MAC Addresses per port.

 Channel Count                               Yes         Supports 4 channels.

 VLAN Filters                                Yes         Support 8 VLAN filters per port.
                                                         Filtering is ignoring the DEI bit and the 802.1P priority bits

 Broadcast Filters                           Yes         Support the following filters:
                                                          • ARP
                                                          • DHCP
                                                          • Net BIOS

 Multicast Filters                           Yes         Supports the following filters:
                                                          • IPv6 Neighbor Advertisement
                                                          • IPv6 Router Advertisement
                                                          • DHCPv6 relay and server multicast

 Hardware Arbitration                        Yes         Supports NC-SI hardware arbitration.

1. TCTL.EN should be set to 1b to activate Tx related counters and RCTL.RXEN, MANC.RCV_EN or GRC.APME should be set to enable
   RX related counters.
2. As described in the Get Controller Packet Statistics Counter Numbers table in NC-SI specification.
3. As described in the Get NC-SI Pass-through Statistics Counters table in NC-SI specification.
4. If OS2BMC traffic is enabled, packets sent both to the net and to the host are counted twice by this counter.
5. The Total Pass-through RX Packets Received On the LAN Interface counter includes also OS2BMC traffic.
6. For OS2BMC traffic, there may be drops after 4 KB.

333369-009                                                                                                                     1023
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                         System Manageability

#### 11.6.2.2 ALD Support

NC-SI PHY power down conditions:
In NC-SI mode, the device may dynamically change the PHY power mode according to the NC-SI
channel state assuming no other functionality requires the PHY to be active (host or wake-up).
The following algorithm is used to define if PHY activity is required:
 • At init time, if the manageability mode is NC-SI, PHY is required to be active only if the Enable All
   PHYs in D3 N bit in Common Firmware Parameters NVM word is set.
 • Once a channel is enabled via Enable Channel NC-SI command, The PHY is powered up.
 • If the channel is disabled via a Disable Channel command with ALD bit set, the PHY is disabled.
 • If the channel is disabled via a Reset Channel command, the PHY power state is set back to the init
   value as define by the Enable All PHYs in D3 N bit.
Note:     Before transitioning to D3 it is the responsibility of the driver to request the PHY to be active
          for wake-up activities using WUC register (setting WUC.PROXYE forces PHY to be active in
          D3).

#### 11.6.2.3 AEN Handling

Asynchronous events may occur when the device is not allowed to send them. The following rules
defines the behavior of the X550 in these cases:
1. While the device is disabled, for each type of AEN only the last event is kept
2. Outstanding AENs that occurred while package was deselected are transmitted when package is
   selected.
3. On a transition from Channel Disabled to Channel Enabled, all outstanding event are erased to
   prevent stale events notifications.

### 11.6.3 NC-SI Mode — Intel Specific Commands

In addition to regular NC-SI commands, the following Intel vendor specific commands are supported.
The purpose of these commands is to provide a means for the BMC to access some of the Intel-specific
features present in the X550.

#### 11.6.3.1 Overview

The following features are available via the NC-SI OEM specific commands:
 • Receive filters.
 • Packet Addition Decision Filters 0x0…0x4.
 • Packet Reduction Decision Filters 0x5…0x7.
 • MNGONLY register (controls the forwarding of manageability packets to the host).
 • Flex 128 filters.
 • Flex TCP/UDP port filters 0x0...0x2.

1024                                                                                               333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

 • IPv4/IPv6 filters.
 • Get System MAC Address — This command enables the BMC to retrieve the system MAC Address
   used by the NC. This MAC Address can be used for a shared MAC Address mode.
 • Keep PHY Link Up (Veto bit) Enable/Disable — This feature enables the BMC to block PHY reset,
   which might cause session loss.
 • TCO Reset — Enables the BMC to reset the X550.
 • Checksum offloading — Offloads IP/UDP/TCP checksum checking from the BMC.
 • OS2BMC control commands.
 • Firmware Version Commands.
These commands are designed to be compliant with their corresponding SMBus commands (if existing).
All of the commands are based on a single DMTF defined NC-SI command, known as OEM Command.
This command is as follows.

#### 11.6.3.2 OEM Command (0x50)

The OEM command can be used by the BMC to request the sideband interface to provide vendor-
specific information. The Vendor Enterprise Number (VEN) is the unique MIB/SNMP private enterprise
number assigned by IANA per organization. Vendors are free to define their own internal data
structures in the vendor data fields.

                                                              Bits

   Bytes              31:24                     23:16                       15:8                              7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                                        Manufacturer ID (Intel 0x157)

    20...      Intel Command Number                                     Optional Data

     ...                                                       ...

     ...                        Optional Data                                     Padding to 32 bits (0x00)

     ...                                                   Checksum

333369-009                                                                                                          1025
                                 Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                           System Manageability

11.6.3.2.1                   OEM Response (0xD0)

                                                                      Bits

   Bytes                 31:24                          23:16                          15:8                            7:0

   0...3

   4...7
                                                                 NC-SI Header
   8...11

  12...15

  16...19                          Response Code                                                 Reason Code

  20...23                                                 Manufacturer ID (Intel 0x157)

  24...27         Intel Command Number                                       Optional Return Data

       ...                                                             ...

       ...                       Optional Return Data                                      Padding to 32 bits (0x00)

       ...                                                         Checksum

Note:          Responses have no command-specific reason code, unless otherwise specified within the
               command.
Note:          The commands/responses described below includes only the part up to the Data. The padding
               and checksum are implied.

#### 11.6.3.3 OEM Commands Summary

Table 11-29. OEM Specific Command Response Reason Codes
             Response Code                                                   Reason Code

  Value           Description          Value                                           Description

   0x1        Command Failed           0x5081      Invalid Intel Command Number

                                       0x5082      Invalid Intel Command Parameter Number

                                       0x5085      Internal Network Controller Error

                                       0x5086      Invalid Vendor Enterprise Code

1026                                                                                                                         333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-30. OEM Commands Summary
    Intel                                                                          Supported in      Section
                 Parameter                        Command Name
  Command                                                                         MCTP without PT    Number

     0x00          0x00       Set IP Filters Control                                    No           11.6.3.5

     0x01          0x00       Get IP Filters Control                                    No           11.6.3.6

                   0x0F       Set Manageability Only                                                11.6.3.7.2

                   0x10       Set Flexible 128 Filter Mask and Length                               11.6.3.7.3

                   0x11       Set Flexible 128 Filter Data                                          11.6.3.7.4

                   0x63       Set Flex TCP/UDP Port Filters                                         11.6.3.7.5
     0x02                                                                               No
                   0x64       Set Flex IPv4 Address Filters                                         11.6.3.7.6

                   0x65       Set Flex IPv6 Address Filters                                         11.6.3.7.7

                   0x67       Set EtherType Filter                                                  11.6.3.7.8

                   0x68       Set Packet Addition Extended Filter                                   11.6.3.7.9

                   0x0F       Get Manageability Only                                                11.6.3.8.2

                   0x10       Get Flexible 128 Filter Mask and Length                               11.6.3.8.3

                   0x11       Get Flexible 128 Filter Data                                          11.6.3.8.4

                   0x63       Get Flex TCP/UDP Port Filters                                         11.6.3.8.5
     0x03                                                                               No
                   0x64       Get Flex IPv4 Address Filters                                         11.6.3.8.6

                   0x65       Get Flex IPv6 Address Filters                                         11.6.3.8.7

                   0x67       Get EtherType Filter                                                  11.6.3.8.8

                   0x68       Get Packet Addition Extended Filter                                   11.6.3.8.9

                   0x10       Set Extended Unicast Packet Reduction                                 11.6.3.9.1

     0x04          0x11       Set Extended Multicast Packet Reduction                   No          11.6.3.9.2

                   0x12       Set Extended Broadcast Packet Reduction                               11.6.3.9.4

                   0x10       Get Extended Unicast Packet Reduction                                 11.6.3.10.1

     0x05          0x11       Get Extended Multicast Packet Reduction                   No          11.6.3.10.2

                   0x12       Get Extended Broadcast Packet Reduction                               11.6.3.10.3

     0x06           N/A       Get System MAC Address                                    Yes         11.6.3.11

     0x20           N/A       Set Intel Management Control                              No          11.6.3.12

     0x21           N/A       Get Intel Management Control                              No          11.6.3.13

     0x22           N/A       Perform TCO Reset                                         Yes         11.6.3.14

     0x23           N/A       Enable IP/UDP/TCP Checksum Offloading                     No          11.6.3.15.1

     0x24           N/A       Disable IP/UDP/TCP Checksum Offloading                    No          11.6.3.15.3

                   0x01       Enable OS2BMC Flow                                                    11.6.3.16.1

                   0x02       Enable Network to BMC Flow                                No          11.6.3.16.2
     0x40
                   0x03       Enable Both Network to BMC and Host to BMC Flow                       11.6.3.16.3

                   0x04       Set BMC IP Address                                        Yes         11.6.3.16.4

     0x41           N/A       Get OS2BMC Parameters                                     No          11.6.3.16.5

     0x48           0x1       Get Controller Information                                Yes         11.6.3.17.1

333369-009                                                                                                  1027
                                  Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                    System Manageability

Table 11-30. OEM Commands Summary [continued]
    Intel                                                                                Supported in           Section
                   Parameter                         Command Name
  Command                                                                               MCTP without PT         Number

                      0x0       Get Thermal Sensor Capabilities                                             11.6.3.18.2

       0x4C           0x1       Get Thermal Sensor Configuration                               Yes          11.6.3.18.3

                      0x2       Get Thermal Sensor Status                                                   11.6.3.18.4

                      0x1       Set Thermal Sensor Configuration                                            11.6.3.19.1
       0x4D                                                                                    Yes
                      0x2       Set Thermal Action                                                          11.6.3.19.2

Note:         All the commands are supported both over RMII NC-SI and over MCTP.

#### 11.6.3.4 Proprietary Commands Format

11.6.3.4.1              Set Intel Filters Control Command (Intel Command 0x00)

                                                                    Bits

   Bytes                31:24                        23:16                       15:8                     7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                                              Manufacturer ID (Intel 0x157)

  20...23               0x00                 Filter Control Index

11.6.3.4.2              Set Intel Filters Control Response Format (Intel Command
                        0x00)

                                                                    Bits

   Bytes                31:24                        23:16                       15:8                     7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                        Response Code                                           Reason Code

  20...23                                              Manufacturer ID (Intel 0x157)

  24...27               0x00                 Filter Control Index

1028                                                                                                            333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.5 Set Intel Filters Control — IP Filters Control Command

                        (Intel Command 0x00, Filter Control Index 0x00)
This command controls different aspects of the Intel filters.

                                                                          Bits

   Bytes                 31:24                              23:16                       15:8                              7:0

    0...3

    4...7
                                                                     NC-SI Header
   8...11

   12...15

   16...19                                                    Manufacturer ID (Intel 0x157)

   20...23               0x00                               0x00                               IP Filters control (3-2)

   24...27                       IP Filters Control (1-0)

Where “IP Filters Control” has the following format.

  Bit(s)         Name                                               Description                                           Default Value

# 0 IPv4/IPv6 Mode     IPv6 (0b): There are zero IPv4 filters and four IPv6 filters                                    1b

                                IPv4 (1b): There are four IPv4 filters and four IPv6 filters

  31:1       Reserved

11.6.3.5.1               Set Intel Filters Control — IP Filters Control Response
                         (Intel Command 0x00, Filter Control Index 0x00)

                                                                          Bits

   Bytes                 31:24                              23:16                       15:8                              7:0

    0...3

    4...7
                                                                     NC-SI Header
   8...11

   12...15

   16...19                          Response Code                                                   Reason Code

   20...23                                                    Manufacturer ID (Intel 0x157)

   24...27               0x00                               0x00

333369-009                                                                                                                           1029
                                       Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

#### 11.6.3.6 Get Intel Filters Control Commands (Intel Command

                    0x01)

11.6.3.6.1           Get Intel Filters Control — IP Filters Control Command (Intel
                     Command 0x01, Filter Control Index 0x00)

This command controls different aspects of the Intel filters.

                                                                      Bits

   Bytes             31:24                              23:16                       15:8                              7:0

   0...3

   4...7
                                                                 NC-SI Header
   8...11

  12...15

  16...19                                                 Manufacturer ID (Intel 0x157)

  20...21            0x01                               0x00

11.6.3.6.1.1          Get Intel Filters Control — IP Filters Control Response (Intel
                      Command 0x01, Filter Control Index 0x00)

                                                                      Bits

   Bytes             31:24                              23:16                       15:8                              7:0

   0...3

   4...7
                                                                 NC-SI Header
   8...11

  12...15

  16...19                       Response Code                                                   Reason Code

  20...23                                                 Manufacturer ID (Intel 0x157)

  24...27            0x01                               0x00                               IP Filters Control (3-2)

  28...29                    IP Filters Control (1-0)

1030                                                                                                                        333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.7 Set Intel Filters Formats

11.6.3.7.1             Set Intel Filters Command (Intel Command 0x02)

                                                                   Bits

   Bytes              31:24                       23:16                        15:8                             7:0

    0...3

    4...7
                                                              NC-SI Header
   8...11

   12...15

   16...19                                           Manufacturer ID (Intel 0x157)

   20...21             0x02                 Parameter Number                          Filters Data (optional)

11.6.3.7.1.1            Set Intel Filters Response (Intel Command 0x02)

                                                                   Bits

   Bytes              31:24                       23:16                        15:8                             7:0

    0...3

    4...7
                                                              NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                              Reason Code

   20...23                                           Manufacturer ID (Intel 0x157)

    24...              0x02                 Filter Control Index                      Return Data (Optional)

333369-009                                                                                                            1031
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                               System Manageability

11.6.3.7.2          Set Intel Filters — Manageability Only Command (Intel
                    Command 0x02, Filter Parameter 0x0F)

This command sets the MNGONLY register. The MNGONLY register controls whether pass-through
packets destined to the BMC are not forwarded to the Host OS. The MNGONLY register is described in
Table 11-4.

                                                              Bits

   Bytes           31:24                      23:16                         15:8                             7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                                         Manufacturer ID (Intel 0x157)

  20...23           0x02                      0x0F                                Manageability Only (3-2)

  24...25              Manageability Only (1-0)

11.6.3.7.2.1         Set Intel Filters — Manageability Only Response (Intel Command
                     0x02, Filter Parameter 0x0F)

                                                              Bits

   Bytes           31:24                      23:16                         15:8                             7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                  Response Code                                               Reason Code

  20...23                                         Manufacturer ID (Intel 0x157)

  24...25           0x02                      0x0F

1032                                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.7.3             Set Intel Filters — Flex Filter Enable Mask and Length
                       Command (Intel Command 0x02, Filter Parameter 0x10)

The following command sets the Intel flex filters mask and length.

                                                                     Bits

   Bytes              31:24                          23:16                         15:8                        7:0

    0...3

    4...7
                                                                 NC-SI Header
   8...11

   12...15

   16...19                                             Manufacturer ID (Intel 0x157)

   20...23             0x02                          0x10                       Mask Byte 1                 Mask Byte 2

   24...27              ...                            ...                          ...                         ...

   28...31              ...                            ...                          ...                         ...

   32...35              ...                            ...                          ...                         ...

   36...37         Mask Byte 15                   Mask Byte 16                   Reserved                    Reserved

# 38 Length

11.6.3.7.3.1            Set Intel Filters — Flex Filter Enable Mask and Length Response
                        (Intel Command 0x02, Filter Parameter 0x10)

                                                                     Bits

   Bytes              31:24                          23:16                         15:8                        7:0

    0...3

    4...7
                                                                 NC-SI Header
   8...11

   12...15

   16...19                        Response Code                                               Reason Code

   20...23                                             Manufacturer ID (Intel 0x157)

   24...25             0x02                          0x10

333369-009                                                                                                                1033
                                    Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

11.6.3.7.4             Set Intel Filters — Flex Filter Data Command (Intel
                       Command 0x02, Filter Parameter 0x11)

                                                                     Bits

   Bytes              31:24                         23:16                         15:8                        7:0

   0...3

   4...7
                                                                 NC-SI Header
   8...11

  12...15

  16...19                                              Manufacturer ID (Intel 0x157)

   20...               0x02                         0x11                    Filter Data Group             Filter Data 1

                        ...                      Filter Data N

The Filter Data Group parameter defines which bytes of the Flex filter are set by this command:

Table 11-31. Filter Data Group
            Code              Bytes Programmed           Filter Data Length

            0x0                   Bytes 0–29                      1–30

            0x1                  Bytes 30–59                      1–30

            0x2                  Bytes 60–89                      1–30

            0x3                  Bytes 90–119                     1–30

            0x4                 Bytes 120–127                     1–8

Note:       Using this command to configure the filters data must be done after the flex filter mask
            command is issued and the mask is set.

11.6.3.7.4.1            Set Intel Filters — Flex Filter Data Response (Intel Command
                        0x02, Filter Parameter 0x11)

                                                                     Bits

   Bytes              31:24                         23:16                         15:8                        7:0

   0...3

   4...7
                                                                 NC-SI Header
   8...11

  12...15

  16...19                        Response Code                                              Reason Code

  20...23                                              Manufacturer ID (Intel 0x157)

  24...25              0x02                         0x11

1034                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.7.5             Set Intel Filters — Flex TCP/UDP Port Filter Command
                       (Intel Command 0x02, Filter Parameter 0x63)

                                                                Bits

   Bytes              31:24                      23:16                         15:8                           7:0

    0...3

    4...7
                                                           NC-SI Header
   8...11

   12...15

   16...19                                          Manufacturer ID (Intel 0x157)

   20...23             0x02                       0x63                    Port filter index             TCP/UDP Port MSB

    24 TCP/UDP Port LSB

Filter index range: 0x0...0xA.
If the filter index is bigger than 10, a command failed Response Code is returned with Invalid Intel
Parameter Number reason (0x5082).

11.6.3.7.5.1            Set Intel Filters — Flex TCP/UDP Port Filter Response
                        (Intel Command 0x02, Filter Parameter 0x63)

                                                                Bits

   Bytes              31:24                      23:16                         15:8                           7:0

    0...3

    4...7
                                                           NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                                  Reason Code

   20...23                                          Manufacturer ID (Intel 0x157)

   24...25             0x02                       0x63

333369-009                                                                                                                 1035
                                    Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                               System Manageability

11.6.3.7.6             Set Intel Filters — IPv4 Filter Command (Intel Command
                       0x02, Filter Parameter 0x64)

                                                              Bits

   Bytes              31:24                    23:16                        15:8                          7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                                        Manufacturer ID (Intel 0x157)

  20...23              0x02                    0x64                     IP filter index             IPv4 Address (3)

  24...26                                IPv4 Address (2-0)

Note:       The filters index range can vary according to the IPv4/IPv6 mode setting in the Filters Control
            command.
IPv4 Mode: Filter index range: 0x0...0x3.
IPv6 Mode: This command should not be used in IPv6 mode.

11.6.3.7.6.1            Set Intel Filters — IPv4 Filter Response (Intel Command 0x02,
                        Filter Parameter 0x64)

                                                              Bits

   Bytes              31:24                    23:16                        15:8                          7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                      Response Code                                              Reason Code

  20...23                                        Manufacturer ID (Intel 0x157)

  24...25              0x02                    0x64

If the IPv4 address equals all zero, a command failed Response Code is returned, with Invalid Intel
Parameter Number reason (0x5082).

1036                                                                                                            333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.7.7              Set Intel Filters — IPv6 Filter Command (Intel Command
                        0x02, Filter Parameter 0x65)

                                                              Bits

   Bytes               31:24                    23:16                       15:8                             7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                                        Manufacturer ID (Intel 0x157)

                                                                                                         IPv6 Address
   20...23              0x02                    0x65                    IP filter index
                                                                                                        (MSB, byte 15)

   24...27               ...                     ...                          ...                            ...

   28...31               ...                     ...                          ...                            ...

   32...35               ...                     ...                          ...                            ...

                                                                        IPv6 Address
   36...37               ...
                                                                        (LSB, byte 0)

Note:        The filters index range can vary according to the IPv4/IPv6 mode setting in the Filters Control
             command.
IPv4 Mode: Filter index range: 0x1...0x3.
IPv6 Mode: Filter index range: 0x0...0x3.

11.6.3.7.7.1             Set Intel Filters — IPv6 Filter Response (Intel Command 0x02,
                         Filter Parameter 0x65)

                                                              Bits

   Bytes               31:24                    23:16                       15:8                             7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                             Reason Code

   20...23                                        Manufacturer ID (Intel 0x157)

   24...25              0x02                    0x65

If the IP filter index does not match the ranges above, a command failed Response Code is returned,
with Invalid Intel Parameter Number reason (0x5082).
If the IPv6 address equals all zero, a command failed Response Code is returned, with Invalid Intel
Parameter Number reason (0x5082).

333369-009                                                                                                               1037
                                  Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                            System Manageability

11.6.3.7.8           Set Intel Filters - EtherType Filter Command (Intel
                     Command 0x02, Filter Parameter 0x67)

                                                          Bits

   Bytes            31:24                   23:16                        15:8                        7:0

   0...3

   4...7
                                                     NC-SI Header
   8...11

  12...15

  16...19                                     Manufacturer ID (Intel 0x157)

  20...23            0x02                   0x67                 EtherType Filter Index      EtherType Filter MSB

  24...27             ...                    ...                 EtherType Filter LSB

Where the EtherType Filter has the format as described in Section 8.2.2.19.6.

11.6.3.7.8.1          Set Intel Filters - EtherType Filter Response (Intel Command
                      0x02, Filter Parameter 0x67)

                                                          Bits

   Bytes            31:24                   23:16                        15:8                        7:0

   0...3

   4...7
                                                     NC-SI Header
   8...11

  12...15

  16...19                   Response Code                                           Reason Code

  20...23                                     Manufacturer ID (Intel 0x157)

  24...25            0x02                   0x67

If the EtherType filter Index is larger than 3, a command failed Response Code is returned with Invalid
Intel Parameter Number reason (0x5082).

1038                                                                                                       333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.7.9                   Set Intel Filters - Packet Addition Extended Decision Filter
                             Command (Intel Command 0x02, Filter Parameter 0x68)

See Figure 11-2 for description of the decision filters structure.
This command overwrites any previously stored value. The value set is not checked.

                                                                          Bits

   Bytes                    31:24                        23:16                            15:8                              7:0

    0...3

    4...7
                                                                     NC-SI Header
   8...11

   12...15

   16...19                                                  Manufacturer ID (Intel 0x157)

                                                                                 Extended Decision filter     Extended Decision filter 1
   20...23                   0x02                        0x68
                                                                                         Index                         MSB

                                                                              Extended Decision filter 1      Extended Decision filter 0
   24...27                     ...                         ...
                                                                                        LSB                            MSB

                                                                              Extended Decision filter 0
   28...30                     ...                         ...
                                                                                        LSB

Extended Decision filter Index Range: 0...4
Filter 0: See Table 11-32.
Filter 1: See Table 11-33.

Table 11-32. Filter Values
  Bit(s)                Name                                                        Description

   1:0       Unicast (AND)               If set, packets must match unicast filter 0 to 1, respectively.

   3:2       Reserved                    Reserved.

# 4 Broadcast (AND)             If set, packets must match the broadcast filter.

  12:5       VLAN (AND)                  If set, packets must match VLAN filter 0 to 7, respectively.

  16:13      IPv4 Address (AND)          If set, packets must match IPv4 filter 0 to 3, respectively

  20:17      IPv6 Address (AND)          If set, packets must match IPv4 filter 0 to 3, respectively

  22:21      Unicast (OR)                If set, packets can pass if match unicast filter 0 to 1, respectively, or a different OR filter.

  24:23      Reserved                    Reserved.

# 25 Broadcast (OR)              If set, packets can pass if match the broadcast filter or a different OR filter.

# 26 Multicast (AND)             If set, packets must match the multicast filter.

    27 ARP Request (OR)            If set, packets can pass if match the ARP request filter or a different OR filter.

    28 ARP Response (OR)           If set, packets can pass if match the ARP response filter or a different OR filter.

# 29 Neighbor Discovery - 134    If set, packets can pass if match the neighbor discovery filter (type134 - router

             (OR)                        advertisement) or a different OR filter.

# 30 Port 0x298 (OR)             If set, packets can pass if match a fixed TCP/UDP port 0x298 filter or a different OR filter.

# 31 Port 0x26F (OR)             If set, packets can pass if match a fixed TCP/UDP port 0x26F filter or a different OR filter.

333369-009                                                                                                                            1039
                                        Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

Table 11-33.       Extended Filter 1 Values
 Bit(s)                 Name                                                     Description

   3:0      EtherType 0 -3 (AND)            If set, packets must match the EtherType filter 0 to 3, respectively.

   7:4      EtherType 0 -3 (OR)             If set, packets must match the EtherType filter 0 to 3, respectively, or a different OR
                                            filter.

  18:8      Flex port 10:0 (OR)             If set, packets can pass if match the TCP/UDP Port filter 10:0.

# 19 DHCPv6 (OR)                     If set, packets can pass if match the DHCPv6 port (0x0223).

    20 DHCP Client (OR)                If set, packets can pass if match the DHCP Server port (0x0043).

    21 DHCP Server (OR)                If set, packets can pass if match the DHCP Client port (0x0044).

# 22 NetBIOS Name Service (OR)       If set, packets can pass if match the NetBIOS Name Service port (0x0089).

# 23 NetBIOS Datagram Service (OR)   If set, packets can pass if match the NetBIOS Datagram Service port (0x008A).

# 24 Flex TCO (OR)                   If set, packets can pass if match the Flex 128 TCO filter.

# 25 Neighbor Discovery - 135 (OR)   If set, packets must also match the neighbor discovery filter (type135 - Neighbor

                                            Solicitation. or a different OR filter.

# 26 Neighbor Discovery - 136 (OR)   If set, packets must also match the neighbor discovery filter (type136 - Neighbor

                                            Advertisement) or a different OR filter.

# 27 Neighbor Discovery - 137 (OR)   If set, packets must also match the neighbor discovery filter (type137 - Redirect) or

                                            a different OR filter.

# 28 Reserved                        Reserved.

    29 MLD (OR)                        If set, packets must also match one of the MLD ICMPv6 types or a different OR filter.

  31:30     Reserved                        Reserved.

11.6.3.7.9.1                 Set Intel Filters – Packet Addition Extended Decision Filter
                             Response (Intel Command 0x02, Filter Parameter 0x68)

                                                                    Bits

   Bytes                  31:24                     23:16                          15:8                             7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                          Response Code                                               Reason Code

  20...23                                               Manufacturer ID (Intel 0x157)

  24...25                   0x02                    0x68

If the Extended Decision filter Index is bigger than 5, a command failed Response Code is returned with
Invalid Intel Parameter Number reason (0x5082).

1040                                                                                                                      333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.8 Get Intel Filters Formats

11.6.3.8.1             Get Intel Filters Command (Intel Command 0x03)

                                                               Bits

   Bytes              31:24                      23:16                       15:8                          7:0

    0...3

    4...7
                                                          NC-SI Header
   8...11

   12...15

   16...19                                         Manufacturer ID (Intel 0x157)

   20...21             0x03                 Parameter Number

11.6.3.8.1.1            Get Intel Filters Response (Intel Command 0x03)

                                                               Bits

   Bytes              31:24                      23:16                       15:8                          7:0

    0...3

    4...7
                                                          NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                           Reason Code

   20...23                                         Manufacturer ID (Intel 0x157)

   24...25             0x03                 Parameter Number                        Optional Return Data

333369-009                                                                                                       1041
                                 Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                  System Manageability

11.6.3.8.2          Get Intel Filters — Manageability Only Command (Intel
                    Command 0x03, Filter Parameter 0x0F)

This command retrieves the MNGONLY register. The MNGONLY register controls whether pass-through
packets destined to the BMC are also be forwarded to the Host OS.

                                                                 Bits

   Bytes           31:24                       23:16                           15:8                            7:0

   0...3

   4...7
                                                            NC-SI Header
   8...11

  12...15

  16...19                                            Manufacturer ID (Intel 0x157)

  20...21           0x03                        0x0F

11.6.3.8.2.1         Get Intel Filters — Manageability Only Response (Intel Command
                     0x03, Filter Parameter 0x0F)

The MNGONLY register structure is described in Table 11-4.

                                                                 Bits

   Bytes           31:24                       23:16                           15:8                            7:0

   0...3

   4...7
                                                            NC-SI Header
   8...11

  12...15

  16...19                    Response Code                                                  Reason Code

  20...23                                            Manufacturer ID (Intel 0x157)

  24...27           0x03                        0x0F                                 Manageability to Host (3-2)

  28...29              Manageability to Host (1-0)

1042                                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.8.3              Get Intel Filters — Flex Filter 0 Enable Mask and Length
                        Command (Intel Command 0x03, Filter Parameter 0x10)

The following command retrieves the Intel flex filters mask and length. See Section 11.3.3.5 for details
of the values returned by this command.

                                                                     Bits

   Bytes               31:24                         23:16                         15:8                        7:0

    0...3

    4...7
                                                                 NC-SI Header
   8...11

   12...15

   16...19                                             Manufacturer ID (Intel 0x157)

   20...21              0x03                         0x10

11.6.3.8.3.1             Get Intel Filters — Flex Filter 0 Enable Mask and Length Response
                         (Intel Command 0x03, Filter Parameter 0x10)

                                                                     Bits

   Bytes               31:24                         23:16                         15:8                        7:0

    0...3

    4...7
                                                                 NC-SI Header
   8...11

   12...15

   16...19                        Response Code                                               Reason Code

   20...23                                             Manufacturer ID (Intel 0x157)

   24...27              0x03                         0x10                       Mask Byte 1                 Mask Byte 2

   28...31               ...                           ...                          ...                         ...

   32...35               ...                           ...                          ...                         ...

   36...39               ...                           ...                          ...                         ...

   40...43               ...                      Mask Byte 16                   Reserved                    Reserved

# 44 Flexible Filter Length

333369-009                                                                                                                1043
                                     Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

11.6.3.8.4           Get Intel Filters — Flex Filter 0 Data Command (Intel
                     Command 0x03, Filter Parameter 0x11)

The following command retrieves the Intel flex filters data.

                                                                  Bits

   Bytes            31:24                        23:16                           15:8                         7:0

   0...3

   4...7
                                                              NC-SI Header
   8...11

  12...15

  16...19                                           Manufacturer ID (Intel 0x157)

  20...21            0x03                        0x11                    Filter Data Group 0...4

The Filter Data Group parameter defines which bytes of the Flex filter are returned by this command:

Table 11-34. Filter Data Group
            Code            Bytes Returned

            0x0               Bytes 0–29

            0x1               Bytes 30–59

            0x2               Bytes 60–89

            0x3              Bytes 90–119

            0x4              Bytes 120–127

11.6.3.8.4.1          Get Intel Filters — Flex Filter 0 Data Response (Intel Command
                      0x03, Filter Parameter 0x11)

                                                                  Bits

   Bytes            31:24                        23:16                           15:8                         7:0

   0...3

   4...7
                                                              NC-SI Header
   8...11

  12...15

  16...19                     Response Code                                                 Reason Code

  20...23                                           Manufacturer ID (Intel 0x157)

   24...             0x03                        0x11                     Filter Group Number             Filter Data 1

                      ...                     Filter Data N

1044                                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.8.5             Get Intel Filters — Flex TCP/UDP Port Filter Command (Intel
                       Command 0x03, Filter Parameter 0x63)

                                                                 Bits

   Bytes               31:24                      23:16                        15:8                      7:0

    0...3

    4...7
                                                            NC-SI Header
   8...11

   12...15

   16...19                                           Manufacturer ID (Intel 0x157)

   20...22             0x03                        0x63                 TCP/UDP Filter Index

Filter index range: 0x0...0xA.

11.6.3.8.5.1            Get Intel Filters — Flex TCP/UDP Port Filter Response
                        (Intel Command 0x03, Filter Parameter 0x63)

                                                                 Bits

   Bytes               31:24                      23:16                        15:8                      7:0

    0...3

    4...7
                                                            NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                            Reason Code

   20...23                                           Manufacturer ID (Intel 0x157)

   24...27             0x03                        0x63                 TCP/UDP Filter Index       TCP/UDP Port (1)

    28 TCP/UDP Port (0)

Filter index range: 0x0...0xA.

333369-009                                                                                                            1045
                                     Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                              System Manageability

11.6.3.8.6             Get Intel Filters — IPv4 Filter Command (Intel Command
                       0x03, Filter Parameter 0x64)

                                                              Bits

   Bytes              31:24                    23:16                       15:8                          7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                                        Manufacturer ID (Intel 0x157)

  20...22              0x03                    0x64                  IPv4 Filter Index

Note:       The filters index range can vary according to the IPv4/IPv6 mode setting in the Filters Control
            command.
IPv4 Mode: Filter index range: 0x0...0x3.
IPv6 Mode: This command should not be used in IPv6 mode.

11.6.3.8.6.1            Get Intel Filters — IPv4 Filter Response (Intel Command 0x03,
                        Filter Parameter 0x64)

                                                              Bits

   Bytes              31:24                    23:16                       15:8                          7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                      Response Code                                             Reason Code

  20...23                                        Manufacturer ID (Intel 0x157)

  24...27              0x03                    0x64                  IPv4 Filter Index             IPv4 Address (3)

  28...29                                IPv4 Address (2-0)

1046                                                                                                           333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.8.7              Get Intel Filters — IPv6 Filter Command (Intel Command
                        0x03, Filter Parameter 0x65)

                                                              Bits

   Bytes               31:24                    23:16                       15:8                             7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                                        Manufacturer ID (Intel 0x157)

   20...22              0x03                    0x65                  IPv6 Filter Index

Note:        The filters index range can vary according to the IPv4/IPv6 mode setting in the Filters Control
             command
IPv4 Mode: Filter index range: 0x0...0x2.
IPv6 Mode: Filter index range: 0x0...0x3.

11.6.3.8.7.1             Get Intel Filters — IPv6 Filter Response Intel Command 0x03,
                         Filter Parameter 0x65)

                                                              Bits

   Bytes               31:24                    23:16                       15:8                             7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                             Reason Code

   20...23                                        Manufacturer ID (Intel 0x157)

                                                                                                         IPv6 Address
   24...27              0x03                    0x65                  IPv6 Filter Index
                                                                                                        (MSB, Byte 16)

   28...31               ...                     ...                         ...                              ...

   32...35               ...                     ...                         ...                              ...

   36...39               ...                     ...                         ...                              ...

                                                                        IPv6 Address
   40...42               ...                     ...
                                                                        (LSB, Byte 0)

333369-009                                                                                                               1047
                                  Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                               System Manageability

11.6.3.8.8             Get Intel Filters - EtherType Filter Command (Intel
                       Command 0x03, Filter Parameter 0x67)

                                                             Bits

   Bytes               31:24                   23:16                        15:8                        7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

  12...15

  16...19                                        Manufacturer ID (Intel 0x157)

  20...22              0x03                    0x67                 EtherType Filter Index

Valid indices: 0...3

11.6.3.8.8.1            Get Intel Filters - EtherType Filter Response (Intel Command
                        0x03, Filter Parameter 0x67)

                                                             Bits

   Bytes               31:24                   23:16                        15:8                        7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

  12...15

  16...19                      Response Code                                           Reason Code

  20...23                                        Manufacturer ID (Intel 0x157)

  24...27              0x03                    0x67                 EtherType Filter Index      EtherType Filter MSB

  28...30               ...                     ...                 EtherType Filter LSB

If the EtherType filter Index is larger than 3, a command failed Response Code is returned with Invalid
Intel Parameter Number reason (0x5082).

1048                                                                                                          333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.8.9             Get Intel Filters – Packet Addition Extended Decision Filter
                       Command (Intel Command 0x03, Filter Parameter 0x68)

This command allows the BMC to retrieve the Extended Decision Filter.

                                                             Bits

   Bytes              31:24                    23:16                         15:8                        7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                                       Manufacturer ID (Intel 0x157)

                                                                    Extended Decision Filter
   20...22             0x03                    0x68
                                                                            Index

11.6.3.8.9.1            Get Intel Filters – Packet Addition Extended Decision Filter
                        Response (Intel Command 0x03, Filter Parameter 0x68)

                                                             Bits

   Bytes              31:24                    23:16                         15:8                        7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                            Reason Code

   20...23                                       Manufacturer ID (Intel 0x157)

   24...27             0x03                    0x68                  Decision Filter Index       Decision Filter 1 MSB

   28...31              ...                     ...                  Decision Filter 1 LSB       Decision Filter 0 MSB

   32...34              ...                     ...                  Decision Filter 0 LSB

Where Decision Filter 0 & Decision Filter 1 have the structure as detailed in the respective “Set”
commands.
If the Extended Decision Filter Index is bigger than 4, a command failed Response Code is returned with
Invalid Intel Parameter Number reason (0x5082).

333369-009                                                                                                           1049
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                          System Manageability

#### 11.6.3.9 Set Intel Packet Reduction Filters Formats

The non extended commands (are obsolete. The extended commands (Section 11.6.3.9.2 to
Section 11.6.3.9.4.1) should be used instead

11.6.3.9.1                  Set Intel Packet Reduction Filters Command (Intel
                            Command 0x04)

                                                                        Bits

   Bytes                 31:24                         23:16                          15:8                               7:0

   0...3

   4...7
                                                                  NC-SI Header
   8...11

  12...15

  16...19                                                 Manufacturer ID (Intel 0x157)

  20...23                   0x04               Packet Reduction Index                        Packet Reduction Data

Note:       It is advised that the BMC only uses the Extended Packet Reduction commands.
The Packet Reduction Data field has the following structure:

Table 11-35. Packet Reduction Field Description
 Bit(s)            Name                                                        Description

  12:0      Reserved               Reserved.

  16:13     IPv4 Address (AND)     If set, packets must match IPv4 filter 0 to 3, respectively.

  20:17     IPv6 Address (AND)     If set, packets must match IPv4 filter 0 to 3, respectively.

  27:21     Reserved               Reserved.

    28 ARP Response (OR)      If set, packets can pass if match the ARP response filter or a different OR filter.

# 29 Reserved               Reserved.

# 30 Port 0x298             If set, packets can pass if match a fixed TCP/UDP port 0x298 filter.

# 31 Port 0x26F             If set, packets can pass if match a fixed TCP/UDP port 0x26F filter.

Table 11-36. Extended Packet Reduction Field Description
 Bit(s)            Name                                                        Description

   3:0      EtherType 0 -3 (AND)   If set, packets must match the EtherType filter 0 to 3, respectively.

   7:4      EtherType 0-3 (OR)     If set, packets can pass if match the EtherType filter 0 to 3, respectively.

  15:12     Reserved               Reserved.

  8:18      Flex port 10:0 (OR)    If set, packets can pass if match the TCP/UDP Port filter 10:0.

  23:19     Reserved

# 24 Flex TCO (OR)          If set, packets can pass if match the Flex 128 TCO filter.

  28:25     Reserved

1050                                                                                                                           333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-36. Extended Packet Reduction Field Description [continued]
  Bit(s)           Name                                                      Description

    29 MLD (OR)            If set, packets must also match one of the MLD ICMPv6 types or a different OR filter.

  31:30      Reserved            Reserved.

The filtering is divided into two decisions:
 • Bit 20:13 in Table 11-35 and Bits 3:2 in Table 11-36 works in an AND manner; it must be true for a
   packet to pass (if was set).
 • Bits 28 in Table 11-35 and Bits 24:10 in Table 11-36 work in an OR manner; at least one of them
   must be true for a packet to pass (if any were set).

11.6.3.9.1.1               Set Intel Packet Reduction Filters Response (Intel Command
                           0x04)

                                                                      Bits

   Bytes                31:24                       23:16                           15:8                        7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                       Response Code                                               Reason Code

   20...23                                             Manufacturer ID (Intel 0x157)

    24...                 0x04               Packet Reduction Index

333369-009                                                                                                               1051
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

11.6.3.9.2            Set Extended Unicast Packet Reduction Command (Intel
                      Command 0x04, Reduction Filter Index 0x10)

This command has the following format:

                                                                  Bits

   Bytes              31:24                    23:16                              15:8                     7:0

   0...3

   4...7
                                                           NC-SI Header
   8...11

  12...15

  16...19                                         Manufacturer ID (Intel 0x157)

                                                                           Extended Unicast
  20...23             0x04                      0x10                                                        ...
                                                                          Reduction Filter MSB

                                         Extended Unicast                Unicast Reduction Filter
  24...27              ...                                                                                  ...
                                        Reduction Filter LSB                      MSB

                                       Unicast Reduction Filter
  28...29              ...
                                                LSB

This command overwrites any previously stored value.
Note:       See Table 11-35 and Table 11-36 for description of the Unicast Extended Packet Reduction
            format.

11.6.3.9.2.1           Set Extended Unicast Packet Reduction Response (Intel
                       Command 0x04, Reduction Filter Index 0x10)

                                                                  Bits

   Bytes              31:24                    23:16                              15:8                     7:0

   0...3

   4...7
                                                           NC-SI Header
   8...11

  12...15

  16...19                     Response Code                                                  Reason Code

  20...23                                         Manufacturer ID (Intel 0x157)

  24...25             0x04                      0x10

1052                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.9.3             Set Extended Multicast Packet Reduction Command (Intel
                       Command 0x04, Reduction Filter Index 0x11)

                                                                     Bits

   Bytes               31:24                      23:16                               15:8                     7:0

    0...3

    4...7
                                                             NC-SI Header
   8...11

   12...15

   16...19                                           Manufacturer ID (Intel 0x157)

                       0x04                        0x11                        Extended Multicast              ...
   20...23
                                                                              Reduction Filter MSB

                        ...                 Extended Multicast              Multicast Reduction Filter         ...
   24...27
                                            Reduction Filter LSB                       MSB

                        ...             Multicast Reduction Filter
   28...29
                                                   LSB

Note:        See Table 11-35 and Table 11-36 for description of the Multicast Extended Packet Reduction
             format.
This command overwrites any previously stored value.

11.6.3.9.3.1            Set Extended Multicast Packet Reduction Response (Intel
                        Command 0x04, Reduction Filter Index 0x11)

                                                                     Bits

   Bytes               31:24                      23:16                               15:8                     7:0

    0...3

    4...7
                                                             NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                                     Reason Code

   20...23                                           Manufacturer ID (Intel 0x157)

   24...25             0x04                        0x11

333369-009                                                                                                           1053
                                 Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                System Manageability

11.6.3.9.4            Set Extended Broadcast Packet Reduction Command (Intel
                      Command 0x04, Reduction Filter Index 0x12)

                                                               Bits

   Bytes              31:24                   23:16                          15:8                     7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                                        Manufacturer ID (Intel 0x157)

                                                                      Extended Broadcast
  20...23             0x04                     0x12                                                    ...
                                                                      Reduction Filter MSB

                                        Extended Broadcast        Broadcast Reduction Filter
  24...27              ...                                                                             ...
                                        Reduction Filter LSB                MSB

                                     Broadcast Reduction Filter
  28...29              ...
                                               LSB

Note:       See Table 11-35 and Table 11-36 for description of the Broadcast Extended Packet Reduction
            format.
This command overwrites any previously stored value.

11.6.3.9.4.1           Set Extended Broadcast Packet Reduction Response (Intel
                       Command 0x04, Reduction Filter Index 0x12)

                                                               Bits

   Bytes              31:24                   23:16                          15:8                     7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                     Response Code                                             Reason Code

  20...23                                        Manufacturer ID (Intel 0x157)

  24...25             0x04                     0x12

1054                                                                                                         333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.10 Get Intel Packet Reduction Filters Formats

Note:        The non extended commands are not supported anymore. Use the extended commands
             (Section 11.6.3.10.1 to Section 11.6.3.10.3.1) instead

11.6.3.10.1            Get Extended Unicast Packet Reduction Command (Intel
                       Command 0x05, Reduction Filter Index 0x10)

                                                                  Bits

   Bytes              31:24                       23:16                         15:8                        7:0

    0...3

    4...7
                                                              NC-SI Header
   8...11

   12...15

   16...19                                           Manufacturer ID (Intel 0x157)

   20...21             0x05                        0x10

11.6.3.10.1.1           Get Extended Unicast Packet Reduction Response (Intel
                        Command 0x05, Reduction Filter Index 0x10)

                                                                  Bits

   Bytes              31:24                       23:16                         15:8                        7:0

    0...3

    4...7
                                                              NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                             Reason Code

   20...23                                           Manufacturer ID (Intel 0x157)

   24...27             0x05                        0x00                      Extended Unicast Packet Reduction (3-2)

   28...29          Extended Unicast Packet Reduction (1-0)                      Unicast Packet Reduction (3-2)

   30...31              Unicast Packet Reduction (1-0)

333369-009                                                                                                             1055
                                  Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                  System Manageability

11.6.3.10.2        Get Extended Multicast Packet Reduction Command (Intel
                   Command 0x05, Reduction Filter Index 0x11)

                                                                Bits

   Bytes           31:24                       23:16                          15:8                          7:0

   0...3

   4...7
                                                            NC-SI Header
   8...11

  12...15

  16...19                                         Manufacturer ID (Intel 0x157)

  20...21          0x05                         0x11

11.6.3.10.2.1        Get Extended Multicast Packet Reduction Response (Intel
                     Command 0x05, Reduction Filter Index 0x11)

                                                                Bits

   Bytes           31:24                       23:16                          15:8                          7:0

   0...3

   4...7
                                                            NC-SI Header
   8...11

  12...15

  16...19                    Response Code                                               Reason Code

  20...23                                         Manufacturer ID (Intel 0x157)

  24...27          0x05                         0x11                       Extended Multicast Packet Reduction (3-2)

  28...29       Extended Multicast Packet Reduction (1-0)                      Multicast Packet Reduction (3-2)

  30...31           Multicast Packet Reduction (1-0)

1056                                                                                                              333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.10.3            Get Extended Broadcast Packet Reduction Command (Intel
                       Command 0x05, Reduction Filter Index 0x12)

                                                                   Bits

   Bytes              31:24                       23:16                           15:8                        7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                                           Manufacturer ID (Intel 0x157)

   20...21             0x05                        0x12

11.6.3.10.3.1           Get Extended Broadcast Packet Reduction Response (Intel
                        Command 0x05, Reduction Filter Index 0x12)

                                                                   Bits

   Bytes              31:24                       23:16                           15:8                        7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                               Reason Code

   20...23                                           Manufacturer ID (Intel 0x157)

   24...27             0x05                        0x12                       Extended Broadcast Packet Reduction (3-2)

   28...29         Extended Broadcast Packet Reduction (1-0)                      Broadcast Packet Reduction (3-2)

   30...31             Broadcast Packet Reduction (1-0)

333369-009                                                                                                                1057
                                  Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                              System Manageability

#### 11.6.3.11 System MAC Address

11.6.3.11.1         Get System MAC Address Command (Intel Command 0x06)

To support a system configuration that requires the NC to hold the MAC Address for the BMC (such as
shared MAC Address mode), the following command is provided to enable the BMC to query the NC for
a valid MAC Address.
The NC must return the system MAC Addresses. The BMC should use the returned MAC Addressing as a
shared MAC Address by setting it using the Set MAC Address command as defined in NC-SI 1.0.
It is also recommended that the BMC use packet reduction and Manageability-to-Host command to set
the proper filtering method.

                                                             Bits

   Bytes           31:24                     23:16                         15:8                     7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                                       Manufacturer ID (Intel 0x157)

       20           0x06

11.6.3.11.2         Get System MAC Address Response (Intel Command 0x06)

                                                             Bits

   Bytes           31:24                     23:16                         15:8                     7:0

   0...3

   4...7
                                                         NC-SI Header
   8...11

  12...15

  16...19                  Response Code                                              Reason Code

  20...23                                       Manufacturer ID (Intel 0x157)

  24...27           0x06                                                MAC Address

  28...30                                  MAC Address

1058                                                                                                      333369-009
                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.12 Set Intel Management Control Formats

11.6.3.12.1               Set Intel Management Control Command (Intel Command
                          0x20)

                                                                     Bits

   Bytes                 31:24                       23:16                        15:8                          7:0

    0...3

    4...7
                                                                NC-SI Header
   8...11

   12...15

   16...19                                              Manufacturer ID (Intel 0x157)

                                                                        Intel Management Control
   20...22                0x20                        0x00
                                                                                    1

Where Intel Management Control 1 is as follows:

  Bit(s)     Default                                                Description

    0          0b      Enable Critical Session Mode (Keep PHY Link Up and Veto Bit)
                        0b = Disabled
                        1b = Enabled
                       When critical session mode is enabled, the following behaviors are disabled:
                        • The PHY is not reset on PE_RST# and PCIe resets (in-band and link drop). Other reset events are not
                          affected — Internal_Power_On_Reset, device disable, Force TCO, and PHY reset by software.
                        • The PHY does not change its power state. As a result link speed does not change.
                        • The device does not initiate configuration of the PHY to avoid losing link.

   7:1        0x0      Reserved.

11.6.3.12.2               Set Intel Management Control Response (Intel Command
                          0x20)

                                                                     Bits

   Bytes                 31:24                       23:16                        15:8                          7:0

    0...3

    4...7
                                                                NC-SI Header
   8...11

   12...15

   16...19                         Response Code                                             Reason Code

   20...23                                              Manufacturer ID (Intel 0x157)

   24...25                0x20                        0x00

333369-009                                                                                                                 1059
                                     Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                          System Manageability

#### 11.6.3.13 Get Intel Management Control Formats

11.6.3.13.1         Get Intel Management Control Command (Intel Command
                    0x21)

                                                         Bits

   Bytes           31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                                    NC-SI Header
   8...11

  12...15

  16...19                                    Manufacturer ID (Intel 0x157)

  20...21           0x21                   0x00

Where Intel Management Control 1 is as described in Section 11.6.3.12.2.

11.6.3.13.2         Get Intel Management Control Response (Intel Command
                    0x21)

                                                         Bits

   Bytes           31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                                    NC-SI Header
   8...11

  12...15

  16...19                  Response Code                                        Reason Code

  20...23                                    Manufacturer ID (Intel 0x157)

                                                             Intel Management Control
  24...26           0x21                   0x00
                                                                        1

1060                                                                                                  333369-009
                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.14 TCO Reset

Depending on the bit set in the TCO mode field this command causes the X550 to perform either:
1. TCO Reset
      • The Force TCO reset clears the data-path (Rx/Tx) of the X550 to enable the BMC to transmit/
        receive packets through the X550.
      • If the BMC has detected that the OS is hung and has blocked the Rx/Tx path The Force TCO
        reset clears the data-path (Rx/Tx) of the Network Controller to enable the BMC to transmit/
        receive packets through the Network Controller.
      • When this command is issued to a channel in a package, it applies only to the specific channel.
      • After successfully performing the command, the Network Controller considers Force TCO
        command as an indication that the OS is hung, and clears the DRV_LOAD flag (disable the
        driver). If TCO reset is disabled in NVM, the X550 does not reset the data-path and notifies BMC
        on successful completion.
2. TCO isolate
      • If TCO isolate is enabled in the NVM (See Section 6.2.16). The TCO Isolate command disables
        PCIe write operations to the LAN port.
      • If TCO Isolate is disabled in NVM, the X550 does not execute the command but sends a
        response to the BMC with successful completion.
      • Following TCO Isolate management isolates the function related to the port on which the
        command was received.
3. Firmware Reset
      • This command causes re-initialization of all the manageability functions and re-load of
        manageability related NVM words.
      • When the BMC has loaded new management-related NVM image, the Firmware Reset command
        loads management-related NVM information without the need to power down the system.
      • This command is issued to the package and affects all channels. After the firmware reset the
        FW Semaphore register (FWSM) is re-initialized.
Note:        TCO isolate and force TCO affects only the channel (port) that the command was issued to.
             Following firmware reset, BMC must re-initialize all ports. Only one of the fields should be set
             in a given command. Setting more than one field may yield unexpected results.

11.6.3.14.1             Perform Intel TCO Reset Command (Intel Command 0x22)

                                                              Bits

   Bytes               31:24                   23:16                        15:8                7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                                        Manufacturer ID (Intel 0x157)

     20                 0x22                                             TCO Mode

333369-009                                                                                               1061
                                  Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                      System Manageability

Where TCO Mode is:

         Field          Bit(s)                                          Description

 DO_TCO_RST               0      Perform TCO Reset.
                                  0b = Do nothing.
                                  1b = Perform TCO reset.

 DO_TCO_ISOLATE1          1      Do TCO Isolate
                                  0b = Enable PCIe write access to LAN port.
                                  1b = Isolate Host PCIe write operation to the port
                                 Note: Should be used for debug only.

 RESET_MGMT               2      Reset manageability; re-load manageability NVM words.
                                  0b = Do nothing.
                                  1b = Issue firmware reset to manageability.
                                 Setting this bit generates a one-time firmware reset. Following the reset, management
                                 related data from NVM is loaded.

 Reserved                7:3     Reserved (set to 0x00).

 Note:   For compatibility, the TCO reset command without the TCO Mode parameter is accepted (TCO reset is performed).

1. TCO Isolate Host Write operation enabled in NVM.

11.6.3.14.2              Perform Intel TCO Reset Response (Intel Command 0x22)

When a firmware reset is requested (TCO Mode = RESET_MGMT), there is no response, as the NC goes
to Initial State as part of the command execution.

                                                                     Bits

    Bytes                31:24                        23:16                        15:8                         7:0

    0...3

    4...7
                                                                NC-SI Header
    8...11

   12...15

   16...19                         Response Code                                             Reason Code

   20...23                                              Manufacturer ID (Intel 0x157)

   24...26               0x22

1062                                                                                                                  333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.15 Checksum Offloading

This command enables the checksum offloading filters in the NC.
When enabled, these filters block any packets that did not pass IP, UDP or TCP checksum from being
forwarded to the BMC.

11.6.3.15.1            Enable Checksum Offloading Command (Intel Command
                       0x23)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                 7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                                       Manufacturer ID (Intel 0x157)

     20                0x23

11.6.3.15.2            Enable Checksum Offloading Response (Intel Command
                       0x23)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                 7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                      Reason Code

   20...23                                       Manufacturer ID (Intel 0x157)

   24...26             0x23

333369-009                                                                                            1063
                                 Did this document help answer your questions?

                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                     System Manageability

11.6.3.15.3   Disable Checksum Offloading Command (Intel Command
              0x24)

                                                    Bits

   Bytes      31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                               NC-SI Header
   8...11

  12...15

  16...19                               Manufacturer ID (Intel 0x157)

       20     0x24

11.6.3.15.4   Disable Checksum Offloading Response (Intel Command
              0x24)

                                                    Bits

   Bytes      31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                               NC-SI Header
   8...11

  12...15

  16...19             Response Code                                       Reason Code

  20...23                               Manufacturer ID (Intel 0x157)

  24...26     0x24

1064                                                                                             333369-009
                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.16 OS2BMC Configuration

These commands control enabling of the OS 2 BMC flow.

11.6.3.16.1            Enable OS2BMC Flow Command (Intel Command 0x40,
                       Index 0x1)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                 7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                                       Manufacturer ID (Intel 0x157)

   20...21             0x40                    0x01

11.6.3.16.1.1           EnableOS2BMC Flow Response (Intel Command 0x40, Index 0x1)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                 7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                     Response Code                                      Reason Code

   20...23                                       Manufacturer ID (Intel 0x157)

   24...25             0x40                    0x01

11.6.3.16.2            Enable Network to BMC Flow Command (Intel Command
                       0x40, Index 0x2)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                 7:0

    0...3

    4...7
                                                        NC-SI Header
   8...11

   12...15

   16...19                                       Manufacturer ID (Intel 0x157)

   20...21             0x40                    0x02

333369-009                                                                                            1065
                                 Did this document help answer your questions?

                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                       System Manageability

11.6.3.16.2.1    Enable Network to BMC Flow Response (Intel Command 0x40,
                 Index 0x2)

                                                      Bits

   Bytes        31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                                 NC-SI Header
   8...11

  12...15

  16...19               Response Code                                       Reason Code

  20...23                                 Manufacturer ID (Intel 0x157)

  24...25       0x40                    0x02

11.6.3.16.3     Enable Both Host and Network to BMC Flows Command
                (Intel Command 0x40, Index 0x3)

                                                      Bits

   Bytes        31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                                 NC-SI Header
   8...11

  12...15

  16...19                                 Manufacturer ID (Intel 0x157)

  20...21       0x40                    0x03

11.6.3.16.3.1    Enable Both Host and Network to BMC Flows Response (Intel
                 Command 0x40, Index 0x3)

                                                      Bits

   Bytes        31:24                   23:16                       15:8                     7:0

   0...3

   4...7
                                                 NC-SI Header
   8...11

  12...15

  16...19               Response Code                                       Reason Code

  20...23                                 Manufacturer ID (Intel 0x157)

  24...25       0x40                    0x03

1066                                                                                               333369-009
                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.16.4             Set BMC IP Address Command (Intel Command 0x40, Index
                        0x4)

This command is used to expose the BMC IP Address to the host.
The IP type entry indicate whether the IP Address is an IPv4 or an IPv6 address:
    0 = IPv4
    1 = IPv6
    2 = No IP Address, then the command should not include an IP Address.

                                                                   Bits

   Bytes               31:24                     23:16                             15:8                      7:0

    0...3

    4...7
                                                            NC-SI Header
   8...11

   12...15

   16...19                                          Manufacturer ID (Intel 0x157)

                                                                                                    IPv6 Address (MSB, byte
   20...23              0x40                      0x04                            IP type           15)/IPv4 Address (MSB,
                                                                                                            byte 3)

                                                                          IPv6 Address (byte 12)/
               IPv6 Address (byte 14)/   IPv6 Address (byte 13)/                                    IPv6 Address (byte 11)/
   24...27                                                                     IPv4 Address
                IPv4 Address (byte 2)     IPv4 Address (byte 1)                                            Reserved
                                                                               (LSB, byte 0)

   28...31               ...                       ...                              ...                       ...

   32...35               ...                       ...                              ...                       ...

                                                                          IPv6 Address (LSB, byte
   36...38               ...                       ...
                                                                                0)/Reserved

11.6.3.16.4.1            Set BMC IP Address Response (Intel Command 0x40, Index 0x4)

                                                                   Bits

   Bytes               31:24                     23:16                             15:8                      7:0

    0...3

    4...7
                                                            NC-SI Header
   8...11

   12...15

   16...19                       Response Code                                               Reason Code

   20...23                                          Manufacturer ID (Intel 0x157)

   24...25              0x40                      0x04

333369-009                                                                                                              1067
                                   Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                               System Manageability

11.6.3.16.5                Get OS2BMC Parameters Command (Intel Command 0x41)

                                                                            Bits

   Bytes                  31:24                           23:16                             15:8                      7:0

   0...3

   4...7
                                                                       NC-SI Header
   8...11

  12...15

  16...19                                                       Manufacturer ID (Intel 0x157)

       20                  0x41

11.6.3.16.5.1               Get OS2BMC Parameters Response (Intel Command 0x41)

                                                                            Bits

   Bytes                  31:24                           23:16                             15:8                      7:0

   0...3

   4...7
                                                                       NC-SI Header
   8...11

  12...15

  16...19                            Response Code                                                    Reason Code

  20...23                                                       Manufacturer ID (Intel 0x157)

                                                                                   IPv6 Address (MSB, byte
                                                                                                             IPv6 Address (byte 14)/
  24...27                  0x41                           Status                   15)/IPv4 Address (MSB,
                                                                                                              IPv4 Address (byte 2)
                                                                                           byte 3)

                                                IPv6 Address (byte 12)/
                 IPv6 Address (byte 13)/                                           IPv6 Address (byte 11)/
  28...31                                            IPv4 Address                                                      ...
                  IPv4 Address (byte 1)                                                   Reserved
                                                     (LSB, byte 0)

  32...35                    ...                            ...                              ...                       ...

  36...39                    ...                            ...                              ...                       ...

                                                IPv6 Address (LSB, byte
  40...41                    ...
                                                      0)/Reserved

Where the Status byte partition is as follows:

Table 11-37. Status Byte Description
 Bit(s)                                                                 Content

# 0 Relevant only if the IP Address valid bit is set.

             0b = IPv4
             1b = IPv6

    1 IP Address valid.

# 2 Network to BMC status.

             0b = Network 2 BMC flow is disabled.
             1b = Network 2 BMC flow is enabled.

1068                                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-37. Status Byte Description [continued]
  Bit(s)                                                      Content

# 3 OS2BMC status.

              0b = OS 2 BMC flow is disabled.
              1b = OS 2 BMC flow is enabled.

   7:4       Reserved.

#### 11.6.3.17 Get Controller Information Command (Intel Command

                         0x48, Index 0x1)
This command gather the controller identification information and return it back to the BMC.

                                                                  Bits

   Bytes                  31:24                    23:16                        15:8      7:0

    0...3

    4...7
                                                             NC-SI Header
   8...11

   12...15

   16...19                                            Manufacturer ID (Intel 0x157)

   20...23                0x48                      0x1

333369-009                                                                                      1069
                                      Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                        System Manageability

11.6.3.17.1               Get Controller Information Response (Intel Command 0x48,
                          Index 0x1)

                                                                         Bits

   Bytes                 31:24                         23:16                         15:8                           7:0

   0...3

   4...7
                                                                  NC-SI Header
   8...11

  12...15

  16...19                          Response Code                                                 Reason Code

  20...23                                                 Manufacturer ID (Intel 0x157)

                                                                                                           Number of Inventory
  24...27                 0x48                          0x01                       Reserved
                                                                                                                entries

                                                Controller Info Item 1
  28...31       Controller Info Item 1 ID                                                 Controller Info Item 1 Data
                                                        length

       ...                                                               ....

                                                Controller Info Item 2
       ...      Controller Info Item 2 ID                                                 Controller Info Item 2 Data
                                                        length

       ...                                                               ....

                                                Controller Info Item n
       ...      Controller Info Item n ID                                                 Controller Info Item n Data
                                                        length

       ...                                                               ....

Where the possible inventory items are as described below. Note that not all the inventory items would
be present in all the implementations of this command.

Table 11-38. Controller Information Items
             Length
   ID                                   Data                                                    Notes
             (bytes)

                                                                  This is the hardware default value, not any value programmed via
  0x00         3       Device ID (2 bytes) + RevID                NVM.
                                                                  Not returned if command set while device is in Dr.

  0x0B         2       NVM Image Version

  0x0C         4       EMP ROM Internal Version

  0x0D         4       Flash Firmware Image Internal version

  0x0E         2       PXE firmware version

  0x0F         2       iSCSI firmware version
                                                                  MajorVersion.MinorVersion.Build
  0x10         2       uEFI firmware version

  0x16         2       FCoE Boot firmware version

  0x17         4       Firmware Mini Loader Internal version

1070                                                                                                                      333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.18 Get Thermal Sensor Commands (Intel Command 0x4C)

The following tables are used in the various commands:

Table 11-39. Actions Word Definition
  Bit(s)                  Action                                                         Notes

# 0 Measure only                         Activate the thermal sensor, but no automatic action.

# 1 Notify BMC

# 2 Power off PHY

# 3 Power on PHY

                                                  When the Cancel TS Action command is received, the X550 should set the PHY to its

# 4 Restore Speed

                                                  previous state.

# 5 Set speed to 10 Mb/s Max             N/A for the X550.

# 6 Set speed to 100 Mb/s Max

                                                  These actions set a maximum on the speed and do not force a specific speed. The Set

# 7 Set speed to 1 Gb/s Max

                                                  Link command should be used to set a specific link speed.

# 8 Set speed to 10 Gb/s Max

# 9 Indicate on SDP (set)                The SDP indication is done on SDP_1_1. Indicate on SDP actions are available only if

                                                  SDP_1_1 is configured as an output in the ESDP register.

# 10 Indicate on SDP (clear)

                                                  This is used for the X550 and is equivalent to the NVM based mechanism described in

    11 HW autonomous algorithm              Section 5.7.3. When the Threshold set by the MC is crossed, both PHYs are powered

                                                  down. This action can be canceled by a Cancel all active actions immediate action

# 12 Cancel all active actions

                                                  When the Cancel TS Action command is received, the X550 should set the PHY to its

# 13 Rearm Event

                                                  previous state.

  31:14      Reserved

Table 11-40. Unit Types Word Definition
   Value             Unit Types                                                       Notes

    0x0        Generic Number            No specific indication of measured value.

    0x1        Celsius                   Temperature.

    0x2        Volts

    0x3        rpm                       Speed.

  0x4-0xFF     Reserved                  Reserved.

11.6.3.18.1                  Threshold and Hysteresis

Each threshold event includes a direction. For example, a thermal event with a threshold of 100 °C and
an “up” direction is defined as the temperature crossing from less than 100 °C to more than 100 °C.
For each threshold an hysteresis may be defined. This hysteresis direction is opposite to the threshold
direction. If in the previous example, an hysteresis of 10 °C is defined, it is activated when the
temperature crosses from more than 90 °C to less than 90 °C.
Figure 11-8 describes the thresholds and hysteresis modes and the actions activated for each of them.

333369-009                                                                                                                         1071
                                          Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                      System Manageability

           Going high Threshold (100)                                              Going Low Threshold (100)
           Activate Going High Action                                              Activate Going Low Action

                     110

                     100
                                                                                          Going Low hysteresis (110)

# 90 Activate Going High Action

                 Reading

                                                             Going high hysteresis (90)
                                                             Activate Going Low Action

Figure 11-8. Thresholds, Hysteresis and Actions

Note:        As there are no low thresholds in the X550, there is no support for thresholds.

11.6.3.18.2                Get Thermal Sensor Capabilities Command (Intel Command
                           0x4C, Index 0x0)

This command requests the thermal sensor capabilities supported by this device.

                                                                    Bits

   Bytes                   31:24                     23:16                        15:8                         7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                                               Manufacturer ID (Intel 0x157)

  20...21                  0x4C                       0x00

1072                                                                                                                 333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.6.3.18.2.1           Get Thermal Sensor Capabilities Response (Intel Command 0x4C,
                        Index 0x0)

                                                                    Bits

   Bytes              31:24                          23:16                        15:8                            7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                       Response Code                                                 Reason Code

   20...23                                             Manufacturer ID (Intel 0x157)

   24...27             0x4C                           0x0                        Version                       Unit Types

   28...31                    Number of Thresholds                              Accuracy                     Max hysteresis

   32...35              M                             B                             K1                            K2

   36...39                                       Available actions - “High going” thresholds

   40...43                                       Available actions - “Low going” thresholds

 • Version should always be 1.
 • Unit Types = 1 - Temperature reported in Celsius.
 • Accuracy describes the accuracy of the reported measurements is as follows:
     — 7:4: Max deviation of actual value above measurement in “unit types” = 3 °C
     — 3:0: Max deviation of actual value below measurement in “unit types” = 3 °C
 • Number of thresholds describes the number of up and down thresholds as follows:
     — 15:12: Reserved
     — 11:8: Max Number of mixed thresholds = 0
     — 7:4: Max number of up thresholds = 1
     — 3:0: Max number of down thresholds = 0
 • Available Actions “High going” thresholds — Describes the actions that can be activated by the
   device as described in Table 11-39 when a high going threshold is crossed. The X550 supports
   Measure Only, Notify BMC, Indicate on SDP (set), Set speed to 100 Mb/s Max, Set speed to 1 GbE
   Max, and HW autonomous actions.
 • Available Actions “Low going” thresholds — Describes the actions that can be activated by the
   device as described in Table 11-39 when a low going threshold is crossed. The X550 does not
   support low going thresholds.
 • Available Actions “Immediate” — Describes the actions that can be activated by the device as
   described in Table 11-39. The X550 supports Reset Thermal Sensor, Cancel all active actions, and
   measure-only actions.
 • M = 1; B = 0, K1 = K2 = 0 — The assumption is that the thermal sensor in the X550 is the readable
   value.
 • Tjunction-Max — The maximal junction temperature supported in X550 is 105 °C.

333369-009                                                                                                                    1073
                                   Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                    System Manageability

Note:       This formula is compliant with the definition of section 36.3 “Sensor Reading Conversion
            Formula” in IPMI 2.0

11.6.3.18.3             Get Thermal Sensor Configuration Command (Intel
                        Command 0x4C, Index 0x1)

This command requests the thermal sensor configuration for threshold “Index” in direction “Direction”.

                                                                   Bits

   Bytes               31:24                        23:16                        15:8                        7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                                              Manufacturer ID (Intel 0x157)

  20...22               0x4C                         0x01                       Index

Note:       If Index points to a non valid threshold as described in the Get Thermal Sensor Capabilities
            Response, the command fails with an Invalid Parameter reason.

11.6.3.18.3.1            Get Thermal Sensor Configuration Response (Intel Command
                         0x4C, Index 0x1)

                                                                   Bits

   Bytes               31:24                        23:16                        15:8                        7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                          Response Code                                           Reason Code

  20...23                                              Manufacturer ID (Intel 0x157)

  24...27               0x4C                         0x1                        Index                    Threshold (1)

  28...31           Threshold(0)                                      Actions “Going High” (3-1)

  32...35      Actions “Going High” (0)                                Actions “Going Low” (3-1)

  36...38      Actions “Going Low” (0)             Direction                  Hysteresis

The threshold and the Hysteresis are measured in “unit types”.
The Actions Going High field describes the actions to activate upon crossing of the threshold for “Going
High” thresholds or when crossing the hysteresis for “Going Low” thresholds according to Table 11-39.
The Actions Going Low field describes the actions to activate upon crossing of the threshold for “Going
Low” thresholds or when crossing the hysteresis for “Going High” thresholds according to Table 11-39.

1074                                                                                                               333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Direction is encoded as follows:
    0 = High Going
    1 = Low Going

11.6.3.18.4            Get Thermal Sensor Status Command (Intel Command 0x4C,
                       Index 0x2)

This command requests the current status of the Thermal sensor.

                                                                    Bits

   Bytes              31:24                        23:16                          15:8                    7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                                              Manufacturer ID (Intel 0x157)

   20...21             0x4C                            0x02

11.6.3.18.4.1           Get Thermal Sensor Status Response (Intel Command 0x4C,
                        Index 0x2)

                                                                    Bits

   Bytes              31:24                        23:16                          15:8                    7:0

    0...3

    4...7
                                                               NC-SI Header
   8...11

   12...15

   16...19                       Response Code                                            Reason Code

   20...23                                              Manufacturer ID (Intel 0x157)

   24...27             0x4C                            0x2                               Measured Value

   28...31                                                     Active Actions

   32...33                    Threshold cross events

Where “Threshold cross events” is a bitmap that describes which events were crossed since the last
read of the status or since the activation of the thermal sensor (the latest of the two).
Bit ‘n’ in the bitmap represent threshold index ‘n’ as configured in the Set Thermal Sensor Configuration
command (Section 11.6.3.19.1).
Active actions can be set for the following actions (if supported by the device):
 • Measure only
 • Notify BMC
 • Power off PHY

333369-009                                                                                                      1075
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                     System Manageability

 • Set speed to 10 Mb/s Max
 • Set speed to 100 Mb/s Max
 • Set speed to 1 Gb/s Max
 • Set speed to 10 Gb/s Max
 • Indicate on SDP (set)
 • Indicate on SDP (clear)
 • HW autonomous algorithm.

#### 11.6.3.19 Set Thermal Sensor Commands (Intel Command 0x4D)

11.6.3.19.1             Set Thermal Sensor Configuration Command (Intel
                        Command 0x4D, Index 0x1)

This command sets the thermal sensor configuration for threshold “Index”
The threshold and the Hysteresis are measured in “unit types”.
Note:       If the Max hysteresis reported in the Thermal Sensor capabilities is zero, the Hysteresis value
            is ignored.
The Actions Going High field describes the actions to activate upon crossing of the threshold for “Going
High” thresholds or when crossing the hysteresis for “Going Low” thresholds according to Table 11-39.
The Actions Going Low field describes the actions to activate upon crossing of the threshold for “Going
Low” thresholds or when crossing the hysteresis for “Going High” thresholds according to Table 11-39.
Direction is encoded as follows:
       0 = High Going
       1 = Low Going

                                                                    Bits

   Bytes                31:24                      23:16                          15:8                           7:0

   0...3

   4...7
                                                               NC-SI Header
   8...11

  12...15

  16...19                                               Manufacturer ID (Intel 0x157)

  20...23               0x4D                       0x01                          Index                        Direction

  24...27                          Threshold                                            Actions “Going High” (MSB)

  28...31                  Actions “Going High” (LSB)                                   Actions “Going Low” (MSB)

  32...34                  Actions “Going Low” (LSB)                           Hysteresis

Note:       If Index and Direction points to a non valid threshold as described in the Get Thermal Sensor
            Capabilities Response, the command fails with an Invalid Parameter reason.
Note:       If the requested action is not supported as defined in Get Thermal Sensor Capabilities
            Command (Section 11.6.3.18.2), the command fails with an Invalid Parameter reason.

1076                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Note:        Actions set can not be contradictory - so for a given set of actions, the following combinations
             are invalid, and result in a command fails with an Invalid Parameter reason:
              • Indicate on SDP (set) and Indicate on SDP (clear) both set,
              • Power Down PHY and Power up PHY both set.
              • Increase and Reduce Speed both set.
              • Both a Speed update and a PHY power down action are requested.
              • Do Nothing and another option are requested.
              • HW independent algorithm and another option are requested.

11.6.3.19.1.1            Set Thermal Sensor Configuration Response (Intel Command
                         0x4D, Index 0x1)

                                                              Bits

   Bytes               31:24                    23:16                       15:8                   7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                      Response Code                                      Reason Code

   20...23                                        Manufacturer ID (Intel 0x157)

   24...25              0x4D                     0x1

11.6.3.19.2             Set Thermal Sensor Action Command (Intel Command 0x4D,
                        Index 0x2)

This command executes actions immediately.
The Actions field describes the actions to activate according to Table 11-39.

                                                              Bits

   Bytes               31:24                    23:16                       15:8                   7:0

    0...3

    4...7
                                                         NC-SI Header
   8...11

   12...15

   16...19                                        Manufacturer ID (Intel 0x157)

   20...23              0x4D                    0x02                               Actions (MSB)

   24...25                      Actions (LSB)

Note:        If one of the requested actions is not supported as defined in Get Thermal Sensor Capabilities
             Command (Section 11.6.3.18.2), the command fails with an Invalid Parameter reason.

333369-009                                                                                               1077
                                  Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                              System Manageability

Note:       Actions set can not be contradictory - so the following combinations are invalid and result in a
            command fails with an Invalid Parameter reason:
             • Indicate on SDP (set) and Indicate on SDP (clear) both set,
             • Power Down PHY and Power up PHY both set.
             • Restore and one of the Reduce Speed both set.
             • Both a Speed update and a PHY power down action are requested.
             • Do Nothing and another option are requested.
             • HW independent algorithm and another option are requested.

11.6.3.19.2.1           Set Thermal Sensor Action Response (Intel Command 0x4D,
                        Index 0x2)

                                                             Bits

   Bytes              31:24                    23:16                       15:8                     7:0

   0...3

   4...7
                                                        NC-SI Header
   8...11

  12...15

  16...19                      Response Code                                       Reason Code

  20...23                                        Manufacturer ID (Intel 0x157)

  24...25              0x4D                     0x2

1078                                                                                                      333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.3.20 Intel OEM AENs

11.6.3.20.1             Thermal Sensor AEN (Intel AEN 0x81)

The following is the AEN that may be sent by the NC following a Thermal Sensor event.
This AEN must be enabled using the NC-SI “AEN Enable” command, using bit 17 (0x20000) of the AEN
Enable mask.
This AEN is sent on all the channels on which it is enabled.

### 11.6.4 Asynchronous Event Notifications

                                                                   Bits

   Bytes               31:24                      23:16                         15:8                    7:0

    0...3

    4...7
                                                           NC-SI AEN Header
   8...11

   12...15

   20...23                                      Reserved                                                0x81

                                                 Direction
   24...27    Index of threshold crossed      0 = High Going                           Measured Value
                                              1 = Low Going

   28...31                                                     Active Actions

The asynchronous event notifications are unsolicited messages sent from the NC to the BMC to report
status changes (such as link change, operating system state change, etc.).
Recommendations:
 • The BMC firmware designer should use AENs. To do so, the designer must take into account the
   possibility that a NC-SI response frame (such as a frame with the NC-SI EtherType), arrives out-of-
   context (not immediately after a command, but rather after an out-of-context AEN).
 • To enable AENs, the BMC should first query which AENs are supported, using the Get Capabilities
   command, then enable desired AEN(s) using the Enable AEN command, and only then enable the
   channel using the Enable Channel command.

### 11.6.5 Querying Active Parameters

The BMC can use the Get Parameters command to query the current status of the operational
parameters.

333369-009                                                                                                     1079
                                    Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                             System Manageability

### 11.6.6 Resets

In NC-SI there are two types of resets defined:
1. Synchronous entry into the initial state.
2. Asynchronous entry into the initial state.
Recommendations:
 • It is very important that the BMC firmware designer keep in mind that following any type of reset,
   all configurations are considered as lost and thus the BMC must re-configure everything.
 • As an asynchronous entry into the initial state might not be reported and/or explicitly noticed, the
   BMC should periodically poll the NC with NC-SI commands (such as Get Version ID, Get Parameters,
   etc.) to verify that the channel is not in the initial state. Should the NC channel respond to the
   command with a Clear Initial State Command Expected reason code, the BMC should consider the
   channel (and most probably the entire NC package) as if it underwent a (possibly unexpected) reset
   event. Thus, the BMC should re-configure the NC. See the NC-SI specification section on Detecting
   Pass-through Traffic Interruption.
 • The Intel recommended polling interval is 2-3 seconds.
For exact details on the resets, refer to NC-SI specification.

### 11.6.7 Advanced Workflows

#### 11.6.7.1 Multi-NC Arbitration

As described in Section 11.6.1.2, in a multi-NC environment, there is a need to arbitrate the NC-SI
lines.
Figure 11-9 shows the system topology of such an environment.

                                                      MC

                                                             NC-SI TX lines

                                                        NC-SI RX lines

                                   NC Package1                    NC Package2
                                  Channel1: 0x0                  Channel1: 0x0
                                  Channel2: 0x1

                                                           HW-Arbitration lines

Figure 11-9. Multi-NC Environment

1080                                                                                                   333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

See Figure 11-9. The NC-SI Rx lines are shared between the NCs. To enable sharing of the NC-SI Rx
lines, NC-SI has defined an arbitration scheme.
The arbitration scheme mandates that only one NC package can use the NC-SI Rx lines at any given
time. The NC package that is allowed to use these lines is defined as selected. All the other NC
packages are de-selected.
NC-SI has defined two mechanisms for the arbitration scheme:
1. Package selection by the BMC. In this mechanism, the BMC is responsible for arbitrating between
   the packages by issuing NC-SI commands (Select/De-Select Package). The BMC is responsible for
   having only one package selected at any given time.
2. Hardware arbitration. In this mechanism, two additional pins on each NC package are used to
   synchronize the NC package. Each NC package has an ARB_IN and ARB_OUT line and these lines
   are used to transfer Tokens. A NC package that has a token is considered selected.
Note:        Hardware arbitration is enabled by the NC-SI HW Arbitration Enable configuration bit in NVM
             Control Word 1.
For details, refer to the NC-SI specification.

#### 11.6.7.2 Package Selection Sequence Example

Following is an example work flow for a BMC and occurs after the discovery, initialization, and
configuration.
Assuming the BMC needs to share the NC-SI bus between packages, the BMC should:
1. Define a time-slot for each device.
2. Discover, initialize, and configure all the NC packages and channels.
3. Issue a De-Select Package command to all the channels.
4. Set active_package to 0x0 (or the lowest existing package ID).
5. At the beginning of each time slot the BMC should:
     a. Issue a De-Select Package to the active_package. The BMC must then wait for a response and
        then an additional timeout for the package to become de-selected (200 s). See the NC-SI
        specification table 10 — parameter NC Deselect to Hi-Z Interval.
     b. Find the next available package (typically active_package = active_package + 1).
     c. Issue a Select Package command to active_package.

#### 11.6.7.3 Multiple Channels (Fail-Over)

To support a fail-over scenario, it is required from the BMC to operate two or more channels. These
channels might or might not be in the same package.
The key element of a fault-tolerance fail-over scenario is having two (or more) channels identifying to
the switch with the same MAC Address, but only one of them being active at any given time (such as
switching the MAC Address between channels). To accomplish this, NC-SI provides the following
commands:

333369-009                                                                                            1081
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                            System Manageability

1. Enable Network Tx command — This command enables shutting off the network transmit path of a
   specific channel. This enables the BMC to configure all the participating channels with the same
   MAC Address but only enable one of them.
2. Link Status Change AEN or Get Link Status command.

11.6.7.3.1              Fail-Over Algorithm Example

The following is a sample workflow for a fail-over scenario for the X550 Quad-port 10 GbE controller
(one package and four channels):
1. BMC initializes and configures all channels after power-up. However, the BMC uses the same MAC
   Address for all of the channels.
2. The BMC queries the link status of all the participating channels. The BMC should continuously
   monitor the link status of these channels. This can be accomplished by listening to AENs (if used)
   and/or periodically polling using the Get Link Status command.
3. The BMC then only enables channel 0 for network transmission.
4. The BMC then issues a gratuitous ARP (or any other packet with its source MAC Address) to the
   network. This packet informs the switch that this specific MAC Address is registered to channel 0's
   specific LAN port.
5. The BMC begins normal workflow.
6. Should the BMC receive an indication (AEN or polling) that the link status for the active channel
   (channel 0) has changed, the BMC should:
       a. Disable channel0 for network transmission.
       b. Check if a different channel is available (link is up).
       c. If found:
           1. Enable network Tx for that specific channel.
           2. Issue a gratuitous ARP (or any other packet with its source MAC Address) to the network.
              This packet informs the switch that this specific MAC Address is registered to channel 0's
              specific LAN port.
           3. Resume normal workflow.
           4. If not found, report the error and continue polling until a valid channel is found.
The above algorithm can be generalized such that the start-up and normal workflow are the same. In
addition, the BMC might need to use a specific channel (such as channel 0). In this case, the BMC
should switch the network transmit to that specific channel as soon as that channel becomes valid (link
is up).
Recommendations:
 • Wait for a link-down-tolerance timeout before a channel is considered invalid. For example, a link
   re-negotiation might take a few seconds (normally 2 to 3 or might be up to 9). Thus, the link must
   be re-established after a short time.
 • Typically, this timeout is recommended to be three seconds.
 • Even when enabling and using AENs, periodically poll the link status, as dropped AENs might not be
   detected.

1082                                                                                                  333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.6.7.4 Statistics

The BMC might use the statistics commands as defined in NC-SI. These counters are meant mostly for
debug purposes and are not all supported.
The statistics are divided into three commands:
1. Controller statistics — These are statistics on the network interface (to the host operating system
   and the pass-through traffic). See the NC-SI specification for details.
2. NC-SI statistics — These are statistics on the NC-SI control frames (such as commands, responses,
   AENs, etc.). See the NC-SI specification for details.
NC-SI pass-through statistics — These are statistics on the NC-SI pass-through frames. See the NC-SI
specification for details.

### 11.6.8 External Link Control via NC-SI

The BMC can use the NC-SI Set Link command to control the external interface link settings. This
command enables the BMC to set the auto-negotiation, link speed, duplex, and other parameters.
This command is only available when the host operating system is not present. Indicating the host
operating system status can be obtained via the Get Link Status command and/or Host OS Status
Change AEN command.
Recommendation:
 • Unless explicitly needed, it is not recommended to use this feature. The NC-SI Set Link command
   does not expose all the possible link settings and/or features. This might cause issues under
   different scenarios. Even if you decided to use this feature, use it only if the link is down (trust the
   X550 until proven otherwise).
 • It is recommended that the BMC first query the link status using the Get Link Status command. The
   BMC should then use this data as a basis and change only the needed parameters when issuing the
   Set Link command.
For details, refer to the NC-SI specification.

#### 11.6.8.1 Set Link While LAN PCIe Functionality is Disabled

In cases where the X550 is used solely for manageability and its LAN PCIe function is disabled, using
the NC-SI Set Link command while advertising multiple speeds and enabling auto-negotiation results in
the lowest possible speed chosen.
To enable link of higher a speed, the BMC should not advertise speeds that are below the desired link
speed, as the lowest advertised link speed is chosen.
When the X550 is only used for manageability and the link speed advertisement is configured by the
BMC, changes in the power state of the LAN device is not effected and the link speed is not
re-negotiated by the LAN device.

333369-009                                                                                             1083
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

#### 11.6.8.2 Set Link Error Codes

The following rules are used to define the error code returned for Set Link command in case an invalid
configuration is requested:
1. Host Driver Check: If host device driver is present, return a Command Specific Response (0x9) with
   a Set Link Host OS/Driver Conflict Reason (0x1).
2. Speed Present Check: If no speed is selected, return a General Reason Code for a failed command
   (0x1) with Parameter Is Invalid, Unsupported, or Out-of-Range Reason (0x2).
3. Parameter Validity:
       a. Auto-Negotiation Parameter Validation: If auto-negotiation is requested and none of the selected
          parameters are valid for the device, return a General Reason Code for a failed command (0x1)
          with a Parameter Is Invalid, Unsupported, or Out-of-Range Reason (0x2).
          Note:     This means that, for example, a command requesting 10 GbE on a 1 GbE device
                    succeeds provided that the command requests at least one other supported speed.
          The same goes for an unsupported duplex setting (a device with no HD support accepts a
          command with both FD and HD set), and also for HD being requested with speeds of 1 GbE and
          higher as long as a speed below 1 GbE is also requested (and is supported in HD). The device
          simply ignores the unsupported parameters.
       b. Force Mode Parameter Validation:
           • If more than one link speed is being forced, return a General Reason Code for a failed
             command (0x1) and a Command Specific Reason with a Set Link Speed Conflict Error
             (0x0905).
           • If more than one duplex setting is being forced, return a General Reason Code for a failed
             command (0x1) with Parameter Is Invalid, Unsupported, or Out-of-Range Reason (0x2).
           • If 1 GbE and above is requested with HD, return a General Reason Code for a failed
             command (0x1) and a Command Specific Reason with Set Link Parameter Conflict Reason
             (0x0903).
4. Media Type Compatibility Check: If current media type is not compatible for the requested link
   parameters, return a General Reason Code for a failed command (0x1) and a Command Specific
   Reason with Set Link Media Conflict Error (0x0902).
5. Power State Compatibility Check: If current power state does not allow for the requested link
   parameters, return a General Reason Code for a failed command (0x1) and a Command Specific
   Reason with Set Link Power Mode Conflict Reason (0x0904).
6. If for some reason the hardware cannot perform the flow required for the command, return a
   General Reason Code for a failed command (0x1) and a Command Specific Response (0x9) with
   Link Command Failed-Hardware Access Error (0x6).

#### 11.6.8.3 Support for 2.5 and 5 Gb/s Speeds

As the Set Link and Get Link commands do not support the proprietary 2.5 and 5 Gb/s speeds, the
following behavior is defined:
 • A Get Link response returns a speed indication of 1 Gb/s if a speed of 2.5 or 5 Gb/s was negotiated.
 • There is no way to request a specific speed of 2.5 or 5 Gb/s in a Set Link command.
 • If both 1 Gb/s and 10 Gb/s are requested in the auto-negotiation, 2.5 and 5 Gb/s are also enabled.

1084                                                                                                 333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability
