## 11.4 OS-to-BMC Traffic

### 11.4.1 Overview

Traditionally, the communication between a host and the local BMC is not handled through the network
interface and requires a dedicated interface such as an IPMI KCS interface. The X550 allows the host
and the local BMC communication via the regular pass-through interface, and thus allow management
of a local console using the same interface used to manage any BMC in the network.
When this flow is used, the host sends packets to the BMC through the network interface. The X550
examines these packets and then decides if they should be forwarded to the BMC. On the inverse path,
when the BMC sends a packet on the pass-through interface, the X550 checks if it should be forwarded
to the network, the host, or both. Figure 11-3 describes the flow for OS-to-BMC traffic for the NC-SI
over RMII case. OS2BMC is available also when working over MCTP. It is not supported in legacy SMBus
mode.
The OS-to-BMC flow can be enabled using the OS2BMC enable field for the relevant port in the OS 2
BMC configuration structure of the NVM.

                                                                               Aplication

                                                                            Networking stack

                                                                  Port 0                             Port N
                                                                  Driver                             Driver

                                   NC-SI                                           ...
                                  Channel N             Port 0                              Port N

                                     ...
                     MC
                                                                 MNG/host                       MNG/host
                                                                   mux                            mux
                                   NC-SI
                                  Channel 0
                                              Network
                                              Controller

                                                                             External
                                                                             Network

Figure 11-3. OS-to-BMC Diagram

333369-009                                                                                                    963
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                          System Manageability

The OS-to-BMC flow is enabled only for ports enabled by the NC-SI “Enable Channel” command or via
the OS-to-BMC Enable field for the relevant port in the OS-to-BMC configuration structure of the NVM.
When the MC uses IPsec for the flow directed to the host, it should make sure the X550 does not offload
the IPsec flow by exposing the IP Address used via the Set IP Address NC-SI OEM command.
OS2BMC traffic must comply with NC-SI specifications and is therefore limited to maximum sized
frames of 1536 bytes (in both directions).

### 11.4.2 Filtering

When OS-to-BMC traffic is enabled, the filters used for network to BMC traffic are also used for OS-to-
BMC traffic. Traffic considered as exclusive to the BMC (Relevant bit in MNGONLY is set) is also
considered as exclusive to the BMC when sent from the Host and not forwarded to the network.

#### 11.4.2.1 Handling of OS-to-BMC Packets

All the regular transmit offloads are also available for OS-to-BMC packets.

#### 11.4.2.2 BMC-to-OS Filtering

When OS-to-BMC is enabled, as with regular BMC transmit traffic, the port (OS or network) to which
the packet is sent is fixed according to the source MAC Address of the packet. After that, the BMC traffic
is filtered according to the L2 Host filters of the selected port (as described in Section 7.1.2). According
to the results of the filtering the packet can be forwarded to the OS, the network or both.
The following rules apply to the forwarding of OS packets:
 • If BMC to net is disabled, all the traffic from the BMC is sent to the Host.
 • If BMC to host is disabled, all the traffic from the BMC is sent to the network.
 • If both BMC to net and BMC to host are enabled, the packet is forwarded only according to the
   destination MAC Address and VLAN tag. Unicast packets that matches one of the exact filters (RAH/
   RAL) are sent only to the Host. Other packets that pass the L2 Host filtering are sent to both the
   Host and the network. Packets that do not pass the L2 host filtering are sent only to the network.
Note:     In virtualization mode, if packet is received by host only due to default pooling
          (PFVTCTL.DIS_DEF_POOL bit is cleared), it is not sent to the host (even if BMC to net is
          disabled).

#### 11.4.2.3 Queuing of Packets Received from the BMC

Packets received from the BMC are queued in the default queue.

#### 11.4.2.4 Offloads of Packets Received from the BMC

Packets received from the BMC and forwarded to the OS do not pass the same path as regular network
packets. Thus parts of the offloads provided for the network packets are not available for the BMC
packets. Packet received from the BMC are identified by the RDESC.STATUS.BMC bit.

964                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

The following list describes which offloads are available for BMC packets:
 • CRC is checked and removed on the BMC packets.
 • The BMC packets are not detected as time sync packet. The RDESC.STATUS.TS is always clear for
   these packets.
 • In systems where the double VLAN feature is enabled (CTRL_EXT.EXTENDED_VLAN is set), the
   VEXT bit is valid for BMC packets and reflects the presence of a tag with an EtherType matching the
   value in EXVET register.
    Note:        In systems that uses double VLAN, the BMC is expected to send all packets (apart from
                 NC-SI commands) with the outer VLAN included. Failing to do so may cause corruptions
                 to the packet received by the OS
 • The RDESC.ERRORS field is always cleared for these packets.
    Note:        Traffic sent from the BMC does not cause a PME event, even if it matches one of the
                 wake-up filters set by the port.

### 11.4.3 Blocking of Network to BMC Flow

In some systems the BMC may have its own private connection to the network and may use the X550
port only for the OS-to-BMC traffic. In this case, the BMC to network flow should be blocked while
enabling the OS-to-BMC and OS to network flows.
This can be done by clearing the MANC.EN_BMC2NET bit for the relevant port. The BMC can control this
functionality using the “Enable Network to BMC flow” and “Disable Network to BMC flow” NC-SI OEM
commands. This can also be controlled using the Network to BMC disable field in the NVM “OS2BMC
Configuration Structure”.
Notes:       When network to BMC flow is blocked and OS-to-BMC flow is enabled, all the traffic from the
             BMC is sent to the OS without any check. The OS traffic filtering is still done using the regular
             decision filters.
             The NC-SI channel should not be enabled for receive or transmit before at least one of the
             EN_BMC2NET or EN_BMC2OS fields is set, unless used for AEN transmissions only. In this
             case, the channel may be enabled for receive, but all receive filters should be cleared.

### 11.4.4 OS2BMC and Flow Control

The traffic between the host and manageability uses the same buffers as any loopback traffic. Thus it
flows through the transmit buffer and then through the receive buffer. If the transmit buffer is flow
controlled, the host to BMC traffic is also stopped. If the receive buffer is full, the traffic is dropped or
the transmit is stopped according to the flow control policy of this traffic class.
Packets received to the manageability (either from host or from network) may be dropped if the
manageability internal buffers are full.

333369-009                                                                                                 965
                                  Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

### 11.4.5 Statistics

Packets sent from the OS to the BMC should be counted by all statistical counters as packets sent by
the OS. If they are sent to both the network and to the BMC, they are counted once.
Packets sent from the BMC to the host are counted as packets received by the host. If they are sent to
the host and to the network, they are counted both as received packets and as packet transmitted to
the network.
In addition, the X550 supports the following statistical counters that measure just the BMC-to-OS and
OS-to-BMC traffic:
 • O2BGPTC: OS-to-BMC packets received by BMC
 • O2BSPC: OS-to-BMC packets transmitted by OS and received by manageability buffer.
 • B2OSPC: BMC-to-OS packets sent by BMC
 • B2OGPRC: BMC-to-OS packets received by OS.
The driver can use these statistics to count packets dropped by the X550 during the transfer between
the OS and the BMC or the LAN and the BMC as follows:
 • Dropped packets in BMC-to-OS path = B2OSPC - B2OGPRC
 • Dropped packet in BMC to LAN path = B2OSDPC - (B2OSPC - B2OGPRC)
 • Dropped packets in OS-to-BMC path = O2BSPC - O2BGPTC
 • Dropped packets in LAN to BMC path = MNGPDC
See Section 7.1.7.2 and Section 7.1.5.2 for details of the statistics hierarchy.

### 11.4.6 OS-to-BMC Enablement

The X550 supports the unified network software model for OS-to-BMC traffic, where the OS-to-BMC
traffic is shared with the regular traffic. In this model, there is no need for a special configuration of the
OS networking stack or the BMC stack. However, if the link is down, the OS-to-BMC communication is
stopped.
To enable OS-to-BMC, either:
 • Enable OS2BMC in the Port Traffic Type field in the Traffic Type Parameters NVM word for the
   relevant port.
 • Send an Enable Network to BMC Command
Note:     When OS2BMC is enabled, OS must avoid sending packets longer than 1.5 KB to BMC.

966                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability
