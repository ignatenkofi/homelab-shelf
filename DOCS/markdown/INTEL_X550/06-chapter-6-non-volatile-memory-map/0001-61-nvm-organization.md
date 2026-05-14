## 6.1 NVM Organization

The X550 NVM contains the following six high-level modules:
 • Legacy EEPROM Modules — These modules are mapped over one of the first two 16 KB sections
   of the Flash device, and cannot be extended beyond them. It is composed of all the NVM modules
   used by MAC hardware or by manageability firmware, not including the manageability and PHY
   firmware code images. The sections included in this block are:
     — NVM Pointers and Generic Words — This section (described in Section 6.1) start is at the
       beginning of the valid section. It contains basic device information, pointers to other NVM
       modules, and several software configurations.
     — PCI Analog Module — This module is pointed by NVM word 0x2, and contains settings for the
       PCI PHY block. It is loaded only at Power On Reset.
     — LCB Module — This module is pointed by NVM word 0x3, and contains settings for the PCI Link
       Layer block. It is loaded at each PCI reset.
     — PCIe Modules — These modules (described in Section 6.2.6 and Section 6.2.7) contain the
       parameters required to configure the PCIe configuration space. The pointers to these modules
       are located at NVM words 0x6 (Generic), 0x7 (Port 0), and 0x8 (Port 1).
     — LAN Core Modules — These two modules (described in Section 6.2.5) contain parameters
       required to configure the LAN port. These include the MAC Address, LED, and SDP
       configuration. The pointers to these modules are located at NVM words 0x9 (Port 0) and 0xA
       (Port 1). In addition, each LAN port has a module that enables loading specific CSR values after
       reset. The pointers to these modules are located at NVM words 0xD (Port 0) and 0xE (Port 1).
       These modules are loaded following a software or hardware reset.
     — Firmware Parameters Module — Pointed by Firmware Module Pointer located at NVM word
       0x0F. The Firmware Extension Module starts with a list of firmware sub-modules pointers, as
       listed in Section 6.2.13.
     — Boot Configuration — This module is pointed by NVM word 0x17, and contains the
       configuration parameters used by the PXE, iSCSI and FCoE boot code.
     — VPD — This module is pointed by NVM word 0x2F, and contains the VPD module exposed via
       the VPD PCIe capability as described in Section 6.2.2.48.
 • Firmware Image — This module contains the main code of the firmware loaded to the internal
   RAM. This image must fit within 512 KB and start at a 4 KB boundary. This module is authenticated
   upon update. See Section 6.1.4 for details.
 • PCIe Expansion/Option ROM — This module includes the PXE Driver (61 KB), iSCSI Boot Image
   (116 KB), FCoE Boot Image (80 KB), UEFI Network Driver (37 KB for x64, 67 KB for IA64), and can
   also include a CLP module (60 KB). It must fit within 512 KB and start at a 4 KB boundary. It is
   pointed by the PCIe Expansion/Option ROM Pointer located at the NVM word 0x05.
 • PHY Image — This module includes the PHY micro controller Boot Vector section, two PHY
   registers provisional segments (one per port), and a PHY micro controller code/data segment. The
   PHY registers provisional segments are used to change the defaults of PHY registers. It must fit
   within 512 KB and start at a 4 KB boundary. The PHY Image Pointer is located at NVM word 0x04.

333369-009                                                                                          215
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                  Non-Volatile Memory Map

 • FCoE Scratch Pad — A scratch pad used for FCoE software usage. The location of this area is
   described in the module pointed by word 0x39. The minimal allocated size is 8 KB, but can be larger
   if there is additional free area available in the NVM. The scratch pad is open to software read or
   write. Software device driver is responsible for the maintenance of this area.
 • Free Space Provisioning Segment — The NVM structure includes a space utilized to update the
   PXE code, Firmware Image, and PHY Image modules via a double image policy. This space is
   referred as the Free Space Provisioning module or segment. It must be large enough to contain the
   largest of these three high-level modules, which means at least 512 KB in a 4 MB flash and 500 KB
   in a 2 MB flash. It is pointed by the Free Space Provisioning Segment Pointer located at NVM word
   0x40. See Section 3.4.8.1 for the usage model of this Flash area.
Note:    Flash device size can be read from NVM Control Word 1 (see Section 6.2.2.1).
Figure 6-1 shows a general NVM structure and not a required order.

                             0x1FFFFF
                                              FCoE Scratch Pad              at least 8 KB

                                          Free Space Provisioning
                                                 Segment                   up to 500/512 KB

                                                  used by
                                             double image policy
                            0xZZZ000

                                        PHY Microcontroller Code/Data

                                                                           PHY Image,
                                          PHY 1 Registers Provisional     up to 500/512 KB
                                          PHY 0 Registers Provisional

                            0xYYY000    PHY Microcontroller Boot Vector

                                        PCIe Expansion/Option ROM          up to 500/512 KB

                            0xXXX000

                                          Firmware Image Module            up to 500/512 KB

                             0xVVV000

                            0x007FFF
                                          Legacy EEPROM Modules            16 KB Section 1
                            0x004000
                            0x003FFF
                                          Legacy EEPROM Modules            16 KB Section 0
                            0x000000
                         Byte Address

Figure 6-1.   NVM Structure

216                                                                                                            333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.1.1 Protected Areas

The following areas are protected from host writes:
       • The Firmware Code Area
       • The PHY code Area
       • The PCI configuration areas (PHY, Link)
       • The pointers to the different modules.
       • The mini loader
       • NVM Control Words 1/2/4
The list of words and modules that are read-only to the software is listed in Table 6-1.
The Firmware, PHY code areas, and Option ROM can be updated using the flow described in
Section 3.4.8.1.
Read/Write words can be updated using the flow described in Section 3.4.7.6 and Section 3.4.2.1.

### 6.1.2 NVM Header

Note:             Intel configures the reserved NVM fields, and they are not intended to be changed
                  beyond the default image provided by Intel.
Table 6-1 lists the fixed part of the Legacy EEPROM Modules used by the X550. This table lists common
modules for the NVM including: hardware pointers, software and firmware. Blocks pointed in this
section are detailed in the following sections. All addresses in this table are absolute in word units.
Pointers may be in word units or in 4 KB units. If bit 15 of the pointer is set, bits [14:0] point to a 4 KB
sector, and the word address is {pointer[14:0], 000,0000,0000b}. If bit 15 is cleared, the word address
is pointer[14:0].

Table 6-1.           Legacy EEPROM Modules Description
Note

         Word
                     Used By                            Field Name                          LAN 0/1         RO to Host
        Address

   0x00                HW      NVM Control Word 1                                         Shared Logic      RO Word

   0x01                HW      NVM Control Word 2                                         Shared Logic      RO Word

                                                                                                            RO Pointer1
   0x02                HW      PCIe Analog Module Pointer                                 Shared Logic
                                                                                                            RO Module

                                                                                                            RO Pointer
   0x03                HW      PCIe Link Configuration Module Pointer                     Shared Logic
                                                                                                            RO Module1

                                                                                                            RO Pointer2
   0x04                HW      PHY Module Pointer                                         Shared Logic
                                                                                                            RO Module

   0x05                HW      PCIe Expansion/Option ROM Pointer                        SW + Shared Logic   RO Module2

   0x06                HW      PCIe General Configuration Module Pointer                  Shared Logic

   0x07                HW      PCIe Configuration Space 0 Module Pointer                   Function 0

   0x08                HW      PCIe Configuration Space 1 Module Pointer                   Function 1

   0x09                HW      LAN Core 0 Module Pointer                                     Port 0

   0x0A                HW      LAN Core 1 Module Pointer                                     Port 1

333369-009                                                                                                            217
                                        Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                Non-Volatile Memory Map

Table 6-1.    Legacy EEPROM Modules Description [continued]
   Word
              Used By                             Field Name                                LAN 0/1         RO to Host
  Address

                                                                                                           RO Pointer
0x0B            HW      MAC 0 Module Pointer                                                  Port 0
                                                                                                           RO Module1

                                                                                                           RO Pointer
0x0C            HW      MAC 1 Module Pointer                                                  Port 1
                                                                                                           RO Module1

                                                                                                           RO Pointer
0x0D            HW      CSR 0 Auto Configuration Module Pointer                               Port 0
                                                                                                           RO Module1

                                                                                                           RO Pointer
0x0E            HW      CSR 1 Auto Configuration Module Pointer                               Port 1
                                                                                                           RO Module1

0x0F            FW      Firmware Module Pointer                                                FW

0x10 – 0x14     SW      SW Compatibility Module                                                SW

0x15 – 0x16     SW      PBA Bytes 1...4                                                        SW

0x17          SW + FW   Boot Configuration Start Address                                     SW+FW

0x18          SW + FW   NVM Dev Starter Version                                              SW+FW

0x19          SW + FW   PHY Firmware Version                                                 SW+FW

0x1A – 0x26     SW      Software Reserved                                                      SW

0x27            SW      Alternate SAN MAC Address Pointer                                      SW

0x28            SW      Active SAN MAC Address Pointer                                         SW

0x29            SW      Map Version                                                            SW

0x2A            SW      Image Revision                                                         SW

0x2B            SW      Software Reserved                                                      SW

0x2C            SW      Platform/NIC/LOM Specific Capabilities                                 SW

0x2D – 0x2E     SW      eTrack_ID number                                                       SW

                                                                                                           RO Pointer3
0x2F           OEM      VPD Pointer                                                        Shared Logic
                                                                                                           RO Section

0x30 – 0x36     PXE     PXE Configuration Words                                                SW

0x37          SW + FW   Alternate Ethernet MAC Addresses Pointer                             SW+FW

0x38            HW      NVM Control Word 3                                                 Shared Logic

0x39            SW      FCoE Scratch Pad Structure Pointer                                     SW

                                                                                                           RO Pointer2
0x3A            FW      Firmware Code Pointer                                                  FW
                                                                                                           RO Module

0x3B – 0x3E     HW      Hardware Reserved                                                   Reserved

0x3F          SW+FW     Software Checksum, Words 0x00 — 0x3F                               Shared Logic

0x40            FW      Free Space Provisioning Segment Pointer                                FW          RO Pointer

                        Free Provisioning Area Size, expressed in 4KB sectors. Default
0x41            FW                                                                             FW          RO Word
                        is 0x80 for 4MB flash and 0x71 for 2 MB flash.

                                                                                                           RO Pointer
0x42            FW      Mini Loader Pointer                                                    FW
                                                                                                           RO Module1

                                                                                                           RO Pointer
0x43            FW      PHY Configuration                                                      FW
                                                                                                           RW Module

218                                                                                                          333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-1.        Legacy EEPROM Modules Description [continued]
    Word
                 Used By                               Field Name                                 LAN 0/1          RO to Host
   Address

 0x44 – 0x4F                 Reserved

                             RO Updates Version - This field is copied by firmware from the
 0x50               FW       RO Updates Version field present in the trailer of the firmware          FW           RO Word
                             secured module. Refer to Section 6.1.4.2.

1. Updated via RO words mechanism.
2. Updated via the secured module update flow (Section 3.4.8.1).
3. VPD area is updated via the VPD PCIe capability or via Shadow RAM Update host I/F command if VPD Write Enable bit in NVM
    Control Word 1 is set.
All pointers refer to word addresses, except pointers to PCIe Expansion/Option ROM (0x5), PHY Image (0x4), Firmware Code (0x3A)
         and Free Space Provisioning Segment (0x41) which are expressed in 4 KB sector units.

### 6.1.3 Hardware Sections

This module contains address control words and hardware pointers indicated as hardware in Table 6-1.
The process of loading this module (or any of it sub-modules) into the device is referred as MAC
auto-load process. These modules must be mapped in the first valid 16 KB section of the Flash.

#### 6.1.3.1 Hardware Section — Auto-Load Sequence

The following table lists sections of auto-read following device reset events or specific commands from
registers. Auto-read is performed from the internal Shadow RAM (or from internal memory for PHY
module) and not from the NVM device, except following LAN_PWR_GOOD or Reset Pin events.

Table 6-2.        NVM Section Auto-Read
                                              PCIe       D3 to
                             LAN_PWR_                                          SW         Link
                                              Reset       D0           FLR                                         PHY Image
                                                                              Reset      Reset    FW       Force
                              GOOD or        or PCIe    Transit       (per                                          Re-Load
                                                                              (per       (per    Reset      TCO
                              Reset Pin      Inband      (per         port)                                        Command1
                                                                              port)      port)
                                              Reset      port)

 PCIe Analog Configuration        X2

 PCI Link Configuration
                                                X
 (LCB)

 PCIe General
                                                X
 Configuration

 PCIe Function 0/1 Config
                                                X
 Space (for each function)

 LAN Core and CSRs (for
                                   X            X           X          X         X         X                X
 each LAN port)

 PHY Module (for each LAN
                                   X                                                                                   X
 port)

 Manageability Firmware
                                   X                                                              X
 Module

1. via MDIO (per port) PHY register bit 1E.C442.0
2. This is the unique module that requires power-up to be reloaded.

333369-009                                                                                                                   219
                                        Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                             Non-Volatile Memory Map

### 6.1.4 Firmware Image Module

The firmware image module contains the main code of the internal firmware loaded to the internal RAM.
This module includes a header and a trailer. The header is used when the firmware is updated to
authenticate it. The optional trailer includes a list of Read only words to be modified by the firmware or
a new version of the first 16 KB of the NVM.

#### 6.1.4.1 Header of Firmware Image Module

Since authenticated modules are by-definition not modifiable in the fields, no “holes” are present in
such modules.
Table 6-3 shows the header of the Firmware Image module. Fields colored in light blue are protected by
the authentication signature.

Table 6-3.      Header of Firmware and Option ROM Images
                 Number of
  Byte Offset                   Field or Segment Name                       Description and Comments
                  Words

0x00 – 0x7F         64       Authentication Header

0x80 – 0x17F        128      RSA Public Key                 This field is skipped for the sake of SHA256 Hash computing.

0x180 – 0x183        2       RSA Exponent                   This field is skipped for the sake of SHA256 Hash computing.

0x184 – 0x283       128      Encrypted SHA256 Hash          This field is skipped for the sake of SHA256 Hash computing.

                                                            A unique ND-provided device ID that identifies the X550
0x284 – 0x285        1       X550 Blank NVM Device ID       controller among other ND controllers. It must be set to
                                                            0x1562 in the X550.

                                                            It is the maximum flash area expressed in words that can be
                                                            used by the module, starting from authentication header
0x286 – 0x289        2       Max Module Area
                                                            (included). It is set to 256 K words (i.e. 512 KB) for all
                                                            modules.

                                                            It is the flash area expressed in words that is currently used
0x28A – 0x28D        2       Current Module Area            by the module, starting from authentication header
                                                            (included).

                                                            Bit[15] =      CRC8 field is used. Set to 1b if a CRC8 is
                                                                           computed over the module, set to 0b otherwise.
                                                            Bits[14:8] = Module format version. Set to 0x02 is this
                                                                           currently defined format is used.
                                                            Bits[7:0] = CRC8 value computed over the parent module
0x28E – 0x28F        1       Module Format Version + CRC8                  only, starting from authentication header
                                                                           (included) and including all other module’s fields
                                                                           and segments – excluding all descendant
                                                                           modules and RSA Public Key/RSA Exponent
                                                                           fields.
                                                            CRC8 field is skipped for the sake of CRC8 computing (when
                                                            bit 15 is set to 0b).

                                                            Bits[15:8] = Major revision number.
0x290 – 0x291        1       Code Revision
                                                            Bits[7:0] = Minor revision number.

0x292 – 0x293        1       Reserved Spare Word            Must be zeroed.

                                                            Length of the parent module contents expressed in words,
                                                            module header and Parent Module Length field excluded. It
                                                            excludes all the descendant modules. It must be set to N.
                                                            Modules read by firmware are NOT size limited to 128 KB.
0x294 – 0x297        2       Parent Module Length
                                                            It excludes the last 16 KB sector of the firmware image which
                                                            is reserved for the RO Commands section.
                                                            This field is not relevant for option ROM header and should be
                                                            zeroed.

220                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

Table 6-3.        Header of Firmware and Option ROM Images [continued]
                      Number of
  Byte Offset                           Field or Segment Name                      Description and Comments
                       Words

...                               parent word 1
                                                                   Format of the contents of firmware modules is specific to
                                  parent word 2                    each module.
                         N
                                  ...                              This field is not relevant for option ROM header and should be
                                                                   zeroed.
                                  parent word N

#### 6.1.4.2 Trailer of the Firmware Image Module

Table 6-4 shows the format of the last 16 KB sector of the firmware image. Fields colored in light blue
are protected by the authentication signature.

Table 6-4.        RO Commands Section Format
 Number of
                      Field or Segment Name                                 Description and Comments
  Words

                                                    Default is 0xFFFF, which means the section is empty and the remaining words
                                                    are discarded. A null field here indicates that the next words up to the 16 KB

    1 RO Commands Version

                                                    sector's end contain the new Shadow RAM contents, starting from word
                                                    0x000 up to word 0x0x1FF7 included.

                                                    A unique ND-provided device ID that identifies the X550 controller among

# 1 X550 Blank NVM Device ID

                                                    other ND controllers. It must be set to 0x1562 in the X550.

                                                    Minimum Firmware Code Revision number required for being able to parse
                                                    the RO Commands section.

# 1 Minimum Firmware Code Revision

                                                    It must be less than or equal to the Code Revision number read from the
                                                    Firmware Image Header listed in Table 6-3.

    1 RO Commands Length                  Length in words (N), starting from next word.

                RO Commands word 1

                RO Commands word 2
      N                                             Format of the RO Commands is described in Section 6.1.4.2.1.
                ...

                RO Commands word N

6.1.4.2.1                  Format of the RO Commands

The RO Commands words can contains the following three structures:
 • Shadow RAM Word Write Command (2 words)
 • CSR Write Command (4 words)
 • Shadow RAM contents, from word 0x0 to 0x1FF7 included
The first two structures starts with a type field.
Table 6-5 describes the different commands types:

333369-009                                                                                                                     221
                                        Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                            Non-Volatile Memory Map

Table 6-5.       RO Commands Types
         Type                                                     Description

        xxx1b          Word auto-load.

        0100b          CSR auto-load with port number.

         Other         Invalid type, parsing is stopped here.

                                             Word Address[14:0]                                           Type
                                                   15b                                                   1b=1'b1

                                                   Word Data[15:0]
                                                        16b

Figure 6-2.      Shadow RAM Word Write Command

                          CSR Address [11:2]                                Port               Type
                                10b                                          2b             4b=4'b0100

                                                 CSR Address [27:12]
                                                       16b

                                                   CSR Data[31:16]
                                                        16b

                                                    CSR Data[15:0]
                                                         16b

Figure 6-3.      CSR Write Command (with Port Number)

If the Port value is invalid, the command is ignored.

### 6.1.5 PCIe Expansion/Option ROM

This module might include the PXE driver, iSCSI boot and/or FCoE boot image, UEFI network driver, and
a Command Line Protocol (CLP) module. It is made of a single combo module (no pointers to sub-
sections) and must fit into 512 KB.
It is not required for LOM systems where it may be stored on the BIOS Flash device.
The module is pointed by the PCIe expansion/option ROM pointer at NVM word 0x05, expressed in 4 KB
sector units. Whenever modifying this pointer in the NVM, it is required to issue a PCIe reset before any
new access is performed to the Expansion ROM. Otherwise the X550 would continue to use the old
pointer each time it internally maps accesses to the expansion ROM. Refer to Section 3.4.3.1.
The first 330 words listed in Table 6-3 (up to the Reserved spare word) are mapped at the end of the
area allocated to the module (a trailer), though for the sake of the authentication, these words are
mapped at the module's header, as listed in the table.

222                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

### 6.1.6 PHY Module

Refer to Section 3.7.3.3 for the way this module is used by the X550.
The module is pointed by the PHY module pointer at NVM word address 0x4 (or word address 0x2004),
expressed in 4 KB sector units. Before performing an auto-load, the PHY reads this pointer directly from
the NVM.
The PHY module is composed of the following three sections as shown in Figure 6-4:
 • Header — Provides configuration information for the SPI interface and pointers to the Instruction
   RAM and Data RAM locations. (See Table 6-6 for detailed description of the header content).
 • Instruction RAM — This section of the image is loaded into the instructional SRAM (ISRAM).
 • Data RAM — This section of the image is loaded into the data SRAM (DSRAM).

Figure 6-4.     PHY Module Map

Table 6-6.      PHY Module Header
  Byte Offset                                                    Description

0x00 – 0x7F     Authentication Header.

0x80 – 0x17F    RSA Public Key — This field is skipped for the sake of SHA256 Hash computing.

0x180 – 0x183   RSA Exponent — This field is skipped for the sake of SHA256 Hash computing.

0x184 – 0x283   Encrypted SHA256 Hash — This field is skipped for the sake of SHA256 Hash computing.

                X550 Blank NVM Device ID — A unique ND-provided device ID that identifies the X550 controller among other
0x284 – 0x285
                ND controllers. It must be set to 0x1562 in the X550.

                Max Module Area — It is the maximum flash area expressed in words that can be used by the module, starting
0x286 – 0x289
                from authentication header (included). It is set to 256 K words (i.e. 512 KB) for all modules.

                Current Module Area — It is the flash area expressed in words that is currently used by the module, starting
0x28A – 0x28D
                from authentication header (included).

333369-009                                                                                                                     223
                                   Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                     Non-Volatile Memory Map

Table 6-6.       PHY Module Header [continued]
  Byte Offset                                                      Description

                  Module Format Version + CRC8:
                   Bit[15] =     CRC8 field is used. Set to 1b if a CRC8 is computed over the module, set to 0b otherwise.
                   Bits[14:8] = Module format version. Set to 0x02 is this currently defined format is used.
 0x28E – 0x28F     Bits[7:0] = CRC8 value computed over the parent module only, starting from authentication header
                                 (included) and including all other module’s fields and segments - excluding all descendant
                                 modules and RSA Public Key/RSA Exponent fields.
                  CRC8 field is skipped for the sake of CRC8 computing (when bit 15 is set to 0b).

                  Code Revision:
 0x290 – 0x291     Bits[15:8] = Major revision number.
                   Bits[7:0] = Minor revision number.

 0x292 – 0x2FF    Reserved Spare Words — Must be set to zero.

 0x300                                                         SPI Clock Divider[7:0]

 0x301                                                    Daisy Chain Clock Divider[7:0]

 0x302                                                            Wait Timer[7:0]

 0x303                                                           Wait Timer[15:8]

 0x304                                                     MCP IRAM Head Pointer[7:0]

 0x305                                                     MCP IRAM Head Pointer[15:8]

 0x306                                                    MCP IRAM Head Pointer[23:16]

 0x307                                                      MCP IRAM Byte Length[7:0]

 0x308                                                     MCP IRAM Byte Length[15:8]

 0x309                                                    MCP IRAM Byte Length[23:16]

 0x30A                                                     MCP DRAM Head Pointer[7:0]

 0x30B                                                    MCP DRAM Head Pointer[15:8]

 0x30C                                                    MCP DRAM Head Pointer[23:16]

 0x30D                                                     MCP DRAM Byte Length[7:0]

 0x30E                                                     MCP DRAM Byte Length[15:8]

 0x30F                                                    MCP DRAM Byte Length[23:16]

 0x310                                      {Timeout Configuration[3:0], Reserved[2:0], Enabled CRC}

 0x311                                                               Reserved

 0x312                                                               Reserved

 0x313                                                               Reserved

 0x314                                                               Reserved

 0x315                                                               Reserved

 0x316                                                        Expected CRC16[7:0]1

 0x317                                                        Expected CRC16[15:8]

1. Calculated from 0x300 to the end of the PHY code.

224                                                                                                                    333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Non-Volatile Memory Map

The PHY module is organized as follows, where offsets are expressed in bytes from the beginning of the
module:
 • 0x00000000 – 0x00000317: Header (see Table 6-6).
 • 0x00000318 – 0x000004BF: Reset Vector (processor jumps here on reset).
    This small assembly language routine sets up basic processor functions and loads the IRAM and
    DRAM memories. When memories are initialized, they jump to the start up code in the IRAM.
 • 0x000004C0 – 0x000005BF: Register Provisioning Table.
    One of the first things that’s done at reset is to override the PIF registers with registers from these
    tables. A utility is available that manages this table called provision.
    Defaults to PHY interrupts mask registers must always be provisioned here because they impact the
    PHY’s operation with the MC before the operating system is up.
 • 0x000005C0 – 0x000005FF: Version String (62 bytes), Firmware major/minor revision numbers (2
   bytes).
 • 0x00000600 – Current Module Area: IRAM/DRAM load tables and contents.
    The boot code uses the load table and data in this region to initialize IRAM and DRAM.

### 6.1.7 Register Provisional Table

The PHY registers provisioning table consists of a variable number of change lists, the minimum number
of change list is zero, and the maximum number is limited only by the size of the table, 256 bytes
shared by both ports.
There is a master provisioning list that applies to both PHYs in addition to separate PHY specific changes
lists (to reduce the table size).
Each change list consists of a 4-byte header and at least one change specification. The header consists
of a one byte PHY identifier, a one byte MMD device address, and a two bytes count of change
specifications to follow. Master provisioning is identified by a 0xFF PHY identifier.
Each change specification consists of a two byte register address within the MMD and a two byte value.
Only fields marked with a PD Type in Chapter 10 are affected.
The following content is expected in the provisioning area:

     Register             Value

      1E.D400              0x40

      1E.D402             0x501

      1E.FF00              0x1

      1E.FF01              0x5

333369-009                                                                                              225
                                  Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                               Non-Volatile Memory Map
