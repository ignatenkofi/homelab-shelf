## 5.3 Network Interfaces Power Management

The X550 transitions any of the network interfaces into a low-power state in the following cases:
 • The respective LAN function is in LAN disable mode using LANx_DIS_N pin.
 • The X550 is in D3 or Dr state, APM WoL is disabled for the port, ACPI wake is disabled for the port
   and pass-through manageability is disabled for the port.
Use of the LAN ports for pass-through manageability follows the following behavior:
 • If manageability is disabled (Manageability Mode field in the Common Firmware Parameters NVM
   word is set to None - Section 6.2.16), LAN ports are not allocated for manageability.
 • If manageability is enabled:
     — Power-up — Following an NVM read, a single port is enabled for manageability, running at the
       lowest speed supported by the interface. If APM WoL is enabled on a single port, the same port
       is used for manageability. Otherwise, manageability protocols (such as teaming) determine
       which port is used.
     — D0 state — Both LAN ports are enabled for manageability.
     — D3 and Dr states — A single port is enabled for manageability, running at the lowest speed
       supported by the interface. If WoL is enabled on a single port, the same port is used for
       manageability. Otherwise, manageability protocols such as teaming) determine which port is
       used.
Enabling a port as a result of the previous behaviors cause an internal reset of the port including its
associated PHY.
When a network interface is in low-power state, the X550 MAC asserts internal signals to notify the PHY
that it must either power down as well or re-negotiate to a lower link speed.

### 5.3.1 PHY Power-Down State

Each X550 port enters a power-down state when none of its clients is enabled and therefore has no
need to maintain a link. This can happen in one of the following cases:
1. D3/Dr state — Each PHY enters a low-power state if all the following conditions are met:
     a. The LAN function associated with this PHY is in a non-D0 state
     b. APM WoL is inactive
     c. Manageability does not use this port
     d. ACPI PME is disabled for this port
2. LAN disable pin — Each PHY is disabled if the associated LAN disable input pin indicates that the
   port should be disabled.
3. LAN PCI Disable bit in NVM — A single LAN port can also be disabled through NVM settings. If
   the LAN PCI Disable bit is set in NVM Control Word 2, and if the port is not used for WoL or for MC
   traffic, the LAN Disable Select bit selects the MAC and PHY port that enters power down even in D0
   state. Note that if the port is used for WoL or by the MC, setting the LAN PCI Disable bit in NVM
   Control Word 2 does not bring the MAC and PHY into power down, but only the DMA block.

333369-009                                                                                                191
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                 Power Management and Delivery

When powered down by one of these means, a significant portion of the MAC and the PHY (including its
microprocessor, MDIO, and interrupt logic) are powered down. Only the PHY PLLs are functioning, and
the Analog Front-End (AFE) is turned off (gets placed in high-impedance mode).
When the X550 is completely powered down (Dr state), the PHYs reach a deeper power saving mode.
When the PHY exits power down, it re-initializes all analog functions, and retrieves the default
configuration settings that were loaded from NVM the last time NVM was read.

### 5.3.2 PHY Power-Down via the PHY Register

The PHY can also be powered down by setting a Low Power bit in a PHY register (Global Standard
Control 1: Address 1E.0, bit B). This bit powers down a significant portion of the PHY but clocks
provided to the MAC and to the register section of the PHY remain active. Only the MDIO, interrupts,
and microprocessor are functioning, and the AFE is turned off (gets placed in high-impedance mode).
This enables the PHY management interface to remain active during register power down. Setting this
bit also sets all of the Low Power bits in the other MMDs.
When the PHY exits software power down (Low Power bit cleared), it re-initializes all analog functions,
but retains its previous configuration settings.

### 5.3.3 Smart Power-Down (SPD)

Smart Power-Down (SPD) is a feature that allows the PHY to enter a deep power saving state if it
detects that the link is down for a long period of time. In this mode, the PHY does not transmit Link
pulses. To detect a connection of a partner, the PHY periodically wakes up and sends link pulses for a
short period of time to allow detection by the link partner. SPD is applicable to all power management
states.
SPD combines a power-saving mechanism with the fact that the link might disappear and resume.
Smart power-down is enabled by Smart Power-Down Enable PHY register field, which can be
provisioned in the PHY NVM section, and is entered when the PHY detects link loss.
SPD is supported only when working in auto-negotiation mode, and not in parallel detect mode.
While in the smart power-down state, the PHY powers down circuits and clocks that are not required for
detection of link activity. The PHY is still able to detect link pulses (including parallel detect) and wakeup
to engage in link negotiation. The PHY does not send auto-negotiation words (FLP) while in SPD state
unless configured to Deadlock-avoidance as defined in Section 5.3.3.1. Register accesses to the PHY is
still possible.
Note:     Since some of the PHY blocks might be in power-down during SPD, Access to the registers of
          these blocks is not supported during SPD.
PHY indicates SPD-Status via the Smart Power-Down Status bit. This register is accessible to the MAC in
all the PHY power-modes.
When the PHY is in smart power-down and detects link activity, it re-negotiates link speed based on the
power state as in the normal case.
Note:     The link-disconnect state applies to all power management states (Dr, D0u, D0a, D3). The
          link might change status, that is go up or go down, while in any of these states
See Section 5.3.3.2 for details of the SPD control bit.

192                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

#### 5.3.3.1 Deadlock Avoidance Mechanism (FLP)

While in link disconnect, the X550 monitors the link for Fast Link Pulses to identify when a link is
reconnected. The X550 also periodically transmits pulses to resolve the case of two X550 (or devices
with X550-like behavior) connected to each other across the link. Otherwise, two such devices might be
locked in smart power-down mode, not capable of identifying that a link was re-connected. The link
pulses are transmitted on average every 100 ms on alternate channels (A/B and C/D), and add
negligible power to total X550 power at link disconnect mode.
Pulses might not conform to IEEE specification regarding link pulse template.
If the link partners are disconnected and then reconnected, it is possible that the two controllers
transmit their pulses at the same time. Since the X550 might mask its receiver during pulse
transmission, such synchronization causes pulses to be missed by both partners. A randomization
factor is therefore applied to the timing of transmitted pulses, affecting the period between pulses. The
randomization factor is specific per device and should reduce the probability of a lock to at least 10-4.
Note:        If the two partners happen to transmit within the same slot, and if the randomization factor
             happens to be similar, it takes longer for the partners to get out of sync with each other.
Deadlock-Avoidance smart power-down is enabled by the Deadlock Avoidance Enable bit in the PHY
registers. The default value is enabled. The Enable bit applies only while in smart power-down mode.
Note:        The emission of FLP by the two ports of the X550 are not synchronized to avoid issues in tests
             where a link is established between the two ports.

#### 5.3.3.2 SPD Control

The following bits in the PHY registers are used to control/monitor the SPD feature:
 • Controls
     — Deadlock Avoidance Enable — Enables deadlock avoidance by transmitting FLP while in smart
       power down mode — 1E.C475.3 (Section 10.6.18).
     — Smart Power-Down Enable — 1E.C475.2 (Section 10.6.18).
     — Smart Power-Down Entered Mask (Enable interrupt generation) — The mask bit is to enable an
       interrupt to the MAC in case SPD was entered — 1E.D401.E (Section 10.6.47).
 • Statuses
     — Smart Power-Down Status (active, inactive) — 1E.C475.D (Section 10.6.18).
     — Smart Power-Down Entered — When this bit is set, it indicates that the smart power down state
       was entered — 1E.CC01.E (Section 10.6.44).
Note:        The Smart Power-Down Entered bit is self cleared when read, but it is set again by the next
             try of the Deadlock avoidance mechanism to establish a link.

333369-009                                                                                              193
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                     Power Management and Delivery

#### 5.3.3.3 Timing Definitions

When port is configure to SPD it should meet the following timing constraints:

Table 5-3.     SPD Timing Parameters
  Parameter                 Description                 Min      Typ      Max                   Remark

Tspd-in        Time elapsed from the Link-              2 sec            10 sec
               Disconnect event until Port actually
               enter into SPD mode.

Tspd-out       Time elapsed from the Link-Reconnect     70 ms            100 ms
               event (first link pulse arrives at
               package pins) until Port actually exit
               from SPD mode and start the auto-
               negotiation mode.

Tb2b-flp       Time between two consecutive FLPs        90 ms   100 ms   110 ms   The Tb2b-flp Min/Max numbers include
               (Fast-Link-Pulses) transmitted by TVL                              the randomization factor during the
               during Deadlock-Avoidance mode.                                    Deadlock-Avoidance mode.

### 5.3.4 Disable 10GBASE-T and/or 1000BASE-T Speeds

To reduce power consumption of a port even when it is active, there is an option to disable

# 10 Gb/s and/or 1000 Mb/s advertisement during auto-negotiation.

This can be useful for cases where a copper link is used as a dormant link for redundancy purposes
only.
These options are enabled by the following bits in PHY registers:
 • Auto-Negotiation 10GBASE-T Control Register: Address 7.20, bit C - Disable 10 Gb/s in any state.
 • Auto-Negotiation Vendor Provisioning 1: Address 7.C400, bit F - Disable 1000 Mb/s in any state.
Note:      These bits disable the advertisement of a speed in any power state, whether the port is active
           (D0u or D0a) or in low power (Dr or D3).

### 5.3.5 Low Power Link Up (LPLU)

The PHY is aware of power management states. If the PHY is not in a power down state, PHY behavior
regarding several features are different depending on the device or port power state. The internal PHY
power state is controlled internally from the MAC.
Normal PHY speed negotiation drives to establish a link at the highest possible speed. The PHY supports
an additional mode of operation, where the PHY drives to establish a link at a low speed. The LPLU
process enables a link to come up at the lowest possible speed in cases where power is more important
than performance. Different behavior is defined for the D0 state and the other non-D0 states.
Table 5-4 lists link speed as function of power management state, link speed control, and GbE speed
enabling:

194                                                                                                         333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

Table 5-4.          Link Speed vs. Power State
                          Disable Bits in NVM         Disable Bits in Register
              LPLU
 Power
              Bit in     Disable        Disable        Disable        Disable                 PHY Speed Negotiation
 State
              NVM       10 GbE in      1 GbE in       10 GbE in       1 GbE in
                       LPLU Mode      LPLU Mode       Any State      Any State

                                                          0b             0b        PHY advertises 10 GbE, 1 GbE, 100 Mb/s

                                                          1b             0b        PHY advertises 1 GbE and 100 Mb/s only.
   D0           X           X              X
                                                          0b             1b        PHY advertises 10 GbE and 100 Mb/s only.

                                                          1b             1b        PHY advertises 100 Mb/s only.

                                                          0b             0b        PHY advertises 10 GbE, 1 GbE, 100 Mb/s

                                                          1b             0b        PHY advertises 1 GbE and 100 Mb/s only.
               0b           X              X
                                                          0b             1b        PHY advertises 10 GbE and 100 Mb/s only.

                                                          1b             1b        PHY advertises 100 Mb/s only.

                                                                                   PHY goes through LPLU procedure, starting
                                                          0b             0b
                                                                                   from 100 Mb/s, up to 1 GbE and 10 GbE.

                                                                                   PHY goes through LPLU procedure, starting
                                                          1b             0b
                           0b             0b                                       from 100 Mb/s and followed by 1 GbE only.
 Non-D0
                                                                                   PHY goes through LPLU procedure, starting
                                                          0b             1b
                                                                                   from 100 Mb/s and followed by 10 GbE only.

               1b                                         1b             1b        PHY advertise 100 Mb/s only.

                                                                                   PHY goes through LPLU procedure, starting
                                                          X              0b
                           1b             0b                                       from 100 Mb/s and followed by 1 GbE.

                                                          X              1b        PHY advertises 100 Mb/s only.

                           1b             1b              X              X         PHY advertises 100 Mb/s only.

                           0b             1b              X              X         N/A (non supported setting)

X means Don’t care.
LPLU bit in NVM - Refers to NVM Control Word 3, bit 3, shared by both ports.
Disable 10 GbE in LPLU mode - Refers to NVM Control Word 3, bits 6 and 8, one bit per port.
Disable 1 GbE in LPLU mode - Refers to NVM Control Word 3, bits 5 and 7, one bit per port.
Disable 10 GbE any state - Refers to PHY register 7.20[C].
Disable 1 GbE any state - Refers to PHY register 7.C400[F].

Notes:       The software device driver is responsible to re-start auto-negotiation when it changes the
             setting of the Disable 10 GbE or 1 GbE bits in the PHY register.
             For proper LPLU functionality, Upshift-Enabled bit must be set in the PHY at register 7.C411.0
             (default is 1b, enabled).
             If manageability and WoL are both disabled, the directives of Table 5-4, when in non-D0
             state, are not relevant as the PHY port is disabled.

333369-009                                                                                                                    195
                                     Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                Power Management and Delivery

#### 5.3.5.1 Behavior in Non-D0 State

If the LPLU bit is set in the NVM, the PHY negotiates to a low speed while in non-D0 states (Dr or D3).
This applies only when the link is required by one of the following: SMBus or NC-SI manageability, APM
wake, or PME. Otherwise, the PHY is disabled during the non-D0 state.
Link negotiation begins with the PHY trying to negotiate at the lowest speed it is allowed to advertise,
as listed in Table 5-4. If link establishment fails, the PHY tries to negotiate at additional speeds, such as
all speeds allowed up to the lowest speed supported by the partner. For example, the PHY advertises
100 Mb/s only and the partner supports 1000 Mb/s only. After the first try fails, PHY enables 100/
1000 Mb/s and tries again. The PHY continues to try and establish a link until it succeeds or until it is
instructed otherwise.
Note:     Automatic MDI/MDI-X resolution is done during the first auto-negotiation stage.

#### 5.3.5.2 Link Speed Change vs. Power Mode

Normal speed negotiation drives to establish a link at the Highest Common Denominator (HCD) link
speed. The X550 supports an additional mode of operation, where the PHY establishes a link at the
Lowest Common Denominator (LCD) link speed. The LPLU process allows a link to come up at any
possible speed in cases where power is more important than performance. Different behavior is defined
for the D0 state and non-D0 states as a function of the D10GMP, D1GMP bits in the NVM and of the
MMNGC.MNG_VETO register bit.
The X550 initiates auto-negotiation without a direct software device driver command in the following
cases:
 • When the state of MAIN_PWR_OK pin changes.
 • When the MNG_VETO bit value changes.
 • On a transition from D0 state to a non-D0 state, or from a non-D0 state to D0 state.
During a manageability session, any change in a power management state must not cause the Ethernet
link to drop because the manageability session will be lost. Therefore in such a case the Ethernet link
speed should be kept unchanged. For example, the transition to D3hot state is not propagated to the
PHY as long as a manageability session exists.
Note:     However, if main power is removed, the PHY is allowed to react to the change in power state
          (such as the PHY might respond in link speed change). The motivation for this exception is to
          reduce power when operating on auxiliary power by reducing link speed.
The capability of masking from the PHY the changes that occur in a power management state is enabled
by default on LAN_PWR_GOOD reset. The Keep_PHY_Link_Up_En bit in NVM Control Word 3 - Offset
0x38 word must be cleared to disable it. Once enabled, the feature is enabled until the next
LAN_PWR_GOOD (such as the X550 does not revert to the hardware default value on PE_RST_N, PCIe
reset, or any other reset but LAN_PWR_GOOD).
Existence of a manageability session is identified by the MNG_VETO bit set in the MMNGC register.
The MNG_VETO bit is set by the MC through the Management Control command (see
Section 11.5.11.1.5 for SMBus command and Section 11.6.3.12 for NC-SI command) on the sideband
interface. It is cleared by the external MC (also through a command on the sideband interface) when
the manageability session ends.

196                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

The MNG_VETO bit becomes meaningless when de-asserting the MAIN_PWR_OK input pin.
MAIN_PWR_OK must be de-asserted at least 10 ms before power drops below its 90% value. This
allows enough time to the PHY to drop the link and restart auto-negotiation before auxiliary power
takes over. Note that since auto-negotiation is restarted, the PHY power consumption is already cut
down.
Figure 5-2 shows the X550 behavior when entering low power mode:

                                (Function disabled via NVM) OR
                                (Function switched to Dx, i.e. Dr/D3) OR
                                (((Function already in Dx) OR (function was disabled via NVM)) AND
                                 (MNG_VETO bit change)) OR
                                (MAIN_PWR_OK de-assertion)))

                         YES                            YES
                                MAIN_PWR_OK                    MNG VETO set
                                     set
                                   NO                                                                     MAC

                                                                                                          PHY
                                                                       NO

                                                        YES
                                                               Speed @100M

                                                                     NO

                 Do                                                              NO
                                                                D10GMP set
               nothing
                                                                     YES

                         YES                             NO                        YES
                                 Speed @10G                     D1GMP set                        Speed @LCD

                                        NO                           YES                             NO

                          YES
                                 Speed @LCD

                                        NO

                         New Advertised Abilities:                                       New Advertised Abilities:
                         Try 1: 100M only                New Advertised Ability:         Try 1: 100M only
                         Try n: 100M, and 1G if it is         100M only                  Try n: 100M, and higher up
                         lowest of link partner                                          to lowest of link partner

                                                          Restart AN with New
                                                          Advertised Abilities

Figure 5-2.    Link Speed Change when Entering Power-Down Mode

333369-009                                                                                                            197
                                        Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                               Power Management and Delivery

Figure 5-3 shows the X550 behavior when going to power-up mode.

                               (Function disabled via NVM) OR
                               (Function switched to Dx, i.e. Dr/D3) OR
                               (((Function already in Dx) OR (function was disabled via NVM)) AND
                                (MNG_VETO bit change)) OR
                               (MAIN_PWR_OK de-assertion)))

                        YES                            YES
                               MAIN_PWR_OK                    MNG VETO set
                                    set
                                  NO                                                                     MAC

                                                                                                         PHY
                                                                      NO

                                                       YES
                                                              Speed @100M

                                                                    NO

                Do                                                              NO
                                                               D10GMP set
              nothing
                                                                    YES

                        YES                             NO                        YES
                                Speed @10G                     D1GMP set                        Speed @LCD

                                       NO                           YES                             NO

                         YES
                                Speed @LCD

                                       NO

                        New Advertised Abilities:                                       New Advertised Abilities:
                        Try 1: 100M only                New Advertised Ability:         Try 1: 100M only
                        Try n: 100M, and 1G if it is         100M only                  Try n: 100M, and higher up
                        lowest of link partner                                          to lowest of link partner

                                                         Restart AN with New
                                                         Advertised Abilities

Figure 5-3.   Link Speed Change when Entering Power-Up Mode

Notes:   To simplify things, the impact of the LPLU and Keep_PHY_Link_Up_En bits in the NVM Control
         Word 3 is not shown in the flow charts because these bits are assumed to be set. If the
         Keep_PHY_Link_Up_En bit is cleared, the VETO bit set condition always returns NO.
         The same remark for the impact of the Disable Speed bits described in Section 5.3.4, which
         are assumed to be cleared.
         The PHY re-negotiates full line speed once exiting power down state, without waiting for the
         Memory Access Enable bit of the PCIe Command register to be written.

198                                                                                                                  333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

### 5.3.6 Energy Efficient Ethernet (EEE)

the X550 enters EEE Low Power Idle (LPI) mode on transmit or receive independently each time the
X550 detects no data is scheduled for transmission, or the link partner indicates no data is pending for
reception.
EEE LPI mode defined in IEEE802.3az enables power saving by switching off part of the X550
functionality when no data needs to be transmitted or/and received. Decision on whether the X550
transmit path should enter LPI mode or exit LPI mode is done according to a need to transmit.
Information on whether a link partner has entered LPI mode is detected by the X550 and utilized for
power saving in the receive circuitry.
When no data needs to be transmitted, a request to enter transmit LPI is issued on the internal xxMII
Tx interface causing the PHY to transmit sleep symbols for a predefined period of time followed by a
quite period. During LPI, the PHY periodically transmits refresh symbols that are used by the link
partner to update adaptive filters and timing circuits to maintain link integrity. This quiet-refresh cycle
continues until transmitting ‘normal inter-frame’ encoding on the internal xxMII Tx interface. The PHY
communicates to the link partner the move to link active state by sending wake symbols for a
predefined period of time. The PHY then enters a normal operating state where data or idle symbols are
transmitted.
In the receive direction, entering LPI mode is triggered by receiving sleep symbols from the link
partner. This signals that the link partner is about to enter LPI mode. After sending the sleep symbols,
the link partner ceases transmission. When the link partner initiates the move to LPI, the PHY indicates
“assert low power idle” on the internal xxMII Rx interface and the X550 receiver disables functionality
to reduce power consumption.
Figure 5-4 and Table 5-5 illustrate the general principles of EEE LPI operation on the Ethernet link.

                  Active                                 Low-Power                                         Active
                                               Refresh

                                                                        Refresh
                  Data/

                           Sleep

                                                                                             Wake

                                                                                                             Data/
                                                                                                    IDLE

                                                                                                             IDLE
                   Idle

                                   Quiet                        Quiet              Quiet

                           Ts        Tq         Tr                                         Tw _PHY

                                                                                            Tw _System

Figure 5-4.       EEE Operation

Table 5-5.        EEE Parameters
                  Parameter                                                       Description

Sleep Time (Ts)                             Duration PHY sends sleep symbols before going quiet.

Quiet Duration (Tq)                         Duration PHY remains quiet before it must wake for refresh period.

Refresh Duration (Tr)                       Duration PHY sends refresh symbols for timing recovery and coefficient
                                            synchronization.

PHY Wake Time (Tw_PHY)                      Minimum duration PHY takes to resume to active state after decision to wake.

Receive System Wake Time (Tw_System_rx)     Wait period where no data is expected to be received to give the local receiving
                                            system time to wake-up.

Transmit System Wake Time (Tw_System_tx)    Wait period where no data is transmitted to give the remote receiving system
                                            time to wake-up.

333369-009                                                                                                                 199
                                   Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                               Power Management and Delivery

#### 5.3.6.1 Conditions to Enter EEE Tx LPI

In the transmit direction entry into EEE LPI mode of operation is triggered when one of the following
conditions exist:
1. No transmission is pending, management does not need to transmit and internal transmit buffer is
   empty and the EEER.TX_LPI_EN bit is set to 1b. If the EEER.TX_LPI_EN bit is set to 1b and a XOFF
   flow control packet is received from the link partner or PFC XOFF are received for all the traffic
   classes supporting PFC, the X550 moves the link into the Tx LPI state for the pause duration even if
   a transmission is pending.
2. When EEER.FORCE_TLPI is set (even if EEER.TX_LPI_EN is cleared).
      • If EEER.FORCE_TLPI is set in mid-packet, the X550 completes the packet transmission and
        moves Tx to LPI.
When one of the previous conditions to enter Tx LPI state are detected “assert LPI” is transmitted on
the internal xxMII interface and the X550 PHY transmits sleep symbols on the network interface to
communicate to the link partner entry into Tx LPI link state. After sleep symbols transmission, the PHY
immediately enters the low power quiet mode. In this state the PHY periodically transitions between
quiet link state, where link is idle, to sending refresh symbols until a request to transition link back to
normal (active) mode is transmitted on the internal xxMII Tx interface (See Figure 5-4).
Note:     Initial EEER.TX_LPI_EN configuration is loaded from NVM.
Note:     10GBASE-T Ethernet LPI allows each link direction to enter sleep, refresh or wake states
          asymmetric from the other direction.
Note:     EEE LPI status of a X550 port can be found in the EEE_STAT register.

#### 5.3.6.2 Transition from Tx LPI to Active Link State

The X550 exits Tx LPI link state and transition link into active link state when none of the conditions
defined in Section 5.3.6.1 exist. To transition into active link state, the X550 transmits:
1. Normal ‘inter-frame’ encoding on the internal xxMII Tx interface for a pre-defined link rate
   dependent period time of Tw_sys_tx-min (defined by the EEE_SU register and IEEE802.3az clause
   78.5). As a result, the PHY transmits wake symbols for a Tw_phy duration followed by idle symbols.
2. If the Tw_System_tx duration defined in the EEER.TW_SYSTEM field is longer than Tw_sys_tx-min,
   the X550 continues transmitting the ‘inter-frame’ encoding on the internal xxMII interface until the
   time defined in the EEER.TW_SYSTEM field has expired, before transmitting the actual data. During
   this period the PHY continues transmitting idle symbols.
Note:     When moving out of Tx LPI to transmit a 802.3x flow control frame, the X550 waits for the
          Tw_sys_tx-min duration before transmitting the flow control frame. It should be noted that
          even in this scenario actual data is transmitted only after the Tw_System_tx time defined in
          the EEER.TW_SYSTEM field has expired.

200                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

#### 5.3.6.3 EEE Auto-Negotiation

Auto-negotiation provides the capability to negotiate EEE capabilities with the link partner using the
next page mechanism defined in IEEE802.3 Annex 73A. IEEE802.3 auto-negotiation is performed at
power up, on command from software, upon detection of a PHY error or following link re-connection.
During the link establishment process, both link partners indicate their EEE capabilities using IEEE802.3
auto-negotiation. If EEE is supported by both link partners for the negotiated PHY type, the EEE
function can be used independently in either direction.

#### 5.3.6.4 EEE Link Level (LLDP) Capabilities Discovery

The X550 supports LLDP negotiation via software using the EEE IEEE802.1AB Link Layer Discovery
Protocol (LLDP) Type, Length, Value (TLV) fields defined in IEEE802.3az clause 78 and clause 79. LLDP
negotiation enables negotiation of increased system wake time (Transmit Tw and Receive Tw) to enable
improving system energy efficiency.

5.3.6.4.1              LLDP Negotiation Actions

Following negotiation of a new system wake time via EEE LLDP negotiation, the following fields and
registers should be updated:
The EEER.TW_SYSTEM field with the negotiated Transmit Tw time value, to increase the duration where
idle symbols are transmitted following a move out of EEE Tx LPI state before actual data can be
transmitted.
 • A value placed in EEER.TW_SYSTEM field does not effect transmission of flow control packets.
   Depending on the technology flow control packet, transmission is delayed following a move out of
   EEE Tx LPI state only by the minimum Tw_sys_tx time as defined in IEEE802.3az clause 78.5. In
   the X550 the minimum Tw_sys_tx time value is defined in the EEE_SU register together with time
   defined in IEEE802.3az clause 78.5. Value varies as a function of link rate and technology.

#### 5.3.6.5 EEE Statistics

The X550 supports reporting a number of EEE LPI Tx and Rx events via the RLPIC and TLPIC registers.

333369-009                                                                                            201
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                               Power Management and Delivery
