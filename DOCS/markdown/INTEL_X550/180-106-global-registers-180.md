## 10.6 Global Registers

### 10.6.1 Global Standard Control 1: Address 1E.0

  Bit           Name             Type     Default                                      Description

  A:0    Reserved                RSV                Reserved. Do not modify.
   B     Low Power               RW         0b      Low Power
                                 PD                 A 1b written to this register causes the corresponding X550 PHY to enter low-
                                                    power mode. This bit puts the entire PHY in low-power mode (with only the
                                                    MDIO and microprocessor functioning) and turns off the Analog Front End
                                                    (AFE). For example, places it in high-impedance mode. Setting this bit also
                                                    sets all of the Low Power bits in the other MMDs.
                                                     0b = Normal operation.
                                                     1b = Low-power mode.
  F:C    Reserved                RSV                Reserved. Do not modify.

### 10.6.2 Global Standard Device Identifier 1: Address 1E.2

  Bit            Name              Type     Default                                     Description

  F:0    Device ID MSW [1F:10]     RO                 Device ID MSW
                                                      Bits [31:16] of the Device ID.

### 10.6.3 Global Standard Device Identifier 2: Address 1E.3

  Bit            Name              Type     Default                                     Description

  F:0    Device ID LSW [F:0]       RO                 Device ID LSW
                                                      Bits [15:0] of the Device ID.

### 10.6.4 Global Standard Devices in Package 1: Address

                     1E.5

  Bit           Name             Type     Default                                      Description

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

333369-009                                                                                                                       919
                                      Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                              PHY Registers

  Bit           Name            Type   Default                                     Description

    3 PCS Present           ROS      1b      PCS Present

                                                  0b = PCS is not present in the package.
                                                  1b = PCS is present in the package.
                                                 This is always set to 1b, as there is PCS functionality in the X550.

    4 PHY XS Present        ROS      0b      PHY XS Present

                                                  0b = PHY XS is not present in the package.
                                                  1b = PHY XS is present in the package.
                                                 This is always set to 0b, as there is no PHY XS interface in the X550.

    5 DTE XS Present        ROS      0b      DTE XS Present

                                                  0b = DTE XS is not present in the package.
                                                  1b = DTE XS is present in the package.
                                                 This is always set to 0b, as there is no DTE XAUI interface in the X550.

    6 TC Present            ROS      0b      TC Present

                                                  0b = TC is not present in the package.
                                                  1b = TC is present in the package.
                                                 This is always set to 0b, as there is no TC functionality in the X550.

# 7 Auto-Negotiation      ROS      1b      Auto-Negotiation Present

          Present                                 0b = Auto-negotiation is not present in the package.
                                                  1b = Auto-negotiation is present in the package.
                                                 This is always set to 1b, as there is auto-negotiation in the X550.
  F:8     Reserved              RSV              Reserved. Do not modify.

### 10.6.5 Global Standard Vendor Devices in Package 2:

                       Address 1E.6

  Bit           Name            Type   Default                                     Description

  C:0     Reserved              RSV              Reserved. Do not modify.
      D   Clause 22 Extension   ROS      1b      Clause 22 Extension Present
          Present                                 0b = Clause 22 extension is not present in the package.
                                                  1b = Clause 22 extension is present in the package.
                                                 This is always set to 1b, as the X550 uses this device for the GbE registers.
      E   Vendor Specific       ROS      1b      Vendor Specific Device #1 Present
          Device #1 Present                       0b = Device #1 is not present in the package.
                                                  1b = Device #1 is present in the package.
                                                 This is always set to 1b, as the X550 uses this device for the global control
                                                 registers.
      F   Vendor Specific       ROS      1b      Vendor Specific Device #2 Present
          Device #2 Present                       0b = Device #2 is not present in the package.
                                                  1b = Device #2 is present in the package.
                                                 This is always set to 1b, as the X550 uses this device for the DSP PMA
                                                 registers.

920                                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.6 Global Standard Status 2: Address 1E.8

  Bit           Name            Type          Default                                      Description

  D:0    Reserved                  RSV                  Reserved. Do not modify.
  F:E    Device Present [1:0]      ROS         10b      Device Present
                                                         00b = No device at this address.
                                                         01b = No device at this address.
                                                         10b = Device present at this address.
                                                         11b = No device at this address.
                                                        This field is always set to 10b, as the global MMD resides here in the X550.

### 10.6.7 Global Standard Package Identifier 1: Address

                     1E.E

  Bit               Name                 Type        Default                                     Description

  F:0    Package ID MSW [1F:10]           RO                    Package ID MSW
                                                                Bits [31:16] of the Package ID.

### 10.6.8 Global Standard Package Identifier 2: Address

                     1E.F

  Bit               Name                 Type        Default                                     Description

  F:0    Package ID LSW [F:0]             RO                    Package ID LSW
                                                                Bits [15:0] of the Package ID.

### 10.6.9 Global Firmware ID: Address 1E.20

  Bit               Name             Type        Default                                     Description

  7:0    Firmware Minor Revision         RO                    Firmware Minor Revision Number
         Number [7:0]                                          The lower six bits of major and minor firmware revision are exchanged in
                                                               auto-negotiation when the PHYID message is sent.
  F:8    Firmware Major Revision         RO                    Firmware Major Revision Number
         Number [7:0]                                          The lower six bits of major and minor firmware revision are exchanged in
                                                               auto-negotiation when the PHYID message is sent.

### 10.6.10 Global Diagnostic Provisioning: Address 1E.C400

  Bit           Name            Type          Default                                      Description

  E:0    Reserved                  RSV                  Reserved. Do not modify.
   F     Enable Diagnostics        RW           0b      Enable Diagnostics
                                   PD                    1b = The X550 performs diagnostics on power up.

333369-009                                                                                                                             921
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.6.11 Global Thermal Provisioning 2: Address 1E.C421

   Bit           Name            Type     Default                                       Description

   F:0    High Temp Failure       RW      0x46001       High Temp Failure Threshold
          Threshold [F:0]         PD                    [F:0] of high temperature failure threshold.
                                                        2’s complement value with the LSB representing 1/256 °C. This corresponds
                                                        to -40 °C = 0xD800. Default is 70 °C.
                                                        Note: All Thresholds are orthogonal and can be set to any value regardless
                                                                 the value of the other thresholds. IN other words, High Temperature
                                                                 Warning (1E.C423) could be higher than High Temperature Failure
                                                                 (1E.C421).

1. The default value is overridden to 0x6600 by the provisioning mechanism.

### 10.6.12 Global Thermal Provisioning 3: Address 1E.C422

   Bit           Name            Type    Default                                       Description

   F:0    Low Temp Failure        RW        0x0        Low Temp Failure Threshold
          Threshold [F:0]         PD                   [F:0] of low temperature failure threshold.
                                                       2’s complement value with the LSB representing 1/256 °C. This corresponds to
                                                       -40 °C = 0xD800. Default is 0 °C.
                                                       Note: All Thresholds are orthogonal and can be set to any value regardless
                                                                the value of the other thresholds. In other words, High Temperature
                                                                Warning (1E.C423) could be higher than High Temperature Failure
                                                                (1E.C421).

### 10.6.13 Global Thermal Provisioning 4: Address 1E.C423

   Bit           Name            Type     Default                                       Description

# 1 High Temp Warning Threshold

   F:0    High Temp Warning       RW      0x3C00
          Threshold [F:0]         PD                    [F:0] of high temperature warning threshold.
                                                        2’s complement value with the LSB representing 1/256 °C. This corresponds
                                                        to -40 °C = 0xD008. Default is 60 °C.
                                                        Note: All Thresholds are orthogonal and can be set to any value regardless
                                                                 the value of the other thresholds. In other words, High Temperature
                                                                 Warning (1E.C423) could be higher than High Temperature Failure
                                                                 (1E.C421).

1. The default value is overridden to 0x6600 by the provisioning mechanism.

### 10.6.14 Global Thermal Provisioning 5: Address 1E.C424

   Bit           Name            Type    Default                                       Description

   F:0    Low Temp Warning        RW      0x0A00       Low Temp Warning Threshold
          Threshold [F:0]         PD                   [F:0] of low temperature Warning threshold
                                                       2's complement value with the LSB representing 1/256 °C. This corresponds to
                                                       -40 °C = 0xD800. Default is 10 °C.
                                                       Note: All Thresholds are orthogonal and can be set to any value regardless
                                                                the value of the other thresholds. In other words, High-Temperature-
                                                                Warning (1E.C423) could be higher than High-Temperature-Failure
                                                                (1E.C421).

922                                                                                                                      333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.15 Global Reserved Provisioning 1: Address 1E.C470

  Bit               Name               Type   Default                                  Description

  3:0    Reserved                      RSV              Reserved. Do not modify.

# 4 Initiate Cable Diagnostics    RW       0b      Initiate Cable Diagnostics

                                       SC               Perform cable diagnostics regardless of link state. If link is up, setting
                                                        this bit causes the link to drop while diagnostics are performed. This
                                                        register is self-clearing upon completion of the cable diagnostics.
                                                         1b = Perform cable diagnostics.

  C:5    Reserved                      RSV              Reserved. Do not modify.
  E:D    Extended MDI Diagnostics      RW      00b      Extended MDI Diagnostics Select / Diagnostics Select
         Select [1:0]                  PD               These bits select what sort of cable diagnostics to perform. For regular
   F     Diagnostics Select            RW       0b      cable diagnostics, Bit [F] is set to 0b, and the diagnostics are triggered
                                       PD               by setting Bit [4]. For extended diagnostics, Bit [F] is set to 1b, and the
                                                        desired extended diagnostics are selected by Bits [E:D]. The routine is
                                                        then triggered by setting Bit [4]. Each of the extended diagnostic
                                                        routines present data for all for MDI pairs (A, B, C, D) consecutively, and
                                                        after the data for each channel is gathered Bits [F:D] are reset. To get
                                                        the data for the next pair, Bits [F:D] must be set back to the desired
                                                        value, which must be the same as the initial channel. This continues until
                                                        the data for all channels has been gathered. The address in memory
                                                        where the data is stored is given in 1E.C802 and 1E.C804.
                                                        For PSD, the structure is as follows:
                                                         • Int32 info
                                                         • Int16 data[Len]
                                                         • Info = Len << 16 | TxEnable << 8 | Pair (0 = A, etc.)
                                                        For TDR:
                                                         • Int32 info
                                                         • Int16 tdr_A[Len]
                                                         • Int16 tdr_B[Len]
                                                         • Int16 tdr_C[Len]
                                                         • Int16 tdr_D[Len]
                                                        Info = Len << 16 | Channel
                                                        TDR data is from the current pair or all other pairs.
                                                        At the end of retrieving extended MDI diagnostic data, the X550 is reset.
                                                        Conversely, the only way to exit this routine once it starts is to issue a
                                                        PMA reset.
                                                        Bits [E:D] settings:
                                                         00b = TDR data.
                                                         01b = RFI channel PSD.
                                                         10b = Noise PSD while the local Tx is off.
                                                         11b = Noise PSD while the local Tx is on.
                                                        Bit [F] settings:
                                                         0b = Provide normal cable diagnostics.
                                                         1b = Provide extended MDI diagnostics information.

### 10.6.16 Global Reserved Provisioning 3: Address 1E.C472

  Bit               Name               Type   Default                                  Description

  5:0    Reserved                      RSV              Reserved. Do not modify.

# 6 Tunable External VDD          RW       0b      Tunable External VDD Power Supply Present

         Power Supply Present          PD                0b = No tunable external VDD power supply present.
                                                         1b = Tunable external VDD power supply present.
                                                        This bit must be set if tuning of external power supply is desired.
  D:7    Reserved                      RSV              Reserved. Do not modify.

333369-009                                                                                                                           923
                                      Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                                      PHY Registers

  Bit                Name                Type    Default                                     Description

      E   Enable VDD Power Supply        RW           0b       Enable VDD Power Supply Tuning
          Tuning                         PD                    This bit controls whether the PHY attempts to tune the external VDD
                                                               power supply via the SMBus. This bit is only operational if the external
                                                               supply is present. See 1E.C472.6 (Section 10.6.16).
                                                                0b = Disable external VDD power supply tuning is disabled
                                                                1b = Enable external VDD power supply tuning
      F   Reserved                       RSV                   Reserved. Do not modify.

### 10.6.17 Global Reserved Provisioning 5: Address 1E.C474

  Bit           Name              Type     Default                                         Description

    0 NVM Daisy Chain         RW           0x0     NVM Daisy Chain Kickstart

          Kickstart               PD                   When in daisy chain master mode, the PHY0 can kickstart the daisy chain. The
                                                       kickstart does not reload the IRAM/DRAM or reset the uP for PHY0. It just
                                                       reads the flash and transfer the flash data to the daisy chain. This is for
                                                       backwards compatibility with the 82599.
                                                        1b = Kickstart the Daisy Chain
  F:1     Reserved                RSV                  Reserved. Do not modify.

### 10.6.18 Global Reserved Provisioning 6: Address 1E.C475

  Bit                Name                 Type       Default                                  Description

  3:0     Reserved                        RSV                   Reserved. Do not modify.

    4 CFR Support                     RW           0b       CFR Support

                                          PD                     0b = Local PHY does support Cisco Fast Retrain.
                                                                 1b = Local PHY supports Cisco Fast Retrain.

    5 CFR THP                         RW           0b       CFR THP

                                          PD                     0b = Local PHY does not require local PHY to enable THP.
                                                                 1b = Local PHY requires local PHY to enable THP.

    6 CFR Extended Max wait           RW           0b       CFR Extended Max wait

                                          PD                     0b = Local PHY does not require extended max wait.
                                                                 1b = Local PHY requires extended max wait.

    7 CFR Disable Timer               RW           0b       CFR Disable Timer

                                          PD                     0b = Local PHY does not require cfr_disable timer.
                                                                 1b = Local PHY requires cfr_disable timer.

    8 CFR LP Support                  RW           0b       CFR LP Support

                                          PD                     0b = Link partner does support Cisco Fast Retrain.
                                                                 1b = Link partner supports Cisco Fast Retrain.

    9 CFR LP THP                      RW           0b       CFR LP THP

                                          PD                     0b = Link partner does not require local PHY to enable THP.
                                                                 1b = Link partner requires local PHY to enable THP.
      A   CFR LP Extended Max wait        RW           0b       CFR LP Extended Max wait
                                          PD                     0b = Link partner does not require extended max wait.
                                                                 1b = Link partner requires extended max wait.
      B   CFR LP Disable Timer            RW           0b       CFR LP Disable Timer
                                          PD                     0b = Link partner does not require cfr_disable timer.
                                                                 1b = Link partner requires cfr_disable timer.
  F:C     Reserved                        RSV         0x0       Reserved. Do not modify.

924                                                                                                                          333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.19 Global SMBus 0 Provisioning 6: Address 1E.C485

  Bit               Name               Type   Default                                 Description

# 0 Reserved                      RSV              Reserved. Do not modify.

  7:1    SMB 0 Slave Address [7:1]      RW        0x0   SMB 0 Slave Address
                                                        SMB slave address configuration.
  F:8    Reserved                      RSV              Reserved. Do not modify.

### 10.6.20 Global SMBus 1 Provisioning 6: Address 1E.C495

  Bit               Name               Type   Default                                 Description

# 0 Reserved                      RSV              Reserved. Do not modify.

  7:1    SMB 1 Slave Address [7:1]      RW        0x0   SMB 1 Slave Address
                                                        SMB slave address configuration.
  F:8    Reserved                      RSV              Reserved. Do not modify.

### 10.6.21 Global Cable Diagnostic Status 1: Address

                    1E.C800

  Bit           Name           Type     Default                                    Description

  2:0    Pair D Status [2:0]    RO                Pair D Status
                                                  This register summarizes the worst case impairment on pair D.
                                                  [6:4]
                                                   000b = OK.
                                                   001b = Connected to Pair C.
                                                   010b = Connected to Pair B.
                                                   011b = Connected to Pair A.
                                                   100b = Short circuit (< 30 ).
                                                   101b = Low mismatch (< 85 ).
                                                   110b = High mismatch (> 115 ).
                                                   111b = Open circuit (> 300 .

# 3 Reserved              RSV                Reserved. Do not modify.

  6:4    Pair C Status [2:0]    RO                Pair C Status
                                                  This register summarizes the worst case impairment on pair C.
                                                  [9:7]
                                                   000b = OK.
                                                   001b = Connected to Pair B.
                                                   010b = Connected to Pair A.
                                                   011b = Connected to Pair D.
                                                   100b = Short circuit (< 30 ).
                                                   101b = Low mismatch (< 85 ).
                                                   110b = High mismatch (> 115 ).
                                                   111b = Open circuit (> 300 ).

# 7 Reserved              RSV                Reserved. Do not modify.

333369-009                                                                                                        925
                                     Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

  Bit            Name             Type     Default                                   Description

  A:8     Pair B Status [2:0]      RO                Pair B Status
                                                     This register summarizes the worst case impairment on pair B.
                                                     [C:A]:
                                                      000b = OK.
                                                      001b = Connected to Pair A.
                                                      010b = Connected to Pair D.
                                                      011b = Connected to Pair C.
                                                      100b = Short circuit (< 30 ).
                                                      101b = Low mismatch (< 85 ).
                                                      110b = High mismatch (> 115 ).
                                                      111b = Open circuit (> 300 ).
      B   Reserved                 RSV               Reserved. Do not modify.
  E:C     Pair A Status [2:0]      RO                Pair A Status
                                                     This register summarizes the worst case impairment on pair A.
                                                     [F:D]:
                                                     000b = OK.
                                                     001b = Connected to Pair D.
                                                     010b = Connected to Pair C.
                                                     011b = Connected to Pair B.
                                                     100b = Short circuit (< 30 ).
                                                     101b = Low mismatch (< 85 ).
                                                     110b = High mismatch (> 115 ).
                                                     111b = Open circuit (> 300 ).
      F   Reserved                 RSV               Reserved. Do not modify.

### 10.6.22 Global Cable Diagnostic Status 2: Address

                     1E.C801

  Bit                Name                Type   Default                                 Description

  7:0     Pair A Reflection #2 [7:0]      RO              Pair A Reflection #2/#1
  F:8     Pair A Reflection #1 [7:0]      RO              The distance in meters (accurate to ±1 m) of the second of the four
                                                          worst case reflections seen by the PHY on Pair A.
                                                          The distance to this reflection is given in Global Cable Diagnostic
                                                          Impedance 1: Address 1E.C880 register (Section 10.6.34). A value of
                                                          zero indicates that this reflection does not exist or was not computed.

### 10.6.23 Global Cable Diagnostic Status 3: Address

                     1E.C802

  Bit            Name             Type     Default                                   Description

  F:0     Impulse Response         RO                Impulse Response MSW
          MSW [F:0]                                  The MSW of the memory location that contains the start of the impulse
                                                     response data for the extended diagnostic type in 1E.C470.E:D.
                                                     See 1E.C470 (Section 10.6.15).

926                                                                                                                     333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.24 Global Cable Diagnostic Status 4: Address

                    1E.C803

  Bit               Name                  Type    Default                                  Description

  7:0    Pair B Reflection #2 [7:0]       RO                 Pair B Reflection #2/#1
  F:8    Pair B Reflection #1 [7:0]       RO                 The distance in meters (accurate to ±1 m) of the first of the four worst
                                                             case reflections seen by the PHY on Pair B.
                                                             The distance to this reflection is given in Global Cable Diagnostic
                                                             Impedance 2: Address 1E.C881 register (Section 10.6.35). A value of
                                                             zero indicates that this reflection does not exist or was not computed.

### 10.6.25 Global Cable Diagnostic Status 5: Address

                    1E.C804

  Bit           Name               Type     Default                                     Description

  F:0    Impulse Response          RO                 Impulse Response LSW
         LSW [F:0]                                    The LSW of the memory location that contains the start of the impulse
                                                      response data for the extended diagnostic type in 1E.C470.E:D.
                                                      See 1E.C470 (Section 10.6.15).

### 10.6.26 Global Cable Diagnostic Status 6: Address

                    1E.C805

  Bit               Name                  Type    Default                                  Description

  7:0    Pair C Reflection #2 [7:0]       RO                 Pair C Reflection #2/#1
  F:8    Pair C Reflection #1 [7:0]       RO                 The distance in meters (accurate to ±1 m) of the first of the four worst
                                                             case reflections seen by the PHY on Pair C.
                                                             The distance to this reflection is given in Global Cable Diagnostic
                                                             Impedance 3: Address 1E.C882 register (Section 10.6.36). A value of
                                                             zero indicates that this reflection does not exist or was not computed.

### 10.6.27 Global Cable Diagnostic Status 7: Address

                    1E.C806

  Bit        Name           Type      Default                                        Description

  F:0    Reserved           RSV                  Reserved.

333369-009                                                                                                                         927
                                        Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                     PHY Registers

### 10.6.28 Global Cable Diagnostic Status 8: Address

                     1E.C807

  Bit                Name                Type        Default                                 Description

  7:0     Pair D Reflection #2 [7:0]      RO                   Pair D Reflection #2/#1
  F:8     Pair D Reflection #1 [7:0]      RO                   The distance in meters (accurate to ±1 m) of the first of the four worst
                                                               case reflections seen by the PHY on Pair D.
                                                               The distance to this reflection is given in Global Cable Diagnostic
                                                               Impedance 4: Address 1E.C883 register (Section 10.6.37). A value of
                                                               zero indicates that this reflection does not exist or was not computed.

### 10.6.29 Global Thermal Status 1: Address 1E.C820

  Bit            Name             Type     Default                                        Description

  F:0     Temperature [F:0]        RO                   Temperature
                                                        [F:0] of temperature.
                                                        2’s complement value with the LSB representing 1/256 °C. This corresponds to
                                                        -40 °C = 0xD800. Default is 70 °C.

### 10.6.30 Global Thermal Status 2: Address 1E.C821

  Bit            Name             Type     Default                                        Description

# 0 Temperature Ready        RO                   Temperature Ready

                                                         1b = Temperature measurement is valid.
  F:1     Reserved                RSV                   Reserved. Do not modify.

### 10.6.31 Global General Status 1: Address 1E.C830

  Bit            Name             Type     Default                                        Description

  A:0     Reserved                RSV                   Reserved. Do not modify.
      B   Low Temperature          RO                   Low Temperature Warning State
          Warning State                                  1b = Low temperature warning threshold has been exceeded.
      C   High Temperature         RO                   High Temperature Warning State
          Warning State                                  1b = High temperature warning threshold has been exceeded.
      D   Low Temperature          RO                   Low Temperature Failure State
          Failure State                                  1b = Low temperature failure threshold has been exceeded.
      E   High Temperature         RO                   High Temperature Failure State
          Failure State                                  1b = High temperature failure threshold has been exceeded.
      F   Reserved                RSV           0b      Reserved. Do not modify.

928                                                                                                                          333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.32 Global Fault Message: Address 1E.C850

  Bit        Name         Type   Default                                          Description

  F:0    Message [F:0]    RO                Message
                                            Error code describing fault.
                                            Code Number:
                                             0x8001 = Firmware is not compatible with the chip architecture. This fault occurs
                                                        when firmware is compiled for a different core that is loaded.
                                             0x8002 = VCO calibration failed. This occurs when the main PLLs on the chip fail to
                                                        lock (no trigger is possible).
                                             0x8003 = XAUI calibration failed. This occurs when the XAUI PLLs fail to lock (no
                                                        trigger is possible).
                                             0x8005 = Unexpected device ID. This occurs if the device ID programmed into the
                                                        internal E-Fuse registers in not valid (no trigger is possible).
                                             0x8006 = Computed checksum does not match expected checksum. This occurs
                                                        when the Flash checksum check performed at boot time fails. This only
                                                        occurs when the system boots from Flash.
                                             0x8007 = Detected a bit error in static memory. To trigger, corrupt one of the static
                                                        regions.
                                             0xC001 = Illegal Instruction exception. This occurs when the processor attempts to
                                                        execute an illegal instruction. To trigger this, write an illegal instruction
                                                        to program memory. It's possible that the bit error check triggers before
                                                        the illegal instruction executes.
                                             0xC002 = Instruction Fetch Error. Internal physical address or a data error during
                                                        instruction fetch (no trigger is possible).
                                             0xC003 = Load Store Error. Internal physical address or data error during load
                                                        store operation (no trigger is possible).
                                             0xC004 = Privileged Instruction. Attempt to execute a privileged operation without
                                                        sufficient privilege (no trigger is possible).
                                             0xC005 = Unaligned Load or Store. Attempt to load or store data at an address
                                                        that cannot be handled due to alignment (no trigger is possible).
                                             0xC006 = Instruction fetch from prohibited space (no trigger is possible).
                                             0xC007 = Data load from prohibited space (no trigger is possible).
                                             0xC008 = Data store into prohibited space (no trigger is possible).
                                             0xDEAD = Uncorrectable IRAM error.
                                             0xDEAE = DRAM parity error.
                                             0xDD00 = CRD16 IRAM check failure (IRAM load error).
                                             0xFACA = E-Fuse CRC16 check failure (E-Fuse is corrupted).

### 10.6.33 Global Primary Status: Address 1E.C851

  Bit        Name         Type   Default                                          Description

# 0 Primary Status   RO                Primary Status

                                             0b = PHY is the secondary PHY.
                                             1b = PHY is the primary PHY.
  F:1    Reserved         RSV               Value always 0b. Writes are ignored.

333369-009                                                                                                                        929
                                  Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

### 10.6.34 Global Cable Diagnostic Impedance 1: Address

                     1E.C880

  Bit                Name               Type   Default                                  Description

  2:0     Pair A Reflection #4 [2:0]     RO              Pair A Reflection #4
                                                         The impedance of the fourth worst case reflection on Pair A. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 1: Address 1E.C800 register (Section 10.6.21).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).

# 3 Reserved                      RSV              Reserved

  6:4     Pair A Reflection #3 [2:0]     RO              Pair A Reflection #3
                                                         The impedance of the third worst case reflection on Pair A. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 1: Address 1E.C800 register (Section 10.6.21).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).

# 7 Reserved                      RSV              Reserved

  A:8     Pair A Reflection #2 [2:0]     RO              Pair A Reflection #2
                                                         The impedance of the second worst case reflection on Pair A. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 1: Address 1E.C800 register (Section 10.6.21).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).
      B   Reserved                      RSV              Reserved
  E:C     Pair A Reflection #1 [2:0]     RO              Pair A Reflection #1
                                                         The impedance of the first worst case reflection on Pair A. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 1: Address 1E.C800 register (Section 10.6.21).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).
      F   Reserved                      RSV              Reserved

930                                                                                                                     333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.35 Global Cable Diagnostic Impedance 2: Address

                    1E.C881

  Bit               Name               Type   Default                                  Description

  2:0    Pair B Reflection #4 [2:0]     RO              Pair B Reflection #4
                                                        The impedance of the fourth worst case reflection on Pair B. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 2: Address 1E.C801 register (Section 10.6.22).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).

# 3 Reserved                      RSV              Reserved

  6:4    Pair B Reflection #3 [2:0]     RO              Pair B Reflection #3
                                                        The impedance of the third worst case reflection on Pair B. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 2: Address 1E.C801 register (Section 10.6.22).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).

# 7 Reserved                      RSV              Reserved

  A:8    Pair B Reflection #2 [2:0]     RO              Pair B Reflection #2
                                                        The impedance of the second worst case reflection on Pair B. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 2: Address 1E.C801 register (Section 10.6.22).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).
   B     Reserved                      RSV              Reserved
  E:C    Pair B Reflection #1 [2:0]     RO              Pair B Reflection #1
                                                        The impedance of the first worst case reflection on Pair B. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 2: Address 1E.C801 register (Section 10.6.22).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).
   F     Reserved                      RSV              Reserved

333369-009                                                                                                                      931
                                      Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

### 10.6.36 Global Cable Diagnostic Impedance 3: Address

                     1E.C882

  Bit                Name               Type   Default                                  Description

  2:0     Pair C Reflection #4 [2:0]     RO              Pair C Reflection #4
                                                         The impedance of the fourth worst case reflection on Pair C. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 3: Address 1E.C802 register (Section 10.6.23).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).

# 3 Reserved                      RSV              Reserved

  6:4     Pair C Reflection #3 [2:0]     RO              Pair C Reflection #3
                                                         The impedance of the third worst case reflection on Pair C. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 3: Address 1E.C802 register (Section 10.6.23).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).

# 7 Reserved                      RSV              Reserved

  A:8     Pair C Reflection #2 [2:0]     RO              Pair C Reflection #2
                                                         The impedance of the second worst case reflection on Pair C. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 3: Address 1E.C802 register (Section 10.6.23).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).
      B   Reserved                      RSV              Reserved
  E:C     Pair C Reflection #1 [2:0]     RO              Pair C Reflection #1
                                                         The impedance of the first worst case reflection on Pair C. The
                                                         corresponding length of this reflection from the PHY is given in the Global
                                                         Cable Diagnostic Status 3: Address 1E.C802 register (Section 10.6.23).
                                                          0xxb = No information available.
                                                          100b = Short circuit (< 30 ).
                                                          101b = Low mismatch (< 85 ).
                                                          110b = High mismatch (> 115 ).
                                                          111b = Open circuit (> 300 ).
      F   Reserved                      RSV              Reserved

932                                                                                                                     333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.37 Global Cable Diagnostic Impedance 4: Address

                    1E.C883

  Bit               Name               Type   Default                                  Description

  2:0    Pair D Reflection #4 [2:0]     RO              Pair D Reflection #4
                                                        The impedance of the fourth worst case reflection on Pair D. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 4: Address 1E.C803 register (Section 10.6.24).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).

# 3 Reserved                      RSV              Reserved

  6:4    Pair D Reflection #3 [2:0]     RO              Pair D Reflection #3
                                                        The impedance of the third worst case reflection on Pair D. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 4: Address 1E.C803 register (Section 10.6.24).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).

# 7 Reserved                      RSV              Reserved

  A:8    Pair D Reflection #2 [2:0]     RO              Pair D Reflection #2
                                                        The impedance of the second worst case reflection on Pair D. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 4: Address 1E.C803 register (Section 10.6.24).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (> 115 ).
                                                         111b = Open circuit (> 300 ).
   B     Reserved                      RSV              Reserved
  E:C    Pair D Reflection #1 [2:0]     RO              Pair D Reflection #1
                                                        The impedance of the first worst case reflection on Pair D. The
                                                        corresponding length of this reflection from the PHY is given in the Global
                                                        Cable Diagnostic Status 4: Address 1E.C803 register (Section 10.6.24).
                                                         0xxb = No information available.
                                                         100b = Short circuit (< 30 ).
                                                         101b = Low mismatch (< 85 ).
                                                         110b = High mismatch (>  ).
                                                         111b = Open circuit (> 300 ).
   F     Reserved                      RSV              Reserved

### 10.6.38 Global Status: Address 1E.C884

  Bit               Name               Type   Default                                  Description

  7:0    Cable Length [7:0]             RO              Cable Length
                                                        The estimated length of the cable in meters.
                                                        The length of the cable shown here is estimated from the cable
                                                        diagnostic engine and should be accurate to ± 1 m.
  F:8    Reserved Status 0 [7:0]        RO              Reserved.

333369-009                                                                                                                      933
                                      Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                 PHY Registers

### 10.6.39 Global Reserved Status 1: Address 1E.C885

  Bit               Name               Type     Default                                  Description

  3:0     Provisioning ID [3:0]        ROS        0x0     Provisioning ID
                                        PD                Customers may receive multiple ROM images that differ only in their
                                                          provisioning. This field is used to differentiate those images. This field is
                                                          used in conjunction with the firmware major and minor revision
                                                          numbers to uniquely identify ROM images.
  7:4     Firmware Build ID [3:0]      ROS        0x0     Firmware Build ID
                                        PD                Customers might receive multiple ROM images that differ only in their
                                                          provisioning. This field is used to differentiate those images. This field is
                                                          used in conjunction with the firmware major and minor revision
                                                          numbers to uniquely identify ROM images.
  9:8     NVM Status [1:0]             ROS        00b     NVM Status
                                        PD                This register indicates the status of the last NVM operation.
                                                          Status of NVM:
                                                           00b = NVM not enabled.
                                                           01b = Last NVM operation succeeded.
                                                           10b = Last NVM operation failed.
                                                           11b = Reserved.
  F:A     Nearly Seconds MSW [5:0]      RO                Nearly Seconds MSW
                                                          Bits [21:16] of the 22-bit nearly seconds uptime counter.
                                                          The nearly seconds counter is incremented every 1024 ms.

### 10.6.40 Global Reserved Status 2: Address 1E.C886

  Bit               Name               Type     Default                                  Description

  F:0     Nearly Seconds LSW [F:0]      RO                Nearly Seconds LSW
                                                          Bit [15:0] of the 22-bit nearly seconds uptime counter.
                                                          The nearly seconds counter is increased every 1024 ms.

### 10.6.41 Global Reserved Status 3: Address 1E.C887

  Bit              Name              Type     Default                                   Description

  D:0     Reserved Status 3 [D:0]    RSV        0b      Reserved Status 3
                                                        Reserved for future use.
      E   Power Up Stall Status      ROS        0b      Power Up Stall Status
                                                         0b = Firmware is unstalled.
                                                         1b = Firmware is stalled at power up.
      F   DTE Status                 ROS                DTE Status
                                                         0b = Does not need power.
                                                         1b = Needs power.

934                                                                                                                        333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.42 Global Reserved Status 4: Address 1E.C888

  Bit            Name            Type   Default                                    Description

  2:0    Rate [2:0]              RO         000b   Rate
                                                   These bits report the selected rate for the loopback and packet generation.
                                                    000b = Invalid
                                                    001b = 100 Mb/s
                                                    010b = 1 GbE
                                                    011b = 10 GbE
                                                    100b = 2.5 GbE
                                                    101b = 5 GbE
                                                    110b = Reserved
                                                    111b = Reserved

# 3 System I/F Packet       RO         0b     System I/F Packet Generation Status

         Generation Status                         Reports whether the CRPAT packet generator in the PHY outputs on the
                                                   selected system interface at the selected rate.
                                                    0b = No CRPAT packet generation out 10 GbE system interface.
                                                    1b = CRPAT packet generation out 10 GbE system interface.

# 4 Reserved                RSV               Reserved. Do not modify

    5 MDI Packet Generation   RO         0b     MDI Packet Generation Status

         Status                                    Reports whether the CRPAT packet generator in the PHY outputs on the MDI
                                                   interface at the selected rate.
                                                     0b = No CRPAT packet generation out MDI interface.
                                                     1b = CRPAT packet generation out MDI interface.
  A:6    Reserved Status 4       RO         0x0    Reserved Status 4
         [5:0]                                     Reserved for future use.
  F:B    Loopback Status [5:0]   RW         0x0    Loopback Status
                                 PD                These bits, in conjunction with the chip configuration and the rate (Bits
                                                   1:0), report the selected loopback.
                                                    0x00 = No loopback
                                                    0x01 = System Interface — System Loopback
                                                    0x02 = System Interface — System Loopback with Pass-through
                                                    0x03 = System Interface — Network Loopback
                                                    0x04 = System Interface — Network Loopback with Pass-through
                                                    0x05 = System Interface — Network Loopback with Pass-through and
                                                             Merge
                                                    0x06 = System Interface — Peer-to-peer loopback
                                                    0x09 = Network Interface — System Loopback
                                                    0x0A = Network Interface — System Loopback with Pass-through
                                                    0x0B = Network Interface — Network Loopback
                                                    0x0C = Network Interface — Network Loopback with Pass-through
                                                    0x0D = Network Interface — Peer-to-peer loopback
                                                    0x10 = Cross-connect System Loopback
                                                    0x11 = Cross-connect Network Loopback
                                                    0x14 = Network Interface — System Loopback via Loopback Plug
                                                    All other values are reserved.

333369-009                                                                                                                     935
                                  Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

### 10.6.43 Global Alarms 1: Address 1E.CC00

  Bit                Name             Type   Default                                   Description

# 0 Reserved Alarm D             LH              Reserved Alarm D

                                                       Reserved for future use.

# 1 Reserved Alarm C             LH              Reserved Alarm C

                                                       Reserved for future use.

# 2 Reserved Alarm B             LH              Reserved Alarm B

                                                       Reserved for future use.

# 3 Reserved Alarm A             LH              Reserved Alarm A

                                                       Reserved for future use.

# 4 Device Fault                 LH              Device Fault

                                                       When set, a fault has been detected by the P and the associated 16-bit
                                                       error code is visible in the Global Fault Message: Address 1E.C850
                                                       register (Section 10.6.32).
                                                        1b = Fault

# 5 Reserved                    RSV              Reserved. Do not modify.

# 6 Reset Completed              LH              Reset Completed

                                                       This bit is set by the P completing it’s initialization sequence. This bit is
                                                       mirrored in 1.CC02.0 (Section 10.6.45)
                                                        1b = Chip wide reset completed.
  A:7     Reserved                    RSV              Reserved. Do not modify.
      B   Low Temperature Warning      LH              Low Temperature Warning
                                                       This bit mirrors the matching bit in 1.A070 and 1.A074. If latched high
                                                       behavior is enabled for this bit via 1E.C440.0, reading one register is the
                                                       same as reading the other.
                                                        1b = Low temperature warning threshold has been exceeded.
      C   High Temperature Warning     LH              High Temperature Warning
                                                       This bit mirrors the matching bit in 1.A070 and 1.A074. If latched high
                                                       behavior is enabled for this bit via 1E.C440.0, reading one register is the
                                                       same as reading the other.
                                                        1b = High temperature warning threshold has been exceeded.
      D   Low Temperature Failure      LH              Low Temperature Failure
                                                       This bit mirrors the matching bit in 1.A070 and 1.A074. If latched high
                                                       behavior is enabled for this bit via 1E.C440.0, reading one register is the
                                                       same as reading the other.
                                                        1b = Low temperature failure threshold has been exceeded.
      E   High Temperature Failure     LH              High Temperature Failure
                                                       This bit mirrors the matching bit in 1.A070 and 1.A074. If latched high
                                                       behavior is enabled for this bit via 1E.C440.0, reading one register is the
                                                       same as reading the other.
                                                        1b = High temperature failure threshold has been exceeded.
      F   Reserved                    RSV      0b      Reserved. Do not modify.

936                                                                                                                      333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.44 Global Alarms 2: Address 1E.CC01

  Bit            Name            Type   Default                                  Description

# 0 Diagnostic Alarm         LH              Diagnostic Alarm

                                                  A diagnostic alarm used to test system alarm circuitry.
                                                   1b = Alarm triggered by a write to 1E.C470.7.

    1 MAC PHY Clear Reset      LH              MAC PHY Clear Reset Request Handled

         Request Handled                           1b = PHY handled the MAC clear reset request.

    2 MAC PHY Normal State     LH              MAC PHY Normal State Request Handled

         Request Handled                           1b = PHY handled the MAC normal state request.

    3 MAC PHY Low Power        LH              MAC PHY Low Power Request Handled

         Request Handled                           1b = PHY handled the MAC low power request.

    4 MAC PHY Disable          LH              MAC PHY Disable Request Handled

         Request Handled                           1b = PHY handled the MAC disable request.

    5 MAC Reset Request        LH              MAC Reset Request Handled

         Handled                                   1b = PHY handled the MAC reset request.

# 6 Reserved Alarm E         LH              Reserved Alarm E

                                                  Reserved.

    7 MDIO Command             LH              MDIO Command Handling Overflow

         Handling Overflow                        Assertion of this bit means that more MDIO commands were issued than
                                                  firmware could handle.
                                                    1b = PHY was issued more MDIO requests than it could service in it’s
                                                         request buffer
  9:8    Reserved Alarms [1:0]    LH              Reserved Alarms
                                                  Reserved.
   A     Fast Link Drop           LH              Fast Link Drop
                                                  This alarm is asserted before entering PHY link recovery state. This alarm
                                                  can be used as an early sign for a link drop in case of unsuccessful link
                                                  recovery.
                                                    1b = PHY has entered link recovery state.
   B     DTE Status Change        LH              DTE Status Change
                                                  Change in 1E.C887.F (Section 10.6.41).
                                                   1b = DTE status change.
   C     IP Phone Detect          LH              IP Phone Detect
                                                  Assertion of this bit means that the presence of an IP Phone has been
                                                  detected.
                                                   1b = IP Phone Detect
  F:D    Reserved                RSV              Reserved. Do not modify.

333369-009                                                                                                                 937
                                  Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

### 10.6.45 Global Alarms 3: Address 1E.CC02

  Bit                Name               Type   Default                                  Description

# 0 Watchdog Timer Alarm           LH              Watchdog Timer Alarm

                                                          1b = Watchdog timer alarm

    1 MDIO Timeout Error             LH              MDIO Timeout Error

                                                          1b = MDIO timeout detected

    2 MDIO MMD Error                 LH              MDIO MMD Error

                                                          1b = Invalid MMD address detected
  4:3     Reserved                      RSV              Reserved. Do not modify.

# 5 Tx Enable State Change        LRF              Transmit Enable State Change

                                                          1b = TX_EN pin has changed state
  7:6     Reserved                      RSV              Reserved. Do not modify.
  9:8     uP IRAM Parity Error [1:0]     LH              uP IRAM Parity Error
                                                         Bit [0] indicates a parity error was detected in the uP IRAM but was
                                                         corrected.
                                                         Bit [1] indicates a multiple parity errors were detected in the uP IRAM
                                                         and could not be corrected.
                                                         The uP IRAM is protected with ECC.
                                                          1b = Parity error detected in the uP IRAM
      A   uP DRAM Parity Error           LH              uP DRAM Parity Error
                                                          1b = Parity error detected in the uP DRAM
  D:B     Reserved                      RSV              Reserved. Do not modify.
      E   Mailbox Operation              LH              Mailbox Operation Complete
          Complete                                       Mailbox interface is ready interrupt for registers
                                                          1b = Mailbox operation is complete
      F   NVM Operation Complete         LH              NVM Operation Complete
                                                         NVM interface is ready interrupt for registers
                                                          1b = NVM operation is complete

938                                                                                                                    333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.46 Global Interrupt Mask 1: Address 1E.D400

  Bit                Name                   Type   Default                              Description

# 0 Reserved Alarm D Mask              RW       0b      Reserved Alarm D Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

# 1 Reserved Alarm C Mask              RW       0b      Reserved Alarm C Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

# 2 Reserved Alarm B Mask              RW       0b      Reserved Alarm B Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

# 3 Reserved Alarm A Mask              RW       0b      Reserved Alarm A Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

# 4 Device Fault Mask                  RW       0b      Device Fault Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

# 5 Reserved                           RSV              Reserved. Do not modify.

# 6 Reset Completed Mask               RW       0b      Reset Completed Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
  A:7    Reserved                           RSV              Reserved. Do not modify.
   B     Low Temperature Warning Mask       RW       0b      Low Temperature Warning Mask
                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   C     High Temperature Warning Mask      RW       0b      High Temperature Warning Mask
                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   D     Low Temperature Failure Mask       RW       0b      Low Temperature Failure Mask
                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   E     High Temperature Failure Mask      RW       1b      High Temperature Failure Mask
                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   F     Reserved                           RSV              Reserved. Do not modify.

333369-009                                                                                            939
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                             PHY Registers

### 10.6.47 Global Interrupt Mask 2: Address 1E.D401

  Bit                 Name                   Type    Default                              Description

# 0 Diagnostic Alarm Mask               RW       0b      Diagnostic Alarm Mask

                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    1 MAC PHY Clear Reset Request         RW       0b      MAC PHY Clear Reset Request Handled Mask

          Handled Mask                        PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    2 MAC PHY Normal State Request        RW       0b      MAC PHY Normal State Request Handled Mask

          Handled Mask                        PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    3 MAC PHY Low Power Request           RW       0b      MAC PHY Low Power Request Handled Mask

          Handled Mask                        PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    4 MAC PHY Disable Request             RW       0b      MAC PHY Disable Request Handled Mask

          Handled Mask                        PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    5 MAC Reset Request Handled Mask      RW       0b      MAC Reset Request Handled Mask

                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

# 6 Reserved Alarm E Mask               RW       0b      Reserved Alarm E Mask

                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.

    7 MDIO Command Handling               RW       0b      MDIO Command Handling Overflow Mask

          Overflow Mask                       PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.
  9:8     Reserved Alarms Mask [1:0]          RW      00b      Reserved Alarms Mask
                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.
      A   Fast Link Drop Mask                 RW       0b      Fast Link Drop Mask
                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.
      B   DTE Status Change Mask              RW       0b      DTE Status Change Mask
                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.
      C   IP Phone Detect Mask                RW       0b      IP Phone Detect Mask
                                              PD                0b = Disable interrupt generation.
                                                                1b = Enable interrupt generation.
  F:D     Reserved                            RSV              Reserved. Do not modify.

940                                                                                                            333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.48 Global Interrupt Mask 3: Address 1E.D402

  Bit                 Name                  Type   Default                              Description

# 0 Watchdog Timer Alarm Mask          RW       1b      Watchdog Timer Alarm Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

    1 MDIO Timeout Error Mask            RW       0b      MDIO Timeout Error Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

    2 MDIO MMD Error Mask                RW       0b      MDIO MMD Error Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
  4:3    Reserved                           RSV              Reserved. Do not modify.

# 5 Tx Enable State Change Mask        RW       0b      Transmit Enable State Change Mask

                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
  7:6    Reserved                           RSV              Reserved. Do not modify.
  9:8    uP IRAM Parity Error [1:0] Mask    RW      00b      uP IRAM Parity Error Mask
                                            PD               Bit [0] indicates a parity error was detected in the uP IRAM but
                                                             was corrected.
                                                             Bit [1] indicates a multiple parity errors were detected in the uP
                                                             IRAM and could not be corrected.
                                                             The uP IRAM is protected with ECC.
                                                              0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   A     uP DRAM Parity Error Mask          RW       0b      uP DRAM Parity Error Mask
                                            PD                0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
  D:B    Reserved                           RSV              Reserved. Do not modify.
   E     Mailbox Operation Complete Mask    RW       0b      Mailbox Operation Complete Mask
                                            PD               Mailbox interface is ready interrupt for registers
                                                              0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.
   F     NVM Operation Complete Mask        RW       0b      NVM Operation Complete Mask
                                            PD               NVM interface is ready interrupt for registers
                                                              0b = Disable interrupt generation.
                                                              1b = Enable interrupt generation.

333369-009                                                                                                                   941
                                     Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                           PHY Registers

### 10.6.49 Global Chip-Wide Standard Interrupt Flags:

                     Address 1E.FC00

  Bit            Name          Type    Default                                  Description

# 0 All Vendor Alarms    RO                All Vendor Alarms Interrupt

          Interrupt                              An interrupt was generated from status register Global Chip-Wide Vendor
                                                 Interrupt Flags: Address 1E.FC01 and the corresponding mask register Global
                                                 Interrupt Chip-Wide Vendor Mask: Address 1E.FF01.
                                                  1b = Interrupt in all vendor alarms.
  5:1     Reserved             RSV               Reserved. Do not modify.

# 6 GbE Standard         RO                GbE Standard Alarms Interrupt

          Alarms Interrupt                       An interrupt was generated from the TGE core.
                                                  1b = Interrupt in GbE standard alarms.

# 7 Auto-Negotiation     RO                Auto-Negotiation Standard Alarms 2 Interrupt

          Standard Alarms 2                      An interrupt was generated from status register Auto-Negotiation 10GBASE-T
          Interrupt                              Status Register: Address 7.21 and the corresponding mask register Auto-
                                                 Negotiation Standard Interrupt Mask 2: Address 7.D001.
                                                  1b = Interrupt in auto-negotiation standard alarms 2.

# 8 Auto-Negotiation     RO                Auto-Negotiation Standard Alarms 1 Interrupt

          Standard Alarms 1                      An interrupt was generated from status register Auto-Negotiation Standard
          Interrupt                              Status 1: Address 7.1 and the corresponding mask register Auto-Negotiation
                                                 Standard Interrupt Mask 1: Address 7.D000.
                                                  1b = Interrupt in auto-negotiation standard alarms 1.
  A:9     Reserved             RSV               Reserved. Do not modify.
      B   PCS Standard Alarm   RO                PCS Standard Alarm 3 Interrupt

# 3 Interrupt                            An interrupt was generated from status register PCS 10GBASE-T Status 2:

                                                 Address 3.21 and the corresponding mask register PCS Standard Interrupt
                                                 Mask 3: Address 3.D002.
                                                  1b = Interrupt in PCS standard alarms 3.
      C   PCS Standard Alarm   RO                PCS Standard Alarm 2 Interrupt

# 2 Interrupt                            An interrupt was generated from status register PCS Standard Status 2:

                                                 Address 3.8 and the corresponding mask register PCS Standard Interrupt Mask
                                                 2: Address 3.D001.
                                                  1b = Interrupt in PCS standard alarms 2.
      D   PCS Standard Alarm   RO                PCS Standard Alarm 1 Interrupt

# 1 Interrupt                            An interrupt was generated from status register PCS Standard Status 1:

                                                 Address 3.1 and the corresponding mask register PCS Standard Interrupt Mask
                                                 1: Address 3.D000.
                                                  1b = Interrupt in PCS standard alarms 1.
      E   PMA Standard Alarm   RO                PMA Standard Alarm 2 Interrupt

# 2 Interrupt                            An interrupt was generated from either Bit 1.8.B or 1.8.A.

                                                 An interrupt was generated from status register PMA Standard Status 2:
                                                 Address 1.8 and the corresponding mask register PMA Transmit Standard
                                                 Interrupt Mask 2: Address 1.D001.
                                                  1b = Interrupt in PMA standard alarms 2.
      F   PMA Standard Alarm   RO                PMA Standard Alarm 1 Interrupt

# 1 Interrupt                            An interrupt was generated from Bit 1.1.2.

                                                 An interrupt was generated from status register PMA Standard Status 1:
                                                 Address 1.1 and the corresponding mask register PMA Transmit Standard
                                                 Interrupt Mask 1: Address 1.D000.
                                                  1b = Interrupt in PMA standard alarms 1.

942                                                                                                              333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.50 Global Chip-Wide Vendor Interrupt Flags:

                    Address 1E.FC01

  Bit          Name           Type     Default                                   Description

# 0 Global Alarms 3       RO                Global Alarms 3 Interrupt

         Interrupt                               An interrupt was generated from status register Global Alarms 3: Address
                                                 1E.CC02 and the corresponding mask register Global Interrupt Mask 3:
                                                 Address 1E.D402.
                                                  1b = Interrupt in Global alarms 3.

# 1 Global Alarms 2       RO                Global Alarms 2 Interrupt

         Interrupt                               An interrupt was generated from status register Global Alarms 2: Address
                                                 1E.CC01 and the corresponding mask register Global Interrupt Mask 2:
                                                 Address 1E.D401.
                                                  1b = Interrupt in Global alarms 2.

# 2 Global Alarms 1       RO                Global Alarms 1 Interrupt

         Interrupt                               An interrupt was generated from status register Global Alarms 1: Address
                                                 1E.CC00 and the corresponding mask register Global Interrupt Mask 1:
                                                 Address 1E.D400.
                                                  1b = Interrupt in Global alarms 1.
  B:3    Reserved             RSV                Reserved. Do not modify.
                                                  1b =
   C     Auto-Negotiation      RO                Auto-Negotiation Vendor Alarm Interrupt
         Vendor Alarm                            An auto-negotiation alarm was generated.
         Interrupt
                                                 See Auto-Negotiation Vendor Global Interrupt Flags 1: Address 7.FC00.
                                                  1b = Interrupt in auto-negotiation vendor specific alarm.
   D     Reserved             RSV                Reserved. Do not modify.
   E     PCS Vendor Alarm      RO                PCS Vendor Alarm Interrupt
         Interrupt                               A PCS alarm was generated.
                                                 See PCS Vendor Global Interrupt Flags 1: Address 3.FC00.
                                                  1b = Interrupt in PCS vendor specific alarm.
   F     PMA Vendor Alarm      RO                PMA Vendor Alarm Interrupt
         Interrupt                               A PMA alarm was generated.
                                                 See PMA Vendor Global Interrupt Flags 1: Address 1.FC00.
                                                  1b = Interrupt in PMA vendor specific alarm.

333369-009                                                                                                                  943
                                    Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

### 10.6.51 Global Interrupt Chip-Wide Standard Mask:

                     Address 1E.FF00

  Bit                Name              Type   Default                                 Description

# 0 All Vendor Alarms            RW       1b      All Vendor Alarms Interrupt Mask

          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
  5:1     Reserved                     RSV              Reserved. Do not modify.

# 6 GbE Standard Alarms          RW       0b      GbE Standard Alarms Interrupt Mask

          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.

# 7 Auto-Negotiation Standard    RW       0b      Auto-Negotiation Standard Alarms 2 Interrupt Mask

          Alarms 2 Interrupt Mask      PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.

# 8 Auto-Negotiation Standard    RW       0b      Auto-Negotiation Standard Alarms 1 Interrupt Mask

          Alarms 1 Interrupt Mask      PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
  A:9     Reserved                     RSV              Reserved. Do not modify.
      B   PCS Standard Alarm 3         RW       0b      PCS Standard Alarm 3 Interrupt Mask
          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
      C   PCS Standard Alarm 2         RW       0b      PCS Standard Alarm 2 Interrupt Mask
          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
      D   PCS Standard Alarm 1         RW       0b      PCS Standard Alarm 1 Interrupt Mask
          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
      E   PMA Standard Alarm 2         RW       0b      PMA Standard Alarm 2 Interrupt Mask
          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
      F   PMA Standard Alarm 1         RW       0b      PMA Standard Alarm 1 Interrupt Mask
          Interrupt Mask               PD                0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.

944                                                                                                              333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.6.52 Global Interrupt Chip-Wide Vendor Mask:

                    Address 1E.FF01

  Bit                Name                  Type   Default                              Description

# 0 Global Alarms 3 Interrupt Mask     RW       1b     Global Alarms 3 Interrupt Mask

                                            PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.

# 1 Global Alarms 2 Interrupt Mask     RW       0b     Global Alarms 2 Interrupt Mask

                                            PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.

# 2 Global Alarms 1 Interrupt Mask     RW       0b     Global Alarms 1 Interrupt Mask

                                            PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.
  A:3    Reserved                           RSV             Reserved. Do not modify.
   B     GbE Vendor Alarm Interrupt         RW       0b     GbE Vendor Alarm Interrupt Mask
         Mask                               PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.
   C     Auto-Negotiation Vendor Alarm      RW       0b     Auto-Negotiation Vendor Alarm Interrupt Mask
         Interrupt Mask                     PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.
   D     Reserved                           RSV             Reserved. Do not modify.
   E     PCS Vendor Alarm Interrupt         RW       0b     PCS Vendor Alarm Interrupt Mask
         Mask                               PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.
   F     PMA Vendor Alarm Interrupt         RW       0b     PMA Vendor Alarm Interrupt Mask
         Mask                               PD               0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.

333369-009                                                                                                 945
                                      Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                         PHY Registers

NOTE:   This page intentionally left blank.

946                                                                                        333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Chapter 11 System Manageability

Network management is an important requirement in today's networked computer environment.
Software-based management applications provide the ability to administer systems while the operating
system is functioning in a normal power state (not in a pre-boot state or powered-down state). The
Intel® Out of Band Management fill the management void that exists when the operating system is not
running or fully functional. This is accomplished by providing mechanisms by which manageability
network traffic can be routed to and from a Management Controller (BMC).
This chapter describes the supported management interfaces and hardware configurations for platform
system management. It describes the interfaces to an external BMC, the partitioning of platform
manageability among system components, and the functionality provided by the X550 in each platform
configuration.
