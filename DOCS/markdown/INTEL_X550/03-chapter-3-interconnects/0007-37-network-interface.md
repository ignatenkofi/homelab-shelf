## 3.7 Network Interface

### 3.7.1 Overview

The X550 provides dual-port network connectivity with copper media. Each port includes integrated
MAC-PHY functionality and can be operated at either 10 GbE, 1 GbE, 5GBASE-T, 2.5GBASE-T, or
100BASE-T(X) link speed. In terms of functionality there is no primary and secondary port as each port
can be enabled or disabled independently from the other, and they can be set at different link speeds.
The integrated PHYs support the following specifications:
 • 10GBASE-T as per the IEEE 802.3an standard.
 • 1000BASE-T and 100BASE-TX as per the IEEE 802.3 standard.
 • 2.5 and 5 Gb/s as per the NBASE-T specification.
Note:        The reader is assumed to be familiar with the specifications included in these standards,
             which is not overlapping with content of subsequent sections.
All MAC configuration is performed using Device Control registers mapped into system memory or I/O
space; an internal MDIO/MDC interface, accessible via software, is used to configure the PHY operation.

114                                                                                                                   333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

### 3.7.2 Internal MDIO Interface

The X550 implements an internal IEEE 802.3 Management Data Input/Output Interface (MDIO
Interface or MII Management Interface) between each MAC and its attached integrated PHY. This
interface provides firmware and software the ability to monitor and control the state of the PHY. It
provides indirect access to an internal set of addressable PHY registers. It complies with the new
protocol defined by Clause 45 of IEEE 802.3 std. No backward compliance with Clause 22.
Notes:       MDIO access to PHY registers must be operational from the time the PHY has completed its
             initialization once having read the PHY image from the NVM.
             During internal PHY reset events where the MAC is not reset, PHY registers might not be
             accessible and the MDIO access does not complete.
             Software is notified that PHY initialization and/or reset has completed by either polling or by
             PHY reset done interrupt (see Section 3.7.3.4.4).
The internal MDIO interface is accessed through registers MSCA and MSRWD. An access transaction to
a single PHY register is performed by setting the MSCA.MDICMD bit to 1b after programming the
appropriate fields in the MSCA and MSRWD registers. The MSCA.MDICMD bit is auto-cleared after the
read or write transaction completes.
To execute a write access, the following steps should be done:
1. Address Cycle - Register MSCA is initialized with the appropriate PHY register address in MDIADD
   DEVADD, and PORTADD fields, the OPCODE field set to 00b and MDICMD bit set to 1b.
2. Poll MSCA.MDICMD bit until it is read as 0b.
3. Write Data Cycle - Data to be written is programmed in field MSRWD.MDIWRDATA.
4. Write Command Cycle - OPCODE field in the MSCA register is set to 01b for a write operation and
   the MSCA.MDICMD bit is set to 1b.
5. Wait for the MSCA.MDICMD bit to reset to 0b, which indicates that the transaction on the internal
   MDIO interface completed.
To execute a read access, the following steps should be done:
1. Address Cycle - Register MSCA is initialized with the appropriate PHY register address in MDIADD
   DEVADD, and PORTADD fields, the OPCODE field set to 00b and MDICMD bit set to 1b.
2. Poll MSCA.MDICMD bit until it is read as 0b.
3. Read Command Cycle - OPCODE field in the MSCA register is set to 11b for a read operation and
   the MSCA.MDICMD bit is set to 1b.
4. Wait for the MSCA.MDICMD bit to reset to 0b, which indicates that the transaction on the internal
   MDIO interface completed.
5. Read Data Cycle - Read the data in field MSRWD.MDIRDDATA.
Notes:       A read-increment-address flow is performed if the OPCODE field is set to 10b in Step 3 The
             address is increased internally once data is read at Step 5 so that no address cycle is needed
             to perform a data read from the next address.
             Before writing the MSCA register, make sure that the MDIO interface is ready to perform the
             transaction by reading MSCA.MDICMD as 0b.

333369-009                                                                                                115
                                  Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

### 3.7.3 Integrated Copper PHY Functionality

#### 3.7.3.1 PHY Performance

3.7.3.1.1              Reach

Table 3-34. BER and Ranges vs. Link Speed and Cable Types
          Speed                   Cable                   Committed Reach                   Committed BER

                                  CAT-7                    Full reach: 100 m

                                  CAT-6a                   Full reach: 100 m

                                  CAT-6a                   Short reach: 30 m
        10GBASE-T                                                                               < 10-12
                                  CAT-6a            Jumper mode / direct attach: 1 m

                                  CAT-6                          55 m

                                  CAT-5e                          1m

        1000BASE-T                CAT-5e                   Full reach: 100 m                    < 10-10

        100BASE-TX                CAT-5e                   Full reach: 100 m                    < 10-8

                                  CAT-5e                   Full Reach: 100 m
        2.5GBASE-T                                                                              < 10-12
                                  CAT-6                    Full Reach: 100 m

                                  CAT-5e                   Full Reach: 100 m
        5GBASE-T                                                                                < 10-12
                                  CAT-6                    Full Reach: 100 m

Note:     Reaches specified in the table refer to real cable lengths and not to the IEEE standard model.

3.7.3.1.2              MDI/Magnetics Spacing

The X550 supports a variable distance of from 1.5 to 4 inches with the magnetics.

3.7.3.1.3              Cable Discharge

The X550 is capable of passing the Intel cable discharge test. Contact your Intel representative for
more details.

#### 3.7.3.2 Auto-Negotiation and Link Setup

