## 10.4 Auto-Negotiation Registers

### 10.4.1 Auto-Negotiation Standard Control 1: Address 7.0

  Bit               Name                  Type        Default                                 Description

  8:0    Reserved                         RSV                   Reserved. Do not modify.

# 9 Restart Auto-Negotiation         RW            0b      Restart Auto-Negotiation

                                          SC                     0b = Normal operation.
                                                                 1b = Restart auto-negotiation process.

  B:A    Reserved                         RSV                   Reserved. Do not modify.
   C     Auto-Negotiation Enable          RW            1b      Auto-Negotiation Enable
                                          PD                    When enabled, auto-negotiation determines the link speed.
                                                                When disabled, the link is forced to its down state.
                                                                 0b = Disable auto-negotiation.
                                                                 1b = Enable auto-negotiation.
   D     Extended Next Page               RW            1b      Extended Next Page Control
         Control                          PD                    This bit is OR’ed with Bit 7.10.C.
                                                                 0b = Extended next pages are disabled.
                                                                 1b = Extended next pages are enabled.
  F:E    Reserved                         RSV                   Reserved. Do not modify.

### 10.4.2 Auto-Negotiation Standard Status 1: Address 7.1

  Bit           Name            Type        Default                                        Description

# 0 Link Partner Auto-         RO                   Link Partner Auto-Negotiation Ability

         Negotiation Ability                              0b = Link partner not able to perform auto-negotiation.
                                                          1b = Link partner able to perform auto-negotiation.

# 1 Reserved                   RSV                  Reserved. Do not modify.

# 2 Link Status                LL                   Link Status

                                                         This bit is a duplicate of the PMA Receive Link Status bit (Bit [2]) of the PMA
                                                         Standard Status 1: Address 1.1 register.
                                                          0b = Link lost since last read.
                                                          1b = Link is up.
                                                         Note: This is latching low, so it can only be used to detect link drops and not
                                                                   the current status of the link without performing back-to-back reads.

# 3 Auto-Negotiation          ROS           1b      Auto-Negotiation Ability

         Ability                                         Always set as 1b because the local device has auto-negotiation ability.
                                                          0b = PHY is not able to perform auto-negotiation.
                                                          1b = PHY is able to perform auto-negotiation.

# 4 Remote Fault               LH                   Remote Fault

                                                         This indicates that the remote PHY has a fault.
                                                          0b = No remote fault condition detected.
                                                          1b = Remote fault condition detected.

# 5 Auto-Negotiation           RO                   Auto-Negotiation Complete

         Complete                                        This indicates the status of the auto-negotiation receive link.
                                                          0b = Auto-negotiation in process.
                                                          1b = Auto-negotiation complete.

333369-009                                                                                                                           895
                                         Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                                      PHY Registers

  Bit            Name                 Type     Default                                     Description

# 6 Page Received                LH                Page Received

                                                         Indicates that a page has been received If it is a regular page, it is placed in
                                                         7.13 ->7.15. If it is an extended next page it is placed in registers 7.19 ->
                                                         7.1B
                                                          0b = A page has not been received.
                                                          1b = A page has been received.

# 7 Extended Next Page          RO                 Extended Next Page Status

          Status                                         Indicates that both the local device and the link partner have indicated support
                                                         for extended next page.
                                                           0b = Extended next page is not used.
                                                           1b = Extended next page is used.

# 8 Reserved                    RSV                Reserved. Do not modify.

# 9 Parallel Detection           LH                Parallel Detection Fault

          Fault                                           0b = A fault has not been detected via the parallel detection function.
                                                          1b = A fault has been detected via the parallel detection function.
  F:A     Reserved                    RSV                Reserved. Do not modify.

### 10.4.3 Auto-Negotiation Standard Device Identifier 1:

                     Address 7.2

  Bit         Name             Type     Default                                         Description

  F:0     OUI LSB              RO       0x154     OUI LSB
                                                  Bits [31:16] of the Device ID.
                                                  OUI[18:3]

### 10.4.4 Auto-Negotiation Standard Device Identifier 2:

                     Address 7.3

  Bit            Name                 Type     Default                                     Description

  3:0     Manufacturer’s              RO         0x0     Manufacturer’s Revision Number
          Revision Number                                4 bits containing the manufacturer’s revision number.

  9:4     Manufacturer’s              RO        0x22     Manufacturer’s Model Number
          Model Number                                   6 bits containing the manufacturer’s part number 0x22 for the X550-AT2 or
                                                         X550-BT2.
  F:A     OUI MSB                     RO         0x0     OUI MSB
                                                         Bits [15:10] of Device ID.
                                                         OUI[24:19]

896                                                                                                                            333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.5 Auto-Negotiation Standard Devices in Package 1:

                      Address 7.5

  Bit           Name           Type   Default                                     Description

# 0 Clause 22 Registers   ROS      0b      Clause 22 Registers Present

         Present                                 0b = Clause 22 registers are not present in package.
                                                 1b = Clause 22 registers are present in package.
                                                This bit is always set to 0b, as there are no Clause 22 registers in the X550.

    1 PMA Present           ROS      1b      PMA Present

                                                 0b = PMA is not present.
                                                 1b = PMA is present in package.
                                                This bit is always set to 1b, as there is PMA functionality in the X550.

    2 WIS Present           ROS      0b      WIS Present

                                                 0b = WIS is not present in package.
                                                 1b = WIS is present in package.
                                                This bit is always set to 0b, as there is no WIS functionality in the X550.

    3 PCS Present           ROS      1b      PCS Present

                                                 0b = PCS is not present in package.
                                                 1b = PCS is present in package.
                                                This bit is always set to 1b, as there is PCS functionality in the X550.

    4 PHY XS Present        ROS      0b      PHY XS Present

                                                 0b = PHY XS is not present in package.
                                                 1b = PHY XS is present in package.
                                                This bit is always set to 0b, as there is no PHY XS interface in the X550.

    5 DTE XS Present        ROS      0b      DTE XS Present

                                                 0b = DTE XS is not present in package.
                                                 1b = DTE XS is present in package.
                                                This bit is always set to 0b, as there is no DTE XAUI interface in the X550.

    6 TC Present            ROS      0b      TC Present

                                                 0b = TC is not present in package.
                                                 1b = TC is present in package.
                                                This bit is always set to 0b, as there is no TC functionality in the X550.

# 7 Auto-Negotiation      ROS      1b      Auto-Negotiation Present

         Present                                 0b = Auto-negotiation is not present in package.
                                                 1b = Auto-negotiation is present in package.
                                                This bit is always set to 1b, as there is auto-negotiation in the X550.
  F:8    Reserved              RSV              Reserved. Do not modify

333369-009                                                                                                                     897
                                  Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                     PHY Registers

### 10.4.6 Auto-Negotiation Standard Devices in Package 2:

                     Address 7.6

  Bit            Name            Type      Default                                        Description

  C:0     Reserved                 RSV                  Reserved. Do not modify
      D   Clause 22 Extension      ROS          1b      Clause 22 Extension Present
          Present                                        0b = Clause 22 Extension is not present in package.
                                                         1b = Clause 22 Extension is present in package.
                                                        This is always set to 1b, as the X550 uses this device for the GbE registers.
      E   Vendor Specific          ROS          1b      Vendor Specific Device #1 Present
          Device #1 Present                              0b = Device #1 is not present in package.
                                                         1b = Device #1 is present in package.
                                                        This is always set to 1b, as the X550 uses this device for the global control
                                                        registers.
      F   Vendor Specific          ROS          1b      Vendor Specific Device #2 Present
          Device #2 Present                              0b = Device #2 is not present in package.
                                                         1b = Device #2 is present in package.
                                                        This is always set to 1b, as the X550 uses this device for the DSP PMA
                                                        registers.

### 10.4.7 Auto-Negotiation Standard Status 2: Address 7.8

  Bit            Name            Type      Default                                        Description

  D:0     Reserved                 RSV                  Reserved. Do not modify
  F:E     Device Present [1:0]   ROS          10b       Device Present
                                                         00b = No device at this address.
                                                         01b = No device at this address.
                                                         10b = Device present at this address.
                                                         11b = No device at this address.
                                                        This field is always set to 10b, as auto-negotiation resides in the X550.

### 10.4.8 Auto-Negotiation Standard Package Identifier 1:

                     Address 7.E

  Bit                Name                Type        Default                                    Description

  F:0     Package ID MSW [1F:10]         RO                    Package ID MSW
                                                               Bits [31:16] of the Package ID.

### 10.4.9 Auto-Negotiation Standard Package Identifier 2:

                     Address 7.F

  Bit                Name                Type        Default                                    Description

  F:0     Package ID FSW [1F:10]         RO                    Package ID FSW
                                                               Bits [15:0] of the Package ID.

898                                                                                                                          333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.10 Auto-Negotiation Advertisement Register:

                    Address 7.10
Note:        This register is used in conjunction with Bit 7.C400.5 to hard-provision the auto-negotiation
             base page that is sent.

  Bit            Name           Type    Default                                    Description

  4:0    Selector Field [4:0]   RW       0x01     Selector Field
                                PD                This defines the device compatibility:
                                                   0x00 = Reserved
                                                   0x01 = IEEE 802.3
                                                   0x02 = IEEE 802.9 ISLAN-16T
                                                   0x03 = IEEE 802.5
                                                   0x04 = IEEE 1394
                                                   All other values are reserved.
                                                  This field should always be set to 0x01 because the PHY is only capable of
                                                  handling 802.3 Ethernet.
  B:5    Technology Ability     RW       0x00     Technology Ability Field
         Field [6:0]            PD                This bit contains information indicating supported technologies defined in
                                                  Annex 28B.2 and Annex 28D. Multiple technologies might be advertised in the
                                                  link code word. A device must support the data service ability for a technology
                                                  it advertises.
                                                    Bit [0] = Reserved
                                                    Bit [1] = Reserved
                                                    Bit [2] = 100BASE-TX
                                                    Bit [3] = 100BASE-TX full duplex
                                                    Bit [4] = 100BASE-T4
                                                    Bit [5] = PAUSE operation for full duplex links
                                                    Bit [6] = Asymmetric PAUSE operation for full duplex links
                                                  Note: Technology NOT supported by the X550. Bits must be set to 0x00.
   C     Extended Next Page     RW        1b      Extended Next Page Ability
         Ability                PD                This bit indicates that the local device supports transmission of extended next
                                                  pages when set to 1b and indicates that the local device does not support
                                                  extended next pages when set to 0b.
                                                   0b = Not capable of extended next pages.
                                                   1b = Extended next page capable.
   D     Advertisement          RW        0b      Advertisement Remote Fault
         Remote Fault                             This bit provides a standard transport mechanism for the transmission of
                                                  simple fault information. When the Remote Fault (RF) bit in the received base
                                                  link code word is set to 1b, the RF bit is set to 1b.
                                                    1b = Remote fault
                                                  Note: Not supported feature. The bit must be maintained as 0b.
   E     Reserved               RSV               Reserved. Do not modify.
   F     Next Page Ability      RW        1b      Next Page Ability
                                PD                If the X550 implements next page ability and needs to engage in a next page
                                                  exchange, it must set the Next Page (NP) bit to 1b. The X550 might implement
                                                  next page ability and choose not to engage in a next page exchange by setting
                                                  the NP bit to 0b.
                                                    1b = Next page ability

333369-009                                                                                                                     899
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

### 10.4.11 Auto-Negotiation Link Partner Base Page Ability

                     Register: Address 7.13

  Bit             Name              Type   Default                                   Description

  4:0     Link Partner Selector     RO               Link Partner Selector Field
          Field [4:0]                                This field encodes 32 possible messages defined in Annex 28A.
                                                     Combinations not specified are reserved for future use and must not be
                                                     transmitted.
                                                     This defines the device compatibility:
                                                       0x00 = Reserved
                                                       0x01 = IEEE 802.3
                                                       0x02 = IEEE 802.9 ISLAN-16T
                                                       0x03 = IEEE 802.5
                                                       0x04 = IEEE 1394
                                                       All other values are reserved.
  B:5     Link Partner Technology   RO               Link Partner Technology Ability Field
          Ability Field [6:0]                        This field contains information indicating supported technologies defined in
                                                     Annex 28B.2 and Annex 28D. Multiple technologies can be advertised in the
                                                     link code word. The X550 must support the data service ability for a
                                                     technology it advertises. The arbitration function determines the common
                                                     mode of operation shared by a link partner and resolves the multiple
                                                     common modes.
                                                       Bit [0] = Reserved
                                                       Bit [1] = Reserved
                                                       Bit [2] = 100BASE-TX
                                                       Bit [3] = 100BASE-TX full duplex
                                                       Bit [4] = 100BASE-T4
                                                       Bit [5] = PAUSE operation for full duplex links
                                                       Bit [6] = Asymmetric PAUSE operation for full duplex links
      C   Link Partner Extended     RO               Link Partner Extended Next Page Ability
          Next Page Ability                          This field indicates that the link partner has indicated support for the
                                                     extended next page when set to 1b. When set to 0b, the link partner does
                                                     not support extended next page.
                                                      0b = Not capable of extended next pages.
                                                      1b = Extended next page capable.
      D   Link Partner Remote       RO               Link Partner Remote Fault
          Fault                                      This bit provides a standard transport mechanism for transmitting simple
                                                     fault information. When the RF bit in the received base link code word is set
                                                     to 1b, the RF bit is set to 1b.
                                                       1b = Remote fault
      E   Link Partner Base Page    RO               Link Partner Base Page Acknowledge
          Acknowledge                                The Acknowledge (ACK) is used by the auto-negotiation function to indicate
                                                     that a device has successfully received its link partner’s link code word.
                                                       1b = Acknowledge
      F   Link Partner Next Page    RO               Link Partner Next Page Ability
          Ability                                    If next page ability is not supported, the NP bit must always be set to 0b. If
                                                     the X550 implements next page ability and needs to engage in a next page
                                                     exchange, it must set the NP bit to 1b.
                                                       0b = Next page ability not supported or not engaged.
                                                       1b = Next page ability.

900                                                                                                                    333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.12 Auto-Negotiation Extended Next Page Transmit

                     Register: Address 7.16
Note:        This register is used in conjunction with Bit 7.C400.5 and registers 7.17 and 7.18 to hard-
             provision the auto-negotiation extended next page that is sent. By using this register, it is
             possible to hard code the 1 GbE and 10 GbE capabilities.

  Bit                Name            Type   Default                                  Description

  A:0    Message Code Field [A:0]     RW    0x001      Message Code Field
                                      PD               Interpreted as message code (see 802.3 Appendix 28C) if the Message
                                                       Page bit is set to 1b (7.16:1). Otherwise, interpreted as an unformatted
                                                       code field.
                                                       [A:0] = Message code field:
                                                        0x0 = Reserved.
                                                        0x1 = Null message.
                                                        0x2 = Reserved expansion message.
                                                        0x3 = Reserved expansion message.
                                                        0x4 = Remote fault details message.
                                                        0x5 = OUI message.
                                                        0x6 = PHY ID message.
                                                        0x7 = 100BASE-T2 message.
                                                        0x8 = 1000BASE-T message.
                                                        All other values are reserved.
   B     Toggle                       RO               Toggle
                                                       Value of toggle bit. Set to opposite of corresponding bit in previous page.
   C     Acknowledge 2                RW      0b       Acknowledge 2
                                                       This field is used by the next page function to indicate that a device has
                                                       the ability to comply with the message.
                                                        0b = Cannot comply with corresponding message.
                                                        1b = Complies with corresponding message.
   D     Message Page                 RW      0b       Message Page
                                                       Message page is used by the next page function to differentiate a
                                                       message page from an unformatted page.
                                                        0b = Unformatted page.
                                                        1b = Message page.
   E     Reserved                    RSV               Reserved. Do not modify.
   F     Next Page                    RW      0b       Next Page
                                                       Next page is used by the next page function to indicate whether this is
                                                       the last next page to be transmitted.
                                                        0b = Last page.
                                                        1b = Additional next page follows.

### 10.4.13 Auto-Negotiation Extended Next Page

                     Unformatted Code Register 1: Address 7.17

  Bit                   Name                Type      Default                             Description

  F:0    Unformatted Code Field 1 [1F:10]   RW         0x0      Unformatted Code Field 1
                                            PD

333369-009                                                                                                                     901
                                    Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

### 10.4.14 Auto-Negotiation Extended Next Page

                     Unformatted Code Register 2: Address 7.18

  Bit                   Name                   Type     Default                             Description

  F:0     Unformatted Code Field 2 [2F:20]      RW        0x0     Unformatted Code Field 2
                                                PD

### 10.4.15 Auto-Negotiation Link Partner Extended Next

                     Page Ability Register: Address 7.19
Note:      This register, along with 7.1A and 7.1B, are used to store the received next pages. If an
           extended next page is used, it is stored in 7.19:7.1B.

  Bit             Name             Type      Default                                  Description

  A:0     Link Partner Message      RO                 Link Partner Message Code Field
          Code Field [A:0]                             Interpreted as message code (see 802.3 Appendix 28C) if the Message
                                                       Page bit is set to 1b (7.16:1). Otherwise, interpreted as an unformatted
                                                       code field.
                                                       [A:0] = Message code field:
                                                        0x0 = Reserved.
                                                        0x1 = Null message.
                                                        0x2 = Reserved expansion message.
                                                        0x3 = Reserved expansion message.
                                                        0x4 = Remote fault details message.
                                                        0x5 = OUI message.
                                                        0x6 = PHY ID message.
                                                        0x7 = 100BASE-T2 message.
                                                        0x8 = 1000BASE-T message.
                                                        All other values are reserved.
      B   Link Partner Toggle       RO                 Link Partner Toggle
                                                       Set opposite of the corresponding bit in the previous page.
                                                       Value of link partner’s toggle bit.
      C   Link Partner              RO                 Link Partner Acknowledge 2
          Acknowledge 2                                 0b = Link partner cannot comply with the current next page.
                                                        1b = Link partner acknowledges that they can comply with the current
                                                             next page.
      D   Link Partner Message      RO                 Link Partner Message Page
          Page                                          0b = Unformatted page.
                                                        1b = Message page.
      E   Link Partner Extended     RO                 Link Partner Extended Next Page Acknowledge
          Next Page Acknowledge                        Acknowledge is used by the auto-negotiation function to indicate that a
                                                       device has successfully received its link partners link code word.
                                                        1b = Link partner acknowledges receipt of corresponding page.
      F   Link Partner Next Page    RO                 Link Partner Next Page
                                                        1b = Next page ability.

902                                                                                                                    333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.16 Auto-Negotiation Link Partner Extended Next

                     Page Unformatted Code Register 1: Address 7.1A

  Bit                Name                  Type     Default                             Description

  F:0    Link Partner Unformatted Code      RO                Link Partner Unformatted Code Field 1 [15:0]
         Field 1 [F:0]

### 10.4.17 Auto-Negotiation Link Partner Extended Next

                     Page Unformatted Code Register 2: Address 7.1B

  Bit                Name                  Type     Default                             Description

  F:0    Link Partner Unformatted Code      RO                Link Partner Unformatted Code Field 2 [15:0]
         Field 2 [F:0]

### 10.4.18 Auto-Negotiation 10GBASE-T Control Register:

                     Address 7.20

  Bit           Name            Type     Default                                   Description

    0 LD Loop Timing         RW         1b      LD Loop Timing Ability

         Ability                PD                  0b = Do not advertise PHY as capable of loop timing.
                                                    1b = Advertise PHY as capable of loop timing

    1 LD Fast Retrain        RW         0b      LD Fast Retrain Ability

         Ability                PD                  0b = Do not advertise PHY as 10GBASE-T fast retrain capable
                                                    1b = Advertise PHY as 10GBASE-T fast retrain capable

    2 LD PMA Training        RW         0b      LD PMA Training Reset Request

         Reset Request          PD                  0b = Local device requests that Link Partner run PMA training PRBS
                                                         continuously.
                                                    1b = Local device requests that Link Partner reset PMA training PRBS every
                                                         frame.
  B:3    Reserved               RSV                Reserved. Do not modify.
   C     10GBASE-T Ability      RW         1b      10GBASE-T Ability
                                PD                  0b = Do not advertise PHY as 10GBASE-T capable.
                                                    1b = Advertise PHY as 10GBASE-T capable.
   D     Port Type              RW         0b      Port Type
                                PD                  0b = Single port device.
                                                    1b = Multiport device.
   E     Master/Slave           RW         0b      Master/Slave Configuration
         Configuration          PD                  0b = Slave.
                                                    1b = Master.
   F     Master/Slave Manual    RW         0b      Master/Slave Manual Configuration Enable
         Configuration Enable   PD                  0b = Disable master/slave manual configuration.
                                                    1b = Enable master/slave manual configuration.

333369-009                                                                                                                  903
                                     Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                                    PHY Registers

### 10.4.19 Auto-Negotiation 10GBASE-T Status Register:

                     Address 7.21

  Bit                Name                 Type     Default                                  Description

# 0 Reserved                        RSV                Reserved. Do not modify.

# 1 Link Partner Fast Retrain        RO                Link Partner Fast Retrain Ability

          Ability                                             0b = Link partner is not capable of 10GBASE-T fast retrain.
                                                              1b = Link partner is capable of 10GBASE-T fast retrain
  8:2     Reserved                        RSV                Reserved. Do not modify.

# 9 Link Partner Training Reset      RO                Link Partner Training Reset Request

          Request                                             0b = Link partner has requested that PMA PRBS training run
                                                                   continuously.
                                                              1b = Link partner has requested that PMA PRBS training be reset every
                                                                   frame.
      A   Link Partner Loop Timing         RO                Link Partner Loop Timing Ability
          Ability                                             0b = Link partner is not capable of loop timing.
                                                              1b = Link partner is capable of loop timing.
      B   Link Partner 10GBASE-T           RO                Link Partner 10GBASE-T Ability
          Ability                                            This bit is only valid when the Page Received Bit 7.1.6 is set to 1b.
                                                              0b = Link partner is not 10GBASE-T capable.
                                                              1b = Link partner is 10GBASE-T capable.
      C   Remote Receiver Status           RO                Remote Receiver Status
                                                             Set by the micro controller.
                                                              0b = Remote receiver not operational.
                                                              1b = Remote receiver operational.
      D   Local Receiver Status            RO                Local Receiver Status
                                                             Set by the micro controller.
                                                              0b = Local receiver not operational.
                                                              1b = Local receiver operational.
      E   Master/Slave                     RO                Master/Slave Configuration Resolution
          Configuration Resolution                            0b = Local PHY resolved to slave.
                                                              1b = Local PHY resolved to master.
      F   Master/Slave                     LH                Master/Slave Configuration Fault
          Configuration Fault                                 1b = Master/slave configuration fault.

### 10.4.20 Auto-Negotiation Vendor Provisioning 1: Address

                     7.C400

  Bit             Name                  Type     Default                                  Description

  3:0     Retry Attempts Before         RW        0x4      Retry Attempts Before Downshift
          Downshift [3:0]               PD                 Number of retry attempts before downshift.
                                                           If automatic downshifting is enabled, this is the number of retry attempts
                                                           the PHY makes to connect at the maximum mutually acceptable rate, before
                                                           removing this rate from the list and trying the next lower rate.

# 4 Automatic Downshift           RW         1b      Automatic Downshift Enable

          Enable                        PD                  0b = Manual downshift.
                                                            1b = Enable automatic downshift.

904                                                                                                                         333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit            Name                Type     Default                                     Description

# 5 User Provided Auto-         RW         0b        User Provided Auto-Negotiation Data

         Negotiation Data            PD                   If this bit is set, the PHY attempts to use the user-provided auto-negotiation
                                                          words. If there is a mismatch (such as a legacy 1GBASE-T device
                                                          attempting to connect), the PHY attempts to construct a new set of
                                                          auto-negotiation words from the data provided in these words.
                                                          Otherwise, the PHY constructs the correct auto-negotiation words based on
                                                          the provisioned values.
                                                            0b = Construct the correct auto-negotiation words based on the register
                                                                   settings of 7.10, 7.20, and 7.C400.
                                                            1b = User provides the next page or extended next page data directly
                                                                   (7.16:7.18), and the configuration information in 7.20 and 7.C400 is
                                                                   ignored.

# 6 Exchange PHY ID             RW         1b        Exchange PHY ID Information

         Information                 PD                    1b = Exchange PHY ID information.
  9:7    Reserved                    RSV                  Reserved. Do not modify.
   A     2.5G                        RW         0b        2.5G
                                     PD                    0b = Do not advertise PHY as supporting 2.5 GbE.
                                                           1b = Advertise PHY as supporting 2.5 GbE.
   B     5G                          RW         0b        5G
                                     PD                    0b = Do not advertise PHY as supporting 5 GbE.
                                                           1b = Advertise PHY as supporting 5 GbE.
   C     AQRate Downshift            RW         0b        NBASE-T Downshift Capability
         Capability                  PD                    0b = Do not allow NBASE-T down-shifting.
                                                           1b = Allow NBASE-T down-shifting.
  E:D    Reserved                    RSV                  Reserved. Do not modify.
   F     1000BASE-T Full             RW         0b        1000BASE-T Full Duplex Ability
         Duplex Ability              PD                    0b = Do not advertise PHY as 1000BASE-T full duplex capable.
                                                           1b = Advertise PHY as 1000BASE-T full duplex capable.

### 10.4.21 Auto-Negotiation Reserved Vendor Provisioning

                    1: Address 7.C410

  Bit               Name               Type     Default                                     Description

  1:0    MDI / MDI-X Control [1:0]     RW         00b       MDI/MDI-X Control
                                       PD                   These bits are used to force a manual MDI or MDI-X configuration.
                                                             00b = Automatic MDI/MDI-X operation.
                                                             01b = Manual MDI.
                                                             10b = Manual MDI-X.
                                                             11b = Reserved.
  5:2    Extra Page Count [3:0]        RW         0x4       Extra Page Count
                                       PD                   Number of extra pages to send at the end of the auto-negotiation
                                                            sequence when the link partner is a legacy GbE PHY.
                                                            Intervals between pages for GbE PHYs might be much longer. If this is
                                                            the case, the link partner might still be in auto-negotiation when the
                                                            X550 starts it’s training. This might confuse the link partner MDI/MDI-X
                                                            state machine. Sending extra pages seems to correct this problem.

# 6 WoL Enable                    RW            0b     WoL Enable

                                       PD                   Setting this bit enables WoL operation. In this state, power is minimized
                                                            by turning off all interfaces except the MDI receive path and the MDIO
                                                            interface.

333369-009                                                                                                                           905
                                      Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                                      PHY Registers

  Bit                Name                Type        Default                                 Description

# 7 WoL Mode                       RW            0b      WoL Mode

                                         PD                    This bit indicates whether the X550 goes into 100BASE-TX or 1000BASE-
                                                               T WoL operation.
                                                                0b = 100BASE-TX
                                                                1b = 1000BASE-T
  A:8     Semi-Cross Link Attempt        RW           0x0      Semi-Cross Link Attempt Period
          Period [2:0]                   PD                    Number of failed link attempts before trying semi cross.
                                                               Set to 0x0 to disable semi-cross. Set to 0x7 to always use semi-cross.
  F:B     Reserved                       RSV                   Reserved. Do not modify.

### 10.4.22 Auto-Negotiation Reserved Vendor Provisioning

                     2: Address 7.C411

  Bit           Name            Type       Default                                        Description

  A:0     Reserved              RSV                     Reserved. Do not modify.
      B   Auto-Negotiation          RW          0b      Auto-Negotiation Timeout Mode
          Timeout Mode              PD                    0b = Enable timeout for all auto-negotiation behavior.
                                                          1b = Enable timeout only if the following are enabled: LPLU, downshifting.
                                                        The timeout behavior can be described as follows:
                                                        Bits F:C = non-zero, Bit B = 0:
                                                        Timeout exists for all auto-negotiation behavior, including LPLU and if
                                                        downshift is enabled.
                                                        Bits F:C = 0, Bit B = 0:
                                                        No timeout enabled
                                                        Bits F:C = non-zero, Bit B = 1:
                                                        If we are in LPLU or downshift is enabled, timeout exists. If we are not in LPLU
                                                        or downshift is not enabled, there is no timeout.
                                                        Bits F:C = 0, Bit B = 1:
                                                        If we are in LPLU or downshift is enabled, there is no timeout. If we are not in
                                                        LPLU or downshift is not enabled, there is no timeout. In other words, there is
                                                        no timeout.
  F:C     Auto-Negotiation          RW         0x0      Auto-Negotiation Timeout
          Timeout [3:0]             PD                  The length of time in (seconds*2) before auto-negotiation restarts. A value of
                                                        zero indicates there is no timeout.
                                                        These bits control the use of auto-negotiation timeout watchdog during the
                                                        Arbit state machine.

906                                                                                                                         333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.23 Auto-Negotiation Vendor Status 1: Address

                     7.C800

  Bit           Name                Type        Default                                   Description

# 0 Connect Type               RO                    Connect Type

                                                          This field is used in conjunction with the Connection State field in the
                                                          Auto-Negotiation Reserved Vendor Status 1: Address 7.C810 to indicate the
                                                          duplex method the PHY is connected or attempting to connect at.
                                                          The duplex method the PHY connected or attempting to connect at:
                                                           0b = Reserved
                                                           1b = Full duplex
  3:1    Connect Rate [2:0]         RO                    Connect Rate
                                                          This field is used in conjunction with the Connection State field in the
                                                          Auto-Negotiation Reserved Vendor Status 1: Address 7.C810 to indicate the
                                                          rate the PHY is connected or attempting to connect at.
                                                          The rate the PHY connected or attempting to connect at:
                                                            000b = Reserved
                                                            001b = 100BASE-TX
                                                            010b = 1000BASE-T
                                                            011b = 10GBASE-T
                                                            100b = 2.5 GbE
                                                            101b = 5 GbE
                                                            All other values are reserved.
  F:4    Reserved                   RSV                   Reserved. Do not modify.

### 10.4.24 Auto-Negotiation Reserved Vendor Status 1:

                     Address 7.C810

  Bit               Name                 Type      Default                                  Description

# 0 Transmit PAUSE                    RO                 Transmit PAUSE Resolution

         Resolution                                           PAUSE resolution from 28B-3
                                                               0b = Transmit PAUSE disabled.
                                                               1b = Transmit PAUSE enabled.

# 1 Receive PAUSE                     RO                 Receive PAUSE Resolution

         Resolution                                           PAUSE resolution from 28B-3
                                                               0b = Receive PAUSE disabled.
                                                               1b = Receive PAUSE enabled.
  6:2    Reserved Status 1 [6:2]           RO                 Reserved Status 1
                                                              Reserved for future use.

# 7 Duplicate Link Partner            RO                 Duplicate Link Partner Auto-Negotiation Ability

         Auto-Negotiation Ability                             The link partner is capable of auto-negotiation.
                                                              This is a duplicate of the bit at 07.0001.0.

    8 MDI/MDI-X                         RO                 MDI/MDI-X

                                                              When auto-negotiation completes, this register indicates whether the
                                                              connection was made as an MDI or MDI-X connection.
                                                               0b = MDI
                                                               1b = MDI-X

333369-009                                                                                                                           907
                                         Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                                       PHY Registers

  Bit             Name                  Type      Default                                     Description

  D:9     Connection State [4:0]          RO                 Connection State
                                                             This field is used in conjunction with the Connect Rate and Connect Type
                                                             fields in the Auto-Negotiation Vendor Status 1: Address 7.C800 register to
                                                             indicate the current state the PHY is in.
                                                             The current state of the connection:
                                                               0x00 = Inactive (such as high-impedance).
                                                               0x01 = Cable diagnostics.
                                                               0x02 = Auto-negotiation.
                                                               0x03 = Training (10 GbE, 5 GbE, 2.5 GbE and 1 GbE only).
                                                               0x04 = Connected.
                                                               0x05 = Fail (auto-negotiation break link).
                                                               0x06 = Test mode.
                                                               0x07 = Loopback mode.
                                                               0x08 = Low Power mode.
                                                               0x09 = Connected WoL mode.
                                                               0x0A = System calibrating.
                                                               0x0B = Cable disconnected.
                                                               0x1C = MAC requested PHY reset.
                                                               0x1D = MAC requested PHY low-power mode.
                                                               0x1E = MAC requested PHY disable mode.
                                                               0x1F = MAC requested PHY resume normal operation.
                                                               All other values are reserved.
      E   Device Present                  RO                 Device Present
                                                             If true, a far-end Ethernet device exists because valid link pulses have
                                                             been detected in the most recent auto-negotiation session, or a valid
                                                             Ethernet connection has been established. If false, no connection is
                                                             established, and the most recent attempt at auto-negotiation failed to
                                                             detect any valid link pulses.Specifically, when MDI/MDI-X resolution has
                                                             completed, this bit is true. This bit is set false before entering auto-
                                                             negotiation.
                                                               0b = No far-end Ethernet device detected.
                                                               1b = Far-end Ethernet device present.
      F   Energy On Line                  RO                 Energy On Line
                                                             This bit is used to indicate that the PHY has detected energy on the line.
                                                             Specifically, when MDI/MDI-X resolution has completed, this bit is true.
                                                             This bit is set false before entering auto-negotiation.
                                                              0b = No energy detected on line.
                                                              1b = Energy detected on line.

### 10.4.25 Auto-Negotiation Reserved Vendor Status 2:

                    Address 7.C811

  Bit           Name               Type        Default                                      Description

  F:0     Auto-Negotiation         RO                    Auto-Negotiation Attempts
          Attempts [F:0]                                 The number of auto-negotiation attempts since the last successful connection
                                                         (or power-up).
                                                         This is a rolling counter (reverts to zero at saturation). It is cleared at reset or
                                                         after a successful connection completes.

908                                                                                                                              333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.26 Auto-Negotiation Reserved Vendor Status 3:

                   Address 7.C812

  Bit             Name                   Type     Default                                    Description

  E:0    Reserved State 3 [E:0]           RO                 Reserved State 3
                                                             Reserved for future use.
   F     Link Pulse Detected Status       RO                 Link Pulse Detected Status
                                                              0b = Link pulse not detected.
                                                              1b = Link pulse detected.

### 10.4.27 Auto-Negotiation Reserved Vendor Status 4:

                   Address 7.C813

  Bit            Name                 Type      Default                                    Description

  F:0    Auto-Negotiation               RO                Auto-Negotiation Restarts Handled
         Restarts Handled [F:0]                           The number of line-side auto-negotiation restart commands received.
                                                          This is a rolling counter (reverts to zero at saturation). It is cleared upon
                                                          reset.

### 10.4.28 Auto-Negotiation Reserved Vendor Status 5:

                   Address 7.C814

  Bit             Name                   Type     Default                                    Description

  F:0    Auto-Negotiation Attempts        RO                 Auto-Negotiation Attempts Since Reset
         Since Reset [F:0]                                   The number of auto-negotiation attempts since the last PHY reset (or
                                                             power-up).
                                                             This is a rolling counter (reverts to zero at saturation). It is cleared upon
                                                             reset.

### 10.4.29 Auto-Negotiation Transmit Vendor Alarms 1:

                   Address 7.CC00

  Bit           Name              Type       Default                                      Description

# 0 Connection State          LH                  Connection State Change

         Change                                        This interrupt indicates a change in the Connection State [D:B] in Auto-
                                                       Negotiation Reserved Vendor Status 1: Address 7.C810 register.
                                                        1b = The connection state has changed.
                                                       Note: This indicates any state change versus 7.CC01.0, which indicates a
                                                                connect or disconnect event.

# 1 Automatic Downshift       LH                  Automatic Downshift

                                                        1b = Automatic downshift has occurred.

# 2 Auto-Negotiation          LH                  Auto-Negotiation Completed For Supported Rate

         Completed for                                  1b = Auto-negotiation has completed successfully for a rate that is supported
         Supported Rate                                      by the X550.

333369-009                                                                                                                                909
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

  Bit            Name             Type      Default                                    Description

# 3 Auto-Negotiation          LH                Auto-Negotiation Completed For Non-Supported Rate

          Completed For Non-                          This means that the X550 has completed auto-negotiation and was unable to
          Supported Rate                              agree on a rate that both could operate at.
                                                       1b = Auto-negotiation has completed for a rate that is not supported by the
                                                             X550.
                                                      Note: This indication should be ignored in the case of master/slave
                                                              resolution fault.
  F:4     Reserved                  RSV               Reserved. Do not modify.

### 10.4.30 Auto-Negotiation Transmit Vendor Alarms 2:

                     Address 7.CC01

  Bit                  Name                   Type      Default                                Description

# 0 Link Connect/Disconnect              LH                 Link Connect/Disconnect

                                                                  This indicates whether the link has achieved a connect state or was
                                                                  in a connect state and disconnected.
                                                                    1b = MDI link has either connected or disconnected.
  E:1     Reserved Vendor Alarms 2 [D:0]       LH                 Reserved Vendor Alarms 2
                                                                  Reserved for future use.
      F   Link Pulse Detect                    LH                 Link Pulse Detect
                                                                   1b = Link pulse detected.

### 10.4.31 Auto-Negotiation Standard Interrupt Mask 1:

                     Address 7.D000

  Bit                   Name                     Type     Default                               Description

  1:0     Reserved                               RSV                Reserved. Do not modify.

# 2 Link Status Mask                       RW         0b      Link Status Mask

                                                 PD                  0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.

# 3 Reserved                               RSV                Reserved. Do not modify.

# 4 Remote Fault Mask                      RW         0b      Remote Fault Mask

                                                 PD                  0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.

# 5 Reserved                               RSV                Reserved. Do not modify.

# 6 Extended Next Page Received Mask       RW         0b      Extended Next Page Received Mask

                                                 PD                  0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
  8:7     Reserved                               RSV                Reserved. Do not modify.

# 9 Parallel Detection Fault Mask          RW          0      Parallel Detection Fault Mask

                                                 PD                  0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
  F:A     Reserved                               RSV                Reserved. Do not modify.

910                                                                                                                       333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.32 Auto-Negotiation Standard Interrupt Mask 2:

                    Address 7.D001

  Bit                   Name                       Type        Default                           Description

  E:0    Reserved                                  RSV                    Reserved. Do not modify.
   F     Master/Slave Configuration Fault Mask     RW            0b       Master/Slave Configuration Fault Mask
                                                   PD                      0b = Disable interrupt generation.
                                                                           1b = Enable interrupt generation.

### 10.4.33 Auto-Negotiation Transmit Vendor Interrupt

                    Mask 1: Address 7.D400

  Bit                Name                  Type     Default                                   Description

# 0 Connection State Change Mask       RW           0b      Connection State Change Mask

                                            PD                    0b = Disable interrupt generation.
                                                                  1b = Enable interrupt generation.

# 1 Automatic Downshift Mask           RW           0b      Automatic Downshift Mask

                                            PD                    0b = Disable interrupt generation.
                                                                  1b = Enable interrupt generation.

# 2 Auto-Negotiation Completed for     RW           0b      Auto-Negotiation Completed for Supported Rate Mask

         Supported Rate Mask                PD                    0b = Disable interrupt generation.
                                                                  1b = Enable interrupt generation.

# 3 Auto-Negotiation Completed For     RW           0b      Auto-Negotiation Completed For Non-Supported Rate Mask

         Non-Supported Rate Mask            PD                    0b = Disable interrupt generation.
                                                                  1b = Enable interrupt generation.
  F:4    Reserved                          RSV                   Reserved. Do not modify.

### 10.4.34 Auto-Negotiation Transmit Vendor Interrupt

                    Mask 2: Address 7.D401

  Bit                   Name                      Type        Default                           Description

# 0 Link Connect/Disconnect Mask             RW            0b       Link Connect/Disconnect Mask

                                                  PD                      0b = Disable interrupt generation.
                                                                          1b = Enable interrupt generation.
  E:1    Reserved Vendor Alarms 2 Mask [D:0]      RW           0x0       Reserved Vendor Alarms 2 Mask
                                                  PD                     Reserved for future use.
   F     Link Pulse Detect Mask                   RW            0b       Link Pulse Detect Mask
                                                  PD                      0b = Disable interrupt generation.
                                                                          1b = Enable interrupt generation.

333369-009                                                                                                            911
                                    Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                   PHY Registers

### 10.4.35 Auto-Negotiation Transmit Vendor Interrupt

                     Mask 3: Address 7.D402

  Bit         Name            Type   Default                                        Description

  F:0     Reserved            RSV                Reserved. Do not modify.

### 10.4.36 Auto-Negotiation Receive Link Partner Status 1:

                     Address 7.E820

  Bit                Name                Type     Default                                 Description

  2:0     Reserved                       RSV                Reserved. Do not modify.
  9:3     Reserved                       RSV                Reserved. Do not modify.
      A   Link Partner 2.5G              RW          0b     Link Partner 2.5G
                                         PD                  0b = Link Partner PHY is not 2.5 GbE capable.
                                                             1b = Link Partner PHY is 2.5 GbE capable.
      B   Link Partner 5G                RW          0b     Link Partner 5G
                                         PD                  0b = Link Partner PHY is not 5 GbE capable.
                                                             1b = Link Partner PHY is 5 GbE capable.
      C   Link Partner AQRate            RW          0b     Link Partner NBASE-T
                                         PD                  0b = Link Partner PHY does not support NBASE-T.
                                                             1b = Link Partner PHY supports NBASE-T.
      D   Reserved                       RSV                Reserved. Do not modify.
      E   Link Partner 1000BASE-T         RO                Link Partner 1000BASE-T Half Duplex Ability
          Half Duplex Ability                                0b = Link partner is not 1000BASE-T half-duplex capable.
                                                             1b = Link partner is 1000BASE-T half-duplex capable.
      F   Link Partner 1000BASE-T         RO                Link Partner 1000BASE-T Full Duplex Ability
          Full Duplex Ability                                0b = Link partner is not 1000BASE-T full-duplex capable.
                                                             1b = Link partner is 1000BASE-T full-duplex capable.

