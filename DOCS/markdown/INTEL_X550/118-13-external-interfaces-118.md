## 1.3 External Interfaces

                                               PCIe v3.0 (2.5GT/s, 5GT/s or 8GT/s) x4
                                                   PCIe v3.0 (2.5GT/s, 5GT/s) x8

                       DFT I/F                                                                        Serial Flash I/F
                                                         Host Interface

                      SDP0[3:0]            MAC (LAN 0)                      MAC (LAN 1)
                                                                                                        SMBus I/F
                      SDP1[3:0]

                       LEDs_0                 PHY                                 PHY                    NC‐SI I/F

                       LEDs_1
                                    X550

                                                 10GBASE‐T_0                            10GBASE‐T_1

Figure 1-2.   X550 External Interfaces Diagram

### 1.3.1 PCIe Interface

The X550 supports PCIe v3.0 (2.5 GT/s, 5 GT/s or 8 GT/s). See Section 2.2.1 for full pin description and
Section 12.4.5 for interface timing characteristics.

### 1.3.2 Network Interfaces

Two independent 10GBASE-T interfaces are used to connect the two X550 ports to external devices.
Each 10GBASE-T interface can operate at any of the following speeds:
 • 10 Gb/s, 10GBASE-T mode
 • 5 Gb/s, NBASE-T mode
 • 2.5 Gb/s, NBASE-T mode
 • 1 Gb/s, 1000BASE-T mode
 • 100 Mb/s, 100BASE-TX mode
 • Refer to Section 2.2.2 for full-pin descriptions. For the timing characteristics of those interfaces,
   refer to the relevant external specifications listed in Section 12.4.6.

36                                                                                                                       333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Introduction

### 1.3.3 Serial Flash Interface

The X550 uses an external SPI serial interface to a Flash device, also referred to as Non-Volatile
Memory (NVM). The X550 supports serial Flash devices with up to 4 MB of memory.
The X550 implements a signed firmware authenticated capability to verify the firmware and critical
device settings with built-in detection of corruption. This is done at the time of firmware updates. See
Section 3.4.1.1, “NVM Protection” for details.

### 1.3.4 SMBus Interface

SMBus is an optional interface for pass-through and/or configuration traffic between an external
Manageability Controller (MC) and the X550.
The X550's SMBus interface supports a standard SMBus, up to a frequency of 1 MHz. Refer to
Section 2.2.4 for full-pin descriptions and Section 12.4.4.3 for timing characteristics of this interface.

### 1.3.5 NC-SI Interface

NC-SI is an optional interface for pass-through traffic to and from an MC. The X550 meets the NC-SI
version 1.0.0 specification.
Refer to Section 2.2.5 for the pin descriptions, and Section 11.6 for NC-SI programming.

### 1.3.6 Software-Definable Pins (SDP) Interface

                  (General-Purpose I/O)
The X550 has four SDP pins per port that can be used for miscellaneous hardware or software-
controllable purposes. These pins can each be individually configured to act as either input or output
pins. Via the SDP pins, the X550 can support IEEE1588 auxiliary device connections and other
functionality. For more details on the SDPs see Section 3.5 and the ESDP register (Section 8.2.2.1.4).

### 1.3.7 LED Interface

The X550 implements four output drivers intended for driving external LED circuits per port. Each of the
four LED outputs can be individually configured to select the particular event, state, or activity, which is
indicated on that output. In addition, each LED can be individually configured for output polarity as well
as for blinking versus non-blinking (steady-state) indications.
The configuration for LED outputs is specified via the LEDCTL register (see Section 8.2.2.1.10). In
addition, the hardware-default configuration for all LED outputs can be specified via an NVM field (see
Section 6.2.5.5 and Section 6.2.5.6), thereby supporting LED displays configured to a particular OEM
preference. For more details on the LEDs see Section 3.6.

333369-009                                                                                                   37
                                 Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                   Introduction
