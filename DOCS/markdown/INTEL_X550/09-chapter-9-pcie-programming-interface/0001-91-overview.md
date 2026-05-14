## 9.1 Overview

The X550 is a multi-function device with the following functions:
 • LAN 0
 • LAN 1
Different parameters affect how LAN functions are exposed on PCIe.
Both functions contain the following regions of the PCI configuration space (some of them are enabled
by NVM settings as detailed in the following sections):
 • Mandatory PCI configuration registers - Section 9.2.2
 • Legacy PCI capabilities - Section 9.2.3
     — Power management capabilities
     — MSI / MSI-X capabilities
     — Vital Product Data (VPD) capability
 • PCIe extended capabilities - Section 9.2.4
     — Advanced Error Reporting (AER)
     — Serial ID
     — Alternate requester ID.
     — Single root IOV
     — Latency Tolerance Reporting
     — TPH Requester
     — Access Control Services
     — Secondary PCI Express

333369-009                                                                                         795
                                 Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                 PCIe Programming Interface

### 9.1.1 Register Attributes

Table 9-1 lists the register attributes used in this section.

Table 9-1.     Register Attribute Descriptions
      Type                                                         Description

RO             Read-Only register
               Register bits are read-only and cannot be altered by software.

RW             Read/Write register
               Register bits are read-write and can be either set or reset.

RW1C           Read-only status — Write 1b to Clear status register
               Writing a 0b to RW1C bits has no effect.

ROS            Read-Only register with Sticky bits
               Register bits are read-only and cannot be altered by software. Bits are not cleared by reset and can only be reset
               with the PWRGOOD signal. Devices that consume AUX power are not allowed to reset sticky bits when AUX power
               consumption (either via AUX power or PME Enable) is enabled.

RWS            Read/Write register with Sticky bits
               Register bits are read-write and can be either set or reset by software to the desired state. Bits are not cleared by
               reset and can only be reset with the PWRGOOD signal. Devices that consume AUX power are not allowed to reset
               sticky bits when AUX power consumption (either via AUX power or PME Enable) is enabled.

RW1CS          Read-only status — Write 1b to Clear status register
               Register bits indicate status when read, a set bit, indicating a status event, can be cleared by writing a 1b to it.
               Writing a 0b to RW1C bits has no effect. Bits are not cleared by reset and can only be reset with the PWRGOOD
               signal. Devices that consume AUX power are not allowed to reset sticky bits when AUX power consumption (either
               via AUX power or PME Enable) is enabled.

HwInit         Hardware Initialized
               Register bits are initialized by firmware or hardware mechanisms such as pin strapping or serial NVM. Bits are
               read-only after initialization and can only be reset (for write-once by firmware) with the PWRGOOD signal.

RsvdP          Reserved and Preserved
               Reserved for future read/write implementations; software must preserve value read for writes to these bits.

RsvdZ          Reserved and Zero
               Reserved for future RW1C implementations; software must use 0b for writes to these bits.

796                                                                                                                      333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface
