## 2.5 Ball Out — Top View Through Package

                                                                                       
                                                               

     $     VSS      MDI0_0_p   MDI0_1_p          VSS      MDI0_2_p   MDI0_3_p     VSS      MDI0_4_p   MDI1_4_p     VSS      MDI1_3_p   MDI1_2_p     VSS      MDI1_1_p     VSS        VSS      $

         NCSI_TX_
     %     EN
                    MDI0_0_n   MDI0_1_n          VSS      MDI0_2_n   MDI0_3_n     VSS      MDI0_4_n   MDI1_4_n     VSS      MDI1_3_n   MDI1_2_n     VSS      MDI1_1_n   BG_REXT    MDI1_0_p   %

         NCSI_ARB   THERM_D    THERM_D
     &     _IN        0_N        0_P
                                               VCC2P1A0     VSS      VCC2P1A0     VSS      VCC2P1A0     VSS      VCC2P1A1     VSS      VCC2P1A1     VSS      VCC2P1A1     VSS      MDI1_0_n   &

         NCSI_ARB   NCSI_CLK   NCSI_TXD        NCSI_TXD
     '     _OUT       _IN         0               1
                                                          VCC2P1A0     VSS      VCC2P1A0     VSS      VCC2P1A1     VSS      VCC2P1A1     VSS      VCC2P1A1     VSS      VCC2P1      XTAL_I    '

         NSCI_RXD   NCSI_RXD   NCSI_CRS
     (       0         1         _DV
                                               VCC1P2       VSS      VCC1P2       VSS      VCC1P2     DVDD0P83   VCC1P2       VSS      VCC1P2       VSS       VCC1P2      VSS      XTAL_O     (

         SMBALRT_
     )      N
                     SMBD       SMBCLK           VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      JTDI      JTDO       JTCK      )

                               MAIN_PW
     *    SDP0_1     SDP0_3
                                R_OK
                                               VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS        JTMS      SDP1_3     SDP1_1    *

     +    SDP0_0     SDP0_2    AUX_PWR           VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83    JTRST_N     SDP1_2     SDP1_0    +

                                                                                                                                                             RSVDJ14_
     -    LED0_1     LED0_3    FLSH_SO         VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS
                                                                                                                                                               VSS
                                                                                                                                                                         LED1_3     LED1_1    -

     .    LED0_0     LED0_2     FLSH_SI          VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS       LED1_2     LED1_0    .
                               ENCRYPTION_EN

                    FLSH_CE_   PE_WAKE                                                                                                                       RSVDL14_   RSVDL15_   RSVDL16_
     /   FLSH_SCK
                       N          _N
                                               VCC3P3       VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83    VCC3P3
                                                                                                                                                                NC         NC         NC
                                                                                                                                                                                              /

                                                                                                                                                             RSVDM14_ LAN0_DIS_ LAN1_DIS_

# 0 VCC1P2A    VCC1P2A    PE_RST_N        VCC3P3     VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC0P83      VSS      VCC3P3

                                                                                                                                                                NC        N         N
                                                                                                                                                                                              0

     1   VCC1P2A    VCC1P2A      VCCA          PE_CLK_p    VCCA        VSS        VSS       VCCA        VSS        VSS       VCCA        VSS        VSS       VCCA        VSS        VSS      1

                    RSVDP2_N

# 3 VCCP2P1

                       C
                                  VSS          PE_CLK_n     VSS      PER_0_p    PER_0_n      VSS      PER_1_p    PER_1_n      VSS      PER_2_p    PER_2_n      VSS      PER_3_p    PER_3_n    3

         RSVDR1_N RSVDR2_N PE_RSENS

    5 C        C         E

                                                 VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS        VSS      5

         RSVDT1_N
     7      C
                      VSS      PE_RBIAS          VSS      PET_0_p    PET_0_n      VSS      PET_1_p    PET_1_n      VSS      PET_2_p    PET_2_n      VSS      PET_3_p    PET_3_n      VSS      7

                                                                                       
                                                               

Figure 2-1.            X550 Package Layout (X550-AT2)

62                                                                                                                                                                                   333369-009
                                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

                                                                          
                                                                                     
                                          
      RSVDA1_   VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A   VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A   RSVDA24
  $     NC         0
                          MDI0_0_p
                                        0
                                               MDI0_1_p
                                                             0
                                                                    MDI0_2_p
                                                                                  0
                                                                                         MDI0_3_p
                                                                                                       0
                                                                                                              MDI0_4_p
                                                                                                                            0         1
                                                                                                                                             MDI1_4_p
                                                                                                                                                           1
                                                                                                                                                                  MDI1_3_p
                                                                                                                                                                                1
                                                                                                                                                                                       MDI1_2_p
                                                                                                                                                                                                     1
                                                                                                                                                                                                            MDI1_1_p
                                                                                                                                                                                                                          1
                                                                                                                                                                                                                                 MDI1_0_p
                                                                                                                                                                                                                                               1        _NC     $

  %    VSS        VSS     MDI0_0_n    VSS      MDI0_1_n     VSS     MDI0_2_n     VSS     MDI0_3_n     VSS     MDI0_4_n     VSS      VSS      MDI1_4_n    VSS      MDI1_3_n    VSS      MDI1_2_n    VSS      MDI1_1_n     VSS     MDI1_0_n     VSS       VSS     %
      RSVDC1_   VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A   RSVDC11              RSVDC13              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A              VCC2P1A
  &     NC         0
                            VSS
                                        0
                                                 VSS
                                                             0
                                                                      VSS
                                                                                  0
                                                                                           VSS
                                                                                                       0        _NC
                                                                                                                         VCC2P1A
                                                                                                                                     _NC
                                                                                                                                               VSS
                                                                                                                                                           1
                                                                                                                                                                    VSS
                                                                                                                                                                                1
                                                                                                                                                                                         VSS
                                                                                                                                                                                                     1
                                                                                                                                                                                                              VSS
                                                                                                                                                                                                                          1
                                                                                                                                                                                                                                   VSS
                                                                                                                                                                                                                                               1
                                                                                                                                                                                                                                                      VCC2P1    &
      RSVDD1_                                                                                                 RSVDD11              RSVDD13   RSVDD14
  '     NC
                  VSS       VSS      VCC1P2      VSS      VCC1P2      VSS      VCC1P2      VSS      VCC1P2
                                                                                                                _NC
                                                                                                                         BG_REXT
                                                                                                                                     _NC       _NC
                                                                                                                                                         VSS      VCC1P2      VSS      VCC1P2      VSS      VCC1P2       VSS       VSS       XTAL_I   XTAL_O    '
      RSVDE1_                                                                                                                                                                                                                               RSVDE23   RSVDE24
  (     NC
                  VSS       VSS       VSS      VCC1P2       VSS     VCC1P2       VSS     VCC1P2       VSS     VCC1P2       VSS     VCC1P2      VSS      VCC1P2      VSS      VCC1P2      VSS      VCC1P2      VSS        VSS       VSS
                                                                                                                                                                                                                                              _NC       _NC     (
      NCSI_AR   NCSI_AR   THERM_     THERM_    RSVDF5_                                                                                                                                                                                                RSVDF24
  )    B_IN      B_OUT     D0_N       D0_P       VSS
                                                            VSS       VSS        VSS       VSS        VSS       VSS        VSS      VSS        VSS       VSS        VSS       VSS        VSS       VSS        VSS        VSS       VSS        VSS
                                                                                                                                                                                                                                                        _NC     )
      NCSI_RX   NCSI_CL   NCSI_TX    NCSI_TX                                                                  RSVDG11              DVDD0P8                                                                             RSVDG21   RSVDG22    RSVDG23   RSVDG24
  *     D1       K_IN       D1         _EN
                                                 NC         VSS       NC         VSS       NC         VSS
                                                                                                                _NC
                                                                                                                           VSS
                                                                                                                                      3
                                                                                                                                               VSS        NC        VSS        NC        VSS        NC        VSS
                                                                                                                                                                                                                         _NC       _NC        _VSS      _VSS    *
      NCSI_CR   NCSI_TX   NSCI_RX                                                                                                                                                                                      RSVDH21   RSVDH22    BYPASS_   RSVDH24
  +    S_DV       D0        D0
                                     LED0_0      VSS        NC        VSS        NC        VSS        NC        VSS        NC       VSS        NC        VSS        NC        VSS        NC        VSS        NC
                                                                                                                                                                                                                        _VSS      _VSS        POR      _VSS     +
      FLSH_SC   FLSH_CE                                                                                                                                                                                                                     RSVDJ23   RSVDJ24
  -      K         _N
                          LED0_1     LED0_2      NC         VSS       NC         VSS       NC         VSS       NC         VSS     VCC0P83     VSS        NC        VSS        NC        VSS        NC        VSS      LED1_0    LED1_1
                                                                                                                                                                                                                                             _VSS      _VSS     -
                          RSVDK3_                                                                                                                                                                                                           LAN0_DI   LAN1_DI
  .   FLSH_SO   FLSH_SI
                            NC
                                     LED0_3      VSS        NC        VSS        NC        VSS        NC        VSS        NC       VSS        NC        VSS        NC        VSS        NC        VSS        NC       LED1_2    LED1_3
                                                                                                                                                                                                                                              S_N       S_N     .
                          RSVDL3_    RSVDL4_                                                                                                                                                                           RSVDL21   RSVDL22    RSVDL23   LAN_PW
  /    SMBD     SMBCLK
                            NC         NC
                                               VCC3P3       VSS       NC         VSS       NC         VSS       NC         VSS       NC        VSS        NC        VSS        NC        VSS        NC        VSS
                                                                                                                                                                                                                         _NC       _NC        _NC     R_GOOD    /
      ENCRYP    SMBALR    RSVDM3     RSVDM4                                                                                                                                                                            RSVDM2    RSVDM2     RSVDM2    RSVDM2

# 0 TION_EN     T_N       _NC        _NC

                                                 VSS      VCC3P3      VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83    VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3
                                                                                                                                                                                                                        1_NC      2_NC       3_NC      4_NC     0
      RSVDN1_   RSVDN2_   RSVDN3_    RSVDN4_                                                                                       RSVDN13                                                                             RSVDN21   RSVDN22    RSVDN23   RSVDN24

    1 NC        NC        NC         NC

                                               VCC3P3       VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83      VSS
                                                                                                                                     _NC
                                                                                                                                               VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3      VSS
                                                                                                                                                                                                                         _NC       _NC        _NC       _NC     1
      RSVDP1_   AUX_PW               RSVDP4_                                                                                                                                                                           RSVDP21   RSVDP22    RSVDP23   RSVDP24

    3 NC         R

                          SDP0_1
                                       NC
                                                 VSS      VCC3P3      VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83    VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3
                                                                                                                                                                                                                         _NC       _NC       _VSS      _VSS     3
      RSVDR1_   MAIN_PW                                                                                                                                                                                                RSVDR21   RSVDR22    RSVDR23   RSVDR24

    5 NC       R_OK

                          SDP0_3     SDP0_0    VCC3P3       VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3      VSS
                                                                                                                                                                                                                         _NC       _NC        _NC       _NC     5
      RSVDT1_   RSVDT2_   RSVDT3_                                                                                                                                                                                                           RSVDT23   RSVDT24

    7 NC        NC        NC

                                     SDP0_2      VSS      VCC3P3      VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83    VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3     SDP1_0    SDP1_1
                                                                                                                                                                                                                                             _VSS      _VSS     7
      RSVDU1_   RSVDU2_   RSVDU3_    RSVDU4_                                                                                                                                                                                                RSVDU23   RSVDV24

    8 NC        NC        NC         NC

                                               VCC2P1       VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3      VSS      SDP1_2    SDP1_3
                                                                                                                                                                                                                                              _NC       _NC     8
      RSVDV1_   RSVDV2_   RSVDV3_    RSVDV4_                                                                                                                                                                           RSVDV21              RSVDU23   RSVDV24

    9 NC        NC        NC         NC

                                                 VSS      VCC1P2A     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83    VSS      VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3
                                                                                                                                                                                                                         _NC
                                                                                                                                                                                                                                  JTDO
                                                                                                                                                                                                                                              _NC       _NC     9
      PE_WAK    PE_RST_                                                                                                                                                                                                                               RSVDW2
  :     E_N        N
                            VSS       VSS      VCC1P2A      VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83      VSS     VCC0P83     VSS      VCC0P83     VSS      VCC0P83     VSS      VCC3P3      VSS       JTMS       JTDI     JTRST_N
                                                                                                                                                                                                                                                       4_NC     :
      PE_CLK_   PE_CLK_              PE_RBIA   PE_RSEN                                                                                                                                                      RSVDY20    RSVDY21
  <      n         p
                            VSS
                                        S         SE
                                                           VCCA       VSS       VCCA       VSS       VCCA       VSS       VCCA      VSS       VCCA       VSS       VCCA       VSS       VCCA       VSS
                                                                                                                                                                                                              _NC        _NC
                                                                                                                                                                                                                                  JTCK        VSS       VSS     <
                                                          RSVDAA6              RSVDAA8              RSVDAA1                                  RSVDAA1              RSVDAA1              RSVDAA1
 $$    VSS        VSS       VSS       VSS        VSS
                                                            _NC
                                                                      VSS
                                                                                 _NC
                                                                                           VSS
                                                                                                     0_NC
                                                                                                                VSS        VSS      VSS
                                                                                                                                               4_NC
                                                                                                                                                         VSS
                                                                                                                                                                   6_NC
                                                                                                                                                                              VSS
                                                                                                                                                                                        8_NC
                                                                                                                                                                                                   VSS        VSS        VSS       VSS        VSS       VSS     $$

 $%   PER_0_n   PER_0_p    VCCA       VSS       VCCA        VSS       VSS       VCCA       VSS        VSS      VCCA        VSS      VSS       VCCA       VSS        VSS       VCCA       VSS       VSS       VCCA        VSS      VCCA      PER_7_p   PER_7_n   $%

 $&    VSS        VSS     PET_0_p    PET_1_p     VSS      PER_1_n   PER_2_n      VSS     PET_2_p    PET_3_p     VSS      PER_3_n   PER_4_n     VSS      PET_4_p   PET_5_p     VSS      PER_5_n    PER_6_n     VSS      PET_6_p   PET_7_p      VSS       VSS     $&
      RSVDAD                                                                                                                                                                                                                                          RSVDAD
 $'    1_VSS
                  VSS     PET_0_n    PET_1_n     VSS      PER_1_p   PER_2_p      VSS     PET_2_n    PET_3_n     VSS      PER_3_p   PER_4_p     VSS      PET_4_n   PET_5_n     VSS      PER_5_p    PER_6_p     VSS      PET_6_n   PET_7_n      VSS
                                                                                                                                                                                                                                                       24_NC    $'

Figure 2-2.                  X550 Package Layout (X550-BT2)

333369-009                                                                                                                                                                                                                                                          63
                                                                         Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                          Pin Interface

NOTE:   This page intentionally left blank.

64                                                                                          333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Chapter 3                     Interconnects
