## 10.3 PCS Registers

### 10.3.1 PCS Standard Control 1: Address 3.0

  Bit             Name          Type   Default                                    Description

  1:0     Reserved              RSV              Reserved. Do not modify.
  5:2     10 GbE Speed          RW      0x0      10 GbE Speed Selection
          Selection [3:0]       PD                0000b = 10 GbE
                                                  xxx1b = 10PASS-TS / 2BASE-TL
                                                  xx1xb = Reserved
                                                  x1xxb = Reserved
                                                  1xxxb = Reserved

# 6 Speed Selection MSB   RW       1b      Speed Selection MSB

                                PD               {6,D}:
                                                  00b = Not supported.
                                                  01b = 100 Mb/s
                                                  10b = 1000 Mb/s
                                                  11b = Speed set by Bits [5:2]
  9:7     Reserved              RSV              Reserved. Do not modify.
      A   Clock Stop Enable     RW       0b      Clock Stop Enable
                                PD                0b = Clock not stoppable.
                                                  1b = The PHY may stop the clock during LPI.
      B   Low Power             RW       0b      Low Power
                                PD               A 1b written to this register causes the PCS to enter low-power mode. If a
                                                 global chip low-power state is desired, Bit [B] in the Global Standard Control
                                                 1: Address 1E.0 register should be set (Section 10.6.1).
                                                  0b = Normal operation.
                                                  1b = Low-power mode.

      C   Reserved              RSV              Reserved. Do not modify.
      D   Speed Selection LSB   RW       1b      Speed Selection LSB
                                PD               {6,D}:
                                                  00b = Not supported
                                                  01b = 100 Mb/s
                                                  10b = 1000 Mb/s
                                                  11b = Speed set by Bits [5:2]
      E   Loopback              RW       0b      Loopback
                                PD               This enables the PCS DSQ system loopback.
                                                  0b = Normal operation.
                                                  1b = Enable loopback mode.

      F   Reserved              RSV              Reserved. Do not modify.

882                                                                                                                 333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.3.2 PCS Standard Status 1: Address 3.1

  Bit            Name            Type       Default                                       Description

# 0 Reserved                RSV                  Reserved. Do not modify.

# 1 Low Power Ability       ROS          1b      Low Power Ability

                                                      Indicates whether the XAUI interface supports a low-power mode.
                                                       0b = No low-power mode supported.
                                                       1b = PCS supports low-power mode.

    2 PCS Receive Link         LL                  PCS Receive Link Status

         Status                                       This indicates the status of the PCS receive link. This is a latching low version
                                                      of Bit 3.20.C (Section 10.3.12).
                                                      Status of the PCS receive link.
                                                       0b = Link lost since last read.
                                                       1b = Link up.
  5:3    Reserved                RSV                  Reserved. Do not modify.

# 6 Clock Stop Capable      ROS          0       Clock Stop Capable

                                                       0b = Clock not stoppable.
                                                       1b = The MAC may stop the clock during LPI.

# 7 Fault                   RO                   Fault

                                                      This is the top-level fault indicator flag for the PCS block. This bit is set if either
                                                      of the two Bits 3.8.B or 3.8.A are set (Section 10.3.9).
                                                       0b = No fault detected.
                                                       1b = Fault condition detected.

# 8 Rx LPI Indication       RO                   Receive LPI Indication

                                                      The source of the LPI signal is configured in 1E.C4A1.3:0.
                                                       0b = Rx PCS is not currently receiving LPI.
                                                       1b = Rx PCS is currently receiving LPI.

# 9 Tx LPI Indication       RO                   Transmit LPI Indication

                                                      The source of the LPI signal is configured in 1E.C4A1.3:0.
                                                       0b = Tx PCS is not currently receiving LPI.
                                                       1b = Tx PCS is currently receiving LPI.
   A     Rx LPI Received          LH                  Receive LPI Received
                                                      The source of the LPI signal is configured in 1E.C4A1.3:0.
                                                       0b = LPI not received.
                                                       1b = Rx PCS has received LPI.
   B     Tx LPI Received          LH                  Transmit LPI Received
                                                      The source of the LPI signal is configured in 1E.C4A1.3:0.
                                                       0b = LPI not received.
                                                       1b = Tx PCS has received LPI.
  F:C    Reserved                RSV                  Reserved. Do not modify.

### 10.3.3 PCS Standard Device Identifier 1: Address 3.2

  Bit            Name              Type       Default                                       Description

  F:0    Device ID MSW [1F:10]         RO                Device ID MSW
                                                         Bits [31:16] of the Device ID.

333369-009                                                                                                                                883
                                       Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                   PHY Registers

### 10.3.4 PCS Standard Device Identifier 2: Address 3.3

  Bit             Name            Type     Default                                       Description

  F:0     Device ID LSW [F:0]      RO                  Device ID LSW
                                                       Bits [15:0] of the Device ID.

### 10.3.5 PCS Standard Speed Ability: Address 3.4

  Bit                   Name                    Type     Default                              Description

      0   10 GbE Capable                        ROS         1b     10 GbE Capable
                                                                    0b = PCS is not 10 GbE capable.
                                                                    1b = PCS is 10 GbE capable.
                                                                   This is always set to 1b in the X550.

    1 PCS 10PASS-TS / 2BASE-TL Capable      ROS         1b     PCS 10PASS-T /2BASE-TL Capable

                                                                    0b = PCS is not 10PASS-TS / 2BASE-TL capable.
                                                                    1b = PCS is 10PASS-TS / 2BASE-TL capable.
                                                                   This is always set to 0b in the X550.
  F:2     Reserved                              RSV                Reserved. Do not modify.

### 10.3.6 PCS Standard Devices in Package 1: Address 3.5

  Bit            Name           Type     Default                                       Description

# 0 Clause 22 Registers   ROS        0b      Clause 22 Registers Present

          Present                                   0b = Clause 22 registers are not present in the package.
                                                    1b = Clause 22 registers are present in the package.
                                                   This is always set to 0b, as there are no Clause 22 registers in the X550.

    1 PMA Present           ROS        1b      PMA Present

                                                    0b = PMA is not present.
                                                    1b = PMA is present in the package.
                                                   This is always set to 1b, as there is PMA functionality in the X550.

    2 WIS Present           ROS        0b      WIS Present

                                                    0b = WIS is not present in the package.
                                                    1b = WIS is present in the package.
                                                   This is always set to 0b, as there is no WIS functionality in the X550.

    3 PCS Present           ROS        1b      PCS Present

                                                    0b = PCS is not present in the package.
                                                    1b = PCS is present in the package.
                                                   This is always set to 1b, as there is PCS functionality in the X550.

    4 PHY XS Present        ROS        0b      PHY XS Present

                                                    0b = PHY XS is not present in the package.
                                                    1b = PHY XS is present in the package.
                                                   This is always set to 0b, as there is no PHY XS interface in the X550.

    5 DTE XS Present        ROS        0b      DTE XS Present

                                                    0b = DTE XS is not present in package.
                                                    1b = DTE XS is present in the package.
                                                   This is always set to 0b, as there is no DTE XAUI interface in the X550.

884                                                                                                                       333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit          Name              Type     Default                                     Description

    6 TC Present              ROS        0b      TC Present

                                                     0b = TC is not present in the package.
                                                     1b = TC is present in the package.
                                                    This is always set to 0b, as there is no TC functionality in the X550.

# 7 Auto-Negotiation        ROS        1b      Auto-Negotiation Present

         Present                                     0b = Auto-negotiation is not present in the package.
                                                     1b = Auto-negotiation is present in the package.
                                                    This is always set to 1b, as there is auto-negotiation in the X550.
  F:8    Reserved                RSV                Reserved. Do not modify.

### 10.3.7 PCS Standard Devices in Package 2: Address 3.6

  Bit          Name              Type     Default                                     Description

  C:0    Reserved                RSV                Reserved. Do not modify.
   D     Clause 22 Extension     ROS        1b      Clause 22 Extension Present
         Present                                     0b = Clause 22 Extension is not present in the package.
                                                     1b = Clause 22 Extension is present in the package.
                                                    This is always set to 1b, as the X550 uses this device for the GbE registers.
   E     Vendor Specific         ROS        1b      Vendor Specific Device #1 Present
         Device #1 Present                           0b = Device #1 is not present in the package.
                                                     1b = Device #1 is present in the package.
                                                    This is always set to 1b, as the X550 uses this device for the global control
                                                    registers.
   F     Vendor Specific         ROS        1b      Vendor Specific Device #2 Present
         Device #2 Present                           0b = Device #2 is not present in the package.
                                                     1b = Device #2 is present in the package.
                                                    This is always set to 1b, as the X550 uses this device for the DSP PMA
                                                    registers.

### 10.3.8 PCS Standard Control 2: Address 3.7

  Bit            Name              Type     Default                                    Description

  1:0    PCS Device Type [1:0]     RW         11b     PCS Device Type
                                   PD                  00b = 10GBASE-R
                                                       01b = 10GBASE-X
                                                       10b = 10GBASE-W
                                                       11b = 10GBASE-T
                                                      The default is 10GBASE-T.
                                                      This is always set to 11b, as the X550 supports only 10GBASE-T operation.
  F:2    Reserved                  RSV                Reserved. Do not modify.

333369-009                                                                                                                          885
                                    Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                     PHY Registers

### 10.3.9 PCS Standard Status 2: Address 3.8

  Bit            Name            Type      Default                                        Description

      0   10GBASE-R Capable      ROS            0b      10GBASE-R Capable
                                                         0b = PCS does not support 10GBASE-R.
                                                         1b = PCS supports 10GBASE-R PCS type.
                                                        This field is always set to 0b, as the PCS in the X550 supports only 10GBASE-T.
      1   10GBASE-X Capable      ROS            0b      10GBASE-X Capable
                                                         0b = PCS does not support 10GBASE-X.
                                                         1b = PCS supports 10GBASE-X PCS type.
                                                        This field is always set to 0b, as the PCS in the X550 supports only 10GBASE-T.
      2   10GBASE-W Capable      ROS            0b      10GBASE-W Capable
                                                         0b = PCS does not support 10GBASE-W.
                                                         1b = PCS supports 10GBASE-W PCS type.
                                                        This field is always set to 0b, as the PCS in the X550 supports only 10GBASE-T.
      3   10GBASE-T Capable      ROS            1b      10GBASE-T Capable
                                                         0b = PCS does not support 10GBASE-T.
                                                         1b = PCS supports 10GBASE-T PCS type.
                                                        This field is always set to 1b, as the PCS in the X550 supports only 10GBASE-T.
  9:4     Reserved               RSV                    Reserved. Do not modify.
      A   Receive Fault            LH                   Receive Fault
                                                        This bit indicates whether there is a fault somewhere along the receive path.
                                                        This bit is duplicated at 3.EC04.2.
                                                         0b = No fault condition on receive path.
                                                         1b = Fault condition on receive path.
      B   Transmit Fault           LH                   Transmit Fault
                                                        This bit indicates whether there is a fault somewhere along the transmit path.
                                                        This bit is duplicated at 3.CC01.0.
                                                         0b = No fault condition on transmit path.
                                                         1b = Fault condition on transmit path.
  D:C     Reserved               RSV                    Reserved. Do not modify.
  F:E     Device Present [1:0]   ROS           10b      Device Present
                                                         00b = No device at this address.
                                                         01b = No device at this address.
                                                         10b = Device present at this address.
                                                         11b = No device at this address.
                                                        This field is always set to 10b, as the PCS registers reside here in the X550.

### 10.3.10 PCS Standard Package Identifier 1: Address 3.E

  Bit                Name                Type        Default                                    Description

  F:0     Package ID MSW [1F:10]          RO                   Package ID MSW
                                                               Bits [31:16] of the Package ID.

### 10.3.11 PCS Standard Package Identifier 2: Address 3.F

  Bit                Name                Type        Default                                    Description

  F:0     Package ID LSW [F:0]            RO                   Package ID LSW
                                                               Bits [15:0] of the Package ID.

886                                                                                                                          333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.3.12 PCS 10GBASE-T Status 1: Address 3.20

  Bit          Name            Type     Default                                     Description

   0     10GBASE-T PCS         RO                 10GBASE-T PCS Block Lock
         Block Lock                               When set, this bit indicates that 10GBASE-T PCS framer has acquired frame
                                                  synchronization and is locked. The interrupt for this bit is at 3.21.F (see
                                                  Section 10.3.13).
                                                   0b = 10GBASE-T PCS framer is not locked.
                                                   1b = 10GBASE-T PCS framer is locked.
   1     10 GbE High BER       RO                 10 GbE High Bit Error Rate
                                                  When set, this bit indicates a high BER is being seen at the PCS. The interrupt
                                                  for this bit is at 3.21.E. The status bit for medium BER is found in Global
                                                  Alarms 2: Address 1E.CC01 (Section 10.6.44).
                                                    0b = PCS is reporting a BER 10-4.
                                                    1b = PCS is reporting a BER  10-4.
  B:2    Reserved              RSV                Reserved. Do not modify.
   C     10 GbE Receive Link   RO                 10 GbE Receive Link Status
         Status                                   When set, this bit indicates that the 10 GbE receive link is functioning properly.
                                                  This is a non-latching version of Bit 3.1.2 (see Section 10.3.2). The receive link
                                                  is up when Block Lock status is asserted and High BER is de-asserted.)
                                                    0b = 10 GbE receive link down.
                                                    1b = 10 GbE receive link up.
  F:D    Reserved              RSV                Reserved. Do not modify.

### 10.3.13 PCS 10GBASE-T Status 2: Address 3.21

  Bit          Name            Type     Default                                     Description

  7:0    Errored Block         SCT        0x0     Errored Block Counter
         Counter [7:0]                            Clear on read. In 10GBASE-T mode, this is taken from the state machine in
                                                  Figure 55.16 in the 10GBASE-T specification.
  D:8    Errored Frame         SCT        0x0     Errored Frame Counter
         Counter [5:0]                            Clear on read. In 10GBASE-T mode, this is taken from the state machine in
                                                  Figure 55.14 in the 10GBASE-T specification. In 10GBASE-R mode, this is
                                                  taken from 3.E
   E     High BER Latched       LH                High Bit Error Rate Latched
                                                  When set, this bit indicates a high BER is being seen at the PCS. This is the
                                                  interrupt for Bit 3.20.1 (see Section 10.3.12).
                                                    0b = PCS is reporting a BER 10-4.
                                                    1b = PCS is reporting a BER  10-4.
   F     PCS Block Lock         LL                PCS Block Lock Latched
         Latched                                  When set, this bit indicates that 10GBASE-T PCS framer has acquired frame
                                                  synchronization and is locked. This is the interrupt for Bit 3.20.0 (see
                                                  Section 10.3.12).
                                                   0b = 10GBASE-T PCS framer is not locked.
                                                   1b = 10GBASE-T PCS framer is locked.

333369-009                                                                                                                        887
                                     Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                                PHY Registers

### 10.3.14 PCS TimeSync Capability: Address 3.1800

  Bit           Name            Type     Default                                     Description

# 0 TimeSync Receive       RO           0b     TimeSync Receive Path Data Delay

          Path Data Delay                             0b = PCS does not provide information on receive path data delay.
                                                      1b = PCS provides information on receive path data delay in registers 3.1805
                                                           through 3.1808.

# 1 TimeSync Transmit      RO           0b     TimeSync Transmit Path Data Delay

          Path Data Delay                             0b = PCS does not provide information on transmit path data delay.
                                                      1b = PCS provides information on transmit path data delay in registers
                                                           3.1801 through 3.1804.
  F:2     Reserved               RSV       0x0       Reserved. Do not modify.

### 10.3.15 PCS TimeSync Transmit Path Data Delay 1:

                     Address 3.1801

  Bit                Name               Type       Default                               Description

  F:0     Maximum PCS Transmit           RO                  Maximum PCS Transmit Path Data Delay LSW
          Path Data Delay LSW [F:0]                          LSW of maximum PCS transmit delay in nanoseconds.

### 10.3.16 PCS TimeSync Transmit Path Data Delay 2:

                     Address 3.1802

  Bit                Name               Type       Default                               Description

  F:0     Maximum PCS Transmit           RO                  Maximum PCS Transmit Path Data Delay MSW
          Path Data Delay MSW [F:0]                          MSW of maximum PCS transmit delay in nanoseconds

### 10.3.17 PCS TimeSync Transmit Path Data Delay 3:

                     Address 3.1803

  Bit                Name               Type       Default                               Description

  F:0     Minimum PCS Transmit Path      RO                  Minimum PCS Transmit Path Data Delay LSW
          Data Delay LSW [F:0]                               LSW of minimum PCS transmit delay in nanoseconds.

### 10.3.18 PCS TimeSync Transmit Path Data Delay 4:

                     Address 3.1804

  Bit                Name               Type       Default                               Description

  F:0     Minimum PCS Transmit Path      RO                  Minimum PCS Transmit Path Data Delay MSW
          Data Delay MSW [F:0]                               MSW of minimum PCS transmit delay in nanoseconds.

888                                                                                                                    333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.3.19 PCS TimeSync Receive Path Data Delay 1:

                    Address 3.1805

  Bit               Name                Type    Default                                  Description

  F:0    Maximum PCS Receive Path        RO                Maximum PCS Receive Path Data Delay LSW
         Data Delay LSW [F:0]                              LSW of maximum PCS Receive delay in nanoseconds.

### 10.3.20 PCS TimeSync Receive Path Data Delay 2:

                    Address 3.1806

  Bit               Name                Type    Default                                  Description

  F:0    Maximum PCS Receive Path        RO                Maximum PCS Receive Path Data Delay MSW
         Data Delay MSW [F:0]                              MSW of maximum PCS Receive delay in nanoseconds.

### 10.3.21 PCS TimeSync Receive Path Data Delay 3:

                    Address 3.1807

  Bit               Name                Type    Default                                  Description

  F:0    Minimum PCS Receive Path        RO                Minimum PCS Receive Path Data Delay LSW
         Data Delay LSW [F:0]                              LSW of minimum PCS Receive delay in nanoseconds.

### 10.3.22 PCS TimeSync Receive Path Data Delay 4:

                    Address 3.1808

  Bit               Name                Type    Default                                  Description

  F:0    Minimum PCS Receive Path        RO                Minimum PCS Receive Path Data Delay MSW
         Data Delay MSW [F:0]                              MSW of minimum PCS Receive delay in nanoseconds.

### 10.3.23 PCS Transmit Vendor Provisioning 1: Address

                    3.C400

  Bit               Name               Type    Default                                  Description

    0 PCS Tx Auxiliary Bit Value    RW        0b       PCS Transmit Auxiliary Bit Value

                                       PD                 The value that is set in the Auxiliary bit of the PCS transmission frame.
                                                          Note: This bit is currently undefined in the 802.3an standard.
  F:1    Reserved                      RSV                Reserved. Do not modify.

333369-009                                                                                                                       889
                                      Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                  PHY Registers

### 10.3.24 PCS Transmit Reserved Vendor Provisioning 1:

                     Address 3.C410

  Bit             Name             Type     Default                                     Description

    0 PCS IEEE Loopback        RW            0b     PCS IEEE Loopback Pass-Through Disable

          Pass-through Disable     PD                   When set, this bit disables the output of the PHY when IEEE loopback is set.
                                                         1b = Disable data pass-through on IEEE loopback.
  F:1     Reserved Transmit        RW         0x0       Reserved Transmit Provisioning 1
          Provisioning 1 [F:1]     PD                   Reserved for future use.

### 10.3.25 PCS Standard Interrupt Mask 1: Address 3.D000

  Bit             Name             Type     Default                                     Description

  1:0     Reserved                 RSV                  Reserved. Do not modify.

    2 PCS Receive Link         RW            0b     PCS Receive Link Status Mask

          Status Mask              PD                   Mask for Bit 3.1.2 (see Section 10.3.2).
                                                         0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
                                                        Note: This bit also shows up as Bit 3.20.C, but only as a status bit.
  9:3     Reserved                 RSV                  Reserved. Do not modify.
      A   Rx LPI Received Mask     RW            0b     Receive LPI Received Mask
                                   PD                   Mask for Bit 3.1.A (see Section 10.3.2).
                                                         0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
      B   Tx LPI Received Mask     RW            0b     Transmit LPI Received Mask
                                   PD                   Mask for Bit 3.1.B (see Section 10.3.2).
                                                         0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.
  F:C     Reserved                 RSV                  Reserved. Do not modify.

### 10.3.26 PCS Standard Interrupt Mask 2: Address 3.D001

  Bit            Name            Type     Default                                      Description

  9:0     Reserved               RSV                  Reserved. Do not modify.
      A   Receive Fault Mask     RW         0b        Receive Fault Mask
                                 PD                   Mask for Bit 3.8.A (see Section 10.3.9).
                                                       0b = Disable interrupt generation.
                                                       1b = Enable interrupt generation.
      B   Transmit Fault Mask    RW         0b        Transmit Fault Mask
                                 PD                   Mask for Bit 3.8.B (see Section 10.3.9).
                                                       0b = Disable interrupt generation.
                                                       1b = Enable interrupt generation.
  F:C     Reserved               RSV                  Reserved. Do not modify.

890                                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

### 10.3.27 PCS Standard Interrupt Mask 3: Address 3.D002

  Bit            Name               Type      Default                                   Description

  D:0    Reserved                   RSV                 Reserved. Do not modify.
   E     10GBASE-T High BER         RW          0b      10GBASE-T High Bit Error Rate Latched Mask
         Latched Mask               PD                  When set, this bit indicates a high BER is being seen at the PCS. This is the
                                                        interrupt for Bit 3.21.E
                                                          0b = Disable interrupt generation.
                                                          1b = Enable interrupt generation.
   F     10GBASE-T PCS Block        RW          0b      10GBASE-T PCS Block Lock Latched Mask
         Lock Latched Mask          PD                  When set, this bit indicates that 10GBASE-T PCS Framer has acquired frame
                                                        synchronization and is locked. This is the interrupt for Bit 3.21.F
                                                         0b = Disable interrupt generation.
                                                         1b = Enable interrupt generation.

### 10.3.28 PCS Receive Vendor State 1: Address 3.E800

  Bit            Name               Type      Default                                   Description

    0 PCS Rx Current Value       RO                  PCS Rx Current Value of Auxiliary Bit

         of Auxiliary Bit                               The current value of the PCS Rx auxiliary bit.
                                                        This value has a maskable interrupt associated with it in 3.EC00.0.
  F:1    Reserved                   RSV                 Reserved. Do not modify.

### 10.3.29 PCS Receive Vendor Alarms 1: Address 3.EC00

  Bit               Name              Type      Default                                  Description

# 0 Change in Auxiliary Bit      LRF                 Change in Auxiliary Bit

                                                          This bit is set when a change is detected in the auxiliary bit.
                                                           1b = Indicates a change in the value of the auxiliary bit.

# 1 Reserved                     RSV                 Reserved. Do not modify.

    2 EEE Rx LPI Received             LH               EEE Rx LPI Received Latched High

         Latched High                                     Indicate LPI ordered-set is detected.
                                                           1b = Rx LPI has been detected

    3 EEE Rx LPI Received             LL               EEE Rx LPI Received Latched Low

         Latched Low                                      Indicate LPI ordered-set is detected.
                                                           1b = Rx LPI has been detected

    4 EEE Rx LPI Alert                LH               EEE Rx LPI Alert

                                                           1b = Rx PCS received alert indication.

    5 LDPC Consecutive Errored        LH               LDPC Consecutive Errored Frame Exceeded

         Frame Exceeded                                   Indicates the consecutive LDPC errored frame has exceeded the
                                                          threshold.
                                                           1b = Rx PCS LDPC consecutive errored frame threshold exceeded

    6 EEE Rx LPI Active On            LH               EEE Rx LPI Active On

                                                           1b = EEE Rx LPI Active On

    7 EEE Rx LPI Active Off           LL               EEE Rx LPI Active Off

                                                           1b = EEE Rx LPI Active Off

333369-009                                                                                                                        891
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               PHY Registers

  Bit                 Name             Type   Default                                  Description

# 8 Invalid 65B Block             LH              Invalid 65-Byte Block

                                                        This bit is set when an invalid 65-byte block (but without LDPC frame
                                                        parity error) has been detected on the received LDPC frame.
                                                         1b = Invalid Rx 65-byte block received in PCS transmission frame.

# 9 Reserved                     RSV              Reserved. Do not modify

      A   LOF Detect                                    LOF Detection Interrupt
                                                         1b = RPL LOF detect
      B   Local Fault Detect                            Local Fault Interrupt
                                                         1b = RPL local fault detect
  D:C     Reserved                     RSV              Reserved. Do not modify.
      E   LDPC Decode Failure           LH              LDPC Decode Failure
                                                        This bit is set when the LDPC decoder fails to decode an LDPC block.
                                                         1b = LDPC decode failure.
      F   CRC Error                     LH              CRC Error
                                                        This bit is set when a CRC-8 error is detected on the receive PCS frame.
                                                         1b = Rx CRC frame error.

### 10.3.30 PCS Receive Vendor Alarms 10: Address 3.EC09

  Bit                 Name             Type   Default                                  Description

    0 PTP Ingress Packet Ready      RO              PTP Ingress Packet Ready

                                                        Asserted when PTP packet is captured. Cleared when the buffer is empty.
                                                         1b = PTP Ingress packet ready.

    1 PTP Ingress Time Stamp        RO              PTP Ingress Time Stamp Ready

          Ready                                         Asserted when PTP packet timestamp is captured. Cleared when the
                                                        timestamp buffer is empty.
                                                          1b = PTP Ingress packet time stamp ready.

    2 PTP Ingress Packet Buffer     LH              PTP Ingress Packet Buffer Overflow Error

          Overflow Error                                Asserted when PTP packet is not captured because the buffer is full.
                                                         1b = PTP Ingress packet buffer overflow error detected.

    3 PTP Ingress Packet            LL              PTP Ingress Packet Correction Field Error

          Correction Field Error                        Asserted when the packet length is too long for the Correction field to be
                                                        updated due to the ingress timestamp appended at the end of packet.
                                                        This should not happen for IEEE1588v2 compliant packets, but if it does,
                                                        the Correction field is not changed.
                                                         1b = PTP Ingress packet correction field error.

    4 PTP Ingress Packet Buffer     LH              PTP Ingress Packet Buffer Parity Error

          Parity Error                                  Asserted when PTP packet pipeline detects FIFO error.
                                                         1b = PTP Ingress packet buffer parity error detected.

    5 PTP Ingress Time Stamp        LH              PTP Ingress Time Stamp Buffer Parity Error

          Buffer Parity Error                           Asserted when PTP packet pipeline detects parity error.
                                                         1b = PTP Ingress time stamp buffer parity error detected.

    6 PTP Ingress Packet            LH              PTP Ingress Packet Pipeline Parity Error

          Pipeline Parity Error                         Asserted when PTP timestamp buffer detects parity error.
                                                         1b = PTP Ingress packet pipeline parity error detected.

    7 PTP Ingress Packet            LL              PTP Ingress Packet Pipeline FIFO Error

          Pipeline FIFO Error                           Asserted when PTP packet buffer detects parity error.
                                                         1b = PTP Ingress packet pipeline FIFO error detected.

    8 PTP Ingress Packet            LH              PTP Ingress Packet Received

          Received                                      Asserted when a valid PTP packet is received. This can be used as the
                                                        valid signal for the received PTP packet information.
                                                         1b = PTP Ingress packet received.

892                                                                                                                   333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

  Bit               Name              Type   Default                                Description

    9 PTP Ingress Packet            LH              PTP Ingress Packet Remove Error

         Remove Error                                  Asserted when the packet length is too long for the UDP checksum to be
                                                       updated during removal of the timestamp appended at the end of
                                                       packet. When this happens, the UDP checksum is set to all-zeros.
                                                        1b = PTP Ingress packet remove error.
   A     PTP Ingress Packet Ready      LH              PTP Ingress Packet Ready FIFO Parity Error
         FIFO Parity Error                             Asserted when PTP packet ready FIFO detects parity error.
                                                        1b = PTP Ingress packet ready FIFO parity error.
   B     PTP Ingress Packet Ready      LH              PTP Ingress Packet Ready FIFO Error
         FIFO Error                                    Asserted when PTP packet ready FIFO detects FIFO error
                                                        1b = PTP Ingress packet ready FIFO error.
  F:C    Reserved                     RSV              Reserved. Do not modify.

### 10.3.31 PCS Vendor Global Interrupt Flags 1: Address

                    3.FC00

  Bit           Name           Type     Default                                   Description

  5:0    Reserved               RSV               Reserved. Do not modify

# 6 Vendor Specific Rx     RO                Vendor Specific Receive Alarms 1 Interrupt

         Alarms 1 Interrupt                       An interrupt was generated from status register PCS Receive Vendor Alarms 1:
                                                  Address 3.EC00 and the corresponding mask register.
  A:7    Reserved               RSV               Reserved. Do not modify
   B     Vendor Specific Tx     RO                Vendor Specific Transmit Alarms 1 Interrupt
         Alarms 1 Interrupt                       An interrupt was generated from status register and the corresponding mask
                                                  register.
   C     Reserved               RSV               Reserved. Do not modify.
   D     Standard Alarm 3       RO                Standard Alarm 3 Interrupt
         Interrupt                                An interrupt was generated from status register PCS 10GBASE-T Status 2:
                                                  Address 3.21 and the corresponding mask register PCS Standard Interrupt
                                                  Mask 3: Address 3.D002.
                                                   1b = Interrupt in standard alarms 3.
   E     Standard Alarm 2       RO                Standard Alarm 2 Interrupt
         Interrupt                                An interrupt was generated from status register PCS Standard Status 2:
                                                  Address 3.8 and the corresponding mask register PCS Standard Interrupt Mask
                                                  2: Address 3.D001.
                                                   1b = Interrupt in standard alarms 2.
   F     Standard Alarm 1       RO                Standard Alarm 1 Interrupt
         Interrupt                                An interrupt was generated from status register PCS Standard Status 1:
                                                  Address 3.1 and the corresponding mask register PCS Standard Interrupt Mask
                                                  1: Address 3.D000.
                                                   1b = Interrupt in standard alarms 1.

333369-009                                                                                                                  893
                                     Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                           PHY Registers

### 10.3.32 PCS Vendor Global Interrupt Flags 3: Address

                     3.FC02

  Bit            Name          Type    Default                                  Description

  5:0     Reserved             RSV               Reserved. Do not modify

# 6 Vendor Specific Rx   RO                Vendor Specific Receive Alarms 6 Interrupt

          Alarms 6 Interrupt                     An interrupt was generated from status register and the corresponding mask
                                                 register.
                                                  1b = Interrupt in vendor specific Rx alarms 6

# 7 Vendor Specific Rx   RO                Vendor Specific Receive Alarms 7 Interrupt

          Alarms 7 Interrupt                     An interrupt was generated from status register and the corresponding mask
                                                 register.
                                                  1b = Interrupt in vendor specific Rx alarms 7
  F:8     Reserved             RSV               Reserved. Do not modify

894                                                                                                              333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers
