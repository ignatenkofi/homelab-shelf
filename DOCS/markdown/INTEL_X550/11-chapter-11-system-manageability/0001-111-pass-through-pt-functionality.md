## 11.1 Pass-Through (PT) Functionality

Pass-Through (PT) is the term used when referring to the process of sending and receiving Ethernet
traffic over the sideband interface. The X550 has the ability to route Ethernet traffic to the host
operating system as well as the ability to send Ethernet traffic over the sideband interface to an
external BMC. See Figure 11-1.

                                                             Host

                                                                    Host
                                                                  Interface
                                                                          Port 0
                                            Sideband
                                                                          LAN
                                 MC                          NIC        Interface
                                            Interface                     Port 1

Figure 11-1. Sideband Interface

333369-009                                                                                            947
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                         System Manageability

The sideband interface provides a mechanism by which the X550 can be shared between the host and
the BMC. By providing this sideband interface, the BMC can communicate with the LAN without
requiring a dedicated Ethernet controller. The X550 supports three sideband interfaces:
 • SMBus
 • NC-SI
 • PCIe (together with MCTP) - when the system is up.
The usable bandwidth for either direction is up to 1 Mb/s when using SMBus and 100 Mb/s for the NC-SI
interface. When working over PCIe, the bandwidth is limited only by the PCIe bandwidth and the the
X550 processing capabilities and can sustain any network bandwidth. The X550 should support MCTP
over PCIe pass though traffic at a rate of up to 1 Mb/s. Only one mode of sideband can be active at any
given time. The configuration is done using an NVM setting.
The maximal packet size supported for traffic received from the LAN to the BMC is 1518 bytes and
additional VLAN or E-tag. For traffic from the BMC to the LAN the maximal supported packet size is
1536 bytes including all tags.
Note:      In MCTP mode, the PCIe and SMBus interface can receive MCTP commands in parallel.For
           example, the MCTP enumeration process can be done both over SMBus and over PCIe.
           However, only one of the interfaces can receive NC-SI commands or pass-through traffic.

### 11.1.1 Supported Topologies

The X550 can support some management topologies. The following connections are available:
 • Single connection via legacy SMBus (See Section 11.5).
 • Single connection via NC-SI over RMII (See Section 11.6)
 • Single connection via NC-SI over MCTP. This connection can be over SMBus, PCI Express or both.
   This connection can be used either for pass-through or for control only (See Section 11.7).
The topology used is defined in the Redirection Sideband Interface field in the Common Firmware
Parameters NVM word (see Section 6.2.16) and is common to all the ports in the device.

### 11.1.2 Pass-Through Packet Routing

When an Ethernet packet reaches the X550, it is examined and compared to a number of configurable
filters. These filters are configurable by the BMC and include, but not limited to, filtering on:
 • MAC Address
 • IP Address
 • UDP/IP Ports
 • VLAN Tags
 • EtherType
If the incoming packet matches any of the configured filters, it is passed to the BMC. Otherwise it is not
passed.
The packet filtering process is described in Section 11.3.

948                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability
