## 5.7 Thermal Management

### 5.7.1 General

The X550’s thermal management solution includes an on-die diode and an on-die thermal sensor used
to:
 • Monitor the die temperature (junction temperature) by an external device. Refer to Section 12.5 for
   more details.
 • Indicate junction temperature as well as being programmed to indicate that temperature thresholds
   (such as trip points) are reached.
 • The thermal sensor indications can be monitored by:
      — The MC (see Section 5.7.2)
      — Autonomously by the X550 in NVM-based mode (see Section 5.7.3).
      — By host software driver in NVM-based mode (see Section 5.7.3.1).
Thermal sensor registers are generally accessible only from MDIO of PHY 0.
Note:     Host software might read these registers but must not change their programming. PHY
          registers remain accessible even after the PHY has been shut down by a thermal sensor
          event.

212                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Power Management and Delivery

### 5.7.2 MC-Based Mode

The thermal sensor behavior relative to the thresholds/actions configured by MC is referred as the TS
MC-based mode. It can be used by the MC to control an active heat sink or the fan operation if present
on the board.
This mode can work together with the NVM mode, where the NVM mode is used by the software device
driver, and this mode is used by the MC. Each mode uses different thresholds in the PHY.
The MC-based mode is configured via the Set Thermal Sensor Commands. Refer to Section 11.5.11.1.9
(Legacy SMBus mode) and Section 11.6.3.19 (NC-SI mode).
Thermal sensor event notifications can be issued:
 • Via an AEN over NC-SI (see Section 11.6.3.20.1)
 • Via an SMBus alert (see Section 11.5.6).
 • Via SDP1 output pin of LAN port 1 indication.

### 5.7.3 NVM-Based Mode

The thermal sensor behavior relative to the threshold configured via NVM is referred as the TS NVM-
based mode. It is mainly useful for non-managed environments or when the MC does not support the
thermal sensor commands. However, this mode can also be enabled in parallel to the TS MC-based
mode, as a back up mode relying on a catastrophic threshold, which must be set beyond the thresholds
configured by the MC to avoid any interference between the two defined modes (NVM based and MC
based).
It is configured as follows:
 • TS NVM-based mode is enabled via setting the TS NVM-based Mode Enable bit to 1b in the Common
   Firmware Parameters word (Section 6.2.16).
 • Program the PHY NVM section as follows:
     — The thermal threshold should be set to 107 °C, by the PHY provisioning register 1E.C421
       (Section 10.6.11) and 1E.C423 (Section 10.6.13) both set to 0x6B00.
     — Enable the high temperature failure alarm to assert the PHY Global Interrupt, via PHY
       provisioning register 1E.D400 bits E:B set to 1000b.
 • Optionally, if on-board thermal alerts are required, set the SDP1 pin of LAN port 0 as an output pin
   that asserts on the thermal sensor event, via the SDP1_IODIR bit (bit 9) set to 1b, the
   SDP1_NATIVE bit (bit 17) set to 0b, and the SDP1_FUNCTION bit (bit 25) set to 1b in the SDP
   Control word (Offset 0x20).
 • Recovering from a thermal sensor PHY power down event in this mode requires a device power
   cycle.
 • The host can check whether the TS NVM-based mode is enabled or not by reading bit 0 in FWSM
   register.

333369-009                                                                                          213
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                       Power Management and Delivery

#### 5.7.3.1 Thermal Sensor (TS) Monitoring by Host Software

When operating in NVM mode, thermal events can be monitored by the host device driver. The thermal
sensor is configured by the NVM and should not be changed by host software. The junction temperature
can be read from the Global Thermal Status 1: Address 1E.C820 register (Section 10.6.29).
Note:        A guard band of ±3 °C should be taken over thermal sensor temperature indication.
TS event notifications can be issued via:
 • An interrupt to the host (via EICR.TS bit 23).
 • SDP1 output pin of LAN port 0 indication.
Note:        TS events are enabled by default and might be spurious. Host software should react TS
             events only if TS NVM-based mode is enabled (Section 5.7.3).
Note:        To get an indication through SDP1, the NVM setting of SDP1 should be configured as
             described in Section 5.7.3.

### 5.7.4 Thermal Sensor Control

The temperature sensor can be manually controlled by the host device driver through the MDIO, by
setting the Temperature Sense Override bit to 1b.
Once the temperature sensor has performed the read, it asserts the Temperature Ready bit to 0b (see
Global Thermal Status 2: Address 1E.C821 — Section 10.6.30). The temperature data can then be read
from the Temperature [F:0] bits (see Common Thermal Status 1: Address 1E.2C820 —
Section 10.6.29).
Note:        Take in account that the Temperature Sense Ready bit toggles a number of times according to
             the number of samples configured in Temperature Sense Sample Configuration field
             (1E.2825) and to the wait time between samples configured in Temperature Sense Wait
             Configuration field (1E.2824).

### 5.7.5 Thermal Sensor Characteristics

Table 5-6.        Thermal Sensor Characteristics
        Parameter             Min                Max                                      Comment

Range                         0 °C              125 °C   Temperature is reported as 16-bit unsigned decimal value.

Resolution                      1/256 °C per LSB         For the least significant bit.

Accuracy                             +/- 3 °C

Conversion time                       11 ms

214                                                                                                          333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Chapter 6                     Non-Volatile Memory Map
