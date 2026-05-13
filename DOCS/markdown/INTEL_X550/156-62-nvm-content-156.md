## 6.2 NVM Content

### 6.2.1 NVM General Summary Table

Table 6-7.       NVM General Summary Table
                                                                                                            Section
                                                      NVM Section
                                                                                                            Number

Init Module Section                                                                                           6.2.2

MAC Module Section                                                                                            6.2.3

CSR Auto Config Section                                                                                       6.2.4

LAN Core Module Section                                                                                       6.2.5

PCIe General Configuration Module Section                                                                     6.2.6

PCIe Configuration Space Section                                                                              6.2.7

Alternate Ethernet MAC Address                                                                                6.2.8

FCoE Scratch Pad Header Section                                                                               6.2.9

Active SAN MAC Address Section                                                                                6.2.10

Alternate SAN MAC Address Section                                                                             6.2.11

Boot Configuration Block Section                                                                              6.2.12

Firmware Module Header Section                                                                                6.2.13

Firmware Header Reserved Word Section                                                                         6.2.14

Test Configuration Module Section                                                                             6.2.15

Common Firmware Parameters Module Section                                                                     6.2.16

Sideband Configuration Structure Section                                                                      6.2.17

Pass-Through Control Words Section                                                                            6.2.18

Flexible TCO Filter Configuration Structure Section                                                           6.2.19

LESM Configurations (not in SGVL) Section                                                                     6.2.20

PXE VLAN Configuration Section                                                                                6.2.21

VPD Module Section                                                                                            6.2.22

PBA Number Module Section                                                                                     6.2.23

Mini Loader Module Section                                                                                    6.2.24

PHY Config Section                                                                                            6.2.25

PCIe Link (LCB) Configuration Section                                                                         6.2.26

PCIe Analog Configuration Module Section                                                                      6.2.27

2'nd Init Module Section                                                                                      6.2.28

FCoE Scratch Pad Section                                                                                      6.2.29

Firmware Module Section                                                                                       6.2.30

PXE/OROM Module Section                                                                                       6.2.31

AQ PHY Module Section                                                                                         6.2.32

Free Provisioning Module Section                                                                              6.2.33

226                                                                                                         333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.2 Init Module Section

Table 6-8.      Init Module Section Summary Table
                                                                                 Section
 Word Address    Used By                                       Word Name
                                                                                 Number

0x0000             HW      NVM Control Word 1                                    6.2.2.1

0x0001             HW      NVM Control Word 2                                    6.2.2.2

0x0002             HW      PCIe Analog Configuration Module Pointer              6.2.2.3

0x0003             HW      PCIe Link (LCB) Configuration Pointer                 6.2.2.4

0x0004             HW      PHY Module Pointer                                    6.2.2.5

0x0005             HW      PCIe Expansion/Option ROM Pointer                     6.2.2.6

0x0006             HW      PCIe General Configuration Module Pointer             6.2.2.7

0x0007             HW      PCIe Configuration Space 0 Module Pointer             6.2.2.8

0x0008             HW      PCIe Configuration Space 1 Module Pointer             6.2.2.9

0x0009             HW      LAN Core 0 Module Pointer                             6.2.2.10

0x000A             HW      LAN Core 1 Module Pointer                             6.2.2.11

0x000B             HW      MAC 0 Module Pointer                                  6.2.2.12

0x000C             HW      MAC 1 Module Pointer                                  6.2.2.13

0x000D             HW      CSR 0 Auto Configuration Module Pointer               6.2.2.14

0x000E             HW      CSR 1 Auto Configuration Module Pointer               6.2.2.15

0x000F              FW     Firmware Module Pointer                               6.2.2.16

0x0010              SW     SW Compatibility Word 1                               6.2.2.17

0x0011              SW     SW Compatibility Word 2                               6.2.2.18

0x0012             SW      SW Compatibility Word 3                               6.2.2.19

0x0013             SW      SW Compatibility Word 4                               6.2.2.20

0x0014             SW      SW Compatibility Word 5                               6.2.2.21

0x0015             SW      PBA Word 1                                            6.2.2.22

0x0016             SW      PBA Word 2                                            6.2.2.23

0x0017             SW      Boot Configuration Start Address                      6.2.2.24

0x0018             SW      Software Reserved Word 1 - Dev Starter Version        6.2.2.25

0x0019             SW      Software Reserved Word 2 - PHY Image Revision         6.2.2.26

0x001A             SW      Software Reserved Word 3                              6.2.2.27

0x001B             SW      Software Reserved Word 4                              6.2.2.28

0x001C             SW      Software Reserved Word 5                              6.2.2.29

0x001D             SW      Software Reserved Word 6                              6.2.2.30

0x001E             SW      Software Reserved Word 7                              6.2.2.31

0x001F             SW      Software Reserved Word 8                              6.2.2.32

0x0020             SW      Software Reserved Word 9 - PXE VLAN Config Pointer    6.2.2.33

0x0021             SW      Software Reserved Word 10                             6.2.2.34

0x0022             SW      Software Reserved Word 11                             6.2.2.35

333369-009                                                                              227
                                 Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

Table 6-8.      Init Module Section Summary Table [continued]
                                                                                                             Section
 Word Address    Used By                                      Word Name
                                                                                                             Number

0x0023             SW      Software Reserved Word 12                                                          6.2.2.36

0x0024             SW      Software Reserved Word 13                                                          6.2.2.37

0x0025             SW      Software Reserved Word 14 - Original EETrack ID 1                                  6.2.2.38

0x0026             SW      Software Reserved Word 15 - Original EETrack ID 2                                  6.2.2.39

0x0027             SW      Software Reserved Word 16 - Alternate SAN MAC Address Pointer                      6.2.2.40

0x0028             SW      Software Reserved Word 17 - Active SAN MAC Address Pointer                         6.2.2.41

0x0029             SW      Software Reserved Word 18 - MAP Version                                            6.2.2.42

0x002A             SW      Software Reserved Word 19 - IMAGE Version                                          6.2.2.43

0x002B             SW      Software Reserved Word 20                                                          6.2.2.44

0x002C             SW      Software Reserved Word 21 - FCoE Offload                                           6.2.2.45

0x002D             SW      Software Reserved Word 22 - EETRACK ID 1                                           6.2.2.46

0x002E             SW      Software Reserved Word 23 - EETRACK ID 2                                           6.2.2.47

0x002F             SW      VPD Module Pointer                                                                 6.2.2.48

0x0030             SW      PXE Setup Options PCI Function 0                                                   6.2.2.49

0x0031             SW      PXE Configuration Customization Options PCI Function 0                             6.2.2.50

0x0032             SW      PXE Version                                                                        6.2.2.51

0x0033             SW      Flash Capabilities                                                                 6.2.2.52

0x0034             SW      PXE Setup Options PCI Function 1                                                   6.2.2.53

0x0035             SW      PXE Configuration Customization Options PCI Function 1                             6.2.2.54

0x0036             SW      iSCSI Option ROM Version                                                           6.2.2.55

0x0037             SW      Alternate Ethernet MAC Addresses Pointer                                           6.2.2.56

0x0038             SW      NVM Control Word 3                                                                 6.2.2.57

0x0039             HW      FCoE Scratch Pad Pointer                                                           6.2.2.58

0x003A             FW      Firmware Code Pointer                                                              6.2.2.59

0x003B             HW      Hardware                                                                           6.2.2.60

0x003C             HW      Hardware                                                                           6.2.2.61

0x003D             HW      Hardware                                                                           6.2.2.62

0x003E             HW      Hardware                                                                           6.2.2.63

0x003F             SW      Software Checksum, Words 0x00 - 0x3F                                               6.2.2.64

0x0040             HW      Free Provisioning Area Pointer                                                     6.2.2.65

0x0041             HW      Free Provisioning Area Size                                                        6.2.2.66

0x0042             HW      Mini Loader Pointer                                                                6.2.2.67

0x0043             HW      PHY Config Pointer                                                                 6.2.2.68

0x0044             HW      Reserved                                                                           6.2.2.69

0x0045            N/A      Reserved                                                                           6.2.2.70

0x0046             HW      Reserved                                                                           6.2.2.71

0x0047             HW      Reserved                                                                           6.2.2.72

228                                                                                                          333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-8.       Init Module Section Summary Table [continued]
                                                                                                                         Section
 Word Address        Used By                                      Word Name
                                                                                                                         Number

0x0048                 HW      Reserved                                                                                  6.2.2.73

0x0049                 HW      Reserved                                                                                  6.2.2.74

0x004A                 HW      Reserved                                                                                  6.2.2.75

0x004B                 HW      Reserved                                                                                  6.2.2.76

0x004C                 HW      Reserved                                                                                  6.2.2.77

0x004D                 HW      Reserved                                                                                  6.2.2.78

0x004E                 HW      Reserved                                                                                  6.2.2.79

0x004F                 HW      Reserved                                                                                  6.2.2.80

0x0050                 HW      RO Updates Version                                                                        6.2.2.81

#### 6.2.2.1 NVM Control Word 1 (0x0000)

 Bit(s)      Field Name         Default                                         Description

# 15 Reserved                 0b     Reserved.

    14 NC-SI Ext HW ARB         0b     NC-SI Hardware Arbitration Enable

          Enable                           0b = NCSI_ARB_IN and NCSI_ARB_OUT pads are not used. NCSI_ARB_IN is pulled
                                                up internally to provide stable input.
                                           1b = NCSI_ARB_IN and NCSI_ARB_OUT pads are used.

# 13 Reserved                 0b     Reserved.

    12 NVM Host Debug           1b     NVM Host Debug Mode

          Mode                             0b = Normal operating mode (default).
                                           1b = Firmware reset has an effect on software write access to NVM via EEPROM-mode
                                                although it should not have any effect on it.

# 11 Reserved                 0b     Reserved.

  10:8    NVM Size                0x5     NVM Size
                                          These bits indicate the Flash’s actual size. Mapped to FLA.FL_SISE (see field definition
                                          in the FLA register section).
                                            0x4 = 1 MB
                                            0x5 = 2 MB
                                            0x6 = 4 MB
                                            All other values are reserved.
  7:6     Signature               01b     Signature
                                          The Signature field indicates that there is a valid NVM present. If the Signature field is
                                          not 01b, the other bits in this word are ignored, no further NVM read is performed, and
                                          the default values are used for the configuration space IDs.
                                          00b = NVM not present 0.
                                          01b = NVM present.
                                          10b = NVM not present 2.
                                          11b = NVM not present 3.
  5:0     Reserved                0x0     Reserved.

333369-009                                                                                                                       229
                                     Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                        Non-Volatile Memory Map

#### 6.2.2.2 NVM Control Word 2 (0x0001)

 Bit(s)       Field Name         Default                                            Description

    15 PCI LAN Function Sel        0b       PCI LAN Function Sel -- Swap

          -- Swap                              When both LAN ports are enabled and the LAN Function Sel equals 0b, LAN 0 is routed
                                               to PCI function 0 and LAN 1 is routed to PCI function 1. If the LAN Function Sel equals
                                               1b, LAN 0 is routed to PCI function 1 and LAN 1 is routed to PCI function 0.
                                               This bit is loaded from NVM.
                                               Note: This field is preserved by Intel NVM update tool.

# 14 Keep PHY CB                 0b       Keep PHY CB

                                               If set, the Keep_phy_in_dx aux bit affects the PHY state only while in D3/DR (legacy
                                               behavior). Otherwise, it affects the PHY state in D0 also.
 13:12    Reserved                00b          Reserved.

    11 PCI Function Off via        0b       PCIe Function Off via SDP Pins Enable.

          SDPins Enable                         0b = Legacy mode (default), SDPn_1 pins does not control PCIe functions off.
                                                1b = SDPn_1 pins are strapped (sampled by PE_RST_N) to disable the corresponding
                                                     PCIe function.
                                               Note: If manageability is present, MC-to-LAN paths are not disabled.
                                               Readable as DEV_FUNC_EN[3]
                                               Note: This field is preserved by Intel NVM update tool.

# 10 Reserved                    0b       Reserved.

    9 LAN PCI Disable             0b       LAN PCI Disable Select

          Select                               Selects which port is disabled.
                                               Note: This field is preserved by Intel NVM update tool.

    8 LAN PCI Disable             0b       LAN PCI Disable

                                               When set one PCI LAN port is disabled.
                                               Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                0x0          Reserved.

# 3 Deadlock Timeout            1b       Deadlock Timeout Enable

          Enable                               If set, a device that was granted access to the NVM that does not toggle the interface
                                               for 2 seconds will have the grant revoked.
                                                 0b = Timeout disabled.
                                                 1b = Timeout enabled.
                                               Note: This field is preserved by Intel NVM update tool.

# 2 Reserved                    1b       Reserved.

# 1 Core Clocks Gate            0b       Core Clocks Gate Disable

          Disable                              During nominal operation, this bit should be zero enabling core clock gating in low
                                               power state.
                                               When set, disables the gating of the core clock in low power state.
                                                0b = Enable Enables gating of the core clock in low power state.
                                                1b = Disable Disables gating of the core clock in low power state
                                               Note: This field is preserved by Intel NVM update tool.

# 0 Reserved                    0b       Reserved.

#### 6.2.2.3 PCIe Analog Configuration Module Pointer (0x0002)

The address is in words.

 Bit(s)          Field Name                Default                                     Description

  15:0    PCIe Analog Configuration        0xFFFF    PCIe Analog Configuration Module Pointer
          Module Pointer                             Points to PCIe Analog Configuration Module Section. For PCIe Analog
                                                     Configuration Module inner structure, see Section 6.2.27.

230                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.4 PCIe Link (LCB) Configuration Pointer (0x0003)

The address is in words.

 Bit(s)          Field Name              Default                                       Description

  15:0    PCIe Link (LCB)                  0x0       PCIe Link (LCB) Configuration Pointer
          Configuration Pointer                      Points to PCIe Link (LCB) Configuration Section. For PCIe Link (LCB) Configuration
                                                     inner structure, see Section 6.2.26.

#### 6.2.2.5 PHY Module Pointer (0x0004)

The address is in 4 KB sector index units.

 Bit(s)       Field Name          Default                                           Description

# 15 Pointer Type              1b       Pointer Type

                                              0b = Word units.
                                              1b = 4 KB sector units.
  14:0    PHY Module Pointer       0x0       PHY Module Pointer
                                             Points to AQ PHY Module Section. For AQ PHY Module inner structure, see
                                             Section 6.2.32.

#### 6.2.2.6 PCIe Expansion/Option ROM Pointer (0x0005)

The address is in 4 KB sector index units.

 Bit(s)       Field Name          Default                                           Description

# 15 Pointer Type              1b       Pointer Type

                                              0b = Word units.
                                              1b = 4 KB sector units.
  14:0    PCIe Expansion/         0x7FFF     PCIe Expansion/Option ROM Pointer
          Option ROM Pointer                 Points to PXE/OROM Module Section. For PXE/OROM Module inner structure, see
                                             Section 6.2.31.

#### 6.2.2.7 PCIe General Configuration Module Pointer (0x0006)

The address is in words.

 Bit(s)           Field Name                Default                                      Description

  15:0    PCIe General Configuration        0xFFFF     PCIe General Configuration Pointer
          Pointer                                      Points to PCIe General Configuration Module Section. For PCIe General
                                                       Configuration Module inner structure, see Section 6.2.6.

#### 6.2.2.8 PCIe Configuration Space 0 Module Pointer (0x0007)

The address is in words.

 Bit(s)           Field Name                Default                                      Description

  15:0    PCIe Configuration Space 0        0xFFFF     PCIe Configuration Space 0 Module Pointer
          Module Pointer                               Points to PCIe Configuration Space Section. For PCIe Configuration Space inner
                                                       structure, see Section 6.2.7.

333369-009                                                                                                                          231
                                       Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

#### 6.2.2.9 PCIe Configuration Space 1 Module Pointer (0x0008)

The address is in words.

 Bit(s)           Field Name             Default                                    Description

  15:0    PCIe Configuration Space 1      0xFFFF    PCIe Configuration Space 1 Module Pointer
          Module Pointer                            Points to PCIe Configuration Space Section. For PCIe Configuration Space inner
                                                    structure, see Section 6.2.7.

#### 6.2.2.10 LAN Core 0 Module Pointer (0x0009)

The address is in words.

 Bit(s)          Field Name             Default                                     Description

  15:0    LAN Core 0 Section Pointer     0xFFFF    LAN Core 0 Section Pointer
                                                   Points to LAN Core Module Section. For LAN Core Module inner structure, see
                                                   Section 6.2.5.

#### 6.2.2.11 LAN Core 1 Module Pointer (0x000A)

The address is in words.

 Bit(s)          Field Name             Default                                     Description

  15:0    LAN Core 1 Section Pointer     0xFFFF    LAN Core 1 Section Pointer
                                                   Points to LAN Core Module Section. For LAN Core Module inner structure, see
                                                   Section 6.2.5.

#### 6.2.2.12 MAC 0 Module Pointer (0x000B)

The address is in words.

 Bit(s)        Field Name          Default                                        Description

  15:0    MAC 0 Section Pointer    0xFFFF    MAC 0 Section Pointer
                                             Points to MAC Module Section. For MAC Module inner structure, see Section 6.2.3.

#### 6.2.2.13 MAC 1 Module Pointer (0x000C)

The address is in words.

 Bit(s)        Field Name          Default                                        Description

  15:0    MAC 1 Section Pointer    0xFFFF    MAC 1 Section Pointer
                                             Points to MAC Module Section. For MAC Module inner structure, see Section 6.2.3.

232                                                                                                                    333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.14 CSR 0 Auto Configuration Module Pointer (0x000D)

The address is in words.

 Bit(s)            Field Name         Default                                     Description

  15:0    CSR 0 Auto Configuration     0xFFFF    CSR 0 Auto Configuration Pointer
          Pointer                                Points to CSR Auto Config Section. For CSR Auto Config inner structure, see
                                                 Section 6.2.4.

#### 6.2.2.15 CSR 1 Auto Configuration Module Pointer (0x000E)

The address is in words.

 Bit(s)            Field Name         Default                                     Description

  15:0    CSR 1 Auto Configuration     0xFFFF    CSR 1 Auto Configuration Pointer
          Pointer                                Points to CSR Auto Config Section. For CSR Auto Config inner structure, see
                                                 Section 6.2.4.

#### 6.2.2.16 Firmware Module Pointer (0x000F)

The address is in words.

 Bit(s)            Field Name         Default                                     Description

  15:0    Firmware Section Pointer      0x0      Firmware Section Pointer
                                                 Points to Firmware Module Header Section. For Firmware Module Header inner
                                                 structure, see Section 6.2.13.

#### 6.2.2.17 SW Compatibility Word 1 (0x0010)

Five words in the NVM image are reserved for compatibility information. New bits within these fields are
defined as the need arises for determining software compatibility between various hardware revisions.

 Bit(s)      Field Name    Default                                           Description

 15:12    Reserved              0x0   Reserved.
                                      Note: This field is preserved by Intel NVM update tool.

    11 LOM                   0b    LOM

                                      Indicates whether the NVM attached to LAN silicon contains dedicated module for option
                                      ROM. Used by option ROM update applications.
                                       0b = NIC (Attached flash contains module for option ROM).
                                       1b = LOM (Attached flash has no module for option ROM).
                                      Note: This field is preserved by Intel NVM update tool.

# 10 Server                1b    Server

                                      Legacy, not currently used.
                                       0b = Client
                                       1b = Server
                                      Note: This field is preserved by Intel NVM update tool.

# 9 Reserved              0b    Reserved.

                                      Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                     233
                                      Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

 Bit(s)    Field Name    Default                                         Description

    8 OEM/Retail       0b      OEM/Retail

                                   Legacy, not currently used.
                                    0b = Retail
                                    1b = OEM
                                   Note: This field is preserved by Intel NVM update tool.
  7:0     Reserved        0x0      Reserved.
                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.18 SW Compatibility Word 2 (0x0011)

Five words in the NVM image are reserved for compatibility information. New bits within these fields are
defined as the need arises for determining software compatibility between various hardware revisions.

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved       0xFFFF    Reserved.

#### 6.2.2.19 SW Compatibility Word 3 (0x0012)

Five words in the NVM image are reserved for compatibility information. New bits within these fields are
defined as the need arises for determining software compatibility between various hardware revisions.

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved       0xFFFF    Reserved.

#### 6.2.2.20 SW Compatibility Word 4 (0x0013)

Five words in the NVM image are reserved for compatibility information. New bits within these fields are
defined as the need arises for determining software compatibility between various hardware revisions.

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved       0xFFFF    Reserved.

#### 6.2.2.21 SW Compatibility Word 5 (0x0014)

Five words in the NVM image are reserved for compatibility information. New bits within these fields are
defined as the need arises for determining software compatibility between various hardware revisions.

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved       0xFFFF    Reserved.

234                                                                                                          333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.22 PBA Word 1 (0x0015)

The nine-digit Printed Board Assembly (PBA) number used for Intel manufactured Network Interface
Cards (NICs) is stored in the NVM.
Note:        Through the course of hardware ECOs, the suffix field is incremented. The purpose of this
             information is to enable customer support (or any user) to identify the revision level of a
             product.
Network driver software should not rely on this field to identify the product or its capabilities.
Current PBA numbers have exceeded the length that can be stored as hex values in these two words.
For these PBA numbers the high word is a flag (0xFAFA) indicating that the PBA is stored in a separate
PBA block. The low word is a pointer to a PBA block.

 Bit(s)    Field Name      Default                                          Description

  15:0    PBA Word 1          0x0    PBA Word 1
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.23 PBA Word 2 (0x0016)

The nine-digit Printed Board Assembly (PBA) number used for Intel manufactured Network Interface
Cards (NICs) is stored in the NVM.
Note:        Through the course of hardware ECOs, the suffix field is incremented. The purpose of this
             information is to enable customer support (or any user) to identify the revision level of a
             product.
Network driver software should not rely on this field to identify the product or its capabilities.
Current PBA numbers have exceeded the length that can be stored as hex values in these two words.
For these PBA numbers the high word is a flag (0xFAFA) indicating that the PBA is stored in a separate
PBA block. The low word is a pointer to a PBA block.

 Bit(s)    Field Name      Default                                          Description

  15:0    PBA Word 2          0x0    PBA Word 2
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.24 Boot Configuration Start Address (0x0017)

Address of iSCSI Boot configuration module. This is a word pointer. The block length is embedded in the
module.

 Bit(s)          Field Name          Default                                      Description

  15:0    iSCSI Boot Configuration     0x0      iSCSI Boot Configuration Start Address
          Start Address                         This module is long by 1504B and must be mapped in the first valid 4 KB sector of
                                                the Flash.
                                                Points to Boot Configuration Block Section. For Boot Configuration Block inner
                                                structure, see Section 6.2.12.

333369-009                                                                                                                    235
                                     Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.2.25 Software Reserved Word 1 - Dev Starter Version

                          (0x0018)
Copy of first contents of MAP Version, not auto generated, to trace source of any image.

 Bit(s)    Field Name      Default                                          Description

 15:12    Major Version     0x1      Major Version
                                     NVM minor version.
  11:8    Reserved          0x0      Reserved. NVM major version.
  7:0     Minor Version     0x92     Minor Version
                                     Human-readable, hex using only the decimal digits to make the digital version.

#### 6.2.2.26 Software Reserved Word 2 - PHY Image Revision

                          (0x0019)

 Bit(s)    Field Name      Default                                          Description

 15:12    Major             0x2      Major
                                     PHY major version.
  11:4    Minor             0x0B     Minor
                                     PHY minor version.
  3:0     ID                0xB      ID
                                     PHY Image ID.

#### 6.2.2.27 Software Reserved Word 3 (0x001A)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.28 Software Reserved Word 4 (0x001B)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.29 Software Reserved Word 5 (0x001C)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.30 Software Reserved Word 6 (0x001D)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

236                                                                                                                   333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.31 Software Reserved Word 7 (0x001E)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.32 Software Reserved Word 8 (0x001F)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.33 Software Reserved Word 9 - PXE VLAN Config Pointer

                          (0x0020)

 Bit(s)          Field Name          Default                                      Description

  15:0    PXE VLAN Config Pointer     0xFFFF     Reserved.
                                                 Points to PXE VLAN Configuration Section. For PXE VLAN Configuration inner
                                                 structure, Section 6.2.21.

#### 6.2.2.34 Software Reserved Word 10 (0x0021)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.35 Software Reserved Word 11 (0x002)

 Bit(s)      Field Name    Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.36 Software Reserved Word 12 (0x0023)

 Bit(s)      Field Name    Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

#### 6.2.2.37 Software Reserved Word 13 (0x0024)

 Bit(s)      Field Name    Default                                          Description

  15:0    Reserved         0xFFFF    Reserved.

333369-009                                                                                                                    237
                                     Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                          Non-Volatile Memory Map

#### 6.2.2.38 Software Reserved Word 14 - Original EETrack ID

                        (0x0025)

 Bit(s)        Field Name             Default                                        Description

  15:0    Original EETrack ID 1       0xFFFF       Reserved.

#### 6.2.2.39 Software Reserved Word 15 - Original EETrack ID

                        (0x0026)

 Bit(s)        Field Name             Default                                        Description

  15:0    Original EETrack ID 2       0xFFFF       Reserved.

#### 6.2.2.40 Software Reserved Word 16 - Alternate SAN MAC

                        Address Pointer (0x0027)
Word 0x27 points to the Alternate SAN MAC Address block used for FCoE (SPMA and FPMA) and DCB.

 Bit(s)       Field Name           Default                                          Description

  15:0    Alternate SAN MAC         0xFFFF      Alternate SAN MAC Address Pointer
          Address Pointer                       Pointer to the Permanent SAN MAC Address block. 0xFFFF indicates an invalid pointer.
                                                Points to Alternate SAN MAC Address Section. For Alternate SAN MAC Address inner
                                                structure, see Section 6.2.11.

#### 6.2.2.41 Software Reserved Word 17 - Active SAN MAC Address

                        Pointer (0x0028)
Word 0x28 points to the Permanent SAN MAC Address block used for FCoE (SPMA and FPMA) and DCB.

 Bit(s)       Field Name           Default                                          Description

  15:0    SAN MAC Address           0xFFFF      SAN MAC Address Pointer
          Pointer                               Pointer to the Permanent SAN MAC Address block. 0xFFFF indicates an invalid pointer.
                                                Points to Active SAN MAC Address Section. For Active SAN MAC Address inner
                                                structure, see Section 6.2.10.

#### 6.2.2.42 Software Reserved Word 18 - MAP Version (0x0029)

 Bit(s)    Field Name      Default                                               Description

  15:0    MAP_Version       0xFFFF         MAP Version
                                           Auto-generated from same input as filename.

#### 6.2.2.43 Software Reserved Word 19 - IMAGE Version (0x002A)

 Bit(s)     Field Name        Default                                              Description

  15:0    IMAGE _Version          0xFFFF     IMAGE Version
                                             Auto-generated from same input as filename

238                                                                                                                       333369-009
                                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.44 Software Reserved Word 20 (0x002B)

 Bit(s)    Field Name        Default                                            Description

  15:0    Reserved           0xFFFF    Reserved.

#### 6.2.2.45 Software Reserved Word 21 - FCoE Offload (0x002C)

This word is for platform/NIC/LOM specific settings.

 Bit(s)         Field Name             Default                                        Description

  15:7    Reserved                      0x1FF      Reserved.
                                                   Note: This field is preserved by Intel NVM update tool.

    6 UEFI Port Number Display        1b       UEFI Port Number Display

                                                    0b = Enabled
                                                    1b = Disabled
                                                   Note: This field is preserved by Intel NVM update tool.

    5 HP OCD Support                  1b       HP OCD Support

                                                    0b = Enabled
                                                    1b = Disabled
                                                   Note: This field is preserved by Intel NVM update tool.

# 4 Lenovo Agentless VPD            1b       Lenovo Agentless VPD

                                                    0b = Enabled
                                                    1b = Disabled
                                                   Note: This field is preserved by Intel NVM update tool.
  3:2     Wake On LAN Support            11b       Wake On LAN Support
                                                   This bit indicates to software if the device supports Wake on LAN.
                                                    00b = Reserved (not supported).
                                                    01b = WoL supported on both ports.
                                                    10b = WoL supported on port A only.
                                                    11b = WoL not supported on either port.
                                                   Note: This field is preserved by Intel NVM update tool.

# 1 FCoE Offload                    0b       FCoE Offload

                                                   This bit indicates to software if the device supports FCoE Offload.
                                                    0b = FCoE Offload enabled.
                                                    1b = FCoE Offload disabled.
                                                   Note: This field is preserved by Intel NVM update tool.

# 0 Reserved                        1b       Reserved.

                                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.46 Software Reserved Word 22 - EETRACK ID 1 (0x002D)

This word is for the first word of the eTrack_ID number written by EEPROM Manager Tool.

 Bit(s)       Field Name           Default                                          Description

  15:0    eTrack_ID Word 1       0xFFFFFFFF     eTrack_ID Word 1
                                                EEPROM Manager Tool writes a unique 32-bit eTrack_ID number in two sequential
                                                NVM words (0x002D-0x002E). The eTrack_ID is written when EEPROM Manager Tool
                                                creates an image on the Intel network. The eTrack_ID DB tracks NVM images back
                                                to a specific SCM build.

333369-009                                                                                                                 239
                                       Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                        Non-Volatile Memory Map

#### 6.2.2.47 Software Reserved Word 23 - EETRACK ID 2 (0x002E)

This word is for the second word of the eTrack_ID number written by EEPROM Manager Tool.

 Bit(s)         Field Name          Default                                         Description

  15:0    eTrack_ID Word 2                    eTrack_ID Word 2

#### 6.2.2.48 VPD Module Pointer (0x002F)

Word pointer to Vital Product Data module. Block length is embedded in the module.

 Bit(s)    Field Name        Default                                             Description

  15:0    VPD Pointer        0xFFFF     VPD Pointer
                                        Vital Product Data Pointer. 0xFFFF Default unless VPD relative section is specified. The VPD
                                        section size is usually 64 words and is initialized to 0 or 0xFFFF. During run time this module
                                        is accessible through the VPD capability in the PCI configuration space. This module must be
                                        mapped in the first valid 4KB sector of the Flash.
                                        Points to VPD Module Section. For VPD Module inner structure, see Section 6.2.22.

#### 6.2.2.49 PXE Setup Options PCI Function 0 (0x0030)

The main setup options for Port 0 are stored in this word. These options are those that can be changed
by the user using the Control-S setup menu.

 Bit(s)    Field Name        Default                                             Description

 15:13    Reserved            000b      Reserved. Must be 000b.
                                        Note: This field is preserved by Intel NVM update tool.
 12:10    FSD                 000b      Force Speed and Duplex
                                        Bits 12-10 control forcing speed and duplex during driver operation.
                                         000b = Auto-negotiate
                                         001b = 10 Mb/s half duplex
                                         010b = 100 Mb/s half duplex
                                         011b = Not valid (treated as 000b)
                                         100b = Not valid (treated as 000b)
                                         101b = 10 Mb/s full duplex
                                         110b = 100 Mb/s full duplex
                                         111b = 1000 Mb/s full duplex
                                        Only applicable for copper-based adapters. Not applicable to 10 GbE. Default value is 000b.
                                        Note: This field is preserved by Intel NVM update tool.

    9 LWS                  0b       Legacy OS Wakeup Support

                                        For 82559-based adapters only.
                                        If set to 1b, the agent enables PME in the adapter’s PCI configuration space during
                                        initialization. This allows remote wake up under legacy operating systems that do not
                                        normally support it.
                                        Note that enabling this makes the adapter technically non-compliant with the ACPI
                                        specification, which is why the default is disabled. Must be set to 0b for 1 GbE and 10 GbE
                                        adapters.
                                          0b = Disabled (default)
                                          1b = Enabled
                                        Note: This field is preserved by Intel NVM update tool.

    8 DSM                  1b       Display Setup Message

                                        If set to 1b, the “Press Control-S” message is displayed after the title message. Default value
                                        is 1b.
                                        Note: This field is preserved by Intel NVM update tool.

240                                                                                                                        333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)    Field Name        Default                                             Description

  7:6     PT                  00b       Prompt Time
                                        These bits control how long the “Press Control-S” setup prompt message is displayed, if
                                        enabled by DIM.
                                         00b = 2 seconds (default)
                                         01b = 3 seconds
                                         10b = 5 seconds
                                         11b = 0 seconds.
                                        Note: The Ctrl-S message is not displayed if 0 seconds prompt time is selected.
                                        Note: This field is preserved by Intel NVM update tool.
   5      iSCSI Disable        0b       iSCSI Disable
                                          0b = Enabled
                                          1b = Disabled
                                        Note: This field is preserved by Intel NVM update tool.
  4:3     DBS                 00b       Default Boot Selection
                                        These bits select which device is the default boot device. These bits are only used if the agent
                                        detects that the BIOS does not support boot order selection or if the MODE field of word 31h
                                        is set to MODE_LEGACY.
                                          00b = Network boot, then local boot (default)
                                          01b = Local boot, then network boot
                                          10b = Network boot only
                                          11b = Local boot only
                                        Note: This field is preserved by Intel NVM update tool.
  2:0     PS                  000b      Protocol Select
                                        These bits select the active boot protocol.
                                         00b = PXE (default value)
                                         01b = RPL (only if RPL is in the Flash)
                                         10b = iSCSI Boot primary port (only if iSCSI Boot is using this adapter)
                                         11b = iSCSI Boot secondary port (only if iSCSI Boot is using this adapter).
                                        Only the default value of 00b should be initially programmed into the adapter. Other values
                                        should only be set by configuration utilities.
                                        Valid values are:
                                         000b = PXE (default value).
                                         001b = Boot Disabled
                                         010b = iSCSI Primary
                                         011b = iSCSI Secondary
                                         100b = FCoE
                                         All other values are reserved.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.50 PXE Configuration Customization Options PCI Function

# 0 (0x0031)

Word 0x31 of the NVM contains settings that can be programmed by an OEM or network administrator
to customize the operation of the software. These settings cannot be changed from within the Control-
S setup menu. The lower byte contains settings that would typically be configured by a network
administrator using an external utility; these settings generally control which setup menu options are
changeable. The upper byte is generally settings that would be used by an OEM to control the operation
of the agent in a LOM environment, although there is nothing in the agent to prevent their use on a NIC
implementation. The default value for this word is 0x4000.

 Bit(s)         Field Name          Default                                         Description

 15:14    Signature                  01b      Signature
                                              Must be set to 01b to indicate that this word has been programmed by the agent or
                                              other configuration software.
                                              Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                           241
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                          Description

 13:12    Reserved                00b      Reserved. Must be 0.
                                           Note: This field is preserved by Intel NVM update tool.

# 11 Continuous Retry         0b      Continuous Retry

                                           Selects Continuous Retry operation. If this bit is set, IBA does NOT transfer control
                                           back to the BIOS if it fails to boot due to a network error (such as failure to receive
                                           DHCP replies). Instead, it restarts the PXE boot process again. If this bit is set, the only
                                           way to cancel PXE boot is for the user to press ESC on the keyboard. Retry is not
                                           attempted due to hardware conditions such as an invalid NVM checksum or failing to
                                           establish link. Default value is 0b.
                                            0b = Disable
                                            1b = Enable
                                           Note: This field is preserved by Intel NVM update tool.
  10:8    Operating Mode          000b     Operating Mode
                                           Selects the agent’s boot order setup mode. This field changes the agent’s default
                                           behavior to make it compatible with systems that do not completely support the BBS
                                           and PnP Expansion ROM standards.
                                           Valid values and their meanings are:
                                            000b = Normal Behavior — The agent attempts to detect BBS and PnP Expansion
                                                     ROM support as it normally does.
                                            001b = Force Legacy Mode — The agent does not attempt to detect BBS or PnP
                                                     Expansion ROM supports in the BIOS and assumes the BIOS is not compliant.
                                                     The user can change the BIOS boot order in the Setup Menu
                                            010b = Force BBS Mode — The agent assumes the BIOS is BBS-compliant, even
                                                     though it might not be detected as such by the agent’s detection code. The
                                                     user CANNOT change the BIOS boot order in the Setup Menu.
                                            011b = Force PnP Int18 Mode — The agent assumes the BIOS allows boot order setup
                                                     for PnP Expansion ROMs and hooks interrupt 0x18 (to inform the BIOS that
                                                     the agent is a bootable device) in addition to registering as a BBS IPL device.
                                                     The user CANNOT change the BIOS boot order in the Setup Menu.
                                            100b = Force PnP Int19 Mode — The agent assumes the BIOS allows boot order setup
                                                     for PnP Expansion ROMs and hook interrupt 0x19 (to inform the BIOS that the
                                                     agent is a bootable device) in addition to registering as a BBS IPL device. The
                                                     user CANNOT change the BIOS boot order in the Setup Menu
                                            101b = Reserved for future use. If specified, is treated as a value of 000b.
                                            110b = Reserved for future use. If specified, is treated as a value of 000b.
                                            111b = Reserved for future use. If specified, is treated as a value of 000b.
                                           Note: This field is preserved by Intel NVM update tool.
  7:6     Reserved                00b      Reserved. Must be 0.
                                           Note: This field is preserved by Intel NVM update tool.

# 5 Disable Flash Update     0b      Disable Flash Update

                                           If this bit is set to 1b, the user is not allowed to update the flash image using PROSet.
                                           Default value is 0b.
                                             0b = Enable Flash Update
                                             1b = Disable Flash Update
                                           Note: This field is preserved by Intel NVM update tool.

# 4 Disable Legacy OS        0b      Disable Legacy Wakeup Support

          Wakeup Menu                      If this bit is set to 1b, the user is not allowed to change the Legacy OS Wakeup Support
                                           menu option. Default value is 0b.
                                             0b = Enable Legacy Wakeup Support
                                             1b = Disable Legacy Wakeup Support
                                           Note: This field is preserved by Intel NVM update tool.

# 3 Disable Boot             0b      Disable Boot Selection

          Selection Menu                   If this bit is set to 1b, the user is not allowed to change the boot order menu option.
                                           Default value is 0b.
                                             0b = Enable
                                             1b = Disable
                                           Note: This field is preserved by Intel NVM update tool.

242                                                                                                                        333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name          Default                                            Description

# 2 Disable Protocol              0b     Disable Protocol Select

          Selection Menu                       If set to 1b, the user is not allowed to change the boot protocol. Default value is 0b.
                                                 0b = Enable
                                                 1b = Disable
                                               Note: This field is preserved by Intel NVM update tool.

# 1 Disable Title                 0b     Disable Title Message

          Message Display                      If this bit is set to 1b, the title message displaying the version of the Boot Agent is
                                               suppressed; the Control-S message is also suppressed. This is for OEMs who do not
                                               wish the boot agent to display any messages at system boot. Default value is 0b.
                                                 0b = Enable
                                                 1b = Disable
                                               Note: This field is preserved by Intel NVM update tool.

# 0 Disable Setup Menu            0b     Disable Setup Menu

                                               If this bit is set to 1b, the user is not allowed to invoke the setup menu by pressing
                                               Control-S. In this case, the NVM may only be changed via an external program. Default
                                               value is 0b.
                                                 0b = Enable
                                                 1b = Disable
                                               Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.51 PXE Version (0x0032)

Word 0x32 of the NVM is used to store the version of the boot agent that is stored in the Flash image.
When the Boot Agent loads, it can check this value to determine if any first-time configuration needs to
be performed. The agent then updates this word with its version. Some diagnostic tools to report the
version of the Boot Agent in the Flash also read this word.

 Bit(s)    Field Name         Default                                             Description

 15:12    Major Version        0x2       Major Version
                                         PXE Boot Agent Major Version.
                                         Note: This field is preserved by Intel NVM update tool.
  11:8    Minor Version        0x3       Minor Version
                                         PXE Boot Agent Minor Version.
                                         Note: This field is preserved by Intel NVM update tool.
  7:0     Build Number         0x48      Build Number
                                         PXE Boot Agent Build Number.
                                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.52 Flash Capabilities (0x0033)

Word 0x33h of the NVM is used to enumerate the boot technologies that have been programmed into
the Flash. This is updated by Flash configuration tools and is not updated or read by IBA.

 Bit(s)      Field Name         Default                                             Description

 15:14    Signature               01b        Signature
                                             Must be set to 01b to indicate that this word has been programmed by the agent or other
                                             configuration software.
                                             Note: This field is preserved by Intel NVM update tool.

# 13 Allow PXE Disable       0b         Allow PXE Disable

                                              0b = Disabled
                                              1b = Enabled
                                             Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                               243
                                         Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

 Bit(s)     Field Name        Default                                          Description

  12:6    Reserved              0x0     Reserved. Must be 0.
                                        Note: This field is preserved by Intel NVM update tool.

    5 FCOE Boot             0b      FCoE Boot

                                        FCoE boot code is present if set to 1b.
                                         0b = Not Present
                                         1b = Present
                                        Note: This field is preserved by Intel NVM update tool.
      4   iSCSI Boot            0b      iSCSI Boot
                                        iSCSI is present if set to 1b.
                                          0b = Not Present
                                          1b = Present
                                        Note: This field is preserved by Intel NVM update tool.

    3 EFI/UNDI Driver       0b      EFI/UNDI Driver

                                        EFI UNDI driver is present if set to 1b.
                                         0b = Not Present
                                         1b = Present
                                        Note: This field is preserved by Intel NVM update tool.

    2 RPL                   0b      RPL

                                        RPL module is present if set to 1b. Reserved bit for devices.
                                         0b = Not Present
                                         1b = Present
                                        Note: This field is preserved by Intel NVM update tool.

    1 PXE/UNDI Driver       1b      PXE/UNDI Driver

                                        PXE UNDI driver is present if set to 1b.
                                         0b = Not Present
                                         1b = Present
                                        Note: This field is preserved by Intel NVM update tool.

    0 PXE Base Code         1b      PXE Base Code

                                        PXE Base Code is present if set to 1b.
                                         0b = Not Present
                                         1b = Present
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.2.53 PXE Setup Options PCI Function 1 (0x0034)

This word is the same as word 0x30, but for function 1 of the device.

 Bit(s)    Field Name       Default                                          Description

 15:13    Reserved           000b     Reserved. Must be 0x0.
                                      Note: This field is preserved by Intel NVM update tool.
 12:10    FSD                000b     Force Speed and Duplex
                                      Bits 12-10 control forcing speed and duplex during driver operation.
                                       000b = Auto-negotiate (0x0)
                                       001b = 10 Mb/s half duplex (0x1)
                                       010b = 100 Mb/s half duplex (0x2)
                                       011b = Not valid (0x3, treated as 0x0).
                                       100b = Not valid (0x4. treated as 0x0).
                                       101b = 10 Mb/s full duplex (0x5)
                                       110b = 100 Mb/s full duplex (0x6)
                                       111b = 1000 Mb/s full duplex (0x7)
                                      Only applicable for copper-based adapters. Not applicable to 10 GbE. Default value is 000b.
                                      Note: This field is preserved by Intel NVM update tool.

244                                                                                                                   333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)    Field Name     Default                                            Description

    9 LWS               0b      Legacy OS Wakeup Support

                                    For 82559-based adapters only.
                                    If set to 1b, the agent enables PME in the adapter’s PCI configuration space during
                                    initialization. This allows remote wake up under legacy operating systems that do not
                                    normally support it.
                                    Note that enabling this makes the adapter technically non-compliant with the ACPI
                                    specification, which is why the default is disabled. Must be set to 0b for 1 GbE and 10 GbE
                                    adapters.
                                      0b = Disabled (default)
                                      1b = Enabled
                                    Note: This field is preserved by Intel NVM update tool.

    8 DSM               1b      Display Setup Message

                                    If the bit is set to 1b, the “Press Control-S” message is displayed after the title message.
                                    Default value is 1b.
                                    Note: This field is preserved by Intel NVM update tool.
  7:6     PT               00b      Prompt Time
                                    These bits control how long the “Press Control-S” setup prompt message is displayed, if
                                    enabled by DIM.
                                    00b = 2 seconds (default)
                                    01b = 3 seconds
                                    10b = 5 seconds
                                    11b = 0 seconds
                                    Note: The Ctrl-S message is not displayed if 0 seconds prompt time is selected.
                                    Note: This field is preserved by Intel NVM update tool.
   5      iSCSI Disable     0b      iSCSI Disable
                                      0b = Enabled
                                      1b = Disabled
                                    Note: This field is preserved by Intel NVM update tool.
  4:3     DBS              00b      Default Boot Selection
                                    These bits select which device is the default boot device. These bits are only used if the agent
                                    detects that the BIOS does not support boot order selection or if the MODE field of word 31h
                                    is set to MODE_LEGACY.
                                      00b = Network boot, then local boot (default)
                                      01b = Local boot, then network boot
                                      10b = Network boot only
                                      11b = Local boot only
                                    Note: This field is preserved by Intel NVM update tool.
  2:0     PS               000b     Protocol Select
                                    These bits select the active boot protocol.
                                     00b = PXE (default value)
                                     01b = RPL (only if RPL is in the Flash)
                                     10b = iSCSI Boot primary port (only if iSCSI Boot is using this adapter)
                                     11b = iSCSI Boot secondary port (only if iSCSI Boot is using this adapter).
                                    Only the default value of 00b should be initially programmed into the adapter. Other values
                                    should only be set by configuration utilities.
                                     000b = PXE (default value).
                                     001b = Boot Disabled
                                     010b = iSCSI Primary
                                     011b = iSCSI Secondary
                                     100b = FCoE
                                     All other values are reserved.
                                    Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                         245
                                    Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                      Non-Volatile Memory Map

#### 6.2.2.54 PXE Configuration Customization Options PCI Function

# 1 (0x0035)

This word is the same as word 0x31, but for function 1 of the device.

 Bit(s)       Field Name         Default                                          Description

 15:14    Signature               01b      Signature
                                           Must be set to 01b to indicate that this word has been programmed by the agent or
                                           other configuration software.
                                           Note: This field is preserved by Intel NVM update tool.
 13:12    Reserved                00b      Reserved. Must be 0.
                                           Note: This field is preserved by Intel NVM update tool.

# 11 Continuous Retry         0b      Continuous Retry

                                           Selects Continuous Retry operation. If this bit is set, IBA will NOT transfer control back
                                           to the BIOS if it fails to boot due to a network error (such as failure to receive DHCP
                                           replies). Instead, it will restart the PXE boot process again. If this bit is set, the only
                                           way to cancel PXE boot is for the user to press ESC on the keyboard. Retry will not be
                                           attempted due to hardware conditions such as an invalid NVM checksum or failing to
                                           establish link. Default value is 0b.
                                            0b = Disable
                                            1b = Enable
                                           Note: This field is preserved by Intel NVM update tool.
  10:8    Operating Mode          000b     Operating Mode
                                           Selects the agent’s boot order setup mode. This field changes the agent’s default
                                           behavior in order to make it compatible with systems that do not completely support
                                           the BBS and PnP Expansion ROM standards.
                                           Valid values and their meanings are:
                                            000b = Normal behavior — The agent will attempt to detect BBS and PnP Expansion
                                                     ROM support as it normally does
                                            001b = Force Legacy Mode — The agent will not attempt to detect BBS or PnP
                                                     Expansion ROM supports in the BIOS and will assume the BIOS is not
                                                     compliant. The user can change the BIOS boot order in the Setup Menu.
                                            010b = Force BBS Mode — The agent will assume the BIOS is BBS-compliant, even
                                                     though it may not be detected as such by the agent’s detection code. The
                                                     user can NOT change the BIOS boot order in the Setup Menu.
                                            011b = Force PnP Int18 Mode — The agent will assume the BIOS allows boot order
                                                     setup for PnP Expansion ROMs and will hook interrupt 18h (to inform the
                                                     BIOS that the agent is a bootable device) in addition to registering as a BBS
                                                     IPL device. The user can NOT change the BIOS boot order in the Setup Menu.
                                            100b = Force PnP Int19 Mode — The agent will assume the BIOS allows boot order
                                                     setup for PnP Expansion ROMs and will hook interrupt 19h (to inform the
                                                     BIOS that the agent is a bootable device) in addition to registering as a BBS
                                                     IPL device. The user can NOT change the BIOS boot order in the Setup Menu.
                                            101b = Reserved for future use. If specified, is treated as a value of 000b.
                                            110b = Reserved for future use. If specified, is treated as a value of 000b.
                                            111b = Reserved for future use. If specified, is treated as a value of 000b.
                                           Note: This field is preserved by Intel NVM update tool.
  7:6     Reserved                00b      Reserved. Must be 0.
                                           Note: This field is preserved by Intel NVM update tool.

# 5 Disable Flash Update     0b      Disable Flash Update

                                           If this bit is set to 1b, the user is not allowed to update the flash image using PROSet.
                                           Default value is 0b.
                                             0b = Enable Flash Update
                                             1b = Disable Flash Update
                                           Note: This field is preserved by Intel NVM update tool.

246                                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                           Description

# 4 Disable Legacy OS            0b    Disable Legacy Wakeup Support

          Wakeup Menu                        If this bit is set to 1b, the user is not allowed to change the Legacy OS Wakeup Support
                                             menu option. Default value is 0b.
                                               0b = Enable Legacy Wakeup Support
                                               1b = Disable Legacy Wakeup Support
                                             Note: This field is preserved by Intel NVM update tool.

# 3 Disable Boot                 0b    Disable Boot Selection

          Selection Menu                     If this bit is set to 1b, the user is not allowed to change the boot order menu option.
                                             Default value is 0b.
                                               0b = Enable
                                               1b = Disable
                                             Note: This field is preserved by Intel NVM update tool.

# 2 Disable Protocol             0b    Disable Protocol Select

          Selection Menu                     If set to 1b, the user is not allowed to change the boot protocol. Default value is 0b.
                                               0b = Enable
                                               1b = Disable
                                             Note: This field is preserved by Intel NVM update tool.

# 1 Disable Title                0b    Disable Title Message

          Message Display                    If this bit is set to 1b, the title message displaying the version of the Boot Agent is
                                             suppressed; the Control-S message is also suppressed. This is for OEMs who do not
                                             wish the boot agent to display any messages at system boot. Default value is 0b.
                                               0b = Enable
                                               1b = Disable
                                             Note: This field is preserved by Intel NVM update tool.

# 0 Disable Setup Menu           0b    Disable Setup Menu

                                             If this bit is set to 1b, the user is not allowed to invoke the setup menu by pressing
                                             Control-S. In this case, the NVM may only be changed via an external program. Default
                                             value is 0b.
                                               0b = Enable
                                               1b = Disable
                                             Note: This field is preserved by Intel NVM update tool.

6.2.2.55                iSCSI Option ROM Version (0x0036)
Word 0x36 of the NVM is used to store the version of iSCSI Option ROM updated. The value must be
above 0x2000 and the value below (word 0x1FFF = 16 KB NVM size) is reserved for future expansion
for a pointer to combo option ROM component version structure. iSCSIUtl, FLAUtil, DMiX update iSCSI
Option ROM version if the value is above 0x2000, 0x0000, or 0xFFFF. The pointer (0x0040 - 0x1FFF)
should be kept and not be overwritten.

 Bit(s)    Field Name        Default                                            Description

  15:0    Reserved           0xFFFF     Reserved.
                                        Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                             247
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

#### 6.2.2.56 Alternate Ethernet MAC Addresses Pointer (0x0037)

The alternate MAC Address does not function if the pointer value is set to 0xFFFF. Word offset for port 0
MAC Address is: value in word 0x37 + 0 ; ;- 3 words. Word offset for port 1 MAC Address is: value in
word 0x37 + 3 ; ;- Next 3 words.

 Bit(s)    Field Name     Default                                               Description

  15:0    Pointer             0xFFFF    Pointer
                                        Points to Alternate Ethernet MAC Address Section. For Alternate Ethernet MAC Address inner
                                        structure, see Section 6.2.8.

#### 6.2.2.57 NVM Control Word 3 (0x0038)

 Bit(s)        Field Name              Default                                      Description

  15:9    Reserved                      0x03     Reserved

# 8 D10GMP Port 1                  1b      D10GMP Port

                                                 Disable 10 GbE in LPLU for LAN Port 1. When set, LAN port 1 never advertises 10
                                                 GbE speed capability when in LPLU state (D3/Dr).
                                                 Note: This field is preserved by Intel NVM update tool.

# 7 D1GMP Port 1                   0b      D1GMP Port

                                                 Disable 1 GbE in LPLU for LAN Port 1. When set, LAN port 1 never advertises 1 GbE
                                                 speed capability when in LPLU state (D3/Dr). If set, D10GMP bit must be set as well.
                                                 Note: This field is preserved by Intel NVM update tool.

# 6 D10GMP Port 0                  1b      D10GMP Port

                                                 Disable 10 GbE in LPLU for LAN Port 0. When set, LAN port 0 never advertises 10
                                                 GbE speed capability when in LPLU state (D3/Dr).
                                                 Note: This field is preserved by Intel NVM update tool.

# 5 D1GMP Port 0                   0b      D1GMP Port

                                                 Disable 1 GbE in LPLU for LAN Port 0. When set, LAN port 0 never advertises 1 GbE
                                                 speed capability when in LPLU state (D3/Dr). If set, D10GMP bit must be set as well.
                                                 Note: This field is preserved by Intel NVM update tool.

# 4 Reserved                       0b      Reserved

# 3 Enable LPLU                    1b      Enable LPLU

                                                 Enable the Low Power Link Up feature. When set, enables a decrease in link speed of
                                                 the port defined to stay awake in non-D0a states when power policy and power
                                                 management states dictate it.
                                                 Note: This field is preserved by Intel NVM update tool.

# 2 Keep_PHY_Link_Up_En            1b      Keep_PHY_Link_Up_En

                                                 Enables No PHY Link Down when the MC indicates that the PHY should be kept on.
                                                 When asserted, this bit prevents changes in power management state to be
                                                 reflected to the PHYs according to the MMNGC.MNG_VETO bit value. When cleared,
                                                 the MMNGC.MNG_VETO bit is meaningless.
                                                 Note: This field is preserved by Intel NVM update tool.

    1 APM Enable Port 1              0b      APM Enable Port

                                                 Initial value of advanced power management wake up enable in the General Receive
                                                 Control register (GRC.APME). Mapped to GRC.APME of port 1.
                                                 Note: This field is preserved by Intel NVM update tool.

    0 APM Enable Port 0              0b      APM Enable Port

                                                 Initial value of advanced power management wake up enable in the General Receive
                                                 Control register (GRC.APME). Mapped to GRC.APME of port 0.
                                                 Note: This field is preserved by Intel NVM update tool.

248                                                                                                                      333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.58 FCoE Scratch Pad Pointer (0x0039)

 Bit(s)          Field Name             Default                                     Description

  15:0    FCOE Scratch Pad Pointer        0x0      FCOE Scratch Pad Pointer
                                                   Points to FCoE Scratch Pad Header Section. For FCoE Scratch Pad Header inner
                                                   structure, see Section 6.2.9.

#### 6.2.2.59 Firmware Code Pointer (0x003A)

The address is in 4KB sector index units.

 Bit(s)         Field Name            Default                                     Description

# 15 Pointer Type                  1b      Pointer Type

                                                 0b = Word units
                                                 1b = 4 KB sector units
  14:0    Firmware Code Pointer        0x0      Points to Firmware Module Section. For Firmware Module inner structure, see
                                                Section 6.2.30.

#### 6.2.2.60 Hardware (0x003B)

 Bit(s)    Field Name      Default                                            Description

  15:0    Reserved           0xFFFF    Reserved.

#### 6.2.2.61 Hardware (0x003C)

 Bit(s)      Field Name    Default                                            Description

  15:0    Reserved           0xFFFF    Reserved.

#### 6.2.2.62 Hardware (0x003D)

 Bit(s)      Field Name    Default                                            Description

  15:0    Reserved                     Reserved.

#### 6.2.2.63 Hardware (0x003E)

 Bit(s)      Field Name    Default                                            Description

  15:0    Reserved                     Reserved.

#### 6.2.2.64 Software Checksum, Words 0x00 - 0x3F (0x003F)

The checksum word (0x3F) is used to ensure that the base NVM image is a valid image. It covers
contents of all the NVM modules located in the first valid 4KB sector, excepted to all Firmware modules.
The value of this word should be calculated such that after adding all the concerned words, including
the checksum word itself, the sum should be 0xBABA. This word is used strictly by the software. The

333369-009                                                                                                                    249
                                       Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                 Non-Volatile Memory Map

hardware does not calculate nor check its content but rather checks the Signature field in the NVM
Control Word 1.

 Bit(s)      Field Name   Default                                           Description

  15:0    Checksum                  Checksum
                                    The following documents the calculation:
                                    #define IXGBE_EEPROM_CHECKSUM 0x3F
                                    #define IXGBE_EEPROM_SUM 0xBABA
                                    #define IXGBE_PCIE_ANALOG_PTR 0x03
                                    #define IXGBE_PHY_PTR               0x04
                                    #define IXGBE_OPTION_ROM_PTR 0x05
                                    #define IXGBE_FW_PTR 0x0F
                                    /**
                                     * ixgbe_calc_eeprom_checksum_X540 - Calculates and returns the checksum
                                     * @hw: pointer to hardware structure
                                     **/
                                    u16 ixgbe_calc_eeprom_checksum_X540(struct ixgbe_hw *hw)
                                    {
                                         u16 i;
                                         u16 j;
                                         u16 checksum = 0;
                                         u16 length = 0;
                                         u16 pointer = 0;
                                         u16 word = 0;
                                         DEBUGFUNC("ixgbe_calc_eeprom_checksum_X540");
                                    /* Include 0x0-0x3F in the checksum */
                                         for (i = 0; i < IXGBE_EEPROM_CHECKSUM; i++) {
                                              if (hw->eeprom.ops.read(hw, i, &word) != IXGBE_SUCCESS) {
                                                    DEBUGOUT("EEPROM read failed\n");
                                                    break;
                                              }
                                              checksum += word;
                                         }
                                         /*
                                          * Include all data from pointers 0x3, 0x6-0xE. This excludes the
                                          * FW, PHY module, and PCIe Expansion/Option ROM pointers.
                                          */
                                         for (i = IXGBE_PCIE_ANALOG_PTR; i < IXGBE_FW_PTR; i++) {
                                              if (i == IXGBE_PHY_PTR || i == IXGBE_OPTION_ROM_PTR)
                                                    continue;
                                              if (hw->eeprom.ops.read(hw, i, &pointer) != IXGBE_SUCCESS) {
                                                    DEBUGOUT("EEPROM read failed\n");
                                                    break;
                                              }
                                              /* Skip pointer section if the pointer is invalid. */
                                              if (pointer == 0xFFFF || pointer == 0 ||
                                                  pointer >= hw->eeprom.word_size)
                                                    continue;
                                              if (hw->eeprom.ops.read(hw, pointer, &length) != IXGBE_SUCCESS) {
                                                    DEBUGOUT("EEPROM read failed\n");
                                                    break;
                                              }
                                              /* Skip pointer section if length is invalid. */
                                              if (length == 0xFFFF || length == 0) ||
                                                  (pointer + length) >= hw->eeprom.word_size)
                                                    continue;
                                              for (j = pointer+1; j <= pointer+length; j++) {
                                                    if (hw->eeprom.ops.read(hw, j, &word) != IXGBE_SUCCESS) {
                                                         DEBUGOUT("EEPROM read failed\n");
                                                         break;
                                                    }
                                                    checksum += word;
                                              }
                                         }
                                         checksum = (u16)IXGBE_EEPROM_SUM - checksum;
                                         return checksum;
                                    }

250                                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.65 Free Provisioning Area Pointer (0x0040)

 Bit(s)        Field Name            Default                                       Description

# 15 Pointer Type                  1b

  14:0    Free Provisioning Area        0x0     Free Provisioning Area Pointer
          Pointer                               Points to Free Provisioning Module Section. For Free Provisioning Module inner
                                                structure, see Section 6.2.33.

#### 6.2.2.66 Free Provisioning Area Size (0x0041)

 Bit(s)          Field Name              Default                                      Description

  15:0    Free Provisioning Area Size        0x7A   Free Provisioning Area Size

#### 6.2.2.67 Mini Loader Pointer (0x0042)

 Bit(s)          Field Name              Default                                      Description

  15:0    Mini Loader Section Pointer     0xFFFF    Mini Loader Section Pointer
                                                    Points to Mini Loader Module Section. For Mini Loader Module inner structure,
                                                    see Section 6.2.24.

#### 6.2.2.68 PHY Config Pointer (0x0043)

 Bit(s)          Field Name              Default                                      Description

  15:0    PHY Config Section Pointer      0xFFFF    PHY Config Section Pointer
                                                    Points to PHY Config Section. For PHY Config inner structure, see Section 6.2.25.

#### 6.2.2.69 Reserved (0x0044)

 Bit(s)    Field Name      Default                                             Description

  15:0    Reserved                      Reserved.

#### 6.2.2.70 Reserved (0x0045)

#### 6.2.2.71 Reserved (0x0046)

 Bit(s)    Field Name      Default                                             Description

  15:0    Reserved                      Reserved.

#### 6.2.2.72 Reserved (0x0047)

 Bit(s)    Field Name      Default                                             Description

  15:0    Reserved                      Reserved.

333369-009                                                                                                                        251
                                        Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                          Non-Volatile Memory Map

#### 6.2.2.73 Reserved (0x0048)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.74 Reserved (0x0049)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.75 Reserved (0x004A)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.76 Reserved (0x004B)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.77 Reserved (0x004C)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.78 Reserved (0x004D)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.79 Reserved (0x004E)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

#### 6.2.2.80 Reserved (0x004F)

 Bit(s)    Field Name    Default                                    Description

  15:0    Reserved                 Reserved.

252                                                                                                    333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.2.81 RO Updates Version (0x0050)

 Bit(s)      Field Name        Default                                Description

  15:0    RO Updates Version    0x0      Reserved.

333369-009                                                                          253
                                   Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

### 6.2.3 MAC Module Section

Table 6-9.         MAC Module General Summary Table
                                                                                                                     Section
 Word Offset                                                Description
                                                                                                                     Number

0x0000             Reserved                                                                                           6.2.3.1

0x0001             MAC Configuration                                                                                  6.2.3.2

0x0002             MAC Configuration Extended                                                                         6.2.3.3

#### 6.2.3.1 Reserved (0x0000)

#### 6.2.3.2 MAC Configuration (0x0001)

 Bit(s)     Field Name         Default                                         Description

# 15 Reserved               0b      Reserved.

# 14 Reserved               00b     Reserved.

 13:10    FIFOLT                 0x3     FIFO Low Threshold
                                         Determines the low threshold of the MAC elastic FIFO. Mapped to MACC.FIFOHT.
  9:6     FIFOHT                 0xD     FIFO High Threshold. Determines the high threshold of the MAC elastic FIFO. Mapped to
                                         MACC.FIFOLT.

# 5 Swap Rx Control        0b      Swap Rx Control

                                         Swap the MAC internal Rx XGMII controls
                                          0b = Swap disabled, normal mode.
                                          1b = Swap enabled.
                                         Mapped to MACC.Swap Rx Control.

# 4 Swap Rx Data           0b      Swap Rx Data

                                         Swap the MAC internal Rx XGMII lanes.
                                          0b = Swap disabled, normal mode.
                                          1b = Swap enabled.
                                         Mapped to MACC.Swap Rx Data.

# 3 Swizzle Rx Data        0b      Swizzle Rx Data

                                         Swizzle the bytes in all 4 MAC internal Rx XGMII lanes.
                                          0b = Swizzle disabled, normal mode.
                                          1b = Swizzle enabled.
                                         Mapped to MACC.Swizzle Rx Data.

# 2 Swap Tx Control        0b      Swap Tx Control

                                         Swap the MAC internal Tx XGMII controls.
                                          0b = Swap disabled, normal mode.
                                          1b = Swap enabled.
                                         Mapped to MACC.Swap Tx Control.

# 1 Swap Tx Data           0b      Swap Tx Data

                                         Swap the MAC internal Tx XGMII lanes.
                                          0b = Swap disabled, normal mode.
                                          1b = Swap enabled.
                                         Mapped to MACC.Swap Tx Data.

# 0 Swizzle Tx Data        0b      Swizzle Tx Data

                                         Swizzle the bytes in all 4 MAC internal Tx XGMII lanes.
                                          0b = Swizzle disabled, normal mode.
                                          1b = Swizzle enabled.
                                         Mapped to MACC.Swizzle Tx Data.

254                                                                                                                 333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.3.3 MAC Configuration Extended (0x0002)

 Bit(s)    Field Name    Default                                          Description

  15:3    Reserved        0x0      Reserved.

    2 LDINFITR         0b      Link Down in Fatal Interrupt

                                    0b = Normal operation. The link indication is the same as comes from the PCS and auto
                                         negotiation machinery.
                                    1b = Link indication is gated with the Fatal interrupt from the PHY. When the PHY assert
                                         fatal interrupt the link is down.
  1:0     BLKXGMII        00b      Block XGMII Interface
                                    00b = Normal Operation — The XGMII interface fed from the PCS while link is down.
                                    01b = Idle State — The XGMII interface fed with Idles while link is down.
                                    10b = Local Fault State — The XGMII interface fed with Local Fault sequences while link is
                                          down.
                                    11b = Reserved.

333369-009                                                                                                                     255
                                   Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

### 6.2.4 CSR Auto Config Section

Table 6-10. CSR Auto Config Section Summary Table
                                                                                                             Section
 Word Offset                                            Description
                                                                                                            Reverence

0x0000          Section Length                                                                                6.2.4.1

0x0001          CSR RAW1                                                                                      6.2.4.2

0x0002          CSR RAW2                                                                                      6.2.4.3

#### 6.2.4.1 Section Length (0x0000)

The section length word contains the length of the section in words. Note that section length does not
include a count for the section length word. Section Length = 3*n (n = number of CSRs to configure).

 Bit(s)     Field Name      Default                                        Description

  15:0    Section Length              Section Length
                                      Length in: 2 Bytes unit - 1
                                       First Section -> Word: CSR Auto Config -> Section length
                                       Last Section -> Word: CSR Auto Config -> CSR RAW2
                                       Section length in words

#### 6.2.4.2 CSR RAW1 (0x0001)

Raw data module length: variable

#### 6.2.4.3 CSR RAW2 (0x0002)

Raw data module length: variable
The section length word contains the length of the section in words. Note that section length does not
include a count for the section length word. Section Length = 3*n (n = number of CSRs to configure).

256                                                                                                          333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.5 LAN Core Module Section

Table 6-11. LAN Core Module Section Summary Table
                                                                                                                 Section
 Word Offset                                                  Description
                                                                                                                 Number

 0x0000          Section Length                                                                                   6.2.5.1

 0x0001          Ethernet MAC Address Register1                                                                   6.2.5.2

 0x0002          Ethernet MAC Address Register2                                                                   6.2.5.3

 0x0003          Ethernet MAC Address Register3                                                                   6.2.5.4

 0x0004          LED Control Lower Word                                                                           6.2.5.5

 0x0005          LED Control Upper Word                                                                           6.2.5.6

 0x0006          SDP Control                                                                                      6.2.5.7

 0x0007          Filter Control                                                                                   6.2.5.8

#### 6.2.5.1 Section Length (0x0000)

The section length word contains the length of the section in words. Note that section length does not
include a count for the section length word.

 Bit(s)      Field Name           Default                                        Description

  15:0    Section Length                    Section Length
                                            Length in: 2 Bytes unit - 1
                                             First Section -> Word: LAN Core Module -> Section Length
                                             Last Section -> Word: LAN Core Module -> Filter Control
                                             Section Length in words

#### 6.2.5.2 Ethernet MAC Address Register1 (0x0001)

The Ethernet Individual Address (IA) is a 6-byte field that must be unique for each NIC or LOM and
must also be unique for each copy of the NVM image. The first three bytes are vendor specific. For
example, the IA is equal to [00 AA 00] or [00 A0 C9] for Intel products. The value of this field is loaded
into the Receive Address register 0 (RAL0/RAH0). For the purpose of this specification, the numbering
convention is as follows: Vendor ; ; ; ; ; ; ; ; ; ; ; ; ; ; ; ;1 ; ; ; ; ; ; ; ; ; ; ; ; ; ;2 ; ; ; ; ; ; ; ; ; ; ; ; ;
;3 ; ; ; ; ; ; ; ; ; ; ; ; ; ;4 ; ; ; ; ; ; ; ; ; ; ; ; ; ;5 ; ; ; ; ; ; ; ; ; ; ; ; ; ;6 Intel original ; ; ; ; ; ;00 ; ; ;
; ; ; ; ; ; ; ; ;AA ; ; ; ; ; ; ; ; ; ; ; ;00 ; ; ;Variable ; ; ;Variable ; ; ;Variable Intel new ; ; ; ; ; ; ; ; ; ;
;00 ; ; ; ; ; ; ; ; ; ; ; ;A0 ; ; ; ; ; ; ; ; ; ; ; ;C9 ; ; ;Variable ; ; ;Variable ; ; ;Variable

 Bit(s)      Field Name           Default                                        Description

  15:8    Eth_Addr_Byte2           0x12     Ethernet MAC Address Byte 2
                                            Note: This field is preserved by Intel NVM update tool.
   7:0    Eth_Addr_Byte1           0x34     Ethernet MAC Address Byte 1
                                            Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                               257
                                          Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

#### 6.2.5.3 Ethernet MAC Address Register2 (0x0002)

 Bit(s)     Field Name     Default                                        Description

  15:8    Eth_Addr_Byte4    0x56     Ethernet MAC Address Byte 4
                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Eth_Addr_Byte3    0x78     Ethernet MAC Address Byte 3
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.5.4 Ethernet MAC Address Register3 (0x0003)

 Bit(s)     Field Name     Default                                        Description

  15:8    Eth_Addr_Byte6    0x0      Ethernet MAC Address Byte 6
                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Eth_Addr_Byte5    0x0      Ethernet MAC Address Byte 5
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.5.5 LED Control Lower Word (0x0004)

The LEDCTL register defaults are loaded from two words as listed in the following tables.

 Bit(s)     Field Name     Default                                        Description

# 15 LED1_BLINK         0b      LED 1 Blink

                                      0b = Don't Blink
                                      1b = Blink
                                     Note: This field is preserved by Intel NVM update tool.

# 14 LED1_IVRT          1b      LED 1 Invert

                                      0b = Active Low
                                      1b = Active High
                                     Note: This field is preserved by Intel NVM update tool.
 13:12    Reserved          00b      Reserved.
                                     Note: This field is preserved by Intel NVM update tool.
  11:8    LED1_MODE         0x1      LED 1 Mode
                                     LED 1 control:
                                      0x0 = LINK_UP
                                      0x1 = LINK 10G
                                      0x2 = MAC ACTIVITY
                                      0x3 = FILTER ACTIVITY
                                      0x4 = LINK/ACTIVITY
                                      0x5 = LINK 1G
                                      0x6 = LINK 100M
                                      0xE = LED ON
                                      0xF = LED OFF
                                      All other values are reserved.
                                     Note: This field is preserved by Intel NVM update tool.

# 7 LED0_BLINK         0b      LED 0 Blink

                                      0b = Don't Blink
                                      1b = Blink
                                     Note: This field is preserved by Intel NVM update tool.

258                                                                                                          333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)      Field Name      Default                                        Description

# 6 LED0_IVRT            1b      LED 0 Invert

                                        0b = Active Low
                                        1b = Active High
                                       Note: This field is preserved by Intel NVM update tool.

# 5 Global Link Mode     0b      Global Link Mode

                                        0b = 200 ms
                                        1b = 83 ms
                                       Note: This field is preserved by Intel NVM update tool.

# 4 Reserved             0b      Reserved.

                                       Note: This field is preserved by Intel NVM update tool.
  3:0     LED0_MODE           0x0      LED 0 Mode
                                       LED 0 control:
                                        0x0 = LINK_UP
                                        0x1 = LINK 10G
                                        0x2 = MAC ACTIVITY
                                        0x3 = FILTER ACTIVITY
                                        0x4 = LINK/ACTIVITY
                                        0x5 = LINK 1G
                                        0x6 = LINK 100M
                                        0xE = LED ON
                                        0xF = LED OFF
                                        All other values are reserved.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.5.6 LED Control Upper Word (0x0005)

 Bit(s)      Field Name      Default                                        Description

# 15 LED3_BLINK           0b      LED 3 Blink

                                        0b = Don't Blink
                                        1b = Blink
                                       Note: This field is preserved by Intel NVM update tool.

# 14 LED3_IVRT            1b      LED 3 Invert

                                        0b = Active Low
                                        1b = Active High
                                       Note: This field is preserved by Intel NVM update tool.
 13:12    Reserved            00b      Reserved.
                                       Note: This field is preserved by Intel NVM update tool.
  11:8    LED3_MODE           0x5      LED 3 Mode
                                       LED 3 control:
                                        0x0 = LINK_UP
                                        0x1 = LINK 10G
                                        0x2 = MAC ACTIVITY
                                        0x3 = FILTER ACTIVITY
                                        0x4 = LINK/ACTIVITY
                                        0x5 = LINK 1G
                                        0x6 = LINK 100M
                                        0xE = LED ON
                                        0xF = LED OFF
                                        All other values are reserved.
                                       Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                       259
                                    Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                               Non-Volatile Memory Map

 Bit(s)     Field Name    Default                                        Description

# 7 LED2_BLINK        1b      LED 2 Blink

                                     0b = Don't Blink
                                     1b = Blink
                                    Note: This field is preserved by Intel NVM update tool.

# 6 LED2_IVRT         0b      LED 2 Invert

                                     0b = Active Low
                                     1b = Active High
                                    Note: This field is preserved by Intel NVM update tool.
  5:4     Reserved         00b      Reserved.
                                    Note: This field is preserved by Intel NVM update tool.
  3:0     LED2_MODE        0x4      LED 2 Mode
                                    LED 2 control:
                                     0x0 = LINK_UP
                                     0x1 = LINK 10G
                                     0x2 = MAC ACTIVITY
                                     0x3 = FILTER ACTIVITY
                                     0x4 = LINK/ACTIVITY
                                     0x5 = LINK 1G
                                     0x6 = LINK 100M
                                     0xE = LED ON
                                     0xF = LED OFF
                                     All other values are reserved.
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.5.7 SDP Control (0x0006)

 Bit(s)     Field Name    Default                                        Description

# 15 SDP3_NATIVE       0b      SDP3 Native

                                    Defines SDP3 operating mode is mapped to ESDP.SDP3_NATIVE loaded at power up.
                                     0b = Operates as generic software controlled IO.
                                     1b = Native mode operation (hardware function).
                                    Note: This field is preserved by Intel NVM update tool.

# 14 SDP2_NATIVE       0b      SDP2 Native

                                    Defines SDP2 operating mode is mapped to ESDP.SDP2_NATIVE loaded at power up.
                                     0b = Operates as generic software controlled IO.
                                     1b = Native mode operation (hardware function).
                                    Note: This field is preserved by Intel NVM update tool.

# 13 SDP1_NATIVE       0b      SDP1 Native

                                    Defines SDP1 operating mode is mapped to ESDP.SDP1_NATIVE loaded at power up.
                                     0b = Operates as generic software controlled IO.
                                     1b = Native mode operation (hardware function).
                                    Note: This field is preserved by Intel NVM update tool.

# 12 SDP0_NATIVE       0b      SDP0 Native

                                    Defines SDP0 operating mode is mapped to ESDP.SDP0_NATIVE loaded at power up.
                                     0b = Operates as generic software controlled IO.
                                     1b = Native mode operation (hardware function).
                                    Note: This field is preserved by Intel NVM update tool.

    11 SDPDIR[3]         0b      SDP3 Direction

                                    Initial Direction is mapped to ESDP.SDP3_IODIR loaded at power up.
                                    Note: This field is preserved by Intel NVM update tool.

    10 SDPDIR[2]         0b      SDP2 Direction

                                    Initial Direction is mapped to ESDP.SDP2_IODIR loaded at power up.
                                    Note: This field is preserved by Intel NVM update tool.

260                                                                                                         333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)      Field Name      Default                                         Description

    9 SDPDIR[1]            0b      SDP1 Direction

                                       Initial Direction is mapped to ESDP.SDP1_IODIR loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

    8 SDPDIR[0]            0b      SDP0 Direction

                                       Initial Direction is mapped to ESDP.SDP0_IODIR loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

# 7 Reserved             0b      Reserved.

                                       Note: This field is preserved by Intel NVM update tool.

# 6 REVERSE_DIR          0b      Reverse Direction

                                       When set, reverses the polarity of the pin direction signal to pads block, such that pads
                                       are fed with output enable signal instead of output disable. Should be cleared for normal
                                       operation.
                                       Note: This field is preserved by Intel NVM update tool.

# 5 SDP23_function       0b      SDP23 Function

                                       Defines the initial value for ESDP.SDP23_function.
                                        0b = 1588 functionality
                                        1b = I2C functionality.
                                       Relevant only if SDP2_NATIVE or SDP3_NATIVE is set. If this bit is set, then SDP2_NATIVE
                                       and SDP3_NATIVE should have the same value.
                                       Note: This field is preserved by Intel NVM update tool.

# 4 SDP1_function        0b      SDP1 Function

                                       Defines the initial value for ESDP.SDP1_function.
                                        0b = Time Sync functionality.
                                        1b = SDP1 Thermal sensor functionality.
                                       SDPDIR[1] should be configured as an output.
                                       Relevant only if SDP1_NATIVE is set.
                                       Note: This field is preserved by Intel NVM update tool.

    3 SDPVAL[3]            0b      SDP3 Value

                                       Initial Output Value is mapped to ESDP.SDP3_DATA loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

    2 SDPVAL[2]            0b      SDP2 Value

                                       Initial Output Value is mapped to ESDP.SDP2_DATA loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

    1 SDPVAL[1]            0b      SDP1 Value

                                       Initial Output Value is mapped to ESDP.SDP1_DATA loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

    0 SDPVAL[0]            0b      SDP0 Value

                                       Initial Output Value is mapped to ESDP.SDP0_DATA loaded at power up.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.5.8 Filter Control (0x0007)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved         0x0001    Reserved.

333369-009                                                                                                                    261
                                     Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                       Non-Volatile Memory Map

### 6.2.6 PCIe General Configuration Module Section

Table 6-12. PCIe General Configuration Module Section Summary Table
                                                                                                    Section
 Word Offset                                      Description
                                                                                                    Number

0x0000         PCI_CNF2 Low                                                                          6.2.6.1

0x0001         PCI_CNF2 High                                                                         6.2.6.2

0x0002         PCI_LBARCTRL L                                                                        6.2.6.3

0x0003         PCI_LBARCTRL H                                                                        6.2.6.4

0x0004         PCI_SERL 1                                                                            6.2.6.5

0x0005         PCI_SERL 2                                                                            6.2.6.6

0x0006         PCI_SERL 3                                                                            6.2.6.7

0x0007         PCI_SERL 4                                                                            6.2.6.8

0x0008         PCI_CAPCTRL L                                                                         6.2.6.9

0x0009         PCI_CAPCTRL H                                                                         6.2.6.10

0x000A         PCI_CAPSUP L                                                                          6.2.6.11

0x000B         PCI_CAPSUP H                                                                          6.2.6.12

0x000C         PCI_DBGCTL L                                                                          6.2.6.13

0x000D         PCI_DBGCTL H                                                                          6.2.6.14

0x000E         PCI_UPADD L                                                                           6.2.6.15

0x000F         PCI_UPADD H                                                                           6.2.6.16

0x0010         PCI_SUBSYSID L                                                                        6.2.6.17

0x0011         PCI_SUBSYSID H                                                                        6.2.6.18

0x0012         PCI_PWRDATA L                                                                         6.2.6.19

0x0013         PCI_PWRDATA H                                                                         6.2.6.20

0x0014         PCI_REVID L                                                                           6.2.6.21

0x0015         PCI_REVID H                                                                           6.2.6.22

0x0016         PCI_VFSUP L                                                                           6.2.6.23

0x0017         PCI_VFSUP H                                                                           6.2.6.24

0x0018         TPH_CTRL L                                                                            6.2.6.25

0x0019         TPH_CTRL H                                                                            6.2.6.26

0x001A         PCI_LINKCAP L                                                                         6.2.6.27

0x001B         PCI_LINKCAP H                                                                         6.2.6.28

0x001C         PCI_PMSUP L                                                                           6.2.6.29

0x001D         PCI_PMSUP H                                                                           6.2.6.30

0x001E         PCI_GLBL_CNF L                                                                        6.2.6.31

0x001F         PCI_GLBL_CNF H                                                                        6.2.6.32

0x0020         PCI_VENDORID L                                                                        6.2.6.33

0x0021         PCI_VENDORID H                                                                        6.2.6.34

262                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-12. PCIe General Configuration Module Section Summary Table [continued]
                                                                                                     Section
 Word Offset                                                  Description
                                                                                                     Number

0x0022            PCI_PCIERR L                                                                       6.2.6.35

0x0023            PCI_PCIERR H                                                                       6.2.6.36

#### 6.2.6.1 PCI_CNF2 Low (0x0000)

MSI-x and cache line configuration.

 Bit(s)      Field Name          Default                                          Description

  15:0    PCI_CNF2 Low       0x400040FC        PCI_CNF2 Low

#### 6.2.6.2 PCI_CNF2 High (0x0001)

 Bit(s)      Field Name      Default                                            Description

  15:0    PCI_CNF2 High                    PCI_CNF2 High

#### 6.2.6.3 PCI_LBARCTRL L (0x0002)

PF BAR registers configuration.

 Bit(s)      Field Name      Default                                            Description

 15:14    RESERVED               00b       Reserved.
 13:11    EXROM_BAR_             011b      Expansion ROM BAR
                                            000b = 64 KB
                                            001b = 128 KB
                                            010b = 256 KB
                                            011b = 512 KB
                                            100b = 1 MB
                                            101b = 2 MB
                                            110b = 4 MB
                                            111b = 8 MB
  10:9    RESERVED               00b       Reserved.
  8:6     FL_BAR_SIZE            101b      Flash BAR Size
                                            101b = 2 MB
                                            110b = 4 MB
                                            111b = 8 MB
                                            All other values are reserved.
  5:4     RESERVED               00b       Reserved.

# 3 FLASH_EXPOSE            1b       Flash Expose

                                            0b = Disabled
                                            1b = Enabled

    2 CSRSIZE                 1b       CSR Size

                                           Note: This field is preserved by Intel NVM update tool.

# 1 BAR32                   0b       BAR32

                                            0b = 64-bit Addressing
                                            1b = 2-bit Addressing

333369-009                                                                                                  263
                                        Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

 Bit(s)     Field Name     Default                                         Description

    0 PREFBAR            1b      Prefetch BAR

                                      0b = No Prefetch
                                      1b = Prefetch Enabled

#### 6.2.6.4 PCI_LBARCTRL H (0x0003)

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved        0x0      Reserved.

#### 6.2.6.5 PCI_SERL 1 (0x0004)

PCIe Serial Number.

 Bit(s)    Field Name    Default                                         Description

  15:0    PCI_SER 1       0x0      PCIe Serial Number 1
                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.6 PCI_SERL 2 (0x0005)

 Bit(s)    Field Name    Default                                         Description

  15:0    PCI_SERL 2      0xC9     PCIe Serial Number 2
                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.7 PCI_SERL 3 (0x0006)

 Bit(s)    Field Name    Default                                         Description

  15:0    PCI_SERL 3      0x0      PCIe Serial Number 3
                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.8 PCI_SERL 4 (0x0007)

 Bit(s)    Field Name    Default                                         Description

  15:0    PCI_SERL 4      0xC9     PCIe Serial Number 4
                                   Note: This field is preserved by Intel NVM update tool.

264                                                                                                          333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.6.9 PCI_CAPCTRL L (0x0008)

VPD_EN

 Bit(s)      Field Name    Default                                          Description

  15:1    PCI_CAPCTRL L      0x0     PCIe Capabilities Control Low

# 0 VPD_EN            0xC9     VPD Enable

                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.10 PCI_CAPCTRL H (0x0009)

 Bit(s)      Field Name    Default                                          Description

  15:0    PCI_CAPCTRL H      0x0     PCIe Capabilities Control High

#### 6.2.6.11 PCI_CAPSUP L (0x000A)

PCIe Capabilities exposed.

 Bit(s)      Field Name    Default                                          Description

# 15 ECRC_MCTP_GEN      0b      ECRC Generation for MCTP

                                      0b = Disabled — Do not add ECRC to MCTP packets even if ECRC is enabled.
                                      1b = Enabled — Add ECRC to MCTP packets if ECRC is enabled via the ECRC
                                     Generation Enable field in PCIe Advanced Error Capabilities and Control Register.
  14:8    Reserved           0x0     Reserved.

# 7 SEC_EN             1b      Secondary Enable

                                     A value of 1b indicates support for the Secondary PCI Express Extended Capability.
                                      0b = Disabled
                                      1b = Enabled

# 6 ACS_EN             1b      ACS Enable

                                     A value of 1b indicates support for the PCIe ACS Capability
                                      0b = Disabled
                                      1b = Enabled

# 5 IOV_EN             1b      SR-IOV Enable

                                     A value of 1b indicates support for the PCIe SR-IOV Capability
                                      0b = Disabled
                                      1b = Enabled
                                     Note: This field is preserved by Intel NVM update tool.

# 4 ARI_EN             1b      ARI Enable

                                     A value of 1b indicates support for the PCIe ARI Capability
                                      0b = Disabled
                                      1b = Enabled

# 3 TPH_EN             1b      TPH Enable

                                     A value of 1b indicates support for the PCIe TPH Requester Capability
                                      0b = Disabled
                                      1b = Enabled

# 2 LTR_EN             1b      LTR Enable

                                     A value of 1b indicates support for the PCIe Latency Tolerance Reporting (LTR) Capability
                                      0b = Disabled
                                      1b = Enabled

# 1 Reserved           0b      Reserved.

333369-009                                                                                                                  265
                                   Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

 Bit(s)     Field Name     Default                                           Description

# 0 PCIE_VER           1b        PCIe Version

                                        0b = 0x1-Capability version
                                        1b = 0x2-Capability version

#### 6.2.6.12 PCI_CAPSUP H (0x000B)

 Bit(s)      Field Name      Default                                           Description

# 15 LOAD_DEV_ID             1b     Load Device ID

                                         When set to 1b, indicates that the device loads its PCI device IDs from NVM.
                                          0b = Disabled
                                          1b = Enabled

# 14 LOAD_SUBSYS_ID          1b     Load Subsystem IDs

                                         When set to 1b, indicates that the device loads its PCIe subsystem ID and sub-system
                                         vendor ID from NVM.
                                          0b = Disabled
                                          1b = Enabled
  13:5    Reserved             0x0       Reserved.

# 4 CSR_CONF__EN            1b     CSR Configuration Space Enable

                                         Enables Access to CSRs via the PCI Configuration Space. Section 8.1.3, “Configuration
                                         Access to Internal Registers and Memories”.
                                          0b = Disabled
                                          1b = Enabled

# 3 MSI_MASK                1b     MSI Mask

                                         MSI per-vector masking setting. This bit is loaded to the masking bit (bit 8) in the
                                         Message Control of the MSI Configuration Capability structure.
                                          0b = Disabled
                                          1b = Enabled

# 2 IDO__EN                 1b     ID-Based Ordering (IDO) Enable

                                          0b = Disabled
                                          1b = Enabled

# 1 ECRC_CHK__EN            1b     ECRC Check Enable

                                         Loaded into the ECRC Check Capable bit of the PCIe Configuration registers.
                                          0b = Disabled
                                          1b = Enabled

# 0 ECRC_GEN__EN            1b     ECRC Generation Enable

                                         Loaded into the ECRC Generation Capable bit of the PCIe Configuration registers.
                                          0b = Disabled
                                          1b = Enabled

#### 6.2.6.13 PCI_DBGCTL L (0x000C)

Allow access to VF config space.

 Bit(s)     Field Name     Default                                           Description

  15:0    PCI_DBGCTL L      0x1        PCIe Debug Control Low

266                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.6.14 PCI_DBGCTL H (0x000D)

 Bit(s)      Field Name     Default                                         Description

  15:0    PCI_DBGCTL H                PCIe Debug Control High

#### 6.2.6.15 PCI_UPADD L (0x000E)

Upper Address accessible.

 Bit(s)    Field Name     Default                                         Description

  15:1    ADDRESS          0x0      Address

    0 MODE             0x0      Mode

#### 6.2.6.16 PCI_UPADD H (0x000F)

 Bit(s)    Field Name     Default                                         Description

  15:0    ADDRESS          0x0      Address

#### 6.2.6.17 PCI_SUBSYSID L (0x0010)

PCIe Subsystem ID.

 Bit(s)    Field Name     Default                                         Description

  15:0    SUB_VEN_ID      0x8086    Sub-Vendor ID
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.18 PCI_SUBSYSID H (0x0011)

 Bit(s)    Field Name     Default                                         Description

  15:0    SUB_ID           0x0      Sub-System ID
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.19 PCI_PWRDATA L (0x0012)

PCIe Power Data register.

 Bit(s)      Field Name     Default                                         Description

  15:0    PCI_PWRDATA L       0x0     PCIe Power Data Low

#### 6.2.6.20 PCI_PWRDATA H (0x0013)

 Bit(s)      Field Name     Default                                         Description

  15:0    PCI_PWRDATA H               PCIe Power Data High

333369-009                                                                                    267
                                    Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                           Non-Volatile Memory Map

#### 6.2.6.21 PCI_REVID L (0x0014)

Revision ID.

 Bit(s)    Field Name    Default                                     Description

  15:0    PCI_REVID L     0x0       PCIe Revision ID Low

#### 6.2.6.22 PCI_REVID H (0x0015)

 Bit(s)    Field Name    Default                                     Description

  15:0    PCI_REVID H               PCIe Revision ID High

#### 6.2.6.23 PCI_VFSUP L (0x0016)

PF Bar registers configuration.

 Bit(s)    Field Name    Default                                     Description

  15:0    PCI_VFSUP L     0x2       PCIe VF Support Low

#### 6.2.6.24 PCI_VFSUP H (0x0017)

 Bit(s)    Field Name    Default                                     Description

  15:0    PCI_VFSUP H               PCIe VF Support High

#### 6.2.6.25 TPH_CTRL L (0x0018)

TPH Control registers.

 Bit(s)    Field Name     Default                                     Description

  15:0    TPH_CTRL L     0x00001800    TPH Control Low

#### 6.2.6.26 TPH_CTRL H (0x0019)

 Bit(s)    Field Name    Default                                     Description

  15:0    TPH_CTRL H                TPH Control High

268                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.6.27 PCI_LINKCAP L (0x001A)

PCIe Link Capabilities.

 Bit(s)          Field Name            Default                                     Description

 15:13    Reserved                       000b    Reserved.
  12:9    LINK_MAX_WIDTH                 0x7     Link Maximum Width
                                                  0x1 = x1 limit
                                                  0x3 = x4 limit
                                                  0x4 = x8 limit
                                                  0x7 = No limit
                                                  All other values are reserved.
  8:6     LINK_MAX_PAYLOAD               010b    Link Maximum Payload
                                                  000b = 128 Bytes
                                                  001b = 256 Bytes
                                                  010b = 512 Bytes
                                                  011b = 1024 Bytes
                                                  100b = 2048 Bytes
                                                  All other values are reserved.
  5:2     Reserved                       0x0     Reserved.

# 1 LINK_SPEED_VECTOR_8GT           1b     Link Speed Vector 8 GT/s

                                                  0b = Disabled
                                                  1b = Enabled

# 0 LINK_SPEED_VECTOR_5GT           1b     Link Speed Vector 5 GT/s

                                                  0b = Disabled
                                                  1b = Enabled

#### 6.2.6.28 PCI_LINKCAP H (0x001B)

 Bit(s)      Field Name     Default                                         Description

  15:0    PCI_LINKCAP H       0x0      PCIe Link Capabilities High

#### 6.2.6.29 PCI_PMSUP L (0x001C)

PCIe Power Management support.

 Bit(s)    Field Name      Default                                           Description

  15:0    PCI_PMSUP L     0x00007397    PCIe Power Management Support Low
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.6.30 PCI_PMSUP H (0x001D)

 Bit(s)    Field Name     Default                                          Description

  15:0    PCI_PMSUP H                PCIe Power Management Support High

333369-009                                                                                        269
                                     Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                      Non-Volatile Memory Map

#### 6.2.6.31 PCI_GLBL_CNF L (0x001E)

Wake# enable.

 Bit(s)         Field Name             Default                                      Description

  15:8    PCIE_CLKGATE_TIMER            0x10     PCIe Clock Gate Timer
                                                 Clock gating idle timer. This field defines the number of clocks (CSR clock) of idle-
                                                 detect before gating the PCIE clocks.
  7:6     RESERVED                       00b     Reserved.

# 5 PCIE_PCLK_GATE_EN              0b      PCIe Clock Gate Enable

                                                 When set to 1b, and if PCIE_CLKGATE_DIS is 0, the PCIE PCLK will also be
                                                 dynamically gated.

# 4 PCIE_CLKGATE_L1_ONLY           0b      PCIe Clock Gate L1 Only

                                                 When set to 1b, and if PCIE_CLKGATE_DIS is 0, the clock gating of the PCIE
                                                 clocks will be only when the PCIE is in L1 state.

# 3 PCIE_CLKGAT_DIS                0b      PCIe Clock Gate Disable

                                                 When set to 0b enables dynamic clock gating of the PCIE clocks (LCB, HIU &
                                                 CSR).

# 2 WAKE_PIN_EN                    0b      Wake Pin Enable

                                                 When set to 1b enables the use of PE_WAKE_N pin for PME event in all power
                                                 states, otherwise, it is enabled only in Dr state.
                                                 Note: This field is preserved by Intel NVM update tool.
  1:0     RESERVED                       0b      Reserved.

#### 6.2.6.32 PCI_GLBL_CNF H (0x001F)

 Bit(s)    Field Name      Default                                            Description

  15:0    RESERVED                   Reserved.

#### 6.2.6.33 PCI_VENDORID L (0x0020)

Wake# enable.

 Bit(s)      Field Name        Default                                           Description

  15:0    PCI_VENDORID L        0x8086     PCIe Vendor ID Low

#### 6.2.6.34 PCI_VENDORID H (0x0021)

 Bit(s)      Field Name        Default                                           Description

  15:0    PCI_VENDORID H         0x0       PCIe Vendor ID High

#### 6.2.6.35 PCI_PCIERR L (0x0022)

Error enable.

 Bit(s)     Field Name       Default                                            Description

  15:0    PCI_PCIERR L       0x3FCB     PCIe Error Low

270                                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.6.36 PCI_PCIERR H (0x0023)

 Bit(s)      Field Name    Default                                 Description

  15:0    PCI_PCIERR H               PCIe Error High

333369-009                                                                       271
                                 Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

### 6.2.7 PCIe Configuration Space Section

Table 6-13. PCIe Configuration Space Section Summary Table
                                                                                                                            Section
 Word Offset                                                 Description
                                                                                                                            Number

0x0000          PCI_PFDEVID Low - LAN                                                                                        6.2.7.1

0x0001          PCI_PFDEVID High - SAN                                                                                       6.2.7.2

0x0002          PCI_CNF Low                                                                                                  6.2.7.3

0x0003          PCI_CNF High                                                                                                 6.2.7.4

0x0004          PCI_VFDEVID Low - LAN                                                                                        6.2.7.5

0x0005          PCI_VFDEVID High - SAN                                                                                       6.2.7.6

0x0006          PCI_CLASS Low                                                                                                6.2.7.7

0x0007          PCI_CLASS High                                                                                               6.2.7.8

#### 6.2.7.1 PCI_PFDEVID Low - LAN (0x0000)

 Bit(s)     Field Name      Default                                              Description

  15:0    PF_DEV_ID_LAN       0x1563     PF Device ID LAN
                                         If the Load Device ID in offset 0x7 of section PCIe General configuration is set, this word is
                                         loaded to the device ID of the LAN function.
                                           0x1563 = Default (2 Port)
                                           0x15D1 = 1 Port

#### 6.2.7.2 PCI_PFDEVID High - SAN (0x0001)

 Bit(s)     Field Name      Default                                              Description

  15:0    PF_DEV_ID_SAN       0x1563     PF Device ID SAN

#### 6.2.7.3 PCI_CNF Low (0x0002)

 Bit(s)    Field Name     Default                                               Description

  15:7    Reserved         0x0      Reserved.
  6:5     INT_PIN          00b      Interrupt Pin
                                    Controls the value advertised in the Interrupt Pin field of the PCI configuration header for this
                                    function.
                                      00b = INTA#
                                      01b = INTB#
                                      10b = INTC#
                                      11b = INTD#
                                    The value advertised in the PCI configuration header is the value loaded from NVM + 1.

# 4 IO_BAR            0b      I/O BAR Support

                                     0b = I/O BAR is not supported.
                                     1b = I/O BAR is supported.

272                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)    Field Name     Default                                              Description

# 3 EXROM_DIS         0b        Expansion ROM Disable

                                       0b = The Expansion ROM BAR in the PCI configuration space is enabled.
                                       1b = The Expansion ROM BAR in the PCI configuration space is disabled.
                                      Note: This field is preserved by Intel NVM update tool.
  2:0     Reserved         00b        Reserved.

#### 6.2.7.4 PCI_CNF High (0x0003)

 Bit(s)    Field Name     Default                                              Description

  15:0    Reserved         0x0        Reserved

#### 6.2.7.5 PCI_VFDEVID Low - LAN (0x0004)

 Bit(s)      Field Name     Default                                             Description

  15:0    VF_DEV_ID_LAN     0x1565      VF Device ID LAN
                                        If the Load Device ID in offset 0x7 of section PCIe General configuration is set, this word is
                                        loaded to the device ID of the LAN function.

#### 6.2.7.6 PCI_VFDEVID High - SAN (0x0005)

 Bit(s)      Field Name     Default                                             Description

  15:0    VF_DEV_ID_SAN     0x1565      VF Device ID SAN

#### 6.2.7.7 PCI_CLASS Low (0x0006)

 Bit(s)      Field Name     Default                                             Description

  15:1    Reserved            0x0       Reserved.

# 0 STORAGE_CLASS          0b     Storage Class

                                         0b = The class code of this port is set to 0x020000 (LAN).
                                         1b = The class code of this port is set to 0x010000 (SCSI).

#### 6.2.7.8 PCI_CLASS High (0x0007)

 Bit(s)      Field Name     Default                                             Description

  15:1    Reserved            0x0       Reserved.

# 0 STORAGE_CLASS          0b     Storage Class

                                         0b = The class code of this port is set to 0x020000 (LAN).
                                         1b = The class code of this port is set to 0x010000 (SCSI).

333369-009                                                                                                                         273
                                      Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                  Non-Volatile Memory Map

### 6.2.8 Alternate Ethernet MAC Address Section

Table 6-14. Alternate Ethernet MAC Address Section Summary Table
                                                                                                               Section
 Word Offset                                             Description
                                                                                                               Number

0x0000          MAC Address Word 1 Port 0                                                                       6.2.8.1

0x0001          MAC Address Word 2 Port 0                                                                       6.2.8.2

0x0002          MAC Address Word 3 Port 0                                                                       6.2.8.3

0x0003          MAC Address Word 1 Port 1                                                                       6.2.8.4

0x0004          MAC Address Word 2 Port 1                                                                       6.2.8.5

0x0005          MAC Address Word 3 Port 1                                                                       6.2.8.6

#### 6.2.8.1 MAC Address Word 1 Port 0 (0x0000)

Port 0 MAC Address Word 1.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 1 Port 0      0xFFFF   MAC Address Word 1 Port 0
                                                  Note: This field is preserved by Intel NVM update tool.

#### 6.2.8.2 MAC Address Word 2 Port 0 (0x0001)

Port 0 MAC Address Word 2.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 2 Port 0      0xFFFF   MAC Address Word 2 Port 0
                                                  Note: This field is preserved by Intel NVM update tool.

#### 6.2.8.3 MAC Address Word 3 Port 0 (0x0002)

Port 0 MAC Address Word 3.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 3 Port 0      0xFFFF   MAC Address Word 3 Port 0
                                                  Note: This field is preserved by Intel NVM update tool.

#### 6.2.8.4 MAC Address Word 1 Port 1 (0x0003)

Port 1 MAC Address Word 1.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 1 Port 1      0xFFFF   MAC Address Word 1 Port 1
                                                  Note: This field is preserved by Intel NVM update tool.

274                                                                                                            333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.8.5 MAC Address Word 2 Port 1 (0x0004)

Port 1 MAC Address Word 2.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 2 Port 1      0xFFFF   MAC Address Word 2 Port 1
                                                  Note: This field is preserved by Intel NVM update tool.

#### 6.2.8.6 MAC Address Word 3 Port 1 (0x0005)

Port 1 MAC Address Word 3.

 Bit(s)          Field Name             Default                                  Description

  15:0    MAC Address Word 3 Port 1      0xFFFF   MAC Address Word 3 Port 1
                                                  Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                  275
                                      Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                  Non-Volatile Memory Map

### 6.2.9 FCoE Scratch Pad Header Section

Table 6-15. FCoE Scratch Pad Header Section Summary Table
                                                                                                                     Section
 Word Offset                                              Description
                                                                                                                     Number

0x0000           FCoE Scratch Pad Pointer                                                                            6.2.9.1

0x0001           FCoE Scratch Pad Size                                                                               6.2.9.2

#### 6.2.9.1 FCoE Scratch Pad Pointer (0x0000)

The address is in 4 KB sector index units.

 Bit(s)          Field Name          Default                                     Description

# 15 Pointer Type                   1b    Pointer Type

                                                0b = Word units.
                                                1b = 4 KB sector units.
  14:0    FCoE Scratch Pad Pointer       0x0   FCoE Scratch Pad Pointer
                                               Points to FCoE Scratch Pad Section. For FCoE Scratch Pad inner structure, see
                                               Section 6.2.29.

#### 6.2.9.2 FCoE Scratch Pad Size (0x0001)

Size of scratch pad (in 4 KB resolution).

 Bit(s)    Field Name      Default                                         Description

  15:0    Size                       Size
                                     Length in: 4 KB unit
                                      First Section -> Word: FCoE Scratch Pad -> Reserved
                                      Last Section -> Word: FCoE Scratch Pad -> Reserved

276                                                                                                                 333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.10 Active SAN MAC Address Section

Table 6-16. Active SAN MAC Address Section Summary Table
                                                                                                  Section
 Word Offset                                            Description
                                                                                                  Number

0x0000          SAN MAC Address Word 0 Port 0                                                     6.2.10.1

0x0001          SAN MAC Address Word 1 Port 0                                                     6.2.10.2

0x0002          SAN MAC Address Word 2 Port 0                                                     6.2.10.3

0x0003          SAN MAC Address Word 0 Port 1                                                     6.2.10.4

0x0004          SAN MAC Address Word 1 Port 1                                                     6.2.10.5

0x0005          SAN MAC Address Word 2 Port 1                                                     6.2.10.6

#### 6.2.10.1 SAN MAC Address Word 0 Port 0 (0x0000)

 Bit(s)      Field Name       Default                                       Description

  15:0    SAN MAC Address     0xFFFF    SAN MAC Address Word 0 Port 0
          Word 0 Port 0                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.10.2 SAN MAC Address Word 1 Port 0 (0x0001)

 Bit(s)      Field Name       Default                                       Description

  15:0    SAN MAC Address     0xFFFF    SAN MAC Address Word 1 Port 0
          Word 1 Port 0                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.10.3 SAN MAC Address Word 2 Port 0 (0x0002)

 Bit(s)      Field Name       Default                                       Description

  15:0    SAN MAC Address     0xFFFF    SAN MAC Address Word 2 Port 0
          Word 2 Port 0                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.10.4 SAN MAC Address Word 0 Port 1 (0x0003)

 Bit(s)      Field Name       Default                                       Description

  15:0    SAN MAC Address     0xFFFF    SAN MAC Address Word 0 Port 1
          Word 0 Port 1                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.10.5 SAN MAC Address Word 1 Port 1 (0x0004)

 Bit(s)      Field Name       Default                                       Description

  15:0    SAN MAC Address     0xFFFF    SAN MAC Address Word 1 Port 1
          Word 1 Port 1                 Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                               277
                                  Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                              Non-Volatile Memory Map

#### 6.2.10.6 SAN MAC Address Word 2 Port 1 (0x0005)

 Bit(s)      Field Name     Default                                       Description

  15:0    SAN MAC Address   0xFFFF    SAN MAC Address Word 2 Port 1
          Word 2 Port 1               Note: This field is preserved by Intel NVM update tool.

278                                                                                                        333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.11 Alternate SAN MAC Address Section

Table 6-17. Alternate SAN MAC Address Section Summary Table
                                                                                                                      Section
 Word Offset                                               Description
                                                                                                                      Number

0x0000           Capabilities                                                                                         6.2.11.1

0x0001           Alternate SAN MAC Address 1, Lower Word - Port 0                                                     6.2.11.2

0x0002           Alternate SAN MAC Address 1, Middle Word - Port 0                                                    6.2.11.3

0x0003           Alternate SAN MAC Address 1, Upper Word - Port 0                                                     6.2.11.4

0x0004           Alternate SAN MAC Address 2, Lower Word - Port 1                                                     6.2.11.5

0x0005           Alternate SAN MAC Address 2, Middle Word - Port 1                                                    6.2.11.6

0x0006           Alternate SAN MAC Address 2, Upper Word - Port 1                                                     6.2.11.7

0x0007           Alternate WWNN Prefix                                                                                6.2.11.8

0x0008           Alternate WWPN Prefix                                                                                6.2.11.9

#### 6.2.11.1 Capabilities (0x0000)

 Bit(s)         Field Name        Default                                       Description

  15:2    Capabilities               0x0      Capabilities
                                              Note: This field is preserved by Intel NVM update tool.

# 1 Alternate WWNN Base        1b       Alternate WWNN Base

                                              Alternate WWNN base address (0x7) is available and can be written to.
                                              Note: This field is preserved by Intel NVM update tool.
   0      <New Field>                1b       <New Field>
                                              Alternate SAN MAC Address words (0x1-0x6) are available and can be written to.
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.2 Alternate SAN MAC Address 1, Lower Word - Port

                         (0x0001)

 Bit(s)            Field Name              Default                                  Description

  15:0    Alternate SAN MAC Address 1,     0xFFFF    Alternate SAN MAC Address 1, Lower Word (Port 0)
          Lower Word (Port 0)                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.3 Alternate SAN MAC Address 1, Middle Word - Port

                         (0x0002)

 Bit(s)            Field Name              Default                                  Description

  15:0    Alternate SAN MAC Address 1,     0xFFFF    Alternate SAN MAC Address 1, Middle Word (Port 0)
          Middle Word (Port 0)                       Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                     279
                                     Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                 Non-Volatile Memory Map

#### 6.2.11.4 Alternate SAN MAC Address 1, Upper Word - Port

                       (0x0003)

 Bit(s)           Field Name             Default                                 Description

  15:0    Alternate SAN MAC Address 1,   0xFFFF    Alternate SAN MAC Address 1, Upper Word (Port 0)
          Upper Word (Port 0)                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.5 Alternate SAN MAC Address 2, Lower Word - Port

                       (0x0004)

 Bit(s)           Field Name             Default                                 Description

  15:0    Alternate SAN MAC Address 2,   0xFFFF    Alternate SAN MAC Address 2, Lower Word (Port 1)
          Lower Word (Port 1)                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.6 Alternate SAN MAC Address 2, Middle Word - Port

                       (0x0005)

 Bit(s)           Field Name             Default                                 Description

  15:0    Alternate SAN MAC Address 2,   0xFFFF    Alternate SAN MAC Address 2, Middle Word (Port 1)
          Middle Word (Port 1)                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.7 Alternate SAN MAC Address 2, Upper Word - Port

                       (0x0006)

 Bit(s)           Field Name             Default                                 Description

  15:0    Alternate SAN MAC Address 2,   0xFFFF    Alternate SAN MAC Address 2, Upper Word (Port 1)
          Upper Word (Port 1)                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.8 Alternate WWNN Prefix (0x0007)

 Bit(s)         Field Name          Default                                    Description

  15:0    Alternate WWNN Base        0xFFFF   Alternate WWNN Base Address (Port 0)
          Address (Port 0)                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.11.9 Alternate WWPN Prefix (0x0008)

 Bit(s)         Field Name          Default                                    Description

  15:0    Alternate WWNN Base        0xFFFF   Alternate WWNN Base Address (Port 1)
          Address (Port 1)                    Note: This field is preserved by Intel NVM update tool.

280                                                                                                           333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.12 Boot Configuration Block Section

Contains the required setup to be used for the boot operations.

Table 6-18. Boot Configuration Block Section Summary Table
                                                                                      Section
     Word Offset                                             Description
                                                                                      Number

0x0000                   Boot Signature                                               6.2.12.1

0x0001                   Block Size                                                   6.2.12.2

0x0002                   Structure Version                                            6.2.12.3

0x0003                   iSCSI Initiator Name                                         6.2.12.4

0x0083                   Combo Image Version High                                     6.2.12.5

0x0084                   Combo Image Version Low                                      6.2.12.6

0x0085 + 1*n, n=0...14   Reserved                                                     6.2.12.7

0x0094                   iSCSI Flags                                                  6.2.12.8

0x0095 + 1*n, n=0...1    iSCSI Initiator IP                                           6.2.12.9

0x0097 + 1*n, n=0...1    Subnet Mask                                                  6.2.12.10

0x0099 + 1*n, n=0...1    Gateway IP                                                   6.2.12.11

0x009B                   iSCSI Boot LUN                                               6.2.12.12

0x009C + 1*n, n=0...1    iSCSI Target IP                                              6.2.12.13

0x009E                   iSCSI Target Port                                            6.2.12.14

0x009F                   iSCSI Target Name                                            6.2.12.15

0x011F                   CHAP Password                                                6.2.12.16

0x0128                   CHAP User Name                                               6.2.12.17

0x0168                   VLAN ID                                                      6.2.12.18

0x0169                   Mutual CHAP Password                                         6.2.12.19

0x0172                   FCoE Flags                                                   6.2.12.20

0x0173 + 1*n, n=0...2    Reserved                                                     6.2.12.21

0x0176                   Target Worldwide Port Name - WWPN                            6.2.12.22

0x017A                   Boot LUN                                                     6.2.12.23

0x017B                   VLAN ID                                                      6.2.12.24

0x017C                   Target Boot Order                                            6.2.12.25

0x017D                   Reserved                                                     6.2.12.26

0x017E                   Target Worldwide Port Name - WWPN                            6.2.12.27

0x0182                   Boot LUN                                                     6.2.12.28

0x0183                   VLAN ID                                                      6.2.12.29

0x0184                   Target Boot Order                                            6.2.12.30

0x0185                   Reserved                                                     6.2.12.31

0x0186                   Target Worldwide Port Name - WWPN                            6.2.12.32

0x018A                   Boot LUN                                                     6.2.12.33

0x018B                   VLAN ID                                                      6.2.12.34

333369-009                                                                                   281
                                      Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                             Non-Volatile Memory Map

Table 6-18. Boot Configuration Block Section Summary Table [continued]
                                                                                                          Section
      Word Offset                                            Description
                                                                                                          Number

0x018C                   Target Boot Order                                                                6.2.12.35

0x018D                   Reserved                                                                         6.2.12.36

0x018E                   Target Worldwide Port Name - WWPN                                                6.2.12.37

0x0192                   Boot LUN                                                                         6.2.12.38

0x0193                   VLAN ID                                                                          6.2.12.39

0x0194                   Target Boot Order                                                                6.2.12.40

0x0195 + 1*n, n=0...44   Reserved                                                                         6.2.12.41

0x01C2                   iSCSI Flags                                                                      6.2.12.42

0x01C3 + 1*n, n=0...1    iSCSI Initiator IP                                                               6.2.12.43

0x01C5 + 1*n, n=0...1    Subnet Mask                                                                      6.2.12.44

0x01C7 + 1*n, n=0...1    Gateway IP                                                                       6.2.12.45

0x01C9                   iSCSI Boot LUN                                                                   6.2.12.46

0x01CA + 1*n, n=0...1    iSCSI Target IP                                                                  6.2.12.47

0x01CC                   iSCSI Target Port                                                                6.2.12.48

0x01CD                   iSCSI Target Name                                                                6.2.12.49

0x024D                   CHAP Password                                                                    6.2.12.50

0x0256                   CHAP User Name                                                                   6.2.12.51

0x0296                   VLAN ID                                                                          6.2.12.52

0x0297                   Mutual CHAP Password                                                             6.2.12.53

0x02A0                   FCoE Flags                                                                       6.2.12.54

0x02A1 + 1*n, n=0...2    Reserved                                                                         6.2.12.55

0x02A4                   Target Worldwide Port Name - WWPN                                                6.2.12.56

0x02A8                   Boot LUN                                                                         6.2.12.57

0x02A9                   VLAN ID                                                                          6.2.12.58

0x02AA                   Target Boot Order                                                                6.2.12.59

0x02AB                   Reserved                                                                         6.2.12.60

0x02AC                   Target Worldwide Port Name - WWPN                                                6.2.12.61

0x02B0                   Boot LUN                                                                         6.2.12.62

0x02B1                   VLAN ID                                                                          6.2.12.63

0x02B2                   Target Boot Order                                                                6.2.12.64

0x02B3                   Reserved                                                                         6.2.12.65

0x02B4                   Target Worldwide Port Name - WWPN                                                6.2.12.66

0x02B8                   Boot LUN                                                                         6.2.12.67

0x02B9                   VLAN ID                                                                          6.2.12.68

0x02BA                   Target Boot Order                                                                6.2.12.69

0x02BB                   Reserved                                                                         6.2.12.70

0x02BC                   Target Worldwide Port Name - WWPN                                                6.2.12.71

282                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-18. Boot Configuration Block Section Summary Table [continued]
                                                                                                              Section
        Word Offset                                                Description
                                                                                                              Number

0x02C0                      Boot LUN                                                                          6.2.12.72

0x02C1                      VLAN ID                                                                           6.2.12.73

0x02C2                      Target Boot Order                                                                 6.2.12.74

0x02C3 + 1*n, n=0...44      Reserved                                                                          6.2.12.75

#### 6.2.12.1 Boot Signature (0x0000)

 Bit(s)      Field Name          Default                                          Description

  15:0     Boot Signature        0x5369     Boot Signature
                                            'i', 'S' (0x5369)
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.2 Block Size (0x0001)

 Bit(s)     Field Name         Default                                           Description

  15:0     Block Size                    Block Size
                                         Length in: 1 Byte unit
                                          First Section -> Word: Boot Configuration Block -> Boot Signature
                                          Last Section -> Word: Boot Configuration Block -> Reserved
                                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.3 Structure Version (0x0002)

 Bit(s)      Field Name          Default                                          Description

  15:8     Reserved               0x00      Reserved.
                                            Note: This field is preserved by Intel NVM update tool.
  7:0      Structure Version      0x01      Structure Version
                                            Version of this structure. Should be set to 1b.
                                            Note: This field is preserved by Intel NVM update tool.

6.2.12.4                 iSCSI Initiator Name (0x0003)
Raw data module length: 128 words
iSCSI initiator name.
This field is optional and built by manual input, DHCP host name, or with MAC Address.
Note:        This word is preserved by Intel NVM update tool.

333369-009                                                                                                           283
                                          Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

#### 6.2.12.5 Combo Image Version High (0x0083)

 Bit(s)    Field Name      Default                                            Description

  15:8    Major                 0x0     Major
                                        Combo image Major version.
                                        Note: This field is preserved by Intel NVM update tool.
  7:0     Build                 0x0     Build
                                        Combo image Build number high (bits 15:8).
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.6 Combo Image Version Low (0x0084)

 Bit(s)    Field Name      Default                                            Description

  15:8    Build                 0x0     Build
                                        Combo image Build number low (bits 7:0).
                                        Note: This field is preserved by Intel NVM update tool.
  7:0     Patch                 0x0     Patch
                                        Combo image Patch level.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.7 Reserved[n] (0x0085 + 1*n, n=0...14)

 Bit(s)    Field Name      Default                                            Description

  15:0    Reserved              0x0     Reserved for future use, should be set to zero.
                                        Note: This field is preserved by Intel NVM update tool.

6.2.12.8                 iSCSI Flags (0x0094)

 Bit(s)       Field Name          Default                                        Description

 15:10    ARP Timeout                 0xF    ARP Timeout
                                             Timeout value for each try.
                                             Note: This field is preserved by Intel NVM update tool.
  9:8     ARP Retries                 01b    ARP Retries
                                             Retry value.
                                             Note: This field is preserved by Intel NVM update tool.
  7:6     Reserved                    00b    Reserved.
                                             Note: This field is preserved by Intel NVM update tool.
  5:4     Ctrl-D Entry                00b    Ctrl-D Entry
                                              00b = Enabled
                                              11b = Disabled — Skip Ctrl-D entry.
                                              All other values are reserved.
                                             Note: This field is preserved by Intel NVM update tool.
  3:2     Authentication Type         00b    Authentication Type
                                              00b = None
                                              01b = One Way CHAP
                                              10b = Mutual CHAP
                                              11b = Reserved
                                             Note: This field is preserved by Intel NVM update tool.

284                                                                                                               333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name       Default                                         Description

# 1 Enable DHCP for        1b      Enable DHCP for iSCSI Target

          iSCSI Target                   Enable DHCP for getting iSCSI target information.
                                          0b = Disabled — Use static target configuration.
                                          1b = Enabled — Use DHCP to get target information by the Option 17 Root Path.
                                         Note: This field is preserved by Intel NVM update tool.

# 0 Enable DHCP            1b      Enable DHCP

                                          0b = Disabled — Use static configurations from this structure.
                                          1b = Enabled — Overrides configurations retrieved from DHCP.
                                         Note: This field is preserved by Intel NVM update tool.

6.2.12.9                 iSCSI Initiator IP[n] (0x0095 + 1*n, n=0...1)

 Bit(s)       Field Name       Default                                         Description

  15:0    iSCSI Initiator IP    0x0      iSCSI Initiator IP
                                         Initiator DHCP flag.
                                           Not set = This field should contain the initiator IP Address.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.10 Subnet Mask[n] (0x0097 + 1*n, n=0...1)

 Bit(s)       Field Name       Default                                         Description

  15:0    iSCSI Initiator IP    0x0      iSCSI Initiator IP
                                         Initiator DHCP flag.
                                           Not set = This field should contain the subnet mask.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.11 Gateway IP[n] (0x0099 + 1*n, n=0...1)

 Bit(s)       Field Name       Default                                         Description

  15:0    iSCSI Initiator IP    0x0      iSCSI Initiator IP
                                         Initiator DHCP flag.
                                           Not set = This field should contain the gateway IP Address.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

6.2.12.12                iSCSI Boot LUN (0x009B)

 Bit(s)       Field Name       Default                                         Description

  15:0    iSCSI Boot LUN        0x0      iSCSI Boot LUN
                                         Target DHCP flag.
                                           Not set = iSCSI target LUN number should be specified.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                285
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                  Non-Volatile Memory Map

6.2.12.13                iSCSI Target IP[n] (0x009C + 1*n, n=0...1)

 Bit(s)       Field Name       Default                                        Description

  15:0    iSCSI Initiator IP    0x0      iSCSI Initiator IP
                                         Target DHCP flag.
                                           Not set = IP Address of iSCSI target.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

6.2.12.14                iSCSI Target Port (0x009E)

 Bit(s)       Field Name       Default                                        Description

  15:0    iSCSI Target Port    0x0CBC    iSCSI Target Port
                                         Target DHCP flag.
                                           Not set = TCP port used by iSCSI target. Default is 3260.
                                           Set =     This field is ignored.
                                         Note: This field is preserved by Intel NVM update tool.

6.2.12.15                iSCSI Target Name (0x009F)
Raw data module length: 128 words
Target DHCP flag.
      Not set = iSCSI target name should be specified.
      Set = This field is ignored.
Note:       This word is preserved by Intel NVM update tool.

#### 6.2.12.16 CHAP Password (0x011F)

Raw data module length: 9 words
The minimum CHAP secret must be 12 octets and maximum CHAP secret size is 16. The last 2 bytes are
null alignment padding.
Note:       This word is preserved by Intel NVM update tool.

#### 6.2.12.17 CHAP User Name (0x0128)

Raw data module length: 64 words
The user name must be non-null value and maximum size of user name allowed is 127 characters.
Note:       This word is preserved by Intel NVM update tool.

286                                                                                                            333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.12.18 VLAN ID (0x0168)

 Bit(s)    Field Name      Default                                              Description

  15:0    VLAN ID               0x0     VLAN ID
                                        Reserved area since the function is disabled due to Microsoft restrictions. VLAN ID to include
                                        the tag in iSCSI boot frames. A valid VLAN ID is between 1 and 4094. Zero means no VLAN
                                        tag support.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.19 Mutual CHAP Password (0x0169)

Raw data module length: 9 words
The minimum mutual CHAP secret must be 12 octets and maximum mutual CHAP secret size is 16. The
last 2 bytes are null alignment padding.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.20 FCoE Flags (0x0172)

 Bit(s)       Field Name          Default                                          Description

  15:2    Reserved                    0x0    Reserved.
                                             Note: This field is preserved by Intel NVM update tool.

# 1 Disable FCoE Ctrl-D         0b     Disable FCoE Ctrl-D Menu

          Menu                                0b = Enabled — FCoE Ctrl-D menu is enabled and user can configure FCoE ports.
                                              1b = Disabled — FCoE Ctrl-D menu is disabled and user cannot configure FCoE ports.
                                             Note: This field is preserved by Intel NVM update tool.

# 0 Reserved                    0b     Reserved.

                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.21 Reserved[n] (0x0173 + 1*n, n=0...2)

 Bit(s)    Field Name      Default                                              Description

  15:0    Reserved              0x0     Reserved for future use, should be set to zero.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.22 Target Worldwide Port Name - WWPN (0x0176)

Raw data module length: 4 words
Byte string of target WWPN.
Note:        This word is preserved by Intel NVM update tool.

333369-009                                                                                                                         287
                                        Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.12.23 Boot LUN (0x017A)

 Bit(s)    Field Name      Default                                          Description

  15:0    Target LUN          0x0     Target LUN
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.24 VLAN ID (0x017B)

 Bit(s)    Field Name      Default                                          Description

  15:0    VLAN ID             0x0     VLAN ID
                                      VLAN ID for the Port. Default is 0.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.25 Target Boot Order (0x017C)

 Bit(s)       Field Name        Default                                        Description

  15:8    Reserved                  0x0    Reserved for future use, should be set to zero.
                                           Note: This field is preserved by Intel NVM update tool.
  7:0     Target Boot Order         0x0    Target Boot Order
                                           Valid range is 0-4, with 0 meaning no boot order.
                                           Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.26 Reserved (0x017D)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved            0x0     Reserved.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.27 Target Worldwide Port Name - WWPN (0x017E)

Raw data module length: 4 words
Byte string of target WWPN.
Note:      This word is preserved by Intel NVM update tool.

#### 6.2.12.28 Boot LUN (0x0182)

 Bit(s)    Field Name      Default                                          Description

  15:0    Target LUN          0x0     Target LUN
                                      Note: This field is preserved by Intel NVM update tool.

288                                                                                                             333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.12.29 VLAN ID (0x0183)

 Bit(s)    Field Name       Default                                         Description

  15:0    VLAN ID             0x0     VLAN ID
                                      VLAN ID for the Port. Default is 0.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.30 Target Boot Order (0x0184)

 Bit(s)        Field Name       Default                                        Description

  15:8    Reserved                  0x0    Reserved for future use, should be set to zero.
                                           Note: This field is preserved by Intel NVM update tool.
  7:0     Target Boot Order         0x0    Target Boot Order
                                           Valid range is 0-4, with 0 meaning no boot order.
                                           Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.31 Reserved (0x0185)

 Bit(s)    Field Name       Default                                         Description

  15:0    Reserved            0x0     Reserved.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.32 Target Worldwide Port Name - WWPN (0x0186)

Raw data module length: 4 words
Byte string of target WWPN.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.33 Boot LUN (0x018A)

 Bit(s)      Field Name     Default                                         Description

  15:0    Target LUN          0x0     Target LUN
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.34 VLAN ID (0x018B)

 Bit(s)      Field Name     Default                                         Description

  15:0    VLAN ID             0x0     VLAN ID
                                      VLAN ID for the Port. Default is 0.
                                      Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                           289
                                      Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.12.35 Target Boot Order (0x018C)

 Bit(s)       Field Name        Default                                        Description

  15:8    Reserved                  0x0    Reserved for future use, should be set to zero.
                                           Note: This field is preserved by Intel NVM update tool.
  7:0     Target Boot Order         0x0    Target Boot Order
                                           Valid range is 0-4, with 0 meaning no boot order.
                                           Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.36 Reserved (0x018D)

 Bit(s)    Field Name      Default                                          Description

  15:0    Reserved            0x0     Reserved.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.37 Target Worldwide Port Name - WWPN (0x018E)

Raw data module length: 4 words
Byte string of target WWPN.
Note:      This word is preserved by Intel NVM update tool.

#### 6.2.12.38 Boot LUN (0x0192)

 Bit(s)    Field Name      Default                                          Description

  15:0    Target LUN          0x0     Target LUN
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.39 VLAN ID (0x0193)

 Bit(s)    Field Name      Default                                          Description

  15:0    VLAN ID             0x0     VLAN ID
                                      VLAN ID for the Port. Default is 0.
                                      Note: This field is preserved by Intel NVM update tool.

#### 6.2.12.40 Target Boot Order (0x0194)

 Bit(s)       Field Name        Default                                        Description

  15:8    Reserved                  0x0    Reserved for future use, should be set to zero.
                                           Note: This field is preserved by Intel NVM update tool.
  7:0     Target Boot Order         0x0    Target Boot Order
                                           Valid range is 0-4, with 0 meaning no boot order.
                                           Note: This field is preserved by Intel NVM update tool.

290                                                                                                             333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.12.41 Reserved[n] (0x0195 + 1*n, n=0...44)

 Bit(s)    Field Name    Default                                         Description

  15:0    Reserved        0x0      Reserved.
                                   Note: This field is preserved by Intel NVM update tool.

6.2.12.42               iSCSI Flags (0x01C2)
For inner structure, see Section 6.2.12.8.
Note:        This word is preserved by Intel NVM update tool.

6.2.12.43               iSCSI Initiator IP[n] (0x01C3 + 1*n, n=0...1)
For inner structure, see Section 6.2.12.9.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.44 Subnet Mask[n] (0x01C5 + 1*n, n=0...1)

For inner structure, see Section 6.2.12.10.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.45 Gateway IP[n] (0x01C7 + 1*n, n=0...1)

For inner structure, see Section 6.2.12.11.
Note:        This word is preserved by Intel NVM update tool.

6.2.12.46               iSCSI Boot LUN (0x01C9)

For inner structure, see Section 6.2.12.12.
Note:        This word is preserved by Intel NVM update tool.

6.2.12.47               iSCSI Target IP[n] (0x01CA + 1*n, n=0...1)
For inner structure, see Section 6.2.12.13.
Note:        This word is preserved by Intel NVM update tool.

6.2.12.48               iSCSI Target Port (0x01CC)
For inner structure, see Section 6.2.12.14.
Note:        This word is preserved by Intel NVM update tool.

333369-009                                                                                   291
                                   Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                     Non-Volatile Memory Map

6.2.12.49           iSCSI Target Name (0x01CD)
For inner structure, see Section 6.2.12.15.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.50 CHAP Password (0x024D)

For inner structure, see Section 6.2.12.16.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.51 CHAP User Name (0x0256)

For inner structure, see Section 6.2.12.17.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.52 VLAN ID (0x0296)

For inner structure, see Section 6.2.12.18.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.53 Mutual CHAP Password (0x0297)

For inner structure, see Section 6.2.12.19.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.54 FCoE Flags (0x02A0)

For inner structure, see Section 6.2.12.20.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.55 Reserved[n] (0x02A1 + 1*n, n=0...2)

For inner structure, see Section 6.2.12.21.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.56 Target Worldwide Port Name - WWPN (0x02A4)

For inner structure, see Section 6.2.12.22.
Note:     This word is preserved by Intel NVM update tool.

292                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.12.57 Boot LUN (0x02A8)

For inner structure, see Section 6.2.12.23.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.58 VLAN ID (0x02A9)

For inner structure, see Section 6.2.12.24.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.59 Target Boot Order (0x02AA)

For inner structure, see Section 6.2.12.25.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.60 Reserved (0x02AB)

For inner structure, see Section 6.2.12.26.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.61 Target Worldwide Port Name - WWPN (0x02AC)

For inner structure, see Section 6.2.12.27.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.62 Boot LUN (0x02B0)

For inner structure, see Section 6.2.12.28.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.63 VLAN ID (0x02B1)

For inner structure, see Section 6.2.12.29.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.64 Target Boot Order (0x02B2)

For inner structure, see Section 6.2.12.30.
Note:        This word is preserved by Intel NVM update tool.

333369-009                                                                       293
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                     Non-Volatile Memory Map

#### 6.2.12.65 Reserved (0x02B3)

For inner structure, see Section 6.2.12.31.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.66 Target Worldwide Port Name - WWPN (0x02B4)

For inner structure, see Section 6.2.12.32.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.67 Boot LUN (0x02B8)

For inner structure, see Section 6.2.12.33.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.68 VLAN ID (0x02B9)

For inner structure, see Section 6.2.12.34.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.69 Target Boot Order (0x02BA)

For inner structure, see Section 6.2.12.35.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.70 Reserved (0x02BB)

For inner structure, see Section 6.2.12.36.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.71 Target Worldwide Port Name - WWPN (0x02BC)

For inner structure, see Section 6.2.12.37.
Note:     This word is preserved by Intel NVM update tool.

#### 6.2.12.72 Boot LUN (0x02C0)

For inner structure, see Section 6.2.12.38.
Note:     This word is preserved by Intel NVM update tool.

294                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.12.73 VLAN ID (0x02C1)

For inner structure, see Section 6.2.12.39.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.74 Target Boot Order (0x02C2)

For inner structure, see Section 6.2.12.40.
Note:        This word is preserved by Intel NVM update tool.

#### 6.2.12.75 Reserved[n] (0x02C3 + 1*n, n=0...44)

For inner structure, see Section 6.2.12.41.
Note:        This word is preserved by Intel NVM update tool.

333369-009                                                                       295
                                 Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                        Non-Volatile Memory Map

### 6.2.13 Firmware Module Header Section

Table 6-19. Firmware Module Header Section Summary Table
                                                                                                                           Section
  Word Offset                                                    Description
                                                                                                                           Number

0x0000              Section Header                                                                                         6.2.13.1

0x0001              Test Configuration Pointer                                                                             6.2.13.2

0x0002              Common Firmware Parameters Pointer                                                                     6.2.13.3

0x0003              Pass-Through LAN 0 Configuration Pointer                                                               6.2.13.4

0x0004              Sideband Configuration Pointer                                                                         6.2.13.5

0x0005              Flexible TCO Filter Configuration Pointer                                                              6.2.13.6

0x0006              Pass-Through LAN 1 Configuration Pointer                                                               6.2.13.7

0x0007              OEM Support Structure Pointer                                                                          6.2.13.8

0x0008              LESM Configuration Pointer                                                                             6.2.13.9

0x0009 - 0x000A     Reserved                                                                                              6.2.13.10

0x000B              Section Footer                                                                                        6.2.13.11

#### 6.2.13.1 Section Header (0x0000)

 Bit(s)    Field Name      Default                                               Description

  15:0    Block Length                  Block Length
                                        Length in words of the section covered by CRC.

#### 6.2.13.2 Test Configuration Pointer (0x0001)

 Bit(s)       Field Name          Default                                           Description

  15:0    Test Configuration         0x0       Test Configuration Pointer
          Pointer                              Points to Test Configuration Module Section. For Test Configuration Module inner
                                               structure, see Section 6.2.15.

#### 6.2.13.3 Common Firmware Parameters Pointer (0x0002)

 Bit(s)       Field Name          Default                                           Description

  15:0    Common Firmware            0x0       Common Firmware Parameters Pointer
          Parameters Pointer                   Points to Common Firmware Parameters Module Section. For Common Firmware
                                               Parameters Module inner structure, see Section 6.2.16.

#### 6.2.13.4 Pass-Through LAN 0 Configuration Pointer (0x0003)

 Bit(s)       Field Name             Default                                        Description

  15:0    Pass Through LAN 0          0x0       Pass-Through LAN 0 Configuration Pointer
          Configuration Pointer                 Points to Pass Through Control Words Section. For Pass Through Control Words inner
                                                structure, see Section 6.2.18.

296                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.13.5 Sideband Configuration Pointer (0x0004)

This module is long by 28 bytes and must be mapped in the first valid 4 KB sector of the Flash.

 Bit(s)        Field Name            Default                                         Description

  15:0    Sideband Configuration       0x0      Sideband Configuration Pointer
          Pointer                               Points to Sideband Configuration Structure Section. For Sideband Configuration
                                                Structure inner structure, see Section 6.2.17.

#### 6.2.13.6 Flexible TCO Filter Configuration Pointer (0x0005)

This section loads all of the flexible filters, The control + mask + filter data are repeatable as the
number of filters. Section length in offset 0 is for all filters.

 Bit(s)       Field Name            Default                                         Description

  15:0    Flexible TCO Filter         0x0      Flexible TCO Filter Configuration Pointer
          Configuration Pointer                Points to Flexible TCO Filter Configuration Structure Section. For Flexible TCO Filter
                                               Configuration Structure inner structure, see Section 6.2.19.

#### 6.2.13.7 Pass-Through LAN 1 Configuration Pointer (0x0006)

 Bit(s)       Field Name            Default                                         Description

  15:0    Pass Through LAN 1          0x0      Pass Through LAN 1 Configuration Pointer
          Configuration Pointer                Points to Pass Through Control Words Section. For Pass Through Control Words inner
                                               structure, see Section 6.2.18.

#### 6.2.13.8 OEM Support Structure Pointer (0x0007)

 Bit(s)        Field Name            Default                                         Description

  15:0    OEM Support Structure        0x0      OEM Support Structure Pointer
          Pointer

#### 6.2.13.9 LESM Configuration Pointer (0x0008)

 Bit(s)       Field Name           Default                                          Description

  15:0    LESM Configuration        0x0       LESM Configuration Pointer
          Pointer                             Points to LESM Configurations (not in SGVL) Section. For LESM Configurations (not in
                                              SGVL) inner structure, see Section 6.2.20.

#### 6.2.13.10 Reserved (0x0009 - 0x000A)

333369-009                                                                                                                          297
                                       Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                              Non-Volatile Memory Map

#### 6.2.13.11 Section Footer (0x000B)

 Bit(s)    Field Name    Default                                       Description

  15:8    Block CRC8               Block CRC8
                                   CRC-8-CCITT:
                                    Start Section -> Word: Firmware Module Header -> Section Header
                                    End Section -> Word: Firmware Module Header -> OEM HP Support Structure Pointer
  7:0     Reserved        0x0      Reserved. Block length in words.

298                                                                                                          333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.14 Firmware Header Reserved Word Section

Placeholder to make header offsets following be the same in BDX/MGPK (they have LESM, one word
longer Firmware module header).

Table 6-20. Firmware Header Reserved Word Section Summary Table
                                                                                        Section
 Word Offset                                           Description
                                                                                        Number

0x0000          Reserved                                                                6.2.14.1

#### 6.2.14.1 Reserved (0x0000)

 Bit(s)    Field Name      Default                                    Description

  15:0    Reserved          0x0      Reserved.

333369-009                                                                                       299
                                     Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                  Non-Volatile Memory Map

### 6.2.15 Test Configuration Module Section

Table 6-21. Test Configuration Module Section Summary Table
                                                                                                               Section
 Word Offset                                               Description
                                                                                                               Number

0x0000          Section Header                                                                                  6.2.15.1

0x0001          Reserved                                                                                        6.2.15.2

0x0002          Miscellaneous                                                                                   6.2.15.3

0x0003          Section Footer                                                                                  6.2.15.4

#### 6.2.15.1 Section Header (0x0000)

 Bit(s)    Field Name      Default                                         Description

  15:0    Block Length               Block Length
                                     Length in words of the section covered by CRC.
                                     Block length in words.

#### 6.2.15.2 Reserved (0x0001)

#### 6.2.15.3 Miscellaneous (0x0002)

 Bit(s)        Field Name            Default                                    Description

  15:0    Reserved                    0x0      Reserved.

#### 6.2.15.4 Section Footer (0x0003)

 Bit(s)    Field Name      Default                                         Description

  15:8    Block CRC                  Block CRC
                                     CRC-8-CCITT:
                                      Start Section -> Word: Test Configuration Module -> Section Header
                                      En Section -> Word: Test Configuration Module -> Miscellaneous
  7:0     Reserved          0x0      Reserved. Block length in words.

300                                                                                                            333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.16 Common Firmware Parameters Module Section

Table 6-22. Common Firmware Parameters Module Section Summary Table
                                                                                                            Section
 Word Offset                                                   Description
                                                                                                            Number

0x0000           Section Header                                                                             6.2.16.1

0x0001           Common Firmware Parameters 1                                                               6.2.16.2

0x0002           Common Firmware Parameters 2                                                               6.2.16.3

0x0003           Section Footer                                                                             6.2.16.4

#### 6.2.16.1 Section Header (0x0000)

 Bit(s)    Field Name         Default                                           Description

  15:0    Block Length                   Block Length
                                         Length in words of the section covered by CRC.
                                         Block length in words.
                                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.16.2 Common Firmware Parameters 1 (0x0001)

 Bit(s)        Field Name               Default                                     Description

# 15 Enable Firmware Reset           1b      Enable Firmware Reset

                                                   0b = Disabled
                                                   1b = Enabled
                                                  Note: This field is preserved by Intel NVM update tool.
 14:13    Redirection Sideband           00b      Redirection Sideband Interface
          Interface                                00b = SMBus
                                                   01b = NC-SI
                                                   10b = PT Disable
                                                   11b = MCTP (over PCIe and SMBus)
                                                  Note: This field is preserved by Intel NVM update tool.

# 12 Restore MAC Address             1b      Restore MAC Address

                                                   0b = Do not restore MAC Address at power-on.
                                                   1b = Restore MAC Address at power-on.
                                                  Note: This field is preserved by Intel NVM update tool.

# 11 Reserved                        1b      Reserved.

  10:8    Manageability Pass             010b     Manageability Pass-Through Mode
          Through Mode                            000b = None
                                                  010b = Pass Through (PT) Mode
                                                  All other values are reserved.
                                                  Note: This field is preserved by Intel NVM update tool.
  7:6     Control Interface              00b      Control Interface
                                                   00b = None
                                                   01b = MCTP over SMBus only
                                                   10b = MCTP over PCIe only
                                                   11b = MCTP over PCIe or SMBus
                                                  Note: This field is preserved by Intel NVM update tool.
  5:3     Reserved                       111b     Reserved.

333369-009                                                                                                         301
                                         Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                             Non-Volatile Memory Map

 Bit(s)        Field Name     Default                                     Description

# 2 OS2BMC Capable        0b      OS2BMC Capable

                                         0b = Disabled
                                         1b = Enabled
                                        Note: This field is preserved by Intel NVM update tool.

# 1 LAN1 TCO Isolate      1b      LAN1 TCO Isolate Disable

          Disable                        0b = Enabled
                                         1b = Disabled
                                        Note: This field is preserved by Intel NVM update tool.

# 0 LAN0 TCO Isolate      1b      LAN0 TCO Isolate Disable

          Disable                        0b = Enabled
                                         1b = Disabled
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.16.3 Common Firmware Parameters 2 (0x0002)

 Bit(s)        Field Name     Default                                     Description

 15:13    Reserved             000b     Reserved.

# 12 Reserved              0b      Reserved.

# 11 Multi-Drop NC-SI      1b      Multi-Drop NC-SI Topology

                                        When this bit is set, the NCSI_CRS_DV and NCSI_RXD[1:0] pins are High-Z
                                        following power-up. Otherwise, the pins are driven.
                                          0b = Point-to-Point
                                          1b = Multi-drop (default)
                                        Note: This field is preserved by Intel NVM update tool.

# 10 Proxying Capable      0b      Proxying Capable

                                         0b = Disable Protocol Offload.
                                         1b = Enable Protocol Offload.
                                        Note: This field is preserved by Intel NVM update tool.

# 9 Reserved              0b      Reserved.

    8 PLDM Over MCTP        0b      PLDM Over MCTP

                                         0b = Disabled
                                         1b = Enabled

    7 OEM Commands Over     0b      OEM Commands Over MCTP

          MCTP                           0b = Disabled
                                         1b = Enabled

    6 NC-SI Over MCTP       0b      NC-SI Over MCTP

                                        Reserved.
                                         0b = Disabled
                                         1b = Enabled
  5:1     Semaphore Backoff    0x2      Semaphore Backoff Interval
          Interval                      Number of 10 ms ticks that firmware must wait before taking semaphore ownership
                                        again since it has released it.
                                        Note: This field is preserved by Intel NVM update tool.

# 0 Reserved              0b      Reserved.

302                                                                                                         333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.16.4 Section Footer (0x0003)

 Bit(s)    Field Name    Default                                      Description

  15:8    Block CRC                Block CRC
                                   CRC-8-CCITT:
                                    Start Section -> Word: Common Firmware Parameters Module -> Section Header
                                    End Section -> Word: Common Firmware Parameters Module -> Common Firmware
                                    Parameters 2
                                   Note: This field is preserved by Intel NVM update tool.
  7:0     Reserved        0x0      Reserved. Block length in words.

333369-009                                                                                                       303
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                    Non-Volatile Memory Map

### 6.2.17 Sideband Configuration Structure Section

Table 6-23. Sideband Configuration Structure Section Summary Table
                                                                                                                   Section
  Word Offset                                                 Description
                                                                                                                   Number

0x0000             Block Length                                                                                    6.2.17.1

0x0001             SMBus Maximum Fragment Size                                                                     6.2.17.2

0x0002             SMBus Notification Timeout and Flags                                                            6.2.17.3

0x0003             SMBus Slave Addresses                                                                           6.2.17.4

0x0004             NC-SI Configuration 1                                                                           6.2.17.5

0x0005             NC-SI Configuration 2                                                                           6.2.17.6

0x0006             NCSI Flow Control XOFF                                                                          6.2.17.7

0x0007             NCSI Flow Control XON                                                                           6.2.17.8

0x0008             NC-SI HW Arbitration TOKEN Timeout                                                              6.2.17.9

0x0009 - 0x000D    Reserved                                                                                        6.2.17.10

0x000E             OEM IANA                                                                                        6.2.17.11

0x000F             NC-SI over MCTP Message Types                                                                   6.2.17.12

0x0010             NC-SI over MCTP Configuration                                                                   6.2.17.13

0x0011             Traffic Types Parameters                                                                        6.2.17.14

0x0012             MCTP Rate Limiter Config 1                                                                      6.2.17.15

0x0013             MCTP Rate Limiter Config 2                                                                      6.2.17.16

0x0014             NC-SI Channel to Port Mapping                                                                   6.2.17.17

0x0015             Block CRC8                                                                                      6.2.17.18

#### 6.2.17.1 Block Length (0x0000)

 Bit(s)    Field Name      Default                                           Description

  15:0    Block Length        0x13     Block Length
                                       Length in words of the section covered by CRC.
                                       Section length in words.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.2 SMBus Maximum Fragment Size (0x0001)

 Bit(s)     Field Name         Default                                         Description

  15:0    Fragment Size         0x20     Fragment Size
                                         SMBus Maximum Fragment Size (bytes).
                                         Supported range is between 32 and 240 bytes.
                                         Note: In MCTP mode, this value should be set to 0x45 (64 bytes payload + 5 bytes of
                                                MCTP header)
                                         Note: This field is preserved by Intel NVM update tool.

304                                                                                                               333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.17.3 SMBus Notification Timeout and Flags (0x0002)

 Bit(s)        Field Name         Default                                       Description

  15:8    SMBus Notification       0xFF      SMBus Notification Timeout (ms)
          Timeout (ms)                       Note: This field is preserved by Intel NVM update tool.
  7:6     SMBus Connection         00b       SMBus Connection Speed
          Speed                               00b = Standard SMBus connection.
                                              01b = Reserved
                                              10b = Reserved
                                              11b = Reserved
                                             Note: This field is preserved by Intel NVM update tool.

# 5 SMBus Block Read          0b       SMBus Block Read Command

          Command                             0b = Block read command is 0xC0.
                                              1b = Block read command is 0xD0.
                                             Note: This field is preserved by Intel NVM update tool.

# 4 Reserved                  1b       Reserved. Must be 1b.

                                              0b = Single address mode.
                                              1b = Dual address mode.

# 3 Reserved                  0b       Reserved.

# 2 Disable SMBus ARP         0b       Disable SMBus ARP Functionality

          Functionality                      Note: This field is preserved by Intel NVM update tool.

# 1 SMBus ARP PEC             1b       SMBus ARP PEC

                                             SMBus Transactions PEC. Should be set.
                                              0b = Disable SMBus ARP PEC.
                                              1b = Enable SMBus ARP PEC.
                                             Note: This field is preserved by Intel NVM update tool.

# 0 SMBus Transaction PEC     0b       SMBus Transactions PEC

                                             Should be set in MCTP modes.
                                              0b = 0x0 Disable PEC — If this bit is cleared, PEC is not added to master write or
                                                   slave read transactions, a slave write transaction with PEC is dropped.
                                              1b = Enable PEC — If this bit is set, PEC is added for master SMBus write
                                                   transactions. a PEC is added to slave read transactions and can be received in
                                                   slave write transaction.
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.4 SMBus Slave Addresses (0x0003)

 Bit(s)         Field Name         Default                                       Description

  15:9    SMBus 1 Slave Address     0x62      SMBus 1 Slave Address
                                              Dual address mode only.
                                              Note: This field is preserved by Intel NVM update tool.

# 8 Reserved                   0x0      Reserved.

  7:1     SMBus 0 Slave Address     0x63      SMBus 0 Slave Address
                                              Note: This field is preserved by Intel NVM update tool.

# 0 Reserved                   0x0      Reserved.

333369-009                                                                                                                    305
                                   Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.17.5 NC-SI Configuration 1 (0x0004)

 Bit(s)         Field Name            Default                                    Description

# 15 Reserved                      0b      Reserved.

 14:11    NC-SI Version                 0x0     NC-SI Version
                                                 0x0 = NCSI 1.0
                                                 0x1 = NCSI 1.1
                                                 All other values are reserved.
                                                Note: This field is preserved by Intel NVM update tool.

# 10 Flow Control                  0b      Flow Control

                                                 0b = Disable
                                                 1b = Enable
                                                Note: This field is preserved by Intel NVM update tool.

    9 RMII HW Arbitration           0b      RMII Hardware Arbitration Enable

          Enable                                Must be 0.
                                                 0b = Not supported
                                                 1b = Supported
                                                Note: This field is preserved by Intel NVM update tool.

    8 RMII HW-Based Packet          1b      RMII Hardware-Based Packet Copy Enable

          Copy Enable                            0b = Disable
                                                 1b = Enable
                                                Note: This field is preserved by Intel NVM update tool.
  7:5     Package ID                   000b     Package ID
                                                Meaningful only when bit 15 of NC-SI Configuration 2 word (offset 0x07) is
                                                cleared.
                                                Note: This field is preserved by Intel NVM update tool.
  4:0     LAN 0 Internal Channel ID     0x0     LAN 0 Internal Channel ID
                                                Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.6 NC-SI Configuration 2 (0x0005)

 Bit(s)         Field Name            Default                                    Description

# 15 Read NC-SI Package ID         0b      Read NC-SI Package ID from SDP

          from SDP                               0b = Disabled — NVM, NC-SI Configuration 1 word bits 7:5 (offset 0x06)
                                                 1b = Enabled — SDP, SDPn_0 pins of LAN ports n=1,0 (where SDP1_0, SDP0 of
                                                      LAN port 1 is the MS bit of NC-SI Package ID).
                                                Note: This field is preserved by Intel NVM update tool.

    14 NC-SI Package ID from         0b      NC-SI Package ID from SDP Workaround

          SDP Workaround                         0b = No Workaround — NC-SI Package ID should be configured according to
                                                      value of Read NC-SI Package ID from SDP field (Bit 15 of this word).
                                                 1b = SDP-SDn_0 pin of LAN port 0, where {0,0,SDP0_0} is the LS bits of NC-SI
                                                      Package ID.
  13:4    Reserved                      0x0     Reserved.

306                                                                                                                  333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)         Field Name             Default                                    Description

  3:0     Max XOFF Renewal              0x6      Max XOFF Renewal
                                                 NC-SI Flow Control MAX XOFF Renewal (# of XOFF renewals allowed).
                                                  0x0 = Disabled (unlimited allowed)
                                                  0x1 = Up to 2 consecutive
                                                  0x2 = Up to 0x3 consecutive
                                                  0x3 = Up to 0x4 consecutive
                                                  0x4 = Up to 0x5 consecutive
                                                  0x5 = Up to 0x6 consecutive
                                                  0x6 = Up to 0x7 consecutive
                                                  0x7 = Up to 0x8 consecutive
                                                  0x8 = Up to 0x9 consecutive
                                                  0x9 = Up to 0xA consecutive
                                                  0xA = Up to 0xB consecutive
                                                  0xB = Up to 0xC consecutive
                                                  0xC = Up to 0xD consecutive
                                                  0xD = Up to 0xE consecutive
                                                  0xE = Up to 0xF consecutive
                                                  0xF = Up to 0x10 consecutive
                                                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.7 NCSI Flow Control XOFF (0x0006)

 Bit(s)      Field Name      Default                                          Description

  15:0    XOFF Threshold     0xAB8      XOFF Threshold
                                        Tx buffer watermark for sending a XOFF NC-SI flow control packet in bytes. The XOFF
                                        Threshold value refers to the occupied space in the buffer.
                                        The value should be 16 bytes aligned.
                                        Notes:
                                         1. Field relevant for NC-SI operation mode only.
                                         2. To support a maximum packet size of 1.5 KB, the value programmed assuming a Tx
                                            buffer size of 8 KB value of field should be 0x12C0 (4,800 bytes).
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.8 NCSI Flow Control XON (0x0007)

 Bit(s)      Field Name      Default                                          Description

  15:0    XON Threshold      0x1340     XON Threshold
                                        Tx buffer water mark for sending a XON NC-SI flow control packet in bytes. The XON
                                        Threshold value refers to the available space in the TX buffer.
                                        The value should be 16 bytes aligned.
                                        Notes:
                                         1. Field relevant for NC-SI operation mode only.
                                         2. To support maximum packet size of 1.5 KB, the value programmed should be a
                                            positive value that equals: Buffer size - XOFF Threshold (refer to Section 6.5.5.7) +
                                            1536 bytes. Assuming a TX Buffer size is 8 KB and the XOFF Threshold is 4800 bytes
                                            value of field should be 0x1340 (4,928 bytes).
                                        Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                    307
                                      Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

#### 6.2.17.9 NC-SI HW Arbitration TOKEN Timeout (0x0008)

 Bit(s)       Field Name             Default                                        Description

  15:0    NC-SI HW Arbitration       0xA000     NC-SI Hardware Arbitration TOKEN Timeout
          TOKEN Timeout                         Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.10 Reserved (0x0009 - 0x000D)

#### 6.2.17.11 OEM IANA (0x000E)

 Bit(s)    Field Name        Default                                            Description

  15:0    OEM IANA             0x0      OEM IANA
                                        If not zero and not 0x157, the X550 will accept NC-SI OEM commands with this IANA
                                        number.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.12 NC-SI Over MCTP Message Types (0x000F)

 Bit(s)       Field Name         Default                                           Description

  15:8    NC-SI Command              0x2       NC-SI Command Packet Type
          Packet Type                          Defines the MCTP packet type used to identify NC-SI Control Packets.
                                               Note: This field is preserved by Intel NVM update tool.
  7:0     NC-SI Pass Through         0x3       NC-SI Pass Through Packet Type
          Packet Type                          Defines the MCTP packet type used to identify NC-SI Pass Through Packets.
                                               Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.13 NC-SI Over MCTP Configuration (0x0010)

 Bit(s)       Field Name         Default                                           Description

  15:8    Reserved                   0x0       Reserved.

# 7 Use Payload Type             1b      Use Payload Type

                                               If set, a payload type byte is expected in NC-SI over MCTP packets after the packet
                                               type. Otherwise, the control and pass through are controlled via the NC-SI over MCTP
                                               Message Types defined in the previous word.
                                               Note: This field is preserved by Intel NVM update tool.

# 6 Simplified MCTP              0b      Simplified MCTP

                                               If set, only SOM & EOM bits are used for the reassembly process.
                                               Relevant only in SMBus mode.
                                               Note: This field is preserved by Intel NVM update tool.

# 5 Disable ACLs                 1b      Disable ACLs

                                               If set, the ACLs on the PCIe VDMs are disabled.
                                               Note: This field is preserved by Intel NVM update tool.
  4:1     Reserved                   0x0       Reserved.

308                                                                                                                        333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                           Description

# 0 Endpoint Discovery          0b     Endpoint Discovery Route

          Route                              Use Route by ID for Endpoint Discovery responses
                                              0b = To Root Complex — Use “Route to root complex” type in outgoing messages and
                                                   “Broadcast from root complex” in incoming messages.
                                              1b = By ID — Use “Route by ID” for MCTP discovery messages.
                                             This mode should be selected only in debug mode.
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.14 Traffic Types Parameters (0x0011)

 Bit(s)       Field Name         Default                                           Description

  15:6    Reserved                    0x0    Reserved.
  5:4     Port1 Traffic Types         01b    Port1 Traffic Types
                                              00b = Reserved.
                                              01b = Network to BMC traffic only allowed through Port 1.
                                              10b = OS2BMC traffic only allowed through Port 1.
                                              11b = Both Network to BMC traffic and OS2BMC traffic allowed through Port 1.
                                             This field is valid only if the Port1 Manageability Capable field in the Common Firmware
                                             Parameters NVM word is set.
                                             Note: This field is preserved by Intel NVM update tool.
  3:2     Reserved                    00b    Reserved.
  1:0     Port 0 Traffic Types        01b    Port 0 Traffic Types
                                             00b = Reserved.
                                             01b = Network to BMC traffic only allowed through Port 0.
                                             10b = OS2BMC traffic only allowed through Port 0.
                                             11b = Both Network to BMC traffic and OS2BMC traffic allowed through Port 0.
                                             This field is valid only if the Port0 Manageability Capable field in the Common Firmware
                                             Parameters NVM word is set.
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.15 MCTP Rate Limiter Config 1 (0x0012)

 Bit(s)    Field Name       Default                                             Description

  15:0    MCTP Rate          0x2800     MCTP Rate
                                        Defines the number of cycles between accesses of the MCTP send client to the memory
                                        arbiter.
                                        Default value assumes a clock of 80 MHz and a bus width of 128 bit. This value provides a bit
                                        rate of 1 Mb/s.
                                        Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                        309
                                        Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                            Non-Volatile Memory Map

#### 6.2.17.16 MCTP Rate Limiter Config 2 (0x0013)

 Bit(s)       Field Name          Default                                              Description

# 15 Decision Point                0b        Decision Point

                                                  Defines if, when credits are available, a full MCTP message is sent or a single VDM is
                                                  sent.
                                                   0b = Per VDM
                                                   1b = Per Packet
                                                  Note: This field is preserved by Intel NVM update tool.
  14:0    MCTP Max Credits           0x5          MCTP Max Credits
                                                  Defines the maximum number of 16 bytes credit that can be accumulated. These
                                                  credits include the VDM header line (one line for each 64-byte VDM).
                                                  Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.17 NC-SI Channel to Port Mapping (0x0014)

 Bit(s)        Field Name               Default                                          Description

# 15 Table Valid                        0b     Table Valid

                                                    If set, the values below are used to define the port to channel mapping.
                                                    Note: This field is preserved by Intel NVM update tool.
  14:7    Reserved                       0x0        Reserved.
  6:5     Port 1 Channel ID              01b        Port 1 Channel ID
                                                    The Channel ID to use for port 1.
                                                    Note: This field is preserved by Intel NVM update tool.

# 4 Port 1 Channel Enable              1b     Port 1 Channel Enable

                                                     0b = Disabled
                                                     1b = Enabled
                                                    Note: This field is preserved by Intel NVM update tool.

# 3 Reserved                           0b     Reserved.

  2:1     Port 0 Channel ID              00b        Port 0 Channel ID
                                                    The Channel ID to use for port 1.
                                                    Note: This field is preserved by Intel NVM update tool.

# 0 Port 0 Channel Enable              1b     Port 0 Channel Enable

                                                     0b = Disabled
                                                     1b = Enabled
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.17.18 Block CRC8 (0x0015)

 Bit(s)    Field Name         Default                                               Description

  15:8    Block CRC8                     Block CRC8
                                         CRC-8-CCITT:
                                          Start Section -> Word: Sideband Configuration Structure -> Block Length
                                          End Section -> Word: Sideband Configuration Structure -> NC-SI Channel to Port Mapping
                                         Note: This field is preserved by Intel NVM update tool.
  7:0     Reserved             0x0       Reserved. Block length in words.

310                                                                                                                            333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.18 Pass-Through Control Words Section

Table 6-24. Pass-Through Control Words Section Summary Table
                                                                                   Section
 Word Offset                                            Description
                                                                                   Number

0x0000         Block Length                                                        6.2.18.1

0x0001         LAN IPv4 Address 0 (LSB) MIPAF0                                     6.2.18.2

0x0002         LAN IPv4 Address 0 (MSB) MIPAF0                                     6.2.18.3

0x0003         LAN IPv4 Address 1 (LSB) MIPAF1                                     6.2.18.4

0x0004         LAN IPv4 Address 1 (MSB) MIPAF1                                     6.2.18.5

0x0005         LAN IPv4 Address 2 (LSB) MIPAF2                                     6.2.18.6

0x0006         LAN IPv4 Address 2 (MSB) MIPAF2                                     6.2.18.7

0x0007         LAN IPv4 Address 3 (LSB) MIPAF3                                     6.2.18.8

0x0008         LAN IPv4 Address 3 (MSB) MIPAF4                                     6.2.18.9

0x0009         LAN Ethernet MAC Address 0 (LSB) MMAL0                              6.2.18.10

0x000A         LAN Ethernet MAC Address 0 (Mid) MMAL0                              6.2.18.11

0x000B         LAN Ethernet MAC Address 0 (MSB) MMAH0                              6.2.18.12

0x000C         LAN Ethernet MAC Address 1 (LSB) MMAL1                              6.2.18.13

0x000D         LAN Ethernet MAC Address 1 (Mid) MMAL1                              6.2.18.14

0x000E         LAN Ethernet MAC Address 1 (MSB) MMAH1                              6.2.18.15

0x000F         LAN Ethernet MAC Address 2 (LSB) MMAL2                              6.2.18.16

0x0010         LAN Ethernet MAC Address 2 (Mid) MMAL2                              6.2.18.17

0x0011         LAN Ethernet MAC Address 2 (MSB) MMAH2                              6.2.18.18

0x0012         LAN Ethernet MAC Address 3 (LSB) MMAL3                              6.2.18.19

0x0013         LAN Ethernet MAC Address 3 (Mid) MMAL3                              6.2.18.20

0x0014         LAN Ethernet MAC Address 3 (MSB) MMAH3                              6.2.18.21

0x0015         LAN TCP/UDP Flexible Filter Port0                                   6.2.18.22

0x0016         LAN TCP/UDP Flexible Filter Port1                                   6.2.18.23

0x0017         LAN TCP/UDP Flexible Filter Port2                                   6.2.18.24

0x0018         LAN TCP/UDP Flexible Filter Port3                                   6.2.18.25

0x0019         LAN TCP/UDP Flexible Filter Port4                                   6.2.18.26

0x001A         LAN TCP/UDP Flexible Filter Port5                                   6.2.18.27

0x001B         LAN TCP/UDP Flexible Filter Port6                                   6.2.18.28

0x001C         LAN TCP/UDP Flexible Filter Port7                                   6.2.18.29

0x001D         LAN TCP/UDP Flexible Filter Port8                                   6.2.18.30

0x001E         LAN TCP/UDP Flexible Filter Port9                                   6.2.18.31

0x001F         LAN TCP/UDP Flexible Filter Port10                                  6.2.18.32

0x0020         LAN TCP/UDP Flexible Filter Port11                                  6.2.18.33

0x0021         LAN TCP/UDP Flexible Filter Port12                                  6.2.18.34

0x0022         LAN TCP/UDP Flexible Filter Port13                                  6.2.18.35

333369-009                                                                                311
                                   Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                           Non-Volatile Memory Map

Table 6-24. Pass-Through Control Words Section Summary Table [continued]
                                                                                                        Section
 Word Offset                                                Description
                                                                                                        Number

0x0023         LAN TCP/UDP Flexible Filter Port14                                                       6.2.18.36

0x0024         LAN TCP/UDP Flexible Filter Port15                                                       6.2.18.37

0x0025         LAN VLAN Filter 0                                                                        6.2.18.38

0x0026         LAN VLAN Filter 1                                                                        6.2.18.39

0x0027         LAN VLAN Filter 2                                                                        6.2.18.40

0x0028         LAN VLAN Filter 3                                                                        6.2.18.41

0x0029         LAN VLAN Filter 4                                                                        6.2.18.42

0x002A         LAN VLAN Filter 5                                                                        6.2.18.43

0x002B         LAN VLAN Filter 6                                                                        6.2.18.44

0x002C         LAN VLAN Filter 7                                                                        6.2.18.45

0x002D         MANC Value LSB - LMANC LSB                                                               6.2.18.46

0x002E         MANC Value LSB - LMANC MSB                                                               6.2.18.47

0x002F         Receive Enable 1 - LRXEN1                                                                6.2.18.48

0x0030         Receive Enable 2 - LRXEN2                                                                6.2.18.49

0x0031         MNGONLY Value - MNGONLY LSB                                                              6.2.18.50

0x0032         MNGONLY Value - MNGONLY MSB                                                              6.2.18.51

0x0033         Manageability Decision Filters - MDEF0 LSB                                               6.2.18.52

0x0034         Manageability Decision Filters - MDEF0 MSB                                               6.2.18.53

0x0035         Manageability Decision Filters - MDEF_EXT0 LSB                                           6.2.18.54

0x0036         Manageability Decision Filters - MDEF_EXT0 MSB                                           6.2.18.55

0x0037         Manageability Decision Filters - MDEF1 LSB                                               6.2.18.56

0x0038         Manageability Decision Filters - MDEF1 MSB                                               6.2.18.57

0x0039         Manageability Decision Filters - MDEF_EXT1 LSB                                           6.2.18.58

0x003A         Manageability Decision Filters - MDEF_EXT1 MSB                                           6.2.18.59

0x003B         Manageability Decision Filters - MDEF2 LSB                                               6.2.18.60

0x003C         Manageability Decision Filters - MDEF2 MSB                                               6.2.18.61

0x003D         Manageability Decision Filters - MDEF_EXT2 LSB                                           6.2.18.62

0x003E         Manageability Decision Filters - MDEF_EXT2 MSB                                           6.2.18.63

0x003F         Manageability Decision Filters - MDEF3 LSB                                               6.2.18.64

0x0040         Manageability Decision Filters - MDEF3 MSB                                               6.2.18.65

0x0041         Manageability Decision Filters - MDEF_EXT3 LSB                                           6.2.18.66

0x0042         Manageability Decision Filters - MDEF_EXT3 MSB                                           6.2.18.67

0x0043         Manageability Decision Filters - MDEF4 LSB                                               6.2.18.68

0x0044         Manageability Decision Filters - MDEF4 MSB                                               6.2.18.69

0x0045         Manageability Decision Filters - MDEF_EXT4 LSB                                           6.2.18.70

0x0046         Manageability Decision Filters - MDEF_EXT4 MSB                                           6.2.18.71

0x0047         Manageability Decision Filters - MDEF5 LSB                                               6.2.18.72

312                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-24. Pass-Through Control Words Section Summary Table [continued]
                                                                                    Section
 Word Offset                                                Description
                                                                                    Number

0x0048         Manageability Decision Filters - MDEF5 MSB                           6.2.18.73

0x0049         Manageability Decision Filters - MDEF_EXT5 LSB                       6.2.18.74

0x004A         Manageability Decision Filters - MDEF_EXT5 MSB                       6.2.18.75

0x004B         Manageability Decision Filters - MDEF6 LSB                           6.2.18.76

0x004C         Manageability Decision Filters - MDEF6 MSB                           6.2.18.77

0x004D         Manageability Decision Filters - MDEF_EXT6 LSB                       6.2.18.78

0x004E         Manageability Decision Filters - MDEF_EXT6 MSB                       6.2.18.79

0x004F         Manageability EtherType filter 0.1 - METF0.1                         6.2.18.80

0x0050         Manageability EtherType filter 0.2 - METF0.2                         6.2.18.81

0x0051         Manageability EtherType filter 1.1 - METF1.1                         6.2.18.82

0x0052         Manageability EtherType filter 1.2 - METF1.2                         6.2.18.83

0x0053         Manageability EtherType filter 2.1 - METF2.1                         6.2.18.84

0x0054         Manageability EtherType filter 2.2 - METF2.2                         6.2.18.85

0x0055         Manageability EtherType filter 3.1 - METF3.1                         6.2.18.86

0x0056         Manageability EtherType filter 3.2 - METF3.2                         6.2.18.87

0x0057         ARP Response IPv4 Address 0 - LSB                                    6.2.18.88

0x0058         ARP Response IPv4 Address 0 - MSB                                    6.2.18.89

0x0059         IPv6 Address 0 - 0                                                   6.2.18.90

0x005A         IPv6 Address 0 - 1                                                   6.2.18.91

0x005B         IPv6 Address 0 - 2                                                   6.2.18.92

0x005C         IPv6 Address 0 - 3                                                   6.2.18.93

0x005D         IPv6 Address 0 - 4                                                   6.2.18.94

0x005E         IPv6 Address 0 - 5                                                   6.2.18.95

0x005F         IPv6 Address 0 - 6                                                   6.2.18.96

0x0060         IPv6 Address 0 - 7                                                   6.2.18.97

0x0061         IPv6 Address 1 - 0                                                   6.2.18.98

0x0062         IPv6 Address 1 - 1                                                   6.2.18.99

0x0063         IPv6 Address 1 - 2                                                   6.2.18.100

0x0064         IPv6 Address 1 - 3                                                   6.2.18.101

0x0065         IPv6 Address 1 - 4                                                   6.2.18.102

0x0066         IPv6 Address 1 - 5                                                   6.2.18.103

0x0067         IPv6 Address 1 - 6                                                   6.2.18.104

0x0068         IPv6 Address 1 - 7                                                   6.2.18.105

0x0069         IPv6 Address 2 - 0                                                   6.2.18.106

0x006A         IPv6 Address 2 - 1                                                   6.2.18.107

0x006B         IPv6 Address 2 - 2                                                   6.2.18.108

0x006C         IPv6 Address 2 - 3                                                   6.2.18.109

333369-009                                                                                  313
                                    Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

Table 6-24. Pass-Through Control Words Section Summary Table [continued]
                                                                                                                  Section
 Word Offset                                                 Description
                                                                                                                  Number

0x006D           IPv6 Address 2 - 4                                                                               6.2.18.110

0x006E           IPv6 Address 2 - 5                                                                               6.2.18.111

0x006F           IPv6 Address 2 - 6                                                                               6.2.18.112

0x0070           IPv6 Address 2 - 7                                                                               6.2.18.113

0x0071           Block CRC8                                                                                       6.2.18.114

#### 6.2.18.1 Block Length (0x0000)

 Bit(s)    Field Name      Default                                            Description

  15:0    Block Length                 Block Length
                                       Length in words of the section covered by CRC.
                                       Block Length in words.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.2 LAN IPv4 Address 0 (LSB) MIPAF0 (0x0001)

 Bit(s)        Field Name             Default                                     Description

  15:8    IPv4 Address 0, Byte 1       0x0      IPv4 Address 0, Byte 1
                                                Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 0, Byte 0       0x0A     IPv4 Address 0, Byte 0
                                                Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.3 LAN IPv4 Address 0 (MSB) MIPAF0 (0x0002)

 Bit(s)        Field Name             Default                                     Description

  15:8    IPv4 Address 0, Byte 3       0x01     IPv4 Address 0, Byte 3
                                                Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 0, Byte 2       0x0      IPv4 Address 0, Byte 2
                                                Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.4 LAN IPv4 Address 1 (LSB) MIPAF1 (0x0003)

 Bit(s)        Field Name             Default                                     Description

  15:8    IPv4 Address 1, Byte 1       0x0      IPv4 Address 1, Byte 1
                                                Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 1, Byte 0       0x0A     IPv4 Address 1, Byte 0
                                                Note: This field is preserved by Intel NVM update tool.

314                                                                                                               333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.5 LAN IPv4 Address 1 (MSB) MIPAF1 (0x0004)

 Bit(s)        Field Name          Default                                     Description

  15:8    IPv4 Address 1, Byte 3    0x02     IPv4 Address 1, Byte 3
                                             Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 1, Byte 2    0x0      IPv4 Address 1, Byte 2
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.6 LAN IPv4 Address 2 (LSB) MIPAF2 (0x0005)

 Bit(s)        Field Name          Default                                     Description

  15:8    IPv4 Address 2, Byte 1    0x0      IPv4 Address 2, Byte 1
                                             Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 2, Byte 0    0x0A     IPv4 Address 2, Byte 0
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.7 LAN IPv4 Address 2 (MSB) MIPAF2 (0x0006)

 Bit(s)        Field Name          Default                                     Description

  15:8    IPv4 Address 2, Byte 3    0x03     IPv4 Address 2, Byte 3
                                             Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 2, Byte 2    0x0      IPv4 Address 2, Byte 2
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.8 LAN IPv4 Address 3 (LSB) MIPAF3 (0x0007)

 Bit(s)        Field Name          Default                                     Description

  15:8    IPv4 Address 3, Byte 1    0x0      IPv4 Address 3, Byte 1
                                             Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 3, Byte 0    0x0A     IPv4 Address 3, Byte 0
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.9 LAN IPv4 Address 3 (MSB) MIPAF3 (0x0008)

 Bit(s)        Field Name          Default                                     Description

  15:8    IPv4 Address 3, Byte 3    0x04     IPv4 Address 3, Byte 3
                                             Note: This field is preserved by Intel NVM update tool.
  7:0     IPv4 Address 3, Byte 2    0x0      IPv4 Address 3, Byte 2
                                             Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                             315
                                    Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

#### 6.2.18.10 LAN Ethernet MAC Address 0 (LSB) MMAL0 (0x0009)

This word is loaded by the firmware to the 16 LS bits of the MMAL[0] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 0, Byte 1    0x88     Ethernet MAC Address 0, Byte 1
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 0, Byte 0    0x88     Ethernet MAC Address 0, Byte 0
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.11 LAN Ethernet MAC Address 0 (Mid) MMAL0 (0x000A)

This word is loaded by the firmware to the 16 MS bits of the MMAL[0] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 0, Byte 3    0x88     Ethernet MAC Address 0, Byte 3
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 0, Byte 2    0x88     Ethernet MAC Address 0, Byte 2
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.12 LAN Ethernet MAC Address 0 (MSB) MMAH0 (0x000B)

This word is loaded by the firmware to the MMAH[0] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 0, Byte 5    0x01     Ethernet MAC Address 0, Byte 5
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 0, Byte 4    0x88     Ethernet MAC Address 0, Byte 4
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.13 LAN Ethernet MAC Address 1 (LSB) MMAL1 (0x000C)

This word is loaded by the firmware to the 16 LS bits of the MMAL[1] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 1, Byte 1    0x88     Ethernet MAC Address 1, Byte 1
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 1, Byte 0    0x88     Ethernet MAC Address 1, Byte 0
                                                     Note: This field is preserved by Intel NVM update tool.

316                                                                                                            333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.14 LAN Ethernet MAC Address 1 (Mid) MMAL1 (0x000D)

This word is loaded by the firmware to the 16 MS bits of the MMAL[1] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 1, Byte 3    0x88     Ethernet MAC Address 1, Byte 3
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 1, Byte 2    0x88     Ethernet MAC Address 1, Byte 2
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.15 LAN Ethernet MAC Address 1 (MSB) MMAH1 (0x000E)

This word is loaded by the firmware to the MMAH[1] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 1, Byte 5    0x02     Ethernet MAC Address 1, Byte 5
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 1, Byte 4    0x88     Ethernet MAC Address 1, Byte 4
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.16 LAN Ethernet MAC Address 2 (LSB) MMAL2 (0x000F)

This word is loaded by the firmware to the 16 LS bits of the MMAL[2] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 2, Byte 1    0x88     Ethernet MAC Address 2, Byte 1
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 2, Byte 0    0x88     Ethernet MAC Address 2, Byte 0
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.17 LAN Ethernet MAC Address 2 (Mid) MMAL2 (0x0010)

This word is loaded by the firmware to the 16 MS bits of the MMAL[2] register.

 Bit(s)            Field Name              Default                                Description

  15:8    Ethernet MAC Address 2, Byte 3    0x88     Ethernet MAC Address 2, Byte 3
                                                     Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 2, Byte 2    0x88     Ethernet MAC Address 2, Byte 2
                                                     Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                     317
                                    Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.18.18 LAN Ethernet MAC Address 2 (MSB) MMAH2 (0x0011)

This word is loaded by the firmware to the MMAH[2] register.

 Bit(s)             Field Name               Default                                 Description

  15:8    Ethernet MAC Address 2, Byte 5      0x03     Ethernet MAC Address 2, Byte 5
                                                       Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 2, Byte 4      0x88     Ethernet MAC Address 2, Byte 4
                                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.19 LAN Ethernet MAC Address 3 (LSB) MMAL3 (0x0012)

This word is loaded by the firmware to the 16 LS bits of the MMAL[3] register.

 Bit(s)             Field Name               Default                                 Description

  15:8    Ethernet MAC Address 3, Byte 1      0x88     Ethernet MAC Address 3, Byte 1
                                                       Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 3, Byte 0      0x88     Ethernet MAC Address 3, Byte 0
                                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.20 LAN Ethernet MAC Address 3 (Mid) MMAL3 (0x0013)

This word is loaded by the firmware to the 16 MS bits of the MMAL[3] register.

 Bit(s)             Field Name               Default                                 Description

  15:8    Ethernet MAC Address 3, Byte 3      0x88     Ethernet MAC Address 3, Byte 3
                                                       Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 3, Byte 2      0x88     Ethernet MAC Address 3, Byte 2
                                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.21 LAN Ethernet MAC Address 3 (MSB) MMAH3 (0x0014)

This word is loaded by the firmware to the MMAH[3] register.

 Bit(s)             Field Name               Default                                 Description

  15:8    Ethernet MAC Address 3, Byte 5      0x04     Ethernet MAC Address 3, Byte 5
                                                       Note: This field is preserved by Intel NVM update tool.
  7:0     Ethernet MAC Address 3, Byte 4      0x88     Ethernet MAC Address 3, Byte 4
                                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.22 LAN TCP/UDP Flexible Filter Port0 (0x0015)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port0     0x0      LAN UDP Flexible Filter Port 0
                                                     Note: This field is preserved by Intel NVM update tool.

318                                                                                                              333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.23 LAN TCP/UDP Flexible Filter Port1 (0x0016)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port1    0x0      LAN UDP Flexible Filter Port 1
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.24 LAN TCP/UDP Flexible Filter Port2 (0x0017)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port2    0x0      LAN UDP Flexible Filter Port 2
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.25 LAN TCP/UDP Flexible Filter Port3 (0x0018)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port3    0x0      LAN UDP Flexible Filter Port 3
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.26 LAN TCP/UDP Flexible Filter Port4 (0x0019)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port4    0x0      LAN UDP Flexible Filter Port 4
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.27 LAN TCP/UDP Flexible Filter Port5 (0x001A)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port5    0x0      LAN UDP Flexible Filter Port 5
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.28 LAN TCP/UDP Flexible Filter Port6 (0x001B)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port6    0x0      LAN UDP Flexible Filter Port 6
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.29 LAN TCP/UDP Flexible Filter Port7 (0x001C)

 Bit(s)            Field Name             Default                                  Description

  15:0    LAN UDP Flexible Filter Port7    0x0      LAN UDP Flexible Filter Port 7
                                                    Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                    319
                                      Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

#### 6.2.18.30 LAN TCP/UDP Flexible Filter Port8 (0x001D)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port8     0x0      LAN UDP Flexible Filter Port 8
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.31 LAN TCP/UDP Flexible Filter Port9 (0x001E)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port9     0x0      LAN UDP Flexible Filter Port 9
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.32 LAN TCP/UDP Flexible Filter Port10 (0x001F)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port10    0x0      LAN UDP Flexible Filter Port 10
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.33 LAN TCP/UDP Flexible Filter Port11 (0x0020)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port11    0x0      LAN UDP Flexible Filter Port 11
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.34 LAN TCP/UDP Flexible Filter Port12 (0x0021)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port12    0x0      LAN UDP Flexible Filter Port 12
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.35 LAN TCP/UDP Flexible Filter Port13 (0x0022)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port13    0x0      LAN UDP Flexible Filter Port 13
                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.36 LAN TCP/UDP Flexible Filter Port14 (0x0023)

 Bit(s)            Field Name              Default                                  Description

  15:0    LAN UDP Flexible Filter Port14    0x0      LAN UDP Flexible Filter Port 14
                                                     Note: This field is preserved by Intel NVM update tool.

320                                                                                                             333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.37 LAN TCP/UDP Flexible Filter Port15 (0x0024)

 Bit(s)              Field Name             Default                                    Description

  15:0    LAN UDP Flexible Filter Port15     0x0        LAN UDP Flexible Filter Port 15
                                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.38 LAN VLAN Filter 0 (0x0025)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                 0x0      Reserved.
  11:0    VLAN Filter 0 Value      0x0      VLAN Filter 0 Value
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.39 LAN VLAN Filter 1 (0x0026)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                 0x0      Reserved.
  11:0    VLAN Filter 1 Value      0x0      VLAN Filter 1 Value
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.40 LAN VLAN Filter 2 (0x0027)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                 0x0      Reserved.
  11:0    VLAN Filter 2 Value      0x0      VLAN Filter 3 Value
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.41 LAN VLAN Filter 3 (0x0028)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                 0x0      Reserved.
  11:0    VLAN Filter 3 Value      0x0      VLAN Filter 3 Value
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.42 LAN VLAN Filter 4 (0x0029)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                 0x0      Reserved.
  11:0    VLAN Filter 4 Value      0x0      VLAN Filter 4 Value
                                            Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                        321
                                      Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

#### 6.2.18.43 LAN VLAN Filter 5 (0x002A)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                    0x0    Reserved.
  11:0    VLAN Filter 5 Value         0x0    VLAN Filter 5 Value
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.44 LAN VLAN Filter 6 (0x002B)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                    0x0    Reserved.
  11:0    VLAN Filter 6 Value         0x0    VLAN Filter 6 Value
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.45 LAN VLAN Filter 7 (0x002C)

 Bit(s)       Field Name          Default                                         Description

 15:12    Reserved                    0x0    Reserved.
  11:0    VLAN Filter 7 Value         0x0    VLAN Filter 7 Value
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.46 MANC Value LSB - LMANC LSB (0x002D)

 Bit(s)    Field Name        Default                                           Description

  15:0    Reserved              0x0     Reserved.

#### 6.2.18.47 MANC Value MSB - LMANC MSB (0x002E)

 Bit(s)       Field Name          Default                                         Description

 15:11    Reserved                    0x0    Reserved.

# 10 Net Type                     0b    Net Type

                                             This bit is loaded to the NET_TYPE bit in the MANC register.
                                             Note: This field is preserved by Intel NVM update tool.

# 9 Fixed Net Type               0b    Fixed Net Type

                                             This bit is loaded to the FIXED_NET_TYPE bit in the MANC register.
                                             Note: This field is preserved by Intel NVM update tool.

# 8 Enable IPv4 Address          0b    Enable IPv4 Address Filters

          Filters                             0b = These bits store a single IPv6 filter.
                                              1b = The last 128 bits of the MIPAF register are used to store four IPv4 addresses for
                                                   IPv4 filtering.
                                             Note: This field is preserved by Intel NVM update tool.

# 7 Enable Xsum                  0b    Enable Xsum Filtering to MNG

          Filtering to MNG                   When this bit is set, only packets that pass the L3 and L4 checksum are sent to the
                                             manageability block.
                                             This feature does not support tunneled IPv4/IPv6 packet inspection.
                                             Note: This field is preserved by Intel NVM update tool.

322                                                                                                                      333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name           Default                                         Description

  6:0     Reserved                  0x0         Reserved.

#### 6.2.18.48 Receive Enable 1 - LRXEN1 (0x002F)

 Bit(s)          Field Name               Default                                     Description

  15:8    Receive Enable byte 12           0x0       Receive Enable byte 12
                                                     BMC SMBus slave address.
                                                     Note: This field is preserved by Intel NVM update tool.

# 7 Enable BMC Dedicated               0b      Enable BMC Dedicated

                                                     Note: This field is preserved by Intel NVM update tool.

# 6 Reserved                           1b      Reserved.

  5:4     Notification Method              00b       Notification Method
                                                      00b = SMBus alert
                                                      01b = Asynchronous notify
                                                      10b = Direct receive
                                                      11b = Reserved
                                                     Note: This field is preserved by Intel NVM update tool.

# 3 Enable ARP Response                0b      Enable ARP Response

                                                     Note: This field is preserved by Intel NVM update tool.

# 2 Enable Status Reporting            0b      Enable Status Reporting

                                                     Note: This field is preserved by Intel NVM update tool.

# 1 Enable Receive All                 0b      Enable Receive All

                                                     Note: This field is preserved by Intel NVM update tool.

# 0 Enable Receive TCO                 0b      Enable Receive TCO

                                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.49 Receive Enable 2 - LRXEN2 (0x0030)

 Bit(s)         Field Name             Default                                        Description

  15:8    Receive Enable byte 14          0x0       Receive Enable byte 14
                                                    Alert value.
                                                    Note: This field is preserved by Intel NVM update tool.
  7:0     Receive Enable byte 13          0x0       Receive Enable byte 13
                                                    Interface data.
                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.50 MNGONLY Value - MNGONLY LSB (0x0031)

 Bit(s)      Field Name         Default                                           Description

  15:8    Reserved               0x0       Reserved.
  7:0     Exclusive to MNG       0x0       Exclusive to Manageability
                                           When set, indicates that packets forwarded by the manageability filters to manageability
                                           are not sent to the host. Bit 0 corresponds to decision rule 0, etc.
                                           Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                       323
                                       Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                        Non-Volatile Memory Map

#### 6.2.18.51 MNGONLY Value - MNGONLY MSB (0x0032)

 Bit(s)    Field Name        Default                                             Description

  15:0    Reserved             0x0      Reserved.

#### 6.2.18.52 Manageability Decision Filters - MDEF0 LSB (0x0033)

 Bit(s)       Field Name         Default                                            Description

 15:12    Flex Port (OR)             0x0     Flex Port (OR)
                                             Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                             section). Bit 12 corresponds to flex port 0, etc.
                                             Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)              0b    Port 0x26F (OR)

                                             Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                             section)
                                             Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)              0b    Port 0x298 (OR)

                                             Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

# 9 Neighbor Discovery           0b    Neighbor Discovery (OR)

          (OR)                               Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                             (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                             and 0x89.
                                             Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)            0b    ARP Response (OR)

                                             Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)             0b    ARP Request (OR)

                                             Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)                    0b    VLAN (OR)

                                             Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                             (OR section).
                                             Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)               0b    Broadcast (OR)

                                             Controls the inclusion of broadcast address filtering in the manageability filter decision
                                             (OR section).
                                             Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)                 0b    Unicast (OR)

                                             Controls the inclusion of unicast address filtering in the manageability filter decision
                                             (OR section).
                                             Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)             0b    IP Address (AND)

                                             Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)                   0b    VLAN (AND)

                                             Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

324                                                                                                                          333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)        Field Name        Default                                            Description

# 1 Broadcast (AND)             0b     Broadcast (AND)

                                             Controls the inclusion of broadcast address filtering in the manageability filter decision
                                             (AND section).
                                             Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)               0b     Unicast (AND)

                                             Controls the inclusion of unicast address filtering in the manageability filter decision
                                             (AND section).
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.53 Manageability Decision Filters - MDEF0 MSB (0x0034)

 Bit(s)    Field Name       Default                                              Description

 15:12    Flex TCO             0x0     Flex TCO
                                       Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                       Bit 28 corresponds to Flex TCO filter 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0     Flex Port
                                       Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                       Bit 12 corresponds to flex port 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.54 Manageability Decision Filters - MDEF_EXT0 LSB

                          (0x0035)

 Bit(s)        Field Name        Default                                            Description

 15:12    Reserved                   0x0     Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0     L2 EtherType OR L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0     Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0     L2 EtherType AND L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.55 Manageability Decision Filters - MDEF_EXT0 MSB

                          (0x0036)

 Bit(s)      Field Name     Default                                              Description

  15:0    Reserved             0x0     Reserved.

333369-009                                                                                                                              325
                                       Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                    Non-Volatile Memory Map

#### 6.2.18.56 Manageability Decision Filters - MDEF1 LSB (0x0037)

 Bit(s)       Field Name       Default                                          Description

 15:12    Flex Port (OR)        0x0      Flex Port (OR)
                                         Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                         section). Bit 12 corresponds to flex port 0, etc.
                                         Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)        0b      Port 0x26F (OR)

                                         Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                         section)
                                         Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)        0b      Port 0x298 (OR)

                                         Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

# 9 Neighbor Discovery     0b      Neighbor Discovery (OR)

          (OR)                           Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                         (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                         and 0x89.
                                         Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)      0b      ARP Response (OR)

                                         Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)       0b      ARP Request (OR)

                                         Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)              0b      VLAN (OR)

                                         Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)         0b      Broadcast (OR)

                                         Controls the inclusion of broadcast address filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)           0b      Unicast (OR)

                                         Controls the inclusion of unicast address filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)       0b      IP Address (AND)

                                         Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)             0b      VLAN (AND)

                                         Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)        0b      Broadcast (AND)

                                         Controls the inclusion of broadcast address filtering in the manageability filter decision
                                         (AND section).
                                         Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)          0b      Unicast (AND)

                                         Controls the inclusion of unicast address filtering in the manageability filter decision
                                         (AND section).
                                         Note: This field is preserved by Intel NVM update tool.

326                                                                                                                      333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.57 Manageability Decision Filters - MDEF1 MSB (0x0038)

 Bit(s)    Field Name       Default                                              Description

 15:12    Flex TCO             0x0     Flex TCO
                                       Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                       Bit 28 corresponds to Flex TCO filter 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0     Flex Port
                                       Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                       Bit 12 corresponds to flex port 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.58 Manageability Decision Filters - MDEF_EXT1 LSB

                           (0x0039)

 Bit(s)        Field Name        Default                                            Description

 15:12    Reserved                   0x0     Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0     L2 EtherType OR L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0     Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0     L2 EtherType AND L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.59 Manageability Decision Filters - MDEF_EXT1 MSB

                           (0x003A)

 Bit(s)      Field Name     Default                                              Description

  15:0    Reserved             0x0     Reserved.

#### 6.2.18.60 Manageability Decision Filters - MDEF2 LSB (0x003B)

 Bit(s)        Field Name        Default                                            Description

 15:12    Flex Port (OR)             0x0     Flex Port (OR)
                                             Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                             section). Bit 12 corresponds to flex port 0, etc.
                                             Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)             0b     Port 0x26F (OR)

                                             Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                             section)
                                             Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)             0b     Port 0x298 (OR)

                                             Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                             327
                                       Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                          Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                             Description

# 9 Neighbor Discovery           0b     Neighbor Discovery (OR)

          (OR)                                Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                              (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                              and 0x89.
                                              Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)            0b     ARP Response (OR)

                                              Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)             0b     ARP Request (OR)

                                              Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)                    0b     VLAN (OR)

                                              Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)               0b     Broadcast (OR)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)                 0b     Unicast (OR)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)             0b     IP Address (AND)

                                              Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)                   0b     VLAN (AND)

                                              Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)              0b     Broadcast (AND)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)                0b     Unicast (AND)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.61 Manageability Decision Filters - MDEF2 MSB (0x003C)

 Bit(s)    Field Name        Default                                              Description

 15:12    Flex TCO             0x0      Flex TCO
                                        Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                        Bit 28 corresponds to Flex TCO filter 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0      Flex Port
                                        Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                        Bit 12 corresponds to flex port 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.

328                                                                                                                           333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.62 Manageability Decision Filters - MDEF_EXT2 LSB

                           (0x003D)

 Bit(s)       Field Name         Default                                           Description

 15:12    Reserved                   0x0    Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0    L2 EtherType OR L2 EtherType
          EtherType                         Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0    Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0    L2 EtherType AND L2 EtherType
          EtherType                         Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.63 Manageability Decision Filters - MDEF2_EXT2 MSB

                           (0x003E)

 Bit(s)    Field Name       Default                                             Description

  15:0    Reserved             0x0     Reserved.

#### 6.2.18.64 Manageability Decision Filters - MDEF3 LSB (0x003F)

 Bit(s)       Field Name         Default                                           Description

 15:12    Flex Port (OR)             0x0    Flex Port (OR)
                                            Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                            section). Bit 12 corresponds to flex port 0, etc.
                                            Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)             0b    Port 0x26F (OR)

                                            Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                            section)
                                            Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)             0b    Port 0x298 (OR)

                                            Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

# 9 Neighbor Discovery          0b    Neighbor Discovery (OR)

          (OR)                              Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                            (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                            and 0x89.
                                            Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)           0b    ARP Response (OR)

                                            Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)            0b    ARP Request (OR)

                                            Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                            329
                                       Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                          Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                             Description

    6 VLAN (OR)                    0b     VLAN (OR)

                                              Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)               0b     Broadcast (OR)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)                 0b     Unicast (OR)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)             0b     IP Address (AND)

                                              Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)                   0b     VLAN (AND)

                                              Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)              0b     Broadcast (AND)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)                0b     Unicast (AND)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.65 Manageability Decision Filters - MDEF3 MSB (0x0040)

 Bit(s)    Field Name        Default                                              Description

 15:12    Flex TCO             0x0      Flex TCO
                                        Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                        Bit 28 corresponds to Flex TCO filter 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0      Flex Port
                                        Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                        Bit 12 corresponds to flex port 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.66 Manageability Decision Filters - MDEF_EXT3 LSB

                          (0x0041)

 Bit(s)       Field Name         Default                                             Description

 15:12    Reserved                   0x0      Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0      L2 EtherType OR L2 EtherType
          EtherType                           Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0      Reserved for additional L2 EtherType AND filters.

330                                                                                                                           333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                           Description

  3:0     L2 EtherType AND L2        0x0    L2 EtherType AND L2 EtherType
          EtherType                         Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.67 Manageability Decision Filters - MDEF_EXT3 MSB

                           (0x0042)

 Bit(s)    Field Name       Default                                             Description

  15:0    Reserved             0x0     Reserved.

#### 6.2.18.68 Manageability Decision Filters - MDEF4 LSB (0x0043)

 Bit(s)       Field Name         Default                                           Description

 15:12    Flex Port (OR)             0x0    Flex Port (OR)
                                            Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                            section). Bit 12 corresponds to flex port 0, etc.
                                            Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)             0b    Port 0x26F (OR)

                                            Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                            section)
                                            Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)             0b    Port 0x298 (OR)

                                            Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

# 9 Neighbor Discovery          0b    Neighbor Discovery (OR)

          (OR)                              Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                            (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                            and 0x89.
                                            Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)           0b    ARP Response (OR)

                                            Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)            0b    ARP Request (OR)

                                            Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)                   0b    VLAN (OR)

                                            Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                            (OR section).
                                            Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)              0b    Broadcast (OR)

                                            Controls the inclusion of broadcast address filtering in the manageability filter decision
                                            (OR section).
                                            Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)                0b    Unicast (OR)

                                            Controls the inclusion of unicast address filtering in the manageability filter decision
                                            (OR section).
                                            Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                             331
                                       Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                          Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                             Description

    3 IP Address (AND)             0b     IP Address (AND)

                                              Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)                   0b     VLAN (AND)

                                              Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)              0b     Broadcast (AND)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)                0b     Unicast (AND)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.69 Manageability Decision Filters - MDEF4 MSB (0x0044)

 Bit(s)    Field Name        Default                                              Description

 15:12    Flex TCO             0x0      Flex TCO
                                        Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                        Bit 28 corresponds to Flex TCO filter 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0      Flex Port
                                        Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                        Bit 12 corresponds to flex port 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.70 Manageability Decision Filters - MDEF_EXT4 LSB

                          (0x0045)

 Bit(s)       Field Name         Default                                             Description

 15:12    Reserved                   0x0      Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0      L2 EtherType OR L2 EtherType
          EtherType                           Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0      Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0      L2 EtherType AND L2 EtherType
          EtherType                           Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.71 Manageability Decision Filters - MDEF_EXT4 MSB

                          (0x0046)

 Bit(s)    Field Name        Default                                              Description

  15:0    Reserved             0x0      Reserved.

332                                                                                                                           333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.72 Manageability Decision Filters - MDEF5 LSB (0x0047)

 Bit(s)       Field Name       Default                                          Description

 15:12    Flex Port (OR)        0x0      Flex Port (OR)
                                         Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                         section). Bit 12 corresponds to flex port 0, etc.
                                         Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)        0b      Port 0x26F (OR)

                                         Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                         section)
                                         Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)        0b      Port 0x298 (OR)

                                         Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

# 9 Neighbor Discovery     0b      Neighbor Discovery (OR)

          (OR)                           Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                         (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                         and 0x89.
                                         Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)      0b      ARP Response (OR)

                                         Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)       0b      ARP Request (OR)

                                         Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)              0b      VLAN (OR)

                                         Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)         0b      Broadcast (OR)

                                         Controls the inclusion of broadcast address filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)           0b      Unicast (OR)

                                         Controls the inclusion of unicast address filtering in the manageability filter decision
                                         (OR section).
                                         Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)       0b      IP Address (AND)

                                         Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)             0b      VLAN (AND)

                                         Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                         section).
                                         Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)        0b      Broadcast (AND)

                                         Controls the inclusion of broadcast address filtering in the manageability filter decision
                                         (AND section).
                                         Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)          0b      Unicast (AND)

                                         Controls the inclusion of unicast address filtering in the manageability filter decision
                                         (AND section).
                                         Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                          333
                                   Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                         Non-Volatile Memory Map

#### 6.2.18.73 Manageability Decision Filters - MDEF5 MSB (0x0048)

 Bit(s)    Field Name       Default                                              Description

 15:12    Flex TCO             0x0     Flex TCO
                                       Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                       Bit 28 corresponds to Flex TCO filter 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0     Flex Port
                                       Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                       Bit 12 corresponds to flex port 0, etc.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.74 Manageability Decision Filters - MDEF_EXT5 LSB

                           (0x0049)

 Bit(s)       Field Name         Default                                            Description

 15:12    Reserved                   0x0     Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0     L2 EtherType OR L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0     Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0     L2 EtherType AND L2 EtherType
          EtherType                          Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.75 Manageability Decision Filters - MDEF5_EXT5 MSB

                           (0x004A)

 Bit(s)    Field Name       Default                                              Description

  15:0    Reserved             0x0     Reserved.

#### 6.2.18.76 Manageability Decision Filters - MDEF6 LSB (0x004B)

 Bit(s)       Field Name         Default                                            Description

 15:12    Flex Port (OR)             0x0     Flex Port (OR)
                                             Controls the inclusion of flex port filtering in the manageability filter decision (OR
                                             section). Bit 12 corresponds to flex port 0, etc.
                                             Note: This field is preserved by Intel NVM update tool.

# 11 Port 0x26F (OR)             0b     Port 0x26F (OR)

                                             Controls the inclusion of port 0x26F filtering in the manageability filter decision (OR
                                             section)
                                             Note: This field is preserved by Intel NVM update tool.

# 10 Port 0x298 (OR)             0b     Port 0x298 (OR)

                                             Controls the inclusion of port 0x298 filtering in the manageability filter decision (OR
                                             section).
                                             Note: This field is preserved by Intel NVM update tool.

334                                                                                                                          333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)       Field Name         Default                                             Description

# 9 Neighbor Discovery           0b     Neighbor Discovery (OR)

          (OR)                                Controls the inclusion of neighbor discovery filtering in the manageability filter decision
                                              (OR section). The neighbor types accepted by this filter are types 0x86, 0x87, 0x88
                                              and 0x89.
                                              Note: This field is preserved by Intel NVM update tool.

    8 ARP Response (OR)            0b     ARP Response (OR)

                                              Controls the inclusion of ARP response filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    7 ARP Request (OR)             0b     ARP Request (OR)

                                              Controls the inclusion of ARP request filtering in the manageability filter decision (OR
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    6 VLAN (OR)                    0b     VLAN (OR)

                                              Controls the inclusion of VLAN addresses filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 5 Broadcast (OR)               0b     Broadcast (OR)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

# 4 Unicast (OR)                 0b     Unicast (OR)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (OR section).
                                              Note: This field is preserved by Intel NVM update tool.

    3 IP Address (AND)             0b     IP Address (AND)

                                              Controls the inclusion of IP Address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

    2 VLAN (AND)                   0b     VLAN (AND)

                                              Controls the inclusion of VLAN address filtering in the manageability filter decision (AND
                                              section).
                                              Note: This field is preserved by Intel NVM update tool.

# 1 Broadcast (AND)              0b     Broadcast (AND)

                                              Controls the inclusion of broadcast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

# 0 Unicast (AND)                0b     Unicast (AND)

                                              Controls the inclusion of unicast address filtering in the manageability filter decision
                                              (AND section).
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.77 Manageability Decision Filters - MDEF6 MSB (0x004C)

 Bit(s)    Field Name        Default                                              Description

 15:12    Flex TCO             0x0      Flex TCO
                                        Controls the inclusion of Flex TCO filtering in the manageability filter decision (OR section).
                                        Bit 28 corresponds to Flex TCO filter 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.
  11:0    Flex Port            0x0      Flex Port
                                        Controls the inclusion of flex port filtering in the manageability filter decision (OR section).
                                        Bit 12 corresponds to flex port 0, etc.
                                        Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                               335
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

#### 6.2.18.78 Manageability Decision Filters - MDEF_EXT6 LSB

                        (0x004D)

 Bit(s)      Field Name          Default                                          Description

 15:12    Reserved                   0x0    Reserved for additional L2 EtherType OR filters.
  11:8    L2 EtherType OR L2         0x0    L2 EtherType OR L2 EtherType
          EtherType                         Controls the inclusion of L2 EtherType filtering in the manageability filter decision (OR
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.
  7:4     Reserved                   0x0    Reserved for additional L2 EtherType AND filters.
  3:0     L2 EtherType AND L2        0x0    L2 EtherType AND L2 EtherType
          EtherType                         Controls the inclusion of L2 EtherType filtering in the manageability filter decision (AND
                                            section).
                                            Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.79 Manageability Decision Filters - MDEF_EXT6 MSB

                        (0x004E)

 Bit(s)    Field Name     Default                                              Description

  15:0    Reserved             0x0     Reserved.

#### 6.2.18.80 Manageability EtherType Filter 0.1 - METF0.1 (0x004F)

 Bit(s)    Field Name     Default                                              Description

  15:0    METF0_L              0x0     METF0 LSB
                                       Loaded to 16 LS bits of METF[0] register.
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.81 Manageability EtherType Filter 0.2 - METF0.2 (0x0050)

 Bit(s)    Field Name     Default                                              Description

  15:0    METF0_M              0x0     METF0 MSB
                                       Loaded to 16 MS bits of METF[0] register (reserved bits in the METF registers should be set in
                                       the NVM to the register’s default values).
                                       Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.82 Manageability EtherType Filter 1.1 - METF1.1 (0x0051)

 Bit(s)    Field Name     Default                                              Description

  15:0    METF1_L              0x0     METF1 LSB
                                       Loaded to 16 LS bits of METF[1] register.
                                       Note: This field is preserved by Intel NVM update tool.

336                                                                                                                       333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.83 Manageability EtherType Filter 1.2 - METF1.2 (0x0052)

 Bit(s)    Field Name      Default                                           Description

  15:0    METF1_M           0x0      METF1 MSB
                                     Loaded to 16 MS bits of METF[1] register (reserved bits in the METF registers should be set in
                                     the NVM to the register’s default values).
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.84 Manageability EtherType filter 2.1 - METF2.1 (0x0053)

 Bit(s)    Field Name      Default                                           Description

  15:0    METF2_L           0x0      METF2 LSB
                                     Loaded to 16 LS bits of METF[2] register.
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.85 Manageability EtherType Filter 2.2 - METF2.2 (0x0054)

 Bit(s)    Field Name      Default                                           Description

  15:0    METF2_M           0x0      METF2 MSB
                                     Loaded to 16 MS bits of METF[2] register (reserved bits in the METF registers should be set in
                                     the NVM to the register’s default values).
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.86 Manageability EtherType Filter 3.1 - METF3.1 (0x0055)

 Bit(s)      Field Name    Default                                           Description

  15:0    METF3_L           0x0      METF3 LSB
                                     Loaded to 16 LS bits of METF[3] register.
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.87 Manageability EtherType Filter 3.2 - METF3.2 (0x0056)

 Bit(s)      Field Name    Default                                           Description

  15:0    METF3_M           0x0      METF3 MSB
                                     Loaded to 16 MS bits of METF[3] register (reserved bits in the METF registers should be set in
                                     the NVM to the register’s default values).
                                     Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                      337
                                     Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                 Non-Volatile Memory Map

#### 6.2.18.88 ARP Response IPv4 Address 0 - LSB (0x0057)

 Bit(s)    Field Name     Default                                         Description

  15:8    Byte 1           0x0      Byte 1
                                    Firmware use.
                                    Note: This field is preserved by Intel NVM update tool.
  7:0     Byte 0           0x0      Byte 0
                                    Firmware use.
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.89 ARP Response IPv4 Address 0 - MSB (0x0058)

 Bit(s)    Field Name     Default                                         Description

  15:8    Byte 3           0x0      Byte 3
                                    Firmware use.
                                    Note: This field is preserved by Intel NVM update tool.
  7:0     Byte 2           0x0      Byte 4
                                    Firmware use.
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.90 IPv6 Address 0 - 0 (0x0059)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.91 IPv6 Address 0 - 1 (0x005A)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.92 IPv6 Address 0 - 2 (0x005B)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.93 IPv6 Address 0 - 3 (0x005C)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

338                                                                                                           333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.18.94 IPv6 Address 0 - 4 (0x005D)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.95 IPv6 Address 0 - 5 (0x005E)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.96 IPv6 Address 0 - 6 (0x005F)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.97 IPv6 Address 0 - 7 (0x0060)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.98 IPv6 Address 1 - 0 (0x0061)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

#### 6.2.18.99 IPv6 Address 1 - 1 (0x0062)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.100                IPv6 Address 1 - 2 (0x0063)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                     339
                                     Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                 Non-Volatile Memory Map

6.2.18.101               IPv6 Address 1 - 3 (0x0064)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.102               IPv6 Address 1 - 4 (0x0065)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.103               IPv6 Address 1 - 5 (0x0066)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.104               IPv6 Address 1 - 6 (0x0067)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.105               IPv6 Address 1 - 7 (0x0068)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.106               IPv6 Address 2 - 0 (0x0069)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

6.2.18.107               IPv6 Address 2 - 1 (0x006A)

 Bit(s)    Field Name     Default                                         Description

  15:0    IPv6 Address     0x0      IPv6 Address
                                    Note: This field is preserved by Intel NVM update tool.

340                                                                                                           333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

6.2.18.108                IPv6 Address 2 - 2 (0x006B)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.109                IPv6 Address 2 - 3 (0x006C)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.110                IPv6 Address 2 - 4 (0x006D)

 Bit(s)    Field Name      Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.111                IPv6 Address 2 - 5 (0x006E)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.112                IPv6 Address 2 - 6 (0x006F)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

6.2.18.113                IPv6 Address 2 - 7 (0x0070)

 Bit(s)      Field Name    Default                                         Description

  15:0    IPv6 Address      0x0      IPv6 Address
                                     Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                     341
                                     Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                               Non-Volatile Memory Map

6.2.18.114              Block CRC8 (0x0071)

 Bit(s)    Field Name    Default                                        Description

  15:8    Block CRC8               Block CRC8
                                   CRC-8-CCITT:
                                    Start Section -> Word: Pass Through Control Words -> Block Length
                                    End Section -> Word: Pass Through Control Words -> IPv6 Address 2 - 7
                                   Note: This field is preserved by Intel NVM update tool.
  7:0     Reserved        0x0      Reserved. Block length in words.

342                                                                                                         333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.19 Flexible TCO Filter Configuration Structure

                         Section

Table 6-25. Flexible TCO Filter Configuration Structure Section Summary Table
                                                                                                              Section
        Word Offset                                                   Description
                                                                                                              Number

0x0000                       Block Length                                                                     6.2.19.1

0x0001                       Flexible Filter Length and Control                                               6.2.19.2

0x0002 + 1*n, n=0...54       Flexible Filter Enable Mask                                                      6.2.19.3

0x0039 + 1*n, n=0...63       Flexible Filter Data                                                             6.2.19.4

0x0079                       Block CRC8                                                                       6.2.19.5

#### 6.2.19.1 Block Length (0x0000)

 Bit(s)     Field Name          Default                                             Description

  15:0     Block Length                    Block Length
                                           Length in words of the section covered by CRC
                                           Section length in words
                                           Note: This field is preserved by Intel NVM update tool.

#### 6.2.19.2 Flexible Filter Length and Control (0x0001)

 Bit(s)          Field Name               Default                                      Description

  15:8     Flexible Filter Length          0x0      Flexible Filter Length (bytes)
           (bytes)                                  Note: This field is preserved by Intel NVM update tool.
  7:5      Reserved                        000b     Reserved.

# 4 Last Filter                      1b      Last Filter

                                                    Note: This field is preserved by Intel NVM update tool.
  3:2      Filter Index (0-3)              01b      Filter Index (0-3)
                                                    Note: This field is preserved by Intel NVM update tool.

# 1 Apply Filter to LAN 1            0b      Apply Filter to LAN

                                                    Note: This field is preserved by Intel NVM update tool.

# 0 Apply Filter to LAN 0            0b      Apply Filter to LAN

                                                    Note: This field is preserved by Intel NVM update tool.

#### 6.2.19.3 Flexible Filter Enable Mask[n] (0x0002 + 1*n, n=0...54)

 Bit(s)          Field Name               Default                                      Description

  15:0     Flexible Filter Enable          0x0      Flexible Filter Enable Mask
           Mask                                     Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                           343
                                           Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                        Non-Volatile Memory Map

#### 6.2.19.4 Flexible Filter Data[n] (0x0039 + 1*n, n=0...63)

 Bit(s)       Field Name           Default                                          Description

  15:0    Flexible Filter Data         0x0    Flexible Filter Data
                                              Note: This field is preserved by Intel NVM update tool.

#### 6.2.19.5 Block CRC8 (0x0079)

 Bit(s)    Field Name        Default                                             Description

  15:8    Block CRC8                     Block CRC8
                                         CRC-8-CCITT:
                                          Start Section -> Word: Flexible TCO Filter Configuration Structure -> Block Length
                                          End Section -> Word: Flexible TCO Filter Configuration Structure -> Flexible Filter Data
                                         Note: This field is preserved by Intel NVM update tool.
  7:0     Reserved               0x0     Reserved. Block length in words.

344                                                                                                                       333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.20 LESM Configurations Section

Table 6-26. LESM Configurations Section Summary Table
                                                                                                                             Section
 Word Offset                                                     Description
                                                                                                                             Number

0x0000           Section Header                                                                                              6.2.20.1

0x0001           LESM Global Configurations                                                                                  6.2.20.2

0x0002           LESM Per State Configurations                                                                               6.2.20.3

0x0003           LESM Per State Configurations LSB                                                                           6.2.20.4

0x0004           LESM Per State Configurations MSB                                                                           6.2.20.5

0x0005           Section Footer                                                                                              6.2.20.6

#### 6.2.20.1 Section Header (0x0000)

 Bit(s)    Field Name       Default                                                Description

  15:8    Reserved           0x0          Reserved.
  7:0     Block Length       0x5          Block Length
                                          Length in words of the section covered by CRC
                                          Block length in words (including the CRC word and not the length word).

#### 6.2.20.2 LESM Global Configurations (0x0001)

 Bit(s)       Field Name              Default                                         Description

  15:6    Reserved                     0x0       Reserved.
  5:1     10G Only Counter             0x3       10G Only Counter
                                                 Number of iterations to go through before enabling 1G parallel detection.

    0 LESM Global                   1b       LESM Global Configurations

          Configurations                          0b = LESM is disabled.
                                                  1b = LESM is enabled.

#### 6.2.20.3 LESM Per State Configurations (0x0002)

 Bit(s)    Field Name       Default                                                Description

  15:1    [New Field]        0x3          [New Field]
                                          Number of iterations to go through before enabling 1G parallel detection.

# 0 State Enable           1b       State Enable

                                           0b = LESM is disabled.
                                           1b = LESM is enabled.

#### 6.2.20.4 LESM Per State Configurations LSB (0x0003)

 Bit(s)        Field Name              Default                                        Description

  15:0    Register Pointer LSB           0x0      Register Pointer LSB

333369-009                                                                                                                          345
                                          Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                       Non-Volatile Memory Map

#### 6.2.20.5 LESM Per State Configurations MSB (0x0004)

 Bit(s)       Field Name          Default                                          Description

  15:0    Register Pointer MSB         0x0       Register Pointer MSB

#### 6.2.20.6 Section Footer (0x0005)

 Bit(s)     Field Name       Default                                             Description

  15:8    Section Footer                     Block CRC8
                                             CRC-8-CCITT:
                                              Start Section -> Word: LESM Configurations (not in SGVL) -> Section Header
                                              End Section -> Word: LESM Configurations (not in SGVL) -> LESM Per State
                                              Configurations MSB
                                             CRC8 of the section above.
  7:0     Reserved               0x0         Reserved.

346                                                                                                                    333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.21 PXE VLAN Configuration Section

Table 6-27. PXE VLAN Configuration Section Summary Table
                                                                                                                          Section
 Word Offset                                                    Description
                                                                                                                          Number

 0x0000              VLAN Block Signature                                                                                 6.2.21.1

 0x0001              Version and Size                                                                                     6.2.21.2

 0x0002              Port 0 VLAN Tag                                                                                      6.2.21.3

 0x0003              Port 1 VLAN Tag                                                                                      6.2.21.4

#### 6.2.21.1 VLAN Block Signature (0x0000)

ASCII 'V', 'L'.

 Bit(s)           Field Name             Default                                     Description

  15:0     VLAN Block Signature          0x4C56    VLAN Block Signature
                                                   Note: This field is preserved by Intel NVM update tool.

#### 6.2.21.2 Version and Size (0x0001)

 Bit(s)     Field Name         Default                                           Description

  15:8     Size                           Size
                                          Length in: 1 Byte unit
                                           First Section -> Word: PXE VLAN Configuration -> VLAN Block Signature
                                           Last Section -> Word: PXE VLAN Configuration -> Port 1 VLAN Tag total size in bytes of
                                           section
                                          Note: This field is preserved by Intel NVM update tool.
  7:0      Version              0x01      Version
                                          Note: This field is preserved by Intel NVM update tool.

#### 6.2.21.3 Port 0 VLAN Tag (0x0002)

  Bit(s)          Field Name                Default                                      Description

  15:13      Priority (0-7)                  0x0         Priority (0-7)
                                                         Note: This field is preserved by Intel NVM update tool.

# 12 Reserved                         0b         Reserved.

                                                         Note: This field is preserved by Intel NVM update tool.
   11:0      VLAN ID (1- 4095)               0x0         VLAN ID (1- 4095)
                                                         Note: This field is preserved by Intel NVM update tool.

333369-009                                                                                                                          347
                                          Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                         Non-Volatile Memory Map

#### 6.2.21.4 Port 1 VLAN Tag (0x0003)

  Bit(s)       Field Name       Default                                   Description

  15:13    Priority (0-7)         0x0      Priority (0-7)
                                           Note: This field is preserved by Intel NVM update tool.

# 12 Reserved               0b       Reserved.

                                           Note: This field is preserved by Intel NVM update tool.
  11:0     VLAN ID (1- 4095)      0x0      VLAN ID (1- 4095)
                                           Note: This field is preserved by Intel NVM update tool.

### 6.2.22 VPD Module Section

Note:      This section is preserved by Intel NVM update tool.

348                                                                                                   333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.23 PBA Number Module Section

Table 6-28. PBA Number Module Section Summary Table
                                                                                                  Section
 Word Offset                                              Description
                                                                                                  Number

0x0000           PBA Section Length                                                               6.2.23.1

0x0001           Word1                                                                            6.2.23.2

0x0002           Word2                                                                            6.2.23.3

0x0003           Word3                                                                            6.2.23.4

0x0004           Word4                                                                            6.2.23.5

0x0005           Word5                                                                            6.2.23.6

#### 6.2.23.1 PBA Section Length (0x0000)

 Bit(s)         Field Name            Default                                       Description

  15:0    PBA Section Length Field      0x6     Length in words of the PBA Block.

#### 6.2.23.2 Word1 (0x0001)

 Bit(s)    Field Name      Default                                         Description

  15:0    Word1 Field                 Word1 Field
                                      PBA Number stored in hexadecimal ASCII values.

#### 6.2.23.3 Word2 (0x0002)

 Bit(s)    Field Name      Default                                         Description

  15:0    Word2 Field                 Word2 Field
                                      PBA Number stored in hexadecimal ASCII values.

#### 6.2.23.4 Word3 (0x0003)

 Bit(s)    Field Name      Default                                         Description

  15:0    Word3 Field                 Word3 Field
                                      PBA Number stored in hexadecimal ASCII values.

#### 6.2.23.5 Word4 (0x0004)

 Bit(s)    Field Name      Default                                          Description

  15:0    Word4 Field                 Word4 Field
                                      PBA Number stored in hexadecimal ASCII values.

333369-009                                                                                               349
                                      Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                               Non-Volatile Memory Map

#### 6.2.23.6 Word5 (0x0005)

 Bit(s)    Field Name    Default                                        Description

  15:0    Word5 Field              Word5 Field
                                   PBA Number stored in hexadecimal ASCII values.

350                                                                                                         333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.24 Mini Loader Module Section

Table 6-29. Mini Loader Module Section Summary Table
                                                                                                                   Section
 Word Offset                                                Description
                                                                                                                   Number

0x0000           Mini Loader Section Header                                                                        6.2.24.1

0x0001           Mini Loader Code                                                                                  6.2.24.2

0x0002           Mini Loader Section Footer                                                                        6.2.24.3

#### 6.2.24.1 Mini Loader Section Header (0x0000)

 Bit(s)    Field Name      Default                                            Description

  15:0    Block Length                Block Length
                                      Length in words of the section covered by CRC.
                                      For now, ROM 0.3 (include len-crc, later only crc).

#### 6.2.24.2 Mini Loader Code (0x0001)

Raw data module length: variable

#### 6.2.24.3 Mini Loader Section Footer (0x0002)

 Bit(s)      Field Name      Default                                            Description

  15:8    CRC8                          CRC8
                                        CRC-8-CCITT:
                                         Start Section -> Word: Mini Loader Module -> Mini Loader Section Header
                                         End Section -> Word: Mini Loader Module -> Mini Loader Code
                                        For now, ML 0.3 code by default: bu in ROM 0.3.
  7:0     Reserved              0x0     Reserved.

333369-009                                                                                                                351
                                      Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                   Non-Volatile Memory Map

### 6.2.25 PHY Config Section

MDIO Indirect Register Programming List.
Address 0xFC2 to 0x1000 has room for 20 registers in case of list expansion in modified images.

Table 6-30. PHY Config Section Summary Table
                                                                                                                Section
 Word Offset                                               Description
                                                                                                                Number

0x0000          Section Length                                                                                   6.2.25.1

0x0001          PMA RX Prov Port0 LSA                                                                            6.2.25.2

0x0002          PMA RX Prov Port0 MSA                                                                            6.2.25.3

0x0003          PMA RX Prov Port0 Data                                                                           6.2.25.4

0x0004          PMA RX Prov Port0 Field Enables                                                                  6.2.25.5

0x0005          PMA RX Prov Port1 LSA                                                                            6.2.25.6

0x0006          PMA RX Prov Port1 MSA                                                                            6.2.25.7

0x0007          PMA RX Prov Port1 Data                                                                           6.2.25.8

0x0008          PMA RX Prov Port1 Field Enables                                                                  6.2.25.9

0x0009          Glob Interrupt Vendor Mask LSA                                                                  6.2.25.10

0x000A          Glob Interrupt Vendor Mask MSA                                                                  6.2.25.11

0x000B          Glob Interrupt Vendor Mask Data                                                                 6.2.25.12

0x000C          Glob Interrupt Vendor Mask Field Enables                                                        6.2.25.13

0x000D          Glob Interrupt Standard Mask LSA                                                                6.2.25.14

0x000E          Glob Interrupt Standard Mask MSA                                                                6.2.25.15

0x000F          Glob Interrupt Standard Mask Data                                                               6.2.25.16

0x0010          Glob Interrupt Standard Mask Field Enables                                                      6.2.25.17

0x0011          CSR RAW1                                                                                        6.2.25.18

0x0012          Section Footer                                                                                  6.2.25.19

#### 6.2.25.1 Section Length (0x0000)

The section length word contains the length of the section in words. Note that section length does not
include a count for the section length word. Section Length = 3*n (n = number of CSRs to configure).

 Bit(s)     Field Name       Default                                         Description

  15:0    Section Length                Section Length
                                        Length in words of the section covered by CRC.
                                        Section length in words.

#### 6.2.25.2 PMA RX Prov Port0 LSA (0x0001)

 Bit(s)    Field Name      Default                                          Description

  15:0    Address LS       0xE400    Address LS

352                                                                                                             333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.25.3 PMA RX Prov Port0 MSA (0x0002)

 Bit(s)    Field Name      Default                                            Description

 15:10    Reserved              0x0    Reserved.
  9:5     Port                  0x0    Port
  4:0     Device                0x1    Device
                                        0x0 = None
                                        0x1 = PMA/PMD
                                        0x3 = PCS
                                        0x7 = Auto-negotiation
                                        0x1D = Clause22 Ext
                                        0x1E = Global
                                        All other values are reserved.

#### 6.2.25.4 PMA RX Prov Port0 Data (0x0003)

 Bit(s)          Field Name           Default                                     Description

# 15 P0 Ena PHY Loopback           0b      P0 Enable PHY Loopback

  14:1    Reserved                     0x0      Reserved.

# 0 P0 MDI Config                 0b      P0 MDI Config

                                                 0b = Normal — MDI normal (ABCD -> ABCD).
                                                 1b = Reverse — MDI reversed (ABCD -> DCBA).
                                                Note: This field is preserved by Intel NVM update tool.

#### 6.2.25.5 PMA RX Prov Port0 Field Enables (0x0004)

 Bit(s)          Field Name           Default                                     Description

# 15 P0 Ena PHY Loopback           0b      P0 Enable PHY Loopback Field Enable

          Field Enable
  14:1    Reserved                     0x0      Reserved.

# 0 P0 MDI Config Field           1b      P0 MDI Config Field Enable

          Enable                                 0b = No Change — No Change to the field.
                                                 1b = Enable — Allow field update.

#### 6.2.25.6 PMA RX Prov Port1 LSA (0x0005)

 Bit(s)      Field Name    Default                                            Description

  15:0    Address LS       0xE400      Address LS

#### 6.2.25.7 PMA RX Prov Port1 MSA (0x0006)

 Bit(s)      Field Name    Default                                            Description

 15:10    Reserved              0x0    Reserved.
  9:5     Port                  0x1    Port

333369-009                                                                                                353
                                       Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                      Non-Volatile Memory Map

 Bit(s)    Field Name      Default                                             Description

  4:0     Device                0x1     Device
                                         0x0 = None
                                         0x1 = PMA/PMD
                                         0x3 = PCS
                                         0x7 = Auto-negotiation
                                         0x1D = Clause22 Ext
                                         0x1E = Global
                                         All other values are reserved.

#### 6.2.25.8 PMA RX Prov Port1 Data (0x0007)

 Bit(s)          Field Name            Default                                     Description

# 15 P1 Ena PHY Loopback            0b      P1 Enable PHY Loopback

  14:1    Reserved                      0x0      Reserved.

# 0 P1 MDI Config                  1b      P1 MDI Config

                                                  0b = Normal — MDI normal (ABCD -> ABCD).
                                                  1b = Reverse — MDI reversed (ABCD -> DCBA).
                                                 Note: This field is preserved by Intel NVM update tool.

#### 6.2.25.9 PMA RX Prov Port1 Field Enables (0x0008)

 Bit(s)          Field Name            Default                                     Description

# 15 P1 Ena PHY Loopback            0b      P1 Enable PHY Loopback Field Enable

          Field Enable
  14:1    Reserved                      0x0      Reserved.

# 0 P1 MDI Config Field            1b      P1 MDI Config Field Enable

          Enable                                  0b = No Change — No Change to the field.
                                                  1b = Enable — Allow field update.

#### 6.2.25.10 Glob Interrupt Vendor Mask LSA (0x0009)

 Bit(s)    Field Name      Default                                             Description

  15:0    Address LS          0xFF01    Address LS

#### 6.2.25.11 Glob Interrupt Vendor Mask MSA (0x000A)

 Bit(s)    Field Name      Default                                             Description

 15:10    Reserved              0x0     Reserved.
  9:5     Port                  0x0     Port

354                                                                                                                333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

 Bit(s)      Field Name     Default                                         Description

  4:0     Device                0x1E     Device
                                          0x0 = None
                                          0x1 = PMA/PMD
                                          0x3 = PCS
                                          0x7 = Auto-negotiation
                                          0x1D = Clause22 Ext
                                          0x1E = Global
                                          All other values are reserved.

#### 6.2.25.12 Glob Interrupt Vendor Mask Data (0x000B)

 Bit(s)        Field Name          Default                                       Description

    15 PMA Vendor Alarm             0b     PMA Vendor Alarm Int Enable

          Int Ena

    14 PCS Vendor Alarm             0b     PCS Vendor Alarm Int Enable

          Int Ena

    13 PHY XS Vendor                0b     PHY XS Vendor Alarm Int Enable

          Alarm Int Ena

# 12 AutoNeg Vendor               0b     Auto-Negotiation Vendor Alarm Int Enable

          Alarm Int Ena

    11 GBE Vendor Alarm             0b     GBE Vendor Alarm Int Enable

          Int Ena
  10:3    Reserved                     0x0    Reserved.

# 2 Global Alarms 1 Int          1b     Global Alarms 1 Int Enable

          Ena

# 1 Global Alarms 2 Int          0b     Global Alarms 2 Int Enable

          Ena

# 0 Global Alarms 3 Int          1b     Global Alarms 3 Int Enable

          Ena

#### 6.2.25.13 Glob Interrupt Vendor Mask Field Enables (0x000C)

 Bit(s)        Field Name          Default                                       Description

    15 PMA Vendor Alarm             0b     PMA Vendor Alarm Int Field Enable

          Int Field Ena

    14 PCS Vendor Alarm             0b     PCS Vendor Alarm Int Field Enable

          Int Field Ena

    13 PHY XS Vendor                0b     PHY XS Vendor Alarm Int Field Enable

          Alarm Int Field Ena

# 12 AutoNeg Vendor               0b     Auto-Negotiation Vendor Alarm Int Field Enable

          Alarm Int Field Ena

    11 GBE Vendor Alarm             0b     GBE Vendor Alarm Int Field Enable

          Int Field Ena
  10:3    Reserved                     0x0    Reserved.

# 2 Global Alarms 1 Int          1b     Global Alarms 1 Int Field Enable

          Field Ena

# 1 Global Alarms 2 Int          0b     Global Alarms 2 Int Field Enable

          Field Ena

# 0 Global Alarms 3 Int          1b     Global Alarms 3 Int Field Enable

          Field Ena

333369-009                                                                                     355
                                         Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                    Non-Volatile Memory Map

#### 6.2.25.14 Glob Interrupt Standard Mask LSA (0x000D)

 Bit(s)    Field Name      Default                                          Description

  15:0    Address LS          0xFF00    Address LS

#### 6.2.25.15 Glob Interrupt Standard Mask MSA (0x000E)

 Bit(s)    Field Name      Default                                          Description

 15:10    Reserved             0x0      Reserved.
  9:5     Port                 0x0      Port
  4:0     Device              0x1E      Device
                                         0x0 = None
                                         0x1 = PMA/PMD
                                         0x3 = PCS
                                         0x7 = Auto-negotiation
                                         0x1D = Clause22 Ext
                                         0x1E = Global
                                         All other values are reserved.

#### 6.2.25.16 Glob Interrupt Standard Mask Data (0x000F)

 Bit(s)          Field Name            Default                                  Description

    15 PMA Standard Alarm 1           0b      PMA Standard Alarm 1 Int Enable

          Int Ena

    14 PMA Standard Alarm 2           0b      PMA Standard Alarm 2 Int Enable

          Int Ena

    13 PCS Standard Alarm 1           0b      PCS Standard Alarm 1 Int Enable

          Int Ena

    12 PCS Standard Alarm 2           0b      PCS Standard Alarm 2 Int Enable

          Int Ena

    11 PCS Standard Alarm 3           0b      PCS Standard Alarm 3 Int Enable

          Int Ena

    10 PHY XS Standard Alarm          0b      PHY XS Standard Alarm 1 Int Enable

# 1 Int Ena

    9 PHY XS Standard Alarm          0b      PHY XS Standard Alarm 2 Int Enable

# 2 Int Ena

# 8 AutoNeg Standard               0b      Auto-Negotiation Standard Alarm 1 Int Enable

          Alarm 1 Int Ena

# 7 AutoNeg Standard               0b      Auto-Negotiation Standard Alarm 2 Int Enable

          Alarm 2 Int Ena

# 6 GbE Standard Alarm 1           0b      GbE Standard Alarm 1 Int Enable

          Int Ena
  5:1     Reserved                      0x0      Reserved.

# 0 All Vendor Alarms Int          1b      All Vendor Alarms Int Enable

          Ena

356                                                                                                              333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

#### 6.2.25.17 Glob Interrupt Standard Mask Field Enables (0x0010)

 Bit(s)          Field Name         Default                                      Description

    15 PMA Standard Alarm 1          0b     PMA Standard Alarm 1 Int Field Enable

          Int Field Ena

    14 PMA Standard Alarm 2          0b     PMA Standard Alarm 2 Int Field Enable

          Int Field Ena

    13 PCS Standard Alarm 1          0b     PCS Standard Alarm 1 Int Field Enable

          Int Field Ena

    12 PCS Standard Alarm 2          0b     PCS Standard Alarm 2 Int Field Enable

          Int Field Ena

    11 PCS Standard Alarm 3          0b     PCS Standard Alarm 3 Int Field Enable

          Int Field Ena

    10 PHY XS Standard Alarm         0b     PHY XS Standard Alarm 1 Int Field Enable

# 1 Int Field Ena

    9 PHY XS Standard Alarm         0b     PHY XS Standard Alarm 2 Int Field Enable

# 2 Int Field Ena

# 8 AutoNeg Standard              0b     Auto-Negotiation Standard Alarm 1 Int Field Enable

          Alarm 1 Int Field Ena

# 7 AutoNeg Standard              0b     Auto-Negotiation Standard Alarm 2 Int Field Enable

          Alarm 2 Int Field Ena

# 6 GbE Standard Alarm 1          0b     GbE Standard Alarm 1 Int Field Enable

          Int Field Ena
  5:1     Reserved                      0x0    Reserved.

# 0 All Vendor Alarms Int         1b     All Vendor Alarms Int Field Enable

          Field Ena

#### 6.2.25.18 CSR RAW1 (0x0011)

Raw data module length: variable
The section length word contains the length of the section in words. Note that section length does not
include a count for the section length word. Section Length = 3*n (n = number of CSRs to configure).

#### 6.2.25.19 Section Footer (0x0012)

 Bit(s)      Field Name       Default                                          Description

  15:8    CRC8                            CRC8
                                          CRC-8-CCITT:
                                           Start Section -> Word: PHY Config -> Section length
                                           End Section -> Word: PHY Config -> CSR RAW1
  7:0     Reserved                0x0     Reserved. Block length in words.

333369-009                                                                                          357
                                        Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

### 6.2.26 PCIe Link (LCB) Configuration Section

Table 6-31. PCIe Link (LCB) Configuration Section Summary Table
                                                                                                                        Section
 Word Offset                                                 Description
                                                                                                                        Number

0x0000          Section Length                                                                                          6.2.26.1

0x0001          Reg Write Indirect List                                                                                 6.2.26.2

#### 6.2.26.1 Section Length (0x0000)

 Bit(s)     Field Name       Default                                            Description

  15:0    Section Length                  Section Length
                                          Length in: 2 Bytes unit - 1
                                           First Section -> Word: PCIe Link (LCB) Configuration -> Section Length
                                           Last Section -> Word: PCIe Link (LCB) Configuration -> Reg Write Indirect List

#### 6.2.26.2 Reg Write Indirect List (0x0001)

Raw data module length: variable

### 6.2.27 PCIe Analog Configuration Module Section

Table 6-32. PCIe Analog Configuration Module Section Summary Table
                                                                                                                        Section
 Word Offset                                                 Description
                                                                                                                        Number

0x0000          Section Length                                                                                          6.2.27.1

0x0001          PCI PHY FW                                                                                              6.2.27.2

#### 6.2.27.1 Section Length (0x0000)

 Bit(s)     Field Name       Default                                            Description

  15:0    Section Length                  Section Length
                                          Length in: 2 Bytes unit - 1
                                           First Section -> Word: PCIe* Analog Configuration Module -> Section Length
                                           Last Section -> Word: PCIe* Analog Configuration Module -> PCI PHY FW

#### 6.2.27.2 PCI PHY FW (0x0001)

Raw data module length: variable

358                                                                                                                     333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

6.2.28               2'nd Init Module Section

Table 6-33. 2'nd Init Module Section Summary Table
                                                                                      Section
 Word Offset                                            Description
                                                                                      Number

0x2000           Data                                                                 6.2.28.1

#### 6.2.28.1 Data (0x2000)

 Bit(s)    Field Name       Default                                    Description

  15:0    Data              0xFFFF    Data

### 6.2.29 FCoE Scratch Pad Section

Length is (4KB * FCoE Scratch Pad Size). For 2M flash, max is 16KB (8192 words).

Table 6-34. FCoE Scratch Pad Section Summary Table
                                                                                      Section
 Word Offset                                            Description
                                                                                      Number

0x0000           Reserved                                                             6.2.29.1

#### 6.2.29.1 Reserved (0x0000)

 Bit(s)    Field Name       Default                                    Description

  15:0    Reserved          0xFFFF    Reserved.

333369-009                                                                                   359
                                      Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                     Non-Volatile Memory Map

### 6.2.30 Firmware Module Section

0x6000 -- 500K for each large section (2MB flash, 488K used for now).
0x4000 + FCoE size -- 512K for each large section (flash larger than 2MB).

Table 6-35. Firmware Module Section Summary Table
                                                                                                  Section
 Word Offset                                    Description
                                                                                                  Number

0x0000         FW 2M                                                                               6.2.30.1

#### 6.2.30.1 FW 2M (0x0000)

Raw data module length: variable

### 6.2.31 PXE/OROM Module Section

0x45800 -- 500K for each large section (2MB flash, 488K used for now).
0x44000 + FCoE size -- 512K for each large section (flash larger than 2MB).

Table 6-36. PXE/OROM Module Section Summary Table
                                                                                                  Section
 Word Offset                                    Description
                                                                                                  Number

0x0000         OROM 2M                                                                             6.2.31.1

#### 6.2.31.1 OROM 2M (0x0000)

Raw data module length: variable
Note:    This word is preserved by Intel NVM update tool.

360                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.2.32 AQ PHY Module Section

0x83000 -- 500K for each large section (2MB flash, 488K used for now).
0x86000 + FCoE size -- 512K for each large section (flash larger than 2MB).

Table 6-37. AQ PHY Module Section Summary Table
                                                                                     Section
 Word Offset                                           Description
                                                                                     Number

0x0000          PHY 2M                                                               6.2.32.1

#### 6.2.32.1 PHY 2M (0x0000)

Raw data module length: variable

### 6.2.33 Free Provisioning Module Section

0xC1800 -- 500K for each large section (2MB flash, 488K used for now).
0xC6000 + FCoE size -- 512K for each large section (flash larger than 2MB).

Table 6-38. Free Provisioning Module Section Summary Table
                                                                                     Section
 Word Offset                                           Description
                                                                                     Number

0x0000          Reserved                                                             6.2.33.1

#### 6.2.33.1 Reserved (0x0000)

 Bit(s)    Field Name      Default                                    Description

  15:0    Reserved         0xFFFF    Reserved.

333369-009                                                                                  361
                                     Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                              Non-Volatile Memory Map

NOTE:   This page intentionally left blank.

362                                                                                        333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Chapter 7                     Inline Functions
