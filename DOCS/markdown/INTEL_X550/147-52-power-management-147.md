## 5.2 Power Management

### 5.2.1 Introduction to X550 Power States

The X550 supports the D0 and D3 power states defined in the PCI Power Management and PCIe
specifications. D0 is divided into two sub-states: D0u (D0 un-initialized), and D0a (D0 active). In
addition, the X550 supports a Dr state that is entered when PE_RST_N pin is asserted (including the
D3cold state).
Figure 5-1 shows the power states and transitions between them.

                  LAN_PWR_GOOD assertion                                                          FLR
                                                                PCIe* Reset deasserted
                                      MAC auto-read        Dr                            D0u
                                      done from NVM

                              Hot Reset:                                              Enable:
                        PCIe* Reset asserted /                                       Master or
                         In-Band PCIe* Reset                                       slave Access

                                                                   Write 11 to
                                                      D3                                 D0a
                                                                   Power State

Figure 5-1.    Power Management State Diagram

### 5.2.2 Auxiliary Power Usage

The X550 uses the AUX_PWR indication that auxiliary power is available to the controller, and therefore
advertises D3cold wake-up support in the PMC.PME_Support field and sets the Aux_Power_Detected bit
in the PCIe capability structure Device Status Register. The AUX_PWR pin is strapped during Power On
Reset (POR). The amount of power required for the function, which includes the entire Network
Interface Card (NIC), is advertised in the Power Management Data register, which is loaded from the
NVM.

333369-009                                                                                              181
                                   Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                              Power Management and Delivery

The only effect of setting AUX_PWR to 1b is advertising D3cold wake-up support and changing the reset
function of PME_En and PME_Status. AUX_PWR is a strapping option in the X550. If D3cold is
supported, the PME_En and PME_Status bits of the Power Management Control/Status Register
(PMCSR), as well as their shadow bits in the Wake-Up Control Register (WUC) are reset only by the
power up reset (detection of power rising). The X550 tracks the PME_En bit of the PMCSR and the
Auxiliary (AUX) power PM Enable bit of the PCIe Device Control register to determine the power it can
consume (and therefore its power state) in the D3cold state (internal Dr state). Note that the actual
amount of power differs between form factors.
According to the following settings the X550 might consume higher auxiliary power than is allowed by
PCIe specifications:
 • If the AUX Power PM Enable bit of the PCIe Device Control register is set, the X550 might consume
   higher power for any purpose (even if PME_En is not set).
 • If the AUX Power PM Enable bit of the PCIe Device Control register is cleared, higher power
   consumption is determined by the PCI-PM legacy PME_En bit of the PMCSR.

### 5.2.3 PCIe Link Power Management

The PCIe link state follows the power management state of the device. Since the X550 incorporates
multiple PCI functions, the device power management state is defined as the power management state
of the most awake function:
 • If any function is in D0a state in ARI mode or either D0a or D0u in non-ARI mode, the PCIe link
   assumes the device is in D0 state.
 • Else, if in ARI mode, at least one of the functions is in D3 state and the other functions are not in
   D0a state, or if in non-ARI mode all of the functions are in the D3 state, the PCIe link assumes the
   device is in D3 state.
 • Else, the device is in Dr state (PE_RST_N is asserted to all functions).
The X550 supports the following PCIe power management link states:
 • L0 state is used in D0u and D0a states.
 • The L1 state is used in D0a and D0u states each time link conditions apply, as well as in the D3
   state.
 • The L2 state is used in the Dr state following a transition from a D3 state if PCI-PM PME is enabled.
 • The L3 state is used in the Dr state following power up, on transition from D0a and also if PME is not
   enabled in other Dr transitions.
The X550 support for active state link power management is reported via the PCIe Active State Link PM
Support register loaded from NVM.
The following NVM fields control L1 behavior:
 • Act_Stat_PM_Sup — Indicates support for ASPM L1 in the PCIe configuration space (loaded into the
   Active State Link PM Support field).
 • L1_Act_Ext_Latency — Defines L1 active exit latency.
 • L1_Act_Acc_Latency — Defines L1 active acceptable exit latency.

182                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

### 5.2.4 Power States

#### 5.2.4.1 D0uninitialized State

The D0u state is a low-power state used after PE_RST_N is de-asserted following power-up (cold or
warm), on hot reset (in-band reset through PCIe physical layer message) or on D3 exit.
When entering D0u, the X550 disables wake-ups.

5.2.4.1.1              Entry to a D0u State

D0u is reached from either the Dr state (on de-assertion of Internal PE_RST_N) or the D3hot state (by
configuration software writing a value of 00b to the Power State field of the PCI PM registers).
De-asserting internal PE_RST_N means that the entire state of the device is cleared, other than sticky
bits. State is loaded from the NVM, followed by establishment of the PCIe link. Once this is done,
configuration software can access the device.
On a transition from D3 to D0u state, the X550 requires that software perform a full re-initialization of
the function not including its PCI configuration space which is kept while in D3.

#### 5.2.4.2 D0active State

Once memory space is enabled, the X550 enters an active state. It can transmit and receive packets if
properly configured by the software device driver. The PHY is enabled or re-enabled by the software
device driver to operate/auto-negotiate to full line speed/power if not already operating at full
capability. Any APM wake-up previously active remains active. The software device driver can
deactivate ACPI wake-up by writing to the Wake-Up Control (WUC) register and APM wake-up by
writing to the General Receive Control (GRC) register, or activate other wake-up filters by writing to the
Wake-Up Filter Control (WUFC) register.

5.2.4.2.1              Entry to D0a State

D0a is entered from the D0u state by writing a 1b to the Memory Access Enable or the I/O Access
Enable bit of the PCI Command register. The DMA, MAC, and PHY of the appropriate LAN function are
enabled.

#### 5.2.4.3 D3 State (PCI-PM D3hot)

The X550 transitions to D3 when the system writes a 11b to the Power State field of the PMCSR. Any
wake-up filter settings that were enabled before entering this reset state are maintained. Upon
transition to D3 state, the X550 clears the Memory Access Enable and I/O Access Enable bits of the PCI
Command register, which disables memory access decode. In D3 the X550 only responds to PCI
configuration accesses and does not generate master cycles.
Configuration and message requests are the only PCIe TLPs accepted by a function in the D3hot state.
All other received requests must be handled as unsupported requests, and all received completions can
optionally be handled as unexpected completions. If an error caused by a received TLP (like an
unsupported request) is detected while in D3hot, and reporting is enabled, the link must be returned to
L0 if it is not already in L0 and an error message must be sent. See section 5.3.1.4.1 in the PCIe Base
Specification.

333369-009                                                                                             183
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                Power Management and Delivery

A D3 state is followed by either a D0u state (in preparation for a D0a state) or by a transition to Dr
state (PCI-PM D3cold state). To transition back to D0u, the system writes a 00b to the Power State field
of the PMCSR. Transition to Dr state is through PE_RST_N assertion.

5.2.4.3.1             Entry to D3 State

Transition to D3 state is through a configuration write to the Power State field of the PCI-PM registers.
Prior to transition from D0 to the D3 state, the software device driver disables scheduling of further
tasks to the X550; it masks all interrupts, it does not write to the Transmit Descriptor Tail (TDT) register
or to the Receive Descriptor Tail (RDT) register and operates the master disable algorithm as defined in
Section 5.2.4.3.2. If wake-up capability is needed, the software device driver should set up the
appropriate wake-up registers and the system should write a 1b to the PME_En bit of the PMCSR prior
to the transition to D3.
If all PCI functions are programmed into D3 state, the X550 brings its PCIe link into the L1 link state. As
part of the transition into L1 state, the X550 suspends scheduling of new TLPs and waits for the
completion of all previous TLPs it has sent. The X550 clears the Memory Access Enable and I/O Access
Enable bits of the PCI Command register, which disables memory access decode. Any receive packets
that have not been transferred into system memory is kept in the device (and discarded later on D3
exit). Any transmit packets that have not be sent can still be transmitted (assuming the Ethernet link is
up).
In preparation to a possible transition to D3cold state, and to reduce power consumption, whenever
entering D3 state, the software device driver might disable one of the LAN ports (LAN disable) and/or
the PHY(s) auto-negotiate network link(s) to a lower speed (if supported by the network interface). See
Section 5.3.5.2 for a description of network interface behavior in this case.

5.2.4.3.2             Master Disable

System software might disable master accesses on the PCIe link by either clearing the PCI Bus Master
bit or by bringing the function into a D3 state. From that time on, the X550 must not issue master
accesses for this function. Due to the full-duplex nature of PCIe, and the pipelined design in the X550,
it might happen that multiple requests from several functions are pending when the master disable
request arrives. The protocol described in this section insures that a function does not issue master
requests to the PCIe link after its Master Enable bit is cleared (or after entry to D3 state).
Two configuration bits are provided for the handshake between the device function and its software
device driver:
 • PCIe Master Disable bit in the Device Control Register (CTRL) register — When the PCIe Master
   Disable bit is set, the X550 blocks new master requests by this function. The X550 then proceeds to
   issue any pending requests by this function. This bit is cleared on master reset (LAN_PWR_GOOD
   all the way to software reset) to allow master accesses.
 • PCIe Master Enable Status bits in the Device Status register — Cleared by the X550 when the PCIe
   Master Disable bit is set and no master requests are pending by the relevant function. Set
   otherwise. Indicates that no master requests are issued by this function as long as the PCIe Master
   Disable bit is set. The following activities must end before the X550 clears the PCIe Master Enable
   Status bit:
 • Master requests by the transmit and receive engines
 • All pending completions to the X550 are received.

184                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

Notes:       The software device driver disables any reception to the Rx queues as described in
             Section 4.6.7.1.1. Then, the software device driver sets the PCIe Master Disable bit when
             notified of a pending master disable (or D3 entry). The X550 then blocks new requests and
             proceeds to issue any pending requests by this function. The software device driver then
             reads the change made in the PCIe Master Disable bit and then polls the PCIe Master Enable
             Status bit. Once the bit is cleared, it is guaranteed that no requests are pending from this
             function.
             The software device driver might time out if the PCIe Master Enable Status bit is not cleared
             within a given time. Examples for cases that the X550 might not clear the PCIe Master Enable
             Status bit for a long time are cases of flow control, link down, or DMA completions not making
             it back to the DMA block. In these cases, the software device driver should check that the
             Transaction Pending bit (bit 5) in the Device Status register in the PCI config space is cleared
             before proceeding. In such cases, the driver needs to clear internal buffers by:
                — Setting the HLREG0.LPBK bit.
                — Clearing RXCTRL.RXEN bit.
                — Setting the setting GCR_EXT.Buffers_Clear_Func bit for 20 s.
                — Initiate two consecutive software resets with a delay larger than 1 s between them.
             Intel’s device driver software times-out at ~800 s. The PCIe Master Disable bit must be
             cleared to enable master request to the PCIe link. This bit should be cleared through reset.

#### 5.2.4.4 Dr State

Transition to Dr state is initiated on several occasions:
 • On system power up — Dr state begins with the assertion of the internal power detection circuit
   (LAN_PWR_GOOD) and ends with de-assertion of PE_RST_N.
 • On transition from a D0a state — During operation the system might assert PE_RST_N at any
   time. In an ACPI system, a system transition to the G2/S5 state causes a transition from D0a to Dr
   state.
 • On transition from a D3 state — The system transitions the device into the Dr state by asserting
   PCIe PE_RST_N.
Any wake-up filter settings that were enabled before entering this reset state are maintained.
The system might maintain PE_RST_N asserted for an arbitrary time. The de-assertion (rising edge) of
PE_RST_N causes a transition to D0u state.
While in Dr state, the X550 might maintain functionality (for WoL or manageability) or might enter a Dr
Disable state (if no WoL and no manageability) for minimal device power. The Dr Disable mode is
described in the sections that follow.

5.2.4.4.1               Dr Disable Mode

The X550 enters a Dr disable mode on transition to D3cold state when it does not need to maintain any
functionality. The conditions to enter either state are:
 • The device such as all PCI functions) is in Dr state.
 • APM WoL is inactive for both LAN functions.
 • Pass-through manageability is disabled.

333369-009                                                                                                185
                                  Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                            Power Management and Delivery

 • ACPI PME is disabled for all PCI functions.
Entry into Dr disable is usually done on assertion of PCIe PE_RST_N. It might also be possible to enter
Dr disable mode by reading the NVM while already in Dr state. The usage model for this later case is on
system power up, assuming that manageability and wake-up are not required. Once the X550 enters Dr
state on power-up, the NVM is read. If the NVM contents determine that the conditions to enter Dr
Disable are met, the X550 then enters this mode (assuming that PCIe PE_RST_N is still asserted).
Exit from Dr disable is through de-assertion of PCIe PE_RST_N.
If Dr disable mode is entered from D3 state, the platform might remove X550 power. If the platform
removes X550 power, it must remove all power rails from the X550 if it needs to use this capability. Exit
from this state is through power-up cycle to the X550.

5.2.4.4.2                Entry to Dr State

Dr-entry on platform power-up is as follows:
 • Asserting the internal power detection circuit (LAN_PWR_GOOD). Device power is kept to a
   minimum by keeping the PHYs in low power.
 • The NVM is then read and determines device configuration.
 • If the APM Enable bit in NVM Control Word 3 is set, APM wake-up is enabled (for each port
   independently).
 • Each of the LAN ports can be enabled if required for WoL or manageability. See Section 5.3.5.2 for
   exact condition to enable a port. In such a case, the PHY might auto-negotiate to a lower speed on
   Dr entry (see Section 5.3.5).
 • The PCIe link is not enabled in Dr state following system power up (since PE_RST_N is asserted).
Entry to Dr state from D0a state is by asserting the PE_RST_N signal. An ACPI transition to the G2/S5
state is reflected in a device transition from D0a to Dr state. The transition can be orderly (such as user
selected a shut down operating system option), in which case the software device driver might have a
chance to intervene. Or, it might be an emergency transition (like power button override), in which
case, the software device driver is not notified.
To reduce power consumption, if any of manageability, APM wake or PCI-PM PME1 is enabled, the PHY
auto-negotiates to a lower link speed on D0a to Dr transition (see Section 5.3.5).
Transition from D3 state to Dr state is done by asserting the PE_RST_N signal. Prior to that, the system
initiates a transition of the PCIe link from L1 state to either the L2 or L3 state (assuming all functions
were already in D3 state). The link enters L2 state if PCI-PM PME is enabled.

 1. ACPI 2.0 specifies that OSPM does not disable wake events before setting the SLP_EN bit when entering the S5 sleeping state.
    This provides support for remote management initiatives by enabling Remote Power On (RPO) capability. This is a change from
    ACPI 1.0 behavior.

186                                                                                                                 333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

### 5.2.5 Timing of Power-State Transitions

The following sections give detailed timing for the state transitions. In the diagrams, the dotted
connecting lines represent the X550 requirements, while the solid connecting lines represent the X550
guarantees.
Note that the timing diagrams are not to scale. The clock’s edges are shown to indicate running clocks
only and are not used to indicate the actual number of cycles for any operation.

#### 5.2.5.1 Transition from D0a to D3 and Back without PE_RST_N

   PCIe reference clock

           PE_RST_N
                                                                      D 0Write
                                                                          3
                                                         2
                                                                                      tfl        td0mem

# 6 Memory Access Enable

          Reading NVM                                                            MAC auto-read
                                                                                                   5                     7
                          D 3write
             PHY reset          1

              PCIe link    L0                                 L1                                                 L0

                                                                                            4
       Wake up enabled                     Any mode                                                    APM / SMBus

             PHY state     Full                               power-managed                               Full

               DState     D0a                                D3                                           D0u                     D0a

  No.                                                                Notes

# 1 Writing 11b to the Power State field of the PMCSR transitions the X550 to D3. PHY re-negotiates to a lower link speed

           once VETO bit is cleared if manageability and/or WoL is enabled, else it is powered down. When in power-down mode,
           PHY is reset and its CSRs are reset to their default values according to provisional register segment loaded from NVM at
           last LAN_PWR_GOOD event.

# 2 The system can keep the X550 in D3 state for an arbitrary amount of time.

# 3 To exit D3 state the system writes 00b to the Power State field of the PMCSR.

    4 APM wake-up or manageability might be enabled based on what is read in the NVM.

# 5 After reading the MAC section of the NVM, the LAN ports are enabled and the X550 transitions to D0u state. PHY re-

           negotiates to full link speed.

# 6 The system can delay an arbitrary time before enabling memory access.

# 7 Writing a 1b to the Memory Access Enable bit or to the I/O Access Enable bit in the PCI Command register transitions the

           X550 from D0u to D0 state.

333369-009                                                                                                                              187
                                       Did this document help answer your questions?

                                                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                                                      Power Management and Delivery

#### 5.2.5.2 Transition from D0a to D3 and Back with PE_RST_N

                                                                   4a
          PCIe reference clock
                                                                        4b
                                                          tclkpg        tl2clk            t PWRGD-CLK
                                                                                                 6
                  PE_RST_N                                     3                 tpgdl
                                                          tl2pg                           tppg-clkint
                                                                                                     7
           Internal PCIe clock
