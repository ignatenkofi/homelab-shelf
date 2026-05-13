## 2.5 Gb/s. This output carries both data and an

                                                                    embedded 8 GHz or 5 GHz or 2.5 GHz clock that
PET_2_p         T11         AC9
                                      A-Out                         is recovered along with data at the receiving
PET_2_n         T12         AD9                                     end.

PET_3_p         T14        AC10
                                      A-Out
PET_3_n         T15        AD10

PET_4_p                    AC15
                N/A                   A-Out
PET_4_n                    AD15

PET_5_p                    AC16                                     PCIe Serial Data Output: A serial differential
                N/A                   A-Out                         output pair running at 5 Gb/s or 2.5 Gb/s. This
PET_5_n                    AD16
                                                                    output carries both data and an embedded

# 5 GHz or 2.5 GHz clock that is recovered along

PET_6_p                    AC21                                     with data at the receiving end.
                N/A                   A-Out
PET_6_n                    AD21                                     Available only in the X550-BT2.
PET_7_p                    AC22
                N/A                   A-Out
PET_7_n                    AD22

PER_0_p          P6         AB2
                                      A-In
PER_0_n          P7         AB1

PER_1_p          P9         AD6                                     PCIe Serial Data Input: A serial differential
                                      A-In
PER_1_n         P10         AC6                                     input pair running at 8 Gb/s, 5 Gb/s, or 2.5 Gb/
                                                                    s. This input carries both data and an embedded
PER_2_p         P12         AD7                                     8 GHz, 5 GHz, or 2.5 GHz clock that is
                                      A-In                          recovered along with data at the receiving end.
PER_2_n         P13         AC7

PER_3_p         P15        AD12
                                      A-In
PER_3_n         P16        AC12

PER_4_p                    AD13
                N/A                   A-In
PER_4_n                    AC13
                                                                    PCIe Serial Data Input: A serial differential
PER_5_p                    AD18
                N/A                   A-In                          input pair running at 5 Gb/s or 2.5 Gb/s. This
PER_5_n                    AC18                                     input carries both data and an embedded 5 GHz
                                                                    or 2.5 GHz clock that is recovered along with
PER_6_p                    AD19                                     data at the receiving end.
                N/A                   A-In
PER_6_n                    AC19                                     Available only in the X550-BT2.
PER_7_p                     AB23
                N/A                   A-In
PER_7_n                     AB24

                                                                    PCIe Differential Reference Clock In (a 100
PE_CLK_p        N4           Y2                                     MHz differential clock input): This clock is
                                      A-In                          used as the reference clock for the PCIe Tx/Rx
PE_CLK_n        P4           Y1                                     circuitry and by the PCIe core PLL to generate
                                                                    clocks for the PCIe core logic.

50                                                                                                       333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

                  Ball #        Ball #                  Internal   External
  Pin Name                                     Type                                         Name and Function
               (X550-AT2)     (X550-BT2)                Pup/Pdn    Pup/Pdn

                                                                              BIAS: A 4.75 K ±0.1% resistor should be
 PE_RBIAS            T3            Y4         A-Inout
                                                                              connected between RBIAS and RSENSE pins.
                                                                              Connect resistor as close as possible to the chip.
                                                                              Resistor is used for internal impedance
 PE_RSENSE          R3             Y5         A-Inout                         compensation and BIAS current generation
                                                                              circuitry.

                                                                              Wake: Pulled low to indicate that a Power
                                                                              Management Event (PME) is pending and the
 PE_WAKE_N           L3            W1          O/d                   Pup1
                                                                              PCIe link should be restored. Defined in the
                                                                              PCIe specifications.

                                                                              Power and Clock Good Indication: Indicates
                                                                              that power and the PCIe reference clock are
 PE_RST_N           M3             W2           In        Pup
                                                                              within specified values. Defined in the PCIe
                                                                              specifications. Also called PCIe Reset.

1. Pup value should be considered as 10 K.

### 2.2.2 MDI

See AC/DC specifications in Section 12.4.6.

                  Ball #        Ball #                  Internal   External
  Pin Name                                     Type                                         Name and Function
               (X550-AT2)     (X550-BT2)                Pup/Pdn    Pup/Pdn

                                                                              Port 0 pair A+ of the Line Interface:
 MDI0_0_p           A2             A3         A-Inout                         Connects to the Pair A+ input of the
                                                                              transformer. On reset, set to high impedance.

                                                                              Port 0 pair A- of the Line Interface:
 MDI0_0_n           B2             B3         A-Inout                         Connects to the Pair A- input of the transformer.
                                                                              On reset, set to high impedance.

                                                                              Port 0 pair B+ of the Line Interface:
 MDI0_1_p           A3             A5         A-Inout                         Connects to the Pair B+ input of the
                                                                              transformer. On reset, set to high impedance.

                                                                              Port 0 pair B- of the Line Interface:
 MDI0_1_n           B3             B5         A-Inout                         Connects to the Pair B- input of the transformer.
                                                                              On reset, set to high impedance.

                                                                              Port 0 pair C+ of the Line Interface:
 MDI0_2_p           A5             A7         A-Inout                         Connects to the Pair C+ input of the
                                                                              transformer. On reset, set to high impedance.

                                                                              Port 0 pair C- of the Line Interface:
 MDI0_2_n           B5             B7         A-Inout                         Connects to the Pair C- input of the transformer.
                                                                              On reset, set to high impedance.

                                                                              Port 0 pair D+ of the Line Interface:
 MDI0_3_p           A6             A9         A-Inout                         Connects to the Pair D+ input of the
                                                                              transformer. On reset, set to high impedance.

                                                                              Port 0 pair D- of the Line Interface:
 MDI0_3_n           B6             B9         A-Inout                         Connects to the Pair D- input of the transformer.
                                                                              On reset, set to high impedance.

                                                                              Port 0 Analog Test+: Connects to the pair E+
 MDI0_4_p           A8             A11        A-Inout
                                                                              input of the transformer.

                                                                              Port 0 Analog Test-: Connects to the pair E-
 MDI0_4_n           B8             B11        A-Inout
                                                                              input of the transformer.

                                                                              Port 1 pair A+ of the Line Interface:
 MDI1_0_p           B16            A22        A-Inout                         Connects to the Pair A+ input of the
                                                                              transformer. On reset, set to high impedance.

333369-009                                                                                                                     51
                                     Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                              Pin Interface

                  Ball #        Ball #                   Internal   External
  Pin Name                                      Type                                        Name and Function
                (X550-AT2)    (X550-BT2)                 Pup/Pdn    Pup/Pdn

                                                                               Port 1 pair A- of the Line Interface:
 MDI1_0_n           C16            B22         A-Inout                         Connects to the Pair A- input of the transformer.
                                                                               On reset, set to high impedance.

                                                                               Port 1 pair B+ of the Line Interface:
 MDI1_1_p           A14            A20         A-Inout                         Connects to the Pair B+ input of the
                                                                               transformer. On reset, set to high impedance.

                                                                               Port 1 pair B- of the Line Interface:
 MDI1_1_n           B14            B20         A-Inout                         Connects to the Pair B- input of the transformer.
                                                                               On reset, set to high impedance.

                                                                               Port 1 pair C+ of the Line Interface:
 MDI1_2_p           A12            A18         A-Inout                         Connects to the Pair C+ input of the
                                                                               transformer. On reset, set to high impedance.

                                                                               Port 1 pair C- of the Line Interface:
 MDI1_2_n           B12            B18         A-Inout                         Connects to the Pair C- input of the transformer.
                                                                               On reset, set to high impedance.

                                                                               Port 1 pair D+ of the Line Interface:
 MDI1_3_p           A11            A16         A-Inout                         Connects to the Pair D+ input of the
                                                                               transformer. On reset, set to high impedance.

                                                                               Port 1 pair D- of the Line Interface: Connect
 MDI1_3_n           B11            B16         A-Inout                         to the pair D- input of the transformer. On reset,
                                                                               set to high impedance.

                                                                               Port 1 Analog Test+: Connects to the pair E+
 MDI1_4_p            A9            A14         A-Inout
                                                                               input of the transformer.

                                                                               Port 1 Analog Test-: Connects to the pair E-
 MDI1_4_n            B9            B14         A-Inout
                                                                               input of the transformer.

                                                                               Connection point for the band-gap reference
 BG_REXT            B15            D12         A-Inout                         resistor. Should be a precision 1% 2 K resistor
                                                                               tied to ground.

 XTAL_I             D16            D23          A-In                           Positive 50.0 MHz crystal oscillator input.

 XTAL_O             E16            D24         A-Out                           Positive 50.0 MHz crystal oscillator output.

 RSVDF5_VSS         N/A             F5           In

### 2.2.3 Serial Flash

See AC/DC specifications in Section 12.4.4.4.

                  Ball #         Ball #                  Internal   External
     Pin Name                                   Type                                         Name and Function
                (X550-AT2)     (X550-BT2)                Pup/Pdn    Pup/Pdn

                                                                               Flash Serial Output: Serial data output to the
 FLSH_SI             K3             K2          Out        Pup                 Flash (used as ENCRYPTION_EN strap in
                                                                               X550-AT2).

                                                                               Flash Serial Input: Serial data input from the
 FLSH_SO             J3             K1           In
                                                                               Flash.

                                                                               Flash serial clock: Operates at the maximum
 FLSH_SCK            L1             J1          Out                            frequency of 25 MHz.
                                                                               This pin acts as a JTAG_DIS strap.

 FLSH_CE_N           L2             J2          Out                   Pup1     Flash Chip Select Output

1. Pup value should be considered as 3.3 K.

52                                                                                                                   333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

### 2.2.4 SMBus

See the AC/DC specifications in Section 12.4.4.3.

                    Ball #         Ball #                   Internal     External
  Pin Name                                        Type                                              Name and Function
                 (X550-AT2)      (X550-BT2)                 Pup/Pdn      Pup/Pdn

                                                                                      SMBus Clock: One clock pulse is generated for
 SMBCLK               F3               L2          O/d                      Pup1
                                                                                      each data bit transferred.

                                                                                      SMBus Data: Stable during the high period of
 SMBD                  F2              L1          O/d                      Pup1
                                                                                      the clock (unless it is a start or stop condition).

                                                                                      SMBus Alert: Acts as an interrupt pin of a slave
 SMBALRT_N             F1             M2           O/d                      Pup1
                                                                                      device on the SMBus.

1. Pup value should be considered as 10 K.

Note:        If the SMBus is disconnected, use the external pull-up value listed.

### 2.2.5 NC-SI

See AC specifications in Section 12.4.4.5.

                       Ball #           Ball #                     Internal      External
    Pin Name                                             Type                                           Name and Function
                     (X550-AT2)       (X550-BT2)                   Pup/Pdn      Pup/Pdn1

                                                                                               NC-SI Reference Clock Input:
                                                                                               Synchronous clock reference for
 NCSI_CLK_IN                D2              G2         NCSI-In                      Pdn
                                                                                               receive, transmit, and control interface.
                                                                                               It is a 50 MHz clock 100 ppm.

                                                                                               MC Transmit Enable: Indicates that
 NCSI_TX_EN                 B1              G4         NCSI-In                      Pup2
                                                                                               received data from MC is valid.

 NCSI_TXD0                  D3              H2                                                 MC Transmit Data: Data signals from
                                                       NCSI-In                  Pdn or Pup2
 NCSI_TXD1                  D4              G3                                                 the MC to the X550.

                                                                                               Carrier Sense/Receive Data Valid
                                                                                               (CRS/DV) to MC: Indicates that the
 NCSI_CRS_DV                E3              H1        NCSI-Out                      Pdn3
                                                                                               data transmitted from the X550 to MC
                                                                                               is valid.

 NSCI_RXD0                  E1              H3                                                 MC Receive Data: Data signals from
                                                      NCSI-Out                      Pup2
 NCSI_RXD1                  E2              G1                                                 the X550 to the MC.

 NCSI_ARB_IN                C1              F1         NCSI-In                      Pdn3       NC-SI Arbitration In

 NCSI_ARB_OUT               D1              F2        NCSI-Out                                 NC-SI Arbitration Out

1. Pdn or Pup value should be considered as 10 K.
2. Should be pulled up if NC-SI interface is disabled or if set to multi drop configuration.
3. Should be pulled down if NC-SI interface is disabled.

333369-009                                                                                                                              53
                                        Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Pin Interface

### 2.2.6 Software Defined Pins (SDPs)

See AC specifications in Section 12.4.4.1.
See Section 3.5 for more details on configurable SDPs.

               Ball #       Ball #            Internal   External
 Pin Name                              Type                                      Name and Function
             (X550-AT2)   (X550-BT2)          Pup/Pdn    Pup/Pdn

                                                                    General Purpose SDPs — 3.3 V I/Os for
SDP0_0           H1          R4                  Pdn                Function 0: Can be used to support IEEE1588
SDP0_1           G1          P3                  Pdn                auxiliary devices.
                                        T/s
SDP0_2           H2          T4                  Pdn                Input for external interrupts, PCIe function
SDP0_3           G2          R3                  Pdn                disablement, etc.
                                                                    See Section 3.5 for possible usages of the pins.

                                                                    General Purpose SDPs — 3.3 V I/Os for
SDP1_0          H16          T21                 Pdn                Function 1: Can be used to support IEEE1588
SDP1_1          G16          T22                 Pdn                auxiliary devices.
                                        T/s
SDP1_2          H15          U21                 Pdn                Input for external interrupts, PCIe function
SDP1_3          G15          U22                 Pdn                disablement, etc.
                                                                    See Section 3.5 for possible usages of the pins.

### 2.2.7 LEDs

See AC specifications in Section 12.4.4.1.

               Ball #       Ball #            Internal   External
 Pin Name                              Type                                      Name and Function
             (X550-AT2)   (X550-BT2)          Pup/Pdn    Pup/Pdn

                                                                    Port 0 LED0: Programmable LED. By default,
LED0_0           K1          H4        Out       Pdn
                                                                    indicates link up.

                                                                    Port 0 LED1: Programmable LED. By default,
LED0_1           J1           J3       Out       Pdn
                                                                    indicates 10 Gb/s link.

                                                                    Port 0 LED2: Programmable LED. By default,
LED0_2           K2           J4       Out       Pdn
                                                                    indicates link/activity.

                                                                    Port 0 LED3: Programmable LED. By default,
LED0_3           J2          K4        Out       Pdn
                                                                    indicates 1 Gb/s link.

                                                                    Port 1 LED0: Programmable LED. By default,
LED1_0          K16          J21       Out       Pdn
                                                                    indicates link up.

                                                                    Port 1 LED1: Programmable LED. By default,
LED1_1           J16         J22       Out       Pdn
                                                                    indicates 10 Gb/s link.

                                                                    Port 1 LED2: Programmable LED. By default,
LED1_2          K15          K21       Out       Pdn
                                                                    indicates link/activity.

                                                                    Port 1 LED3: Programmable LED. By default,
LED1_3           J15         K22       Out       Pdn
                                                                    indicates 1 Gb/s link.

54                                                                                                       333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

### 2.2.8 RSVD and No-Connect Pins

Connecting RSVD pins based on naming convention:
 • NC — Pin is not connected in the package.
 • RSVD_NC — Reserved pin. Should be left unconnected.
 • RSVD_VSS — Reserved pin. Should be connected to GND.
 • RSVD_VCC — Reserved pin. Should be connected to VCC3P3.

                  Ball #        Ball #
   Pin Name                                  Type                           Name and Function
                (X550-AT2)    (X550-BT2)

RSVDD14_NC           N/A          D14       A-Inout   Reserved/No-connect pin.

RSVDG21_NC                        G21       A-Inout
                     N/A                              Reserved/No-connect pins.
RSVDG22_NC                        G22       A-Inout

RSVDL4_NC                          L4        Out
RSVDL3_NC                          L3        Out
RSVDM4_NC                         M4         Out
RSVDM3_NC                         M3         Out
RSVDN4_NC                         N4         Out
RSVDN3_NC                         N3         Out
RSVDN2_NC                         N2         Out
RSVDP4_NC                          P4        Out
                     N/A                              Reserved/No-connect pins.
RSVDL22_NC                        L22        Out
RSVDL21_NC                        L21        Out
RSVDM22_NC                        M22        Out
RSVDM21_NC                        M21        Out
RSVDN22_NC                        N22        Out
RSVDN21_NC                        N21        Out
RSVDP22_NC                        P22        Out
RSVDP21_NC                        P21        Out

RSVDT23_VSS                       T23        Inout
RSVDT24_VSS                       T24        Inout
                     N/A                              Reserved VSS pins.
RSVDP23_NC                        P23        Inout
RSVDP24_VSS                       P24        Inout

RSVDL15_NC           L15                     Inout
                                  N/A                 Reserved/No-connect pins.
RSVDL16_NC           L16                     Inout

RSVDR22_NC           N/A          R22        Out      Reserved/No-connect pin.

RSVDAA6_NC                       AA6
RSVDAA8_NC                       AA8
RSVDAA10_NC                      AA10
RSVDAA14_NC                      AA14
RSVDAA16_NC                      AA16
RSVDAA18_NC          N/A         AA18                 Reserved/No-connect pins.
RSVDK3_NC                         K3
RSVDM24_NC                       M24
RSVDT2_NC                          T2
RSVDV21_NC                       V21
RSVDY21_NC                        Y21

RSVDG11_NC           N/A          G11        PWR      Reserved/No-connect pin.

333369-009                                                                                      55
                                 Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                       Pin Interface

                   Ball #      Ball #
     Pin Name                              Type                            Name and Function
                (X550-AT2)   (X550-BT2)

RSVDU3_NC                       U3          T/s
RSVDR21_NC                      R21         T/s
RSVDU2_NC                       U2          T/s
RSVDT3_NC                        T3         T/s
                   N/A                               Reserved/No-connect pin.
RSVDV24_NC                      V24         T/s
RSVDU24_NC                      U24         T/s
RSVDU23_NC                      U23         T/s
RSVDV23_NC                      V23         T/s

RSVDC1_NC                       C1
RSVDD1_NC                       D1
RSVDE1_NC                        E1
RSVDE23_NC                      E23
RSVDE24_NC         N/A          E24                  Reserved/No-connect pin.
RSVDF24_NC                      F24
RSVDG24_VSS                     G24
RSVDH22_VSS                     H22
RSVDY20_NC                      Y20

RSVDN24_NC                      N24
                   N/A                               Reserved/No-connect pin.
RSVDW24_NC                      W24

RSVDL23_NC         N/A          L23         O/d      Reserved/No-connect pin.

RSVDJ23_VSS        N/A          J23       In-Only    Reserved VSS pin.

RSVDJ24_VSS        N/A          J24          In      Reserved VSS pin.

RSVDH24_VSS        N/A          H24          In      Reserved VSS pin.

RSVDG23_VSS        N/A          G23       In-Only    Reserved VSS pin.

RSVDAD1_VSS        N/A          AD1          In      Reserved VSS pin.v

RSVDD13_NC                     D13        A-Inout
RSVDC13_NC                      C13       A-Inout
RSVDC11_NC                      C11        A-Out
RSVDD11_NC                     D11         A-Out
RSVDA1_NC                       A1        In-Only
RSVDA24_NC         N/A          A24       In-Only    Reserved/No-connect pin.
RSVDAD24_NC                    AD24       In-Only
RSVDT1_NC                        T1       PWR-O
RSVDU1_NC                       U1        PWR-O
RSVDN13_NC                      N13       PWR-O
RSVDU4_NC                       U4        PWR-O

RSVDR24_NC                      R24       LVDS-O
RSVDR23_NC         N/A          R23       LVDS-O     Reserved/No-connect pin.
RSVDN1_NC                       N1        Out-Only

RSVDP1_NC                        P1        Inout
                   N/A                               Reserved/No-connect pin.
RSVDR1_NC                        R1         Out

RSVDM23_NC                      M23        Inout
                   N/A                               Reserved/No-connect pin.
RSVDN23_NC                      N23         Out

RSVDL14_NC         L14                     Inout
                                N/A                  Reserved/No-connect pin.
RSVDM14_NC         M14                      Out

RSVDV4_NC                        V4
                   N/A                     A-Out     Reserved/No-connect pin.
RSVDV3_NC                        V3

RSVDT1_NC           T1
                                N/A        A-Out     Reserved/No-connect pin.
RSVDR1_NC           R1

56                                                                                                       333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

                  Ball #         Ball #
   Pin Name                                     Type                              Name and Function
                (X550-AT2)     (X550-BT2)

RSVDV1_NC                             V1
                     N/A                       A-Out     Reserved/No-connect pin.
RSVDV2_NC                             V2

RSVDR2_NC            R2
                                     N/A       A-Out     Reserved/No-connect pin.
RSVDP2_NC            P2

#### 2.2.8.1 Pin Differences in the X550-AT Single Port Device

NC = Pin is not connected in the package.

     Name              Ball # (X550-AT2)               Connection (X550-AT)

    MDI1_0_p                   B16                                NC

    MDI1_0_n                   C16                                NC

    MDI1_1_p                   A14                                NC

    MDI1_1_n                   B14                                NC

    MDI1_2_p                   A12                                NC

    MDI1_2_n                   B12                                NC

    MDI1_3_p                   A11                                NC

    MDI1_3_n                   B11                                NC

    MDI1_4_p                   A9                                 NC

    MDI1_4_n                   B9                                 NC

   LAN1_DIS_N                  M16                                NC

For additional information on these pins in the X550-AT2, see Section 2.2.2.

### 2.2.9 Miscellaneous

See AC/DC specifications in Section 12.4.4.1.

                    Ball #        Ball #                 Internal      External
   Pin Name                                     Type                                          Name and Function
                  (X550-AT2)    (X550-BT2)               Pup/Pdn       Pup/Pdn

                                                                                   LAN Power Good: A 3.3 V input signal. A
                                                                                   transition from low to high initializes the
                                                                                   X550 into operation. If not used
LAN_PWR_GOOD          N/A             L24         In        Pup          Pup1
                                                                                   (BYPASS_POR = 0b), an internal Power-on-
                                                                                   Reset (POR) circuit triggers the X550 power
                                                                                   up.

BYPASS_POR            N/A             H23         In        Pdn          Pdn2      Bypass POR

                                                                                   Auxiliary Power Available: When set,
                                                                                   indicates that auxiliary power is available
                                                                            3
AUX_PWR               H3               P2         In                    Note       and the X550 should support D3COLD power
                                                                                   state if enabled to do so. This pin is latched
                                                                                   at the rising edge of LAN_PWR_GOOD.

                                                                                   Main Power Good: Indicates that platform
MAIN_PWR_OK           G3               R2         In                    Note4      main power is up. Must be connected
                                                                                   externally.

333369-009                                                                                                                      57
                                     Did this document help answer your questions?

                                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                                                          Pin Interface

                      Ball #          Ball #                     Internal      External
     Pin Name                                       Type                                                  Name and Function
                    (X550-AT2)      (X550-BT2)                   Pup/Pdn       Pup/Pdn

                                                                                               LAN 1 Disable: This pin is a strapping pin
                                                                                               latched at the rising edge of
                        M16                                                                    LAN_PWR_GOOD or PE_RST_N or In-Band
 LAN1_DIS_N                               K24           In5           Pup        Pup1          PCIe Reset. If this pin is not connected or
                       (Strap)                                                                 driven high during initialization, LAN 1 is
                                                                                               enabled. If this pin is driven low during
                                                                                               initialization, LAN 1 port is disabled.

                                                                                               LAN 0 Disable: This pin is a strapping
                                                                                               option pin latched at the rising edge of
                        M15                                                                    LAN_PWR_GOOD or PE_RST_N or In-Band
 LAN0_DIS_N                               K23           In5           Pup        Pup1          PCIe Reset. If this pin is not connected or
                       (Strap)                                                                 driven high during initialization, LAN 0 is
                                                                                               enabled. If this pin is driven low during
                                                                                               initialization, LAN 0 port is disabled.

                                                                                               Encryption Enable: Enable/disable for the
                      Strap on
                                                                                         1     internal IPsec engines.
 ENCRYPTION_EN        FLSH_SI             M1            In            Pup      Pdn/Pup
                                                                                               When pulled up, encryption features are
                        (K3)
                                                                                               enabled.

 THERM_D0_P               C3              F4       A-Inout                                     Thermal Diode Reference: Can be used
 THERM_D0_N               C2              F3       A-Inout                                     to measure on-die temperature.

1. Pup value should be considered as 1 K.
2. Pdn value should be considered as 1 K.
3. Connect AUX_PWR signal to Pup if AUX power is available. Connect Pdn if AUX power is not available. Pup/Pdn value should be
   considered as 1 K.
4. Connect MAIN_PWR_OK signal to Main Power through Pup resistor. Pup value should be considered as 10 K.
5. For the X550-AT and X550-AT2, this pin is input during PCIe_RST_N assertion only, and is output after that.

### 2.2.10 JTAG

See AC specifications in Section 12.4.4.2.

                  Ball #           Ball #                     Internal      External
  Pin Name                                       Type                                                   Name and Function
                (X550-AT2)       (X550-BT2)                   Pup/Pdn       Pup/Pdn

 JTCK               F16             Y22         In-Only         Pup           Pdn1      JTAG Clock Input

 JTDI               F14             W22         In-Only         Pup           Pup2      JTAG Data Input

 JTDO               F15             V22          Out                          Pup3      JTAG Data Output

 JTMS               G14             W21         In-Only         Pup           Pup2      JTAG TMS Input

                                                                                        JTAG Reset Input: Active low reset for the
 JTRST_N            H14             W23         In-Only         Pup           Pdn1
                                                                                        JTAG port.

1. Pdn value should be considered as 470 .
2. Pup value should be considered as 10 K.
3. Pup value should be considered as 3.3 K.

Note:       If the JTAG is disconnected, use the external pull-up or pull-down values listed.

58                                                                                                                              333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

### 2.2.11 Power Supplies

See AC specifications in Section 12.3.1.

     Pin Name            Ball # (X550-AT2)                    Ball # (X550-BT2)                Type      Name and Function

RSVDH21_VSS                      N/A                                   H21                     PWR      Reserved power pin.

RSVDJ14_VSS                      J14                                   N/A                     PWR      Reserved power pin.

                                                         B1, B2, D2, E2, C3, D3, B4, E4,
                                                         C5, D5, B6, E6, C7, D7, B8, E8,
                                                       C9, D9, B10, E10, B12, E12, B13,
                                                         C14, E14, B15, D15, C16, E16,
                                                         B17, D17, C18, E18, B19, D19,
                                                         C20, E20, B21, D21, F21, C22,
                   A1, A4, A7, A10, A13, A15, A16,
                                                       D22, E22, F22, B23, F23, B24, L6,
                    B4, B7, B10, B13, C5, C7, C9,
VSS                                                     L8, L10, L12, L14, L16, L18, L20,     PWR_ALG   1.2 V ground.
                  C11, C13, C15, D6, D8, D10, D12,
                                                       F6, F7, F8, F9, F10, F11, F12, F13,
                          D14, E5, E13, E15
                                                       F14, F15, F16, F17, F18, F19, F20,
                                                          G6, G8, G10, G12, G14, G16,
                                                       G18, G20, H5, H7, H9, H11, H13,
                                                        H15, H17, H19, J6, J8, J10, J12,
                                                         J14, J16, J18, J20, K5, K7, K9,
                                                            K11, K13, K15, K17, K19

                                                       U6, V5, AA1, AC1, AA2, AC2, AD2,
                                                       W3, W4, W6, Y3, AA3, AA4, AB4,
                                                         AA5, AC5, AD5, AB6, Y7, AA7,
                  N6, N7, N9, N10, N12, N13, N15,        AB7, AC8, AD8, Y9, AA9, AB9,
                  N16, P3, P5, P8, P11, P14, R4, R5,     AB10, Y11, AA11, AC11, AD11,
VSS                R6, R7, R8, R9, R10, R11, R12,        AA12, AB12, Y13, AA13, AB13,         PWR_ALG   Ground for PCIe.
                   R13, R14, R15, R16, T2, T4, T7,       AC14, AD14, Y15, AA15, AB15,
                            T10, T13, T16                AB16, Y17, AA17, AC17, AD17,
                                                         AB18, Y19, AA19, AB19, AA20,
                                                        AC20, AD20, AA21, AB21, AA22,
                                                        AA23, AA24, AC23, AD23, AC24

                                                        M5, P5, T5, N6, R6, M7, P7, T7,
                                                        V7, N8, R8, U8, W8, M9, P9, T9,
                                                         V9, N10, R10, U10, W10, M11,
                  F4, F6, F8, F10,F12, G5, G7, G9,
                                                         P11, T11, V11, N12, R12, U12,
                  G11, G13, H4, H6, H8, H10, H12,
                                                        W12, M13, P13, T13, V13, N14,
VSS                J5, J7, J9, J11, J13, K4, K6, K8,                                           PWR      Ground
                                                        R14, U14, W14, M15, P15, T15,
                   K10, K12, K14, L5, L7, L9, L11,
                                                        V15, N16, R16, U16, W16, M17,
                          M6, M8, M10, M12
                                                         P17, T17, V17, N18, R18, U18,
                                                        W18, M19, P19, T19, V19, J20,
                                                         N20, R20, U20, W20, Y23, Y24

                                                        G5, G7, G9, G15, G17, G19, H6,
                                                         H8, H10, H12, H14, H16, H18,
                                                       H20, J5, J7, J9, J11, J15, J17, J19,
NC                               N/A                                                                    No-connect pins.
                                                       K6, K8, K10, K12, K14, K16, K18,
                                                        K20, L7, L9, L11, L13, L15, L17,
                                                                        L19

                                                        N7, R7, U7, W7, M8, P8, T8, V8,
                                                        N9, R9, U9, W9, M10,M12, P10,
                  F5, F7, F9, F11, F13, G4, G6, G8,
                                                        T10, V10, N11, R11, U11, W11,
                  G10, G12, H5, H7, H9, H11, H13,
                                                         P12, T12, V12, J13, R13, U13,
VCC0P83            J4, J6, J8, J10, J12, K5, K7, K9,                                           PWR      0.83 V
                                                        W13, M14, P14, T14, V14, N15,
                   K11, K13, L6, L8, L10, L12, M5,
                                                        R15, U15, W15, M16, P16, T16,
                             M7, M9, M11
                                                        V16, N17, R17, U17, W17, M18,
                                                                 P18, T18, V18

VCC1P2A                    M1, M2, N1, N2                            V6, W5                   PWR_ALG   1.2 V

VCC1P2                        E4, E6, E8               D10, D4, D8, E11, E7, E9, D6, E5       PWR_ALG   1.2 V

                                                        E19, D20, D16, D18, E13, E15,
VCC1P2                      E10, E12, E14                                                     PWR_ALG   1.2 V
                                                                    E17

333369-009                                                                                                                    59
                                    Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                     Pin Interface

     Pin Name       Ball # (X550-AT2)               Ball # (X550-BT2)              Type      Name and Function

                                              A2, A12, C2, A4, C4, A6, C6, A8,
VCC2P1A0            C4, C6, C8, D5, D7                                            PWR_ALG   2.1 V
                                                       C8, A10, C10

                                               A13, A15, C15, A17, C17, A19,
VCC2P1A1        C10, C12, C14, D9, D11, D13                                       PWR_ALG   2.1 V
                                                 C19, A21, C21, A23, C23

VCC2P1A                    N/A                              C12                   PWR_ALG   2.1 V

VSS                        E11                              E21                   PWR_ALG   Ground

VSS                         E7                               E3                   PWR_ALG   Ground

DVDD0P83                    E9                              G13                   PWR_ALG   0.83 V

                                              L5, N5, R5, M6, P6, T6, N19, R19,
VCC3P3               L4, M4, L13, M13                                              PWR      3.3 V
                                               U19, W19, M20, P20, T20, V20

                                                AB3, AB5, Y6, Y8, AB8, Y10,
VCCA               N3, N5, N8, N11, N14       AB11, Y12, Y14, AB14, Y16, AB17,     PWR      1.0 V
                                                      Y18, AB20, AB22

VCC2P1                     D15                              C24                   PWR_ALG   2.1 V

VCC2P1                      P1                               U5                    PWR      2.1 V

60                                                                                                     333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface
