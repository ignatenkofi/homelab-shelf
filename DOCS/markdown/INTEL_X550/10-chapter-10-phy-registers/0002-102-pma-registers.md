## 10.2 PMA Registers

### 10.2.1 PMA Standard Control 1: Address 1.0

  Bit           Name           Type    Default                                    Description

# 0 Loopback              RW        0b      Loopback

                               PD                This enables the PMA analog system loopback.
                                                  0b = Normal operation.
                                                  1b = Enable loopback mode.

# 1 Reserved              RSV               Reserved. Do not modify.

  5:2    10 GbE Speed          ROS       0x0     10 GbE Speed Selection
         Selection [3:0]                          0000b = 10 GbE
                                                  xxx1b = 10PASS-TS / 2BASE-TL
                                                  xx1xb = Reserved
                                                  x1xxb = Reserved
                                                  1xxxb = Reserved

# 6 Speed Selection MSB   RW        1b      Speed Selection MSB

                               PD                {6,D}:
                                                  00b = Not supported
                                                  01b = 100 Mb/s
                                                  10b = 1000 Mb/s
                                                  11b = Speed set by Bits [5:2]
  A:7    Reserved              RSV               Reserved. Do not modify.
   B     Low Power             RW        0b      Low Power
                               PD                A 1b written to this register causes the PMA to enter low-power mode. If a
                                                 global chip low-power state is desired, use Bit [B] in the Global Standard
                                                 Control 1: Address 1E.0 register.
                                                  0b = Normal operation.
                                                  1b = Low-power mode.

   C     Reserved              RSV               Reserved. Do not modify.
   D     Speed Selection LSB   RW        1b      Speed Selection LSB
                               PD                {6,D}:
                                                  00b = Not supported
                                                  01b = 100 Mb/s
                                                  10b = 1000 Mb/s
                                                  11b = Speed set by Bits [5:2]
  F:E    Reserved              RSV               Reserved. Do not modify.

### 10.2.2 PMA Standard Status 1: Address 1.1

  Bit           Name           Type    Default                                    Description

# 0 Reserved              RSV               Reserved. Do not modify.

# 1 Low Power Ability     ROS       1b      Low Power Ability

                                                 Indicates whether the PHY supports a low-power mode.
                                                  0b = No low-power mode supported.
                                                  1b = PMA supports low-power mode.

333369-009                                                                                                                    865
                                    Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                                        PHY Registers

  Bit             Name            Type        Default                                        Description

    2 PMA Receive Link         LL                    PMA Receive Link Status

          Status                                         This indicates the status of the PMA receive link. This is the latched version of
                                                         1.E800.0 (see Section 10.2.46).
                                                          0b = Link lost since last read.
                                                          1b = Link up.
                                                         Note: This is latching low, so it can only be used to detect link drops, and
                                                                  not the current status of the link without performing back-to-back
                                                                  reads.
  6:3     Reserved                RSV                    Reserved. Do not modify.

# 7 Fault                   RO                     Fault

                                                         This is the top-level fault indicator flag for the PMA. This bit is set if either of
                                                         the two bits 1.8.B or 1.8.A are set (see Section 10.2.9).
                                                          0b = No fault detected.
                                                          1b = Fault condition detected.
  F:8     Reserved                RSV                    Reserved. Do not modify.

### 10.2.3 PMA Standard Device Identifier 1: Address 1.2

  Bit                Name               Type     Default                                       Description

  F:0     Device ID MSW [1F:10]          RO                  Device ID MSW
                                                             Bits [31:16] of the Device ID.

### 10.2.4 PMA Standard Device Identifier 2: Address 1.3

  Bit                Name               Type     Default                                       Description

  F:0     Device ID LSW [F:0]            RO                  Device ID LSW
                                                             Bits [15-0] of the Device ID.

### 10.2.5 PMA Standard Speed Ability: Address 1.4

  Bit                Name               Type     Default                                       Description

    0 PMA 10 GbE Capable            ROS         1b       PMA 10 GbE Capable

                                                              0b = PMA is not 10 GbE capable.
                                                              1b = PMA is 10 GbE capable.
                                                             This is always set to 1b in the X550.

    1 PMA 2BASE-TL Capable          ROS         0b       PMA 2BASE-TL Capable

                                                              0b = PMA is not 2BASE-TL capable.
                                                              1b = PMA is 2BASE-TL capable.
                                                             This is always set to 0b in the X550.

    2 PMA 10PASS-TS Capable         ROS         0b       PMA 10PASS-TS Capable

                                                              0b = PMA is not 10PASS-TS capable.
                                                              1b = PMA is 10PASS-TS capable.
                                                             This is always set to 0b in the X550.

# 3 Reserved                      RSV                  Reserved. Do not modify.

866                                                                                                                               333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit               Name           Type      Default                                      Description

    4 PMA 1 GbE Capable            ROS        1b       PMA 1 GbE Capable

                                                           0b = PMA is not 1 GbE capable.
                                                           1b = PMA is 1 GbE capable.
                                                          This is always set to 1b in the X550.

    5 PMA 100 Mb/s Capable         ROS        1b       PMA 100 Mb/s Capable

                                                           0b = PMA is not 100 Mb/s capable.
                                                           1b = PMA is 100 Mb/s capable.
                                                          This is always set to 1b in the X550.

    6 PMA 10 Mb/s Capable          ROS        0b       PMA 10 Mb/s Capable

                                                           0b = PMA is not 10 Mb/s capable.
                                                           1b = PMA is 10 Mb/s capable.
                                                          This is always set to 0b in the X550.
  F:7    Reserved                     RSV                 Reserved. Do not modify.

### 10.2.6 PMA Standard Devices in Package 1: Address 1.5

  Bit           Name            Type    Default                                         Description

# 0 Clause 22 Registers    ROS         0b        Clause 22 Registers Present

         Present                                       0b = Clause 22 registers are not present in the package.
                                                       1b = Clause 22 registers are present in the package.
                                                      This is always set to 0b, as there are no Clause 22 registers in the X550.

    1 PMA Present            ROS         1b        PMA Present

                                                       0b = PMA is not present.
                                                       1b = PMA is present in the package.
                                                      This is always set to 1b, as there is PMA functionality in the X550.

    2 WIS Present            ROS         0b        WIS Present

                                                       0b = WIS is not present in the package.
                                                       1b = WIS is present in the package.
                                                      This is always set to 0b, as there is no WIS functionality in the X550.

    3 PCS Present            ROS         1b        PCS Present

                                                       0b = PCS is not present in the package.
                                                       1b = PCS is present in the package.
                                                      This is always set to 1b, as there is PCS functionality in the X550.

    4 PHY XS Present         ROS         0b        PHY XS Present

                                                       0b = PHY XS is not present in the package.
                                                       1b = PHY XS is present in the package.
                                                      This is always set to 0b as there is no PHY XS interface in the X550.,

    5 DTE XS Present         ROS         0b        DTE XS Present

                                                       0b = DTE XS is not present in the package.
                                                       1b = DTE XS is present in the package.
                                                      This is always set to 0b, as there is no DTE XAUI interface in the X550.

    6 TC Present             ROS         0b        TC Present

                                                       0b = TC is not present in the package.
                                                       1b = TC is present in the package.
                                                      This is always set to 0b, as there is no TC functionality in the X550.

# 7 Auto-Negotiation       ROS         1b        Auto-Negotiation Present

         Present                                       0b = Auto-negotiation is not present in the package.
                                                       1b = Auto-negotiation is present in the package.
                                                      This is always set to 1b, as there is auto-negotiation in the X550.
  F:8    Reserved               RSV                   Reserved. Do not modify.

333369-009                                                                                                                         867
                                   Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.2.7 PMA Standard Devices in Package 2: Address 1.6

  Bit           Name              Type     Default                                    Description

  C:0     Reserved                RSV                Reserved. Do not modify.
      D   Clause 22 Extension     ROS        1b      Clause 22 Extension Present
          Present                                     0b = Clause 22 extension is not present in the package.
                                                      1b = Clause 22 extension is present in the package.
                                                     This is always set to 1b, as the X550 uses this device for the GbE registers.
      E   Vendor Specific         ROS        1b      Vendor-Specific Device #1 Present
          Device #1 Present                           0b = Device #1 is not present in the package.
                                                      1b = Device #1 is present in the package.
                                                     This is always set to 1b, as the X550 uses this device for the Global registers.
      F   Vendor Specific         ROS        1b      Vendor-Specific Device #2 Present
          Device #2 Present                           0b = Device #2 is not present in the package.
                                                      1b = Device #2 is present in the package.
                                                     This is always set to 1b, as the X550 uses this device for the DSP PMA
                                                     registers.

### 10.2.8 PMA Standard Control 2: Address 1.7

  Bit             Name              Type     Default                                    Description

  3:0     PMA Device Type [3:0]     ROS        0x9     PMA Device Type
                                                        0x9 = 10GBASE-T PMA type.
                                                        All other values are reserved.
                                                       This is always set to 0x9, as the X550 is a 10GBASE-T device.
  F:4     Reserved                  RSV                Reserved. Do not modify.

### 10.2.9 PMA Standard Status 2: Address 1.8

  Bit           Name              Type     Default                                    Description

    0 PMA Loopback            ROS        1b      PMA Loopback Ability

          Ability                                     0b = PMA does not support loopback.
                                                      1b = PMA supports loopback.
                                                     This is always set to 1b, as the PMA in the X550 supports loopback.

    1 PMA 10GBASE-EW          ROS        0b      PMA 10GBASE-EW Capable

          Capable                                     0b = PMA does not support 10GBASE-EW.
                                                      1b = PMA supports 10GBASE-EW.
                                                     This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    2 PMA 10GBASE-LW          ROS        0b      PMA 10GBASE-LW Capable

          Capable                                     0b = PMA does not support 10GBASE-LW.
                                                      1b = PMA supports 10GBASE-LW.
                                                     This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    3 PMA 10GBASE-SW          ROS        0b      PMA 10GBASE-SW Capable

          Capable                                     0b = PMA does not support 10GBASE-SW.
                                                      1b = PMA supports 10GBASE-SW.
                                                     This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

868                                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit           Name            Type     Default                                     Description

    4 PMA 10GBASE-LX4        ROS        0b      PMA 10GBASE-LX4 Capable

         Capable                                    0b = PMA does not support 10GBASE-LX4.
                                                    1b = PMA supports 10GBASE-LX4.
                                                   This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    5 PMA 10GBASE-ER         ROS        0b      PMA 10GBASE-ER Capable

         Capable                                    0b = PMA does not support 10GBASE-ER.
                                                    1b = PMA supports 10GBASE-ER.
                                                   This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    6 PMA 10GBASE-LR         ROS        0b      PMA 10GBASE-LR Capable

         Capable                                    0b = PMA does not support 10GBASE-LR.
                                                    1b = PMA supports 10GBASE-LR.
                                                   This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    7 PMA 10GBASE-SR         ROS        0b      PMA 10GBASE-SR Capable

         Capable                                    0b = PMA does not support 10GBASE-SR.
                                                    1b = PMA supports 10GBASE-SR.
                                                   This field is always set to 0b, as the PMA in the X550 supports only 10GBASE-T.

    8 PMD Transmit           ROS        1b      PMD Transmit Disable Ability

         Disable Ability                           This bit indicates whether the PMD has the capability of disabling its
                                                   transmitter.
                                                     0b = PMD does not have the capability of disabling the transmitter.
                                                     1b = PMD has the capability of disabling the transmitter.
                                                   This field is always set to 1b, as the PMD in the X550 has this ability.

# 9 Extended Abilities     ROS        1b      Extended Abilities

                                                    0b = PMA does not have extended abilities.
                                                    1b = PMA has extended abilities listed in register 1.11.
                                                   This field is set to 1b, as the PMA in the X550 has extended abilities.
   A     Receive Fault           LH                Receive Fault
                                                   This bit indicates whether there is a fault somewhere along the receive path.
                                                   This is a hardware fault and should never occur during normal operation.
                                                    0b = No fault condition on receive path.
                                                    1b = Fault condition on receive path.
   B     Transmit Fault          LH                Transmit Fault
                                                   This bit indicates whether there is a fault somewhere along the transmit path.
                                                   This is a hardware fault and should never occur during normal operation.
                                                    0b = No fault condition on transmit path.
                                                    1b = Fault condition on transmit path.
   C     Receive Fault          ROS        1b      Receive Fault Location Ability
         Location Ability                          This bit indicates whether the PMA has the ability to locate faults along the
                                                   receive path.
                                                    0b = PMA does not have the capability to detect a fault condition on the
                                                           receive path.
                                                    1b = PMA has the capability to detect a fault condition on the receive path.
   D     Transmit Fault         ROS        1b      Transmit Fault Location Ability
         Location Ability                          This bit indicates whether the PMA has the ability to locate faults along the
                                                   transmit path.
                                                     0b = PMA does not have the capability to detect a fault condition on the
                                                           transmit path.
                                                     1b = PMA has the capability to detect a fault condition on the transmit path.
  F:E    Device Present [1:0]   ROS        10b     Device Present
                                                    00b = No device at this address.
                                                    01b = No device at this address.
                                                    10b = Device present at this address.
                                                    11b = No device at this address.
                                                   This field is always set to 10b, as the PMA is present in the X550.

333369-009                                                                                                                     869
                                      Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                   PHY Registers

### 10.2.10 PMD Standard Transmit Disable Control: Address

                     1.9

  Bit            Name             Type     Default                                      Description

    0 PMD Global Transmit     RW         0b      PMD Global Transmit Disable

          Disable                 PD                 When set, this bit disables (and overrides) all four channels, and sets the
                                                     average launch power on all pairs to less than -53 dBm.
                                                      0b = Normal operation.
                                                      1b = Disable output on all channels.

    1 PMD Channel 0           RW         0b      PMD Channel 0 Transmit Disable

          Transmit Disable        PD                 When disabled, the average launch power on a pair is set to less than
                                                     -53 dBm.
                                                      0b = Normal operation.
                                                      1b = Disable output on transmit channel 0.

    2 PMD Channel 1           RW         0b      PMD Channel 1 Transmit Disable

          Transmit Disable        PD                 When disabled, the average launch power on a pair is set to less than
                                                     -53 dBm.
                                                      0b = Normal operation.
                                                      1b = Disable output on transmit channel 1.

    3 PMD Channel 2           RW         0b      PMD Channel 2 Transmit Disable

          Transmit Disable        PD                 When disabled, the average launch power on a pair is set to less than
                                                     -53 dBm.
                                                      0b = Normal operation.
                                                      1b = Disable output on transmit channel 2.

    4 PMD Channel 3           RW         0b      PMD Channel 3 Transmit Disable

          Transmit Disable        PD                 When disabled, the average launch power on a pair is set to less than
                                                     -53 dBm.
                                                      0b = Normal operation.
                                                      1b = Disable output on transmit channel 3.

  F:5     Reserved                RSV                Reserved. Do not modify.

### 10.2.11 PMD Standard Signal Detect: Address 1.A

  Bit          Name             Type     Default                                      Description

    0 PMD Global Signal     RO                 PMD Global Signal Detect

          Detect                                   This bit is marked when all required, valid Ethernet signals to create a connection
                                                   are present on the line.
                                                    0b = No signal detected.
                                                    1b = Signals detected on all required channels.

    1 PMD Channel 0         RO                 PMD Channel 0 Signal Detect

          Signal Detect                            These bits are used to indicate the presence of signals on a given pair. A signal is
                                                   defined as an auto-negotiation pulse or Ethernet signals.
                                                    0b = No signal detected.
                                                    1b = Signal detected on receive channel 0.

870                                                                                                                        333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit         Name          Type        Default                                         Description

    2 PMD Channel 1          RO                   PMD Channel 1 Signal Detect

         Signal Detect                               These bits are used to indicate the presence of signals on a given pair. A signal is
                                                     defined as an auto-negotiation pulse or Ethernet signals.
                                                      0b = No signal detected.
                                                      1b = Signal detected on receive channel 1.

    3 PMD Channel 2          RO                   PMD Channel 2 Signal Detect

         Signal Detect                               These bits are used to indicate the presence of signals on a given pair. A signal is
                                                     defined as an auto-negotiation pulse or Ethernet signals.
                                                      0b = No signal detected.
                                                      1b = Signal detected on receive channel 2.

    4 PMD Channel 3          RO                   PMD Channel 3 Signal Detect

         Signal Detect                               These bits are used to indicate the presence of signals on a given pair. A signal is
                                                     defined as an auto-negotiation pulse or Ethernet signals.
                                                      0b = No signal detected.
                                                      1b = Signal detected on receive channel 3.
  F:5    Reserved           RSV                      Reserved. Do not modify.

### 10.2.12 PMD Standard 10G Extended Ability Register:

                    Address 1.B

  Bit          Name              Type     Default                                         Description

  1:0    Reserved                RSV                   Reserved. Do not modify.

    2 PMA 10GBASE-T           ROS           1b      PMA 10GBASE-T Capable

         Capable                                        0b = PMA incapable of 10GBASE-T.
                                                        1b = PMA capable of 10GBASE-T.
                                                       This field is set to 1b, as the PMA in the X550 supports 10GBASE-T.
  F:3    Reserved                RSV                   Reserved. Do not modify.

### 10.2.13 PMA Standard Package Identifier 1: Address 1.E

  Bit               Name                Type        Default                                    Description

  F:0    Package ID MSW [1F:10]          RO                   Package ID MSW
                                                              Bits [31:16] of the Package ID.

### 10.2.14 PMA Standard Package Identifier 2: Address 1.F

  Bit               Name                Type        Default                                    Description

  F:0    Package ID LSW [F:0]            RO                   Package ID LSW
                                                              Bits [15:0] of the Package ID.

333369-009                                                                                                                            871
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.2.15 PMA 10GBASE-T Status: Address 1.81

  Bit            Name              Type     Default                                    Description

# 0 Link Partner             RO                 Link Partner Information Valid

          Information Valid                           When set, this bit indicates that the start-up protocol has completed.
                                                       0b = 10GBASE-T link partner information is not valid.
                                                       1b = 10GBASE-T link partner information is valid.
  F:1     Reserved                 RSV                Reserved. Do not modify.

### 10.2.16 PMA 10GBASE-T Pair Swap and Polarity Status:

                     Address 1.82

  Bit              Name              Type     Default                                   Description

  1:0     MDI / MD-X Connection       RO                MDI/MD-X Connection State
          State [1:0]                                   These two bits indicate the current status of pair swaps at the MDI / MD-X
                                                         00b = Pair A/B and C/D crossover.
                                                         01b = Pair C/D crossover.
                                                         10b = Pair A/B crossover.
                                                         11b = No crossover.
  7:2     Reserved                   RSV                Reserved. Do not modify.
  B:8     Pair Polarity [3:0]         RO                Pair Polarity
                                                        When set, this bit indicates that the wires on the respective pair are
                                                        reversed.
                                                         0b = Polarity of pair is normal.
                                                         1b = Polarity of pair is reversed.
                                                        where:
                                                         [0] = Pair A polarity.
                                                         [1] = Pair B polarity.
                                                         [2] = Pair C polarity.
                                                         [3] = Pair D polarity.
  F:C     Reserved                   RSV                Reserved. Do not modify.

### 10.2.17 PMA 10GBASE-T Tx Power Backoff Setting:

                     Address 1.83

  Bit              Name              Type     Default                                   Description

  9:0     Reserved                   RSV                Reserved. Do not modify.
  C:A     Tx Power Backoff [2:0]      RO                Transmit Power Backoff
                                                        The power backoff of the PMA.
                                                         000b = 0 dB
                                                         001b = 2 dB
                                                         010b = 4 dB
                                                         011b = 6 dB
                                                         100b = 8 dB
                                                         101b = 10 dB
                                                         110b = 12 dB
                                                         111b = 14 dB

872                                                                                                                       333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit            Name                Type     Default                                     Description

  F:D    Link Partner Tx Power       RO                 Link Partner Transmit Power Backoff
         Backoff [2:0]                                  The power backoff of the link partner.
                                                         000b = 0 dB
                                                         001b = 2 dB
                                                         010b = 4 dB
                                                         011b = 6 dB
                                                         100b = 8 dB
                                                         101b = 10 dB
                                                         110b = 12 dB
                                                         111b = 14 dB

### 10.2.18 PMA 10GBASE-T Test Modes: Address 1.84

  Bit            Name                Type     Default                                     Description

  9:0    Reserved                    RSV                Reserved. Do not modify.
  C:A    Transmitter Test            RW         0x0     Transmitter Test Frequencies
         Frequencies [2:0]           PD                 The test frequencies associated with test mode #4 in [F:D].
                                                         000b = Reserved
                                                         001b = Dual tone #1
                                                         010b = Dual tone #2
                                                         011b = Reserved
                                                         100b = Dual tone #3
                                                         101b = Dual tone #4
                                                         110b = Dual tone #5
                                                         111b = Reserved
  F:D    Test Mode Control [2:0]     RW         0x0     Test Mode Control
                                     PD                 Test mode control for the PMA as defined in Section 55.5.2 of 802.3an.
                                                         000b = Normal operation.
                                                         001b = Master source for slave mode jitter test.
                                                         010b = Master mode jitter test.
                                                         011b = Slave mode jitter test.
                                                         100b = Transmitter distortion test.
                                                         101b = PSD and power level test.
                                                         110b = Transmitter droop test.
                                                         111b = Pseudo random test mode for BER Monitor.

### 10.2.19 PMA 10GBASE-T SNR Operating Margin Channel

                    A: Address 1.85

  Bit           Name               Type     Default                                     Description

  F:0    Channel A Operating       RO                 Channel A Operating Margin
         Margin [F:0]                                 Operating margin (dB) of Channel A.
                                                      The excess SNR that is used by the channel, over and above the minimum SNR
                                                      required to operate at a BER of 10-12. It is reported with 0.1 dB of resolution to
                                                      an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB. The number is
                                                      in offset binary, with 0.0 dB represented by 0x8000.

333369-009                                                                                                                           873
                                        Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                                 PHY Registers

### 10.2.20 PMA 10GBASE-T SNR Operating Margin Channel

                  B: Address 1.86

  Bit         Name               Type     Default                                     Description

  F:0   Channel B Operating      RO                 Channel B Operating Margin
        Margin [F:0]                                Operating margin (dB) of Channel B.
                                                    The excess SNR that is used by the channel, over and above the minimum SNR
                                                    required to operate at a BER of 10-12. It is reported with 0.1 dB of resolution to
                                                    an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB. The number is
                                                    in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.21 PMA 10GBASE-T SNR Operating Margin Channel

                  C: Address 1.87

  Bit         Name               Type     Default                                     Description

  F:0   Channel C Operating      RO                 Channel C Operating Margin
        Margin [F:0]                                Operating margin (dB) of Channel C.
                                                    The excess SNR that is used by the channel, over and above the minimum SNR
                                                    required to operate at a BER of 10-12. It is reported with 0.1 dB of resolution to
                                                    an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB. The number is
                                                    in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.22 PMA 10GBASE-T SNR Operating Margin Channel

                  D: Address 1.88

  Bit         Name               Type     Default                                     Description

  F:0   Channel D Operating      RO                 Channel D Operating Margin
        Margin [F:0]                                Operating margin (dB) of Channel D.
                                                    The excess SNR that is used by the channel, over and above the minimum SNR
                                                    required to operate at a BER of 10-12. It is reported with 0.1 dB of resolution to
                                                    an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB. The number is
                                                    in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.23 PMA 10GBASE-T SNR Minimum Operating Margin

                  Channel A: Address 1.89

  Bit           Name               Type     Default                                     Description

  F:0   Channel A Minimum           RO                Channel A Minimum Operating Margin
        Operating Margin [F:0]                        Minimum operating margin (dB) of Channel A since the last link up.
                                                      The excess SNR that is used by the channel, over and above the minimum
                                                      SNR required to operate at a BER of 10-12. It is reported with 0.1 dB of
                                                      resolution to an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB.
                                                      The number is in offset binary, with 0.0 dB represented by 0x8000.

874                                                                                                                       333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.2.24 PMA 10GBASE-T SNR Minimum Operating Margin

                   Channel B: Address 1.8A

  Bit            Name               Type     Default                                  Description

  F:0    Channel B Minimum          RO                 Channel B Minimum Operating Margin
         Operating Margin [F:0]                        Minimum operating margin (dB) of Channel B since the last link up.
                                                       The excess SNR that is used by the channel, over and above the minimum
                                                       SNR required to operate at a BER of 10-12. It is reported with 0.1 dB of
                                                       resolution to an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB.
                                                       The number is in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.25 PMA 10GBASE-T SNR Minimum Operating Margin

                   Channel C: Address 1.8B

  Bit            Name               Type     Default                                  Description

  F:0    Channel C Minimum          RO                 Channel C Minimum Operating Margin
         Operating Margin [F:0]                        Minimum operating margin (dB) of Channel C since the last link up.
                                                       The excess SNR that is used by the channel, over and above the minimum
                                                       SNR required to operate at a BER of 10-12. It is reported with 0.1 dB of
                                                       resolution to an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB.
                                                       The number is in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.26 PMA 10GBASE-T SNR Minimum Operating Margin

                   Channel D: Address 1.8C

  Bit            Name               Type     Default                                  Description

  F:0    Channel D Minimum          RO                 Channel D Minimum Operating Margin
         Operating Margin [F:0]                        Minimum operating margin (dB) of Channel D since the last link up.
                                                       The excess SNR that is used by the channel, over and above the minimum
                                                       SNR required to operate at a BER of 10-12. It is reported with 0.1 dB of
                                                       resolution to an accuracy of 0.5 dB within the range of -12.7 dB to 12.7 dB.
                                                       The number is in offset binary, with 0.0 dB represented by 0x8000.

### 10.2.27 PMA 10GBASE-T Receive Signal Power Channel A:

                   Address 1.8D

  Bit          Name               Type     Default                                   Description

  F:0    Channel A Received       RO                 Channel A Received Signal Power
         Signal Power [F:0]                          Received signal power (dBm) for Channel A.
                                                     The received signal power on the channel. It is reported with 0.1 dB of
                                                     resolution to an accuracy of 0.5 dB within the range of -20.0 dB to +5.5 dB.
                                                     The number is in offset two’s complement notation, with 0.0 dB represented by
                                                     0x8000.

333369-009                                                                                                                      875
                                       Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                             PHY Registers

### 10.2.28 PMA 10GBASE-T Receive Signal Power Channel B:

                     Address 1.8E

  Bit           Name           Type    Default                                    Description

  F:0     Channel B Received   RO                Channel B Received Signal Power
          Signal Power [F:0]                     Received signal power (dBm) for Channel B.
                                                 The received signal power on the channel. It is reported with 0.1 dB of
                                                 resolution to an accuracy of 0.5 dB within the range of -20.0 dB to +5.5 dB.
                                                 The number is in offset two’s complement notation, with 0.0 dB represented by
                                                 0x8000.

### 10.2.29 PMA 10GBASE-T Receive Signal Power Channel C:

                     Address 1.8F

  Bit           Name           Type    Default                                    Description

  F:0     Channel C Received   RO                Channel C Received Signal Power
          Signal Power [F:0]                     Received signal power (dBm) for Channel C.
                                                 The received signal power on the channel. It is reported with 0.1 dB of
                                                 resolution to an accuracy of 0.5 dB within the range of -20.0 dB to +5.5 dB.
                                                 The number is in offset two’s complement notation, with 0.0 dB represented by
                                                 0x8000.

### 10.2.30 PMA 10GBASE-T Receive Signal Power Channel D:

                     Address 1.90

  Bit           Name           Type    Default                                    Description

  F:0     Channel D Received   RO                Channel D Received Signal Power
          Signal Power [F:0]                     Received signal power (dBm) for Channel D.
                                                 The received signal power on the channel. It is reported with 0.1 dB of
                                                 resolution to an accuracy of 0.5 dB within the range of -20.0 dB to +5.5 dB.
                                                 The number is in offset two’s complement notation, with 0.0 dB represented by
                                                 0x8000.

### 10.2.31 PMA 10GBASE-T Skew Delay 1: Address 1.91

  Bit           Name           Type    Default                                    Description

  7:0     Reserved             RSV               Reserved. Do not modify.
  E:8     Skew Delay B [6:0]   RO                Skew Delay for Pair B
                                                 The skew delay reports the current skew delay on each of the pair with respect
                                                 to physical pair A. It is reported with 1.25 ns resolution to an accuracy of 2.5
                                                 ns. The number is in 2’s complement notation with positive values
                                                 representing delay and negative values representing advance with respect to
                                                 physical pair A. If the delay exceeds the maximum amount that can be
                                                 represented by the range (-80 ns to +78.75 ns), the field displays the
                                                 maximum respective value.
      F   Reserved             RSV               Reserved. Do not modify.

876                                                                                                                  333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.2.32 PMA 10GBASE-T Skew Delay 2: Address 1.92

  Bit           Name            Type    Default                                     Description

  6:0    Skew Delay C [6:0]     RO                Skew Delay for Pair C
                                                  The skew delay reports the current skew delay on each of the pair with respect
                                                  to physical pair A. It is reported with 1.25 ns resolution to an accuracy of 2.5
                                                  ns. The number is in two’s complement notation with positive values
                                                  representing delay and negative values representing advance with respect to
                                                  physical pair A. If the delay exceeds the maximum amount that can be
                                                  represented by the range (-80 ns to +78.75 ns), the field displays the
                                                  maximum respective value.

# 7 Reserved               RSV               Reserved. Do not modify.

  E:8    Skew Delay D [6:0]     RO                Skew Delay for Pair D
                                                  The skew delay reports the current skew delay on each of the pair with respect
                                                  to physical pair A. It is reported with 1.25 ns resolution to an accuracy of 2.5
                                                  ns. The number is in two’s complement notation with positive values
                                                  representing delay and negative values representing advance with respect to
                                                  physical pair A. If the delay exceeds the maximum amount that can be
                                                  represented by the range (-80 ns to +78.75 ns), the field displays the
                                                  maximum respective value.
   F     Reserved               RSV               Reserved. Do not modify.

### 10.2.33 PMA 10GBASE-T Fast Retrain Status and Control:

                     Address 1.93

  Bit           Name            Type    Default                                     Description

# 0 Fast Retrain Enable    RW        0b      Fast Retrain Enable

                                                   0b = Fast retrain capability is disabled.
                                                   1b = Fast retrain capability is enabled.
  2:1    Fast Retrain Signal    RW        00b     Fast Retrain Signal Type
         Type [1:0]                                00b = PHY signals IDLE during fast retrain.
                                                   01b = PHY signals Local Fault during fast retrain.
                                                   10b = PHY signals Link Interruption during fast retrain.
                                                   11b = Reserved.

# 3 Fast Retrain           RO                Fast Retrain Negotiated

         Negotiated                                0b = Fast retrain capability was not negotiated.
                                                   1b = Fast retrain capability was negotiated.

# 4 Fast Retrain Ability   RO                Fast Retrain Ability

                                                   0b = Fast retrain capability is not supported.
                                                   1b = Fast retrain capability is supported.

# 5 Reserved               RS                Reserved. Do not modify.

  A:6    LD Fast Retrain        SCT       0x0     Local Device Fast Retrain Count
         Count [4:0]                              Counts the number of fast retrains requested by the local device.
                                                  Saturating clear on read counter.
  F:B    LP Fast Retrain        SCT       0x0     Link Partner Fast Retrain Count
         Count [4:0]                              Counts the number of fast retrains requested by the link partner.
                                                  Saturating clear on read counter.

333369-009                                                                                                                     877
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

### 10.2.34 PMA TimeSync Capability: Address 1.1800

  Bit           Name           Type      Default                                    Description

# 0 TimeSync Receive      RO         0b       TimeSync Receive Path Data Delay

          Path Data Delay                            0b = PMA does not provide information on receive path data delay.
                                                     1b = PMA provides information on receive path data delay in registers 1.1805
                                                          through 1.1808.

# 1 TimeSync Transmit     RO         0b       TimeSync Transmit Path Data Delay

          Path Data Delay                            0b = PMA does not provide information on transmit path data delay.
                                                     1b = PMA provides information on transmit path data delay in registers
                                                          1.1801 through 1.1804.
  F:2     Reserved             RSV         0x0      Reserved. Do not modify.

### 10.2.35 PMA TimeSync Transmit Path Data Delay 1:

                     Address 1.1801

  Bit                Name                Type      Default                              Description

  F:0     Maximum PMA Transmit Path       RO                 Maximum PMA Transmit Path Data Delay LSW
          Data Delay LSW [F:0]                               LSW of maximum PMA transmit delay in nanoseconds.

### 10.2.36 PMA TimeSync Transmit Path Data Delay 2:

                     Address 1.1802

  Bit                Name                Type      Default                              Description

  F:0     Maximum PMA Transmit Path       RO                 Maximum PMA Transmit Path Data Delay MSW
          Data Delay MSW [F:0]                               MSW of maximum PMA transmit delay in nanoseconds.

### 10.2.37 PMA TimeSync Transmit Path Data Delay 3:

                     Address 1.1803

  Bit                Name                Type      Default                              Description

  F:0     Minimum PMA Transmit Path       RO                 Minimum PMA Transmit Path Data Delay LSW
          Data Delay LSW [F:0]                               LSW of minimum PMA transmit delay in nanoseconds.

### 10.2.38 PMA TimeSync Transmit Path Data Delay 4:

                     Address 1.1804

  Bit                Name                Type      Default                              Description

  F:0     Minimum PMA Transmit Path       RO                 Minimum PMA Transmit Path Data Delay MSW
          Data Delay MSW [F:0]                               MSW of minimum PMA transmit delay in nanoseconds.

878                                                                                                                   333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.2.39 PMA TimeSync Receive Path Data Delay 1:

                    Address 1.1805

  Bit               Name                Type    Default                                Description

  F:0    Maximum PMA Receive Path       RO                 Maximum PMA Receive Path Data Delay LSW
         Data Delay LSW [F:0]                              LSW of maximum PMA Receive delay in nanoseconds.

### 10.2.40 PMA TimeSync Receive Path Data Delay 2:

                    Address 1.1806

  Bit               Name                Type    Default                                Description

  F:0    Maximum PMA Receive Path       RO                 Maximum PMA Receive Path Data Delay MSW
         Data Delay MSW [F:0]                              MSW of maximum PMA Receive delay in nanoseconds.

### 10.2.41 PMA TimeSync Receive Path Data Delay 3:

                    Address 1.1807

  Bit               Name                Type    Default                                Description

  F:0    Minimum PMA Receive Path       RO                 Minimum PMA Receive Path Data Delay LSW
         Data Delay LSW [F:0]                              LSW of minimum PMA Receive delay in nanoseconds.

### 10.2.42 PMA TimeSync Receive Path Data Delay 4:

                    Address 1.1808

  Bit               Name                Type    Default                                Description

  F:0    Minimum PMA Receive Path       RO                 Minimum PMA Receive Path Data Delay MSW
         Data Delay MSW [F:0]                              MSW of minimum PMA Receive delay in nanoseconds.

### 10.2.43 PMA Transmit Standard Interrupt Mask 1:

                    Address 1.D000

  Bit               Name                 Type    Default                                Description

  1:0    Reserved                        RSV                Reserved. Do not modify.

    2 PMA Receive Link Status Mask    RW        0b       PMA Receive Link Status Mask

                                         PD                 Mask for Bit 1.1.2 (see Section 10.2.2).
                                                             0b = Disable interrupt generation.
                                                             1b = Enable interrupt generation.
  F:3    Reserved                        RSV                Reserved. Do not modify.

333369-009                                                                                                    879
                                    Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                              PHY Registers

### 10.2.44 PMA Transmit Standard Interrupt Mask 2:

                     Address 1.D001

  Bit            Name            Type   Default                                    Description

  9:0     Reserved               RSV              Reserved. Do not modify.
      A   Receive Fault Mask     RW       0b      Receive Fault Mask
                                 PD               Mask for Bit 1.8.A (see Section 10.2.9).
                                                   0b = Disable interrupt generation.
                                                   1b = Enable interrupt generation.
      B   Transmit Fault Mask    RW       0b      Transmit Fault Mask
                                 PD               Mask for Bit 1.8.B (see Section 10.2.9).
                                                   0b = Disable interrupt generation.
                                                   1b = Enable interrupt generation.
  F:C     Reserved               RSV              Reserved. Do not modify.

### 10.2.45 PMA Receive Reserved Vendor Provisioning 1:

                     Address 1.E400

  Bit            Name            Type   Default                                    Description

    0 MDI Configuration      RW       0b      MDI Configuration

                                 PD               Setting this bit determines whether MDI is reversed or not.
                                                  Note: The reversal does not change pair polarity. For example, A+ maps to
                                                           D+, etc.
                                                  The value of this bit is sampled during auto-negotiation. If this bit is changed
                                                  manually after auto-negotiation completes, auto-negotiation must be restarted
                                                  to achieve the desired MDI configuration.
                                                   0b = MDI Normal (ABCD -> ABCD)
                                                   1b = MDI Reversed (ABCD -> DCBA)

# 1 Force MDI              RW       0b      Force MDI Configuration

          Configuration          PD               MDI_CFG pin is not brought out. Set this bit to 1b and use the MDI
                                                  Configuration bit to control the MDI pairs’ arrangement.
                                                   0b = Set MDI Configuration based on state of MDI_CFG.
                                                   1b = Ignore state of MDI_CFG pin.

# 2 Enable X550 Cisco      RW       0b      Enable X550 Cisco Fast Retrain

          Fast Retrain           PD               If the link is a X550 PHY and also has Cisco Fast Retrain enabled, use a special
                                                  retrain sequence to bring the link back up without going back through the
                                                  auto-negotiation sequence.
                                                    0b = Disable PMA fast link retrain.
                                                    1b = Enable PMA fast link retrain.
  E:3     Reserved Receive       RW      0x0      Reserved Receive Provisioning 1
          Provisioning 1 [B:0]   PD               Reserved for future use.
      F   External PHY           RW       0b      External PHY Loopback
          Loopback               PD               External PHY loopback expects a loopback connector such that Pair A is
                                                  connected to Pair B, and Pair C is connected to Pair D.
                                                   0b = Normal operation.
                                                   1b = Enable external PHY loopback.

880                                                                                                                    333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.2.46 PMA Receive Vendor State 1: Address 1.E800

  Bit                 Name                  Type     Default                              Description

    0 PMA Receive Link Current Status     RO                PMA Receive Link Current Status

                                                               This is the current state of Bit 1.1.2 (see Section 10.2.2).
                                                                1b = Rx link good.
  F:1    Reserved                           RSV                Reserved. Do not modify.

### 10.2.47 PMA Receive Vendor State 2: Address 1.E811

  Bit            Name             Type     Default                                   Description

  7:0    Total Number Of RFI       RO                Total Number Of RFI Training Link Recovery Events Since Last
         Training Link Recovery                      Auto-Negotiation
         Events Since Last                           The count of the cumulative number of RFI training link recovery events
         AutoNeg [7:0]                               since last auto-negotiation.
                                                     This register is automatically reset to zero during auto-negotiation. The
                                                     result is reported modulo 256 (wrap-around).
  F:8    Total Number Of Link      RO                Total Number Of Link Recovery Events Since Last Auto-Negotiation
         Recovery Events Since                       The count of the cumulative number of Link Recovery Events since last
         Last AutoNeg [7:0]                          auto-negotiation.
                                                     This register is automatically reset to zero during auto-negotiation. It
                                                     increments once for each series of back-to-back fast retrain events.
                                                     The result is reported modulo 256 (wrap-around).

### 10.2.48 PMA Vendor Global Interrupt Flags 1: Address

                    1.FC00

  Bit            Name             Type     Default                                   Description

  9:0    Reserved                  RSV               Reserved. Do not modify.
   A     Standard Alarm 2          RO                Standard Alarm 2 Interrupt
         Interrupt                                   An interrupt was generated from either Bit 1.8.B or 1.8.A.
                                                     An interrupt was generated from status register PMA Standard Status 2:
                                                     Address 1.8 and the corresponding mask register PMA Transmit Standard
                                                     Interrupt Mask 2: Address 1.D001.
                                                      1b = Interrupt
   B     Standard Alarm 1          RO                Standard Alarm 1 Interrupt
         Interrupt                                   An interrupt was generated from Bit 1.1.2.
                                                     An interrupt was generated from status register PMA Standard Status 1:
                                                     Address 1.1 and the corresponding mask register PMA Transmit Standard
                                                     Interrupt Mask 1: Address 1.D000.
                                                      1b = Interrupt
  F:C    Reserved                  RSV               Reserved. Do not modify.

333369-009                                                                                                                       881
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                            PHY Registers