Link configuration is always determined by PHY auto-negotiation with the link partner. The X550 does
not support parallel detect 100BASE-TX.

116                                                                                                      333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

3.7.3.2.1               Automatic MDI Cross-Over and Lane Inversion

Twisted pair Ethernet PHYs must be correctly configured for MDI (no cross-over) or MDI-X (cross-over)
operation to inter operate. This has historically been accomplished using special patch cables,
magnetics pinouts or Printed Circuit Board (PCB) wiring. The PHY supports the automatic MDI/MDI-X
configuration (like automatic cross-over detection) originally developed for 1000Base-T and
standardized in IEEE 802.3 clause 40, at any link speed and also during auto-negotiation. Manual (non-
automatic) MDI/MDI-X configuration is still possible via bits 1:0 of Auto-Negotiation Reserved Vendor
Provisioning 1 register at address 7.C410.
In addition to supporting MDI/MDI-X, the PHY supports lane inversion (MDI swap) of the ABCD pairs to
DCBA. It is useful for tab up or tab down RJ45 or integrated magnetics modules on the board. It is
configurable via PHY register 1.E400.

                 MDI (DTE/NIC)                                                           MDI (Switch)
                                                        Flat Cable
                                          1                                    1
                      TX    A                  Tx                        Rx              A              TX
                                          2                                    2
                                   R                                                   R
                                          3                                    3
                      RX    B      J           Rx                        Tx            J B              RX
                                          6                                    6
              PHY                  ‐                                                   ‐     PHY
                                          5                                    5
                      TX    C      4           Tx                        Rx            4 C              TX
                                          4                                    4
                                   5                                                   5
                                          7                                    7
                      RX    D                  Rx                        Tx              D              RX
                                          8                                    8

                 CROSS(1:0) = 00                                                        CROSS(1:0) = 01
Table 3-35. Cross-Over Function (7.C410.1:0 = 00b)

3.7.3.2.2               Auto-Negotiation Process

The integrated copper PHY performs the auto-negotiation function. Auto-Negotiation provides a method
for two link partners to exchange information in a systematic manner to establish a link configuration
providing the highest common level of functionality supported by both partners. Once configured, the
link partners exchange configuration information to resolve link settings such as:
 • Speed: 100/1000 Mb/s or 10 Gb/s
 • Link flow control operation (known as PAUSE operation)
Notes:       When operating in Data Center Bridging (DCB) mode, generally, priority flow control is used
             instead of link flow control, and it is negotiated via higher layer protocol (DCBx protocol) and
             not via auto-negotiation. Refer to Section 3.7.4.
             Each PHY is capable of successfully auto-negotiating with any device that supports 100 Mb/s
             or higher Ethernet, regardless of its method of Power over Ethernet (PoE) detection.
             The X550 supports only full duplex mode of operation at any speed.
PHY specific information required for establishing the link is also exchanged.

333369-009                                                                                                   117
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

If link flow control is enabled in the X550, the settings for the desired flow control behavior must be set
by software in the PHY registers and auto-negotiation is restarted. After auto-negotiation completes,
the software device driver must read the PHY registers to determine the resolved flow control behavior
of the link and reflect these in the MAC register settings (FCCFG.TFCE and MFLCN.RFCE).
Once PHY auto-negotiation completes, the PHY asserts a link-up indication to the MAC that might notify
software by an interrupt if the Link Status Change (LSC) interrupt is enabled. The resolved speed is also
indicated by the PHY to the MAC. The status of both is directed to software via LINKS.LINK_UP and
LINKS.LINK_SPEED bits.

3.7.3.2.2.1            Speed Resolution and Partner Presence

At the end of the auto-negotiation process, the link speed is automatically set to the highest common
denominator between the abilities advertised by the link partners.
If there is no common denominator, the PHY asserts the Device Present bit (Auto-Negotiation Reserved
Vendor Status 1: Address 7.C810, bit E) if it detected valid link pulses during auto-negotiation even
though there is no common link speed with the link partner. This bit is valid only if auto-negotiation is
enabled.
If the PHY training sequence cannot complete properly in spite of auto-negotiation completing, the PHY
retries auto-negotiation for a programmable number of times (set by PHY register 7.C400: 3:0) before
downshifting cyclically. Downshifting is enabled by PHY register 7.C400: 4. Automatic downshifting
events are reported by the Automatic Downshift bit in PHY register 7.CC00.

3.7.3.2.2.2            Link Flow Control Resolution

Flow control is a function that is described in Clause 31 of the IEEE 802.3 standard. It allows congested
nodes to pause traffic. Flow control is essentially a MAC-to-MAC function. PHYs indicate their MAC ability
to implement flow control during auto-negotiation. These advertised abilities are controlled through two
bits in the auto-negotiation registers (Auto-Negotiation Advertisement Register: Address 7.10), bits 5
and 6 for PAUSE and Asymmetric PAUSE, respectively.
After auto-negotiation, the link partner's flow control capabilities are indicated in Auto-Negotiation Link
Partner Base Page Ability Register: Address 7.13, bits 5 and 6.
There are two forms of flow control that can be established via auto-negotiation: symmetric and
asymmetric. Symmetric flow control was defined originally for point-to-point links; and asymmetric for
hub-to-end-node connections. Symmetric flow control enables either node to flow-control the other.
Asymmetric flow-control enables a repeater or switch to flow-control a DTE, but not vice versa.
Generally either symmetric PAUSE is used or PAUSE is disabled, even between a end-node and a
switch.
Table 3-36 lists the intended operation for the various settings of ASM_DIR and PAUSE. This information
is provided for reference only; it is the responsibility of the software to implement the correct function.
The PHY merely enables the two MACs to communicate their abilities to each other.

118                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-36. Pause and Asymmetric Pause Settings
       Local and Remote           Local Pause     Remote Pause
                                                                                         Result
       ASM_DIR Settings             Setting          Setting

       Both ASM_DIR = 1b               1                 1       Symmetric — Either side can flow control the other.

                                       1                 0       Asymmetric — Remote can flow control local only.

                                       0                 1       Asymmetric — Local can flow control remote.

                                       0                 0       No flow control.

   Either or both ASM_DIR = 0b         1                 1       Symmetric — Either side can flow control the other.

                                        Either or both = 0       No flow control.

#### 3.7.3.3 PHY Initialization

3.7.3.3.1               PHY Boot

Each PHY has an Embedded Microprocessor (MCP). Each MCP has its own instruction RAM (IRAM) and
Data RAM (DRAM). The MCP code/data segment and the PHY default configuration are fetched from the
external Flash device, right after power-on reset and also per PHY MMD register set to force a reload
(Global General Provisioning 3: Address 1E.C442, bit 0).
PHY access to the Flash device is controlled by the MAC. Assuming the PHY is granted by the MAC with
back-to-back access to the Flash, the PHY initialization process should take less than 200 ms, at the
end of which a PHY reset done interrupt is issued and/or reported in PHY register 1E.CC00.6.
Internal MDIO interface provides access to the PHY registers but it does not provide the software with
the ability to overwrite the PHY image located in the NVM. MDIO access is done via dedicated MAC
registers only.
The X550 maintains a CRC-16 (standard CCITT CRC x16 + x12 + x5 + 1) over the PHY image in the
NVM, and checks this on NVM loads. Inversion of the CRC after calculation is not required. If a CRC
error occurs, the PHY image is reloaded again. If an error also occurs on the second try, the PHY is
stopped and a fatal interrupt is generated to the host.
Default configuration read from the Flash overrides the default register values of the PHY. The same
MCP code/data segment is auto-loaded to both PHYs, but each PHY has its own default configuration.
MCP code/data segment and default configuration read from the Flash are stored into internal Shadow
RAMs. At PHY reset events, which are either issued by software (Global Standard Control 1: Address
1E.0000, bit F) or internally by the MAC, there is a reset of the micro controller; however there is no
reload of ISRAM/DSRAM from the Flash. The micro controller begins executing instructions out of
internal memory loaded from the previous Flash load. The same stands for PHY registers, which
retrieves their default values loaded from the previous Flash load.

3.7.3.3.2               PHY Power-Up Operations

The integrated PHY is designed to perform the following operations at boot:
1. Power-up calibration of VCOs and power supplies.
2. Provision stored default values (from Flash into internal data RAM and then into PHY registers).
3. Calibration of the Analog Front-End (AFE).
4. Cable diagnostics.

333369-009                                                                                                             119
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

5. Auto-negotiation.
6. Perform training (as required).
7. Verify error-free operation.
8. Enter steady state.

3.7.3.3.3            PHY Reset

Each PHY protects its data RAM via parity bits and its code RAM via ECC. In the event data corruption is
detected, a PHY fault interrupt is issued (see Section 3.7.3.4.1).
Each PHY supports a watchdog timer to detect a stuck micro controller. Upon failure, a PHY fault
interrupt is issued as well. Watchdog timer is set to 5 seconds by default.
The PHY is also reset on the same occasions that MAC is reset, except on software reset events for
which the PHY does not get reset. A dedicated PHY reset command is provided to software instead, via
a PHY register (Global Standard Control 1: Address 1E.0, bit F). Refer to Table 4-5.
At PHY reset events, all the PHY functionality go to reset including the micro controller except the PHY
PLLs that go to reset only at power-up.
PHY reset completion is expected to take up to 5 ms, with no MDIO access during that time. PHY reset
event causes link failure, which can take up to several seconds for resuming via auto-negotiation.

#### 3.7.3.4 PHY Interrupts

The interrupt structure of each internal PHY is hierarchical in nature, and allows masking of all
interrupts, at each of the levels of the hierarchy. The PHY has two interrupt hierarchies one is fully
clause 45 compliant, the other is vendor defined, which is intended to allow determining the cause of an
interrupt with only two status reads.
The values of these interrupt masks are visible via the internal MDIO interface in the vendor specific
areas of each MMD, and the global summary register is located in the vendor specific area of the PHY
registers (Global PHY Standard Interrupt Flags: Addresses 1E.FC00 and Global PHY Vendor Interrupt
Flags: Addresses 1E.FC01).
The interrupt structure of each PHY is such that all standards-based interrupts can be read and cleared
using a maximum of two PHY register reads.
There are two types of PHY interrupts according to their severity, normal or fatal:
 • Fatal PHY interrupts are reported together with other fatal interrupts by the ECC bit in the EICR
   register. They concern the following events:
      — ECC error when reading PHY micro controller code
      — CRC error on the second attempt to load the PHY image from the NVM
      — PHY micro controller watchdog failure
 • Normal PHY interrupts are reported by the PHY_GLOBAL_INTERRUPT bit in EICR register. They
   concern all other PHY interrupt causes.
Note:     The PHY micro controller never resets itself to a fatal interrupt or to any other event. The host
          is responsible to reset the link in such situations. The link is down until then.
Many of the interrupt causes are mostly useful to debug the PHY hardware. Therefore, they are masked
by default and unless a specific need arises should remain so.

120                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

By default, Link State Change and Global Fault are the only interrupts that should be unmasked by
software. To enable them software should set the following bits:
 • 1E.FF01.C and 1E.FF01.2 — PHY vendor mask
 • 1E.D400.4 — Enable chip fault interrupt
 • 1E.FF00.8 — Enable standard autoneg interrupt 1
Additionally, software can enable an interrupt on reset complete:
 • 1E.D400.6 — Enable reset done interrupt

3.7.3.4.1              PHY Fault Interrupt

In the event of a PHY fatal error, 1E.CC00.4 is set and an error code is written to 1E.C850. Software
should log this code and attempt to reset the PHY.
Among others, a fatal interrupt is generated on one of the following events:
 • CRC error over the PHY image when trying to load it from Flash twice without success
 • ECC error on one of the PHY’s internal memory that contains control data
 • Watchdog failure of the PHY embedded micro controller
In reaction to a fatal error, the MAC drops the link until the fatal error is cleared. Software is therefore
required to reset the link (not only the PHY) and retry to reload the PHY firmware as described in
Section 3.7.3.4.2.
If three fatal PHY interrupts are handled with no link-up event in between, the link is considered to be
down and the port must be disabled.

3.7.3.4.2              PHY Firmware Reload Flow

First read is 1E.FC00.0 = Vendor Alarm, followed by 1E.FC01, checking for bits 2 and 0 (Global Alarms
1 and 3 respectively) being set.
1. If any of them is set, check the following bits:
      • 1E.CC02.0 Watchdog Timer Alarm
      • 1E.CC00.4 Device Fault alarm (DRAM/IRAM non-correctable parity error)
      • 1E.CC02.A DRAM Parity Error alarm
      • 1E.CC02.9 Multi-bits IRAM Parity Error alarm; errors not corrected.
2. If any of them is set, initiate daisy-chain reload on the PHY that is corrupted by setting 1E.C442.0.
3. Wait for PHY interrupt and check that the reset is done by reading PHY register 1.CC02 and
   checking that bit 0 (Reset Complete) is set.
4. Resume normal operation.

333369-009                                                                                               121
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

3.7.3.4.3             Link State Change Interrupt

When an interrupt is caused by a change in the link state, bit 7.1.2 is latching low. The actual link state
can be found in register 1.E800.0.

Table 3-37. PHY Link State Registers
      Register Bits                Name                                      Description

7.C800 2:1               Connect Rate             0x0 = Reserved
                                                  0x1 = 100BASE-TX
                                                  0x2 = 1000BASE-T
                                                  0x3 = 10GBASE-T

7.C800 0                 Connect Type (Duplex)    0b = Half
                                                  1b = Full

7.C810 F                 Energy Detect            1b = Detected

7.C800 E                 Far End Device Present   1b = Present

7.C800 D:9               Connection State         0x00 =      Inactive (such as low-power or high-impedance).
                                                  0x01 =      Cable diagnostics.
                                                  0x02 =      Auto-negotiation.
                                                  0x03 =      Training (10 GbE and 1 GbE only).
                                                  0x04 =      Connected.
                                                  0x05 =      Fail (waiting to retry autoneg).
                                                  0x06 =      Test Mode.
                                                  0x07 =      Loopback Mode.
                                                  0x08 =      Reserved.
                                                  0x09 =      Reserved.
                                                  0x0A =      Reserved.
                                                  0x0B:0x10 = Reserved.

3.7.3.4.4             Reset Done Interrupt

If software has enabled the reset done interrupt, such an event generates an interrupt, which is
indicated by bit 1E.CC00.6 being set. Note that a boot complete event is simultaneous with the reset
event.

3.7.3.4.5             PHY Interrupt Handling Flow

Firmware is responsible to guarantee an operative PHY even when host is down or malfunctioning, to:
 • Provide a remote access to MC from the network.
 • Receive WoL packets.
When the host is down, interrupts from MAC blocks which are critical for MC/WoL are also handled by
the firmware:
 • ECC-Error from Security Rx/Tx blocks
 • ECC-Error from Rx-Filter
 • ECC-Error from DMA-Tx

122                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

3.7.3.4.5.1              Firmware to Software PHY Interrupt Handling Coordination

Note:        As the software device driver does not handle PHY interrupt events, the flow below is not
             implemented and is provided as a guideline if implemented in the future. The software device
             driver needs to handle PHY interrupts.
Firmware cannot be sure the host is well functioning and consequently it always handles PHY interrupts
first. Once it has completed to do its handling of PHY interrupts, firmware sets the relevant
EEMNGCTL.CFG_DONE0/1 bit and notifies the host it can start its own handling by issuing EICR.MNG
interrupt. Since the PHY interrupt flags are cleared by read, the following flow must be run by host and
firmware whenever a PHY interrupt occurs:
1. Host does not attempt to take ownership over the PHY semaphore until CFG_DONE bit is set by
   firmware.
      • In case the PHY semaphore is currently owned by the host, it stops accessing PHYINT_STATUS
        or PHY registers and releases the PHY ownership as soon as possible. Refer to Section 11.8.4
        for the maximum semaphore ownership time allowed.
2. Firmware takes ownership of PHY semaphore
3. Firmware copies the PHY interrupt flags read from PHY registers into the PHYINT_STATUS registers
      • When writing PHYINT_STATUS registers firmware must not clear bits that were not cleared by
        the host yet
4. Firmware handles the PHY interrupt by resetting the PHY (only if it is a fatal PHY interrupt)
5. Firmware sets CFG_DONE bit, releases ownership of the PHY semaphore, and issues EICR.MNG
   interrupt to host.
6. Host takes semaphore ownership over the PHY.
7. Host reads the PHYINT_STATUS registers and clears them (by writing zeros).
8. Host handles the PHY interrupts.
      • Prior to doing a PHY re-configuration that might drop the link (e.g. restart auto-negotiation),
        the host must wait until the VETO bit is read as 0b.
9. Host releases PHY semaphore.
Notes:       CFG_DONE bits are set by firmware and cleared by software. They cannot be cleared by
             firmware, and cannot be set by software.
             For simplifying drivers, firmware runs the above flow even if there is no MC or WoL. No
             wake-up of the host occurs for the fatal PHY events handled by firmware.
             PHYINT_STATUS registers and EEMNGCTL.CFG_DONE bits are reset by hardware only at
             power-up events.

#### 3.7.3.5 Cable Diagnostics

The PHY implements a powerful cable diagnostic algorithm to accurately measure all of the TDR and
TDT sequences within the group of four channels. The algorithm used transmits a pseudo-noise
sequence with an amplitude of less than 300 mV for a brief period of time during startup. From the
results of this measurement, the length of each pair, the top four impairments along the pair, and the
impedance of the cable are flagged. These measurements are accurate to ±1 m under the assumption
of the ISO 11801 cable propagation characteristics of 5.46 ns / m and are presented in the Global MMD
register map.

333369-009                                                                                             123
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  Interconnects

Cable diagnostics performed by the PHY are listed in Table 3-38 and apply to all operating rates and
scenarios.
Note:       The PHY does not distinguish more than one feature within 5 m, the dominant source of
            reflection can be recorded as a single feature.
Each PHY completes the TDR measurement within 5 seconds of activation from an MDIO accessible
register bit (1E.C470[4]. The PHY indicates that the operation is complete using the Connection State
field in Auto-Negotiation Reserved Vendor Status 1 register (7.C810.[D:9]). The PHY completes the
entire cable diagnostic functions following a single access from the host.

Table 3-38. Proprietary Cable Diagnostics
           Test                                                Feature                                          Notes

                             Distance to four reflection points for each pair.

                             Un-terminated end point (>300 ).

Distance to reflections:     Terminated > 115 or mismatch.
each of four pairs.          Terminated  100 or compliant connector (if reflection is visible.
                                                                                                       ±1 m resolution.
                             Terminated < 85 or mismatch.

                             Short circuit < 30  or mismatch.

                             Distance to short.
Pair-to-pair short.
                             Suspected pairs.

Cable diagnostics is able to detect all simple shorts on a cable. If the short is from one pair to any other
pair, it is necessary to indicate the detail of the pair-pair short connectivity. It is recommended to use a
mechanism that includes sending a signal on one pair and listening on all pairs. If a reflection is
detected (greater than the limit allowed for NEXT) on any pair other than the one with the signal, it can
be assumed that this is due to an inter-pair short.
Each PHY performs cable diagnostics at startup, prior to attempting auto-negotiation. Manual
re-running of diagnostics can also be initiated by setting bit 4 of Global Reserved Provisioning 1 register
(1E.C470).

#### 3.7.3.6 False Training Detection

Each PHY restricts the amplitude of the cable diagnostics sequence to be less than 300 mV to avoid
false detection of the training sequence by a parallel detection auto-negotiation block.

#### 3.7.3.7 Low Power Operation and Power Management

The PHY incorporates numerous features to maintain the lowest power possible. Refer to Section 5.3.1.

124                                                                                                                  333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

### 3.7.4 Ethernet Flow Control (FC)

The X550 supports flow control as defined in 802.3x, as well as the specific operation of asymmetrical
flow control defined by 802.3z. The X550 also supports Priority Flow Control (PFC), known as Class
Based Flow Control, as part of the DCB architecture.
Note:        The X550 can either be configured to receive regular FC packets or PFC packets. The X550
             does not support receiving both types of packets simultaneously.
FC is implemented to reduce receive buffer overflows, which result in the dropping of received packets.
FC also allows for local controlling of network congestion levels. This can be accomplished by sending
an indication to a transmitting station of a nearly full receive buffer condition at a receiving station.
The implementation of asymmetric FC allows for one link partner to send FC packets while being
allowed to ignore their reception. For example, not required to respond to PAUSE frames.
The following registers are defined for implementing FC. In DCB mode, some of the registers are
duplicated replicated per Traffic Class (TC), up to eight duplicates copies of the registers. If DCB is
disabled, index [0] of each register is used.
 • MAC Flow Control Register (MFLCN) — Enables FC and passing of control packets to the host.
 • Flow Control Configuration (FCCFG) — Determines mode for Tx FC (No FC vs. link-based vs.
   priority-based). Note that if Tx FC is enabled, Tx CRC by hardware should be enabled as well
   (HLREG0.TXCRCEN = 1b).
 • Flow Control Source Address Low, High (RAL[0], RAH[0])
 • Flow Control Destination Address Low, High (FCAMACL, FCAMACH) — 6-byte FC multicast address.
 • Priority Flow Control Type Opcode (PFCTOP) — Contains the type and OpCode values for PFC.
 • Flow Control Receive Threshold High (FCRTH[7:0]) — A set of 13-bit high watermarks indicating
   receive buffer fullness. A single watermark is used in link FC mode and up to eight watermarks are
   used in PFC mode.
 • Flow Control Receive Threshold Low (FCRTL[7:0]) — A set of 13-bit low watermarks indicating
   receive buffer emptiness. A single watermark is used in link FC mode and up to eight watermarks
   are used in PFC mode.
 • Flow Control Transmit Timer Value (FCTTV[3:0]) — A set of 16-bit timer values to include in
   transmitted PAUSE frame. A single timer is used in link FC mode and up to eight timers are used in
   PFC mode.
 • Flow Control Refresh Threshold Value (FCRTV) — 16-bit PAUSE refresh threshold value (in legacy FC
   FCRTV[0] must be smaller than FCTTV[0]).

333369-009                                                                                                125
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                              Interconnects

#### 3.7.4.1 MAC Control Frames and Reception of Flow Control

                        Packets

3.7.4.1.1               MAC Control Frame — Other than FC

The IEEE specification reserved the EtherType value of 0x8808 for MAC control frames, which are listed
in Table 3-39.

Table 3-39. MAC Control Frame Format
         Field                                                         Description

DA                       The Destination Address field can be an individual or multicast (including broadcast) address.
                         Permitted values for the Destination Address field can be specified separately for a specific control
                         OpCode such as FC packets.

SA                       Port Ethernet MAC Address (six bytes).

Type                     0x8808 (two bytes).

Opcode                   The MAC control OpCode indicates the MAC control function.

Parameters               The MAC control Parameters field must contain MAC control OpCode-specific parameters. This field can
                         contain none, one, or more parameters up to a maximum of minFrameSize = 20 bytes.

Reserved field = 0x00    The Reserved field is used when the MAC control parameters do not fill the fixed length MAC control
                         frame.

CRC                       Four bytes.

3.7.4.1.2               Structure of 802.3X FC Packets

802.3X FC packets are defined by the following three fields (see Table 3-40):
1. A match on the six-byte multicast address for MAC control frames or a match to the station address
   of the device (Receive Address Register 0). The 802.3x standard defines the MAC control frame
   multicast address as 01-80-C2-00-00-01.
2. A match on the Type field. The Type field in the FC packet is compared against an IEEE reserved
   value of 0x8808.
3. A match of the MAC control Opcode field has a value of 0x0001.
Frame-based FC differentiates XOFF from XON based on the value of the PAUSE Timer field. Non-zero
values constitute XOFF frames while a value of zero constitutes an XON frame. Values in the Timer field
are in units of pause quanta (such as slot time). A pause quanta lasts 64 byte times, which is converted
into an absolute time duration according to the line speed.
Note:        XON frame signals the cancellation of the pause from that was initiated by an XOFF frame.
             Pause for zero pause quanta.

Table 3-40. 802.3X Packet Format
         Field                                                         Description

DA                       01_80_C2_00_00_01 (6 bytes).

SA                       Port Ethernet MAC Address (6 bytes).

Type                     0x8808 (2 bytes).

Opcode                   0x0001 (2 bytes).

Time                     XXXX (2 bytes).

126                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-40. 802.3X Packet Format [continued]
         Field                                                     Description

Pad                      42 bytes.

CRC                      4 bytes.

3.7.4.1.3              Priority Flow Control

DCB introduces support for multiple TCs assigning different priorities and bandwidth per TC. Link-level
Flow Control (PAUSE) stops all the TCs. Priority Flow Control (PFC), known as Class Based Flow Control
or CBFC, allows more granular Flow Control on the Ethernet link in a DCB environment as opposed to
the PAUSE mechanism defined in 802.3X.
PFC is implemented to prevent the possibility of receive packet buffers overflow. Receive packet buffers
overflow results in the dropping of received packets for a specific TC. Implement PFC by sending a timer
indication to the transmitting station TC (XOFF) of a nearly full receive buffer condition at the X550. At
this point the transmitter stops transmitting packets for that TC until the XOFF timer expires or a XON
message is received for the stopped TC.
Similarly, once the X550 receives a priority-based XOFF it stops transmitting packets for that specific TC
until the XOFF timer expires or XON packet for that TC is received.

                            Data to      802.3                                                 802.3
                             MAC        MAC TX                                                MAC Rx

                                                                 XOFF blocks traffic on
                                                                    the entire link

Figure 3-7.      802.3X Link Flow Control (PAUSE)

Link flow control (802.3X) causes all traffic to be stopped on the link. DCB uses the same mechanism of
FC but provides the ability to do PFC on TCs, as shown in Figure 3-8.

333369-009                                                                                             127
                                      Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Interconnects

                                Data to      802.3                                                                         802.3
                                 MAC        MAC TX                                                                        MAC Rx

                                                               Class based XOFF blocks traffic on a
                                                               specific traffic class and not the entire link

Figure 3-8.         Priority Flow Control

Table 3-41. Packet Format for PFC
            Field                                                           Description

DA                              01_80_C2_00_00_01 (6 bytes).

SA                              Port Ethernet MAC Address (6 bytes).

Type                            0x8808 (2 bytes).

Opcode                          0x0101 (2 bytes).

Priority Enable Vector          0x00XX (2 bytes).

Timer 0                         XXXX (2 bytes).

Timer 1                         XXXX (2 bytes).

Timer 2                         XXXX (2 bytes).

Timer 3                         XXXX (2 bytes).

Timer 4                         XXXX (2 bytes).

Timer 5                         XXXX (2 bytes).

Timer 6                         XXXX (2 bytes).

Timer 7                         XXXX (2 bytes).

Pad                             26 bytes.

CRC                             4 bytes.

Table 3-42. Format of Priority Enable Vector
                                                                           ms octet                                  ls octet

Priority enable vector definition                                              0                                e[7]...e[n]...e[0]

e[n] =1 => time (n) valid
e[n] =0 => time (n) invalid

The Priority Flow Control Type Opcode (PFCTOP) register contains the type and OpCode values for PFC.
These values are compared against the respective fields in the received packet.

128                                                                                                                             333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Each of the eight timers refers to a specific User Priority (UP), such as Timer 0 refers to UP 0, etc. The
X550 binds a UP and timer to one of its TCs according to the UP-to-TC binding tables. Refer to the
RTTUP2TC register for the binding of received PFC frames to Tx TCs, and to the RTRUP2TC register for
the binding of transmitted PFC frames to Rx TCs.
Tx manageability traffic is bound to one the TCs via the MNGTXMAP register, and should thus be paused
according to RTTUP2TC mapping when receiving PFC frames.
When a PFC frame is formatted by the X550, the same values are replicated into every Timer field and
priority enable vector bit of all the UPs bound to the associated TC. These values are configured in the
RTRUP2TC register.
The following rule is applicable for the case of multiple UPs that share the same TC (as configured in the
RTTUP2TC register). When PFC frames are received with different timer values for the previously
mentioned UPs, the traffic on the associated TC must be paused by the highest XOFF timer’s value.

3.7.4.1.4               Operation and Rules

The X550 operates in either link FC or in PFC mode. Note that enabling both modes concurrently is not
allowed:
 • Link FC is enabled by the RFCE bit in the MFLCN register.
 • PFC is enabled per UP by the corresponding RPFCE bit in the MFLCN register, and globally by
   MFLCN.RPFCM bit.
Note:        Link FC capability must be negotiated between link partners via the auto-negotiation process.
             The PFC capability is negotiated via some higher level protocol and the resolution is usually
             provided to the driver by the DCB management agent. It is the driver’s responsibility to
             reconfigure the link FC settings (including RFCE and PRFCE) after the auto-negotiation
             process was resolved.
Note:        Receiving a link FC frame while in PFC mode might be ignored or might pause TCs in an
             unpredictable manner. Receiving a PFC frame while in link FC mode is ignored. Flow control
             events that are ignored do not increment any flow control statistics counters.
Once the receiver has validated the reception of an XOFF, or PAUSE frame, the device performs the
following:
 • Increment the appropriate statistics register(s)
 • Initialize the pause timer based on the packet's PAUSE Timer field (overwriting any current timer’s
   value)
     — For PFC, this is done per TC. If several UPs are associated with a TC, the device sets the timer
       to the maximum value among all enabled Timer fields associated with the TC.
 • Disable packet transmission or schedule the disabling of transmission after the current packet
   completes.
     — For PFC, this is done per paused TC
     — Tx manageability traffic is bound to a specific TC as defined in the MNGTXMAP register, and is
       thus paused when its TC is paused
Resumption of transmission can occur under the following conditions:
 • Expiration of the PAUSE timer
     — For PFC, this is done per TC

333369-009                                                                                             129
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                  Interconnects

 • Receiving an XON frame (a frame with its PAUSE timer set to 0b)
       — For PFC, this is done per TC
Both conditions clear the relevant TXOFF status bits in the Transmit Flow Control Status (TFCS) register
and transmission can resume. Hardware records the number of received XON frames.

3.7.4.1.5             Timing Considerations

When operating at 10 GbE line speed, the X550 must not begin to transmit a (new) frame more than 74
pause quanta after receiving a valid Link XOFF frame, as measured at the wires (a pause quantum is
512 bit times).
When operating at 1 GbE line speed, the X550 must not begin to transmit a (new) frame more than 2
pause quanta after receiving a valid Link XOFF frame, as measured at the wires.
When operating at 100 Mb/s line speed, the X550 must not begin to transmit a (new) frame more than
1 pause quantum plus 64 bit times after receiving a valid Link XOFF frame, as measured at the wires.
The 802.1Qbb draft 2, proposes that the tolerated response time for Priority XOFF frames are the same
as Link XOFF frames with extra budget of 2 pause quanta. This extra budget is aimed to compensate
the fact that decision to stop new transmissions from a specific TC must be taken earlier in the transmit
data path than for the Link Flow Control case.

#### 3.7.4.2 PAUSE and MAC Control Frames Forwarding

Two bits in the Receive Control register control transfer of PAUSE and MAC control frames to the host.
These bits are Discard PAUSE Frames (DPF) and Pass MAC Control Frames (PMCF). Note also that any
packet must pass the L2 filters as well.
 • The DPF bit controls the transfer of PAUSE packets to the host. The same policy applies to both link
   FC and PFC packets as listed in Table 3-43. Note that any packet must pass the L2 filters as well.
 • The Pass MAC Control Frames (PMCF) bit controls the transfer of non-PAUSE packets to the host.
   Note that when link FC frames are not enabled (RFCE = 0b), link FC frames are considered as MAC
   control frames for this case. Similarly, when PFC frames are not enabled (RPFCM = 0b), PFC frames
   are considered as MAC control frames as well.
Note:      When virtualization is enabled, forwarded control packets are queued according to the regular
           switching procedure defined in Section 7.8.3.4.

Table 3-43. Transfer of PAUSE Packet to Host (DPF Bit)
  RFCE      RPFCM     DPF                Link FC Handling                            PFC Handling

      0b      0b       X    Treat as MAC control (according to PMCF   Treat as MAC control (according to PMCF
                            setting).                                 setting).

      1b      0b      0b    Accept.                                   Treat as MAC control (according to PMCF
                                                                      setting).

      1b      0b      1b    Reject.                                   Treat as MAC control (according to PMCF
                                                                      setting).

      0b      1b      0b    Treat as MAC control (according to PMCF   Accept.
                            setting).

      0b      1b      1b    Treat as MAC control (according to PMCF   Reject.
                            setting).

      1b      1b       X    Unsupported setting.                      Unsupported setting.

130                                                                                                     333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

#### 3.7.4.3 Transmitting PAUSE Frames

The X550 generates PAUSE packets to ensure there is enough space in its receive packet buffers to
avoid packet drop. The X550 monitors the fullness of its receive FIFOs and compares it with the
contents of a programmable threshold. When the threshold is reached, the X550 sends a PAUSE frame.
The X550 supports both link FC and PFC — but not both concurrently. When DCB is enabled, it only
sends PFC, and when DCB is disabled, it only sends link FC.
Note:        Similar to receiving flow control packets previously mentioned, software can enable FC
             transmission by setting the FCCFG.TFCE field only after it is negotiated between the link
             partners (possibly by auto-negotiation).

3.7.4.3.1               Priority Flow Control (PFC)

The X550 operates in either a link 802.3X compliant mode or in a Priority Flow Control mode, but not in
both at the same time.
The same watermarks mechanism is used for PFC and for 802.3X FC to determine when to send XOFF
and XON packets. When PFC is used in the receive path, priority PAUSE packets are sent instead of
802.3X PAUSE packets. The format of priority PAUSE packets is described in Section 3.7.4.1.3.
Specific considerations for generating PFC packets:
 • When a PFC packet is sent, the packet sets all the UPs that are associated with the relevant TC
   (UP-to-TC association in receive is defined in RTRUP2TC register).

3.7.4.3.2               Operation and Rules

The TFCE field in the Flow Control Configuration (FCCFG) register enables transmission of PAUSE
packets as well as selects between the link FC mode and the PFC mode.
The content of the Flow Control Receive Threshold High (FCRTH) register determines at what point the
X550 transmits the first PAUSE frame. The X550 monitors the fullness of the receive FIFO and
compares it with the contents of FCRTH. When the threshold is reached, the X550 sends a PAUSE frame
with its pause time field equal to FCTTV.
At this time, the X550 starts counting an internal shadow counter (reflecting the pause time-out
counter at the partner end). When the counter reaches the value indicated in FCRTV register, then, if
the PAUSE condition is still valid (meaning that the buffer fullness is still above the low watermark), an
XOFF message is sent again.
Once the receive buffer fullness reaches the low water mark, the X550 sends an XON message (a
PAUSE frame with a timer value of zero). Software enables this capability with the XONE field of the
FCRTL.
The X550 sends a PAUSE frame if it has previously sent one and the FIFO overflows. This is intended to
minimize the amount of packets dropped if the first PAUSE frame did not reach its target.

333369-009                                                                                               131
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                    Interconnects

3.7.4.3.3               Flow Control High Threshold — FCRTH

The X550 sends a PAUSE frame when the Rx packet buffer is full above the high threshold. The
threshold should be large enough to overcome the worst case latency from the time that crossing the
threshold is sensed until packets are not received from the link partner.
Referring to Annex O of IEEE802.1Qbb rev 2.3, worst case latency depends on two parameters:
1. Maximum frame size over the traffic class for which FCRTH is computed. It is referred as
   MaxFrame(TC).
2. Maximum frame size over the link (all traffic classes altogether). It is referred as MaxFrame(link).
Three values are envisaged for MaxFrame:
 • 1.5 KB (Ethernet - Jumbo disabled)
 • 2.2 KB (FCoE)
 • 9.5 KB (Jumbo enabled)
Worst case latency, which is referred as Standard Delay Value (Std DV), is given by:
      Std DV = MaxFrame(TC) + MaxFrame(link) + PFC Frame + 2 x Cable Delay + 2 x Interface Delay + Higher
      Layer Delay x Sec Y Transmit Delay

      Std DV (bit time units) = MaxFrame(TC) + MaxFrame(link) + 672 + 2 x 5,556 + 2 x (25,600 + 8,192 + 2 x
      2,048) + 6,144 x (MaxFrame(link) + 3,200)

MaxFrame(TC) term and MaxFrame(link) term included in Sec Y Transmit Delay correspond to worst
case scenarios issued by the link partner. All other terms in Std DV formula must take in account worst
case incoming traffic pattern which would lead to worst case buffer utilization as per the internal
architecture of Rx packet buffer in the X550.
Internal architecture of the Rx packet buffer has the following restrictions:
1. Any packet starts at 32 byte aligned address.
2. Any packet has an internal status of 32 bytes. As a result, the Rx packet buffer is used at worst
   conditions when the Rx packet includes 65 bytes that are posted to the host memory. Assuming
   that the CRC bytes are not posted to host memory, in the worst case the Rx packet buffer can be
   filled at 1.44 higher rate than the wire speed (69-byte packet including CRC + 8-byte preamble +
   12-byte back-to-back IFS consumes 4 x 32 bytes = 128 bytes on the Rx packet buffer).
3. An additional packet from the concerned traffic class may be inserted into the Rx packet buffer due
   to the internal loopback switch *just before* it is decided to issue XOFF to the link partner
It leads to the below revised formula for the X550:
      X550 DV (bit time units) = 1.44 x [(MaxFrame(link) + 672 + 2 x 5,556 + 2 x (25,600 + 8,192 + 2 x 2,048) +
      6,144 x (3,200)] + MaxFrame(TC) + MaxFrame(TC) x MaxFrame(link)

132                                                                                                   333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

FCRTH must be set to the size of the Rx packet buffer allocated to the traffic class minus the X550 DV.

Table 3-44. X550 Delay Values (DV) Used for FCRTH
