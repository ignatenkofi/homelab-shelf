## 1.4 Feature Summary

Table 1-1 to Table 1-7 list the X550's features in comparison to previous dual-port 10 GbE Ethernet
controllers.

Table 1-1.         Network Features
                              Feature                                       82599                 X540                 X550

 Compliant with the 10 GbE and 1 GbE Ethernet/802.3ap (KX/KX4)
                                                                               Y                    N                     N
 specification

 Compliant with the 10 GbE 802.3ap (KR) specification                          Y                    N                     N

 Compliant with XFI/SFI interface                                              Y                    N                     N

 Compliant with the 1000BASE-BX specification                                  Y                    N                     N

 Full-duplex operation at all supported speeds                                 Y                    Y                     Y

 Half-duplex at 100 Mb/s operation                                             N                    N                     N

# 10 GbE/1 GbE/100 Mb/s copper PHYs integrated on-chip                          N                    Y                     Y

 802.3az Energy Efficient Ethernet (EEE) support                               N                    N                     Y

 Support jumbo frames of up to 15.5 KB                                        Y1                    Y1                   Y1

 MDIO interface Clause 45                                                      Y              Y (internally)        Y (internally)

 Flow Control support: Send/receive pause frames and receive Fifo
                                                                               Y                    Y                     Y
 thresholds

 Statistics for Management and RMON                                            Y                    Y                     Y

 802.1q VLAN support                                                           Y                    Y                     Y

 SerDes interface for external PHY connection or system
                                                                               Y                    N                     N
 interconnect

                                                                              Y
 SGMII interface                                                        (100 Mb/s and               N                     N

# 1 GbE only)

 Double VLAN                                                                   Y                    Y                     Y

1. All the products support full-size 15.5 KB jumbo packets while in a basic mode of operation. When DCB mode is enabled, or security
   engines enabled, or virtualization is enabled, or OS2BMC is enabled, then only 9.5 KB jumbo packets are supported. Packets to/
   from the MC longer than 2 KB are filtered out.

38                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Introduction

Table 1-2.         Host Interface Features
                                Feature                                 82599                 X540              X550

                                                                       PCIe v2.0           PCIe v2.1          PCIe v3.0
 PCIe* version (Speed)
                                                                      (5/2.5 GT/s)        (5/2.5 GT/s)      (8/5/2.5 GT/s)

                                                                                                                 x1, x4
 Number of lanes                                                     x1, x2, x4, x8       x1, x2, x4, x8   x8 (For X550-BT2,
                                                                                                             x8 available in
                                                                                                             Gen 1/2 only)

 64-bit address support for systems using more than 4 GB of
                                                                           Y                    Y                  Y
 physical memory

 Outstanding requests for Tx data buffers                                 16                   16                 16

 Outstanding requests for Tx descriptors                                   8                    8                  8

 Outstanding requests for Rx descriptors                                   8                    8                  8

 Credits for P-H/P-D/NP-H/NP-D (shared for the two ports)              16/16/4/4           16/16/4/4          16/16/4/4

 Max Payload Size supported                                            512 Bytes           512 Bytes          512 Bytes

 Max Request Size supported                                              2 KB                 2 KB               2 KB

 Link layer retry buffer size (shared for the two ports)                3.4 KB               3.4 KB             3.4 KB

 Vital Product Data (VPD)                                                  Y                    Y                  Y

 End to End CRC (ECRC)                                                     Y                    Y                  Y

 TLP Processing Hints (TPH)                                                N                    N                  Y

 Latency Tolerance Reporting (LTR)                                         N                    N                  Y

 ID-Based Ordering (IDO)                                                   N                    N                  Y

 Access Control Services (ACS)                                             N                    Y                  Y

 ASPM optional compliance capability                                       N                    Y                  Y

 PCIe functions off via pins, while LAN ports are on                       N                    Y                  Y

Table 1-3.         Miscellaneous Features
                                Feature                                 82599                 X540              X550

 Serial Flash Interface (SFI)                                              Y                    Y                  Y

 4-wire SPI EEPROM interface                                               Y                    N                 N

 Configurable LED operation for software or OEM customization of
                                                                           Y                    Y                  Y
 LED displays

 Protected NVM Space for Private Configuration                             Y                    Y                  Y

 Device disable capability                                                 Y                    Y                  Y

                                                                                                           25 mm x 25 mm
 Package size                                                       25 mm x 25 mm     25 mm x 25 mm
                                                                                                           17 mm x 17 mm

 Embedded thermal sensor                                                   N                    Y                  Y

 Embedded thermal diode                                                    N                    Y                  Y

 Watchdog timer                                                            Y                    Y                  Y
                                                                                                 1
 Time Sync (IEEE 1588)                                                     Y                   Y                   Y

 Time Stamp in packet                                                      N                    N                  Y

1. Time sync not supported at 100 Mb/s link speed.

333369-009                                                                                                                   39
                                          Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                   Introduction

Table 1-4.       LAN Functions Features
                              Feature                                    82599                  X540               X550

Programmable host memory receive buffers                                    Y                     Y                  Y

Descriptor ring management hardware for transmit and receive                Y                     Y                  Y

ACPI register set and power down functionality supporting D0 and
                                                                            Y                     Y                  Y
D3 states

Integrated IPsec security engines: AES-GCM 128-bit; AH or ESP
                                                                     1024 SA / port         1024 SA / port     1024 SA / port
encapsulation; IPv4 and IPv6 (no option or extension headers)

Software-controlled global reset bit (resets everything except the
                                                                            Y                     Y                  Y
PCIe configuration registers)

Software-Definable Pins (SDP) (per port)                                    8                     4                  4

Four SDP Pins can be configured as general purpose interrupts               Y                     Y                  Y

Wake on LAN (WoL)                                                           Y                     Y                  Y

IPv6 Wake-up Filters                                                        Y                     Y                  Y

Configurable (through NVM) Wake-up Flexible Filters                         Y                     Y                  Y

Default configuration by NVM for all LEDs for pre-driver
                                                                            Y                     Y                  Y
functionality

LAN Function Disable capability                                             Y                     Y                  Y

Programmable memory transmit buffers                                  160 KB / port         160 KB / port      160 KB / port

Programmable memory receive buffers                                   512 KB / port         384 KB / port      384 KB / port

Table 1-5.       LAN Performance Features
Feature                                                                  82599                  X540               X550

                                                                      256 KB in all          256 KB in all      256 KB in all
TCP/UDP segmentation offload
                                                                        modes                  modes              modes

TSO interleaving for reduced latency                                        Y                     Y                  Y

TCP Receive Side Coalescing (RSC)                                    32 flows / port        32 flows / port    32 flows / port

Data Center Bridging (DCB), IEEE Compliance to:
 • Enhanced Transmission Selection (ETS) - 802.1Qaz                    Y (up to 8)           Y (up to 8)         Y (up to 8)
 • Priority-based Flow Control (PFC) - 802.1Qbb                        Y (up to 8)           Y (up to 8)         Y (up to 8)

Rate limit VM Tx traffic per TC (i.e. per TxQ)                              Y                     Y                  Y

IPv6 support for IP/TCP and IP/UDP receive checksum offload                 Y                     Y                  Y

Fragmented UDP checksum offload for packet reassembly                       Y                     Y                  Y

FCoE Tx / Rx CRC offload                                                    Y                     Y                  Y

FCoE transmit segmentation                                               256 KB                256 KB             256 KB

                                                                     512 outstanding       512 outstanding    2048 outstanding
                                                                       Read — Write          Read — Write       Read — Write
FCoE coalescing and direct data placement                             requests / port       requests / port    requests / port
                                                                     256 buffers per       256 buffers per    1024 buffers per
                                                                         request               request            request

Message Signaled Interrupts (MSI)                                           Y                     Y                  Y

Message Signaled Interrupts (MSI-X)                                         Y                     Y                  Y

Interrupt Throttling Control to limit maximum interrupt rate and
                                                                            Y                     Y                  Y
improve CPU use

Rx packet split header                                                      Y                     Y                  Y

40                                                                                                                  333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Introduction

Table 1-5.         LAN Performance Features [continued]
Feature                                                                   82599               X540               X550

                                                                              Y                  Y                  Y
Multiple Rx queues (RSS)
                                                                      (multiple modes)   (multiple modes)   (multiple modes)

Flow Director Filters: up to 32 KB flows by hash filters or up to 8
                                                                             Y                  Y                  Y
KB perfect match filters

Number of Rx queues (per port)                                              128                128                128

Number of Tx queues (per port)                                              128                128                128

Low Latency Interrupts (LLI)                                                 Y                  Y                  N

DCA support                                                                  Y                  Y                  N

TCP timer interrupts                                                         Y                  Y                  Y

No snoop                                                                     Y                  Y                  N

Relax ordering                                                               Y                  Y                  Y

DMA coalescing                                                               N                  N                  Y

Table 1-6.         Virtualization Features
                               Feature                                    82599               X540               X550

Support for Virtual Machine Device Queues (VMDq1 and Next
                                                                            64                 64                 64
Generation VMDq)

L2 Ethernet MAC Address filters (unicast and multicast)                     128                128                128

L2 VLAN filters                                                             64                 64                 64

PCI-SIG SR IOV                                                               Y                  Y                  Y

RSS table per VF                                                             N                  N                  Y

Traffic shaping                                                              Y                  Y                  Y

                                                                                                              MAC, VLAN,
Anti-spoof                                                              MAC, VLAN          MAC, VLAN
                                                                                                               EtherType

Malicious driver protection                                                  N                  N                  Y

Forwarding modes                                                        MAC, VLAN          MAC, VLAN        MAC, VLAN, E-tag

VEB support
 • Multicast and broadcast packet replication                                Y                  Y                  Y
 • Packet mirroring                                                          Y                  Y                  Y
 • Packet loopback                                                           Y                  Y                  Y

VEPA support (on top of VEB support)
 • Source pruning                                                            N                  N                  Y

E-tag filtering support                                                      N                  N                  Y

333369-009                                                                                                                 41
                                         Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                          Introduction

Table 1-7.           Manageability Features
                            Feature                                 82599              X540              X550

Advanced pass-through-compatible management packet transmit/          Y                  Y                 Y
receive support

SMBus interface to an external MC                                     Y                  Y                 Y

New Management Protocol Standards Support (NC-SI) interface to        Y                  Y                 Y
an external MC

L2 address filters                                                    4                  4                 4

VLAN L2 filters                                                       8                  8                 8

Flex L3 port filters                                                  16                16                 16

Flexible TCO filters                                                  4                  4                 1

L3 address filters (IPv4)                                             4                  4                 4

L3 address filters (IPv6)                                             4                  4                 4

Host-based Application-to-BMC Network Communication patch             N                  Y                 Y
(OS2BMC)

Flexible MAC Address                                                  N                  Y                 Y

MC inventory of LOM device information                                N                  Y                 Y

iSCSI boot configuration parameters via MC                            N                  Y                 Y

MC monitoring                                                         N                  Y                 Y

NC-SI to iMC                                                          N                  Y                 Y

NC-SI arbitration                                                     N                  Y                  Y

MCTP over SMBus (pass-through and control)                            N           Y (control only)          Y

MCTP over PCIe (pass-through and control)                             N                  N                  Y

NC-SI package ID via SDP pins                                         N                  Y                  Y

NC-SI Flow control                                                    N                  N                  Y

42                                                                                                         333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Introduction
