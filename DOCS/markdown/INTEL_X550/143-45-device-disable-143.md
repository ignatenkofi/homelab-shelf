## 4.5 Device Disable

### 4.5.1 Overview

To disable the device, both LANx_DIS_N signals should be tied statically to low. When sampled at a
power-on reset, PCIe reset, or in-band reset, the X550 is disabled. It is held in reset and power-down
mode (some clocks are still running), and digital I/O pins are at High-Z if DEV_FUNC_EN.DEV_OFF_EN
bit was set in NVM Control Word 1. As an example, digital I/O pins are in an electrical off state where
pull-up/pull-down resistors are at their defined values. The manageability interface is also disabled in
this state.

333369-009                                                                                            155
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   Initialization

### 4.5.2 BIOS Disable of the Device at Boot Time by Using

                 the Strapping Option
Assume that following a power-up sequence LANx_DIS_N signals are driven high.
1. PCIe is established following the PCIe reset.
2. BIOS recognizes that the X550 should be disabled.
3. The BIOS drives the LANx_DIS_N signals to the low level.
4. BIOS issues a PCIe reset or an in-band PCIe reset.
5. As a result, the X550 samples the LANx_DIS_N signals and disables the LAN ports and the PCIe
   connection.
6. Re-enable can be done by driving high at least one of the LANx_DIS_N signals and then issuing a
   PCIe reset to restart the device.
