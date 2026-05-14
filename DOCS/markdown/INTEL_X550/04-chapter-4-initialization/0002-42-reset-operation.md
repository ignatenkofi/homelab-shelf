## 4.2 Reset Operation

### 4.2.1 Reset Sources

The X550 reset sources are described in the sections that follow. Figure 4-4 and Figure 4-5 describes
the hierarchy between the different reset causes.

                    Firmware Reset                     Power On Reset

                   Management Core                     LAN Power Good
                        Reset                               Reset              PE_RST_N
                                                                               assertion

                                     PCIe link down,         PCIe Power Good
                                     PCIe Hot Reset               Reset

                                                                  PCIe Core Reset          Common
                                                                  (Inband Reset)

Figure 4-4.   Reset Tree (Common)

142                                                                                                      333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

               LAN Power Good
                    Reset

                                               FLR                        PCIE Config Reset   Per Port

                              D3‐>D0
                                                     Per port Reset

                            Low Power Active
                           (MNG/WoL/Proxy)
                                                     1                0

         Soft Link Reset
                                                                           SW Reset

                                                          Low Power not
                                                              Active

             PHY Reset                  MAC Reset                              Master Reset

Figure 4-5.      Reset Tree (per Port)

#### 4.2.1.1 LAN_PWR_GOOD

The X550 has an internal mechanism for sensing power pins. Once power is up and stable, the X550
creates an internal reset, which acts as a master reset of the entire chip. It is level sensitive, and while
it is 0b, all of the registers are held in reset. LAN_PWR_GOOD is interpreted to be an indication that
device power supplies are all stable. Note that LAN_PWR_GOOD changes state during system power-
up.

#### 4.2.1.2 PE_RST_N (PCIe Reset)

De-asserting PCIe reset indicates that both the power and the PCIe clock sources are stable. This pin
also asserts an internal reset after a D3cold exit. Most units are reset on the rising edge of PCIe reset.
The only exception is the GIO unit, which is kept in reset while PCIe reset is asserted (level).

333369-009                                                                                               143
                                   Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   Initialization

#### 4.2.1.3 In-Band PCIe Reset

The X550 generates an internal reset in response to a physical layer message from PCIe or when the
PCIe link goes down (entry to a polling or detect state). This reset is equivalent to PCI reset in previous
PCI Gigabit Ethernet (GbE) controllers.

#### 4.2.1.4 D3hot to D0 Transition

This is also known as ACPI reset. The X550 generates an internal reset on the transition from D3hot
power state to D0 (caused after configuration writes from a D3 to D0 power state). Note that this reset
is per function and resets only the function that transitions from D3hot to D0 and do not reset the
config space of the function. Its effect is equivalent to a software reset (Section 4.2.1.6.1).

#### 4.2.1.5 Function Level Reset (FLR) Capability

The FLR bit is required for the Physical Function (PF) and per Virtual Function (VF). Setting this bit for a
VF only resets the part of the logic dedicated to the specific VF and does not influence the shared part
of the port. Setting the PF FLR bit resets the entire function.

4.2.1.5.1             FLR in Non-IOV Mode

A FLR reset to a function is equivalent to a D0  D3  D0 transition with the exception that this reset
does not require driver intervention to stop the master transactions of this function. FLR affects the
device 1 parallel clock cycle from FLR assertion by default setting, or any other value defined by the FLR
Delay Disable and FLR Delay fields in the PCIe Init Configuration 2 — Offset 0x02 word in the NVM.

4.2.1.5.2             Physical Function FLR (PFLR)

A FLR reset to the PF function in an IOV mode is equivalent to a FLR reset in non-IOV mode. All VFs in
the PCIe function of the PF are affected.
The affected VFs are not notified of the reset in advance. The RSTD bit in VFMailbox[n] is set following
the reset (per VF) to indicate to the VFs that a PF FLR took place. Each VF is responsible to probe this
bit (such as after a timeout).

4.2.1.5.3             Virtual Function FLR (VFLR)

A VF operating in an IOV mode can issue a FLR. VFLR resets the resources allocated to the VF (like
disabling the queues and masking interrupts). It also clears the PCIe configuration for the VF. There is
no impact on other VFs or on the PF.
Tx and Rx flows for the queues allocated to this VF are disabled. All pending read requests are dropped
and PCIe read completions to this function can be completed as unsupported requests.
Note:     Clearing the IOV Enable bit in the IOV structure is equivalent to a VFLR to all VFs in the same
          port.
          A VFLR does not release queues that were blocked due to malicious events. The PF device
          driver needs to release them using the matching bit in WQBR_RX and WQBR_TX registers.
          The matching bits in these registers should be cleared after each VFLR, even if not caused
          due to a malicious event.
Note:     PF driver should clear the VF's VFMBMEM after a VFLR is detected.

144                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

#### 4.2.1.6 Soft Resets

4.2.1.6.1               Software Reset

Software reset is done by writing to the Device Reset bit of the Device Control (CTRL.RST) register. The
X550 re-reads the per-function NVM fields after software reset. Bits that are not normally read from the
NVM are reset to their default hardware values.
Note:        This reset is per function and resets only the function that received the software reset.
PCI configuration space (configuration and mapping) of the device is unaffected. The MAC might or
might not be reset (see Section 4.2.3).
Prior to issuing a software reset, the software driver needs to execute the master disable algorithm as
defined in Section 5.2.4.3.2.
If DCB is enabled, following a software reset the steps below must be executed to prevent potential
races between manageability mapping to TC before and after initialization.
 • Clear the Flow Control enablement in the MAC by clearing the MFLCN.RFCE (or simply clear the
   whole register)
 • Software should waits ~10s
 • The software polls the TFCS.TC_XON[0] = 0 (most of the time it is expected to be found at zero
   while max poll time is always shorted than the max expected PAUSE time before the software reset
   initiated)
 • The software maps the Manageability transmit TC (setting the MNGTXMAP register) and then maps
   the user priority of Manageability traffic to the Manageability TC (setting the RTRUP2TC and
   RTTUP2TC registers)
 • The software waits ~10s
 • The software can re-enable the Flow Control as part of the rest of the init flow

4.2.1.6.2               Physical Function Software Reset

A software reset by the PF in IOV mode has the same consequences as a software reset in a non-IOV
mode.
The procedure for PF software reset is as follows:
 • The PF driver disables master accesses by the device through the master disable mechanism (see
   Section 5.2.4.3.2). Master disable affects all VFs traffic.
 • Execute the procedure described in Section 4.2.2 to synchronize between the PF and VFs.
VFs are expected to timeout and check on the RSTD bit to identify a PF software reset event. The RSTD
bits are cleared on read.

4.2.1.6.3               VF Software Reset

A software reset applied by a VF is equivalent to a FLR reset to this VF with the exception that the PCIe
configuration bits allocated to this function are not reset. It is activated by setting the VTCTRL.RST bit.

333369-009                                                                                               145
                                  Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    Initialization

4.2.1.6.4             Force TCO

This reset is generated when manageability logic is enabled. It is only generated if enabled by the Force
TCO Reset bit in the Common Firmware Parameters word in the NVM. If enabled by the NVM, the
firmware triggers a port reset by setting the CTRL.LRST bit. In pass-through mode it is generated when
receiving a Force TCO SMBus or NC-SI command with bit 0 set.

#### 4.2.1.7 Link Reset

Also referred to as MAC reset.
Initiated by writing the Link Reset bit of the Device Control register (CTRL.LRST).
A link reset is equivalent to a software reset + reset of the MAC + reset of the PHY. The X550 re-reads
the per-function NVM fields after link reset. Bits that are normally read from the NVM are reset to their
default hardware values. Note that this reset is per function and resets only the function that received
the link reset.
The PF in IOV mode can generate a link reset.
Prior to issuing link reset the software driver needs to execute the master disable algorithm as defined
in Section 5.2.4.3.2.

#### 4.2.1.8 PHY Resets

Software can reset each PHY separately via MDIO, by setting the corresponding Soft Reset bit in the
Global Standard Control 1 register. It resets all PHY functionalities expected to PLLs; however, the PHY
image is not reloaded from the NVM.
Software can at once reset a PHY (excluding PLLs) and cause a PHY image reload from the NVM, for
each PHY separately, by setting via MDIO the corresponding PHY Image Reload bit in the Global
Standard Control 1 register.
A PHY reset event causes a link down and restarts the auto-negotiation process. This can take a few
seconds to complete, which might result in drop of the TCP sessions with the host and/or with a
Manageability Controller (MC).Because the PHY can be accessed by the MC (via internal firmware) and
by the driver software concurrently, the driver software should coordinate any PHY reset with the
firmware using the following procedure:
1. Ensure that the MMNGC.MNG_VETO bit is cleared. If it is set, the MC requires a stable link and thus
   the PHY should not be reset at this stage. The software driver can skip the PHY reset (if it is not
   mandatory) or wait for this bit to be cleared by the MC. See Section 5.3.5.2 for more details on
   MNG_VETO bit.
2. Take ownership of the relevant PHY using the flow described in Section 11.8.4.
3. Set the PHY Reset bit in the Global Standard Control 1 register (or bit 0 in PHY register 1E.C442 for
   a PHY Image Reload event).
4. For a PHY reset, wait for 2 s before initiating any MDIO access.
5. For a PHY image re-load and before initiating any MDIO access, do one of the following:
      a. Wait for 100 ms and poll Global Reset Completed bit in PHYINT_STATUS2 register until it is set
         by firmware.
      b. Wait to receive a PHY reset done interrupt.
6. Release ownership of the relevant PHY using the flow described in Section 11.8.4.

146                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

### 4.2.2 Reset in PCI-IOV Environment

Several mechanisms are provided to synchronize reset procedures between the PF and the VFs.

#### 4.2.2.1 RSTI/RSTD

This mechanism is provided specifically for a PF software reset but can be used in other reset cases as
follows.
 • One of the following reset cases takes place:
     — LAN Power Good
     — PCIe reset (PE_RST_N and in-band)
     — D3hot --> D0
     — FLR
     — Software reset by the PF
 • The X550 sets the RSTI bits in all the VFMailbox registers. Once the reset completes, each VF can
   read its VFMailbox register to identify a reset in progress.
     — The VF can poll the RSTI bit to detect if the PF is in the process of configuring the device.
 • Once the PF completes configuring the device, it sets the CTRL_EXT.PFRSTD bit. As a result, the
   X550 clears the RSTI bits in all the VFMailbox registers and sets the Reset Done (RSTD) bits in all
   the VFMailbox registers.
     — The VF might read the RSTD bit to detect that a reset has occurred. The RSTD bit is cleared on
       read.

#### 4.2.2.2 VF Receive Enable (PFVFRE)/VF Transmit Enable

                      (PFVFTE)
This mechanism insures that a VF cannot transmit or receive before the Tx and Rx path have been
initialized by the PF.
 • The PFVFRE register contains a bit per VF. When the bit is set to 0b, assignment of an Rx packet for
   the VF’s pool is disabled. When set to 1b, the assignment of an Rx packet for the VF’s pool is
   enabled.
 • The PFVFTE register contains a bit per VF. When the bit is set to 0b, fetching data for the VF’s pool
   is disabled. When set to 1b, fetching data for the VF’s pool is enabled. Fetching descriptors for the
   VF pool is maintained, up to the limit of the internal descriptor queues — regardless of PFVFTE
   settings.
PFVFTE and PFVFRE are initialized to zero (VF Tx and Rx traffic gated) following a PF reset. The relevant
bits per VF are also initialized by a VF software reset or VFLR.

333369-009                                                                                             147
                                 Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Initialization

### 4.2.3 Reset Effects

The resets listed in Section 4.2.1 affect the following registers and logic:

Table 4-5.        Reset Effects — Common Resets
                                          LAN Power        PCIe                  In-Band           Firmware
            Reset Activation                                                                                        Notes
                                            Good         PE_RST_N               PCIe Reset           Reset

NVM read                                                                   See Section 6.1.3

LTSSM (back to detect/polling)                   X               X                    X

PCIe link data path                              X               X                    X

PCI configuration registers (RO)                 X               X                    X                               8

PCI configuration registers (RW)                 X               X                    X                               8

PCIe local registers                             X

Data path                                        X               X                    X                              2, 7
                                                                     6                   6
MAC, TimeSync                                    X               X                   X

PHY (excluding PLLs)                             X               X6                  X6                              15

PCIe analog, PHY PLLs                            X

Wake-up (PM) Context                             X               1                                                    3

Wake-up/manageability control/status             X                                                                   4, 5
registers

Manageability unit                               X                                                     X

LAN disable strapping pins                       X               X                    X

All other strapping pins                         X

Shadow RAMs in MAC or PHY                        X

Table 4-6.        Reset Effects — per Function Resets
                                                                                          Link Reset     PHY
                                                       FLR or            Software           or Exit     Image
            Reset Activation              D3 or Dr                                                                   Notes
                                                        PFLR              Reset           from LAN     Reload or
                                                                                            Disable    PHY Reset

NVM read                                                                   See Section 6.1.3

LTSSM (back to detect/polling)

PCIe link data path

PCI configuration registers (RO)                                                                                          8

PCI configuration registers (RW)                         X                                                            8, 9

Data path and memory space, TimeSync         X           X                  X                 X                       2, 7
                                                6           16                 16
MAC                                         X           X                  X                  X

    6 X

PHY (excluding PLLs)                        X                                                 X            X           15

Virtual function resources                   X           X                  X                                          10

Wake-up (PM) context                                                                                                      3

Wake-up/manageability control/status                                                                                  4, 5
registers

Manageability unit

148                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

Table 4-6.        Reset Effects — per Function Resets [continued]
                                                                                 Link Reset         PHY
                                                           FLR or     Software     or Exit         Image
             Reset Activation                 D3 or Dr                                                         Notes
                                                            PFLR       Reset     from LAN         Reload or
                                                                                   Disable        PHY Reset

Strapping pins

Shadow RAMs in MAC or PHY

Table 4-7.        Reset Effects — Virtual Function Resets
                                                                                       VF Software
                           Reset Activation                               VFLR                                Notes
                                                                                          Reset

Interrupt registers                                                         X                 X                11

Queue disable                                                               X                 X                12

VF specific PCIe configuration space                                        X                                  13

Data path

Statistics registers                                                                                           14

Notes for Table 4-5 through Table 4-7:
1. If AUX_PWR = 0b the wake-up context is reset (PME_Status and PME_En bits should be 0b at reset
   if the X550 does not support PME from D3cold).
2. The following register fields do not follow the general rules previously described:
      • ESDP registers — Reset on LAN Power Good only.
      • LED configuration registers — Reset on LAN Power Good and on software reset events.
      • The Aux Power Detected bit in the PCIe Device Status register is reset on LAN Power Good and
        PCIe reset only.
      • FLA — Reset on LAN Power Good only.
      • RAH/RAL[n, where n>0], MTA[n], VFTA[n], WUPM[n], FFMT[n], FFVT[n], TDBAH/TDBAL, and
        RDBAH/RDVAL registers have no default value. If the functions associated with these registers
        are enabled they must be programmed by software. Once programmed, their value is
        preserved through all resets as long as power is applied.
      • Statistic registers (physical function)
3. The wake-up context is defined in the PCI Bus Power Management Interface specification (sticky
   bits). It includes:
      • PME_En bit of the Power Management Control/Status Register (PMCSR).
      • PME_Status bit of the PMCSR.
      • Aux_En bit in the PCIe registers.
      • The device requester ID (since it is required for PM_PME TLP).
      • The shadow copies of these bits in the Wake-Up Control (WUC) register are treated identically.
4. Refers to bits in the WUC register that are not part of the wake-up context (the PME_En and
   PME_Status bits). The WUFC register is not part of the wake-up context and is reset as part of the
   data path.

333369-009                                                                                                             149
                                       Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    Initialization

5. The Wake-Up Status (WUS) registers include the following:
      • WUS register.
      • Wake-Up Packet Length (WUPL) register.
      • Wake-Up Packet Memory (WUPM) register.
6. The MAC cluster and the PHY are reset by the appropriate event only if the manageability unit is
   disabled and the host is in a low-power state with WoL disabled. WoL disabled means either
   AUX_PWR pin is cleared, or APM Enable bit in NVM Control Word 3 is disabled, or ACPI is disabled
   (all wake-up filters are disabled or PME_EN bit is disabled in PMCSR register).
7. The contents of the following memories are cleared to support the requirements of PCIe FLR:
      • The Tx packet buffers.
      • The Rx packet buffers.
8. Sticky bits and hardware init bits (indicated as HwInit) in the PCI Configuration registers are cleared
   only by LAN Power Good reset.
9. The following register fields are not affected by FLR or PFLR:
      • Max_Payload_Size in the Device Control register
      • Active State Power Management (ASPM) Control in the Link Control register
      • Common Clock Configuration in the Link Control register
      • Link Equalization Request in the Link Status 2 register.
      • Read Completion Boundary (RCB) in the Link Control register
      • Extended Synch in the Link Control register
      • Hardware Autonomous Speed Disable in the Link Control 2 register
      • Link Equalization Control registers in the Secondary PCI Express Extended Capability structure
10. These registers include:
      • VFEICS
      • VFEIMS
      • VFEIAC
      • VFEIAM
      • VFEITR 0-2
      • VFIVAR0
      • VFIVAR_MISC
      • VFPBACL
      • VFMailbox
11. These registers include:
      — VFEICS
      • VFEIMS
      • VFEIMC
      • VFEIAC

150                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

      • VFEIAM
      • VFEICR
      • VFEITR 0-2
      • VFIVAR0
      • VFIVAR_MISC
      • VFPBACL
      • VFMailbox
      • RSCINT
12. These registers include specific VF bits in the FVRE and FVTE registers are cleared as well.
13. These registers include:
      • MSI/MSI-X enable bits
      • BME
      • Error indications
14. Rx and Tx counters might miss proper counting due to VFLR indicating more packets than those
    ones actually transferred. It could happen if VFLR happened after counting occurred but before Tx
    or Rx completed.
15. PHY reset events that exclude PLLs reset the following blocks:
      • PMA
      • PCS
      • Autoneg
      • MCP
      • PHY NVM I/F
      • Global, excluding PLLs.The PHY Image Reload command should be effective even if the PHY
        embedded micro controller is stuck by a faulty PHY image.
16. Concerned functionalities do not reset if the Manageability or WoL are enabled.
Note:        Unless specified otherwise the X550’s on-die memories are reset together with the functional
             block(s) they belong to.
