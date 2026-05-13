## 4.4 Function Disable

### 4.4.1 General

For a LAN on Motherboard (LOM) design, it might be desirable for the system to provide BIOS-setup
capability for selectively enabling or disabling LAN functions. It enables end users more control over
system resource-management and avoids conflicts with add-in NIC solutions. The X550 provides
support for selectively enabling or disabling one or both LAN device(s) in the system.

### 4.4.2 Overview

Device presence (or non-presence) must be established early during BIOS execution, to ensure that
BIOS resource-allocation (of interrupts, of memory or IO regions) is done according to devices that are
present only. This is frequently accomplished using a BIOS Configuration Values Driven on Reset
(CVDR) mechanism. The X550’s. LAN-disable mechanism is implemented to be compatible with such a
solution.
The X550 provides three mechanisms to disable LAN ports and/or PCIe functions:
 • The LANx_DIS_N pins (one pin per LAN port) are sampled on reset to determine the LAN
   enablement.
 • One of the LAN ports can be disabled using a NVM configuration.
 • Both SDP1 pins are sampled on reset to determine (electrical) disablement of both PCIe functions.
   If the MC is present, LAN ports are still available for manageability purposes.
Disabling a LAN port affects the PCI function it resides on. When function 0 is disabled (either LAN0 or
LAN1), it does not disappear from the PCIe configuration space. Rather, the function presents itself as a
dummy function. The device ID and class code of this function changes to other values (dummy
function device ID 0x10A6, class code 0xFF0000). In addition, the function does not require any I/O
space, and does not require an interrupt line. It requires a minimal memory space (4K) that is not
mapped to internal registers.
Mapping between function and LAN ports is listed in Table 4-8.

Table 4-8.       PCI Functions Mapping
                     PCI Function #                  LAN Function Select           Function 0               Function 1

Both LAN functions are enabled.                                0                      LAN 0                    LAN 1

    1 LAN 1                    LAN

LAN 0 is disabled.                                             0                     Dummy                     LAN1

    1 LAN 1                   Disable

LAN 1 is disabled.                                             0                      LAN 0                   Disable

# 1 Dummy                     LAN

Both LAN functions are disabled.                     Both PCI functions are disabled. Device is in low-power mode.

The following rules apply to function disable:
 • When function 0 is disabled, it is converted into a dummy PCI function. Function 1 is not affected.
 • When function 1 is disabled, it disappears from the PCI configuration space.

152                                                                                                                  333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

 • The disabled LAN port is still available for manageability purposes if disabled through the NVM or
   SDP1 mechanism. In this case, and if the LPLU bit is set, the PHY attempts to create a link at
   100 Mb/s. The disabled LAN port is not available for manageability purposes if disabled through the
   LANx_DIS_N pin mechanism. Section 11.2.2.2 and Section 11.5.3 describe the NC-SI channels and
   SMBus ports, respectively, exposed in each mode.
 • Dummy function mode should not be used in PCI IOV mode (since PF0 is required to support certain
   functionality).
The following NVM bits control function disable:
 • One PCI function can be enabled or disabled according to the LAN_PCI_DISABLE field in NVM
   (reflected in DEV_FUNC_EN.LAN_PCI_DISABLE bit).
 • The LAN Disable Select field in NVM (reflected in DEV_FUNC_EN.LAN_DISABLE_SELECT bit)
   indicates which function is disabled.
 • The LAN_FUNCTION_SEL field in NVM (reflected in FACTPS.LAN_FUNCTION_SEL bit) defines the
   correspondence between LAN port and PCI function.
 • The SDP_FUNC_OFF_EN field in NVM (reflected in DEV_FUNC_EN.SDP_FUNC_OFF_EN bit) enables
   the function disable mechanism made via SDP1 pins.
When a particular LAN is fully disabled, all internal clocks to that LAN are disabled, the device is held in
reset, and the internal PHY for that LAN is powered down. In both modes, the device does not respond
to PCI configuration cycles. Effectively, the LAN device becomes invisible to the system from both a
configuration and power consumption standpoint.

### 4.4.3 Control Options

The functions have a separate enabling mechanism. Any function that is not enabled does not function
and does not expose its PCI configuration registers.
LAN0 or LAN1 can be disabled in the NVM by setting the DEV_FUNC_EN.LAN_PCI_DISABLE bit. The
LAN_DISABLE_SELECT in the same register in the NVM selects which LAN is disabled. Furthermore, if
the LAN port at function 0 is disabled, the disabled function is filled by a dummy function.
Note:        Mapping LAN0 and LAN1 to PCI function 0 and PCI function 1 is controlled by the
             FACTPS.LAN_FUNCTION_SEL field.
LAN0 and LAN1 can be disabled on the board level by driving the LAN0_Dis_N or LAN1_Dis_N pins
respectively to low. These I/O pins have weak internal pull up resistors so leaving them unconnected or
driving them to high enable the respective LAN port. These pins are strapping options, sampled at LAN
Power Good, PCIe reset or in-band PCIe reset.
PCIe Functions 0 and 1 can be disabled at the board level by driving SDP0_1 or SDP1_1 pins
respectively high. These I/O pins have weak internal pull-down resistors so leaving them unconnected
or driving them to low enables the PCIe functions. These pins are strapping options, sampled at
PE_RST_N de-assertion. This feature is enabled/disabled via the DEV_FUNC_EN.SDP_FUNC_OFF_EN bit
(set from NVM Control word 2 — Section 6.2.2.2).

333369-009                                                                                               153
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

### 4.4.4 Event Flow for Enable/Disable Functions

This section describes the driving levels and event sequence for device functionality.
Following a power on reset / LAN Power Good/ PCIe reset/ in-band reset the LANx_DIS_N signals
should be driven high (or left open) for normal operation. If any of the LAN functions are not required
statically, its associated disable strapping pin can be tied statically to low.
Following a PCIe reset, the SDP1 pins should be driven low (or left open) for normal operation. If both
PCIe functions are not required statically, the SDP1 strapping pins can be tied statically to high.

#### 4.4.4.1 BIOS Disable of the LAN Function at Boot Time by Using

                    the Strapping Option
Assume that following a power-up sequence LANx_DIS_N signals are driven high.
1. PCIe is established following the PCIe reset.
2. BIOS recognizes that a LAN function in the X550 should be disabled.
3. The BIOS drives the LANx_DIS_N signal to a low level.
4. BIOS issues a PCIe reset or an in-band PCIe reset.
5. As a result, the X550 samples the LANx_DIS_N signals and disables the LAN function and issues an
   internal reset to this function.
6. The BIOS might start with the device enumeration procedure (the disabled LAN function is invisible;
   changed to dummy function).
7. Proceed with normal operation.
8. Re-enable could be done by driving the LANx_DIS_N signal high and then requesting the end user
   to issue a warm boot to initialize new bus enumeration.

#### 4.4.4.2 BIOS Disable of the PCIe Functions at Boot Time by

                    Using the Strapping Option
Assume that following a power-up sequence SDP1 signals are driven low and/or the
SDP_FUNC_OFF_EN bit is cleared.
1. PCIe is established following the PCIe reset.
2. The BIOS recognizes that both PCIe functions in the X550 should be disabled.
3. The BIOS modifies the DEV_FUNC_EN.SDP_FUNC_OFF_EN NVM bit and it might eventually issue an
   in-band PCIe reset that causes the X550 to auto-load the PCIe general configuration from the NVM.
4. The BIOS drives the two SDP1 signals to a high level.
5. The BIOS issues a PCIe reset (via PE_RST_N).
6. The system reboots.
7. PE_RST_N might toggle a couple of times during POST, before its last de-assertion.
8. As a result, the X550 samples the SDP1 signals and disables the two PCIe functions.
9. The BIOS might start with the device enumeration procedure (the disabled PCIe function is invisible
   and PCIe lanes are electrically off).

154                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

#### 4.4.4.3 Multi-Function Advertisement

If one of the LAN devices is disabled and function 0 is the only active function, the X550 is no longer a
multi-function device. The X550 normally reports 0x80 in the PCI Configuration Header field (Header
Type), indicating multi-function capability. However, if a LAN is disabled and only function 0 is active,
the X550 reports 0x0 in this field to signify single-function capability.

#### 4.4.4.4 Interrupt Use

When both LAN devices are enabled, the X550 uses the PCI legacy interrupts of both ports for interrupt
reporting. The NVM configuration controls the Interrupt Pin field of the PCI configuration header to be
advertised for each LAN device to comply with PCI specification requirements.
However, if either LAN device is disabled, the legacy PCI interrupt of port A must be used for the
remaining LAN device, therefore the NVM configuration must be set accordingly. Under these
circumstances, the Interrupt Pin field of the PCI header always reports a value of 0x1, indicating INTA#
pin usage, which means legacy PCI interrupt of port A is used.

#### 4.4.4.5 Power Reporting

When both LAN devices are enabled, the PCI Power Management register block has the capability of
reporting a common power value. The common power value is reflected in the Data field of the PCI
Power Management registers. The value reported as common power is specified via an NVM field, and is
reflected in the Data field each time the Data_Select field has a value of 0x8 (0x8 = common power
value select).
When only one LAN port is enabled and the X550 appears as a single-function device, the common
power value, if selected, reports 0x0 (undefined value), as common power is undefined for a single-
function device.
