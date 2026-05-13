## 1.2 Product Overview

The X550 is a derivative of the X540. Many features of its predecessor remain intact; however, some
have been removed or modified as well as new features introduced.
The X550 includes two integrated 10GBASE-T copper Physical Layer Transceivers (PHYs). A standard
MDIO interface, accessible to software via MAC control registers, is used to configure and monitor each
PHY operation.

### 1.2.1 System Configurations

The X550 is targeted for system configurations such as rack mounted, pedestal servers or workstations,
where it can be implemented used as an add-on NIC or LAN on Motherboard (LOM), or purchased from
Intel as a standard PCIe* adapter card.

                                                                  PCIe v3.0 (2.5GT/s, 5GT/s or 8GT/s) x4
                                                                      PCIe v3.0 (2.5GT/s, 5GT/s) x8

                                             SMBus/
                                              NC‐SI                                                                  Flash
                      MC / ME                                MAC (LAN 0)                     MAC (LAN 1)

             MC = Manageability Controller                            MDIO                                 MDIO
              ME = Manageability Engine

                                                                PHY                                PHY

                                                      X550            10GBASE‐T_0                      10GBASE‐T_1

                                                                             Network

Figure 1-1.     Typical Rack/Pedestal System Configuration

333369-009                                                                                                                   35
                                             Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                                        Introduction
