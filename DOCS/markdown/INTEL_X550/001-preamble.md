---
title: INTEL X550 DS
source: INTEL_X550_DS.pdf
format: auto-extracted from PDF via pdftotext -layout, post-processed
---

Intel® Ethernet Controller X550
Datasheet

Ethernet Products Group (EPG)

PRODUCT FEATURES

General                                                          Host Interface
 Serial Flash interface                                          PCIe 3.0 Base Specification
  •    Firmware authentication on update                          Bus width — x1, x4, x8
 Configurable LED operation for software or customizing OEM      64-bit address support for systems using more than 4 GB of
  LED displays                                                     physical memory
 Device disable capability
 Package sizes                                                  MAC Functions
  •    25 mm x 25 mm (X550-BT2)
  •    17 mm x 17 mm (X550-AT2)                                   Descriptor ring management hardware for transmit and
                                                                   receive
                                                                  ACPI register set and power down functionality supporting
Networking                                                         D0 and D3 states
 10 GbE/1 GbE/100 Mb/s copper PHYs integrated on-chip            A mechanism for delaying/reducing transmit interrupts
 Support for jumbo frames of up to 15.5 KB                       Software-controlled global reset bit (resets everything
 Flow control support: send/receive pause frames and receive      except the configuration registers)
  FIFO thresholds                                                 Four Software-Definable Pins (SDP) per port
 Statistics for management and RMON                              Wake up
 802.1q VLAN support                                             IPv6 wake-up filters
 TCP segmentation offload: up to 256 KB                          Configurable flexible filter (through NVM)
 IPv6 support for IP/TCP and IP/UDP receive checksum             LAN function disable capability
  offload                                                         Programmable memory transmit buffers (160 KB/port)
 Fragmented UDP checksum offload for packet reassembly           Default configuration by NVM for all LEDs for pre-driver
 Message Signaled Interrupts (MSI)                                functionality
 Message Signaled Interrupts (MSI-X)
 Interrupt throttling control to limit maximum interrupt rate   Manageability
  and improve CPU usage
 Flow Director (16 x 8 and 32 x 4)                               SR-IOV support
 128 transmit queues                                             Eight VLAN L2 filters
 Receive packet split header                                     16 Flex L3 port filters
 Receive header replication                                      Four Flexible TCO filters
 Dynamic interrupt moderation                                    Four L3 address filters (IPv4)
 TCP timer interrupts                                            Advanced pass through-compatible management packet
 Relaxed ordering                                                 transmit/receive support
 Support for 64 virtual machines per port (64 VMs x 2            SMBus interface to an external Manageability Controller (MC)
  queues)                                                         NC-SI interface to an external MC
 Support for Data Center Bridging (DCB);(802.1Qaz,               Four L3 address filters (IPv6)
  802.1Qbb, 802.1p)                                               Four L2 address filters

                                                                                                        Revision 2.7
                                                                                                          July 2023
                                                                                                        333369-009

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                            Revision History

Revision History

    Revision         Date                                                      Notes