### 10.4.37 Auto-Negotiation Receive Link Partner Status 4:

                     Address 7.E823

  Bit                Name                  Type      Default                               Description

  7:0     Link Partner Firmware Minor       RO                 Link Partner Firmware Minor/Major Revision Number
          Revision Number [7:0]                                Only the lower six bits of major and minor firmware revision are
  F:8     Link Partner Firmware Major       RO                 exchanged in auto-negotiation when the PHYID message is sent.
          Revision Number [7:0]                                Consequently the upper two bits of the major and minor revision
                                                               should always be zero.
                                                                Bits [7:0] = Link partner firmware minor revision number.
                                                                Bits [F:8] = Link partner firmware major revision number.

912                                                                                                                     333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.38 Auto-Negotiation Receive Vendor Alarms 1:

                    Address 7.EC00

  Bit        Name          Type      Default                                        Description

  F:0    Reserved          RSV                  Reserved. Do not modify.

### 10.4.39 Auto-Negotiation Receive Vendor Alarms 2:

                    Address 7.EC01

  Bit               Name               Type      Default                                 Description

  B:0    Reserved Receive Vendor        LH                 Reserved Receive Vendor Alarms 2
         Alarms 2 [7:0]                                    Reserved for future use.
   C     FLP Idle Error                 LH                 FLP Idle Error
                                                            1b = No FLP burst has been seen for 50 milliseconds forcing the receive
                                                                  state machine back to the Idle state.
                                                           Once FLP bursts are detected on any receive channel, they must keep
                                                           coming. If no burst has been detected for a period of 50 ms, the auto-
                                                           negotiation process resets itself and goes back to the “break link” state.
   D     Auto-Negotiation Protocol      LH                 Auto-Negotiation Protocol Error
         Error                                               1b = Link partner has violated the auto-negotiation protocol.
                                                           If the arbiter state machine detects a protocol violation, the auto-
                                                           negotiation process resets itself and goes back to the “break link” state.
  F:E    Reserved                       LH                 Reserved. Do not modify.

### 10.4.40 Auto-Negotiation Receive Vendor Alarms 3:

                    Address 7.EC02

  Bit               Name               Type      Default                                 Description

  1:0    Reserved                      RSV                 Reserved. Do not modify.
   2     10BASE-T Device Detect         LL                 10BASE-T Device Detect
                                                           This bit indicates that the detected far-end device is 10BASE-T when it is
                                                           0b. This bit is 1b when link pulses are no longer received.
                                                            0b = 10BASE-T device detected.
  F:3    Reserved                      RSV                 Reserved. Do not modify.

### 10.4.41 Auto-Negotiation Receive Vendor Alarms 4:

                    Address 7.EC03

  Bit                 Name                     Type   Default                               Description

   0     100BASE-TX Parallel Detect             LH              100BASE-TX Parallel Detect
                                                                 1b = 100BASE-TX parallel event detection circuit.
  F:1    Reserved Receive Vendor                LH              Reserved Receive Vendor Alarms 4
         Alarms 4 [E:0]                                         Reserved.

333369-009                                                                                                                        913
                                      Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.4.42 Auto-Negotiation Receive Vendor Interrupt Mask

                     1: Address 7.F400

  Bit                   Name                   Type     Default                                Description

  F:0     Reserved Receive Vendor Alarms 1     RW         0x0       Reserved Receive Vendor Alarms 1 Mask
          Mask [F:0]                           PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.

### 10.4.43 Auto-Negotiation Receive Vendor Interrupt Mask

                     2: Address 7.F401

  Bit                   Name                   Type     Default                                Description

  B:0     Reserved Receive Vendor Alarms 2     RW         0x0       Reserved Receive Vendor Alarms 2 Mask
          Mask [B:0]                           PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
      C   FLP Idle Error Mask                  RW            0b     FLP Idle Error Mask
                                               PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
      D   Auto-Negotiation Protocol Error      RW            0b     Auto-Negotiation Protocol Error Mask
          Mask                                 PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
  F:E     Reserved                             RSV           0b     Reserved. Not supported.

### 10.4.44 Auto-Negotiation Receive Vendor Interrupt Mask

                     3: Address 7.F402

  Bit                 Name                   Type     Default                                Description

  1:0     Reserved                           RSV                  Reserved. Do not modify.
      2   10BASE-T Device Detect Mask        RW         0b        10BASE-T Device Detect Mask
                                             PD                    0b = Disable interrupt generation.
                                                                   1b = Enable interrupt generation.
  F:3     Reserved                           RSV                  Reserved. Do not modify.

### 10.4.45 Auto-Negotiation Receive Vendor Interrupt Mask

                     4: Address 7.F403

  Bit                   Name                   Type     Default                                Description

      0   100BASE-TX Parallel Detect Mask      RW            0b     100BASE-TX Parallel Detect Mask
                                               PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.
  F:1     Reserved Receive Vendor Alarms 4     RW         0x0       Reserved Receive Vendor Alarms 4 Mask
          Mask [E:0]                           PD                    0b = Disable interrupt generation.
                                                                     1b = Enable interrupt generation.

914                                                                                                                 333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.4.46 Auto-Negotiation Vendor Global Interrupt Flags

                    1: Address 7.FC00

  Bit           Name          Type     Default                                  Description

# 0 Vendor Specific Rx    RO                Vendor Specific Rx Alarms 4 Interrupt

         Alarms 4 Interrupt                      An interrupt was generated from status register Auto-Negotiation Receive
                                                 Vendor Alarms 4: Address 7.EC03 and the corresponding mask register Auto-
                                                 Negotiation Receive Vendor Interrupt Mask 4: Address 7.F403.
                                                  1b = Interrupt

# 1 Vendor Specific Rx    RO                Vendor Specific Rx Alarms 3 Interrupt

         Alarms 3 Interrupt                      An interrupt was generated from status register Auto-Negotiation Receive
                                                 Vendor Alarms 3: Address 7.EC02 and the corresponding mask register Auto-
                                                 Negotiation Receive Vendor Interrupt Mask 3: Address 7.F402.
                                                  1b = Interrupt

# 2 Vendor Specific Rx    RO                Vendor Specific Rx Alarms 2 Interrupt

         Alarms 2 Interrupt                      An interrupt was generated from status register Auto-Negotiation Receive
                                                 Vendor Alarms 2: Address 7.EC01 and the corresponding mask register Auto-
                                                 Negotiation Receive Vendor Interrupt Mask 2: Address 7.F401.
                                                  1b = Interrupt

# 3 Vendor Specific Rx    RO                Vendor Specific Rx Alarms 1 Interrupt

         Alarms 1 Interrupt                      An interrupt was generated from status register Auto-Negotiation Receive
                                                 Vendor Alarms 1: Address 7.EC00 and the corresponding mask register Auto-
                                                 Negotiation Receive Vendor Interrupt Mask 1: Address 7.F400.
                                                  1b = Interrupt
  8:4    Reserved             RSV                Reserved. Do not modify.

# 9 Vendor Specific       RO                Vendor Specific Alarms 2 Interrupt

         Alarms 2 Interrupt                      An interrupt was generated from status register Auto-Negotiation Transmit
                                                 Vendor Alarms 2: Address 7.CC01 and the corresponding mask register Auto-
                                                 Negotiation Transmit Vendor Interrupt Mask 2: Address 7.D401.
                                                  1b = Interrupt
   A     Vendor Specific       RO                Vendor Specific Alarms 1 Interrupt
         Alarms 1 Interrupt                      An interrupt was generated from status register Auto-Negotiation Transmit
                                                 Vendor Alarms 1: Address 7.CC00 and the corresponding mask register Auto-
                                                 Negotiation Transmit Vendor Interrupt Mask 1: Address 7.D400.
                                                  1b = Interrupt
  D:B    Reserved             RSV                Reserved. Do not modify.
   E     Standard Alarms 2     RO                Standard Alarms 2 Interrupt
         Interrupt                               An interrupt was generated from status register Auto-Negotiation 10GBASE-T
                                                 Status Register: Address 7.21 and the corresponding mask register Auto-
                                                 Negotiation Standard Interrupt Mask 2: Address 7.D001.
                                                  1b = Interrupt
   F     Standard Alarms 1     RO                Standard Alarms 1 Interrupt
         Interrupt                               An interrupt was generated from status register Auto-Negotiation Standard
                                                 Status 1: Address 7.1 and the corresponding mask register Auto-Negotiation
                                                 Standard Interrupt Mask 1: Address 7.D000.
                                                  1b = Interrupt

333369-009                                                                                                               915
                                    Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                                    PHY Registers

10.5             100BASE-TX and 1000BASE-T Registers

### 10.5.1 GbE Standard Device Identifier 1: Address 1D.2

  Bit             Name              Type     Default                                      Description

  F:0     Device ID MSW [1F:10]      RO                Device ID MSW
                                                       Bits [31:16] of the Device ID.

### 10.5.2 GbE Standard Device Identifier 2: Address 1D.3

  Bit             Name              Type     Default                                      Description

  F:0     Device ID LSW [F:0]        RO                Device ID LSW
                                                       Bits [15: 0] of the Device ID.

### 10.5.3 GbE Standard Devices in Package 1: Address 1D.5

  Bit            Name             Type     Default                                      Description

# 0 Clause 22 Registers     ROS        0b      Clause 22 Registers Present

          Present                                     0b = Clause 22 registers are not present in the package.
                                                      1b = Clause 22 registers are present in the package.
                                                     This is always set to 0b, as there are no Clause 22 registers in the X550.

    1 PMA Present             ROS        1b      PMA Present

                                                      0b = PMA is not present.
                                                      1b = PMA is present in the package.
                                                     This is always set to 1b, as there is PMA functionality in the X550.

    2 WIS Present             ROS        0b      WIS Present

                                                      0b = WIS is not present in the package.
                                                      1b = WIS is present in the package.
                                                     This is always set to 0b, as there is no WIS functionality in the X550.

    3 PCS Present             ROS        1b      PCS Present

                                                      0b = PCS is not present in the package.
                                                      1b = PCS is present in the package.
                                                     This is always set to 1b, as there is PCS functionality in the X550.

# 4 Control Present         ROS        1b      Control Present

                                                      0b = Control is not present in the package.
                                                      1b = Control is present in the package.
                                                     This is always set to 1b, as there is a PHY XAUI interface in the X550.

    5 DTE XS Present          ROS        0b      DTE XS Present

                                                      0b = DTE XS is not present in the package.
                                                      1b = DTE XS is present in the package.
                                                     This is always set to 0b, as there is no MAC XAUI interface in the X550.

    6 TC Present              ROS        0b      TC Present

                                                      0b = TC is not present in the package.
                                                      1b = TC is present in the package.
                                                     This is always set to 0b, as there is no TC functionality in the X550.

916                                                                                                                         333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit           Name            Type     Default                                        Description

# 7 Auto-Negotiation       ROS           1b      Auto-Negotiation Present

         Present                                       0b = Auto-negotiation is not present in the package.
                                                       1b = Auto-negotiation is present in the package.
                                                      This is always set to 1b, as there is auto-negotiation in the X550.
  F:8    Reserved               RSV                   Reserved. Do not modify.

### 10.5.4 GbE Standard Vendor Devices in Package 2:

                    Address 1D.6

  Bit           Name            Type     Default                                        Description

  C:0    Reserved               RSV                   Reserved. Do not modify.
   D     Clause 22 Extension    ROS           1b      Clause 22 Extension Present
         Present                                       0b = Clause 22 Extension is not present in the package.
                                                       1b = Clause 22 Extension is present in the package.
                                                      This is always set to 1b, as the X550 uses this device for the global control
                                                      registers.
   E     Vendor Specific        ROS           1b      Vendor Specific Device #1 Present
         Device #1 Present                             0b = Device #1 is not present in the package.
                                                       1b = Device #1 is present in the package.
                                                      This is always set to 1b, as the X550 uses this device for the global control
                                                      registers.
   F     Vendor Specific        ROS           1b      Vendor Specific Device #2 Present
         Device #2 Present                             0b = Device #2 is not present in the package.
                                                       1b = Device #2 is present in the package.
                                                      This is always set to 1b, as the X550 uses this device for the DSP PMA
                                                      registers.

### 10.5.5 GbE Standard Status 2: Address 1D.8

  Bit           Name            Type     Default                                        Description

  D:0    Reserved               RSV                   Reserved. Do not modify.
  F:E    Device Present [1:0]   ROS         10b       Device Present
                                                       00b = No device at this address.
                                                       01b = No device at this address.
                                                       10b = Device present at this address.
                                                       11b = No device at this address.
                                                      This field is always set to 10b, as the control is present in the X550.

### 10.5.6 GbE Standard Package Identifier 1: Address 1D.E

  Bit               Name               Type        Default                                 Description

  F:0    Package ID MSW [1F:10]        RO                    Package ID MSW
                                                             Bits [31:16] of the Package ID.

333369-009                                                                                                                            917
                                   Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

### 10.5.7 GbE Standard Package Identifier 2: Address 1D.F

  Bit            Name                Type      Default                                    Description

  F:0   Package ID LSW [F:0]            RO               Package ID LSW
                                                         Bits [15:0] of the Package ID.

### 10.5.8 GbE Reserved Provisioning 2: Address 1D.C501

  Bit               Name                     Type   Default                                 Description

  1:0   100BASE-TX Test Mode [1:0]           RW      00b      100BASE-TX Test Mode
                                                              100BASE-TX IEEE test mode = MLT-3 idle sequence.
                                                              ANSI jitter test = FDDI - Clause 9.1.3 Fig. 12.
                                                               00b = Normal mode.
                                                               01b = 100BASE-TX IEEE test mode.
                                                               10b = 100BASE-TX ANSI jitter test.
                                                               11b = Reserved.
  C:2   Reserved Provisioning 2 [A:0]        RW      0x0      Reserved Provisioning 2
                                             PD               Reserved for future use.
  F:D   Test Mode [2:0]                      RW      000b     Test Mode
                                             PD                000b = Normal mode.
                                                               001b = Test Mode 1 - Transmit waveform test.
                                                               010b = Test Mode 2 - Master transmit jitter test.
                                                               011b = Test Mode 3 - Slave transmit jitter test.
                                                               100b = Test Mode 4 - Transmitter distortion test.
                                                               All other values are reserved.

918                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers
