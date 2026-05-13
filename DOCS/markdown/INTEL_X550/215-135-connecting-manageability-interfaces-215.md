## 13.5 Connecting Manageability Interfaces

SMBus and NC-SI are optional interfaces for pass-through and/or configuration traffic between the MC
and the X550. For a description of the operation mode of these interfaces, refer to Section 7 and
Section 12.

### 13.5.1 Connecting the SMBus Interface

To connect the SMBus interface to the chipset or the MC; connect the SMBD, SMBCLK and SMBALRT_N
signals to the corresponding pins of the chipset/MC. These pins require pull-up resistors to the 3.3V
supply rail.
Note:        If the interface is not used, the previously mentioned pull-up resistors on the SMBD, SMBCLK
             and SMBALRT_N signals still have to be in place.
It is recommended that the SMBus be connected to the chipset or MC for the Flash recovery solution. If
the connection is to a MC, it is able to send the Flash release command.

### 13.5.2 Connecting the NC-SI Interface

The NC-SI interface is a connection to an external MC. It operates as a single interface with an external
MC, where all traffic (other than header redirection) between the X550 and the MC flows through the
interface.

#### 13.5.2.1 External MC

The external MC is required to meet the electrical specifications called out in the NC-SI specification.

#### 13.5.2.2 Single and Multi-Drop Applications

Figure 13-8 shows the connectivity requirements and provides information about a single-drop
application. This configuration only has a single package connected to the MC. The X550 does support a
multi-drop NC-SI configuration architecture, including hardware arbitration support from the MC. refer
to the NC-SI specification for requirements for multi-drop applications.

333369-009                                                                                            1151
                                 Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                              Design Considerations and Guidelines

                                                         SMBCLK

                                                         SMBD                    EthernetController
                                                                             ConfiguredforSMBus(passͲ
                                                       SMBALRT_N
                                                                                   throughtraffic,
                                                                              configurationandstatus)

                                  ExternalMC
                            SMBusorDMTFcompliant   NCSI_RXD[1:0]
                                                      NCSI_CRS_DV
                                                                                 EthernetController
                                                                              ConfiguredforNCͲSI(passͲ
                                                      NCSI_TXD[1:0]          throughtraffic,configuration
                                                       NCSI_TX_EN                     andstatus)
                                                       NCSI_CLK_IN

Figure 13-8. External MC Connections with NC-SI and SMBus

#### 13.5.2.3 Pull-Ups and Pull-Downs

Depending on whether or not the NC-SI interface is used, different pull-up and pull-down resistors are
required. Figure 13-8 shows the connectivity requirements necessary for interfacing a NC-SI compliant
MC.

          50MHz                                                                  3.3V

          50MHzReferenceClock
                  Buffer

                                                          10kɏ        10kɏ     10kɏ      10kɏ

                        REF_CLK
                                      33ɏ                                                                      NCͲSI_CLK_IN
                                                                                                       33ɏ
                        CRS_DV                                                                                 NCͲSI_CRS_DV
                         RXD_0                                                                                 NCͲSI_RXD_0        X550
       DMTFCompliant    RXD_0                                                                                 NCͲSI_RXD_1        NCͲSI
       MCDevice                                                                                                              Interface
                        TX_EN                                                                                  NCͲSI_TX_EN      Signals
                        TXD_0                                                                                  NCͲSI_TXD_0
                                      22ɏ
                        TXD_1
                                                                                                               NCͲSI_TXD_1
                                      22ɏ

                                              10kɏ                                    10kɏ      10kɏ

Figure 13-9. NC-SI Connections to an External MC

1152                                                                                                                              333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

### 13.5.3 Layout Requirements

#### 13.5.3.1 Board Impedance

The NC-SI manageability interface is a single ended signaling environment. It is recommended that a
target board and trace impedance of 50 plus 20% and minus 10%. This ensures optimal signal
integrity.

#### 13.5.3.2 Trace Length Restrictions

It is recommended that a trace length maximum value from a board placement and routing topology
perspective of eight inches for direct connect applications. This ensures signal integrity and quality is
preserved from a design perspective and that compliance is met for NC-SI electrical requirements.

                             8 inches

                                                 NC-SI_CLK_IN

                                                 NC-SI_TXD(1:0)
                                                                            External
                         X550
                                                  NC-SI_TX_EN               MC
                                                 NC-SI_RXD(1:0)

                                                 NC-SI_CRS_DV

Figure 13-10. NC-SI Maximum Trace Length Requirement for Direct Connect Applications

For multi-drop applications, a spacing recommendation of a maximum of four inches between the two
packages connected to the same MC. This is done to keep the overall length between the MC and the
X550 within specification. See Figure 13-11

                                  Network
                                  Controller

                                   Network
                                   Controller

Figure 13-11. Spacing Recommendation for Multi-Drop Applications

333369-009                                                                                             1153
                                  Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                           Design Considerations and Guidelines

#### 13.5.3.3 Special Delay Requirements

To ensure that the X550 is able to communicate with a specification-compliant MC, the following
guidelines must be followed:
 • Total skew from the clock source to all devices should be less than 1 ns (less than or equal to an
   approximate 5.5 inch trace length skew).
 • Each inch of trace has about 160 ps to 180 ps of delay, depending on the effective dielectric
   constant.
