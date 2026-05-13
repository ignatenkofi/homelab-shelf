## 9.2 PCIe Register Map

### 9.2.1 PCIe Configuration Space Summary

Table 9-2 lists the PCIe configuration registers while their detailed description is given in the sections
that follow. PCI configuration fields in the summery table are presented by the following marking:
 • Fields that have meaningful default values are indicated in parenthesis — (value).
 • Dotted fields indicates the same value for both LAN functions
 • Light-blue fields indicate read-only fields (loaded from the NVM)
 • Magenta fields indicate hard-coded values.
 • Other fields contain RW attributes.

Table 9-2.      PCI Configuration Registers Map - LAN Functions
     Section        Byte Offset             Byte 3                     Byte 2                     Byte 1                 Byte 0

                   0x0                                 Device ID                                           Vendor ID

                   0x4                               Status Register                                  Command Register

                   0x8                                 Class Code (0x020000/0x010000)                                  Revision ID

                                                              Header Type (0x0/                                   Cache Line Size
                   0xC                  Reserved                                             Latency Timer
                                                                   0x80)                                              (0x0)

                   0x10                                                  Base Address Register 0

                   0x14                                                  Base Address Register 1

                   0x18                                                  Base Address Register 2

Mandatory PCI      0x1C                                                  Base Address Register 3
Register           0x20                                                  Base Address Register 4

                   0x24                                                  Base Address Register 5

                   0x28                                                CardBus CIS pointer (0x0000)

                   0x2C                              Subsystem ID                                    Subsystem Vendor ID

                   0x30                                                Expansion ROM Base Address

                   0x34                                             Reserved                                       Cap Ptr (0x40)

                   0x38                                                           Reserved

                                                                                              Interrupt Pin        Interrupt Line
                   0x3C            Max Latency (0x00)          Min Grant (0x00)
                                                                                             (0x01...0x04)             (0x00)

                   0x40...0x47                                         Power Management Capability

                   0x50...0x67                                                  MSI Capability
PCI / PCIe
                   0x70...0x7B                                               MSI-X Capability
Capabilities
                   0xA0...0xDB                                                  PCIe Capability

                   0xE0...0xE7                                                  VPD Capability

333369-009                                                                                                                           797
                                  Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                PCIe Programming Interface

Table 9-2.      PCI Configuration Registers Map - LAN Functions [continued]
      Section      Byte Offset          Byte 3                   Byte 2                     Byte 1                    Byte 0

                  0x100...0x12B                                           AER Capability

                  0x140...0x14B                                         Serial ID Capability

                  0x150...0x157                                            ARI Capability

Extended PCIe     0x160...0x19F                                          SR-IOV Capability
Configuration     0x1A0...0x1AB                                           TPH Capability

                  0x1B0...0x1B7                                           ACS Capability

                  0x1C0...0x1C7                                            LTR Capability

                  0x1D0...0x1E3                           Secondary PCI Express Extended Capability

Table 9-3.      PCIe Configuration Registers Map - Dummy Function
      Section       Byte Offset           Byte 3                     Byte 2                     Byte 1                 Byte 0

                  0x0                                Device ID                                           Vendor ID

                  0x4                              Status Register                                  Command Register

                  0x8                                     Class Code (0xFF0000)                                      Revision ID

                                                                 Header Type                                    Cache Line Size
                  0xC                    Reserved                                        Latency Timer
                                                                 (0x0/0x80)                                         (0x0)

                  0x10                                                 Base Address Register 0

                  0x14                                             Base Address Register 1 (0x0)

                  0x18                                             Base Address Register 2 (0x0)

Mandatory PCI     0x1C                                             Base Address Register 3 (0x0)
Register
                  0x20                                             Base Address Register 4 (0x0)

                  0x24                                             Base Address Register 5 (0x0)

                  0x28                                             CardBus CIS pointer (0x0000)

                  0x2C                        Subsystem Device ID                                  Subsystem Vendor ID

                  0x30                                         Expansion ROM Base Address (0x0)

                  0x34                                            Reserved                                       Cap Ptr (0x40)

                  0x38                                                          Reserved

                                                                                                                 Interrupt Line
                  0x3C               Max Latency (0x00)      Min Grant (0x00)         Interrupt Pin (0x00)
                                                                                                                     (0x00)

                  0x40...0x47                                        Power Management Capability
PCI / PCIe
                  0xA0...0xDB                                                 PCIe Capability
Capabilities
                  0xE0...0xE7                                                 VPD Capability

                  0x100...0x12B                                               AER Capability
Extended PCIe
                  0x140...0x14B                                          Serial ID Capability
Configuration
                  0x1B0...0x1B7                                               ACS Capability

798                                                                                                                      333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.1.1 Sharing Among PCI Functions

The X550 supports multiple PCI functions. As each function exposes a PCIe configuration space, each
register and each field is either shared among the functions or is replicated per each PCI function. In
each section a table summarizes configuration sharing of the registers described in this section. Also,
the description of each field describes special considerations regarding configuration sharing.

### 9.2.2 Mandatory PCI Configuration Registers

Table 9-4.          Configuration Sharing of PCI Configuration Space
        Field                    Sub-field          Shared?     Replicated?                    Comments

Vendor ID                Vendor ID                      x

Device ID                Device ID                                   x

                         I/O Access Enable                           x        Issue UR per PF if disabled.

                         Memory Access Enable                        x        Issue UR per PF if disabled.

                         Bus Master Enable                           x
Command Register
                         Parity Error Response                       x        Enables certain error reporting per PF.

                         SERR# Enable                                x        Controls error reporting per PF.

                         Interrupt Disable                           x        Selection of interrupt method per PF.

                         Interrupt Status                            x

                         Capabilities List              x                     Hard-wired to 1b.

                         Data Parity Reported /
                                                                     x        Reports poisoned packets per PF.
                         Master Data Parity Error

Status Register          Signaled Target Abort                       x        Reports Completer Abort per PF.

                         Received Target Abort                       x        Reports receiving a Completer Abort per PF.

                         Received Master Abort                       x        Reports receiving an UR per PF.

                         Signaled System Error                       x        Reports Fatal / non-fatal message per PF.

                         Detected Parity Error                       x        Reports receiving a poisoned TLP per PF.

Revision Register                                       x

Class Code Register                                                  x        Per function type.

Cache Line Size
                                                                     x        Does not affect device behavior.
Register

Latency Timer                                           x                     Hard-wired to 00h in PCIe.

Header Type Register                                    x

BIST                                                    x                     Not supported (00h).

                         Memory BAR                                  x

BARs                     I/O BAR                                     x

                         MSI-X BAR                                   x        See Section 9.2.3.3, “MSI-X Capability”.

I/O BAR mapping          IOADDR, IODATA                              x

Subsystem Vendor ID                                     x

Subsystem ID                                            x

333369-009                                                                                                                799
                                      Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                       PCIe Programming Interface

Table 9-4.         Configuration Sharing of PCI Configuration Space [continued]
         Field                Sub-field         Shared?     Replicated?                    Comments

Expansion ROM                                                    x

Cap_Ptr Register                                    x

Interrupt Line Register                                          x        Just store the register value.

Interrupt Pin Register                                           x        Separate interrupt number (A-D) per PF.

Min. Grant                                          x

Max Latency                                         x

#### 9.2.2.1 Vendor ID Register (0x0; RO)

This is a read-only register that has the same value for all PCI functions. It identifies unique Intel
products. The value of this field is loaded from the PCI_VENDORID register loaded from NVM. The
default value, if not loaded, is 0x8086.

#### 9.2.2.2 Device ID Register (0x2; RO)

This is a read-only register that identifies individual X550 PCI functions. Both ports have the same
default value equals to 0x1562, and can be auto-loaded from the NVM during initialization with different
values for each port as well as the dummy function (See Section 4.4 for dummy function relevance).
The device ID values available for different the X550 SKUs are:
 • 0x1563: X550 LOM & NIC. This is the value used for LOM & Sage Pond NIC.
 • 0x1564: X550 VF for Hyper-V. This is the value used for VFs under Hyper-V (windows 8). This value
   is never exposed as part of the hardware configuration space.
 • 0x1565: X550 VF for non-Hyper-V. This is the value used for VFs under “other” virtual
   environments.

800                                                                                                        333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.2.3 Command Register (0x4; RW)

Shaded bits are not used by this implementation and are hard-wired to 0b. Each function has its own
Command register. Unless explicitly specified, functionality is the same in both functions.

 Bit(s)      Init.                                                      Description

   0          0b     I/O Access Enable
                     If I/O BAR is not requested, this bit is hard-wired to zero.
   1          0b     Memory Access Enable
   2          0b     Enable Mastering
                     Also named Bus Master Enable (BME).
                      • LAN functions RW field.
                      • Dummy function RO as zero field.
   3          0b     Special Cycle Monitoring
                     Hard-wired to 0b.
   4          0b     MWI Enable
                     Hard-wired to 0b.
   5          0b     Palette Snoop Enable
                     Hard-wired to 0b.
   6          0b     Parity Error Response
   7          0b     Wait Cycle Enable
                     Hard-wired to 0b.
   8          0b     SERR# Enable
   9          0b     Fast Back-to-Back Enable
                     Hard-wired to 0b.
   10         0b     Interrupt Disable
                     When set, devices are prevented from generating legacy interrupt messages.
 15:11       0x0     Reserved.

333369-009                                                                                        801
                                         Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

#### 9.2.2.4 Status Register (0x6; RO)

Shaded bits are not used by this implementation and are hard-wired to 0b. Each function has its own
Status register. Unless explicitly specified, functionality is the same in both functions.

 Bit(s)     Init.     Type                                                   Description

   2:0      000b               Reserved.
      3       0b        RO     Interrupt Status1
      4       1b        RO     New Capabilities
                               Indicates that a device implements extended capabilities. The X550 sets this bit and implements a
                               capabilities list to indicate that it supports PCI Power Management, Message Signaled Interrupts
                               (MSI), Enhanced Message Signaled Interrupts (MSI-X), VPD and the PCIe extensions.
      5       0b               66 MHz Capable
                               Hard-wired to 0b.
      6       0b               Reserved.
      7       0b               Fast Back-to-Back Capable
                               Hard-wired to 0b.
      8       0b      RW1C     Data Parity Reported
  10:9       00b               DEVSEL Timing
                               Hard-wired to 0b.
   11         0b      RW1C     Signaled Target Abort
   12         0b      RW1C     Received Target Abort
   13         0b      RW1C     Received Master Abort
   14         0b      RW1C     Signaled System Error
   15         0b      RW1C     Detected Parity Error

1. The Interrupt Status field is a RO field that indicates that an interrupt message is pending internally to the device.

#### 9.2.2.5 Revision Register (0x8; RO)

The default revision ID of this device is 0x00 for X550 A0 and 0x01 for X550 B0. The value of the rev ID
is a logic XOR between the default value and the value in the NVM PCIe Device Revision ID
(PCI_REVID). Note that LAN 0 and LAN 1 functions have the same revision ID.

#### 9.2.2.6 Class Code Register (0x9; RO)

The class code is a read-only value that identifies the device functionality according to the value of the
Storage Class bit in the NVM PCI_CLASS NVM register.
 • Class Code = 0x020000 (Ethernet Adapter) if NVM->Storage Class = 0b
 • Class Code = 0x010000 (SCSI Storage device) if NVM->Storage Class = 1b
In the dummy function the class code equals to 0xFF0000.

#### 9.2.2.7 Cache Line Size Register (0xC; RW)

This field is implemented by PCIe devices as a read/write field for legacy compatibility purposes but has
no impact on any PCIe device functionality. The default value is zero.

802                                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.2.8 Latency Timer (0xD; RO)

Not used. Hard-wired to 0b.

#### 9.2.2.9 Header Type Register (0xE; RO)

This indicates if a device is single- or multi-function. If a single LAN function is the only active one, this
field has a value of 0x00 to indicate a single function device. If other functions are enabled, this field
has a value of 0x80 to indicate a multi-function device. Table 9-5 lists the different options to set the
header type field.

Table 9-5.      Header Type Settings
    LAN 0 Enable         LAN 1 Enable       Cross-Mode Enable               Header Type Expected Value

         0                    0                    X            N/A (no function)

         1                    0                    0            0x00

         0                    1                    0            0x80 (dummy exist)

         1                    1                    X            0x80 (dual function)

         1                    0                    1            0x80 (dummy exist)

         0                    1                    1            0x00

#### 9.2.2.10 Subsystem Vendor ID Register (0x2C; RO)

This value can be loaded automatically from the NVM at power up or reset. A value of 0x8086 is the
default for this field at power up if the NVM does not respond or is not programmed. All functions are
initialized to the same value.

#### 9.2.2.11 Subsystem ID Register (0x2E; RO)

This value can be loaded automatically from the NVM at power up with a default value of 0x0000.

             PCI Function                              Default Value                       NVM Address

              LAN Functions                               0x0000                               0x0B

#### 9.2.2.12 Cap_Ptr Register (0x34; RO)

The Capabilities Pointer field (Cap_Ptr) is an 8-bit field that provides an offset in the X550's PCI
configuration space for the location of the first item in the capabilities linked list. The X550 sets this bit
and implements a capabilities list to indicate that it supports PCI power management, MSIs, and PCIe
extended capabilities. Its value is 0x40, which is the address of the first entry: PCI power management.

#### 9.2.2.13 Interrupt Line Register (0x3C; RW)

Read/write register programmed by software to indicate which of the system interrupt request lines the
X550's interrupt pin is bound to. Refer to the PCI definition for more details. Each PCI function has its
own register.

333369-009                                                                                                 803
                                  Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                PCIe Programming Interface

#### 9.2.2.14 Interrupt Pin Register (0x3D; RO)

Read-only register. LAN 0 / LAN 1 — A value of 0x1...0x4 indicates that this function implements a
legacy interrupt on INTA#...INTD#, respectively. Loaded from the PCI_CNF NVM word per function. For
dummy function the returned value is 0x0 (Function uses no legacy interrupt Message).
Note:       If only a single device/function of the X550 component is enabled, this value is ignored and
            the Interrupt Pin field of the enabled device reports INTA# usage.

#### 9.2.2.15 Max_Lat and Min_Gnt (0x3E; RO)

Not used. Hard-wired to 0b.
For Dummy functions this register is RO - zero.

#### 9.2.2.16 Memory and IO Base Address Registers (0x10...0x27;

                         RW)
Base Address Registers (BARs) are used to map the X550 register space of the device functions. The
X550 has a memory BAR, I/O BAR and MSI-X BAR described in Table 9-6. The BARs location and sizes
are described in the Table 9-6 and Table 9-8. The fields within each BAR are then described in Table 9-
8.

Table 9-6.         X550 Base Address Registers Description — LAN 0 / LAN 1
  Mapping Windows                                                Mapping Description

Memory BAR               The internal registers memories and external Flash device are accessed as direct memory mapped offsets
                         from the BAR. Software can access a DWord or 64 bits.
                         The Flash space in this BAR is enabled by the FL_BAR_SIZE and CSRSize fields in the PCI_LBARCTRL
                         register. Address 0 in the Flash device is mapped to address 256 K in the memory BAR. When the usable
                         Flash size + CSR space are smaller than the memory BAR, accessing addresses above the top of the
                         Flash wraps back to the beginning of the Flash.

I/O BAR                  All internal registers and memories can be accessed using I/O operations. There are two 4-byte registers
                         in the I/O mapping window: Addr Reg and Data Reg accessible as DWord entities. The I/O BAR is
                         supported depending on the IO_Sup bit in the NVM at word PCIe Control 3 – Offset 0x07.

MSI-X BAR                The MSI-X vectors and Pending Bit Array (PBA) structures are accessed as direct memory mapped offsets
                         from the MSI-X BAR. Software can access DWord entities.

Table 9-7.         X550 Base Address Setting in 64-bit BARs Mode
  BAR       Addr    31                                                               5     4        3       2        1        0

      0     0x10    Memory CSR + FLASH BAR Low see Table 9-8                                       0/1      1        0       0

      1     0x14    Memory CSR + FLASH BAR High (RW)

      2     0x18    IO BAR (RW — 31:5)                                                     0        0       0        0       1

      3     0x1C    Reserved (RO — 0)

      4     0x20    MSI-X BAR Low (RW — 31:14; RO 0b — 13:4)                                       0/1      1        0       0

      5     0x24    MSI-X BAR High (RW)

804                                                                                                                   333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Table 9-8.        Base Address Registers Fields
          Field                Bit(s)     Type                                      Description

Memory and I/O Space             0         RO    Memory and I/O Space Indication
Indication                                        0b = Indicates memory space.
                                                  1b = Indicates I/O.

Memory Type                     2:1        RO    Memory Type
                                                  00b = Reserved.
                                                  10b = 64-bit BAR

Prefetch Memory                  3         RO    Prefetch Memory
                                                  0b = Non-prefetchable space.
                                                  1b = Prefetchable space.
                                                 This bit should be set only in systems that do not generate prefetchable cycles.
                                                 This bit is loaded from the PREFBAR bit in the NVM because it is required for 64-bit
                                                 memory BARs.

Address Space                  31:4        RW    Address Space
(low register for 64-bit                         The length of the RW bits and RO 0b bits depend on the mapping window size.
memory BARs)                                     Initial value of the RW fields is 0x0.
                                                 The size of the memory BAR is described in Table 9-9.

                                                 Mapping Window                                                   RO bits

                                                 Memory CSR + Flash BAR size depends on                           17:4 for 256 KB
                                                 PCI_LBARCTRL.FL_BAR_SIZE and PCI_LBARCTRL.CSRSize                18:4 for 512 KB
                                                 fields.
                                                                                                                  and so on...

                                                 MSI-X space is 16 KB.                                            13:4

                                                 I/O space size is 32 bytes.                                      4:0

Table 9-9.        Usable FLASH Size and CSR Mapping Window Size
 FL_BAR_SIZE         CSRSize          Resulted CSR + FLASH BAR Size        Installed FLASH Device          Usable FLASH Space

   000b-100b               X                     Reserved

      101b                 0                      2 MB                                2 MB                   2 MB minus 256 KB

      101b                 1                      4 MB                                2 MB                           2 MB

      110b                 0                      4 MB                                4 MB                   4 MB minus 256 KB

      110b                 1                      8 MB                                4 MB                           4 MB

      111b                 0                      8 MB                                8 MB                   8 MB minus 256 KB

      111b                 1                      16 MB                               8 MB                           8 MB

333369-009                                                                                                                          805
                                         Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

#### 9.2.2.17 Expansion ROM Base Address Register (0x30; RW)

This register is used to define the address and size information for boot-time access to the Expansion
ROM Module in the Flash memory. It is enabled by the PCI_LBARCTRL.EXROM_DIS register field. This
register returns a zero value for functions without an expansion ROM window and for dummy functions.

      Field    Bit(s)    Init.      Type                                         Description

En               0        0b        RW       Enable
                                              0b = Disables expansion ROM access.
                                              1b = Enables expansion ROM access.
Reserved        10:1      0x0        R       Reserved.
                                             Always read as 0x0. Writes are ignored.
Address         31:11     0x0       RW       Address
                                             Read-write bits are hard-wired to 0b and dependent on the memory mapping window
                                             size. The LAN Expansion ROM spaces can be either 64 KB or up to 8MBin powers of 2.
                                             Mapping window size is set by PCI_LBARCTRL.EXROM_BAR_SIZE field.

### 9.2.3 PCI Capabilities

The first entry of the PCI capabilities link list is pointed to by the Cap_Ptr register. Table 9-10 lists the
capabilities supported by the X550.

Table 9-10. PCI Capabilities List for LAN Functions
           Address                                             Item                                            Next Pointer

 0x40:4F                    PCI Power Management                                                        0x50 / 0xA01

 0x50:6F                    MSI                                                                         0x70

 0x70:8F                    MSI-X                                                                       0xA0

 0xA0:DF                    PCIe Capabilities                                                           0xE0 / 0x00

 0xE0:0xEF                  VPD Capability                                                              0x00

1. In the dummy function, the power management capability points to the PCIe capabilities.

Table 9-11. PCI Capabilities for Dummy Function
           Address                                             Item                                            Next Pointer

 0x40:47                    PCI Power Management                                                        0x50

 0xA0:DB                    PCIe Capabilities                                                           0x00

806                                                                                                                    333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.3.1 PCI Power Management Capability

All fields are reset at full power up. All fields except PME_En and PME_Status are reset after exiting
from the D3cold state. If AUX power is not supplied, the PME_En and PME_Status fields also reset after
exiting from the D3cold state. Refer to the detailed description for registers loaded from the NVM at
initialization.

Table 9-12. PCI Power Management Capability Structure
 Byte Offset            Byte 3                        Byte 2                       Byte 1                      Byte 0

                                                                             Next Pointer (0x50 /
     0x40                 Power Management Capabilities                                                  Capability ID (0x01)
                                                                                    0xA0)

     0x44                Data              Bridge Support Extensions               Power Management Control & Status

Table 9-13 summarizes sharing of the Power Management Capability registers among the different PCI
functions.

Table 9-13.      Sharing the Power Management Capability Registers
         Field               Sub-field         Shared?         Replicated?                          Comments

Capability ID                                     x

Next Pointer                                                       x

                       PME_Support                x

                       D2_Support                 x

                       D1_Support                 x
Power Management
                       AUX Current                x
Capabilities
                       DSI                        x

                       PME Clock                  x                           Hard-wired to 0b.

                       Version                    x

                       PME_Status                                  x

                       Data_Scale                 x
Power Management       Data_Select                                 x
Control / Status
                       PME_En                                      x

                       No_Soft_Reset              x

                       PowerState                                  x

Data Register                                                      x

9.2.3.1.1              Capability ID Register (0x40; RO)

This field equals 0x01 indicating the linked list item as being the PCI Power Management registers.

9.2.3.1.2              Next Pointer Register (0x41; RO)

This field provides an offset to the next capability item in the capability list. This field equals for both
LAN ports to 0x50 pointing to the MSI capability. In dummy function, it equals to 0xA0 pointing to the
PCIe Capabilities.

333369-009                                                                                                                      807
                                     Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

9.2.3.1.3                    Power Management Capabilities — PMC Register (0x42; RO)

This register describes the device functionality during the power management states as listed in the
following table. Note that each device function has its own register.

 Bit(s)    Init.     Type                                                   Description

  2:0      011b         RO     Version
                               The X550 complies with the PCI PM specification revision 1.2.
      3     0b          RO     PME_Clock
                               Disabled. Hard-wired to 0b.
      4     0b          RO     Reserved.
      5     1b          RO     DSI
                               The X550 requires its device driver to be executed following a transition to the D0 uninitialized state.
  8:6      000b         RO     AUX Current
                               Required current defined in the Data register.
      9     0b          RO     D1_Support
                               The X550 does not support the D1 state.
  10        0b          RO     D2_Support
                               The X550 does not support the D2 state.
 15:11    01001b        RO     PME_Support
                               This 5-bit field indicates the power states in which the function can assert PME#.
                               Condition Functionality Values:
                                01001b = No AUX Pwr - PME at D0 and D3hot
                                11001b = AUX Pwr - PME at D0, D3hot, and D3cold
                               Note: For dummy function, this field is RO - zero.

9.2.3.1.4                    Power Management Control/Status Register — PMCSR
                             (0x44; RW)

This register is used to control and monitor power management events in the device. Note that each
device function has its own PMCSR.

 Bit(s)      Init.           Type                                               Description

  1:0        00b             RW     PowerState
                                    This field is used to set and report the power state of a function as follows:
                                     00b = D0
                                     01b = D1 (cycle ignored if written with this value)
                                     10b = D2 (cycle ignored if written with this value)
                                     11b = D3
      2       0b             RO     Reserved for PCIe.
      3       1b             RO     No_Soft_Reset
                                    This bit is always set to 1b to indicate that the X550 does not perform an internal reset upon
                                    transition from D3hot to D0 via software control of the PowerState bits. Configuration context is
                                    kept as part of the transition from the D3hot to the D0 state, thus a full re-initialization
                                    sequence of the configuration space is not needed to return the X550 to the D0 Initialized state.
  7:4        0x0             RO     Reserved.
      8        0b            RWS    PME_En
          at power up               If power management is enabled in the NVM. Writing a 1b to this register enables Wake-up.
  12:9       0x0             RW     Data_Select
                                    This 4-bit field is used to select which data is to be reported through the Data register and
                                    Data_Scale field. These bits are writable only when power management is enabled via the NVM.

808                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

 Bit(s)        Init.      Type                                                    Description

 14:13         01b            RO      Data_Scale
                                      This field indicates the scaling factor that is used when interpreting the value of the Data
                                      register.
                                      This field equals 01b (indicating 0.1 watt/units) if the Data_Select field is set to 0, 3, 4, 7, (or 8
                                      for function 0 in multi-function device). Otherwise, it equals 00b.
   15            0b       RW1CS       PME_Status
            at power up               This bit is set to 1b when the function detects a wake-up event independent of the state of the
                                      PME_En bit. Writing a 1b clears this bit.

9.2.3.1.5                 PMCSR_BSE Bridge Support Extensions Register (0x46; RO)

This register is not implemented in the X550; values set to 0x00.

9.2.3.1.6                 Data Register (0x47; RO)

This optional register is used to report power consumption and heat dissipation. The reported register is
controlled by the Data_Select field in the PMCSR; the power scale is reported in the Data_Scale field in
the PMCSR. The data for this field is loaded from the NVM via the PCI_PWRDATA register if power
management is enabled in the NVM or with a default value of 0x00. The values for the X550’s functions
are as follows (the relevant column is selected based on the value of the Data_Select field):

   Function       D0 (Consume/ Dissipate)          D3 (Consume/ Dissipate)                       Common                      Data_Scale

 Data_Select      (0x0/0x4)                        (0x3/0x7)                        (0x8)

# 0 PCI_PWRDATA.D0_POWER             PCI_PWRDATA.D3_POWER             Function zero of a Multi-function              01b

                                                                                    device:
                                                                                     PCI_PWRDATA.COMM_POWER
                                                                                    Single-function device:
                                                                                     0x00

# 1 PCI_PWRDATA.D0_POWER             PCI_PWRDATA.D3_POWER             0x00                                           01b

Note:        For other Data_Select values the Data register output is reserved (0b).

#### 9.2.3.2 MSI Capability

Note:        This capability is not available for dummy functions.
This structure is required for PCIe devices.

Table 9-14. MSI Capability Structure
 Byte Offset               Byte 3                           Byte 2                          Byte 1                        Byte 0

     0x50                          Message Control (0x0080)                         Next Pointer (0x70)            Capability ID (0x05)

     0x54                                                             Message Address

     0x58                                                         Message Upper Address

     0x5C                                  Reserved                                                    Message Data

     0x60                                                                 Mask Bits

     0x64                                                               Pending Bits

333369-009                                                                                                                                809
                                         Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   PCIe Programming Interface

Table 9-15 summarizes configuration sharing of the MSI Capability registers among the different PCI
functions.

Table 9-15. Configuration Sharing of the MSI Capability
          Field                      Sub-field              Shared?       Replicated?                    Comments

 Capability ID                                                  x

 Next Pointer                                                                   x

                            MSI Enable                                          x

                            Multiple Messages Capable           x

 Message Control            Multiple Message Enable                             x

                            64-bit Capable                      x

                            MSI per-vector masking              x

 Message Address Low                                                            x

 Message Address High                                                           x

 Message Data                                                                   x

 Mask Bits                                                                      x

 Pending Bits                                                                   x

9.2.3.2.1                   Capability ID Register (0x50; RO)

This field equals 0x05 indicating that the linked list item as being the MSI registers.

9.2.3.2.2                   Next Pointer Register (0x51; RO)

This field provides an offset to the next capability item in the capability list. Its value of 0x70 and points
to MSI-X capability.

9.2.3.2.3                   Message Control Register (0x52; RW)

Note:        There is a dedicated register (per PCI function) to separately enable its MSI.

 Bit(s)      Init.   Type                                                  Description

      0         0b     RW      MSI Enable
                                1b = Message Signaled Interrupts — The X550 generates an MSI for interrupt assertion instead of
                                     INTx signaling.
   3:1       000b      RO      Multiple Messages Capable
                               The X550 indicates a single requested message per function.
   6:4       000b      RW      Multiple Message Enable
                               Since the X550 requests a single vector in the Multiple Message Capable field, software is expected to
                               write 000b to this field.
      7         1b     RO      64-bit Capable
                               A value of 1b indicates that the X550 is capable of generating 64-bit message addresses.
      8      1b1       RO      MSI per-vector masking
                               A value of 0b indicates that the X550 is not capable of per-vector masking. A value of 1b indicates
                               that the X550 is capable of per-vector masking.
  15:9       0x0       RO      Reserved. Reads as 0x0.

1. The value is loaded from the MSI Mask bit in the NVM.

810                                                                                                                       333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.3.2.4                 Message Address Low Register (0x54; RW)

Written by the system to indicate the lower 32 bits of the address to use for the MSI memory write
transaction. The lower two bits always return 0b regardless of the write operation.

9.2.3.2.5                 Message Address High Register (0x58; RW)

Written by the system to indicate the upper 32 bits of the address to use for the MSI memory write
transaction.

9.2.3.2.6                 Message Data Register (0x5C; RW)

Written by the system to indicate the lower 16 bits of the data written in the MSI memory write DWord
transaction. The upper 16 bits of the transaction are written as 0b.

9.2.3.2.7                 Mask Bits Register (0x60; RW)

The Mask Bits and Pending Bits registers enable software to disable or defer message sending on a per-
vector basis. As the X550 supports only one message, only bit 0 of these registers are implemented.

 Bit(s)      Init.   Type                                              Description

   0          0b     RW     MSI Vector 0 Mask
                            If set, the X550 is prohibited from sending MSI messages.
  31:1       0x0     RO     Reserved.

9.2.3.2.8                 Pending Bits Register (0x64; RW)

 Bit(s)      Init.   Type                                              Description

   0          0b     RO     MSI Message
                            If set, the X550 has a pending MSI message.
  31:1       0x0     RO     Reserved.

#### 9.2.3.3 MSI-X Capability

Note:        This capability is not available for dummy functions.
More than one MSI-X capability structure per function is prohibited while a function is permitted to have
both an MSI and an MSI-X capability structure.
In contrast to the MSI capability structure, which directly contains all of the control/status information
for the function's vectors, the MSI-X capability structure instead points to an MSI-X table structure and
an MSI-X Pending Bit Array (PBA) structure, each residing in memory space.
Each structure is mapped by a BAR belonging to the function that begins at 0x10 in the configuration
space. A BAR Indicator Register (BIR) indicates which BAR and a QWord-aligned offset indicates where
the structure begins relative to the base address associated with the BAR. The BAR is 64-bit, but must
map to the memory space. A function is permitted to map both structures with the same BAR or map
each structure with a different BAR.

333369-009                                                                                             811
                                    Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                        PCIe Programming Interface

The MSI-X table structure (Section 9.2.3.4) typically contains multiple entries, each consisting of
several fields: Message Address, Message Upper Address, Message Data, and Vector Control. Each
entry is capable of specifying a unique vector.
The PBA structure [MSI-X Table Offset Register (0x74; RW)] contains the function's pending bits, one
per table entry, organized as a packed array of bits within QWords. The last QWord is not necessarily
fully populated.
To request service using a given MSI-X table entry, a function performs a DWord memory write
transaction using:
 • The contents of the Message Data field entry for data.
 • The contents of the Message Upper Address field for the upper 32 bits of the address.
 • The contents of the Message Address field entry for the lower 32 bits of the address.
A memory read transaction from the address targeted by the MSI-X message produces undefined
results.
The MSI-X table and MSI-X PBA are permitted to co-reside within a naturally aligned 4 KB address
range, though they must not overlap with each other.
MSI-X table entries and Pending bits are each numbered 0 through N-1, where N-1 is indicated by the
Table Size field in the MSI-X Message Control register. For a given arbitrary MSI-X table entry K, its
starting address can be calculated with the formula:
Entry starting address = Table base + K*16
For the associated Pending bit K, its address for QWord access and bit number within that QWord can
be calculated with the formulas:
QWord address = PBA base + (K div 64)*8
QWord bit# = K mod 64
Software that chooses to read Pending bit K with DWord accesses can use these formulas:
DWord address = PBA base + (K div 32)*4
DWord bit# = K mod 32

Table 9-16. MSI-X Capability Structure
 Byte Offset         Byte 3                    Byte 2                       Byte 1                  Byte 0

      0x70               Message Control (0x00090)                    Next Pointer (0xA0)     Capability ID (0x11)

      0x74                                                Table Offset

      0x78                                                   PBA Offset

Table 9-17 summarizes configuration sharing of the MSI-X Capability registers among the different PCI
functions.

Table 9-17. Configuration Sharing of the MSI-X Capability
             Field       Sub-field     Shared?       Replicated?                        Comments

Capability ID                              x

Next Pointer                                             x

Message Control        Table Size          x

Function Mask                                            x

812                                                                                                       333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Table 9-17. Configuration Sharing of the MSI-X Capability [continued]
          Field                Sub-field        Shared?       Replicated?                          Comments

MSI-X Enable                                                        x

                             Table BIR                              x
MSI-X Table Offset
                             Table Offset                           x

                             PBA BIR                                x
MSI-X Pending Bit Array
                             PBA Offset                             x

MSI-X Table                                                         x

MSI-X PBA Structure                                                 x

9.2.3.3.1                  Capability ID Register (0x70; RO)

This field equals 0x11 indicating that the linked list item as being the MSI-X registers.

9.2.3.3.2                  Next Pointer Register (0x71; RO)

This field provides an offset to the next capability item in the capability list. Its value of 0xA0 points to
PCIe capability.

9.2.3.3.3                  Message Control Register (0x72; RW)

Note:        There is a dedicated register (per PCI function).

 Bit(s)      Init.    Type                                                 Description

  10:0       0x3F     RO      Table Size
                              System software reads this field to determine the MSI-X Table Size N, which is encoded as N-1. The
                              X550 supports up to 64 different interrupt vectors per function.
                              This field is loaded from the PCI_CNF2.MSI_X_PF_N register field.
 13:11       000b     RO      Reserved. Always returns 000b on a read. A write operation has no effect.
   14         0b      RW      Function Mask
                               0b = Each vector’s Mask bit determines whether the vector is masked or not.
                               1b = All of the vectors associated with the function are masked, regardless of their per-vector Mask
                                     bit states.
                              Setting or clearing the MSI-X Function Mask bit has no effect on the state of the per-vector Mask bits.
   15         0b      RW      MSI-X Enable
                                0b = The function is prohibited from using MSI-X to request service.
                                1b = If 1b and the MSI Enable bit in the MSI Message Control register is 0b, the function is
                                      permitted to use MSI-X to request service and is prohibited from using its INTx# pin.
                              System configuration software sets this bit to enable MSI-X. A device driver is prohibited from writing
                              this bit to mask a function’s service request.

333369-009                                                                                                                        813
                                         Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

9.2.3.3.4                    MSI-X Table Offset Register (0x74; RW)

 Bit(s)        Init.     Type                                                Description

  2:0         0x3/0x4    RO      Table BIR
                                 Indicates which one of a function’s BARs, beginning at 0x10 in the configuration space, is used to
                                 map the function’s MSI-X table into the memory space. while BIR values: 0...5 correspond to BARs
                                 0x10…0x 24, respectively.
  31:3         0x0       RO      Table Offset
                                 Used as an offset from the address contained in one of the function’s BARs to point to the base of
                                 the MSI-X table. The lower three Table BIR bits are masked off (set to 0b) by software to form a
                                 32-bit QWord-aligned offset.
                                 This field is read only.

9.2.3.3.5                    MSI-X Pending Bit Array — PBA Offset (0x78; RW)

 Bit(s)       Init.     Type                                                Description

  2:0          0x4      RO      PBA BIR
                                Indicates which one of a function’s BARs, beginning at 0x10 in the configuration space, is used to map
                                the function’s MSI-X PBA into the memory space. while BIR values: 0...5 correspond to BARs
                                0x10…0x 24, respectively.
  31:3    0x0400        RO      PBA Offset
                                Used as an offset from the address contained in one of the functions BARs to point to the base of the
                                MSI-X PBA. The lower three PBA BIR bits are masked off (set to 0b) by software to form a 32-bit
                                QWord-aligned offset.
                                This field is read only.

#### 9.2.3.4 MSI-X Table Structure

   DWord3 —               DWord2 —                 DWord1 —                   DWord0 —               Entry
                                                                                                                   BAR 3 — Offset
  MSIXTVCTRL              MSIXTMSG                MSIXTUADD                   MSIXTADD              Number

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address             0           Base (0x0000)

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address             1            Base + 1*16

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address             2            Base + 2*16

          …                     …                       …                          …                    …

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address            63           Base + 63*16

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address            64           Base + 64*16

          …                     …                       …                          …                    …

  Vector Control             Msg Data          Msg Upper Address          Msg Lower Address            255          Base + 255*16

Note:          All MSI-X vectors > MSI-X 63, are usable only by the Virtual Functions (VFs) in IOV mode.
               These vectors are not exposed to the operating system by the Table Size field in the MSI-X
               Message Control word.
See Section 8.2.2.7 for details of the MSI-X registers in BAR 3 of the PF.

814                                                                                                                        333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.3.5 VPD Registers

Note:        This capability is not available for dummy functions.
The X550 supports access to a VPD structure stored in the NVM using the following set of registers.
Initial values of the configuration registers are marked in parenthesis.
Note:        The VPD structure is available through both ports functions. As the interface is common to the
             two functions, accessing the VPD structure of one function while an access to the NVM is in
             process on the other function can yield to unexpected results.

Table 9-18. VPD Capability Structure
 Byte Offset                Byte 3                     Byte 2                       Byte 1                      Byte 0

     0xE0                             VPD Address                             Next Pointer (0x00)         Capability ID (0x03)

     0xE4                                                           VPD Data

Table 9-19 summarizes configuration sharing of the VPD Capability registers among the different PCI
functions.

Table 9-19. Configuration Sharing of the VPD Capability
          Field             Shared?      Replicated?                                   Comments

Capability ID                  X

Next Pointer                   X

VPD Address/F                  X

VPD Data                       X

9.2.3.5.1                 Capability ID Register (0xE0; RO)

This field equals 0x3 indicating the linked list item as being the VPD registers.

9.2.3.5.2                 Next Pointer Register (0xE1; RO)

Offset to the next capability item in the capability list. A 0x00 value indicates that it is the last item in
the capability-linked list.

9.2.3.5.3                 VPD Address Register (0xE2; RW)

Word-aligned byte address of the VPD area in the NVM to be accessed. The register is read/write, and
the initial value at power-up is indeterminate.

 Bit(s)      Init.   Type                                                Description

  14:0          X    RW       Address
                              DWord-aligned byte address of the VPD area in the NVM to be accessed. The register is read/write,
                              and the initial value at power-up is indeterminate. The two LSBs are RO as zero.
   15          0b    RW       F
                              A flag used to indicate when the transfer of data between the VPD Data register and the storage
                              component completes. The Flag register is written when the VPD Address register is written.
                                0b = Read — Set by hardware when data is valid.
                                1b = Write — Cleared by hardware when data is written to the NVM.
                              The VPD address and data should not be modified before the action is done.

333369-009                                                                                                                       815
                                      Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                     PCIe Programming Interface

9.2.3.5.4                 VPD Data Register (0xE4; RW)

VPD read/write data.

 Bit(s)      Init.   Type                                                  Description

  31:0        X      RW       VPD Data
                              VPD data can be read or written through this register. The LS byte of this register (at offset 4 in this
                              capability structure) corresponds to the byte of VPD at the address specified by the VPD Address
                              register. The data read from or written to this register uses the normal PCI byte transfer capabilities.
                              Four bytes are always transferred between this register and the VPD storage component. Reading or
                              writing data outside of the VPD space in the storage component is not allowed.
                              In a write access, the data should be set before the address and the flag is set.

#### 9.2.3.6 PCIe Capability

The X550 implements the PCIe capability structure linked to the legacy PCI capability list for endpoint
devices as follows:

Table 9-20. PCIe Capability Structure
 Byte Offset                Byte 3                       Byte 2                         Byte 1                      Byte 0

      0xA0             PCI Express Capability Register (0x0002)              Next Pointer (0xE0/0x00)         Capability ID (0x10)

      0xA4                                                        Device Capability

      0xA8                            Device Status                                               Device Control

      0xAC                                                          Link Capability

      0xB0                              Link Status                                                Link Control

      0xB4                                                             Reserved

      0xB8                               Reserved                                                   Reserved

      0xBC                                                             Reserved

      0xC0                               Reserved                                                   Reserved

      0xC4                                                        Device Capability 2

      0xC8                               Reserved                                                Device Control 2

      0xCC                                                             Reserved

      0xD0                             Link Status 2                                              Link Control 2

      0xD4                                                             Reserved

      0xD8                               Reserved                                                   Reserved

Table 9-21 summarizes configuration sharing of the PCIe Capability registers among the different PCI
functions.

816                                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Table 9-21. Configuration Sharing of the PCIe Capability
        Field                        Sub-field               Shared?    Replicated?             Comments

Capability ID                                                   x

Next Pointer                                                                 x

PCIe Capabilities                                               x

                      Max Payload Size Supported                x

                      Phantom Functions Supported               x                     Not supported.

                      Extended Tag Field Supported              x
Device Capabilities
                      Endpoint L0s Acceptable Latency           x

                      Endpoint L1 Acceptable Latency            x

                      Function Level Reset Capability           x

                      Correctable Error Reporting Enable                     x

                      Non-Fatal Error Reporting Enable                       x

                      Fatal Error Reporting Enable                           x

                      Unsupported Request Reporting Enable                   x

                      Enable Relaxed Ordering                                x

                                                                                      Use minimum of all configured
                      Max Payload Size                                       x        values. In ARI mode, use value
                                                                                      in Function 0.
Device Control
                      Extended Tag field Enable                              x

                                                                                      Same policy for all PFs (Logical
                      Auxiliary Power PM Enable                              x
                                                                                      OR of the PF’s bits)

                      Enable No Snoop                                        x

                                                                                      Use minimum of all configured
                      Max Read Request Size                                  x
                                                                                      values.

                      Initiate Function Level Reset                          x

                      Correctable Detected                                   x

                      Non-Fatal Error Detected                               x

                      Fatal Error Detected                                   x
Device Status
                      Unsupported Request Detected              x

                      Aux Power Detected                        x

                      Transactions Pending                                   x

                      Supported Link Speeds                     x

                      Max Link Width                            x

                      Active State Link PM Support              x

Link Capabilities     L0s Exit Latency                          x

                      L1 Exit Latency                           x

                      Clock Power Management                    x

                      Port Number                               x

333369-009                                                                                                          817
                                    Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                         PCIe Programming Interface

Table 9-21. Configuration Sharing of the PCIe Capability [continued]
        Field                           Sub-field              Shared?    Replicated?             Comments

                                                                                        Same policy for all PFs (Logical
                        Active State Link PM Control                           x        AND of the PF’s bits). In ARI
                                                                                        mode, use value in Function 0.

                        Read Completion Boundary (RCB)                         x
Link Control                                                                            Same policy for all PFs (Logical
                        Common Clock Configuration                             x        AND of the PF’s bits) In ARI
                                                                                        mode, use value in Function 0.

                                                                                        Same policy for all PFs (Logical
                        Extended Sync                                          x
                                                                                        OR of the PF’s bits).

                        Current Link Speed                        x

Link Status             Negotiated Link Width                     x

                        Slot Clock Configuration                  x

                        Completion Timeout Ranges Supported       x

                        Completion Timeout Disable Supported      x

                        LTR Mechanism Supported                   x
Device Capabilities 2
                        TPH Completer Supported                   x

                        Extended Fmt Field Supported              x

                        OBFF Supported                            x

                                                                                        Completion timeout decision per
                        Completion Timeout Value                               x        PF or use the largest configured
                                                                                        value among PFs.

                                                                                        Completion timeout mechanism
                        Completion Timeout Disable                             x
                                                                                        enabled per PF.

Device Control 2        IDO Request Enable                                     x

                        IDO Completion Enable                                  x

                                                                                        PF0 only. RsvdP on other
                        LTR Mechanism Enable                                   x
                                                                                        functions.

                                                                                        PF0 only. RsvdP on other
                        OBFF Enable                                            x
                                                                                        functions.

Link Capabilities 2                                               x

                                                                                        PF0 only. RsvdP on other
Link Control 2                                                    x
                                                                                        functions.

Link Status 2                                                     x

9.2.3.6.1                Capability ID Register (0xA0; RO)

This field equals 0x10 indicating that the linked list item as being the PCIe Capabilities registers.

9.2.3.6.2                Next Pointer Register (0xA1; RO)

Offset to the next capability item in the capability list. Its value of 0xE0 points to the VPD structure. If
VPD is disabled or for a dummy function, a value of 0x00 value indicates that it is the last item in the
capability-linked list.

818                                                                                                           333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.3.6.3                 PCIe Capabilities Register (0xA2; RO)

The PCIe Capabilities register identifies PCIe device type and associated capabilities. This is a read-only
register identical to all functions.

 Bit(s)      Init.   Type                                                Description

  3:0        0x2     RO     Capability Version
                            Indicates the PCIe capability structure version. The X550 supports PCIe version 2 (also loaded from
                            the PCI_CAPSUP.PCIE_VER bit in the NVM).
  7:4        0x0     RO     Device/Port Type
                            Indicates the type of PCIe functions. All functions are native PCI functions with a value of 0x0.
   8          0b     RO     Slot Implemented
                            The X550 does not implement slot options. Therefore, this field is hard-wired to 0b.
  13:9       0x0     RO     Interrupt Message Number
                            The X550 does not implement multiple MSI per function. As a result, this field is hard-wired to 0x0.
 15:14       00b     RO     Reserved.

9.2.3.6.4                 Device Capabilities Register (0xA4; RO)

This register identifies the PCIe device specific capabilities. It is a read-only register with the same
value for the two LAN functions and for all other functions.

 Bit(s)      Init.   Type                                                Description

  2:0        010b    RO     Max Payload Size Supported
                            This field indicates the maximum payload that The X550 can support for TLPs. It is loaded from the
                            NVM with a default value of 512 bytes.
  4:3        00b     RO     Phantom Function Supported
                            Not supported by the X550.
   5          0b     RO     Extended Tag Field Supported
                            Maximum supported size of the Tag field. The X550 supports a 5-bit Tag field for all functions.
  8:6        011b    RO     Endpoint L0s Acceptable Latency
                            This field indicates the acceptable latency that the X550 can withstand due to the transition from L0s
                            state to the L0 state. All functions share the same value loaded from the NVM PCIe Init Configuration
                            1 bits [8:6].
                            A value of 011b equals 512 ns.
  11:9       110b    RO     Endpoint L1 Acceptable Latency
                            This field indicates the acceptable latency that the X550 can withstand due to the transition from L1
                            state to the L0 state.
                            A value of 110b equals 32 s to 64 s.
                            All functions share the same value loaded from the NVM.
   12         0b     RO     Attention Button Present
                            Hard-wired in the X550 to 0b for all functions.
   13         0b     RO     Attention Indicator Present
                            Hard-wired in the X550 to 0b for all functions.
   14         0b     RO     Power Indicator Present
                            Hard-wired in the X550 to 0b for all functions.
   15         1b     RO     Role Based Error Reporting
                            Hard-wired in the X550 to 1b for all functions.
 17:16       000b    RO     Reserved.
 25:18       0x0     RO     Slot Power Limit Value
                            Used in upstream ports only. Hard-wired in the X550 to 0x0 for all functions.
 27:26       00b     RO     Slot Power Limit Scale
                            Used in upstream ports only. Hard-wired in the X550 to 0b for all functions.

333369-009                                                                                                                      819
                                    Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                     PCIe Programming Interface

 Bit(s)    Init.     Type                                                    Description

  28        1b          RO      Function Level Reset Capability
                                A value of 1b indicates the Function supports the optional Function Level Reset (FLR) mechanism.
 31:29     000b         RO      Reserved.

9.2.3.6.5                    Device Control Register (0xA8; RW)

This register controls the PCIe specific parameters. Note that there is a dedicated register per each
function.

 Bit(s)      Init.           Type                                              Description

      0       0b             RW     Correctable Error Reporting Enable
                                    Enable error report.
      1       0b             RW     Non-Fatal Error Reporting Enable
                                    Enable error report.
      2       0b             RW     Fatal Error Reporting Enable
                                    Enable error report.
      3       0b             RW     Unsupported Request Reporting Enable
                                    Enable error report.
      4       1b             RW     Enable Relaxed Ordering
                                    If this bit is set, the X550 is permitted to set the Relaxed Ordering bit in the Attribute field of
                                    write transactions that do not need strong ordering. Refer to the CTRL_EXT register bit RO_DIS
                                    for more details.
  7:5        000b            RW     Max Payload Size
          (128 bytes)               This field sets the maximum TLP payload size for the X550 functions. As a receiver, the X550
                                    must handle TLPs as large as the set value. As a transmitter, the X550 must not generate TLPs
                                    exceeding the set value.
                                    The Max Payload Size field supported in the Device Capabilities register indicates permissible
                                    values that can be programmed.
                                    In ARI mode, Max Payload Size is determined solely by the field in function 0(even when it is a
                                    dummy function) while it is meaningless in the other function(s).
      8       0b             RW     Extended Tag field Enable
                                    Not implemented in the X550.
      9       0b             RW     Phantom Functions Enable
                                    Not implemented in the X550.
  10          0b             RWS    Auxiliary Power PM Enable
                                    When set, enables the X550 to draw AUX power independent of PME AUX power. The X550 is a
                                    multi-function device, therefore allowed to draw AUX power if at least one of the functions has
                                    this bit set.
  11          0b             RW     Enable No Snoop
                                    No-snoop is not used by the X550.
 14:12       010b            RW     Max Read Request Size
                                    This field sets maximum read request size for the X550 as a requester.
                                     000b = 128 bytes
                                     001b = 256 bytes
                                     010b = 512 bytes
                                     011b = 1024 bytes
                                     100b = 2048 bytes
                                     101b = 4096 bytes (Not supported by the X550)
                                     110b = Reserved
                                     111b = Reserved
  15          0b             RW     Initiate FLR
                                    A write of 1b initiates FLR to the function. The value read by software from this bit is always 0b.

820                                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.3.6.6                         Device Status Register (0xAA; RW1C)

This register provides information about PCIe device specific parameters. Note that there is a dedicated
register per each function.

 Bit(s)      Init.         Type                                                    Description

   0          0b           RW1C     Correctable Detected
                                    Indicates status of correctable error detection.
   1          0b           RW1C     Non-Fatal Error Detected
                                    Indicates status of non-fatal error detection.
   2          0b           RW1C     Fatal Error Detected
                                    Indicates status of fatal error detection.
   3          0b           RW1C     Unsupported Request Detected
                                    Indicates that the X550 received an unsupported request. This field is identical in all functions. The
                                    X550 cannot distinguish which function causes the error.
   4          0b             RO     Aux Power Detected
                                    If Aux Power is detected, this field is set to 1b. It is a strapping signal from the periphery and is
                                    identical for all functions. Resets on LAN Power Good and PE_RST_N only.
   5          0b             RO     Transaction Pending
                                    Indicates whether the X550 has ANY transactions pending. (transactions include completions for any
                                    outstanding non-posted request for all used traffic classes).
  15:6       0x0             RO     Reserved.

9.2.3.6.7                         Link Capabilities Register (0xAC; RO)

This register identifies PCIe link-specific capabilities. This is a read-only register identical to all
functions.

 Bit(s)              Init.           Type                                               Description

  3:0                0x1              RO        Supported Max Link Speed
                                                This field indicates the supported Link speed(s) of the associated link port.
                                                Defined encodings are:
                                                 0001b = 2.5 GT/s link speed supported.
                                                 0010b = 5 GT/s and 2.5 GT/s link speeds supported.
                                                 0011b = 8 GT/s and 5 GT/s and 2.5 GT/s link speeds supported
  9:4     0x04 - X550-AT2             RO        Max Link Width
          0x08 - X550-BT2                       Indicates the maximum link width. The X550 supports a x1, x4 and x8-link width. This field
                                                is loaded from the PCIe Analog Configuration NVM module by interpreting the masked
                                                lanes, with a default value of eight lanes for the X550-BT2 and four for the X550-AT2.
                                                Defined encoding:
                                                  000000b = Reserved
                                                  000001b = x1
                                                  000010b = Reserved
                                                  000100b = x4
                                                  001000b = x8
 11:10               10b              RO        Active State Link PM Support
                                                Indicates the level of the active state of power management supported in the X550. Defined
                                                encodings are:
                                                 00b = No ASPM support.
                                                 01b = L0s Entry supported.
                                                 10b = L1 supported.
                                                 11b = L0s and L1 supported.
                                                All functions share the same value loaded from the NVM.

333369-009                                                                                                                                  821
                                             Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                PCIe Programming Interface

 Bit(s)       Init.        Type                                              Description

 14:12        101b          RO       L0s Exit Latency
          (1 s – 2 s)              Indicates the exit latency from L0s to L0 state.
                                      000b = Less than 64 ns.
                                      001b = 64 ns – 128 ns
                                      010b = 128ns – 256 ns
                                      011b = 256 ns – 512 ns
                                      100b = 512 ns — 1 s
                                      101b = 1 s – 2 s
                                      110b = 2 s – 4 s
                                      111b = Reserved.
                                     All functions share the same value loaded from the NVM.
 17:15         100b         RO       L1 Exit Latency
          (8 s — 16 s)             Indicates the exit latency from L1 to L0 state.
                                      000b = Less than 1 s
                                      001b = 1 s — 2 s
                                      010b = 2 s — 4 s
                                      011b = 4 s — 8 s
                                      100b = 8 s — 16 s
                                      101b = 16 s — 32 s
                                      110b = 32 s — 64 s
                                      111b = L1 transition not supported.
                                     All functions share the same value loaded from the NVM.
  18            0           RO       Clock Power Management
  19            0           RO       Surprise Down Error Reporting Capable
                                     Hard-wired to 0b.
  20            0           RO       Data Link Layer Link Active Reporting Capable
  21            0           RO       Link Bandwidth Notification Capability
                                     Hard-wired to 0b.
  22           1b           RO       ASPM Optional Compliance
                                     This bit must be set to 1b. Components that were implemented according to an earlier PCIe
                                     specification version has this bit set to 0b.
                                     Software is permitted to use the value of this bit to help determine whether to enable ASPM
                                     or run ASPM compliance tests.
  23           0b           RO       Reserved.
 31:24         0x0         HwInit    Port Number
                                     The PCIe port number for the given PCIe link. This field is set in the link training phase.

822                                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.3.6.8                 Link Control Register (0xB0; RO)

This register controls PCIe link specific parameters. There is a dedicated register per each function.

 Bit(s)      Init.   Type                                                 Description

  1:0        00b     RW     Active State Link PM Control
                            This field controls the active state PM supported on the link. Link PM functionality is determined by
                            the lowest common denominator of all functions. For non-ARI mode, only capabilities enabled in all
                            functions are enabled for the component as a whole.
                            When ARI support is exposed, ASPM control is determined solely by the setting in Function 0 (even
                            when it is a dummy function), regardless of Function 0’s D-state. The settings in the other functions
                            always return whatever value software programmed for each, but otherwise are ignored by the X550.
                            Defined encodings are:
                              00b = PM Disabled.
                              01b = L0s Entry Supported.
                              10b = L1 Entry Enabled.
                              11b = L0s and L1 Supported.
                            In ARI mode, the ASPM is determined solely by the field in function 0 while it is meaningless in the
                            other function(s).
   2          0b     RO     Reserved.
   3          0b     RO     Read Completion Boundary
   4          0b     RO     Link Disable
                            Reserved for endpoint devices. Hard-wired to 0b.
   5          0b     RO     Retrain Clock
                            Not applicable for endpoint devices. Hard-wired to 0b.
   6          0b     RW     Common Clock Configuration
                            When set, indicates that the X550 and the component at the other end of the link are operating with
                            a common reference clock. A value of 0b indicates that they are operating with an asynchronous
                            clock.
                            In ARI mode, the common clock configuration is determined solely by the field in function 0 (even
                            when it is a dummy function) while it is meaningless in the other function(s).
   7          0b     RW     Extended Sync
                            When set, this bit forces an extended Tx of the FTS ordered set in FTS and an extra TS1 at the exit
                            from L0s prior to entering L0.
   8          0b     RO     Enable Clock Power Management
                            Not supported in the X550. Hard-wired to 0.
   9          0b     RW     Reserved.
                            Returns the value that was written.
   10         0b     RO     Link Bandwidth Management Interrupt Enable
                            Not supported in the X550. Hard-wired to 0.
   11         0b     RO     Link Autonomous Bandwidth Interrupt Enable
                            Not supported in the X550. Hard-wired to 0.
 15:12       0x0     RO     Reserved.

333369-009                                                                                                                    823
                                    Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

9.2.3.6.9               Link Status Register (0xB2; RO)

This register provides information about PCIe Link specific parameters. This is a read only register
identical to all functions.

 Bit(s)   Init.   Type                                                   Description

  3:0      X       RO      Current Link Speed
                           This field indicates the negotiated link speed of the given PCIe link.
                           Defined encodings are:
                            0001b = 2.5 GT/s PCIe link.
                            0010b = 5 GT/s PCIe link.
                            0011b = 8 GT/s PCIe link.
                            All other encodings are reserved.
                           The value in this field is undefined when the Link is not up.
  9:4      X       RO      Negotiated Link Width
                           Indicates the negotiated width of the link.
                           Relevant encodings for the X550 are:
                            000001b = x1
                            000010b = Reserved
                            000100b = x4
                            001000b = x8
                           The value in this field is undefined when the Link is not up.
  10       0b      RO      Undefined.
  11       0b      RO      Link Training
                           Indicates that link training is in progress.
                           This field is not applicable and is reserved for endpoint devices, and is hard-wired to 0b.
  12       1b     HwInit   Slot Clock Configuration
                           When set, indicates that the X550 uses the physical reference clock that the platform provides at the
                           connector. This bit must be cleared if the X550 uses an independent clock. The Slot Clock
                           Configuration bit is loaded from the Slot_Clock_Cfg NVM bit.
  13       0b      RO      Data Link Layer Link Active
                           Not supported in the X550. Hard-wired to 0b.
  14       0b      RO      Link Bandwidth Management Status
                           Not supported in the X550. Hard-wire to 0b.
  15       0b      RO      Link Autonomous Bandwidth Status
                           This bit is not applicable and is reserved for endpoints.

The following registers are supported only if the capability version is two and above.

824                                                                                                                      333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.3.6.10                Device Capability 2 Register (0xC4; RO)

This register identifies the PCIe device-specific capabilities. It is a read-only register with the same
value for both LAN functions.

 Bit(s)      Init.   Type                                               Description

  3:0        0xF     RO     Completion Timeout Ranges Supported
                            This field indicates the X550’s support for the optional completion timeout programmability
                            mechanism.
                            Four time value ranges are defined:
                             • Range A: 50 s to 10 ms
                             • Range B: 10 ms to 250 ms
                             • Range C: 250 ms to 4 s
                             • Range D: 4 s to 64 s
                            Bits are set according to the following values to show the timeout value ranges that the X550
                            supports.
                             0000b = Completion timeout programming not supported. The X550 must implement a timeout
                                         value in the range of 50 s to 50 ms.
                             0001b = Range A.
                             0010b = Range B.
                             0011b = Ranges A and B.
                             0110b = Ranges B and C.
                             0111b = Ranges A, B and C.
                             1110b = Ranges B, C and D.
                             1111b = Ranges A, B, C and D.
                             All other values are reserved.
   4          1b     RO     Completion Timeout Disable Supported
                            A value of 1b indicates support for the completion timeout disable mechanism.
                            Note: For dummy functionality, a completion timeout is not relevant as a dummy function because
                                    it never sends non-posted requests.
   5          0b     RO     ARI Forwarding Supported
                            Applicable only to Switch Downstream. Ports and Root Ports; must be 0b for other function types.
  10:6       0x0     RO     Not supported
                            Hard-wired to 0x0.
   11         1b     RO     LTR Mechanism Supported
                            A value of 1b indicates support for the optional Latency Tolerance Reporting (LTR) mechanism.
                            For a multi-Function device associated with an Upstream Port, each Function must report the same
                            value for this bit.
                            Note: Value loaded from LTR_EN bit in the NVM
 13:12       00b     RO     TPH Completer Supported
                            Value indicates Completer support for TPH or Extended TPH.
                            This capability is not supported.
 17:14       0x0     RO     Reserved.
 19:18       00b     RO     OBFF Supported
                             00b = OBFF not supported.
                             01b = OBFF supported using Message signaling only..
                             10b = OBFF supported using WAKE# signaling only
                             11b = OBFF supported using WAKE# and Message signaling.
   20         0b     RO     Extended Fmt Field Supported
                             0b = The Function supports a 2-bit definition of the Fmt field.
                             1b = The Function supports the 3-bit definition of the Fmt field.
                            Not supported by this device
   21         0b     RO     End-End TLP Prefix Supported
                            Indicates whether End-End TLP Prefix support is offered by a Function.
                            Not supported by this device.

333369-009                                                                                                                     825
                                    Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                               PCIe Programming Interface

 Bit(s)   Init.   Type                                                  Description

 23:22    00b     RsvdP   Max End-End TLP Prefixes
                          Indicates the maximum number of End-End TLP Prefixes supported by this Function.
                          Reserved for this device.
 31:24    0x0      RO     Reserved.

9.2.3.6.11              Device Control 2 Register (0xC8; RW)

This register controls the PCIe specific parameters. Note that there is a dedicated register per each
function.

 Bit(s)   Init.   Type                                                  Description

  3:0     0x0      RW     Completion Timeout Value
                          For devices that support completion timeout programmability, this field enables system software to
                          modify the completion timeout value.
                          Defined encodings:
                            0000b = Default range: 16 ms to 32 ms.
                          Note: It is strongly recommended that the completion timeout mechanism not expire in less than
                                   10 ms.
                          Values available if Range A (50 s to 10 ms) programmability range is supported:
                            0001b = 50 s to 100 s.
                            0010b = 1 ms to 2 ms.
                          Values available if Range B (10 ms to 250 ms) programmability range is supported:
                            0101b = 16 ms to 32 ms.
                            0110b = 65 ms to 130 ms.
                          Values available if Range C (250 ms to 4 s) programmability range is supported:
                            1001b = 260 ms to 520 ms.
                            1010b = 1 s to 2 s.
                          Values available if the Range D (4 s to 64 s) programmability range is supported:
                            1101b = 4 s to 8 s.
                            1110b = 17 s to 34 s.
                          Values not defined are reserved.
                          Software is permitted to change the value of this field at any time. For requests already pending when
                          the completion timeout value is changed, hardware is permitted to use either the new or the old value
                          for the outstanding requests and is permitted to base the start time for each request either on when
                          this value was changed or on when each request was issued.
                          Note: For dummy function, this field is RO - zero.
      4    0b      RW     Completion Timeout Disable
                          When set to 1b, this bit disables the completion timeout mechanism.
                          Software is permitted to set or clear this bit at any time. When set, the completion timeout detection
                          mechanism is disabled. If there are outstanding requests when the bit is cleared, it is permitted but
                          not required for hardware to apply the completion timeout mechanism to the outstanding requests. If
                          this is done, it is permitted to base the start time for each request on either the time this bit was
                          cleared or the time each request was issued.
                          Note: For dummy function, this field is RO - zero.
      5    0b      RO     ARI Forwarding Enable
                          Applicable only to switch devices.
  7:6     00b      RO     Not supported. Hard-wired to 00b.
      8    0b      RW     IDO Request Enable
                          If this bit is Set, the Function is permitted to set the ID-Based Ordering (IDO) bit (Attribute[2]) of
                          Requests it initiates.
                          Default value of this bit is 0b.
      9    0b      RW     IDO Completion Enable
                          If this bit is Set, the Function is permitted to set the ID-Based Ordering (IDO) bit (Attribute[2]) of
                          Completions it returns
                          Default value of this bit is 0b.

826                                                                                                                    333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

 Bit(s)      Init.     Type                                                  Description

   10         0b       RW /     LTR Mechanism Enable
                       RsvdP    When Set to 1b, this bit enables Upstream Ports to send LTR messages.
                                For a multi-function device, the bit in Function 0 is RW, and only Function 0 controls the component’s
                                Link behavior. In all other Functions of that device, this bit is RsvdP.
                                If the LTR_EN bit in the NVM is 0b, this bit is RO with a value of 0b.
                                Default value of this bit is 0b.
 12:11       00b        RO      Reserved
 14:13       00b       RsvdP    OBFF Enable
                                 00b = Disabled
                                 01b = Enabled using Message signaling [Variation A]
                                 10b = Enabled using Message signaling [Variation B]
                                 11b = Enabled using WAKE# signaling
   15         0b       RsvdP    End-End TLP Prefix Blocking
                                Not applicable to endpoints.

9.2.3.6.12                   Link Capabilities 2 Register (0xCC)

 Bit(s)      Init.     Type                                                  Description

   0          0b        RO      Reserved.
  7:1        0x01       RO      Supported Link Speeds Vector
                                This field indicates the supported Link speed(s) of the associated Port. For each bit, a value of 1b
                                indicates that the corresponding Link speed is supported; otherwise, the Link speed is not supported.
                                Bit definitions are:
                                  Bit 1 =      2.5 GT/s
                                  Bit 2 =      5.0 GT/s
                                  Bit 3 =      8.0 GT/s
                                  Bits 7:4 = RsvdP
                                Multi-Function devices associated with the same Upstream Port must report the same value in this
                                field for all Functions. This field is loaded from NVM and is reflected in the PCI_LINKCAP register.
   8          0b        RO      Crosslink Supported
                                When set to 1b, this bit indicates that the associated Port supports cross links.
                                It is recommended that this bit be Set in any Port that supports cross-links even though doing so is
                                only required for Ports that also support operating at 8.0 GT/s or higher Link speeds.
  31:9       0x0        RO      Reserved.

9.2.3.6.13                   Link Control 2 Register (0xD0; RWS)

All RW fields in this register affect the device behavior only through function 0. In function 1, these
fields are reserved read as zeros.

 Bit(s)        Init.            Type                                               Description

  3:0     0x1 (func 0)       RWS (func 0)   Target Link Speed
           0x0 (else)        RsvdP (else)   This field is used to set the target compliance mode speed when software is using the
                                            Enter Compliance bit to force a link into compliance mode.
                                            The encoding is the binary value of the bit in the Supported Link Speeds Vector (in the
                                            Link Capabilities 2 register) that corresponds to the desired target Link speed. All other
                                            encodings are Reserved.
                                            For example, 5.0 GT/s corresponds to bit 2 in the Supported Link Speeds Vector, so the
                                            encoding for a 5.0 GT/s target Link speed in this field is 0010b
                                            If a value is written to this field that does not correspond to a speed included in the
                                            Supported Link Speeds field, the result is undefined.
                                            The default value of this field is the highest link speed supported by the X550 (as reported
                                            in the Supported Link Speeds field of the Link Capabilities register).

333369-009                                                                                                                           827
                                        Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                          PCIe Programming Interface

 Bit(s)   Init.      Type                                               Description

      4    0b     RWS (func 0)   Enter Compliance
                  RsvdP (else)   Software is permitted to force a link to enter compliance mode at the speed indicated in
                                 the Target Link Speed field by setting this bit to 1b in both components on a link and then
                                 initiating a hot reset on the link.
                                 The default value of this field following a fundamental reset is 0b.
      5    0b     RWS (func 0)   Hardware Autonomous Speed Disable
                  RsvdP (else)   When set to 1b, this bit disables hardware from changing the link speed for reasons other
                                 than attempting to correct unreliable link operation by reducing link speed.
      6    0b         RO         Selectable De-Emphasis
                                 This bit is not applicable and reserved for endpoints.
  9:7     000b    RWS (func 0)   Transmit Margin
                  RsvdP (else)   This field controls the value of the non de emphasized voltage level at the Transmitter
                                 pins.
                                 Encodings:
                                  000b = Normal operating range.
                                  001b = 800-1200 mV for full swing and 400-700 mV for half-swing.
                                  010b = (n-1) — Values must be monotonic with a non-zero slope. The value of n must be
                                            greater than 3 and less than 7. At least two of these must be below the normal
                                            operating range of n: 200-400 mV for full-swing and 100-200 mV for half-swing.
                                  111b = (n) Reserved.
  10       0b     RWS (func 0)   Enter Modified Compliance
                  RsvdP (else)   When this bit is set to 1b, the device transmits modified compliance pattern if the LTSSM
                                 enters Polling.Compliance state.
                                 The default value of this bit is 0b.
  11       0b     RWS (func 0)   Compliance SOS
                  RsvdP (else)   When set to 1b, the LTSSM is required to send SOS periodically in between the (modified)
                                 compliance patterns.
                                 This bit is applicable when the Link is operating at 2.5 GT/s or 5 GT/s data rates only.
                                 The default value of this bit is 0b.
 15:12    0x0     RWS (func 0) Compliance Preset/De-emphasis
                  RsvdP (else) For 8.0 GT/s Data Rate:
                                This field sets the Transmitter Preset in Polling.Compliance state if the entry occurred
                                due to the Enter Compliance bit being 1b.
                               For 5.0 GT/s Data Rate:
                                This field sets the de-emphasis level in Polling.Compliance state if the entry occurred due
                                to the Enter Compliance bit being 1b.
                               When the Link is operating at 2.5 GT/s, the setting of this bit field has no effect.
                               Defined Encodings are:
                                0001b -3.5 dB
                                0000b -6 dB
                               For a Multi-Function device associated with an Upstream Port, the bit field in Function 0 is
                               of type RWS, and only Function 0 controls the component’s Link behavior. In all other
                               Functions of that device, this bit field is of type RsvdP.
                               This bit field is intended for debug, and compliance testing purposes.
                               The default value of this field is 0000b

828                                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

#### 9.2.3.7 Link Status 2 Register (0xD2; RW)

 Bit(s)      Init.        Type                                                     Description

   0           0b          RO           Current De-emphasis Level
                                        When the link is operating at 5 GT/s speed, this bit reflects the level of de-emphasis. it is
                                        undefined when the Link is operating at 2.5 GT/s speed
                                        Encodings:
                                         0b = -6 dB
                                         1b = -3.5 dB
   1           0b     ROS (Func 0) Equalization Complete
                     RsvdZ (Func 1) When set to 1b, this bit indicates that the Transmitter Equalization procedure has completed
   2           0b     ROS (Func 0) Equalization Phase 1 Successful
                     RsvdZ (Func 1) When set to 1b, this bit indicates that Phase 1 of the Transmitter Equalization procedure has
                                    successfully completed.
   3           0b     ROS (Func 0) Equalization Phase 2 Successful
                     RsvdZ (Func 1) When set to 1b, this bit indicates that Phase 2 of the Transmitter Equalization procedure has
                                    successfully completed.
   4           0b     ROS (Func 0) Equalization Phase 3 Successful
                     RsvdZ (Func 1) When set to 1b, this bit indicates that Phase 3 of the Transmitter Equalization procedure has
                                    successfully completed.
   5           0b    RW1C (Func 0) Link Equalization Request
                     RsvdZ (Func 1) This bit is Set by hardware to request the Link equalization process to be performed on the
                                    Link.
                                    This bit is available only in function zero.
  15:6         0x0        RsvdZ         Reserved.

### 9.2.4 PCIe Extended Configuration Space

PCIe configuration space is located in a flat memory-mapped address space. PCIe extends the
configuration space beyond the 256 bytes available for PCI to 4096 bytes. The X550 decodes an
additional four bits (bits 27:24) to provide the additional configuration space as shown. PCIe reserves
the remaining four bits (bits 31:28) for future expansion of the configuration space beyond 4096 bytes.
The configuration address for a PCIe device is computed using a PCI-compatible bus, device, and
function numbers as follows:

 31             28   27                      20     19                 15    14           12   11                               2   1         0

       0000b                    Bus #                     Device #                Fun #             Register Address (offset)           00b

PCIe extended configuration space is allocated using a linked list of optional or required PCIe extended
capabilities following a format resembling PCI capability structures. The first PCIe extended capability is
located at offset 0x100 in the device configuration space. The first DWord of the capability structure
identifies the capability/version and points to the next capability.
The X550 supports the following PCIe extended capabilities:

333369-009                                                                                                                                829
                                         Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    PCIe Programming Interface

Table 9-22. Extended Capabilities List
                                                                                                                           Section
                       Capability                                    Offset                    Next Header
                                                                                                                           Number

 Advanced Error Reporting                                            0x100              Any of the below / 0x000            9.2.4.1

 Serial Number                                                       0x140              Any of the below / 0x0001           9.2.4.2

 Alternative RID Interpretation (ARI)                                0x150              Any of the below / 0x0001           9.2.4.3
              2
 IOV Support                                                         0x160              Any of the below / 0x000            9.2.4.4

 TPH Requester                                                       0x1A0              Any of the below / 0x000            9.2.4.5

 Access Control Services (ACS)3                                      0x1B0              Any of the below / 0x000            9.2.4.6

 Latency Tolerance Reporting (LTR)                                   0x1C0              Any of the below / 0x000            9.2.4.7

 Secondary PCI Express                                               0x1D0                         0x000                    9.2.4.8

1. Depends on NVM settings enabling the ARI/IOV structures.
2. In a dummy function, the IOV and TPH structures are not exposed.
3. When in Single function mode (function 1 is disabled), the ACS capability is not exposed.

#### 9.2.4.1 Advanced Error Reporting Capability (AER)

The PCIe advanced error reporting capability is an optional extended capability to support advanced
error reporting. The tables that follow list the PCIe advanced error reporting extended capability
structure for PCIe devices.

Table 9-23. AER Capability Structure
   Byte Offset               Byte 3                         Byte 2                      Byte 1                       Byte 0

                                                                   Version
      0x100                  Next Capability offset                                           AER Capability ID (0x0001)
                                                                    (0x1)

      0x104                                                     Uncorrectable Error Status

      0x108                                                      Uncorrectable Error Mask

      0x10C                                                    Uncorrectable Error Severity

      0x110                                                       Correctable Error Status

      0x114                                                       Correctable Error Mask

      0x118                                           Advanced Error Capabilities and Control Register

 0x11C... 0x128                                                         Header Log

Table 9-24 summarizes configuration sharing of the AER Capability registers among the different PCI
functions.

830                                                                                                                        333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Table 9-24. Configuration Sharing of the AER Capability
              Field                            Sub-field            Shared?       Replicated?                 Comments

                                     Extended Capability ID             x
Enhanced Capability Header
                                     Capability Version                 x
Register
                                     Next Capability Offset                             x

Uncorrectable Error Status                                                              x

Uncorrectable Error Mask                                                                x

Uncorrectable Error Severity                                                            x

Correctable Error Status                                                                x

Correctable Error Mask                                                                  x

                                     First Error Pointer                                x

                                     ECRC Generation Capable            x
Advanced Error Capabilities and
                                     ECRC Generation Enable                             x         ECRC insertion is per PF.
Control
                                     ECRC Check Capable                 x

                                     ECRC Check Enable                                  x         See Section 3.1.2.7.

Header Log                                                                              x

9.2.4.1.1                  Advanced Error Reporting Enhanced Capability Header
                           Register (0x100; RO)

 Bit(s)        Init.       Type                                                Description

  15:0         0x1            RO     Extended Capability ID
                                     PCIe extended capability ID indicating advanced error reporting capability.
 19:16         0x2            RO     Version Number
                                     PCIe advanced error reporting extended capability version number.
 31:20       See              RO     Next Capability Offset
          description                Next PCIe extended capability offset.
                                     See Table 9-22 and Table 9-11 for possible values of the next capability offset.

9.2.4.1.2                  Uncorrectable Error Status Register (0x104; RW1CS)

The Uncorrectable Error Status register reports error status of individual uncorrectable error sources on
a PCIe device. An individual error status bit that is set to 1b indicates that a particular error occurred;
software can clear an error status by writing a 1b to the respective bit. Register is cleared by
LAN_PWR_GOOD.

 Bit(s)      Init.      Type                                                  Description

   0          0b         RO        Reserved.
  3:1        000b       RsvdP      Reserved.
   4          0b       RW1CS       Data Link Protocol Error Status
   5          0b         RO        Reserved.
  11:6       0x0        RsvdP      Reserved.
   12         0b       RW1CS       Poisoned TLP Status
   13         0b       RW1CS       Flow Control Protocol Error Status

333369-009                                                                                                                    831
                                         Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                    PCIe Programming Interface

 Bit(s)   Init.   Type                                         Description

  14       0b     RW1CS    Completion Timeout Status
  15       0b     RW1CS    Completer Abort Status
  16       0b     RW1CS    Unexpected Completion Status
  17       0b     RW1CS    Receiver Overflow Status
  18       0b     RW1CS    Malformed TLP Status.
  19       0b     RW1CS    ECRC Error Status
  20       0b     RW1CS    Unsupported Request Error Status
  21       0b      RO      ACS Violation Status
                           Not supported. Hard-wired to 0b.
 25:22    0x0      RO      Not Supported.
 31:26    0x0     RsvdP    Reserved.

9.2.4.1.3               Uncorrectable Error Mask Register (0x108; RWS)

The Uncorrectable Error Mask register controls reporting of individual uncorrectable errors by device to
the host bridge via a PCIe error message. A masked error (respective bit set in mask register) is not
reported to the host bridge by an individual device. Note that there is a mask bit per bit of the
Uncorrectable Error Status register.

 Bit(s)   Init.   Type                                        Description

      0    0b      RO     Reserved.
  3:1     000b    RsvdP   Reserved.
      4    0b     RWS     Data Link Protocol Error Mask
      5    0b      RO     Reserved.
  11:6    0x0     RsvdP   Reserved.
  12       0b     RWS     Poisoned TLP Mask
  13       0b     RWS     Flow Control Protocol Error Mask
  14       0b     RWS     Completion Timeout Mask
  15       0b     RWS     Completer Abort Mask
  16       0b     RWS     Unexpected Completion Mask
  17       0b     RWS     Receiver Overflow Mask
  18       0b     RWS     Malformed TLP Mask
  19       0b     RWS     ECRC Error Mask
  20       0b     RWS     Unsupported Request Error Mask
  21       0b      RO     ACS Violation Mask
 25:22    0x0      RO     Not Supported.
 31:26    0x0     RsvdP   Reserved.

832                                                                                                  333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.1.4                  Uncorrectable Error Severity Register (0x10C; RWS)

The Uncorrectable Error Severity register controls whether an individual uncorrectable error is reported
as a fatal error. An uncorrectable error is reported as fatal when the corresponding error bit in the
severity register is set. If the bit is cleared, the corresponding error is considered non-fatal.

 Bit(s)      Init.   Type                                           Description

   0          0b      RO     Reserved.
  3:1        000b    RsvdP   Reserved.
   4          1b     RWS     Data Link Protocol Error Severity
   5          0b      RO     Reserved.
  11:6       0x0     RsvdP   Reserved.
   12         0b     RWS     Poisoned TLP Severity
   13         1b     RWS     Flow Control Protocol Error Severity
   14         0b     RWS     Completion Timeout Severity
   15         0b     RWS     Completer Abort Severity
   16         0b     RWS     Unexpected Completion Severity
   17         1b     RWS     Receiver Overflow Severity
   18         1b     RWS     Malformed TLP Severity
   19         0b     RWS     ECRC Error Severity
   20         0b     RWS     Unsupported Request Error Severity
   21         0b      RO     ACS Violation Severity
 25:22       0x0      RO     Not Supported.
 31:26       0x0     RsvdP   Reserved.

9.2.4.1.5                  Correctable Error Status Register (0x110; RW1CS)

The Correctable Error Status register reports error status of individual correctable error sources on a
PCIe device. When an individual error status bit is set to 1b it indicates that a particular error occurred;
software can clear an error status by writing a 1b to the respective bit. Register is cleared by
LAN_PWR_GOOD.

 Bit(s)      Init.   Type                                           Description

   0          0b     RW1CS    Receiver Error Status
  5:1        0x0     RsvdZ    Reserved.
   6          0b     RW1CS    Bad TLP Status
   7          0b     RW1CS    Bad DLLP Status
   8          0b     RW1CS    REPLAY_NUM Rollover Status
  11:9       000b    RsvdZ    Reserved.
   12         0b     RW1CS    Replay Timer Timeout Status
   13         0b     RW1CS    Advisory Non-Fatal Error Status
 15:14       00b      RO      Reserved.

333369-009                                                                                               833
                                    Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                PCIe Programming Interface

9.2.4.1.6               Correctable Error Mask Register (0x114; RWS)

The Correctable Error Mask register controls reporting of individual correctable errors by device to the
host bridge via a PCIe error message. A masked error (respective bit set in mask register) is not
reported to the host bridge by an individual device. There is a mask bit per bit in the Correctable Error
Status register.

 Bit(s)   Init.   Type                                                  Description

      0    0b     RWS     Receiver Error Mask
  5:1     0x0     RsvdP   Reserved.
      6    0b     RWS     Bad TLP Mask
      7    0b     RWS     Bad DLLP Mask
      8    0b     RWS     REPLAY_NUM Rollover Mask
  11:9    000b    RsvdP   Reserved.
  12       0b     RWS     Replay Timer Timeout Mask
  13       1b     RWS     Advisory Non-Fatal Error Mask
                          This bit is set by default to enable compatibility with software that does not comprehend Role-Based
                          Error Reporting.
 15:14    00b      RO     Reserved.

9.2.4.1.7               Advanced Error Capabilities and Control Register (0x118;
                        RO)

 Bit(s)   Init.   Type                                                  Description

  4:0     0x0     ROS     Vector
                          Vector pointing to the first recorded error in the Uncorrectable Error Status register. This is a read-
                          only field that identifies the bit position of the first uncorrectable error reported in the Uncorrectable
                          Error Status register.
      5    1b      RO     ECRC Generation Capable
                          If set, this bit indicates that the function is capable of generating ECRC.
                          This bit is loaded from NVM. It is reflected in the PCI_CAPSUP register.
      6    0b     RWS     ECRC Generation Enable
                          When set, ECRC generation is enabled.
      7    1b      RO     ECRC Check Capable
                          If set, this bit indicates that the function is capable of checking ECRC.
                          This bit is loaded from NVM. It is reflected in the PCI_CAPSUP register.
      8    0b     RWS     ECRC Check Enable
                          When set Set, ECRC checking is enabled.
      9    0b      RO     Multiple Header Recording Capable
                          Not Supported. Hard-wired to 0b
  10       0b      RO     Multiple Header Recording Enable
                          Not Supported. Hard-wired to 0b
  11       0b     RsvdP   TLP Prefix Log Present
                          Not supported. Hard-wired to 0b
 15:12    0x0     RsvdP   Reserved.

834                                                                                                                      333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.1.8                 Header Log Register (0x11C:128; RO)

The header log register captures the header for the transaction that generated an error. This register is
16 bytes.

 Bit(s)      Init.    Type                                                    Description

 127:0       0x0      ROS      Header Log Register
                               Header of the packet in error (TLP or DLLP).

#### 9.2.4.2 Serial Number Capability

The PCIe device serial number capability is an optional extended capability that can be implemented by
any PCIe device. The device serial number is a read-only 64-bit value that is unique for a given PCIe
device.
The X550 implements this capability on all the functions and returns the same value in both.

Table 9-25. Serial Number Capability Structure
 Byte Offset                 Byte 3                      Byte 2                        Byte 1                         Byte 0

                                                                Version
    0x140                    Next Capability Offset                                         Serial ID Capability ID (0x0003)
                                                                 (0x1)

    0x144                                              Serial Number Register (Lower DWord)

    0x148                                              Serial Number Register (Upper DWord)

Table 9-26 summarizes configuration sharing of the Serial ID Capability registers among the different
PCI functions.

Table 9-26. Configuration Sharing of the Serial Number Capability
          Field                       Sub-field             Shared?       Replicated?                       Comments

                              Extended Capability ID            x
Enhanced Capability
                              Capability Version                x
Header Register
                              Next Capability Offset                              x

Serial Number Registers                                         x

333369-009                                                                                                                     835
                                        Did this document help answer your questions?

                                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                                          PCIe Programming Interface

9.2.4.2.1                      Device Serial Number Enhanced Capability Header Register
                               (0x140; RO)

 Bit(s)          Init.         Type                                                 Description

  15:0            0x3          RO       PCIe Extended Capability ID
                                        This field is a PCI-SIG defined ID number that indicates the nature and format of the extended
                                        capability.
                                        The extended capability ID for the device serial number capability is 0x0003.
 19:16            0x1          RO       Capability Version
                                        This field is a PCI-SIG defined version number that indicates the version of the capability
                                        structure present.
                                        Note: Must be set to 0x1 for this version of the specification.
 31:20           See           RO       Next Capability Offset
              description               This field contains the offset to the next PCIe capability structure or 0x000 if no other items exist
                                        in the linked list of capabilities.
                                        See Table 9-22 and Table 9-11 for possible values of the next capability offset.

9.2.4.2.2                      Serial Number Registers (0x144:0x148; RO)

The Serial Number register is a 64-bit field that contains the IEEE defined 64-bit Extended Unique
Identifier (EUI-64*). The register at offset 0x144 holds the lower 32 bits and the register at offset
0x148 holds the higher 32 bits. The following figure details the allocation of register fields in the Serial
Number register.

 Bit(s)        Type                                                         Description

  63:0          RO       PCIe Device Serial Number
                         This field contains the IEEE defined 64-bit EUI-64*. This identifier includes a 24-bit company ID value assigned
                         by IEEE registration authority and a 40-bit extension identifier assigned by the manufacturer.

The serial number uses the Ethernet MAC Address according to the following definition:

      Field                       Company ID                                                Extension Identifier

      Order           Addr+0           Addr+1        Addr+2          Addr+3         Addr+4         Addr+5          Addr+6            Addr+7

              Most Significant Byte                                                                         Least Significant Byte

               Most Significant Bit                                                                          Least Significant Bit

The serial number can be constructed from the 48-bit Ethernet MAC Address in the following form:

      Field                      Company ID                              MAC Label                         Extension identifier

      Order          Addr+0           Addr+1        Addr+2         Addr+3         Addr+4          Addr+5           Addr+6            Addr+7

              Most Significant Bytes                                                                       Least Significant Byte

               Most Significant Bit                                                                        Least Significant Bit

In this case, the MAC label is 0xFFFF.

836                                                                                                                                 333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

For example, assume that the company ID is (Intel) 00-A0-C9 and the extension identifier is 23-45-67.
In this case, the 64-bit serial number is:

   Field                     Company ID                                    MAC Label                         Extension Identifier

   Order           Addr+0          Addr+1         Addr+2        Addr+3            Addr+4         Addr+5             Addr+6             Addr+7

# 00 A0              C9                FF               FF             23               45

           Most Significant Byte                                                                              Least Significant Byte

            Most Significant Bit                                                                               Least Significant Bit

The Ethernet MAC Address for the serial number capability is loaded from the NVM (not the same field
that is loaded from NVM into the RAL and RAH registers). It is reflected in the PCI_SERL and PCI_SERH
registers. The default value in case of no NVM is 0x0.
Note:        The official document that defines EUI-64* is:
              http://standards.ieee.org/regauth/oui/tutorials/EUI64.html

#### 9.2.4.3 Alternate Routing ID Interpretation (ARI) Capability

To allow more than eight functions per endpoint without requesting an internal switch, as is usually
needed in virtualization scenarios, the PCI-SIG defines a new capability that allows a different
interpretation of the Bus, Device, and Function fields. The capability is exposed when the
PCI_CAPSUP.ARI_EN bit is set from NVM.
The ARI capability structure is as follows:

Table 9-27. ARI Capability Structure
 Byte Offset                 Byte 3                          Byte 2                          Byte 1                           Byte 0

                                                                     Version
    0x150                    Next Capability Offset                                             ARI Capability ID (0x000E)
                                                                      (0x1)

    0x154                             ARI Control Register                                                 ARI Capabilities

Table 9-28 summarizes configuration sharing of the ARI Capability registers among the different PCI
functions.

Table 9-28. Configuration Sharing of the ARI Capability
           Field                      Sub-field               Shared?          Replicated?                        Comments

                             Extended Capability ID              x
Enhanced Capability
                             Capability Version                  x
Header Register
                             Next Capability Offset                                x

ARI capability Register      Next Function Pointer                                 x

333369-009                                                                                                                                      837
                                            Did this document help answer your questions?

                                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                               PCIe Programming Interface

9.2.4.3.1                       PCIe ARI Header Register (0x150; RO)

       Field         Bit(s)           Init.         Type                                          Description

ID                       15:0          0xE            RO       PCIe Extended Capability ID
                                                               PCIe extended capability ID for the alternative RID interpretation.
Version              19:16             0x1            RO       Capability Version
                                                               This field is a PCI-SIG defined version number that indicates the version of the
                                                               capability structure present.
                                                               Must be 0x1 for this version of the specification.
Next Capability      31:20            See             RO       Next Capability Offset
Offset                             description                 This field contains the offset to the next PCIe extended capability structure.
                                                               See Table 9-22. and Table 9-11 for possible values of the next capability offset.

9.2.4.3.2                       PCIe ARI Capabilities and Control Register (0x154; RO)

      Field      Bit(s)             Init.          Type                                           Description

Reserved           7:0              0x2             RO     Reserved.
NFP               15:8          0x1 (func 0)        RO     Next Function Pointer
                                0x0 (func 1)1              This field contains the pointer to the next physical function configuration space
                                                           or 0x0000 if no other items exist in the linked list of functions. Function 0 is the
                                                           start of the link list of functions.
Reserved          31:16             0x0             RO     Reserved.

1. Even if port 0 and port 1 are switched or function zero is a dummy function, this register should keep its attributes according to
   the function number. If LAN1 is disabled, the value of this field in function zero should be zero.

#### 9.2.4.4 IOV Capability

Note:          This capability structure is not exposed in a dummy function.
This is a structure used to support the SR-IOV capabilities reporting and control. The capability is
exposed when the PCI_CAPSUP.IOV_EN bit is set from NVM and the PCI_CNF2.NUM_VFS is non zero.

Table 9-29. IOV Capability Structure
  Byte Offset                    Byte 3                           Byte 2                          Byte 1                          Byte 0

                                                                         Version
      0x160                 Next Capability Offset (0x0)                                              IOV Capability ID (0x0010)
                                                                          (0x1)

      0x164                                                                 SR IOV Capabilities

      0x168                                   SR IOV Status                                                  SR IOV Control

      0x16C                                   Total VFs (RO)                                                 Initial VF (RO)

                                                       Function Dependency Link
      0x170                     Reserved                                                                      Num VF (RW)
                                                                 (RO)

      0x174                                   VF Stride (RO)                                               First VF Offset (RO)

      0x178                                     VF Device ID                                                    Reserved

      0x17C                                                           Supported Page Size (0x553)

      0x180                                                              System Page Size (RW)

      0x184                                                                VF BAR0 — Low (RW)

      0x188                                                              VF BAR0 — High (RW)

838                                                                                                                                   333369-009
                                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Table 9-29. IOV Capability Structure [continued]
 Byte Offset               Byte 3                    Byte 2                      Byte 1                         Byte 0

    0x18C                                                       VF BAR2 (RO)

    0x190                                                VF BAR3- Low (RW) (64 bit)

    0x194                                                VF BAR3 High (RW) (64 bit)

    0x198                                                       VF BAR5 (RO)

    0x19C                                            VF Migration State Array Offset (RO)

Table 9-30 summarizes configuration sharing of the SR-IOV Capability registers among the different PCI
functions.

Table 9-30. Configuration Sharing of the SR-IOV Capability
             Field                  Sub-field           Shared?      Replicated?                       Comments

                            Extended Capability ID          x
Enhanced Capability
                            Capability Version              x
Header Register
                            Next Capability Offset                         x

                            VF Migration Capable            x                         Not supported.

                            ARI Capable Hierarchy
                                                                           x          PF0 only. RO zero in all other functions.
SR-IOV Capabilities         Preserved

                            VF Migration Interrupt
                                                                                      Not supported.
                            Message Number

                            VF Enable                                      x

SR-IOV Control              Memory Space Enable                            x

                            ARI Capable Hierarchy           x                         PF0 only. RO zero in all other functions.

InitialVFs                                                                 x

TotalVFs                                                                   x

NumVFs                                                                     x

Function Dependency Link                                                   x          Each PF indicates its PF number here.

First VF Offset                                                            x

VF Stride                                                                  x

VF Device ID                                                               x

Supported Page Size                                         x

System Page Size                                                           x

VF BARs                                                                    x

333369-009                                                                                                                        839
                                     Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                      PCIe Programming Interface

9.2.4.4.1                PCIe SR-IOV Header Register (0x160; RO)

      Field    Bit(s)      Init.           Type                                         Description

ID              15:0       0x10            RO       PCIe Extended Capability ID
                                                    PCIe extended capability ID for the SR-IOV capability.
Version        19:16        0x1            RO       Capability Version
                                                    This field is a PCI-SIG defined version number that indicates the version of the
                                                    capability structure present.
                                                    Must be 0x1 for this version of the specification.
Next offset    31:20       See             RO       Next Capability Offset
                        description                 This field contains the offset to the next PCIe extended capability structure or
                                                    0x000 if no other items exist in the linked list of capabilities.
                                                    See Table 9-22. and Table 9-11 for possible values of the next capability offset.

9.2.4.4.2                PCIe SR-IOV Capabilities Register (0x164; RO)

      Field    Bit(s)    Init.     Type                                               Description

Reserved         0        0b          RO        Reserved.
ARICHP           1      1b/0b1        RO        ARI Capable Hierarchy Preserved
                                                If set, the ARI Capable Hierarchy bit is preserved across certain power state transitions.
Reserved        31:2      0x0         RO        Reserved.

1. Set on first function where SR-IOV is enabled (see PCI_CAPSUP.IOV_EN bit) and Read Only Zero in the other PF.

9.2.4.4.3                PCIe SR-IOV Control/Status Register (0x168; RW)

      Field    Bit(s)    Init.              Type                                             Description

VFE              0        0b                 RW              VF Enable/Disable
                                                             VF Enable manages the assignment of VFs to the associated PF. If VF
                                                             Enable is set to 1b, VFs must be enabled, associated with the PF, and
                                                             exists in the PCIe fabric. When enabled, VFs must respond to and can
                                                             issue PCIe transactions following all other rules for PCIe functions.
                                                             If set to 0b, VFs must be disabled and not visible in the PCIe fabric; VFs
                                                             cannot respond to or issue PCIe transactions.
                                                             In addition, if VF Enable is cleared after having been set, all of the VFs
                                                             must no longer:
                                                               • Issue PCIe transactions
                                                               • Respond to configuration space or memory space accesses.
                                                             The behavior must be as if an FLR was issued to each of the VFs.
                                                             Specifically, VFs must not retain any context after VF Enable has been
                                                             cleared. Any errors already logged via PF error reporting registers, remain
                                                             logged. However, no new VF errors must be logged after VF Enable is
                                                             cleared.
Reserved        2:1       00b                RO              Reserved.
VF MSE           3        0b                 RW              Memory Space Enable for Virtual Functions
                                                             VF MSE controls memory space enable for all VFs associated with this PF
                                                             as with the Memory Space Enable bit in a functions PCI command register.
                                                             The default value for this bit is 0b.
                                                             When VF Enable is 1, virtual function memory space access is permitted
                                                             only when VF MSE is Set. VFs must follow the same error reporting rules
                                                             as defined in the base specification if an attempt is made to access a
                                                             virtual functions memory space when VF Enable is 1 and VF MSE is zero.
                                                             Implementation Note: Virtual functions memory space cannot be accessed
                                                             when VF Enable is zero. Thus, VF MSE is “don't care” when VF Enable is
                                                             zero, however, software may choose to set VF MSE after programming the
                                                             VF BARn registers, prior to setting VF Enable to 1.

840                                                                                                                           333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

    Field       Bit(s)     Init.               Type                                            Description

ARI Capable       4         0b                   RW            ARI Capable Hierarchy
Hierarchy                              (first function where   The X550 is permitted to locate VFs in function numbers 8 to 255 of the
                                        SR-IOV is enabled)     captured bus number.
                                                 ROS           This field is R/W in the lowest numbered PF. Other functions use the PF0
                                         (other function)1     value as sticky.
                                                               Note: If either ARI Capable Hierarchy Preserved is set (see
                                                                         Section 9.2.4.4.2) or No_Soft_Reset is set, a power state
                                                                         transition of this PF from D3hot to D0 does not affect the value of
                                                                         this bit.
Reserved         31:5      0x0                  RO             Reserved.

1. Even if port 0 and port 1 are switched or function zero is a dummy function, this field should keep its attributes according to the
   function number.

9.2.4.4.4                  PCIe SR-IOV Max/Total VFs Register (0x16C; RO)

    Field       Bit(s)     Init.        Type                                            Description

InitialVFs       15:0       64           RO      InitialVFs
                                                 Indicates the number of VFs that are initially associated with the PF. If VF Migration
                                                 Capable is cleared, this field must contain the same value as TotalVFs.
                                                 In the X550 this parameter is equal to the TotalVFs in this register.
TotalVFs        31:16       64           RO      TotalVFs
                                                 Defines the maximum number of VFs that can be associated with the PF. This field is
                                                 loaded from the Max VFs field in the NVM. Reflected in PCI_CNF2.TOTAL_VFS.

9.2.4.4.5                  PCIe SR-IOV Num VFs Register (0x170; RW)

    Field       Bit(s)        Init.            Type                                         Description

NumVFs           15:0            0x0            RW      Num VFs
                                                        Defines the number of VFs software has assigned to the PF. Software sets
                                                        NumVFs to any value between one and the TotalVFs as part of the process of
                                                        creating VFs. NumVFs VFs must be visible in the PCIe fabric after both NumVFs
                                                        is set to a valid value VF Enable is set to 1b.
FDL             23:16     0x0 (func 0)          RO      Function Dependency Link
                          0x1 (func 1)1                 Defines dependencies between physical functions allocation. In the X550 there
                                                        are no constraints.
Reserved        31:24            0x0            RO      Reserved.

1. Even if port 0 and port 1 are switched or function zero is a dummy function, this register should keep it’s attributes according to
   the function number.

9.2.4.4.6                  PCIe SR-IOV VF RID Mapping Register (0x174; RO)

    Field       Bit(s)     Init.        Type                                            Description

FVO              15:0     0x180          RO      First VF offset
                                                 Defines the requestor ID (RID) offset of the first VF that is associated with the PF that
                                                 contains this capability structure. The first VFs 16-bit RID is calculated by adding the
                                                 contents of this field to the RID of the PF containing this field.
                                                 The content of this field is valid only when VF Enable is set. If VF Enable is 0b, the
                                                 contents are undefined.
                                                 If the ARI Enable bit is set, this field changes to 0x80.

333369-009                                                                                                                                841
                                           Did this document help answer your questions?

                                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                           PCIe Programming Interface

      Field      Bit(s)     Init.      Type                                               Description

VFS              31:16      0x21            RO      VF stride
                                                    Defines the requestor ID (RID) offset from one VF to the next one for all VFs associated
                                                    with the PF that contains this capability structure. The next VFs 16-bit RID is calculated
                                                    by adding the contents of this field to the RID of the current VF.
                                                    The contents of this field is valid only when VF Enable is set and NumVFs is non-zero. If
                                                    VF Enable is 0b or if NumVFs is zero, the contents are undefined.

1. See Section 7.8.2.6.1.

                                                  VF #1                    VF #2                     VF #3

                          First VF Offset        VF Stride               VF Stride                VF Stride

9.2.4.4.7                   PCIe SR-IOV VF Device ID Register (0x178; RO)

      Field      Bit(s)      Init.          Type                                           Description

DEVID            31:16      0x1565          RO       VF Device ID
                                                     This field contains the device ID that should be presented for every VF to the Virtual
                                                     Machine (VM).
                                                     The value of this field can be read from the IOV Control Word 2 in the NVM.
Reserved         15:0         0x0           RO       Reserved.

9.2.4.4.8                   PCIe SR-IOV Supported Page Size Register (0x17C; RO)

         Field            Bit(s)      Init.         Type                                       Description

Supported Page Size        31:0      0x553           RO      Supported Page Size
                                                             For PFs that supports the stride-based BAR mechanism, this field defines the
                                                             supported page sizes. This PF supports a page size of 2^(n+12) if bit n is set.
                                                             For example, if bit 0 is Set, the Endpoint (EP) supports 4KB page sizes.
                                                             Endpoints are required to support 4 KB, 8 KB, 64 KB, 256 KB, 1 MB and 4 MB
                                                             page sizes. All other page sizes are optional.

9.2.4.4.9                   PCIe SR-IOV System Page Size Register (0x180; RW)

      Field      Bit(s)     Init.      Type                                               Description

Page Size        31:0        0x1            RW      Page Size
                                                    This field defines the page size the system uses to map the PF's and associated VFs'
                                                    memory addresses. Software must set the value of the System Page Size to one of the
                                                    page sizes set in the Supported Page Sizes field. As with Supported Page Sizes, if bit n
                                                    is set in System Page Size, the PF and its associated VFs are required to support a page
                                                    size of 2^(n+12). For example, if bit 1 is set, the system is using an 8 KB page size.
                                                    The results are undefined if more than one bit is set in System Page Size. The results
                                                    are undefined if a bit is set in System Page Size that is not set in Supported Page Sizes.
                                                    When System Page Size is set, the PF and associated VFs are required to align all BAR
                                                    resources on a System Page Size boundary. Each BAR size, including VF BARn Size
                                                    (described later) must be aligned on a System Page Size boundary. Each BAR size,
                                                    including VF BARn Size must be sized to consume a multiple of System Page Size
                                                    bytes. All fields requiring page size alignment within a function must be aligned on a
                                                    System Page Size boundary. VF Enable must be zero when System Page Size is set.
                                                    The results are undefined if System Page Size is set when VF Enable is set.

842                                                                                                                               333369-009
                                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.4.10                  PCIe SR-IOV BAR 0 — Low Register (0x184; RW)

       Field      Bit(s)        Init.          Type                                          Description

Mem                     0           0b           RO       Memory
                                                           0b = Indicates memory space.
Mem Type              2:1         10b            RO       Memory Type
                                                          Indicates the address space size.
                                                           10b = 64-bit.
                                                          This bit is loaded from the NVM. It is reflected in the PCI_VFSUP register.
Prefetch Mem            3         0b*            RO       Prefetch Memory
                                                           0b = Non-prefetchable space.
                                                           1b = Prefetchable space.
                                                          This bit is loaded from the NVM. It is reflected in the PCI_VFSUP register.
Memory Address     31:4             0x0        RW         Memory Address Space
Space                                                     Which bits are RW bits and which are RO to 0x0 depend on the memory mapping
                                                          window size. The size is a maximum between 16 KB and the page size.

9.2.4.4.11                  PCIe SR-IOV BAR 0 — High Register (0x188; RW)

      Field      Bit(s)       Init.         Type                                             Description

BAR0 — MSB        31:0         0x0          RW          MSB part of BAR0.

9.2.4.4.12                  PCIe SR-IOV BAR 2 Register (0x18C; RO)

   Field       Bit(s)       Init.         Type                                             Description

BAR2           31:0         0x0           RO          This BAR is not used.

9.2.4.4.13                  PCIe SR-IOV BAR 3 — Low Register (0x190; RW)

       Field      Bit(s)        Init.          Type                                          Description

Mem                     0           0b           RO       Memory
                                                           0b = Indicates memory space.
Mem Type              2:1         10b            RO       Memory Type
                                                          Indicates the address space size.
                                                           10b = 64-bit.
                                                          This bit is loaded from the NVM. It is reflected in the PCI_VFSUP register.
Prefetch Mem            3         0b*            RO       Prefetch Memory
                                                           0b = Non-prefetchable space.
                                                           1b = Prefetchable space.
                                                          This bit is loaded from the NVM. It is reflected in the PCI_VFSUP register.
Memory Address     31:4             0x0        RW         Memory Address Space
Space                                                     Which bits are RW bits and which are RO to 0x0 depend on the memory mapping
                                                          window size. The size is a maximum between 16 KB and the page size.

333369-009                                                                                                                              843
                                            Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                        PCIe Programming Interface

9.2.4.4.14                      PCIe SR-IOV BAR 3 — High Register (0x194; RW)

       Field           Bit(s)     Init.     Type                                          Description

BAR4 — MSB             31:0        0x0       RW        MSB part of BAR3.

9.2.4.4.15                      PCIe SR-IOV BAR 5 Register (0x198; RO)

      Field        Bit(s)       Init.     Type                                           Description

BAR5               31:0         0x0       RO       This BAR is not used

9.2.4.4.16                      PCIe SR-IOV VF Migration State Array Offset Register
                                (0x19C; RO)

      Field        Bit(s)       Init.     Type                                           Description

Reserved           31:0         0x0       RO       Reserved.

#### 9.2.4.5 TPH Requester Capability

The TPH Requester capability is an optional extended capability to support TLP Processing Hints.
Table 9-31 lists the TPH extended capability structure for PCIe devices.

Table 9-31. TPH Requester Capability Structure
 Byte Offset                     Byte 3                        Byte 2                       Byte 1                      Byte 0

                                                                      Version
      0x1A0                      Next Capability Offset                                         TPH Capability ID (0x0017)
                                                                       (0x1)

      0x1A4                                                     TPH Requester Capability Register

      0x1A8                                                      TPH Requester Control Register

Table 9.2.4.5.3 summarizes configuration sharing of the TPH Requester Capability registers among the
different PCI functions.

Table 9-32. Configuration Sharing of the TPH Requester Capability
               Field                      Sub-field               Shared?       Replicated?                   Comments

                                  Extended Capability ID             x
Enhanced Capability
                                  Capability Version                 x
Header Register
                                  Next Capability Offset                            x

TPH Requester Capability                                             x

TPH Requester Control                                                                x

                                                                                               The Steering Table Upper fields are not
TPH ST Table                                                                         x
                                                                                               supported

844                                                                                                                           333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.5.1                    TPH Requester Extended Capability Header (0x1A0; RO)

 Bit(s)        Init.         Type                                                 Description

  15:0         0x17           RO       Extended Capability ID
                                       PCIe extended capability ID indicating TPH capability.
 19:16         0x1            RO       Capability Version
                                       PCIe TPH extended capability version number.
 31:20       See              RO       Next Capability Offset
          description                  This field contains the offset to the next PCIe capability structure.
                                       See Table 9-22. and Table 9-11 for possible values of the next capability offset.

9.2.4.5.2                    TPH Requester Capability Register (0x1A4; RO)

 Bit(s)      Init.     Type                                                    Description

   0          1b        RO         No ST Mode Supported
                                   If set indicates that the Function supports the No ST Mode of operation
   1          0b        RO         Interrupt Vector Mode Supported
                                   Cleared to indicates that the X550 does not support Interrupt Vector Mode of operation
   2          1b        RO         Device Specific Mode
                                   Set to indicate that the X550 supports Device Specific Mode of operation
  7:3        0x0        RO         Reserved.
   8          0b        RO         Extended TPH Requester Supported
                                   Cleared to indicate that the function is not capable of generating requests with Extended TPH TLP
                                   Prefix
  10:9       00b        RO         ST Table Location
                                   Value indicates if and where the ST Table is located.
                                   Defined Encodings are:
                                    00b = ST Table is not present.
                                    01b = ST Table is located in the TPH Requester Capability structure.
                                    10b = ST Table is located in the MSI-X Table structure.
                                    11b = Reserved
                                   ST Table is not supported.
 15:11       0x0        RO         Reserved.
 26:16       0x0        RO         ST_Table Size
                                   System software reads this field to determine the ST_Table_Size N, which is encoded as N-1. For
                                   example, a returned value of 00000000011b indicates a table size of 4.
                                   The value in this field is undefined since the X550 does not support an ST Table
 31:27       0x0        RO         Reserved.

333369-009                                                                                                                             845
                                           Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                        PCIe Programming Interface

9.2.4.5.3                    TPH Requester Control Register (0x1A8; R/W)

 Bit(s)       Init.     Type                                                    Description

  2:0         000b      RW          ST Mode Select
                                    Indicates the ST mode of operation selected.
                                    Defined encodings are:
                                     000b = No Table Mode
                                     001b = Interrupt Vector Mode (not supported by the X550)
                                     010b = Device Specific Mode
                                     All other values are reserved.
                                    The default value of 000 indicates No Table mode of operation.
                                    Functions that support only the No ST Mode of operation must hard-wire this field to 000b.
  7:3         0x0       RO          Reserved.
  9:8         00b       RW          TPH Requester Enable
                                    Controls the ability to issue Request TLPs using either TPH or Extended TPH.
                                    Defined Encodings are:
                                     00b = The X550 is not permitted to issue transactions with TPH or Extended TPH as Requester
                                     01b = The X550 is permitted to issue transactions with TPH as Requester and is not permitted to
                                            issue transactions with Extended TPH as Requester
                                     10b = Reserved
                                     11b = The X550 is permitted to issue transactions with TPH and Extended TPH as Requester (The
                                            X550 does not issue transactions with Extended TPH).
                                    The default value of this field is 00b.
 31:10        0x0       RO          Reserved.

#### 9.2.4.6 Access Control Services (ACS) Capability

The PCIe ACS defines a set of control points within a PCIe topology to determine whether a TLP should
be routed normally, blocked, or redirected. ACS is applicable to RCs, switches, and multifunction
devices and is not exposed in Single function mode (when function 1 is disabled). The capability is
exposed when the PCI_CAPSUP.ACS_EN bit is set from NVM.
The ACS Capability structure is shared and exposed to all PFs.
Table 9-33 lists the PCIe ACS extended capability structure for PCIe devices.

Table 9-33. ACS Capability Structure
 Byte Offset                   Byte 3                         Byte 2                        Byte 1                          Byte 0

                                                                     Version
      0x1B0                    Next Capability Offset                                              ACS Capability ID (0x0D)
                                                                      (0x1)

      0x1B4                          ACS Control Register (0x0)                                  ACS Capability Register (0x0)

9.2.4.6.1                    ACS CAP ID (0x1B0; RO)

 Bit(s)         Init.        Type                                                  Description

  15:0         0x0D            RO       ACS Capability ID
                                        PCIe extended capability ID indicating ACS capability.
 19:16          0x1            RO       Version Number
                                        PCIe ACS extended capability version number.
 31:20       See               RO       Next Capability Pointer
          description                   This is the last capability, so the next pointer is 0x000.
                                        See Table 9-22. and Table 9-11 for possible values of the next capability offset.

846                                                                                                                              333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.6.2                 ACS Control and Capabilities (0x1B4; RO)

 Bit(s)      Init.   Type                                              Description

   0          0b     RO     ACS Source Validation (V)
                            Hard-wired to zero, not supported in the X550.
   1          0b     RO     ACS Translation Blocking (B)
                            Hard-wired to zero, not supported in the X550.
   2          0b     RO     ACS P2P Request Redirect (R)
                            Hard-wired to zero, not supported in the X550.
   3          0b     RO     ACS P2P Completion Redirect (C)
                            Hard-wired to zero, not supported in the X550.
   4          0b     RO     ACS Upstream Forwarding (U)
                            Hard-wired to zero, not supported in the X550.
   5          0b     RO     ACS P2P Egress Control (E)
                            Hard-wired to zero, not supported in the X550.
   6          0b     RO     ACS Direct Translated P2P (T)
                            Hard-wired to zero, not supported in the X550.
   7          0b     Rsrv   Reserved.
  15:8       0x0     RO     Egress Control Vector Size
                            Hard-wired to zero, not supported in the X550.
   16         0b     RO     ACS Source Validation Enable (V)
                            Hard-wired to zero, not supported in the X550.
   17         0b     RO     ACS Translation Blocking Enable (B)
                            Hard-wired to zero, not supported in the X550.
   18         0b     RO     ACS P2P Request Redirect Enable (R)
                            Hard-wired to zero, not supported in the X550.
   19         0b     RO     ACS P2P Completion Redirect Enable (C)
                            Hard-wired to zero, not supported in the X550.
   20         0b     RO     ACS Upstream Forwarding Enable (U)
                            Hard-wired to zero, not supported in the X550.
   21         0b     RO     ACS P2P Egress Control Enable (E)
                            Hard-wired to zero, not supported in the X550.
   22         0b     RO     ACS Direct Translated P2P Enable (T)
                            Hard-wired to zero, not supported in the X550.
 31:23       0x0     Rsrv   Reserved.

333369-009                                                                           847
                                    Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                        PCIe Programming Interface

#### 9.2.4.7 Latency Tolerance Reporting (LTR) Capability

The Latency Tolerance Reporting Capability is an optional Extended Capability that allows software to
provide platform latency information to devices with upstream ports (Endpoints and Switches). This
capability structure is required if the device supports Latency Tolerance Reporting (LTR). The capability
is exposed when the PCI_CAPSUP.LTR_EN bit is set from NVM.
The LTR Capability structure is implemented only in Function 0 even when Function 0 is a dummy
function, and controls the component’s Link behavior on behalf of all the Functions of the device
Table 9-34 lists the PCIe LTR extended capability structure for PCIe devices.

Table 9-34. LTR Capability Structure
 Byte Offset                   Byte 3                         Byte 2                       Byte 1                          Byte 0

      0x1C0                                                 PCI Express Extended Capability Header

      0x1C4                     Max No-Snoop Latency Register                                    Max Snoop Latency Register

9.2.4.7.1                    LTR Extended Capability Header (0x1C0; RO)

 Bit(s)         Init.      Type                                                    Description

  15:0          0x18           RO       PCI Express Extended Capability ID
                                        PCIe extended capability ID indicating LTR capability.
 19:16          0x1            RO       Capability Version
                                        PCIe LTR extended capability version number.
 31:20       See               RO       Next Capability Offset
          description                   See Table 9-22 and Table 9-11 for possible values of the next capability offset.

9.2.4.7.2                    Max Snoop Latency Register (0x1C4; RW)

 Bit(s)       Init.     Type                                                    Description

  9:0         0x0       RW          Maximum Snoop Latency Value
                                    Along with the Max Snoop Latency Scale field, this register specifies the maximum snoop latency that
                                    a device is permitted to request. Software should set this to the platform’s maximum supported
                                    latency or less.
                                    Field is also an indicator of the platform maximum latency, should an endpoint send up LTR Latency
                                    Values with the Requirement bit not set.
 12:10        000b      RW          Max Snoop Latency Scale
                                    This field provides a scale for the value contained within the Maximum Snoop Latency Value field.
                                    Encoding:
                                     000b = Value times 1 ns
                                     001b = Value times 32 ns
                                     010b = Value times 1,024 ns
                                     011b = Value times 32,768 ns
                                     100b = Value times 1,048,576 ns
                                     101b = Value times 33,554,432 ns
                                     110b = Not permitted
                                     111b = Not permitted
 15:13        0x0       RW          Reserved.

848                                                                                                                            333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.2.4.7.3                   Max No-Snoop Latency Register (0x1C6; RW)

 Bit(s)      Init.     Type                                                    Description

  9:0        0x0       RW          Maximum No-Snoop Latency Value
                                   Along with the Max No-Snoop Latency Scale field, this register specifies the maximum no-snoop
                                   latency that a device is permitted to request. Software should set this to the platform’s maximum
                                   supported latency or less.
                                   Field is also an indicator of the platforms maximum latency, should an endpoint send up LTR Latency
                                   Values with the Requirement bit not set.
 12:10       000b      RW          Max No-Snoop Latency Scale
                                   This field provides a scale for the value contained within the Maximum No-Snoop Latency Value field.
                                   Encoding:
                                    000b = Value times 1 ns
                                    001b = Value times 32 ns
                                    010b = Value times 1,024 ns
                                    011b = Value times 32,768 ns
                                    100b = Value times 1,048,576 ns
                                    110b = Not permitted
                                    111b = Not permitted
 15:13       0x0       RW          Reserved.

#### 9.2.4.8 Secondary PCI Express Extended Capability

The Secondary PCI Express Extended Capability structure is required for all Ports and RCRBs that
support a Link speed of 8.0 GT/s or higher. For Multi-Function Upstream Ports, this capability must be
implemented in Function 0 and must not be implemented in other Functions. The capability is exposed
when the PCI_CAPSUP.SEC_EN bit is set from NVM.
Table 9-35 lists the Secondary PCI Express extended capability structure for PCIe devices.

Table 9-35. Secondary PCI Express Extended Capability Structure
 Byte Offset                  Byte 3                         Byte 2                       Byte 1                        Byte 0

    0x1D0                                                  PCI Express Extended Capability Header

    0x1D4                                                          Link Control 3 Register

    0x1D8                                                         Lane Error Status Register

    0x1DC                                       Equalization Control Register (Sized by Maximum Link Width)

    0x1E0                                       Equalization Control Register (Sized by Maximum Link Width)

9.2.4.8.1                   Secondary PCIe Extended Capability Header (0x1D0)

 Bit(s)        Init.      Type                                                   Description

  15:0         0x19           RO       PCI Express Extended Capability ID
                                       This field is a PCI-SIG defined ID number that indicates the nature and format of the Extended
                                       Capability.
                                       PCI Express Extended Capability ID for the Secondary PCI Express Extended Capability is 0019h.

 19:16         0x1            RO       Capability Version
                                       This field is a PCI-SIG defined version number that indicates the version of the Capability
                                       structure present.
                                       Must be 1h for this version of the specification.

333369-009                                                                                                                           849
                                           Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                       PCIe Programming Interface

 Bit(s)      Init.         Type                                                 Description

 31:20       See            RO       Next Capability Offset
          description                See Table 9-22. and Table 9-11 for possible values of the next capability offset.

9.2.4.8.2                  Link Control 3 Register (0x1D4)

 Bit(s)   Init.         Type                                                   Description

      0     0b       RW/RsvdP      Perform Equalization
                                   When this bit is 1b and a 1b is written to the Link Retrain register with Target Link Speed set to 8.0
                                   GT/s, the Downstream Port must perform Transmitter Equalization.
                                   This bit is RW for Upstream Ports when Crosslink Supported is 1b. This bit is not applicable and is
                                   RsvdP for Upstream Ports when the Crosslink Supported bit is 0b.
                                   The default value is 0b.
      1     0b       RW/RsvdP      Link Equalization Request Interrupt Enable
                                   When Set, this bit enables the generation of interrupt to indicate that the Link Equalization
                                   Request bit has been set.
                                   This bit is RW for Upstream Ports when Crosslink Supported is 1b. This bit is not applicable and is
                                   RsvdP for Upstream Ports when the Crosslink Supported bit is 0b.
                                   The default value for this bit is 0b.
  31:2     0x0          RsvdZ      Reserved.

9.2.4.8.3                  Lane Error Status Register (0x1D8)

The Lane Error Status register consists of a 32-bit vector, where each bit indicates if the corresponding
PCI Express Lane detected an error.

 Bit(s)   Init.         Type                                                  Description

  7:0      0x0       RW1CS        Lane Error Status Bits
                                  Each bit indicates if the corresponding Lane detected a Lane-based error. A value of 1b indicates
                                  that a Lane based-error was detected on the corresponding Lane Number.
                                  The default value of this field is 0b.
                                  This field is intended for debug purposes only.
  31:8     0x0          RsvdZ     Reserved.

9.2.4.8.4                  Lane Equalization Control Register (0x1DC: 0x1E3)

The Equalization Control register consists of control fields required for per Lane equalization and
number of entries in this register are sized by Maximum Link Width.

15                                                                                                                                     0

                                                 Lane (0) Equalization Control Register

                                                 Lane (1) Equalization Control Register

                                                                    ...

                                     Lane (Maximum Link Width - 1) Equalization Control Register

Lane ((Maximum Link Width – 1):0) Equalization Control Register:

850                                                                                                                          333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

 Bit(s)      Init.     Type                                                    Description

  3:0        0x0      RsvdP      Downstream Port Transmitter Preset
                                 For an Upstream Port if Crosslink Supported is 0b, this field is RsvdP.

  6:4        000b     RsvdP      Downstream Port Receiver Preset Hint
                                 For an Upstream Port if Crosslink Supported is 0b, this field is RsvdP.

  11:8       0xF        RO       Upstream Port Transmitter Preset
                                 Field contains the Transmit Preset value sent or received during Link Equalization.
                                 Since crosslink is not supported, the field is intended for debug and diagnostics. It contains the
                                 value captured from the associated Lane during Link Equalization. Field is RO.
                                 The default value is 1111b.

 14:12       111b    HwInit/RO   Upstream Port Receiver Preset Hint
                                 Field contains the Receiver Preset Hint value sent or received during Link Equalization. Field
                                 usage varies as follows:
                                 Since crosslink is not supported, the field is intended for debug and diagnostics. It contains the
                                 value captured from the associated Lane during Link Equalization. Field is RO.
                                 The default value is 111b.

   15         0b       Rsvd      Reserved.

### 9.2.5 Driver Forward Compatibility Register (0x94; RO)

This register is an advisory register that returns a fixed value indicating the type of software device
driver class needed for this device.

 Bit(s)      Init.    Type                                                    Description

  15:0    0xFFFF       RO     Pointer to Admin Queues
                              A value of 0xFFFF indicates that this device does not support admin. queues.
 19:16        0x0      RO     Status
                              Not implemented in the X550.
 31:20       0xA0A     RO     Signature
                              Signature indicating a driver class register.

### 9.2.6 CSR Access Via Configuration Address Space

The registers described in the section are not part of the PCI Express standard configuration and can be
used to access the CSR space before memory BARs are allocated. When this mechanism is used, there
is no need to expose an I/O BAR for pre boot operation.
Note:        These registers are not available for dummy functions.

333369-009                                                                                                                       851
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   PCIe Programming Interface

#### 9.2.6.1 IOADDR Register (0x98; R/W)

This is a read/write register. Each function has its own IOADDR register. Functionality is the same in all
functions. Register is cleared at power-up (LAN_PWR_GOOD) or PCIe reset.
Note:       When functioning in a D3 state, software should not attempt to access CSRs via the IOADDR
            and IODATA registers.

 Bit(s)     Init.     Type                                                 Description

  30:0       0x0      R/W1    Internal Register or Internal Memory location Address
                               0x00000-0x1FFFF =     Internal registers and memories
                               0x20000-0x7FFFFFFF = Undefined
   31        0b       R/W     Configuration IO Access Enable
                               0b = CSR configuration read or write disabled.
                               1b = CSR configuration read or write enabled.
                              When this bit is set, accesses to the IODATA register actually generate transactions to the X550.
                              Otherwise, accesses to the IODATA register are don't-cares (writes are discarded silently, reads
                              return arbitrary results).

1. In the event that the PCI_CAPSUP.CSR_CONF_EN bit is cleared, accesses to the IOADDR register via the configuration address
   space is ignored and has no effect on the register and the CSRs referenced by the IOADDR register.

#### 9.2.6.2 IODATA Register (0x9C; R/W)

This is a read/write register. Each function has its own IODATA register. Functionality is the same in all
functions. Register is cleared at power-up (LAN_PWR_GOOD) or PCIe reset.

 Bit(s)     Init.     Type                                                 Description

  31:0       0x0      R/W1    Data field for reads or writes to the Internal register or internal memory location as identified by the
                              current value in IOADDR. All 32 bits of this register can be read from or written to.

1. In the event that the IO_by_cfg bit in the PCIe Init Configuration 2 EEPROM word is cleared, access to the IODATA register via the
   configuration address space is ignored and has no effect on the register and the CSRs referenced by the IOADDR register.

852                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface
