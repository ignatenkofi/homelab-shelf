## 13.8 Connecting Miscellaneous Signals

### 13.8.1 LAN Disable

The X550 has two signals that can be used for disabling Ethernet functions from system BIOS.
LAN0_DIS_N and LAN1_DIS_N are the separated port disable signals. Each signal can be driven from a
system output port. Choose outputs from devices that retain their values during reset. For example,
some PCH GPIO outputs transition high during reset. It is important not to use these signals to drive
LAN0_DIS_N or LAN1_DIS_N because these inputs are latched upon the rising edge of PE_RST_N or an
in-band reset end.
A LAN port can also be disabled through Flash settings. See Section 4.4 for details. Note that setting
the Flash LAN_PCI_DIS bit does not bring the PHY into power down.

Table 13-3. PCI Functions Mapping (Legacy Mode)
                    PCI Function #                  LAN Function Select          Function 0               Function 1

    0 LAN 0                    LAN

Both LAN functions are enabled

    1 LAN 1                    LAN

LAN 0 is disabled                                            x                      LAN 1                   Disable

LAN 1 is disabled                                            x                      LAN 0                   Disable

Both LAN functions are disabled                    Both PCI functions are disabled. The X550 is in low power mode.

Table 13-4. PCI Functions Mapping (Dummy Function Mode)
                    PCI Function #                  LAN Function Select          Function 0               Function 1

    0 LAN 0                    LAN

Both LAN functions are enabled

    1 LAN 1                    LAN

# 0 Dummy                     LAN

LAN 0 is disabled

    1 LAN 1                   Disable

    0 LAN 0                   Disable

LAN 1 is disabled

# 1 Dummy                     LAN

Both LAN functions are disabled                    Both PCI functions are disabled. The X550 is in low power mode.

When both LAN ports are disabled following a power on reset / LAN_PWR_GOOD / PE_RST_N / in-band
reset, the LAN_DIS_N signals should be tied statically to low. At this state, the X550 is disabled, LAN
ports are powered down, all internal clocks are shut and the PCIe connection is powered down (similar
to L2 state).

333369-009                                                                                                             1155
                                     Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                          Design Considerations and Guidelines

### 13.8.2 BIOS Handling of Device Disable

Assume that in the following power up sequence the LANx_DIS_N signals are driven high (or is already
disabled):
1. PCIe link is established following the PE_RST_N.
2. BIOS recognizes that the X550 should be disabled.
3. BIOS drives the LANx_DIS_N signals to the low level.
4. BIOS issues PE_RST_N or an in-band PCIe reset.
5. As a result, the X550 samples the LANx_DIS_N signals and enters the desired device-disable mode.
6. Re-enable could be done by driving high one of the LANx_DIS_N signals and then issuing a
   PE_RST_N to restart the X550.
