## 8.2 Device Registers - PF

### 8.2.1 BAR0 Registers Summary

Table 8-4.      PF - General Control Registers Summary
                                                                                              Section
 Offset/Alias Offset     Abbreviation                                        Name
                                                                                              Number

0x00000000             CTRL                Device Control Register                            8.2.2.1.1

0x00000008             STATUS              Device Status Register                             8.2.2.1.2

0x00000018             CTRL_EXT            Extended Device Control Register                   8.2.2.1.3

0x00000020             ESDP                Extended SDP Control                               8.2.2.1.4

0x00000028             PHY_GPIO            PHY GPIO Register                                  8.2.2.1.5

0x00000030             MAC_GPIO            MAC GPIO Register                                  8.2.2.1.6

0x00000100             PHYINT_STATUS0      PHY Interrupt Status Register 0                    8.2.2.1.7

0x00000104             PHYINT_STATUS1      PHY Interrupt Status Register 1                    8.2.2.1.8

0x00000108             PHYINT_STATUS2      PHY Interrupt Status Register 2                    8.2.2.1.9

0x00000200             LEDCTL              LED Control                                        8.2.2.1.10

0x00005078             EXVET               Extended VLAN Ether Type - Receive                 8.2.2.1.11

0x00008224             EXVET_T             Extended VLAN Ether Type - Transmit                8.2.2.1.12

0x00010150             FACTPS              Function Active and Power State to Manageability   8.2.2.1.13

0x00010200             GRC                 General Receive Control                            8.2.2.1.14

0x00010208             DEV_FUNC_EN         Device and Functions Enable Control                8.2.2.1.15
                                                2C Command                                    8.2.2.1.16
0x00015F58             I2CCMD              SFP I

0x00015F5C             I2CPARAMS           SFP I2C Parameters                                 8.2.2.1.17

Table 8-5.      PF - NVM Registers Summary
                                                                                              Section
 Offset/Alias Offset   Abbreviation                                      Name
                                                                                              Number

0x00010010             EEC              EEPROM Mode Control Register                          8.2.2.2.1

0x0001001C             FLA              Flash Access Register                                 8.2.2.2.2

0x00010110             EEMNGCTL         Manageability EEPROM-Mode Control Register            8.2.2.2.3

0x00010114             EEMNGDATA        Manageability EEPROM-Mode Read/Write Data             8.2.2.2.4

0x00010118             FLMNGCTL         Manageability Flash Control Register                  8.2.2.2.5

0x0001011C             FLMNGDATA        Manageability Flash Read/Write Data                   8.2.2.2.6

0x00015F2C             JEDEC_ID_1       JEDEC ID 1                                            8.2.2.2.7

333369-009                                                                                            589
                                    Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Programming Interface

Table 8-6.      PF - Flow Control Registers Summary
                                                                                                             Section
      Offset/Alias Offset     Abbreviation                                    Name
                                                                                                             Number

0x00003200 + 0x4*n, n=0...3   FCTTVN[n]         Flow Control Transmit Timer Value n                          8.2.2.3.1

0x00003220 + 0x4*n, n=0...7   FCRTL[n]          Flow Control Receive Threshold Low                           8.2.2.3.2

0x00003260 + 0x4*n, n=0...7   FCRTH[n]          Flow Control Receive Threshold High                          8.2.2.3.3

0x000032A0                    FCRTV             Flow Control Refresh Threshold Value                         8.2.2.3.4

0x00003D00                    FCCFG             Flow Control Configuration                                   8.2.2.3.5

0x00004294                    MFLCN             MAC Flow Control Register                                    8.2.2.3.6

0x0000431C                    PFCTOP            Priority Flow Control Type Opcode                            8.2.2.3.7

0x0000CE00                    TFCS              Transmit Flow Control Status                                 8.2.2.3.8

Table 8-7.      PF - PCIe Registers Summary
                                                                                                             Section
      Offset/Alias Offset       Abbreviation                                   Name
                                                                                                             Number

0x00011028                    PCI_STATUS1          PCIe Function Status 1                                    8.2.2.4.1

0x00011040                    PCI_FWCTRL           PCIe Firmware Control                                     8.2.2.4.2

0x00011044                    PCI_CSRTO            PCIe CSR Access Timeout                                   8.2.2.4.3

0x00011050                    GCR_EXT              PCIe Control Extended Register                            8.2.2.4.4

0x00011054                    PCI_FLASHTO          PCI Flash Access Timeout                                  8.2.2.4.5

0x00011070                    FUNC_RID             Function Requester ID Information Register                8.2.2.4.6

0x00011098                    PCI_REVID            PCIe Revision ID                                          8.2.2.4.7

0x00011140                    PCI_PCIERR           PCIe Errors Reported                                      8.2.2.4.8

0x00011520                    PCI_ICAUSE           PCIe Interrupt Cause                                      8.2.2.4.9

0x00011528                    PCI_IENA             PCIe Interrupts Enable                                    8.2.2.4.10

0x00011530                    PCI_VMINDEX          PCIe VM Pending Index                                     8.2.2.4.11

0x00011538                    PCI_VMPEND           PCIe VM Pending Status                                    8.2.2.4.12

0x00011540                    PCI_DREVID           PCIe Default Revision ID                                  8.2.2.4.13

0x00011544                    PCI_BYTCTH           PCIe Byte Counter High                                    8.2.2.4.14

0x00011548                    PCI_BYTCTL           PCIe Byte Counter Low                                     8.2.2.4.15

0x00011734                    PCI_LCBDATA          PCIe LCB Data Port                                        8.2.2.4.16

0x00011788                    PCI_LCBADD           PCIe LCB Address Port                                     8.2.2.4.17

0x00011800                    PCI_GSCL_1           PCIe Statistic Control Register #1                        8.2.2.4.18

0x00011804                    PCI_GSCL_2           PCIe Statistic Control Registers #2                       8.2.2.4.19

0x00011810 + 0x4*n, n=0...3   PCI_GSCL_5_8[n]      PCIe Statistic Control Register #5...#8                   8.2.2.4.20

0x00011820 + 0x4*n, n=0...3   PCI_GSCN_0_3[n]      PCIe Statistic Counter Registers #0...#3                  8.2.2.4.21

590                                                                                                          333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-8.      PF - PCIe Configuration Space Setting Registers Summary
                                                                                                         Section
 Offset/Alias Offset    Abbreviation                                       Name
                                                                                                         Number

0x00011000             PCI_CNF           PCIe PF Configuration                                           8.2.2.5.1

0x00011008             PCI_PFDEVID       PCIe PF Device ID                                               8.2.2.5.2

0x00011010             PCI_VFDEVID       PCIe VF Device ID                                               8.2.2.5.3

0x00011038             PCI_CLASS         PCIe Storage Class                                              8.2.2.5.4

0x0001103C             PCI_VENDORID      PCIe Vendor ID                                                  8.2.2.5.5

0x00011048             PCI_LBARCTRL      PCI BAR Control                                                 8.2.2.5.6

0x00011058             PCI_SUBSYSID      PCIe Subsystem ID                                               8.2.2.5.7

0x00011060             PCI_PWRDATA       PCIe Power Data Register                                        8.2.2.5.8

0x00011078             PCI_SERH          PCIe Serial Number MAC Address High                             8.2.2.5.9

0x00011080             PCI_CAPCTRL       PCIe Capabilities Control                                       8.2.2.5.10

0x00011088             PCI_CAPSUP        PCIe Capabilities Support                                       8.2.2.5.11

0x00011090             PCI_LINKCAP       PCIe Link Capabilities                                          8.2.2.5.12

0x000110A0             PCI_PMSUP         PCIe PM Support                                                 8.2.2.5.13

0x000110A8             PCI_VFSUP         PCIe VF Capabilities Support                                    8.2.2.5.14

0x000110B8             PCI_GLBL_CNF      PCIe Global Config                                              8.2.2.5.15

0x000110E8             PCI_UPADD         PCIe Upper Address                                              8.2.2.5.16

0x000110F0             PCI_SERL          PCIe Serial Number MAC Address Low                              8.2.2.5.17

0x000110F8             PCI_CNF2          PCIe Global Config 2                                            8.2.2.5.18

Table 8-9.      PF - Interrupt Registers Summary
                                                                                                         Section
         Offset/Alias Offset            Abbreviation                               Name
                                                                                                         Number

0x00000800                              EICR              Extended Interrupt Cause Register              8.2.2.6.1

0x00000808                              EICS              Extended Interrupt Cause Set Register          8.2.2.6.2

0x00000810                              EIAC              Extended Interrupt Auto Clear Register         8.2.2.6.3

0x00000820 + 0x4*n, n=0...23
 and                                    EITR[n]           Extended Interrupt Throttle Registers          8.2.2.6.4
0x00012300 + 0x4*(n-24), n=24...128

0x00000880                              EIMS              Extended Interrupt Mask Set/Read Register      8.2.2.6.5

0x00000888                              EIMC              Extended Interrupt Mask Clear Register         8.2.2.6.6

0x00000890                              EIAM              Extended Interrupt Auto Mask Enable Register   8.2.2.6.7

0x00000894                              EITRSEL           MSIX to EITR Select                            8.2.2.6.8

0x00000898                              GPIE              General Purpose Interrupt Enable               8.2.2.6.9

0x00000900 + 0x4*n, n=0...63            IVAR[n]           Interrupt Vector Allocation Registers          8.2.2.6.10

0x00000A00                              IVAR_MISC         Miscellaneous Interrupt Vector Allocation      8.2.2.6.11

0x00000A90                              EICS1             Extended Interrupt Cause Set Registers 1       8.2.2.6.12

0x00000A94                              EICS2             Extended Interrupt Cause Set Registers 2       8.2.2.6.13

0x00000AA0                              EIMS1             Extended Interrupt Mask Set/Read Registers     8.2.2.6.14

333369-009                                                                                                       591
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                     Programming Interface

Table 8-9.      PF - Interrupt Registers Summary [continued]
                                                                                                                 Section
         Offset/Alias Offset             Abbreviation                               Name
                                                                                                                 Number

0x00000AA4                               EIMS2           Extended Interrupt Mask Set/Read Registers              8.2.2.6.15

0x00000AB0                               EIMC1           Extended Interrupt Mask Clear Registers 1               8.2.2.6.16

0x00000AB4                               EIMC2           Extended Interrupt Mask Clear Registers 2               8.2.2.6.17

0x00000AD0                               EIAM1           Extended Interrupt Auto Mask Enable Registers 1         8.2.2.6.18

0x00000AD4                               EIAM2           Extended Interrupt Auto Mask Enable Registers 2         8.2.2.6.19

0x00012000 + 0x4*n, n=0...128            RSCINT[n]       RSC Enable Interrupt                                    8.2.2.6.20

Table 8-10. PF - MSI-X Table Registers Summary
                                                                                                                 Section
      Offset/Alias Offset       Abbreviation                                      Name
                                                                                                                 Number

0x000110C0 + 0x4*n, n=0...7     PBACL[n]          MSI-X PBA Clear                                                8.2.2.7.1

0x000110C8 + 0x4*n, n=0...5     VFPBACL[n]        VF MSI-X PBA Clear                                             8.2.2.7.2

Table 8-11. PF - Receive Registers Summary
                                                                                                                 Section
       Offset/Alias Offset         Abbreviation                                   Name
                                                                                                                 Number

0x00005000                        RXCSUM             Receive Checksum Control                                    8.2.2.8.1

0x00005008                        RFCTL              Receive Filter Control Register                             8.2.2.8.2

0x0000507C                        VXLANCTRL          VXLAN Control                                               8.2.2.8.3

0x00005080                        FCTRL              Filter Control Register                                     8.2.2.8.4

0x00005084                        ETAG_ETYPE         E-tag EtherType Register                                    8.2.2.8.5

0x00005088                        VLNCTRL            VLAN Control Register                                       8.2.2.8.6

0x00005090                        MCSTCTRL           Multicast Control Register                                  8.2.2.8.7

0x00005128 + 0x4*n, n=0...7       ETQF[n]            EType Queue Filter                                          8.2.2.8.8

0x00005200 + 0x4*n, n=0...127     MTA[n]             Multicast Table Array                                       8.2.2.8.9

0x00005400 + 0x8*n, n=0...15      RAL_ALIAS[n]       Receive Address Low                                         8.2.2.8.10

0x00005404 + 0x8*n, n=0...15      RAH_ALIAS[n]       Receive Address High                                        8.2.2.8.11

0x00005818                        MRQC_ALIAS         Multiple Receive Queues Command Register                    8.2.2.8.12

0x0000A000 + 0x4*n, n=0...127     VFTA[n]            VLAN Filter Table Array                                     8.2.2.8.13

0x0000A200 + 0x8*n, n=0...127     RAL[n]             Receive Address Low                                         8.2.2.8.14

0x0000A204 + 0x8*n, n=0...127     RAH[n]             Receive Address High                                        8.2.2.8.15

0x0000A600 + 0x4*n, n=0...255     MPSAR[n]           MAC Pool Select Array                                       8.2.2.8.16

0x0000EA00 + 0x4*n, n=0...63      PSRTYPE[n]         Packet Split Receive Type Register                          8.2.2.8.17

0x0000EB00 + 0x4*n, n=0...31      RETA[n]            Redirection Table                                           8.2.2.8.18

0x0000EB80 + 0x4*n, n=0...9       RSSRK[n]           RSS Random Key Register                                     8.2.2.8.19

0x0000EC00 + 0x4*n, n=0...7       ETQS[n]            EType Queue Select                                          8.2.2.8.20

0x0000EC30                        SYNQF              SYN Packet Queue Filter                                     8.2.2.8.21

0x0000EC70                        RQTC               RSS Queues per Traffic Class Register                       8.2.2.8.22

592                                                                                                              333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-11. PF - Receive Registers Summary [continued]
                                                                                                    Section
      Offset/Alias Offset        Abbreviation                                   Name
                                                                                                    Number

0x0000EC80                      MRQC               Multiple Receive Queues Command Register         8.2.2.8.23

0x0000EE80 + 0x4*n, n=0...95    ERETA[n]           Extended Redirection Table                       8.2.2.8.24

0x00018000 + 0x4*n + 0x40*m,
                                VFRSSRK[n,m]       Per-Pool RSS Random Key Register                 8.2.2.8.25
n=0...15, m=0...63

0x00019000 + 0x4*n + 0x40*m,
                                VFRETA[n,m]        Per-Pool Redirection Table                       8.2.2.8.26
n=0...15, m=0...63

Table 8-12. PF - Receive DMA Registers Summary
                                                                                                    Section
         Offset/Alias Offset                Abbreviation                           Name
                                                                                                    Number

0x00001000 + 0x40*n, n=0...63
 and                                   RDBAL[n]              Receive Descriptor Base Address Low    8.2.2.9.1
0x0000D000 + 0x40*(n-64), n=64...127

0x00001004 + 0x40*n, n=0...63
 and                                   RDBAH[n]              Receive Descriptor Base Address High   8.2.2.9.2
0x0000D004 + 0x40*(n-64), n=64...127

0x00001008 + 0x40*n, n=0...63
 and                                   RDLEN[n]              Receive Descriptor Length              8.2.2.9.3
0x0000D008 + 0x40*(n-64), n=64...127

0x00001010 + 0x40*n, n=0...63
 and                                   RDH[n]                Receive Descriptor Head                8.2.2.9.4
0x0000D010 + 0x40*(n-64), n=64...127

0x00001014 + 0x40*n, n=0...63
 and                                   SRRCTL[n]             Split Receive Control Registers        8.2.2.9.5
0x0000D014 + 0x40*(n-64), n=64...127

0x00001018 + 0x40*n, n=0...63
 and                                   RDT[n]                Receive Descriptor Tail                8.2.2.9.6
0x0000D018 + 0x40*(n-64), n=64...127

0x00001028 + 0x40*n, n=0...63
 and                                   RXDCTL[n]             Receive Descriptor Control             8.2.2.9.7
0x0000D028 + 0x40*(n-64), n=64...127

0x0000102C + 0x40*n, n=0...63
 and                                   RSCCTL[n]             RSC Control                            8.2.2.9.8
0x0000D02C + 0x40*(n-64), n=64...127

0x00002100 + 0x4*n, n=0...15           SRRCTL_ALIAS[n]       Split Receive Control Registers        8.2.2.9.9

0x00002F00                             RDRXCTL               Receive DMA Control Register           8.2.2.9.10

0x00003000                             RXCTRL                Receive Control Register               8.2.2.9.11

0x00003C00 + 0x4*n, n=0...7            RXPBSIZE[n]           Receive Packet Buffer Size             8.2.2.9.12

333369-009                                                                                                  593
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

Table 8-13. PF - Transmit Registers Summary
                                                                                                               Section
       Offset/Alias Offset           Abbreviation                                Name
                                                                                                               Number

0x00004950 + 0x4*n, n=0...7        TXPBTHRESH[n]      Tx Packet Buffer Threshold                               8.2.2.10.1

0x00004A80                         DMATXCTL           DMA Tx Control                                           8.2.2.10.2

0x00004A88                         DTXTCPFLGL         DMA Tx TCP Flags Control Low                             8.2.2.10.3

0x00004A8C                         DTXTCPFLGH         DMA Tx TCP Flags Control High                            8.2.2.10.4

0x00006000 + 0x40*n, n=0...127     TDBAL[n]           Transmit Descriptor Base Address Low                     8.2.2.10.5

0x00006004 + 0x40*n, n=0...127     TDBAH[n]           Transmit Descriptor Base Address High                    8.2.2.10.6

0x00006008 + 0x40*n, n=0...127     TDLEN[n]           Transmit Descriptor Length                               8.2.2.10.7

0x00006010 + 0x40*n, n=0...127     TDH[n]             Transmit Descriptor Head                                 8.2.2.10.8

0x00006018 + 0x40*n, n=0...127     TDT[n]             Transmit Descriptor Tail                                 8.2.2.10.9

0x00006028 + 0x40*n, n=0...127     TXDCTL[n]          Transmit Descriptor Control                             8.2.2.10.10

0x00006038 + 0x40*n, n=0...127     TDWBAL[n]          Tx Descriptor Completion Write Back Address Low         8.2.2.10.11

0x0000603C + 0x40*n, n=0...127     TDWBAH[n]          Tx Descriptor Completion Write Back Address High        8.2.2.10.12

0x00008100                         DTXMXSZRQ          DMA Tx TCP Max Allow Size Requests                      8.2.2.10.13

0x00008120                         MTQC               Multiple Transmit Queues Command Register               8.2.2.10.14

0x0000CC00 + 0x4*n, n=0...7        TXPBSIZE[n]        Transmit Packet Buffer Size                             8.2.2.10.15

0x0000CD10                         MNGTXMAP           Manageability Transmit TC Mapping                       8.2.2.10.16

0x00017100                         TAG_ETYPE          Tags EtherTypes                                         8.2.2.10.17

Table 8-14. PF - DCB Registers Summary
                                                                                                               Section
      Offset/Alias Offset        Abbreviation                                 Name
                                                                                                               Number

0x00002140 + 0x4*n, n=0...7   RTRPT4C[n]         DCB Receive Packet Plane T4 Config                            8.2.2.11.1

0x00002430                    RTRPCS             DCB Receive Packet Plane Control and Status                   8.2.2.11.2

0x00003020                    RTRUP2TC           DCB Receive User Priority to Traffic Class                    8.2.2.11.3

0x00004904                    RTTDQSEL           DCB Transmit Descriptor Plane Queue Select                    8.2.2.11.4

0x00004908                    RTTDT1C            DCB Transmit Descriptor Plane T1 Config                       8.2.2.11.5

0x00004910 + 0x4*n, n=0...7   RTTDT2C[n]         DCB Transmit Descriptor Plane T2 Config                       8.2.2.11.6

0x00004980                    RTTQCNRM           DCB Transmit QCN Rate-Scheduler MMW                           8.2.2.11.7

0x00004984                    RTTQCNRC           DCB Transmit QCN Rate-Scheduler Config                        8.2.2.11.8

0x00004988                    RTTQCNRS           DCB Transmit QCN Rate-Scheduler Status                        8.2.2.11.9

0x0000498C                    RTTQCNRR           DCB Transmit QCN Rate Reset                                  8.2.2.11.10

0x00004A90                    RTTQCNTG           DCB Transmit QCN Tagging                                     8.2.2.11.11

0x000082E0 + 0x4*n, n=0...3   TXLLQ[n]           Strict Low Latency Tx Queues                                 8.2.2.11.12

0x0000C800                    RTTUP2TC           DCB Transmit User Priority to Traffic Class                  8.2.2.11.13

0x0000CD00                    RTTPCS             DCB Transmit Packet Plane Control and Status                 8.2.2.11.14

0x0000CD20 + 0x4*n, n=0...7   RTTPT2C[n]         DCB Transmit Packet Plane T2 Config                          8.2.2.11.15

594                                                                                                            333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-15. PF - TPH Registers Summary
                                                                                                             Section
          Offset/Alias Offset                    Abbreviation                                   Name
                                                                                                             Number

0x0000100C + 0x40*n, n=0...63
 and                                         TPH_RXCTRL[n]                Rx TPH Control Register           8.2.2.12.1
0x0000D00C + 0x40*(n-64), n=64...127

0x00002200 + 0x4*n, n=0...15                 TPH_RXCTRL_ALIAS[n]          Rx TPH Control Register           8.2.2.12.2

0x0000600C + 0x40*n, n=0...127               TPH_TXCTRL[n]                Tx TPH Control Registers          8.2.2.12.3

Table 8-16. PF - Timers Registers Summary
                                                                                                             Section
 Offset/Alias Offset   Abbreviation                                            Name
                                                                                                             Number

0x0000004C             TCPTIMER            TCP Timer                                                        8.2.2.13.1

Table 8-17. PF - FCoE Registers Summary
                                                                                                             Section
      Offset/Alias Offset           Abbreviation                                     Name
                                                                                                             Number

0x00002410                         FCPTRL               FC Indirect DMA Context: User Descriptor PTR Low    8.2.2.14.1

0x00002414                         FCPTRH               FC Indirect DMA Context: User Descriptor PTR High   8.2.2.14.2

0x00002418                         FCBUFF               FC Indirect DMA Context: Buffer Control             8.2.2.14.3

0x00002420                         FCDMARW              FC Indirect DMA Context: Receive DMA RW             8.2.2.14.4

0x00005100                         FCRXCTRL             FC Receive Control                                  8.2.2.14.5

0x00005108                         FCFLT                FC Indirect Filter Context: Control                 8.2.2.14.6

0x0000510C                         FCSMAC               FC Indirect Filter Context: Source MAC Address      8.2.2.14.7

0x00005110                         FCFLTRW              FC Indirect Filter Context: RW Control              8.2.2.14.8

0x00005114                         FCD_ID               FC Indirect Filter Context: D_ID Register           8.2.2.14.9

0x000051D8                         FCPARAM              FC Indirect Filter Context: Offset Parameter        8.2.2.14.10

0x0000ED00                         FCRECTL              FCoE Redirection Control                            8.2.2.14.11

0x0000ED10 + 0x4*n, n=0...31       FCRETA[n]            FCoE Redirection Table                              8.2.2.14.12

0x00020000 + 0x4*n +
                                   FCDDC[n,m]           FCoE Direct DMA Context                             8.2.2.14.13
0x10*m, n=0...3, m=0...2047

0x00028000 + 0x4*n +
                                   FCDFC[n,m]           FCoE Direct Filter Context                          8.2.2.14.14
0x10*m, n=0...3, m=0...2047

0x00030000 + 0x4*n,
                                   FCDFCD[n]            FCoE Direct Filter Context D_ID                     8.2.2.14.15
n=0...2047

Table 8-18. PF - Flow Director Registers Summary
                                                                                                             Section
     Offset/Alias Offset          Abbreviation                                       Name
                                                                                                             Number

0x0000EE00                        FDIRCTRL             Flow Director Filters Control Register               8.2.2.15.1

0x0000EE0C + 0x4*n, n=0...2       FDIRSIPV6[n]         Flow Director Filters Source IPv6                    8.2.2.15.2

0x0000EE18                        FDIRIPSA             Flow Director Filters IP SA                          8.2.2.15.3

0x0000EE1C                        FDIRIPDA             Flow Director Filters IP DA                          8.2.2.15.4

333369-009                                                                                                          595
                                     Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                      Programming Interface

Table 8-18. PF - Flow Director Registers Summary [continued]
                                                                                                                  Section
      Offset/Alias Offset       Abbreviation                                     Name
                                                                                                                  Number

0x0000EE20                      FDIRPORT          Flow Director Filters Port                                      8.2.2.15.5

0x0000EE24                      FDIRVLAN          Flow Director Filters VLAN and FLEX Bytes                       8.2.2.15.6

0x0000EE28                      FDIRHASH          Flow Director Filters Hash Signature                            8.2.2.15.7

0x0000EE2C                      FDIRCMD           Flow Director Filters Command Register                          8.2.2.15.8

0x0000EE38                      FDIRFREE          Flow Director Filters Free                                      8.2.2.15.9

0x0000EE3C                      FDIRDIP4M         Flow Director Filters DIPv4 Mask                               8.2.2.15.10

0x0000EE40                      FDIRSIP4M         Flow Director Filters Source IPv4 Mask                         8.2.2.15.11

0x0000EE44                      FDIRTCPM          Flow Director Filters TCP Mask                                 8.2.2.15.12

0x0000EE48                      FDIRUDPM          Flow Director Filters UDP Mask                                 8.2.2.15.13

0x0000EE4C                      FDIRLEN           Flow Director Filters Length                                   8.2.2.15.14

0x0000EE50                      FDIRUSTAT         Flow Director Filters Usage Statistics                         8.2.2.15.15

0x0000EE54                      FDIRFSTAT         Flow Director Filters Failed Usage Statistics                  8.2.2.15.16

0x0000EE58                      FDIRMATCH         Flow Director Filters Match Statistics                         8.2.2.15.17

0x0000EE5C                      FDIRMISS          Flow Director Filters Miss Match Statistics                    8.2.2.15.18

0x0000EE68                      FDIRHKEY          Flow Director Filters Lookup Table HASH Key                    8.2.2.15.19

0x0000EE6C                      FDIRSKEY          Flow Director Filters Signature HASH Key                       8.2.2.15.20

0x0000EE70                      FDIRM             Flow Director Filters Other Mask                               8.2.2.15.21

0x0000EE74                      FDIRIP6M          Flow Director Filters IPv6 Mask                                8.2.2.15.22

0x0000EE78                      FDIRSCTPM         Flow Director Filters SCTP Mask                                8.2.2.15.23

Table 8-19. PF - MAC Registers Summary
                                                                                                                  Section
 Offset/Alias Offset   Abbreviation                                       Name
                                                                                                                  Number

0x00004240             HLREG0           Highlander Control 0 Register                                             8.2.2.16.1

0x00004244             HLREG1           Highlander Status 1 Register                                              8.2.2.16.2

0x00004248             PAP              Pause and Pace Register                                                   8.2.2.16.3

0x0000425C             MSCA             MDI Single Command and Address                                            8.2.2.16.4

0x00004260             MSRWD            MDI Single Read and Write Data                                            8.2.2.16.5

0x00004268             MAXFRS           Max Frame Size                                                            8.2.2.16.6

0x000042A4             LINKS            Link Status Register                                                      8.2.2.16.7

0x000042D0             MMNGC            MAC Manageability Control Register                                        8.2.2.16.8

0x00004330             MACC             MAC Control Register                                                      8.2.2.16.9

596                                                                                                               333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-20. PF - Statistics Registers Summary
                                                                                                  Section
      Offset/Alias Offset         Abbreviation                              Name
                                                                                                  Number

0x00001030 + 0x40*n, n=0...15   QPRC[n]          Queue Packets Received Count                    8.2.2.17.1

0x00001034 + 0x40*n, n=0...15   QBRC_L[n]        Queue Bytes Received Count Low                  8.2.2.17.2

0x00001038 + 0x40*n, n=0...15   QBRC_H[n]        Queue Bytes Received Count High                 8.2.2.17.3

0x00001430 + 0x40*n, n=0...15   QPRDC[n]         Queue Packets Received Drop Count               8.2.2.17.4

0x00002300 + 0x4*n, n=0...31    RQSMR[n]         Receive Queue Statistic Mapping Registers       8.2.2.17.5

0x0000241C                      FCOERPDC         FCoE Rx Packets Dropped Count                   8.2.2.17.6

0x00002424                      FCLAST           Fiber Channel Last Error Count                  8.2.2.17.7

0x00002428                      FCOEPRC          FCoE Packets Received Count                     8.2.2.17.8

0x0000242C                      FCOEDWRC         FCOE DWord Received Count                       8.2.2.17.9

0x00002F40                      RXDSTATCTRL      Rx DMA Statistic Counter Control                8.2.2.17.10

0x00002F50                      RXDGPC           DMA Good Rx Packet Counter                      8.2.2.17.11

0x00002F54                      RXDGBCL          DMA Good Rx Byte Counter Low                    8.2.2.17.12

0x00002F58                      RXDGBCH          DMA Good Rx Byte Counter High                   8.2.2.17.13

0x00002F5C                      RXDDPC           DMA Duplicated Good Rx Packet Counter           8.2.2.17.14

0x00002F60                      RXDDBCL          DMA Duplicated Good Rx Byte Counter Low         8.2.2.17.15

0x00002F64                      RXDDBCH          DMA Duplicated Good Rx Byte Counter High        8.2.2.17.16

0x00002F68                      RXLPBKPC         DMA Good Rx LPBK Packet Counter                 8.2.2.17.17

0x00002F6C                      RXLPBKBCL        DMA Good Rx LPBK Byte Counter Low               8.2.2.17.18

0x00002F70                      RXLPBKBCH        DMA Good Rx LPBK Byte Counter High              8.2.2.17.19

0x00002F74                      RXDLPBKPC        DMA Duplicated Good Rx LPBK Packet Counter      8.2.2.17.20

0x00002F78                      RXDLPBKBCL       DMA Duplicated Good Rx LPBK Byte Counter Low    8.2.2.17.21

0x00002F7C                      RXDLPBKBCH       DMA Duplicated Good Rx LPBK Byte Counter High   8.2.2.17.22

0x00002F90                      B2OGPRC          BMC2OS Packets Received by Host                 8.2.2.17.23

0x00004000                      CRCERRS          CRC Error Count                                 8.2.2.17.24

0x00004004                      ILLERRC          Illegal Byte Error Count                        8.2.2.17.25

0x00004008                      ERRBC            Error Byte Packet Count                         8.2.2.17.26

0x00004010                      MSPDC            MAC Short Packet Discard Count                  8.2.2.17.27

0x00004018                      MBSDC            Bad SFD Count                                   8.2.2.17.28

0x00004034                      MLFC             MAC Local Fault Count                           8.2.2.17.29

0x00004038                      MRFC             MAC Remote Fault Count                          8.2.2.17.30

0x00004040                      RLEC             Receive Length Error Count                      8.2.2.17.31

0x0000405C                      PRC64            Packets Received [64 Bytes] Count               8.2.2.17.32

0x00004060                      PRC127           Packets Received [65-127 Bytes] Count           8.2.2.17.33

0x00004064                      PRC255           Packets Received [128-255 Bytes] Count          8.2.2.17.34

0x00004068                      PRC511           Packets Received [256-511 Bytes] Count          8.2.2.17.35

0x0000406C                      PRC1023          Packets Received [512-1023 Bytes] Count         8.2.2.17.36

0x00004070                      PRC1522          Packets Received [1024 to Max Bytes] Count      8.2.2.17.37

333369-009                                                                                                597
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                             Programming Interface

Table 8-20. PF - Statistics Registers Summary [continued]
                                                                                                         Section
      Offset/Alias Offset      Abbreviation                              Name
                                                                                                         Number

0x00004074                    GPRC             Good Packets Received Count                              8.2.2.17.38

0x00004078                    BPRC             Broadcast Packets Received Count                         8.2.2.17.39

0x0000407C                    MPRC             Multicast Packets Received Count                         8.2.2.17.40

0x00004080                    GPTC             Good Packets Transmitted Count                           8.2.2.17.41

0x00004088                    GORCL            Good Octets Received Count Low                           8.2.2.17.42

0x0000408C                    GORCH            Good Octets Received Count High                          8.2.2.17.43

0x00004090                    GOTCL            Good Octets Transmitted Count Low                        8.2.2.17.44

0x00004094                    GOTCH            Good Octets Transmitted Count High                       8.2.2.17.45

0x000040A4                    RUC              Receive Undersize Count                                  8.2.2.17.46

0x000040A8                    RFC              Receive Fragment Count                                   8.2.2.17.47

0x000040AC                    ROC              Receive Oversize Count                                   8.2.2.17.48

0x000040B0                    RJC              Receive Jabber Count                                     8.2.2.17.49

0x000040B4                    MNGPRC           Management Packets Received Count                        8.2.2.17.50

0x000040B8                    MNGPDC           Management Packets Dropped Count                         8.2.2.17.51

0x000040C0                    TORL             Total Octets Received Low                                8.2.2.17.52

0x000040C4                    TORH             Total Octets Received High                               8.2.2.17.53

0x000040D0                    TPR              Total Packets Received                                   8.2.2.17.54

0x000040D4                    TPT              Total Packets Transmitted                                8.2.2.17.55

0x000040D8                    PTC64            Packets Transmitted [64 Bytes] Count                     8.2.2.17.56

0x000040DC                    PTC127           Packets Transmitted [65-127 Bytes] Count                 8.2.2.17.57

0x000040E0                    PTC255           Packets Transmitted [128-255 Bytes] Count                8.2.2.17.58

0x000040E4                    PTC511           Packets Transmitted [256-511 Bytes] Count                8.2.2.17.59

0x000040E8                    PTC1023          Packets Transmitted [512-1023 Bytes] Count               8.2.2.17.60

0x000040EC                    PTC1522          Packets Transmitted [Greater than 1024 Bytes] Count      8.2.2.17.61

0x000040F0                    MPTC             Multicast Packets Transmitted Count                      8.2.2.17.62

0x000040F4                    BPTC             Broadcast Packets Transmitted Count                      8.2.2.17.63

0x00004120                    XEC              XSUM Error Count                                         8.2.2.17.64

0x00004140 + 0x4*n, n=0...7   PXONRXCNT[n]     Priority XON Received Count                              8.2.2.17.65

0x00004160 + 0x4*n, n=0...7   PXOFFRXCNT[n]    Priority XOFF Received Count                             8.2.2.17.66

0x00004180                    BUPRC            Total Unicast Packets Received (BMC copy)                8.2.2.17.67

0x00004184                    BMPRC            BMC Total Multicast Packets Received                     8.2.2.17.68

0x00004188                    BBPRC            Total Broadcast Packets Received (BMC copy)              8.2.2.17.69

0x0000418C                    BUPTC            Total Unicast Packets Transmitted (BMC copy)             8.2.2.17.70

0x00004190                    BMPTC            BMC Total Multicast Packets Transmitted                  8.2.2.17.71

0x00004194                    BBPTC            Total Broadcast Packets Transmitted (BMC copy)           8.2.2.17.72

0x00004198                    BCRCERRS         BMC FCS Receive Errors                                   8.2.2.17.73

0x0000419C                    BXONRXC          BMC Pause XON Frames Received                            8.2.2.17.74

598                                                                                                      333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-20. PF - Statistics Registers Summary [continued]
                                                                                                   Section
      Offset/Alias Offset          Abbreviation                             Name
                                                                                                   Number

0x000041A4                       LXONRXCNT          Link XON Received Count                       8.2.2.17.75

0x000041A8                       LXOFFRXCNT         Link XOFF Received Count                      8.2.2.17.76

0x000041B0                       RXNFGPC            Good Rx Non-Filtered Packet Counter           8.2.2.17.77

0x000041B4                       RXNFGBCL           Good Rx Non-Filter Byte Counter Low           8.2.2.17.78

0x000041B8                       RXNFGBCH           Good Rx Non-Filter Byte Counter High          8.2.2.17.79

0x000041C0                       B2OSPC             BMC2OS Packets Sent by BMC                    8.2.2.17.80

0x000041C4                       O2BGPTC            OS2BMC Packets Received by BMC                8.2.2.17.81

0x000041E0                       BXOFFRXC           BMC Pause XOFF Frames Received                8.2.2.17.82

0x000041E4                       BXONTXC            BMC Pause XON Frames Transmitted              8.2.2.17.83

0x000041E8                       BXOFFTXC           BMC Pause XOFF Frames Transmitted             8.2.2.17.84

0x000041F0                       B2OSDPC            Sideband Receive Dropped Packet Count         8.2.2.17.85

0x00005118                       FCCRC              Fiber Channel CRC Error Count                 8.2.2.17.86

0x00006030 + 0x40*n, n=0...15    QPTC_ALIAS[n]      Queue Packets Transmitted Count               8.2.2.17.87

0x00008600 + 0x4*n, n=0...31     TQSM[n]            Transmit Queue Statistic Mapping Registers    8.2.2.17.88

0x00008680 + 0x4*n, n=0...15     QPTC[n]            Queue Packets Transmitted Count               8.2.2.17.89

0x00008700 + 0x8*n, n=0...15     QBTC_L[n]          Queue Bytes Transmitted Count Low             8.2.2.17.90

0x00008704 + 0x8*n, n=0...15     QBTC_H[n]          Queue Bytes Transmitted Count High            8.2.2.17.91

0x00008780                       SSVPC              Switch Security Violation Packet Count        8.2.2.17.92

0x00008784                       FCOEPTC            FCoE Packets Transmitted Count                8.2.2.17.93

0x00008788                       FCOEDWTC           FCoE DWord Transmitted Count                  8.2.2.17.94

0x000087A0                       TXDGPC             DMA Good Tx Packet Counter                    8.2.2.17.95

0x000087A4                       TXDGBCL            DMA Good Tx Byte Counter Low                  8.2.2.17.96

0x000087A8                       TXDGBCH            DMA Good Tx Byte Counter High                 8.2.2.17.97

0x000087B0                       O2BSPC             OS2BMC Packets Transmitted by Host            8.2.2.17.98

Table 8-21. PF - Wake-Up and Proxy Control Registers Summary
                                                                                                    Section
      Offset/Alias Offset                Abbreviation                               Name
                                                                                                    Number

0x00005800                      WUC                           Wake-Up Control Register             8.2.2.18.1

0x00005808                      WUFC                          Wake-Up Filter Control Register      8.2.2.18.2

0x00005810                      WUS                           Wake-Up Status Register              8.2.2.18.3

0x00005838                      IPAV                          IP Address Valid                     8.2.2.18.4

0x00005840 + 0x8*n, n=0...3     IP4AT[n]                      IPv4 Address Table                   8.2.2.18.5

0x00005880 + 0x4*n, n=0...3     IP6AT[n]                      IPv6 Address Table                   8.2.2.18.6

0x00005900                      WUPL                          Wake-Up Packet Length                8.2.2.18.7

0x00005990 + 0x4*n, n=0...11    IP6AT_EXT[n]                  IPv6 Address Table Extended          8.2.2.18.8

0x00005A00 + 0x4*n, n=0...31    WUPM[n]                       Wake-Up Packet Memory (128 Bytes)    8.2.2.18.9

333369-009                                                                                                 599
                                  Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

Table 8-21. PF - Wake-Up and Proxy Control Registers Summary [continued]
                                                                                                            Section
      Offset/Alias Offset                Abbreviation                              Name
                                                                                                            Number

0x00005F60                      PROXYS                       Proxying Status Register                      8.2.2.18.10

0x00005F64                      PROXYFC                      Proxying Filter Control Register              8.2.2.18.11

0x00009000 + 0x10*n +
0x100*m, n=0...15, m=0...3
 and                            FHFT_FILTER_DW_EVEN[n,m]     Filter DW Even                                8.2.2.18.12
0x00009600 + 0x10*(n-16) +
0x100*m, n=16...31, m=0...3

0x00009004 + 0x10*n +
0x100*m, n=0...15, m=0...3
 and                            FHFT_FILTER_DW_ODD[n,m]      Filter DW Odd                                 8.2.2.18.13
0x00009604 + 0x10*(n-16) +
0x100*m, n=16...31, m=0...3

0x00009008 + 0x10*n +
0x100*m, n=0...15, m=0...3
 and                            FHFT_FILTER_MASK[n,m]        Filter Mask                                   8.2.2.18.14
0x00009608 + 0x10*(n-16) +
0x100*m, n=16...31, m=0...3

0x0000900C + 0x10*n +
0x100*m, n=0...15, m=0...3
 and                            FHFT_FILTER_LENGTH[n,m]      Filter Length                                 8.2.2.18.15
0x0000960C + 0x10*(n-16) +
0x100*m, n=16...31, m=0...3

Table 8-22. PF - Management Filters Registers Summary
                                                                                                            Section
      Offset/Alias Offset               Abbreviation                               Name
                                                                                                            Number

0x00005010 + 0x4*n, n=0...7      MAVTV[n]                  Management VLAN TAG Value                        8.2.2.19.1

0x00005030 + 0x4*n, n=0...7      MFUTP[n]                  Management Flex UDP/TCP Ports                    8.2.2.19.2

0x00005050 + 0x4*n, n=0...3      BMCIP[n]                  BMC IP Address Register                          8.2.2.19.3

0x00005060                       BMCIPVAL                  BMC IP Valid Register                            8.2.2.19.4

0x00005160 + 0x4*n, n=0...7      MDEF_EXT[n]               Manageability Decision Filters Ext               8.2.2.19.5

0x00005190 + 0x4*n, n=0...3      METF[n]                   Management Ethernet Type Filters                 8.2.2.19.6

0x00005820                       MANC                      Management Control Register                      8.2.2.19.7

0x00005864                       MNGONLY                   Manageability Only Traffic                       8.2.2.19.8

0x00005890 + 0x4*n, n=0...7      MDEF[n]                   Manageability Decision Filters                   8.2.2.19.9

0x000058B0 + 0x4*n + 0x10*m,
                                 MIPAF[n,m]                Manageability IP Address Filter                 8.2.2.19.10
n=0...3, m=0...3

0x00005910 + 0x8*n, n=0...3      MMAL[n]                   Manageability Ethernet MAC Address Low          8.2.2.19.11

0x00005914 + 0x8*n, n=0...3      MMAH[n]                   Manageability Ethernet MAC Address High         8.2.2.19.12

0x00009400 + 0x10*n, n=0...15    FTFT_FILTER_EVEN[n]       FTFT Filter DW Even words                       8.2.2.19.13

0x00009404 + 0x10*n, n=0...15    FTFT_FILTER_ODD[n]        FTFT Filter DW Odd words                        8.2.2.19.14

0x00009408 + 0x10*n, n=0...15    FTFT_FILTER0_MASK[n]      FTFT Filter Mask                                8.2.2.19.15

0x0000940C + 0x10*n, n=0...15    FTFT_FILTER0_LENGTH[n]    FTFT Filter Length                              8.2.2.19.16

600                                                                                                         333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-23. PF - Manageability (ARC subsystem) HOST Interface Summary
                                                                                                  Section
      Offset/Alias Offset              Abbreviation                                  Name
                                                                                                  Number

0x00010140                          SWSM                     Software Semaphore Register         8.2.2.20.1

0x00010148                          FWSM                     Firmware Semaphore Register         8.2.2.20.2

0x00010160                          SW_FW_SYNC               Software-Firmware Synchronization   8.2.2.20.3

0x00015800 + 0x4*n, n=0...447       ARCRAM[n]                Host ARC Data RAM                   8.2.2.20.4

0x00015F00                          HICR                     HOST Interface Control Register     8.2.2.20.5

0x00015F40                          FWRESETCNT               Firmware Resets Count               8.2.2.20.6

Table 8-24. PF - Time Sync (IEEE 1588) Registers Summary
                                                                                                  Section
 Offset/Alias Offset   Abbreviation                                           Name
                                                                                                  Number

0x0000003C             TSSDP               Time Sync SDP Configuration Register                  8.2.2.21.1

0x00005120             RXMTRL              Rx Message Type Register Low                          8.2.2.21.2

0x00005188             TSYNCRXCTL          Rx Time Sync Control Register                         8.2.2.21.3

0x000051A4             RXSTMPH             Rx Timestamp High                                     8.2.2.21.4

0x000051E8             RXSTMPL             Rx Timestamp Low                                      8.2.2.21.5

0x00008C00             TSYNCTXCTL          Tx Time Sync Control Register                         8.2.2.21.6

0x00008C04             TXSTMPL             Tx Timestamp Value Low                                8.2.2.21.7

0x00008C08             TXSTMPH             Tx Timestamp Value High                               8.2.2.21.8

0x00008C0C             SYSTIMEL            System Time Register Low                              8.2.2.21.9

0x00008C10             SYSTIMEH            System Time Register High                             8.2.2.21.10

0x00008C14             TIMEINCA            Increment Attributes Register                         8.2.2.21.11

0x00008C18             TIMADJ              Time Adjustment Offset Register                       8.2.2.21.12

0x00008C20             TSAUXC              TimeSync Auxiliary Control Register                   8.2.2.21.13

0x00008C24             TRGTTIMEL0          Target Time Register 0 Low                            8.2.2.21.14

0x00008C28             TRGTTIMEH0          Target Time Register 0 High                           8.2.2.21.15

0x00008C2C             TRGTTIMEL1          Target Time Register 1 Low                            8.2.2.21.16

0x00008C30             TRGTTIMEH1          Target Time Register 1 High                           8.2.2.21.17

0x00008C34             FREQOUT0            Frequency Out 0 Control Register                      8.2.2.21.18

0x00008C38             FREQOUT1            Frequency Out 1 Control Register                      8.2.2.21.19

0x00008C3C             AUXSTMPL0           Auxiliary Timestamp 0 Register Low                    8.2.2.21.20

0x00008C40             AUXSTMPH0           Auxiliary Timestamp 0 Register High                   8.2.2.21.21

0x00008C44             AUXSTMPL1           Auxiliary Timestamp 1 Register Low                    8.2.2.21.22

0x00008C48             AUXSTMPH1           Auxiliary Timestamp 1 Register High                   8.2.2.21.23

0x00008C58             SYSTIMR             System Time Register Residue                          8.2.2.21.24

0x00008C60             TSICR               Time Sync Interrupt Cause Register                    8.2.2.21.25

0x00008C68             TSIM                Time Sync Interrupt Mask Register                     8.2.2.21.26

333369-009                                                                                               601
                                     Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

Table 8-25. PF - Virtualization PF Registers Summary
                                                                                                            Section
      Offset/Alias Offset       Abbreviation                                 Name
                                                                                                            Number

0x00000700 + 0x4*n, n=0...1     PFVFLREC[n]    PF VFLR Events Clear                                         8.2.2.22.1

0x00000710 + 0x4*n, n=0...3     PFMBICR[n]     PF Mailbox Interrupt Causes Register                         8.2.2.22.2

0x00000720 + 0x4*n, n=0...1     PFMBIMR[n]     PF Mailbox Interrupt Mask Register                           8.2.2.22.3

0x00002F04                      PFQDE          PF Queue Drop Enable Register                                8.2.2.22.4

0x00002FA4                      LMVM_RX        Last Malicious VM - Rx                                       8.2.2.22.5

0x00002FA8                      LVMMC_RX       Last VM Misbehavior Cause - Rx                               8.2.2.22.6

0x00002FB0 + 0x4*n, n=0...3     WQBR_RX[n]     Wrong Queue Behavior Register - Rx                           8.2.2.22.7

0x00004B00 + 0x4*n, n=0...63    PFMAILBOX[n]   PF Mailbox                                                   8.2.2.22.8

0x000050B0                      PFFLPL         Filter Local Packets Low                                     8.2.2.22.9

0x000050B4                      PFFLPH         Filter Local Packets High                                   8.2.2.22.10

0x00005180 + 0x4*n, n=0...1     PFVMTXSW[n]    PF VM Tx Switch Loopback Enable                             8.2.2.22.11

0x000051B0                      PFVTCTL        PF Virtual Control Register                                 8.2.2.22.12

0x000051E0 + 0x4*n, n=0...1     PFVFRE[n]      PF VF Receive Enable                                        8.2.2.22.13

0x00008000 + 0x4*n, n=0...63    PFVMVIR[n]     PF VM VLAN Insert Register                                  8.2.2.22.14

0x00008108                      LVMMC_TX       Last VM Misbehavior Cause - Tx                              8.2.2.22.15

0x00008110 + 0x4*n, n=0...1     PFVFTE[n]      PF VF Transmit Enable                                       8.2.2.22.16

0x00008124                      LMVM_TX        Last Malicious VM - Tx                                      8.2.2.22.17

0x00008130 + 0x4*n, n=0...3     WQBR_TX[n]     Wrong Queue Behavior Register - Tx                          8.2.2.22.18

0x00008200 + 0x4*n, n=0...7     PFVFSPOOF[n]   PFVF Anti-Spoof Control                                     8.2.2.22.19

0x00008220                      PFDTXGSWC      PF DMA Tx General Switch Control                            8.2.2.22.20

0x00008790                      PFVMECM0       PF VM 0:31 Error Count Mask                                 8.2.2.22.21

0x00008794                      PFVMECM1       PF VM 32:63 Error Count Mask                                8.2.2.22.22

0x0000F000 + 0x4*n, n=0...63    PFVML2FLT[n]   PF VM L2Control Register                                    8.2.2.22.23

0x0000F100 + 0x4*n, n=0...63    PFVLVF[n]      PF VM VLAN Pool Filter                                      8.2.2.22.24

0x0000F200 + 0x4*n, n=0...127   PFVLVFB[n]     PF VM VLAN Pool Filter Bitmap                               8.2.2.22.25

0x0000F400 + 0x4*n, n=0...127   PFUTA[n]       PF Unicast Table Array                                      8.2.2.22.26

0x0000F600 + 0x4*n, n=0...3     PFMRCTL[n]     PF Mirror Rule Control                                      8.2.2.22.27

0x0000F610 + 0x4*n, n=0...7     PFMRVLAN[n]    PF Mirror Rule VLAN                                         8.2.2.22.28

0x0000F630 + 0x4*n, n=0...7     PFMRVM[n]      PF Mirror Rule Pool                                         8.2.2.22.29

0x00017000 + 0x4*n, n=0...63    PFVMTIR[n]     PF VM Tag Insert Register                                   8.2.2.22.30

602                                                                                                         333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Table 8-26. PF - Power Management Registers Summary
                                                                                                    Section
     Offset/Alias Offset       Abbreviation                                    Name
                                                                                                    Number

0x00002400                    DMACR               DMA Coalescing Control Register                  8.2.2.23.1

0x00002404                    DMCTLX              DMA Coalescing Time to Lx Request                8.2.2.23.2

0x00003300 + 0x4*n, n=0...7   DMCTH[n]            DMA Coalescing Threshold                         8.2.2.23.3

0x000041F4                    TLPIC               EEE Tx LPI Count                                 8.2.2.23.4

0x000041F8                    RLPIC               EEE Rx LPI Count                                 8.2.2.23.5

0x00004380                    EEE_SU              Energy Efficient Ethernet (EEE) Setup Register   8.2.2.23.6

0x00004398                    EEE_STAT            Energy Efficient Ethernet (EEE) STATUS           8.2.2.23.7

0x000043A0                     EEER               Energy Efficient Ethernet (EEE) Register         8.2.2.23.8

0x00011708                     LTRC               Latency Tolerance Reporting (LTR) Control        8.2.2.23.9

0x00015F20                     DMCMNGTH           DMA Coalescing Management Threshold              8.2.2.23.10

Table 8-27. PF - Security Registers Summary
                                                                                                    Section
 Offset/Alias Offset   Abbreviation                                         Name
                                                                                                    Number

0x00008800             SECTXCTRL        Security Tx Control                                        8.2.2.24.1

0x00008804             SECTXSTAT        Security Tx Status                                         8.2.2.24.2

0x00008808             SECTXBUFFAF      Security Tx Buffer Almost Full                             8.2.2.24.3

0x00008810             SECTXMINIFG      Security Tx Buffer Minimum IFG                             8.2.2.24.4

0x00008D00             SECRXCTRL        Security Rx Control                                        8.2.2.24.5

0x00008D04             SECRXSTAT        Security Rx Status                                         8.2.2.24.6

Table 8-28. PF - IPsec Registers Summary
                                                                                                    Section
     Offset/Alias Offset           Abbreviation                                Name
                                                                                                    Number

0x00008900                    IPSTXIDX             IPsec Tx Index                                  8.2.2.25.1

0x00008904                    IPSTXSALT            IPsec Tx Salt Register                          8.2.2.25.2

0x00008908 + 0x4*n, n=0...3   IPSTXKEY[n]          IPsec Tx Key Registers                          8.2.2.25.3

0x00008E00                    IPSRXIDX             IPsec Rx Index                                  8.2.2.25.4

0x00008E04 + 0x4*n, n=0...3   IPSRXIPADDR[n]       IPsec Rx IP Address Register                    8.2.2.25.5

0x00008E14                    IPSRXSPI             IPsec Rx SPI Register                           8.2.2.25.6

0x00008E18                     IPSRXIPIDX          IPsec Rx SPI Register IP Index                  8.2.2.25.7

0x00008E1C + 0x4*n, n=0...3    IPSRXKEY[n]         IPsec Rx Key Register                           8.2.2.25.8

0x00008E2C                     IPSRXSALT           IPsec Rx Salt Register                          8.2.2.25.9

0x00008E30                     IPSRXMOD            IPsec Rx Mode Register                          8.2.2.25.10

333369-009                                                                                                 603
                                     Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

Table 8-29. PF - VF Registers Mapping in the PF Space Summary
                                                                                                           Section
      Offset/Alias Offset        Abbreviation                               Name
                                                                                                           Number

0x00000300 + 0x4*n, n=0...63    VFCTRL[n]        VF Control Register                                       8.2.2.26.1

0x00000B00 + 0x4*n, n=0...63    VFEICR[n]        VF Extended Interrupt Cause                               8.2.2.26.2

0x00000C00 + 0x4*n, n=0...63    VFEICS[n]        VF Extended Interrupt Cause Set                           8.2.2.26.3

0x00000D00 + 0x4*n, n=0...63    VFEIMS[n]        VF Extended Interrupt Mask Set/Read                       8.2.2.26.4

0x00000E00 + 0x4*n, n=0...63    VFEIMC[n]        VF Extended Interrupt Mask Clear                          8.2.2.26.5

0x0000101C + 0x40*n, n=0...63   VFGPRC[n]        VF Good Packets Received Count                            8.2.2.26.6

0x00001020 + 0x40*n, n=0...63   VFGORC_LSB[n]    VF Good Octets Received Count Low                         8.2.2.26.7

0x00003400 + 0x4*n, n=0...63    VFMRQC[n]        VF Multiple Receive Queues Command Register               8.2.2.26.8

0x00004C00 + 0x4*n, n=0...63    VFMAILBOX[n]     VF Mailbox                                                8.2.2.26.9

0x00004D00 + 0x4*n, n=0...63    VFEIAM[n]        VF Extended Interrupt Auto Mask Enable                   8.2.2.26.10

0x00004E00 + 0x4*n, n=0...63    VFIVAR_MISC[n]   VF Interrupt Vector Allocation Registers Misc            8.2.2.26.11

0x00008300 + 0x4*n, n=0...63    VFGPTC[n]        VF Good Packets Transmitted Count                        8.2.2.26.12

0x00008400 + 0x8*n, n=0...63    VFGOTC_LSB[n]    VF Good Octets Transmitted Count LSB                     8.2.2.26.13

0x00008404 + 0x8*n, n=0...63    VFGOTC_MSB[n]    VF Good Octets Transmitted Count MSB                     8.2.2.26.14

0x0000D01C + 0x40*n, n=0...63   VFMPRC[n]        VF Multicast Packets Received Count                      8.2.2.26.15

0x0000D020 + 0x40*n, n=0...63   VFGORC_MSB[n]    VF Good Octets Received Count High                       8.2.2.26.16

0x00012500 + 0x4*n, n=0...63    VFIVAR[n]        VF Interrupt Vector Allocation Registers                 8.2.2.26.17

0x00013000 + 0x4*n + 0x40*m,
                                PFMBMEM[n,m]     PF Mailbox Memory                                        8.2.2.26.18
n=0...15, m=0...63

604                                                                                                        333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

### 8.2.2 Detailed Register Descriptions - PF BAR0

#### 8.2.2.1 PF - General Control Registers

8.2.2.1.1               Device Control Register - CTRL (0x00000000)

CTRL is also mapped to address 0x00004 to maintain compatibility with predecessors.

         Field           Bit(s)   Init.     Type                                    Description

RESERVED                  1:0     00b       RSV    Reserved.
PCIE_MASTER_DISABLE        2       0b       RW     PCIe Master Disable
                                                   When set, the device blocks new master requests, including manageability
                                                   requests, by using this function. Once no master requests are pending by
                                                   using this function, the PCIE_MASTER_ENABLE_STATUS bit is cleared.
                                                   Note: After any change to this bit, the host must read that the bit has
                                                            been modified as expected before reading
                                                            STATUS.PCIE_MASTER_ENABLE_STATUS bit (Section 8.2.2.1.2).
LRST                       3       0b       RW     Link Reset
                                                   This bit performs a reset of the MAC, PHY, and the entire 10GBase-T
                                                   Controller (software reset) resulting in a state nearly approximating the
                                                   state following a power-up reset or internal PCIe reset, except for the
                                                   system PCI configuration.
                                                   Normally 0b. Writing 1b initiates the reset.
                                                   This bit is self-clearing. Also referred to as MAC reset.
RESERVED                  25:4    0x0       RSV    Reserved.
RST                        26      0b       RW     Device Reset
                                                   This bit performs a complete reset of the device, resulting in a state nearly
                                                   approximating the state following a power-up reset or internal PCIe reset,
                                                   except for the system PCI configuration.
                                                   Normally 0b. Writing 1b initiates the reset.
                                                   This bit is self-clearing. Also referred to as a software reset or global reset.
RESERVED                 31:27    0x0       RSV    Reserved.

Note:        LRST and RST can be used to globally reset the entire 10GBase-T Controller. This register is
             provided primarily as a software mechanism to recover from an indeterminate or suspected
             hung hardware state. Most registers (receive, transmit, interrupt, statistics, etc.) and state
             machines are set to their power-on reset values, approximating the state following a
             power-on or PCI reset. However, PCIe configuration registers are not reset, thereby leaving
             the device mapped into system memory space and accessible by a software device driver. To
             ensure that a global device reset has fully completed and that the device responds to
             subsequent accesses, programmers must wait approximately 1 ms after setting before
             attempting to check if the bit has cleared, or to access (read or write) any other device
             register.

333369-009                                                                                                                     605
                                  Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

8.2.2.1.2                   Device Status Register - STATUS (0x00000008)

              Field               Bit(s)          Init.       Type                                 Description

RESERVED                               1:0         00b         RSV     Reserved.
LAN_ID                                 3:2         00b          RO     LAN ID
                                                                       Provides software a mechanism to determine the device LAN
                                                                       identifier for this MAC.
                                                                         00b = LAN 0
                                                                         01b = LAN 1
                                                                         All other values are reserved.
RESERVED                               6:4        000b         RSV     Reserved.
LINKUP                                 7            0b         RW      Linkup Status Indication
                                                                       This bit is useful for IOV mode. The PF software driver sets it
                                                                       according to the LINKS register and PHY state. It is reflected in the
                                                                       VFSTATUS register indicating link up to the VF drivers.
RESERVED                               9:8         00b         RSV     Reserved.
NUM_VFS                              17:10         0x0          RO     Num VFs
                                                                       This field reflects the value of the Num VFs in the IOV capability
                                                                       structure.
                                                                       Note: Bit 17 is always 0b.
IOV_ACTIVE                             18           0b          RO     IOV Active
                                                                       This bit reflects the value of the VF Enable (VFE) bit in the IOV
                                                                       Control/Status register.
PCIE_MASTER_ENABLE_STATUS              19           1b          RO     PCIe Master Enable Status
                                                                       This is a status bit of the appropriate CTRL.PCIE_MASTER_DISABLE
                                                                       bit (Section 8.2.2.1.1).
                                                                        0b = Associated LAN function does not issue any master request
                                                                               and all previously issued requests are complete.
                                                                        1b = Associated LAN function can issue master requests.
THERMAL_SENSOR_STATUS                  20           0b          RO     Thermal Sensor Status
                                                                       This indication is received from the internal PHY.
                                                                        0b = Thermal sensor normal state.
                                                                        1b = Thermal sensor current event.
RESERVED                             31:21         0x0         RSV     Reserved. Reads as 0b.

8.2.2.1.3                   Extended Device Control Register - CTRL_EXT (0x00000018)

      Field           Bit(s)   Init.         Type                                          Description

RESERVED              13:0     0x0           RSV         Reserved.
PFRSTD                 14       0b           SC          PF Reset Done
                                                         When set, the RSTI bit in all the VFMailbox registers are cleared and the RSTD bit
                                                         in all the VFMailbox registers are set.
RESERVED              16:15    00b           RSV         Reserved.
RO_DIS                 17       0b           RW          Relaxed Ordering Disable
                                                         When set to 1b, the device does not request any relaxed ordering transactions.
                                                         When this bit is cleared and the Enable Relaxed Ordering bit in the Device Control
                                                         register is set, the device requests relaxed ordering transactions per queues as
                                                         configured in the TPH_RXCTRL[n] and TPH_TXCTRL[n] registers
                                                         (Section 8.2.2.12.1 and Section 8.2.2.12.3, respectively).
RESERVED              25:18    0x0           RSV         Reserved.

606                                                                                                                             333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field       Bit(s)    Init.      Type                                       Description

EXTENDED_VLAN       26       0b         RW     Extended VLAN
                                               When set, all incoming Rx packets are expected to have at least one VLAN with
                                               the EtherType as defined in the EXVET register (Section 8.2.2.1.11). This bit
                                               should only be reset by a PCIe reset, and should only be changed while Tx and Rx
                                               processes are stopped.
                                               Should be set to the same value as DMATXCTL.GDV (Section 8.2.2.10.2)
RESERVED            27       0b        RSV     Reserved.
DRV_LOAD            28       0b         RW     Driver Load
                                               Software device driver loaded and the corresponding network interface is
                                               enabled.
                                               This bit should be set by the software device driver after it was loaded, and
                                               cleared when it unloads or at PCIe reset. The Manageability Controller (MC) loads
                                               this bit as an indication that the software device driver successfully loaded to it.
RESERVED          31:29     000b       RSV     Reserved.

8.2.2.1.4                 Extended SDP Control - ESDP (0x00000020)

This register is initialized only at LAN_PWR_GOOD, preserving the SDP states across software and PCIe
resets. Some specific I/O pins are initialized in other resets in native mode as expected for the specific
behavior, and described explicitly as follows:

      Field        Bit(s)    Init.      Type                                       Description
                                                                   1,2
SDP0_DATA             0       0b         RW     SDP0 Data Value
                                                Used to read (write) a value of the software-controlled I/O pin SDP0.
                                                If SDP0 is configured as an output (SDP0_IODIR = 1b), this bit controls the
                                                value driven on the pin. If SDP0 is configured as an input, all reads return the
                                                current value of the pin.
SDP1_DATA             1       0b         RW     SDP1 Data Value1,3
                                                Used to read (write) a value of the software-controlled I/O pin SDP1.
                                                If SDP1 is configured as an output (SDP1_IODIR = 1b), this bit controls the
                                                value driven on the pin. If SDP1 is configured as an input, all reads return the
                                                current value of the pin.
SDP2_DATA             2       0b         RW     SDP2 Data Value1
                                                Used to read (write) a value of software-controlled I/O pin SDP2.
                                                If SDP2 is configured as an output (SDP2_IODIR = 1b), this bit controls the
                                                value driven on the pin. If SDP2 is configured as an input, all reads return the
                                                current value of the pin.
SDP3_DATA             3       0b         RW     SDP3 Data Value1
                                                Used to read (write) a value of the software-controlled I/O pin SDP3.
                                                If SDP3 is configured as an output (SDP3_IODIR = 1b), this bit controls the
                                                value driven on the pin. If SDP3 is configured as an input, all reads return the
                                                current value of the pin.
RESERVED             7:4      0x0       RSV     Reserved.
SDP0_IODIR            8       0b         RW     SDP0 Pin Directionality1,2
                                                Controls whether software-controlled pin SDP0 is configured as an input or
                                                output.
                                                 0b = Input
                                                 1b = Output
SDP1_IODIR            9       0b         RW     SDP1 Pin Directionality1,3
                                                Controls whether software-controlled pin SDP1 is configured as an input or
                                                output.
                                                 0b = Input
                                                 1b = Output

333369-009                                                                                                                      607
                                     Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

        Field           Bit(s)         Init.        Type                                    Description

SDP2_IODIR                10            0b          RW     SDP2 Pin Directionality1
                                                           Controls whether software-controlled pin SDP2 is configured as an input or
                                                           output.
                                                            0b = Input
                                                            1b = Output
SDP3_IODIR                11            0b          RW     SDP3 Pin Directionality1
                                                           Controls whether software-controlled pin SDP3 is configured as an input or
                                                           output.
                                                            0b = Input
                                                            1b = Output
RESERVED                15:12          0x0          RSV    Reserved.
SDP0_NATIVE               16            0b          RW     SDP0 Operating Mode2
                                                            0b = Generic software controlled I/O by SPD0_DATA and SDP0_IODIR.
                                                            1b = Native mode operation (connected to hardware function) is IEEE 1588
                                                                 functionality.
SDP1_NATIVE               17            0b          RW     SDP1 Operating Mode1,3
                                                            0b = Generic software controlled I/O by SPD1_DATA and SDP1_IODIR.
                                                            1b = Native mode operation (connected to hardware function) is IEEE 1588
                                                                 functionality or thermal sensor mode according to the SDP1_Function bit.
SDP2_NATIVE               18            0b          RW     SDP2 Operating Mode.
                                                            0b = Generic software controlled I/O by SPD2_DATA and SDP2_IODIR.
                                                            1b = Native mode operation (connected to hardware function). 1588
                                                                 functionality or I2C functionality according to the SDP23_FUNCTION bit.
SDP3_NATIVE               19            0b          RW     SDP3 Operating Mode.
                                                            0b = Generic software controlled I/O by SPD3_DATA and SDP3_IODIR.
                                                            1b = Native mode operation (connected to hardware function). 1588
                                                                 functionality or I2C functionality according to the SDP23_FUNCTION bit.
RESERVED                24:20          0x0          RSV    Reserved.
SDP1_FUNCTION             25            0b          RW     SDP1 Function3
                                                           SDP1 native mode functionality (SDP1_NATIVE = 1b).
                                                            0b = 1588 functionality. SDP1_IODIR should be configured as an output.
                                                            1b = SDP1 Thermal sensor functionality. The SDP1 pin drives the active high
                                                                 thermal sensor level signal that indicates that junction temperature has
                                                                 risen above a preset limit. SDP1_IODIR should be configured as an
                                                                 output.
SDP23_FUNCTION            26            0b          RW     SDP23 Function
                                                           Defines the usage of SDP2 & SDP3 when SDP[23]_NATIVE is set to 1b.
                                                             0b = Use for 1588 functionality.
                                                             1b = Use for I2C functionality.
                                                           If this bit is set to 1b, SDP3_NATIVE should be equal to SDP2_NATIVE.
RESERVED                31:27          0x0          RSV    Reserved.

1. Initial values are read from the NVM when direction of SDP is Output (SDPx_IODIR = 1).
2. It is assumed that bit 15 of NC-SI Configuration 2 word in the NVM is cleared. Otherwise, the SDP0 pin of function 0 is used as
   input pins that encode the NC-SI Package ID of the controller.
3. It is assumed that bit SDP_FUNC_OFF_EN of NVM Control word 2 is cleared. Otherwise, SDP1 pins are strapped during PE_RST_N
   to determine that both PCIe functions are disabled.

8.2.2.1.5                  PHY GPIO Register - PHY_GPIO (0x00000028)

      Field      Bit(s)        Init.         Type                                        Description

PHY_GPIO          3:0          0x0             RO     PHY-to-MAC GPIO
                                                      Used to read the four internal PHY to MAC general purpose signals.
RESERVED         31:4          0x0           RSV      Reserved.

608                                                                                                                            333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.1.6               MAC GPIO Register - MAC_GPIO (0x00000030)

    Field      Bit(s)   Init.   Type                                      Description

MAC_GPIO        3:0     0x0      RW    MAC-to-PHY GPIO
                                       Used to set the four internal MAC-to-PHY general purpose signals.
RESERVED       31:4     0x0      RSV   Reserved.

8.2.2.1.7               PHY Interrupt Status Register 0 - PHYINT_STATUS0
                        (0x00000100)

Register contents is valid once the corresponding EEMNGCTL.CFG_DONE0/1 bit is asserted by firmware.
Bits are set by firmware to notify the host of the PHY interrupts that were triggered. This register is
reset by hardware only at power-up events. The host is responsible to clear the PHY interrupts once it
completes the PHY interrupt handling routine.

                Field                  Bit(s)      Init.   Type                          Description

PMA_RECEIVE_LINK_STATUS                     0       0b     RW     Reflects the inverse state of PHY register bit 1.1.2 before
                                                                  it was set by a firmware read.
PMA_TRANSMIT_FAULT                          1       0b     RW     Reflects the state of PHY register bit 1.8.B before it was
                                                                  cleared by a firmware read.
PMA_RECEIVE_FAULT                           2       0b     RW     Reflects the state of PHY register bit 1.8.A before it was
                                                                  cleared by a firmware read.
PMA_RESERVED                            7:3        0x0     RW     Reserved. Read as written.
PCS_RECEIVE_LINK_STATUS                     8       0b     RW     Reflects the inverse state of PHY register bit 3.1.2 before
                                                                  it was set by a firmware read.
PCS_TRANSMIT_FAULT                          9       0b     RW     Reflects the state of PHY register bit 3.8.B before it was
                                                                  cleared by a firmware read.
PCS_RECEIVE_FAULT                           10      0b     RW     Reflects the state of PHY register bit 3.8.A before it was
                                                                  cleared by a firmware read.
PCS_10GBASE_T_BLOCK_LOCK_LATCHED            11      0b     RW     Reflects the inverse state of PHY register bit 3.21.F
                                                                  before it was set by a firmware read.
PCS_10GBASE_T_HIGH_BER_LATCHED              12      0b     RW     Reflects the state of PHY register bit 3.21.E before it was
                                                                  cleared by a firmware read.
PCS_CRC_ERROR                               13      0b     RW     Reflects the state of PHY register bit 3.EC00.F before it
                                                                  was cleared by firmware read.
PCS_LDPC_DECODE_FAILURE                     14      0b     RW     Reflects the state of PHY register bit 3.EC00.E before it
                                                                  was cleared by a firmware read.
PCS_INVALID_65B_BLOCK                       15      0b     RW     Reflects the state of PHY register bit 3.EC00.8 before it
                                                                  was cleared by a firmware read.
PCS_CHANGE_IN_AUXILIARY_BIT                 16      0b     RW     Reflects the state of PHY register bit 3.EC00.0 before it
                                                                  was cleared by a firmware read.
PCS_RESERVED                           23:17       0x0     RW     Reserved. Read as written.
PHY_XS_RESERVED                        31:24       0x0     RW     Reserved. Read as written.

333369-009                                                                                                                609
                                 Did this document help answer your questions?

                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                          Programming Interface

8.2.2.1.8            PHY Interrupt Status Register 1 - PHYINT_STATUS1
                     (0x00000104)

Register contents is valid once the corresponding EEMNGCTL.CFG_DONE0/1 bit is asserted by firmware.
Bits are set by firmware to notify the host of the PHY interrupts that were triggered. This register is
reset by hardware only at power-up events. The host is responsible to clear the PHY interrupts once it
completes the PHY interrupt handling routine.

                        Field                            Bit(s)   Init.     Type             Description

AUTO_NEGOTIATION_EXTENDED_NEXT_PAGE_RECEIVED               0       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.1.6 before it was cleared by
                                                                                   a firmware read.
AUTO_NEGOTIATION_REMOTE_FAULT                              1       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.1.4 before it was cleared by
                                                                                   a firmware read.
AUTO_NEGOTIATION_LINK_STATUS                               2       0b        RW    Reflects the inverse state of PHY
                                                                                   register bit 7.1.2 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_MASTER_SLAVE_CONFIGURATION_FAULT          3       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.21.F before it was cleared
                                                                                   by a firmware read.
AUTO_NEGOTIATION_COMPLETED_FOR_NON_SUPPORTED_RATE          4       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.CC00.3 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_COMPLETED_FOR_SUPPORTED_RATE              5       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.CC00.2 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_AUTOMATIC_DOWNSHIFT                       6       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.CC00.1 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_CONNECTION_STATE_CHANGE                   7       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.CC00.0 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_100BASE_TX_DEVICE_DETECT                  8       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.F before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_ENERGY_ON_LINE_DETECT                     9       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.E before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_NEXT_PAGE_3RD_RECEIVED                   10       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.3 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_NEXT_PAGE_2ND_RECEIVED                   11       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.2 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_NEXT_PAGE_1ST_RECEIVED                   12       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.1 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_BASE_PAGE_RECEIVED                       13       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.0 before it was
                                                                                   cleared by a firmware read.
AUTO_NEGOTIATION_10BASE_T_DEVICE_DETECT                   14       0b        RW    Reflects the inverse state of PHY
                                                                                   register bit 7.EC02.2 before it
                                                                                   was cleared by a firmware read.
AUTO_NEGOTIATION_PROTOCOL_ERROR                           15       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.D before it was
                                                                                   cleared by a firmware read.
FLP_IDLE_ERROR                                            16       0b        RW    Reflects the state of PHY register
                                                                                   bit 7.EC01.C before it was
                                                                                   cleared by a firmware read.

610                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

                            Field                            Bit(s)    Init.     Type               Description

AUTO_NEGOTIATION_GBE_PHY_RESERVED                            27:17      0x0       RW      Reserved. Read as written.
PCIE_SERDES_LOSS_OF_SIGNAL_3_0                               31:28      0x0       RW      Reflects the state of PHY register
                                                                                          bit 4.CC02.F:C before it was
                                                                                          cleared by a firmware read.

8.2.2.1.9                 PHY Interrupt Status Register 2 - PHYINT_STATUS2
                          (0x00000108)

Register contents is valid once the corresponding EEMNGCTL.CFG_DONE0/1 bit is asserted by firmware.
Bits are set by firmware to notify the host of the PHY interrupts that were triggered. This register is
reset by hardware only at power-up events. The host is responsible to clear the PHY interrupts once it
completes the PHY interrupt handling routine.

                  Field                     Bit(s)   Init.   Type                         Description

GLOBAL_MAC_RESET                               0      0b      RW      Reflects the inverse state of PHY register bit
                                                                      1E.1200.0 before it was cleared by a firmware read.
GLOBAL_MAC_LOW_POWER_LINK_UP_MODE              1      0b      RW      Reflects the state of PHY register bit 1E.1204.4
                                                                      before it was cleared by a firmware read.
GLOBAL_MAC_PHY_DISABLE_MODE                    2      0b      RW      Reflects the inverse state of PHY register bit
                                                                      1E.1204.1 before it was cleared by a firmware read.
GLOBAL_MAC_LOW_POWER_MODE                      3      0b      RW      Reflects the inverse state of PHY register bit
                                                                      1E.1204.0 before it was cleared by a firmware read.
GLOBAL_MAC_SPI_GRANT                           4      0b      RW      Reflects the state of PHY register bit 1E.1206.2
                                                                      before it was cleared by a firmware read.
GLOBAL_MAC_SPI_CONTROL                         5      0b      RW      Reflects the inverse state of PHY register bit
                                                                      1E.1206.1 before it was cleared by a firmware read.
GLOBAL_HIGH_TEMPERATURE_FAILURE                6      0b      RW      Reflects the state of PHY register bit 1E.CC00.E
                                                                      before it was cleared by a firmware read.
GLOBAL_LOW_TEMPERATURE_FAILURE                 7      0b      RW      Reflects the state of PHY register bit 1E.CC00.D
                                                                      before it was cleared by a firmware read.
GLOBAL_HIGH_TEMPERATURE_WARNING                8      0b      RW      Reflects the state of PHY register bit 1E.CC00.C
                                                                      before it was cleared by a firmware read.
GLOBAL_LOW_TEMPERATURE_WARNING                 9      0b      RW      Reflects the state of PHY register bit 1E.CC00.B
                                                                      before it was cleared by a firmware read.
GLOBAL_RESET_COMPLETED                        10      0b      RW      Reflects the state of PHY register bit 1E.CC00.6
                                                                      before it was cleared by a firmware read.
GLOBAL_DEVICE_FAULT                           11      0b      RW      Reflects the state of PHY register bit 1E.CC00.4
                                                                      before it was cleared by a firmware read.
GLOBAL_PAIR_A_CHANGE_OF_STATUS                12      0b      RW      Reflects the state of PHY register bit 1E.CC00.3
                                                                      before it was cleared by a firmware read.
GLOBAL_PAIR_B_CHANGE_OF_STATUS                13      0b      RW      Reflects the state of PHY register bit 1E.CC00.2
                                                                      before it was cleared by a firmware read.
GLOBAL_PAIR_C_CHANGE_OF_STATUS                14      0b      RW      Reflects the state of PHY register bit 1E.CC00.1
                                                                      before it was cleared by a firmware read.
GLOBAL_PAIR_D_CHANGE_OF_STATUS                15      0b      RW      Reflects the state of PHY register bit 1E.CC00.0
                                                                      before it was cleared by a firmware read.
GLOBAL_MEDIUM_BER                             16      0b      RW      Reflects the state of PHY register bit 1E.CC01.E
                                                                      before it was cleared by a firmware read.
GLOBAL_RESERVED                              31:17    0x0     RW      Reserved. Read as written.

333369-009                                                                                                               611
                                    Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

8.2.2.1.10             LED Control - LEDCTL (0x00000200)

Note:       All init bits in this register are read from the NVM. See Section 6.2.5.5 and Section 6.2.5.6.

        Field          Bit(s)   Init.   Type                                    Description

LED0_MODE               3:0     0x0     RW     LED0 Mode
                                               This field specifies the control source for the LED0 output. An initial value of
                                               0000b selects the LINK_UP indication.
RESERVED                 4       0b     RSV    Reserved.
GLOBAL_BLINK_MODE        5       0b     RW     Global Blink Mode
                                               This bit specifies the blink mode of all LEDs.
                                                0b = Blink at 200 ms on and 200 ms off.
                                                1b = Blink at 83 ms on and 83 ms off.
LED0_IVRT                6       0b     RW     LED0 Invert
                                               This bit specifies the polarity/inversion of the LED0 source prior to output or
                                               blink control. By default the output drives the cathode of the LED0 so when
                                               the LED output is 0b the LED0 is on.
                                                 0b = LED0 output is active low.
                                                 1b = LED0 output is active high.
LED0_BLINK               7       0b     RW     LED0 Blink
                                               This bit specifies whether to apply blink logic to the (inverted) LED0 control
                                               source prior to the LED0 output.
                                                0b = Do not blink LED0 output.
                                                1b = Blink LED0 output.
LED1_MODE               11:8    0x1     RW     LED1 Mode
                                               This field specifies the control source for the LED1 output. An initial value of
                                               0001b selects the 10 Gb/s link indication.
RESERVED               13:12    00b     RSV    Reserved.
LED1_IVRT                14      0b     RW     LED1 Invert
                                               This bit specifies the polarity/inversion of the LED1 source prior to output or
                                               blink control. By default the output drives the cathode of the LED so when
                                               the LED1 output is 0b the LED1 is on.
                                                 0b = LED1 output is active low.
                                                 1b = LED output is active high.
LED1_BLINK               15      1b     RW     LED1 Blink
                                               This bit specifies whether to apply blink logic to the (inverted) LED1 control
                                               source prior to the LED output.
                                                0b = Do not blink LED output.
                                                1b = Blink LED output.
LED2_MODE              19:16    0x4     RW     LED2 Mode
                                               This field specifies the control source for the LED2 output. An initial value of
                                               0100b selects LINK/ACTIVITY indication.
RESERVED               21:20    00b     RSV    Reserved.
LED2_IVRT                22      0b     RW     LED2 Invert
                                               This bit specifies the polarity/inversion of the LED2 source prior to output or
                                               blink control. By default the output drives the cathode of the LED2 so when
                                               the LED2 output is 0b the LED2 is on.
                                                 0b = LED2 output is active low.
                                                 1b = LED2 output is active high.
LED2_BLINK               23      0b     RW     LED2 Blink
                                               This bit specifies whether to apply blink logic to the (inverted) LED2 control
                                               source prior to the LED2 output.
                                                0b = Do not blink LED2 output.
                                                1b = Blink LED2 output.
LED3_MODE              27:24    0x5     RW     LED3 Mode
                                               This field specifies the control source for the LED3 output. An initial value of
                                               0101b selects the 1 Gb/s link indication.

612                                                                                                                333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

          Field            Bit(s)   Init.    Type                                        Description

RESERVED                   29:28    00b       RSV       Reserved.
LED3_IVRT                    30      0b       RW        LED3 Invert
                                                        This bit specifies the polarity/inversion of the LED3 source prior to output or
                                                        blink control. By default the output drives the cathode of the LED3 so when
                                                        the LED3 output is 0b the LED3 is on.
                                                          0b = LED3 output is active low.
                                                          1b = LED3 output is active high.
LED3_BLINK                   31      0b       RW        LED3 Blink
                                                        This bit specifies whether to apply blink logic to the (inverted) LED3 control
                                                        source prior to the LED3 output.
                                                         0b = Do not blink LED3 output.
                                                         1b = Blink LED3 output.

8.2.2.1.11                 Extended VLAN Ether Type - Receive - EXVET (0x00005078)

    Field         Bit(s)    Init.   Type                                           Description

RESERVED          15:0      0x0     RSV     Reserved.
VET_EXT           31:16    0x8100   RW      Outer VLAN Ether Type
                                            The VLAN Tag Protocol Identifier (TPID).
                                            Note: This field appears in little endian (MS byte first on the wire).

8.2.2.1.12                 Extended VLAN Ether Type - Transmit - EXVET_T
                           (0x00008224)

    Field         Bit(s)    Init.   Type                                           Description

RESERVED          15:0      0x0     RSV     Reserved.
VET_EXT           31:16    0x8100   RW      Outer VLAN Ether Type
                                            The VLAN Tag Protocol Identifier (TPID).
                                            Note: This field appears in little endian (MS byte first on the wire).

8.2.2.1.13                 Function Active and Power State to Manageability - FACTPS
                           (0x00010150)

Register for use by the device firmware for configuration.
Note:        In regular mode (port swap disabled - LAN_FUNCTION_SEL = 0b), the power state indication
             of port 0 is mapped to the FUNC0_POWER_STATE field, and the power state indication of port
             1 is mapped the FUNC1_POWER_STATE field. Vice-versa when port swap mode is enabled
             (LAN_FUNCTION_SEL = 1b).

          Field            Bit(s)   Init.    Type                                        Description

FUNC0_POWER_STATE           1:0     00b       RO        Function 0 Power State
                                                        Power state indication of function 0.
                                                         00b = DR
                                                         01b = D0u
                                                         10b = D0a
                                                         11b = D3

333369-009                                                                                                                          613
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                        Programming Interface

          Field            Bit(s)   Init.    Type                                       Description

LAN0_VALID                   2       0b       RO        LAN 0 Enable
                                                        This status of this bit reflects whether the LAN 0 function is disabled
                                                        through the external pad.
                                                          0b = Disabled
                                                          1b = Enabled
FUNC0_AUX_EN                 3       0b       RO        Function 0 Auxiliary (AUX) Power PM Enable
                                                        Shadow from the configuration space.
RESERVED                    5:4     00b       RSV       Reserved.
FUNC1_POWER_STATE           7:6     00b       RO        Function 1 Power State
                                                        Power state indication of function 1.
                                                         00b = DR
                                                         01b = D0u
                                                         10b = D0a
                                                         11b = D3
LAN1_VALID                   8       0b       RO        LAN 1 Enable
                                                        This status of this bit reflects whether the LAN 1 function is disabled
                                                        through the external pad.
                                                          0b = Disabled
                                                          1b = Enabled
FUNC1_AUX_EN                 9       0b       RO        Function 1 Auxiliary (AUX) Power PM Enable
                                                        Shadow from the configuration space.
RESERVED                   29:10    0x0       RSV       Reserved.
LAN_FUNCTION_SEL            30       0b       RO        LAN Function Select
                                                        When both LAN ports are enabled and LAN_FUNCTION_SEL =:
                                                         0b = LAN 0 is routed to PCI function 0, and LAN 1 is routed to PCI function
                                                                1.
                                                         1b = LAN 0 is routed to PCI function 1 and LAN 1 is routed to PCI function
                                                                0.
                                                        This bit is loaded from NVM.
PM_STATE_CHANGED            31       0b       RO        PM State Changed
                                                        An indication that one or more of the functional power states had changed.
                                                        This bit is also a signal to manageability to create an interrupt. This bit is
                                                        cleared on read and is not set for at least eight cycles after it was cleared.

8.2.2.1.14                 General Receive Control - GRC (0x00010200)

      Field       Bit(s)   Init.    Type                                           Description

RESERVED            0       0b      RSV     Reserved.
APME                1       0b      RW      Advance Power Management Enable
                                            If set to 1b, manageability wake-up is enabled. The device sets the PME_Status bit in
                                            the Power Management Control/Status Register (PMCSR), asserts PE_WAKE_N when
                                            manageability wake-up is enabled, and when it receives a matching magic packet. It
                                            is a single read/write bit in a single register, but has two values depending on the
                                            function that accesses the register.
                                            The value of this bit is loaded from NVM Control Word 3 (bit 0 for port 0 and bit 1 for
                                            port 1).
                                            The bit is loaded after each PCIe reset and at power on.
RESERVED          31:2      0x0     RSV     Reserved.

614                                                                                                                        333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.1.15                   Device and Functions Enable Control - DEV_FUNC_EN
                             (0x00010208)

This register is common to the two ports, and reflects the LAN disable and device disable/enable bits in
the NVM.

            Field            Bit(s)    Init.     Type                                      Description

LAN_PCI_DISABLE                   0     0b         RO     LAN PCI Disable
                                                          When set, one LAN port is disabled. The function that is disabled is
                                                          determined by the LAN_DISABLE_SELECT bit. If the disabled function is
                                                          function 0, it acts as a dummy function or the other LAN function
                                                          depending on the Dummy function enable setting.
                                                          If the disabled port is used for WoL or by MC, only the DMA block of the
                                                          port is powered down. Otherwise, the port is powered down including the
                                                          PHY.
                                                          If the LAN PCI Disable bit is set for a port, the port's respective APM bit in
                                                          NVM Control Word 3 must be cleared as well.
LAN_DISABLE_SELECT                1     0b         RO     LAN Disable Select
                                                           0b = LAN 0 is disabled.
                                                           1b = LAN 1 is disabled.
DEV_OFF_EN                        2     0b         RO     Device Electrical Off Enable
                                                          This bit is relevant only when the device is disabled via strapping during
                                                          PE_RST_N both LANn_DIS_N pins to 0b at once.
                                                           0b = Legacy mode (default). Though the device is disabled, the digital
                                                                  I/O pins are not moved to an electrical off state.
                                                           1b = Enable device electrical off. When the device is disabled, the digital
                                                                  I/O pins are put at High-Z. For example, electrical off state where
                                                                  pull-ups/downs are at their defined values.
SDP_FUNC_OFF_EN                   3     0b         RO     PCIe Function Off via SDP Pins Enable
                                                           0b = Legacy mode (default), SDPn_1 pins does not control PCIe
                                                                functions off.
                                                           1b = Two SDP pins are used in conjunction by strapping (sampled by
                                                                PE_RST_N) to disable the two PCIe functions altogether.
                                                          Note: If MNG is present, MC-to-LAN paths are not disabled. PCIe
                                                                  Function Off pins can also work independently, where each pin
                                                                  controls the corresponding PCIe function. However independent
                                                                  mode is not supported in this device.
IGNORE_PHY_FW_VALID               4     0b         RO     Ignore PHY Firmware Valid
                                                          Reflects the Ignore PHY Firmware valid indication in NVM Control Word 2.
RESERVED                      31:5     0x0        RSV     Reserved.

8.2.2.1.16                   SFP I2C Command - I2CCMD (0x00015F58)

This register is used by software to read or write to the configuration registers in an SFP module when
the SDP23_FUNCTION bit and the SDP[23]_NATIVE bit are set in ESDP register (Section 8.2.2.1.4).

    Field           Bit(s)   Init.    Type                                             Description

DATA                15:0      X       RW       Data
                                               Data in a write command: Software places the data bits and then the MAC shifts
                                               them out to the I2C bus.
                                               Data in a read command: The MAC reads these bits serially from the I2C bus and
                                               then software reads them from this location.
                                               This field is interpreted as two consecutive bytes unless the
                                               I2CPARAMS.I2C_DATA_ORDER bit is set, in which case the data is considered as a
                                               single 16-bit word. When I2CPARAMS.ACCESS_WIDTH = 0b, bits 15:8 are not used.
REGADD              23:16    0x0      RW       I2C Register Address
                                               For example, register 0, 1, 2... 255.
RESERVED            26:24    000b     RSV      Reserved

333369-009                                                                                                                           615
                                       Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Programming Interface

      Field      Bit(s)         Init.         Type                                          Description

OP                27             0b             RW     Op Code
                                                        0b = I2C write.
                                                        1b = I2C read.
RESET             28             0b             RW     Reset Sequence
                                                       If set, sends a reset sequence before the actual read or write.
                                                       This bit is self clearing. A reset sequence is defined as nine consecutive stop
                                                       conditions.
R                 29             1b             RW     Ready Bit
                                                       Set to 1b by the device at the end of the I2C transaction.
                                                       Indicates the read or write completed. Reset by a software write of a command.
RESERVED          30             0b           RSV      Reserved
E                 31             0b             RW     Error
                                                       This bit set is to 1b by hardware when it fails to complete an I2C read.
                                                       Reset by a software write of a command.
                                                       Note: This bit is valid only when the Ready (R) bit is set.

8.2.2.1.17                    SFP I2C Parameters - I2CPARAMS (0x00015F5C)

This register is used to set the parameters for I2C access and to allow bit-banging access to the I2C
interface.
Note:         This register is reset only on LAN_PWR_GOOD.

        Field          Bit(s)           Init.        Type                                      Description

WRITE_TIME                4:0           0x6          RW     Write Time
                                                            Defines the delay between a write access and the next access. The value is in
                                                            milliseconds.
                                                            Note: A value of zero is not valid.
READ_TIME                 7:5           010b         RW     Read Time
                                                            Defines the delay between a read access and the next access. The value is in
                                                            microseconds.
                                                            Note: A value of zero is not valid
I2CBB_EN                  8              0b          RW     I2C Bit-Bang Enable
                                                            If set, the I2C_CLK and I2C_DATA lines are controlled via the CLK, DATA, and
                                                            DATA_OE_N bits of this register. Otherwise, they are controlled by hardware
                                                            once activated via the I2CCMD register (Section 8.2.2.1.16).
CLK_OUT                   9              0b          RW     I2C Clock
                                                            While in bit-bang mode, controls the value driven on the I2C_CLK pad of this
                                                            port.
DATA_OUT                  10             0b          RW     I2C_DATA
                                                            While in bit-bang mode and when the DATA_OE_N field is zero, controls the
                                                            value driven on the I2C_DATA pad of this port.
DATA_OE_N                 11             0b          RW     I2C Data Output Enable
                                                            While in bit-bang mode, controls the direction of the I2C_DATA pad of this port.
                                                             0b = Pad is output.
                                                             1b = Pad is input.
DATA_IN                   12             0b          RO     I2C Data In
                                                            Reflects the value of the I2C_DATA pad. While in bit-bang mode when the
                                                            DATA_OE_N field is zero, this field reflects the value set in the DATA_OUT field.
CLK_OE_N                  13             0b          RW     I2C Clock Output Enable
                                                            While in bit-bang mode, controls the direction of the I2C_CLK pad of this port.
                                                             0b = Pad is output.
                                                             1b = Pad is input.

616                                                                                                                                333369-009
                                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field        Bit(s)    Init.      Type                                     Description

CLK_IN               14       0b         RO    I2C Clock In Value
                                               Reflects the value of the I2C_CLK pad. While in bit-bang mode when the
                                               CLK_OE_N field is zero, this field reflects the value set in the CLK_OUT field.
CLK_STRETCH_DIS      15       0b         RW    Clock Stretch Disable
                                                0b = Enable slave clock stretching support in an I2C access.
                                                1b = Disable clock stretching support in an I2C access.
ACCESS_WIDTH         16       0b         RW    I2C Access Width
                                                0b = Byte access.
                                                1b = Word access.
RESERVED            23:17    0x0        RSV    Reserved. Write 0x0, ignore on read.
PHYADD              30:24    0x0         RW    Device Address Bits 7:1
                                               The actual address used is b{PHYADD[6:0], 0}.
I2C_DATA_ORDER       31       0b         RW    I2C Data Order
                                                0b = I2CCMD.DATA field read in byte order.
                                                1b = I2CCMD.DATA field read in word order.

333369-009                                                                                                                       617
                                     Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                            Programming Interface

#### 8.2.2.2 PF - NVM Registers

8.2.2.2.1           EEPROM Mode Control Register - EEC (0x00010010)

      Field        Bit(s)   Init.   Type                                    Description

RESERVED            7:0     0x0     RSV    Reserved. Reads as 0b.
EE_PRES              8       0b     RO     NVM Present
                                           When this bit is set, indicates that an NVM is present and has the correct
                                           signature field. This bit is read-only.
AUTO_RD              9       0b     RO     NVM Auto-Read Done
                                           When set to 1b, this bit indicates that the auto-read by hardware from the
                                           NVM caused by the latest reset for this port is done. This bit is also set when
                                           the NVM is not present or when its signature field is not valid.
                                           This bit does not reflect the status of the PHY image auto-load process. Use
                                           Reset Completed (bit 6) in PHY register 1E.CC00 to get this indication.
MNG_READY           10       0b     RO     Management Auto-Load Done
                                           When set, indicates the sections needed for manageability are valid.
EE_SIZE            14:11    0x7     RO     NVM Size Via EEPROM Mode
                                           This field defines the size of the NVM that is accessible via EEPROM mode.
                                           This is equal to the size of the internal Shadow RAM, fixed to 16 KB (0x7
                                           defines 16 KB - legacy).
PCI__ANA_DONE       15       0b     RO     PCIe Analog Done
                                           When set to 1b, indicates that the PCIe analog section read from NVM is
                                           done. This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
PCI_CORE_DONE       16       0b     RO     PCIe Core Done
                                           When set to 1b, indicates that the core analog section read from NVM is
                                           done. This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
                                           Note: This bit returns the relevant done indication for the function that
                                                     reads the register.
PCI_GENERAL_DONE    17       0b     RO     PCIe General Done
                                           When set to 1b, indicates that the PCIe general section read from the NVM is
                                           done. This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
PCI_FUNC_DONE       18       0b     RO     PCIe Function Done
                                           When set to 1b, indicates that the PCIe function section read from the NVM is
                                           done. This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
                                           Note: This bit returns the relevant done indication for the function that
                                                     reads the register.
CORE_DONE           19       0b     RO     Core Done
                                           When set to 1b, indicates that the core section read from the NVM is done.
                                           This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
                                           Note: This bit returns the relevant done indication for the function that
                                                     reads the register.
CORE_CSR_DONE       20       0b     RO     Core CSR Done
                                           When set to 1b, indicates that the core CSR section read from the NVM is
                                           done. This bit is cleared when auto-read starts.
                                           This bit is also set when the NVM is not present or when its signature field is
                                           not valid.
                                           Note: This bit returns the relevant done indication for the function that
                                                     reads the register.

618                                                                                                           333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

         Field            Bit(s)    Init.   Type                                      Description

MAC_DONE                   21        0b      RO     MAC Done
                                                    When set to 1b, indicates that the MAC section read from the NVM is done.
                                                    This bit is cleared when auto-read starts.
                                                    This bit is also set when the NVM is not present or when its signature field is
                                                    not valid.
                                                    Note: This bit returns the relevant done indication for the function that
                                                              reads the register.
LCB_DONE                   22        0b      RO     LCB Done
                                                    When set, indicates that the LCB section read from the NVM is done. This bit
                                                    is cleared when auto-read starts.
                                                    This bit is also set when the NVM is not present or when its signature field is
                                                    not valid.
RESERVED                  24:23     00b     RSV     Reserved. Reads as 00b.
SEC1VAL                    25        0b      RO     Sector 1 Valid
                                                    Meaningful only when the EE_PRES bit is read as 1b.
                                                     0b = Indicates that the content of the first section (from byte address
                                                            0x0000 to 0x3FFF) is valid.
                                                     1b = Indicates that the content of the second Shadow RAM section (from
                                                            byte address 0x4000 to 0x7FFF) of the Flash device is valid.
                                                    This bit can be written by firmware
FLUDONE                    26        1b      RO     Flash Update Done
                                                    When set to 1b, indicates that the last Flash update process completed.
                                                    This bit is set by firmware.
RESERVED                   27        1b     RSV     Reserved.
RESERVED                  31:28     0x0     RSV     Reserved. Reads as 0b.

8.2.2.2.2                  Flash Access Register - FLA (0x0001001C)

Note:        When NVM is locked, this register is RO to software.

    Field        Bit(s)     Init.    Type                                         Description

FL_SCK             0         0b       RW    Clock input to the Flash
                                            When FL_GNT is set to 1b, the FL_SCK output signal is mapped to this bit and
                                            provides the serial clock input to the Flash. Software clocks the Flash via toggling this
                                            bit with successive writes.
FL_CE              1         0b       RW    Chip select input to the Flash
                                            When FL_GNT is set to 1b, the FL_CE output signal is mapped to the chip select of the
                                            Flash device. Software enables the Flash by writing a 0b to this bit.
FL_SI              2         0b       RW    Data input to the Flash
                                            When FL_GNT is set to 1b, the FL_SI output signal is mapped directly to this bit.
                                            Software provides data input to the Flash via writes to this bit.
FL_SO              3         0b      ROS    Data output bit from the Flash
                                            The FL_SO input signal is mapped directly to this bit in the register and contains the
                                            Flash serial data output. This bit is read-only from a software perspective.
                                            Note: Writes to this bit have no effect.
FL_REQ             4         0b       RW    Request Flash Access
                                            Software must write 1b to this bit to get direct Flash access. It has access when
                                            FL_GNT is set to 1b. When software completes the access, it must then write 0b.
FL_GNT             5         0b       RO    Grant Flash Access
                                            When this bit is set to 1b, software can access the Flash using the FL_SCK, FL_CE,
                                            FL_SI, and FL_SO bits.
RESERVED           6         0b       RO    Reserved.
JTAG_DIS           7         0b       RO    JTAG Disable
                                            Reflects the value of the JTAG_DIS strap.

333369-009                                                                                                                        619
                                      Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

      Field     Bit(s)       Init.         Type                                          Description

RESERVED        11:8         0x0           RSV     Reserved. Reads as 0b.
FL_SIZE         14:12        101b          RO      Flash Size
                                                   Indicates Flash size of 64 KB * 2 ** “FL_SIZE”.
                                                   The Flash size impacts the requested memory space for the Flash and expansion ROM
                                                   BARs in PCIe configuration space (according to the CSRSIZE and FL_BAR_SIZE fields
                                                   in the PCI_LBARCTRL register - Section 8.2.2.5.6).
                                                   Supported Flash sizes:
                                                     101b = 2 MB
                                                     110b = 4 MB
                                                   This register limits the accesses to the actual flash size.
RESERVED         15           0b           RSV     Reserved. Reads as 0b.
FL_SADDR        28:16        0x0           RW      Flash Sector Erase Address
                                                   Determines which 4 KB sector is erased when the FL_SER command is used. This
                                                   address is expressed in sector index units, starting from sector index 0.
FL_SER           29           0b           RW      Flash Sector Erase Command
                                                   This bit is auto-cleared and reads as 0b. The 4 KB sector index to be erased is
                                                   determined by the FL_SADDR field.
                                                   Note: The address should fit in the size defined in the FLA.FL_SIZE field.
FL_BUSY          30           0b           RO      Flash Busy
                                                   This bit is set to 1b by hardware while Flash access has been granted to a client.
                                                   Note: This bit is read-only from a software perspective.
                                                   Note: This bit only reflect flash busy state if FLA mechanisms, like FL_SER or
                                                             FL_DER, are used.
                                                   If the flash is busy due to some action done directly on the SPI pins, it is not reflected
                                                   in this bit.
FL_DER           31           0b           RW      Flash Device Erase Command
                                                   This bit is auto-cleared and reads as 0b. The entire Flash device is erased.

8.2.2.2.3                    Manageability EEPROM-Mode Control Register - EEMNGCTL
                             (0x00010110)

This register is read/write to manageability firmware, and is read-only to host software. The
transactions performed through this register are directed to/from the internal Shadow RAM.

        Field       Bit(s)         Init.        Type                                       Description

ADDR                  12:0           0x0         RW    Address
                                                       This field is written by manageability along with the START and WRITE bits to
                                                       indicate which NVM word address to read or write. Only the first valid 16 KB is
                                                       accessible through this EEPROM mode interface dedicated to manageability.
RESERVED            14:13            00b         RSV   Reserved. Reads as 0b.
START                   15           0b          RW    Start
                                                       Writing a 1b to this bit causes the device to start the read or write operation of
                                                       the Shadow RAM according to the write bit. This bit is self cleared by hardware.
                                                       If one of the CFG_DONE0/1 bit’s value is set in this write, writing of this bit is
                                                       ignored.
WRITE                   16           0b          RW    Write
                                                       This bit signals the device if the current operation is read or write.
                                                        0b = Read
                                                        1b = Write
EEBUSY                  17           0b          RW    EEPROM Mode Busy
                                                       This bit indicates that the internal Shadow RAM is busy and should not be
                                                       accessed.

620                                                                                                                               333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

       Field      Bit(s)         Init.       Type                                            Description

CFG_DONE0              18           0b         RW         Configuration Done Port 0
                                                          Manageability configuration cycle of port 0 completed.
                                                          This bit indicates that the manageability configuration cycle (configuration of
                                                          PCIe, core or PHY) completed. This bit is set to 1b by manageability firmware to
                                                          indicate that the configuration completed and is cleared by software.
                                                          Writing a 0b by firmware does not affect the state of this bit. Writing a 1b by
                                                          software does not affect the state of this bit.
                                                          Note: Software should not try to access the PHY for configuration before this bit
                                                                    is set.
CFG_DONE1              19           0b         RW         Configuration Done Port 1
                                                          Manageability configuration cycle of port 1 completed.
                                                          This bit indicates that the manageability configuration cycle (configuration of
                                                          PCIe, core or PHY) completed. This bit is set to 1b by manageability firmware to
                                                          indicate that the configuration completed and is cleared by software.
                                                          Writing a 0b by firmware does not affect the state of this bit. Writing a 1b by
                                                          software does not affect the state of this bit.
                                                          Note: Software should not try to access the PHY for configuration before this bit
                                                                    is set.
TRANS_ABORTED          20           0b           RO       Transaction Aborted
                                                          When read as 1b, indicates that the current EEMNGCTL access was aborted due
                                                          to a firmware reset. The bit is cleared by hardware on the next write access to the
                                                          EEMNGCTL register, regardless of the written value.
RESERVED           30:21            0x0        RSV        Reserved.
DONE                   31           1b         RW         Transaction Done
                                                          This bit is cleared when the START and WRITE bits are set by manageability, and
                                                          is set back again when the Shadow RAM write or read transaction completes.

8.2.2.2.4                   Manageability EEPROM-Mode Read/Write Data -
                            EEMNGDATA (0x00010114)

This register is read/write to manageability firmware, and is read-only to host software.

    Field      Bit(s)       Init.         Type                                             Description

WRDATA         15:0         0x0           RW          Write Data
                                                      Data to be written to the Shadow RAM.
RDDATA         31:16         X            RW          Read Data
                                                      Data returned from the read command.
                                                      Note: This field is read only.

8.2.2.2.5                   Manageability Flash Control Register - FLMNGCTL
                            (0x00010118)

This register is read/write to manageability firmware, and is read-only to host software.

    Field      Bit(s)       Init.         Type                                             Description

ADDR           23:0         0x0           RW          Address
                                                      This field is written by manageability along with CMD and CMDV to indicate which
                                                      Flash address to read or write. For the Sector Erase command (CMD = 10b), it must
                                                      point to any address in the 4 KB sector to be erased.

333369-009                                                                                                                                621
                                           Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

      Field      Bit(s)      Init.      Type                                          Description

CMD               25:24         00b      RW      Command
                                                 Indicates which command should be executed. Valid only when the CMDV bit is set.
                                                  00b = Read
                                                  01b = Write (single byte)
                                                  10b = Sector Erase — The ADDR field determines the 4 KB sector index to be erased
                                                         by this command.
                                                  11b = Device Erase
CMDV               26           0b       RW      Command Valid
                                                 When set, indicates that the manageability firmware issues a new command and is
                                                 cleared by hardware at the end of the command.
FLBUSY             27           0b       RW      Flash Busy
                                                 This bit indicates that the Flash is busy processing a Flash transaction and should not
                                                 be accessed.
RESERVED          29:28         00b      RSV     Reserved.
DATA_VALID         30           0b       RW      Read Done
                                                 Read done and data in FLMNGDATA is valid.
                                                 This bit is cleared by firmware when it sets the CMDV bit. It is set by hardware for
                                                 each DWord read that completes. This bit is read/clear by hardware enabling the
                                                 multiple DWord read flow.
GLDONE             31           1b       RW      Global Done
                                                 This bit clears after the CMDV bit is set by manageability, and is set back again when
                                                 all Flash transactions complete. For example, the Flash device finished reading all the
                                                 requested read or other accesses (write and erase).

8.2.2.2.6                   Manageability Flash Read/Write Data - FLMNGDATA
                            (0x0001011C)

This register is read/write to manageability firmware, and is read-only to host software.

      Field      Bit(s)      Init.      Type                                          Description

DATA              31:0          0x0      RW      Data
                                                 Read/Write data on a read transaction. This register contains the data returned from
                                                 the Flash read. On write transactions, bits 7:0 are written to the Flash.

8.2.2.2.7                   JEDEC ID 1 - JEDEC_ID_1 (0x00015F2C)

Exposes the JEDEC ID of the connected flash. Reflects an internal auxiliary register.
Note:         This register is valid only if a valid firmware is present.

         Field            Bit(s)      Init.     Type                                      Description

BANK                       6:0        0x0        ROS    Bank
                                                        Defines the bank number of the manufacturer ID (number of 0x7F read).
VALID                       7          0b        ROS    Valid
                                                        When this bit is set, the firmware stored a valid content to this register.
MANUFACTURER_ID           15:8        0x0        ROS    Manufacturer ID
                                                        Returns the manufacturer ID read by RDID command.
DEVICE_ID_1               23:16       0x0        ROS    Device ID 1
                                                        First byte of the device ID read by RDID command (Family and Density fields).
DEVICE_ID_2               31:24       0x0        ROS    Device ID 2
                                                        Second Byte of the device ID read by RDID command (Sub version and
                                                        Revision).

622                                                                                                                           333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.3 PF - Flow Control Registers

8.2.2.3.1                 Flow Control Transmit Timer Value n - FCTTVN[n]
                          (0x00003200 + 0x4*n, n=0...3)

Each 32-bit register (n=0...3) refers to two timer values (register 0 refers to timer 0 and 1; register 1
refers to timer 2 and 3, etc.).
Note:         The 16-bit value in the TTV field is inserted into a transmitted frame (either XOFF frames or
              any pause frame value in any software transmitted packets). It counts in units of slot time
              (usually 64 bytes). The device uses a fixed slot time value of 64-byte times.

      Field      Bit(s)    Init.   Type                                       Description

TTV_2N            15:0     0x0     RW     Transmit Timer Value 2n
                                          Timer value included in XOFF frames as Timer (2n). The same value must be set to
                                          User Priorities (UPs) attached to the same TC, as defined in the RTTUP2TC register.
                                          For legacy 802.3X flow control packets, TTV0 is the only timer that is used.
TTV_2N_1         31:16     0x0     RW     Transmit Timer Value 2n+1
                                          Timer value included in XOFF frames as Timer 2n+1. The same value must be set to
                                          UPs attached to the same TC, as defined in the RTTUP2TC register.

8.2.2.3.2                 Flow Control Receive Threshold Low - FCRTL[n]
                          (0x00003220 + 0x4*n, n=0...7)

This register contains the receive threshold used to determine when to send an XON packet, and counts
in units of bytes. The lower four bits must be programmed to 0x0 (16-byte granularity). Software must
set XONE to enable the transmission of XON frames. Each time incoming packets cross the receive high
threshold (become more full), and then crosses the receive low threshold, with XONE enabled (1b),
hardware transmits an XON frame.
Note:         Each 32-bit register (n=0...7) refers to a different receive packet buffer.

      Field      Bit(s)    Init.   Type                                       Description

RESERVED          4:0      0x0     RSV    Reserved.
RTL               18:5     0x0     RW     Receive Threshold Low n
                                          Receive packet buffer n FIFO low water mark for flow control transmission (32-byte
                                          granularity).
RESERVED         30:19     0x0     RSV    Reserved.
XONE               31       0b     RW     XON Enable n
                                          Per the receive packet buffer XON enable.
                                           0b = Disabled
                                           1b = Enabled

333369-009                                                                                                                  623
                                    Did this document help answer your questions?

                                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                                Programming Interface

8.2.2.3.3                   Flow Control Receive Threshold High - FCRTH[n]
                            (0x00003260 + 0x4*n, n=0...7)

This register contains the receive threshold used to determine when to send an XOFF packet and counts
in units of bytes. This value must be at least eight bytes less than the maximum number of bytes
allocated to the receive packet buffer and the lower five bits must be programmed to 0x0 (32-byte
granularity). Each time the receive FIFO reaches the fullness indicated by RTH, hardware transmits a
pause frame if the transmission of flow control frames is enabled.
Note:          Each 32-bit register (n=0... 7) refers to a different receive packet buffer.

      Field       Bit(s)        Init.         Type                                         Description

RESERVED           4:0          0x0           RSV     Reserved.
RTH                18:5         0x0           RW      Receive Threshold High n
                                                      Receive packet buffer n FIFO high water mark for flow control transmission (32-byte
                                                      granularity).
RESERVED          30:19         0x0           RSV     Reserved.
FCEN                31           0b           RW      Flow Control Enable
                                                      Transmit Flow control enable for packet buffer n. Should be set only for traffic classes
                                                      to which UPs are mapped (in RTRUP2TC register).

8.2.2.3.4                   Flow Control Refresh Threshold Value - FCRTV
                            (0x000032A0)

       Field          Bit(s)          Init.      Type                                        Description

FC_REFRESH_TH            15:0           0x0         RW    Flow Control Refresh Threshold
                                                          This value is used to calculate the actual refresh period for sending the next
                                                          pause frame if conditions for a pause state are still valid (buffer fullness above
                                                          low threshold value). The formula for the refresh period for priority group N is:
                                                            FCTTV[N/2].TTV[Nmod2] - FCRTV.FC_REFRESH_TH
                                                          Note: The FC_REFRESH_TH must be smaller than TTV of the TC and larger than
                                                                   the maximum packet size in the TC + FC packet size + link latency and
                                                                   Tx latency and Rx latency in 64-byte units.
RESERVED              31:16             0x0         RSV   Reserved.

8.2.2.3.5                   Flow Control Configuration - FCCFG (0x00003D00)

      Field       Bit(s)        Init.         Type                                         Description

RESERVED           2:0          000b          RSV     Reserved.
TFCE               4:3          00b           RW      Transmit Flow Control Enable
                                                      These bits indicate that the device transmits flow control packets (XON/XOFF frames)
                                                      based on receive fullness. If auto-negotiation is enabled, this bit should be set by
                                                      software to the negotiated flow control value.
                                                       00b = Transmit flow control disabled.
                                                       01b = Link flow control enabled.
                                                       10b = Priority flow control enabled.
                                                       11b = Reserved.
                                                      Note: Priority flow control should be enabled in DCB mode only.
RESERVED           31:5         0x0           RSV     Reserved.

624                                                                                                                               333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.3.6              MAC Flow Control Register - MFLCN (0x00004294)

      Field   Bit(s)    Init.   Type                                         Description

PMCF             0       0b      RW    Pass MAC Control Frames
                                       Filter out unrecognized pause (flow control opcode does not match) and other control
                                       frames.
                                         0b = Filter unrecognized pause frames.
                                         1b = Pass/forward unrecognized pause frames.
DPF              1       0b      RW    Discard Pause Frame
                                         0b = PAUSE frames are sent to the host.
                                         1b = PAUSE frames are discarded only when RFCE or RPFCM are set to 1b.
                                       If both RFCE and RPFCM are set to 0b, this bit has no effect on incoming PAUSE
                                       frames.
RPFCM            2       0b      RW    Receive Priority Flow Control Mode
                                       Indicates that the X550 responds to the reception of Priority Flow Control packets. If
                                       auto-negotiation is enabled, this bit should be set by software to the negotiated flow
                                       control value.
                                       This bit must be set as a logical “OR” over the RPFCE[7:0] bitmap. It is useful to
                                       control forwarding of PFC frames to host if required.
                                       Notes:
                                        1. Priority Flow control should be enabled in DCB mode only.
                                        2. Receive Priority Flow Control and Receive Link Flow Control are mutually
                                           exclusive and user should not configure both of them to be enabled at the same
                                           time.
                                        3. This bit should not be set if bit 3 (RFCE) is set.
RFCE             3       0b      RW    Receive Link Flow Control Enable
                                       Indicates that the X550 responds to the reception of Link Flow Control packets. If
                                       auto-negotiation is enabled, this bit should be set by software to the negotiated flow
                                       control value.
                                       Note: This bit should not be set if bit 2 is set.
RPFCE          11:4     0x0      RW    Receive Priority Flow Control Enable bitmap
                                       When bit n is:
                                        0b = Priority Flow Control indication received for UP#n is ignored and transmit from
                                             UP#n is not paused.
                                        1b = The device responds to the reception of Priority Flow Control packets for UP#n.
RESERVED       31:12    0x0      RSV   Reserved.

8.2.2.3.7              Priority Flow Control Type Opcode - PFCTOP (0x0000431C)

This register contains the Type and Opcode fields that are matched against a recognized priority flow
control packet.

      Field   Bit(s)    Init.   Type                                         Description

FCT            15:0    0x8808    RW    Priority Flow Control EtherType
                                       This field appears in little endian (MS byte first on the wire).
FCOP           31:16   0x0101    RW    Priority Flow Control Opcode
                                       This field appears in big endian (LS byte first on the wire).

8.2.2.3.8              Transmit Flow Control Status - TFCS (0x0000CE00)

      Field   Bit(s)    Init.   Type                                         Description

TC_XON          7:0     0xFF     RO    TC XON
                                       TC is in FC XON state.
RESERVED       31:8     0x0      RSV   Reserved.

333369-009                                                                                                                 625
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                    Programming Interface

#### 8.2.2.4 PF - PCIe Registers

This section contains the registers used to control the PCIe core behavior.

8.2.2.4.1               PCIe Function Status 1 - PCI_STATUS1 (0x00011028)

      Field   Bit(s)     Init.    Type                                          Description

FUNC_VALID      0         0b      RO      Function Valid
                                          0b - Function is disabled
                                          1b - Function is enabled
                                          Note: This bit is valid to firmware even when the function is disabled
RESERVED      31:1       0x0      RSV     Reserved.

8.2.2.4.2               PCIe Firmware Control - PCI_FWCTRL (0x00011040)

      Field    Bit(s)     Init.    Type                                         Description

TCO_ISOLATE         0      0b      RW      TCO Isolate
                                           Set to 1b on a TCO Reset SMBus or NC-SI OEM command, when the TCO_ISOLATE
                                           bit is set.
                                           Host write cycles are completed successfully on the PCIe, but silently ignored by
                                           internal logic.
                                           Note: When firmware initiates the TCO Isolate command, it also writes a value of
                                                     0x03 to the FWSM.EXT_ERR_IND field.
                                           This bit is RO and mirrors the value of the Isolate bit in the internal management
                                           registers.
                                           Note:
                                             1. Bit is reset by LAN_PWR_GOOD and firmware reset only.
                                             2. Bit reflects internal management register Aux bit.
RESERVED        31:1       0x0     RSV     Reserved.

8.2.2.4.3               PCIe CSR Access Timeout - PCI_CSRTO (0x00011044)

      Field   Bit(s)     Init.    Type                                          Description

CSR_TO        15:0      0x000F    RW      CSR Timeout
                                          Defines the timeout value in micro second for CSR accesses
MSIX_TO       31:16     0x0028    RW      MSI-X Timeout
                                          Defines the timeout value in micro second for MSI-X table accesses

8.2.2.4.4               PCIe Control Extended Register - GCR_EXT (0x00011050)

      Field   Bit(s)     Init.    Type                                          Description

VT_MODE        1:0       00b      RW      VT Mode of operation
                                          Defines the allocation of physical registers to the VFs. Software must set this field the
                                          same as GPIE.
                                          VT_Mode:
                                           00b = noVT — Reserved for the case that STATUS.IOV_ENA is not set.
                                           01b = VT16 — Resources are allocated to 16 VFs.
                                           10b = VT32 — Resources are allocated to 32 VFs
                                           11b = VT64 — Resources are allocated to 64 VFs.
RESERVED       3:2       00b      RSV     Reserved.

626                                                                                                                    333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

    Field      Bit(s)      Init.         Type                                              Description

APBACD           4          0b            RW          Auto PBA Clear Disable
                                                        0b = Any active PBA entry is cleared on the falling edge of the appropriate interrupt
                                                             request to the PCIe block.
                                                        1b = Software can clear PBA only by direct write to clear access to the PBA bit.
                                                      The appropriate interrupt request is cleared when software sets the associated
                                                      interrupt mask bit in the EIMS (re-enabling the interrupt) or by direct write to clear
                                                      the PBA.
RESERVED       31:5        0x0            RSV         Reserved.

8.2.2.4.5                 PCI Flash Access Timeout - PCI_FLASHTO (0x00011054)

     Field      Bit(s)           Init.              Type                                      Description

PCI_FLASHTO      31:0      0x00000FA0               RW      PCI Flash Timeout
                                                            Defines the timeout value in microseconds for flash accesses.

8.2.2.4.6                 Function Requester ID Information Register - FUNC_RID
                          (0x00011070)

       Field            Bit(s)         Init.         Type                                     Description

FUNCTION_NUMBER          2:0           000b          RO      Function Number
                                                             Function number assigned to the function based on BIOS/OS Enumeration.
DEVICE_NUMBER            7:3           0x0           RO      Device Number
                                                             Device number assigned to the function based on BIOS/OS Enumeration.
BUS_NUMBER               15:8          0x0           RO      Bus Number
                                                             Bus Number assigned to the function based on BIOS/OS Enumeration.
RESERVED                31:16          0x0           RSV     Reserved.

8.2.2.4.7                 PCIe Revision ID - PCI_REVID (0x00011098)

    Field      Bit(s)      Init.         Type                                              Description

NVM_REVID       7:0        0x0            RW          NVM Revision ID
                                                      Value of Rev ID loaded from NVM. This value is XORed with the hardware default to
                                                      create the value reflected in the config space.
RESERVED       31:8        0x0            RSV         Reserved.

8.2.2.4.8                 PCIe Errors Reported - PCI_PCIERR (0x00011140)

This register indicates which PCIe errors are reported to device software.

     Field      Bit(s)         Init.       Type                                             Description

PCIE_ERR_REP     31:0           0x0            RO      PCIe Errors Reported
                                                       Each bit corresponds to a particular error event as described in Section 3.1.5.8,
                                                       “Proprietary Error Reporting”.

333369-009                                                                                                                                 627
                                           Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Programming Interface

8.2.2.4.9                   PCIe Interrupt Cause - PCI_ICAUSE (0x00011520)

       Field          Bit(s)         Init.        Type                                        Description

PCIE_ERR_CAUSE         31:0            0x0      RW1C       Each bit corresponds to a particular error event as described in Section 3.1.5.8,
                                                           “Proprietary Error Reporting”.

8.2.2.4.10                  PCIe Interrupts Enable - PCI_IENA (0x00011528)

      Field      Bit(s)         Init.         Type                                           Description

PCIE_ERR_EN       31:0           0x0          RW         Each bit corresponds to a particular error event as described in Section 3.1.5.8,
                                                         “Proprietary Error Reporting”.

8.2.2.4.11                  PCIe VM Pending Index - PCI_VMINDEX (0x00011530)

      Field     Bit(s)         Init.         Type                                           Description

VMINDEX          8:0           0x0           RW       VM Index
                                                      Software sets the VMINDEX that its transaction pending flag should be reflected in the
                                                      PCI_VMPEND register (Section 8.2.2.4.12).
                                                      The VM index is an absolute index in the range of 0 through 63. It can be set by the
                                                      software only to VMs that the PF owns and only to VMs which are not assigned to a VF.
RESERVED        31:9           0x0           RSV      Reserved.

8.2.2.4.12                  PCIe VM Pending Status - PCI_VMPEND (0x00011538)

      Field     Bit(s)         Init.         Type                                           Description

PENDING           0             0b           RO       PCIe Transaction Pending Status
                                                      The reported VM is controlled by the VMINDEX field in the PCI_VMINDEX register
                                                      (Section 8.2.2.4.11).
                                                      This flag is set to 1b as long as there is at least one PCIe transaction, pending for its
                                                      completion.
RESERVED        31:1           0x0           RSV      Reserved.

8.2.2.4.13                  PCIe Default Revision ID - PCI_DREVID (0x00011540)

       Field      Bit(s)         Init.         Type                                           Description

DEFAULT_REVID         7:0         0x1           RO        Default Revision ID
                                                          Mirroring of Default Rev ID prior to NVM load.
                                                           0x00 = A0
                                                           0x01 = B0
RESERVED           31:8           0x0          RSV        Reserved.

628                                                                                                                                 333369-009
                                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.4.14                PCIe Byte Counter High - PCI_BYTCTH (0x00011544)

A byte counter used by the PCIe performance counters.

        Field            Bit(s)    Init.   Type                                     Description

PCI_COUNT_BW_BCT         31:0      0x0      RO     PCIe Byte Counter High
                                                   This register contains the high double-word of a 64-bit counter that counts
                                                   PCIe payload bytes.
                                                   This register gets stuck at its maximum value of 0xFF...F.

8.2.2.4.15                PCIe Byte Counter Low - PCI_BYTCTL (0x00011548)

A byte counter used by the PCIe performance counters.

        Field            Bit(s)    Init.   Type                                     Description

PCI_COUNT_BW_BCT         31:0      0x0      RO     PCIe Byte Counter Low
                                                   This register contains the low double-word of a 64-bit counter that counts
                                                   PCIe payload bytes.
                                                   This register gets stuck at its maximum value of 0xFF...F.

8.2.2.4.16                PCIe LCB Data Port - PCI_LCBDATA (0x00011734)

    Field       Bit(s)     Init.    Type                                        Description

LCB_DATA        31:0       0x0       RW    LCB Data
                                           A 32-bit data register (part of a port) used to load NVM configuration into the PCIe
                                           LCB unit. Operates together with the PCI_LCBADD register (Section 8.2.2.4.17).

8.2.2.4.17                PCIe LCB Address Port - PCI_LCBADD (0x00011788)

    Field       Bit(s)     Init.    Type                                        Description

ADDRESS         17:0       0x0       RW    Address
                                           An 18-bit address register (part of a port) used to load NVM configuration into the
                                           PCIe LCB unit.
                                           Operates together with the PCI_LCBDATA register (Section 8.2.2.4.16).
RESERVED        19:18      00b      RSV    Reserved.

333369-009                                                                                                                       629
                                     Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                          Programming Interface

      Field      Bit(s)      Init.      Type                                         Description

BLOCK_ID         27:20          0x0      RW      Block ID
                                                 An ID of a sub-unit in the PCIe unit. Supported values are:
                                                  0    = NPQ: RLAN
                                                  1    = NPQ: TLAN
                                                  2    = NPQ: RX_PE
                                                  3    = NPQ: TX_PE
                                                  4    = NPQ: PMAT
                                                  5    = NPQ: MNG
                                                  6    = NPQ: TDPU
                                                  7    = PQ: RLAN
                                                  8    = PQ: TLAN
                                                  9    = PQ: RX_PE
                                                  10   = PQ: TX_PE
                                                  11   = PQ: PMAT
                                                  12   = PQ: MNG
                                                  13   = PQ: RDPU
                                                  14   = VDM
                                                  15   = Don't care
                                                  16   = HIU: CFG/Slave/MSG/MSI-X
                                                  126 = LCB's internal config space registers
                                                  127 = LCB's internal memory space registers
RESERVED         31:28          0x0      RSV     Reserved.

8.2.2.4.18                  PCIe Statistic Control Register #1 - PCI_GSCL_1
                            (0x00011800)

This register controls the operation of the PCIe performance counters.

         Field            Bit(s)      Init.     Type                                     Description

GIO_COUNT_EN_0              0          0b        RW     GIO Counter 0 Enable
                                                        Enables PCIe statistic counter number 0.
GIO_COUNT_EN_1              1          0b        RW     GIO Counter 1 Enable
                                                        Enables PCIe statistic counter number 1.
GIO_COUNT_EN_2              2          0b        RW     GIO Counter 2 Enable
                                                        Enables PCIe statistic counter number 2.
GIO_COUNT_EN_3              3          0b        RW     GIO Counter 3 Enable
                                                        Enables PCIe statistic counter number 3.
LBC_ENABLE_0                4          0b        RW     Leaky Bucket Counter 0 Enable
                                                         0b = Leaky Bucket mode is disabled and the counter is incremented by one
                                                              for each event.
                                                         1b = Statistics counter 0 operates in Leaky Bucket mode.
LBC_ENABLE_1                5          0b        RW     Leaky Bucket Counter 1 Enable
                                                         0b = Leaky Bucket mode is disabled and the counter is incremented by one
                                                              for each event.
                                                         1b = Statistics counter 1 operates in Leaky Bucket mode.
LBC_ENABLE_2                6          0b        RW     Leaky Bucket Counter 2 Enable
                                                         0b = Leaky Bucket mode is disabled and the counter is incremented by one
                                                              for each event.
                                                         1b = Statistics counter 2 operates in Leaky Bucket mode.
LBC_ENABLE_3                7          0b        RW     Leaky Bucket Counter 3 Enable
                                                         0b = Leaky Bucket mode is disabled and the counter is incremented by one
                                                              for each event.
                                                         1b = Statistics counter 3 operates in Leaky Bucket mode.

630                                                                                                                    333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

       Field         Bit(s)   Init.     Type                                     Description

PCI_COUNT_LAT_EN       8       0b        RW    PCIe Count Latency Enable
                                               Enables the latency counter.
                                                0b = Disable the latency counter.
                                                1b = Enable the latency counter.
PCI_COUNT_LAT_EV     13:9     0x0        RW    PCIe Count Latency Event
                                               Selects the event to be measured.
PCI_COUNT_BW_EN       14       0b        RW    PCIe Count Bandwidth Enable
                                               Enables the bandwidth counter.
                                                0b = Disable the bandwidth counter.
                                                1b = Enable the bandwidth counter.
PCI_COUNT_BW_EV      19:15    0x0        RW    PCIe Count Bandwidth Event
                                               Selects the event to be measured.
RESERVED             27:20    0x0        RSV   Reserved.
GIO_64_BIT_EN         28       0b        RW    GIO 64-bit Enable
                                               Enables two 64-bit counters instead of four 32-bit counters.
GIO_COUNT_RESET       29       0b       RWS    GIO Counter Reset
                                               Reset indication of PCIe statistic counters. Write of zero has no effect.
GIO_COUNT_STOP        30       0b       RWS    GIO Counter Stop
                                               Stop indication of PCIe statistic counters. Write of zero has no effect.
GIO_COUNT_START       31       0b       RWS    GIO Counter Start
                                               Start indication of PCIe statistic counters. Write of zero has no effect.

8.2.2.4.19             PCIe Statistic Control Registers #2 - PCI_GSCL_2
                       (0x00011804)

This register defines the events counted by the performance counters.

       Field         Bit(s)   Init.     Type                                     Description

GIO_EVENT_NUM_0       7:0     0x0        RW    GIO Event Number 0
                                               Event number that counter 0 counts (GSCN_0).
GIO_EVENT_NUM_1      15:8     0x0        RW    GIO Event Number 1
                                               Event number that counter 1 counts (GSCN_1).
GIO_EVENT_NUM_2      23:16    0x0        RW    GIO Event Number 2
                                               Event number that counter 2 counts (GSCN_2).
GIO_EVENT_NUM_3      31:24    0x0        RW    GIO Event Number 3
                                               Event number that counter 3 counts (GSCN_3).

333369-009                                                                                                                 631
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Programming Interface

8.2.2.4.20            PCIe Statistic Control Register #5...#8 - PCI_GSCL_5_8[n]
                      (0x00011810 + 0x4*n, n=0...3)

These registers control the operation of the leaky bucket counter n.
      GSCL_5 corresponds to n=0.
      GSCL_6 corresponds to n=1.
      GSCL_7 corresponds to n=2.
      GSCL_8 corresponds to n=3.

        Field       Bit(s)     Init.     Type                                    Description

LBC_THRESHOLD_N      15:0       0x0       RW      Leaky Bucket Counter Threshold n
                                                  Threshold for the Leaky Bucket Counter n.
LBC_TIMER_N         31:16       0x0       RW      Leaky Bucket Counter Timer n
                                                  Time period between decrementing the value in Leaky Bucket Counter n.
                                                  The time period is defined in s units.

8.2.2.4.21            PCIe Statistic Counter Registers #0...#3 -
                      PCI_GSCN_0_3[n] (0x00011820 + 0x4*n, n=0...3)

These registers contain the performance counters 0-3.
      GSCL_0 corresponds to n=0.
      GSCL_1 corresponds to n=1.
      GSCL_2 corresponds to n=2.
      GSCL_3 corresponds to n=3.

       Field      Bit(s)     Init.     Type                                     Description

EVENT_COUNTER     31:0       0x0        RO      Event Counter
                                                Event counter as defined in PCI_GSCL_2.GIO_EVENT_NUM_[0...3] fields.
                                                These registers are stuck at their maximum value of 0xFF...F.

632                                                                                                              333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.5 PF - PCIe Configuration Space Setting Registers

This section contains registers used to set the default setting of the PCIe configuration space. These
registers are reset and loaded from the NVM at PCIe reset.

8.2.2.5.1                 PCIe PF Configuration - PCI_CNF (0x00011000)

Contains the per-PF configuration loaded from the NVM.

    Field     Bit(s)          Init.         Type                                        Description

RESERVED        2:0          000b           RW     Reserved.
EXROM_DIS        3             1b           RW     Expansion ROM Disable
                                                    0b = The Expansion ROM BAR in the PCI configuration space is enabled.
                                                    1b = The Expansion ROM BAR in the PCI configuration space is disabled.
IO_BAR           4             0b           RW     I/O BAR support
                                                    0b = I/O BAR is not supported.
                                                    1b = I/O BAR is supported.
INT_PIN         6:5           00b           RW     Interrupt Pin
                                                   Controls the value advertised in the Interrupt Pin field of the PCI configuration header
                                                   for this function.
                                                     00b = INTA#
                                                     01b = INTB#
                                                     10b = INTC#
                                                     11b = INTD#
                                                   The value advertised in the PCI configuration header is the value loaded from
                                                   NVM + 1. The default value for port 1 is 0x1.
RESERVED        31:7          0x0           RSV    Reserved.

8.2.2.5.2                 PCIe PF Device ID - PCI_PFDEVID (0x00011008)

Contains the per-PF Device ID.

      Field          Bit(s)         Init.      Type                                       Description

PF_DEV_ID_LAN         15:0       0x1562           RW   PF Device ID LAN
                                                       Contains the Device ID for this PF when the function has an Ethernet device Class
                                                       Code
PF_DEV_ID_SAN        31:16       0x1562           RW   PF Device ID SAN
                                                       Contains the Device ID for this PF when the function has a SCSI device Class
                                                       Code.

8.2.2.5.3                 PCIe VF Device ID - PCI_VFDEVID (0x00011010)

Contains the per-PF Device IDs for its VFs.

      Field          Bit(s)         Init.      Type                                       Description

VF_DEV_ID_LAN         15:0       0x1565           RW   VF Device ID LAN
                                                       Contains the device ID for this PF's VFs when the function has an Ethernet device
                                                       class code.
VF_DEV_ID_SAN        31:16       0x1565           RW   VF Device ID SAN
                                                       Contains the device ID for this PF's VFs when the function has a SCSI device class
                                                       code.

333369-009                                                                                                                              633
                                             Did this document help answer your questions?

                                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                                   Programming Interface

8.2.2.5.4                        PCIe Storage Class - PCI_CLASS (0x00011038)

Contains the per-PF configuration loaded from the NVM.

       Field       Bit(s)              Init.       Type                                         Description

STORAGE_CLASS            0               0b           RW     Storage Class
                                                              0b = The class code of this port is set to 0x020000 (LAN).
                                                              1b = The class code of this port is set to 0x010000 (SCSI).
RESERVED            31:1                 0x0          RSV    Reserved.

8.2.2.5.5                        PCIe Vendor ID - PCI_VENDORID (0x0001103C)

The Vendor ID exposed in config space. A value of 0xFFFF is not loaded to configuration space. Shared
for all PFs.

      Field     Bit(s)           Init.         Type                                           Description

VENDOR_ID       15:0         0x8086              RW     Vendor ID
                                                        Contains the Vendor ID exposed in offset 0x0 in the configuration space of all
                                                        functions. A value of 0xFFFF is ignored.
RESERVED        31:16            0x0            RSV     Reserved.

8.2.2.5.6                        PCI BAR Control - PCI_LBARCTRL (0x00011048)

        Field          Bit(s)            Init.        Type                                       Description

PREFBAR                      0            1b           RW     Prefetch BAR
                                                              Prefetchable bit indication in the memory BARs (should be set when 64-bit BARs
                                                              are used).
                                                               0b = BARs are marked as non prefetchable.
                                                               1b = BARs are marked as prefetchable.
BAR32                        1            0b           RW     BAR 32-bit Enable
                                                               0b = 64-bit BAR addressing mode is selected.
                                                               1b = 32-bit BARs are enabled.
CSRSIZE                      2            0b           RW     CSR Size
                                                              The CSRSIZE and FL_BAR_SIZE fields define the usable FLASH size and CSR
                                                              mapping window size as described in Section 9.2.2.16.
RESERVED                 5:3             001b          RSV    Reserved.
FL_BAR_SIZE              8:6             101b          RW     This field indicates the size of the external Flash as:
                                                               64KB x (2 ** FL_BAR_SIZE)
                                                              as used to define exposure in the BAR.
                                                              The following values are supported:
                                                               101b = 2 MB
                                                               110b = 4 MB
                                                               111b = 8 MB
                                                               All other values are reserved.
RESERVED                 10:9             00b          RW     Reserved.

634                                                                                                                               333369-009
                                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field           Bit(s)       Init.           Type                                     Description

EXROM_BAR_SIZE        13:11        011b             RW    EXROM BAR Size
                                                          This field indicates the size of the expansion ROM BAR as:
                                                           64KB x (2 ** EXROM_BAR_SIZE)
                                                          Values are:
                                                           000b = Corresponds to a 64 KB size.
                                                           001b = Corresponds to a 128 KB size.
                                                           010b = Corresponds to a 256 KB size.
                                                           011b = Corresponds to a 512 KB size.
                                                           100b = Corresponds to a 1 MB size.
                                                           101b = Corresponds to a 2 MB size.
                                                           110b = Corresponds to a 4 MB size.
                                                           111b = Corresponds to a 8 MB size.
                                                          Default value is 512 KB (011b).
RESERVED              31:14            0x0          RSV   Reserved.

8.2.2.5.7                PCIe Subsystem ID - PCI_SUBSYSID (0x00011058)

    Field     Bit(s)      Init.          Type                                            Description

SUB_VEN_ID     15:0      0x8086              RW      Subsystem Vendor ID
                                                     Loaded to the PCI configuration Subsystem Vendor ID Register.
SUB_ID         31:16       0x0               RW      Subsystem ID
                                                     Loaded to the PCI configuration Subsystem ID Register.

8.2.2.5.8                PCIe Power Data Register - PCI_PWRDATA (0x00011060)

     Field      Bit(s)         Init.         Type                                         Description

D0_POWER         7:0           0x0            RW      D0 Power
                                                      The value in this field is reflected in the PCI Power Management Data register of the
                                                      LAN functions for D0 power consumption and dissipation (Data_Select = 0 or 4).
COMM_POWER       15:8          0x0            RW      Comm Power
                                                      The value in this field is reflected in the PCI Power Management Data register of
                                                      function 0 when the Data_Select field is set to 8 (common function).
D3_POWER        23:16          0x0            RW      D3 Power
                                                      The value in this field is reflected in the PCI Power Management Data register of the
                                                      LAN functions for D3 power consumption and dissipation (Data_Select = 3 or 7).
RESERVED        31:24          0x0            RSV     Reserved.

8.2.2.5.9                PCIe Serial Number MAC Address High - PCI_SERH
                         (0x00011078)

    Field     Bit(s)      Init.          Type                                            Description

SER_NUM_H      15:0        0x0               RW      Serial Number High
                                                     The high Word of the Ethernet MAC Address used to generate the PCIe serial number.
RESERVED       31:16       0x0               RSV     Reserved.

333369-009                                                                                                                                635
                                             Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

8.2.2.5.10                    PCIe Capabilities Control - PCI_CAPCTRL (0x00011080)

Determines PCIe capabilities supported by the device and that software is allowed to enable or disable.

      Field     Bit(s)        Init.         Type                                         Description

VPD_EN            0             0b            RW     VPD Enable
                                                      0b = The PCIe VPD Capability is not present and is not exposed.
                                                      1b = The PCIe VPD Capability is present and exposed.
RESERVED        31:1            0x0         RSV      Reserved.

8.2.2.5.11                    PCIe Capabilities Support - PCI_CAPSUP (0x00011088)

Determines PCIe capabilities supported by the device.

        Field          Bit(s)         Init.        Type                                     Description

PCIE_VER                  0            1b          RW     PCIe Version
                                                          Determines the PCIe capability version.
                                                           0b = Capability version: 0x1
                                                           1b = Capability version: 0x2
RESERVED                  1            0b          RSV    Reserved.
LTR_EN                    2            1b          RW     LTR Enable
                                                          A value of 1b indicates support for the PCIe Latency Tolerance Reporting (LTR)
                                                          Capability.
TPH_EN                    3            1b          RW     TPH Enable
                                                          A value of 1b indicates support for the PCIe TPH Requester Capability.
ARI_EN                    4            1b          RW     ARI Enable
                                                          A value of 1b indicates support for the PCIe ARI Capability.
IOV_EN                    5            1b          RW     IOV Enable
                                                          A value of 1b indicates support for the PCIe SR-IOV Capability.
ACS_EN                    6            1b          RW     ACS Enable
                                                          A value of 1b indicates support for the PCIe ACS Capability.
SEC_EN                    7            0b          RW     SEC Enable
                                                          A value of 1b indicates support for the Secondary PCI Express Extended
                                                          Capability.
RESERVED                 14:8         0x0          RSV    Reserved.
ECRC_MCTP_GEN            15            0b          RW     ECRC Generation for MCTP
                                                           0b = Do not add ECRC to MCTP packets even if ECRC is enabled.
                                                           1b = Add ECRC to MCTP packets if ECRC is enabled via the ECRC Generation
                                                                Enable field in PCIe Advanced Error Capabilities and Control Register.
ECRC_GEN_EN              16            1b          RW     ECRC Generation Enable
                                                          Loaded into the ECRC Generation Capable bit of the PCIe Configuration
                                                          registers.
ECRC_CHK_EN              17            1b          RW     ECRC Check Enable
                                                          Loaded into the ECRC Check Capable bit of the PCIe Configuration registers.
IDO_EN                   18            1b          RW     IDO Enable
                                                          Enables ID-based ordering (IDO).
MSI_MASK                 19            1b          RW     MSI Mask
                                                          MSI per-vector masking setting. This bit is loaded to the masking bit (bit 8) in
                                                          the Message Control of the MSI Configuration Capability structure.
CSR_CONF_EN              20            1b          RW     CSP Configuration Enable
                                                          Enables Access to CSRs via the PCI Configuration Space. See Section 8.1.3.
RESERVED               29:21          0x0          RSV    Reserved.

636                                                                                                                             333369-009
                                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field        Bit(s)           Init.          Type                                     Description

LOAD_SUBSYS_ID          30            0b           RW     Load Subsystem IDs
                                                          When set to 1b, indicates that the device loads its PCIe subsystem ID and
                                                          sub-system vendor ID from NVM.
LOAD_DEV_ID             31            0b           RW     Load Device ID
                                                          When set to 1b, indicates that the device loads its PCI device IDs from NVM.

8.2.2.5.12               PCIe Link Capabilities - PCI_LINKCAP (0x00011090)

Determines PCIe Link capabilities supported by the device.

        Field            Bit(s)            Init.      Type                                    Description

LINK_SPEEDS_VECTOR           5:0            0x0         RW    Supported Link Speeds Vector
                                                              Loaded to the Link Capabilities 2 Register in the PCIe Capability.
                                                               Bit[0]    = 5.0 GT/s
                                                               Bit[1]    = 8.0 GT/s
                                                               Bits[5:2] = Reserved
                                                              Note: 2.5 GT/s is always supported.
MAX_PAYLOAD                  8:6           010b         RW    Max Payload Size Supported
                                                              Loaded to the PCIe Device Capabilities Register.
                                                              Supported values are:
                                                               000b = 128 B
                                                               001b = 256 B
                                                               010b = 512 B
                                                               011b = 1 KB
                                                               100b = 2 KB
                                                              Otherwise, keep hardware default.
MAX_LINK_WIDTH               12:9          0x07         RW    Max Link Width
                                                              Loaded to the PCIe Link Capabilities Register
                                                               0001b = Limit max link width to x1.
                                                               0011b = Limit max link width to x4.
                                                               0100b = Limit max link width to x8.
                                                               0111b = Do not limit max link width. Negotiate to the max width
                                                                         supported by the link.
                                                               All other values are reserved.
RESERVED                 31:13              0x0         RSV   Reserved.

8.2.2.5.13               PCIe PM Support - PCI_PMSUP (0x000110A0)

This register contains parameters that define PCIe power management support.

     Field      Bit(s)        Init.         Type                                          Description

RESERVED         7:0          0x97          RSV       Reserved.
L0S_ACC_LAT      10:8         011b           RW       L0s Acceptable Latency
                                                      Loaded to the Endpoint L0s Acceptable Latency field in the PCIe Device Capabilities
                                                      register.
L1_ACC_LAT      13:11         110b           RW       L1 Acceptable Latency
                                                      Loaded to the Endpoint L1 Acceptable Latency field in the PCIe Device Capabilities
                                                      register.
RESERVED         14            1b           RSV       Reserved.
RESERVED        31:15         0x0           RSV       Reserved.

333369-009                                                                                                                               637
                                            Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                             Programming Interface

8.2.2.5.14                      PCIe VF Capabilities Support - PCI_VFSUP (0x000110A8)

      Field            Bit(s)    Init.    Type                                           Description

VF_PREFETCH                 0     1b      RW       VF Prefetchable
                                                    0b = IOV memory BARs are declared as non-prefetchable.
                                                    1b = IOV memory BARs are declared as prefetchable.
RESERVED                31:1      0x0     RSV      Reserved.

8.2.2.5.15                      PCIe Global Config - PCI_GLBL_CNF (0x000110B8)

              Field             Bit(s)    Init.     Type                                      Description

RESERVED                          1:0     00b        RSV       Reserved.
WAKE_PIN_EN                        2       0b         RW       Wake Pin Enable
                                                               When set to 1b, enables the use of PE_WAKE_N pin for PME event in all
                                                               power states. Otherwise, it is enabled only in Dr state.
PCIE_CLKGATE_DIS                   3       1b         RW       PCIe Clock Gate Disable
                                                               When set to 0b, enables dynamic clock gating of the PCIe clocks (LCB, HIU
                                                               & CSR).
PCIE_CLKGATE_L1_ONLY               4       1b         RW       PCIe Clock Gate L1 Only
                                                               When set to 1b, and if PCIE_CLKGATE_DIS is 0, the clock gating of the
                                                               PCIe clocks is only when the PCIe is in L1 state.
PCIE_PCLK_GATE_EN                  5       0b         RW       PCIe PCLK Gate Enable
                                                               When set to 1b, and if PCIE_CLKGATE_DIS is 0b, the PCIe PCLK is also
                                                               dynamically gated.
RESERVED                          7:6     00b        RSV       Reserved.
PCIE_CLKGATE_TIMER               15:8     0x10        RW       PCIe Clock Gate Timer
                                                               Clock gating idle timer. This field defines the number of clocks (CSR clock)
                                                               of idle-detect before gating the PCIe clocks.
RESERVED                         31:16    0x0        RSV       Reserved.

8.2.2.5.16                      PCIe Upper Address - PCI_UPADD (0x000110E8)

This register is used to block PCIe master accesses above some address.

      Field           Bit(s)    Init.    Type                                           Description

RESERVED                0        0b      RSV      Reserved.
ADDRESS               31:1      0x0      RW       Address
                                                  Bits[31:1] correspond to Bits[63:33] in the PCIe address space, respectively.
                                                  Bits that should not be set in the addresses on the PCIe should be set in this field. For
                                                  example in a 48-bit architecture, the value of this field should be 0xFFFF0000.

8.2.2.5.17                      PCIe Serial Number MAC Address Low - PCI_SERL
                                (0x000110F0)

      Field           Bit(s)    Init.    Type                                           Description

SER_NUM_L             31:0      0x0      RW       Serial Number Low
                                                  The low DW of the Ethernet MAC Address used to generate the PCIe serial number.

638                                                                                                                            333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.5.18              PCIe Global Config 2 - PCI_CNF2 (0x000110F8)

This register contains global status fields of the PCIe configuration.

      Field       Bit(s)   Init.     Type                                     Description

RESERVED            0       0b       RSV    Reserved.
CACHELINE_SIZE      1       0b        RW    Cache Line Size
                                            Determines the system cache line size
                                             0b = 64 B
                                             1b = 128 B
                                            This field is loaded from NVM.
MSI_X_PF_N         12:2    0x3F       RW    MSI_X PF Table Size
                                            System software reads this field to determine the MSI-X Table Size N, which is
                                            encoded as N-1.
                                            This field is loaded from the NVM MSI_X_N_PF field, and reflects the same field in
                                            the PCIe MSI-X configuration (Message Control Register)
MSI_X_VF_N        23:13    0x02       RW    MSI_X VF Table Size
                                            System software reads this field to determine the MSI-X Table Size N for VFs,
                                            which is encoded as N-1.
                                            This field is loaded from the NVM MSI_X_N_VF field and reflects the same field in
                                            the PCIe MSI-X configuration (VF MSI-X Control Register).
NUM_VFS           31:24    0x40       RW    Number of VFs
                                            The number of VFs requested by the function. Valid values are 0 - 64. If value is
                                            zero, SR-IOV capability is hidden.

333369-009                                                                                                                 639
                                   Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                             Programming Interface

#### 8.2.2.6 PF - Interrupt Registers

8.2.2.6.1           Extended Interrupt Cause Register - EICR (0x00000800)

The EICR register is RW1C and can be optionally cleared on a read depending on the ODC flag setting in
the GPIE register (Section 8.2.2.6.9).

           Field       Bit(s)    Init.   Type                                  Description

RTXQ                   15:0      0x0     RW1C   Receive/Transmit Queue Interrupts
                                                One bit per queue or a bundle of queues, activated on receive/transmit
                                                events.The mapping of queue to the RTxQ bits is done by the IVAR
                                                registers.
FLOW_DIRECTOR           16        0b     RW1C   Flow Director
                                                Flow director exception is activated by one of the following events:
                                                 • Filter removal failed (there was no matched filter to be removed).
                                                 • The number of remaining free filters in the flexible filter table
                                                    exceeds (goes below) the FDIRCTRL.FULL_THRESH
                                                    (Section 8.2.2.15.1).
                                                 • Filter programming failed due to no space in the flow director table.
                                                    Note that this case should not happen if the driver handles the
                                                    FDIRCTRL.FULL_THRESH event.
RX_MISS                 17        0b     RW1C   Rx Miss
                                                Missed packet interrupt is activated for each received packet that
                                                overflows the Rx packet buffer (overrun).
PCI_EXCEPTION           18        0b     RW1C   PCI Exception
                                                The PCI exception is activated by one of the events described in Section
                                                3.1.5.8, “Proprietary Error Reporting”
                                                The specific PCI event is error reported in the PCI_ICAUSE register
                                                (Section 8.2.2.4.9).
MAILBOX                 19        0b     RW1C   Mailbox
                                                VF to PF mailbox interrupt. Caused by a VF write access to the PF
                                                mailbox or by a malicious event detection
LSC                     20        0b     RW1C   Link Status Change
                                                This bit is set each time the link status changes (either from up-to-down,
                                                or from down-to-up).
LINKSEC                 21        0b     RW1C   LinkSec
                                                Indicates that the Tx LinkSec packet counter reached the threshold
                                                requiring key exchange.
MNG                     22        0b     RW1C   Manageability Event Detected
                                                Indicates that a manageability event occurred.
                                                When the device is in power-down mode, the BMC might generate a PME
                                                for the same events that would cause an interrupt when the device is at
                                                the D0 state.
                                                This interrupt bit is also used to alert the host when the BMC IP Address
                                                was changed or when EEMNGCTL.CFG_DONE0/1 bit is set by firmware
                                                (see Section 3.7.3.4.5).
                                                It is also used to indicate ECC events in the embedded management
                                                controller memories.
TS                      23        0b     RW1C   Thermal Sensor event
                                                Indicates that a thermal sensor trip point was crossed.
TIMESYNC                24        0b     RW1C   TimeSync Interrupt
                                                Indicates that a Time Sync event has occurred. Check TSIM register for
                                                precise cause.
GPI_SDP0                25        0b     RW1C   General Purpose Interrupt on SDP0
                                                If GPI interrupt detection is enabled on this pin (via GPIE), this interrupt
                                                cause is set when a transition to high is sampled on SDP0.

640                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

           Field          Bit(s)    Init.    Type                                    Description

GPI_SDP1                    26       0b     RW1C     General Purpose Interrupt on SDP1
                                                     If GPI interrupt detection is enabled on this pin (via GPIE), this interrupt
                                                     cause is set when a transition to high is sampled on SDP1.
GPI_SDP2                    27       0b     RW1C     General Purpose Interrupt on SDP2
                                                     If GPI interrupt detection is enabled on this pin (via GPIE), this interrupt
                                                     cause is set when the SDP2 is sampled high.
ECC                         28       0b     RW1C     Unrecoverable ECC error
                                                     This bit is set when one of the following occurs:
                                                      • An unrecoverable error is detected in one of the device memories
                                                         (except embedded management controller memories).
                                                      • A CRC error occurred on the second attempt to load the PHY image
                                                         from NVM.
                                                      • PHY micro-controller watchdog failure.
                                                     Software should issue a software reset following this error.
PHY_GLOBAL_INTERRUPT        29       0b     RW1C     PHY Global Interrupt
                                                     PHY Interrupt (non-fatal).
TCP_TIMER                   30       0b     RW1C     TCP Timer Expired
                                                     This bit is set when the timer expires.
OTHER_CAUSE                 31       0b      ROS     Other Cause Interrupt
                                                     Activated when any Bit[29:16] in this register is set and its relevant
                                                     mask bit in the EIMS register (Section 8.2.2.6.5) is enabled.

8.2.2.6.2              Extended Interrupt Cause Set Register - EICS (0x00000808)

         Field           Bit(s)    Init.    Type                                    Description

INTERRUPT_CAUSE_SET      30:0      0x0      WO      Interrupt Cause Set
                                                    Setting any bit in this field, sets its corresponding bit in the EICR register
                                                    (Section 8.2.2.6.1)and generates an interrupt if enabled by the EIMS
                                                    register (Section 8.2.2.6.5).
RESERVED                  31        0b      RSV     Reserved.

8.2.2.6.3              Extended Interrupt Auto Clear Register - EIAC
                       (0x00000810)

Note:        Bits[29:16] should never be set to auto clear since they share the same MSI-X vector.

           Field          Bit(s)    Init.    Type                                    Description

RTXQ_AUTO_CLEAR            15:0      0x0     RW      RTxQ Auto-Clear
                                                      0b = The corresponding bits in the EICR register (Section 8.2.2.6.1)
                                                           are not auto-cleared.
                                                      1b = Each bit enables auto-clear of the corresponding RTxQ bits in the
                                                           EICR register following interrupt assertion.
RESERVED                  29:16      0x0     RSV     Reserved.
TCP_TIMER_AUTO_CLEAR        30       0b      RW      TCP Timer Auto-Clear
                                                      0b = Auto-clear is not enabled.
                                                      1b = This bit enables auto-clear of the TCP timer interrupt cause in the
                                                           EICR register following interrupt assertion.
RESERVED                    31       0b      RSV     Reserved.

333369-009                                                                                                                      641
                                   Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

8.2.2.6.4                  Extended Interrupt Throttle Registers - EITR[n]
                           (0x00000820 + 0x4*n, n=0...23 and 0x00012300 + 0x4*(n-
                           24), n=24...128)

Mapping of the EITR registers to the MSI-X vectors is described in Section 7.3.4.3.3, “MSI-X Vectors
Mapping to EITR”.
Note:         Additional address(es): 0x012300 + 4*(n-24), n=24...128

      Field         Bit(s)     Init.        Type                                        Description

RESERVED             2:0       000b         RSV      Reserved.
ITR_INTERVAL         11:3      0x0           RW      Interrupt Interval
                                                     Minimum inter-interrupt interval specified in 2.048 s units at 1 GbE and 10 GbE
                                                     link. At 100 Mb/s, link the interval is specified in 20.48 s units.
                                                     At 0x0, interrupt throttling is disabled while any event causes an immediate
                                                     interrupt.
RESERVED            13:12      00b          RSV      Reserved.
HIGH_PRIORITY        14         0b           RW      High Priority vector
                                                     Setting this bit causes assertion of this vector to break DMA coalescing.
RESERVED             15         0b          RSV      Reserved.
LLI_CREDIT          20:16      0x0           RW      LLI Credit
                                                     Reflects the current credits for associated interrupt. When CNT_WDIS is not set
                                                     on write cycle, this field must be set to zero.
ITR_COUNTER         27:21      0x0           RW      Interrupt Counter
                                                     This field represents the 7 MS bits (out of 9 bits) of the ITR counter. It is a down
                                                     counter that is loaded with ITR_INTERVAL value each time the associated
                                                     interrupt is asserted.
                                                     When the ITR counter reaches zero, it stops counting and triggers an interrupt.
                                                     On a write cycle, software must set this field to 0 if CNT_WDIS in this register is
                                                     cleared (write enable to the ITR counter).
RESERVED            30:28      000b         RSV      Reserved.
CNT_WDIS             31         0b           RW      Counter Write Disable
                                                     Write disable to the LLI credit and ITR counter.
                                                      0b = Software must set the LLI credit and ITR counter to zero, which enables an
                                                             immediate interrupt on packet reception.
                                                      1b = The LLI credit and ITR counter are not overwritten by the write access.
                                                     This bit is write only and always read as zero.

8.2.2.6.5                  Extended Interrupt Mask Set/Read Register - EIMS
                           (0x00000880)

        Field         Bit(s)     Init.        Type                                        Description

INTERRUPT_ENABLE       30:0       0x0         RWS      Interrupt Enable
                                                       Each bit that is set to 1b enables its corresponding interrupt in the EICR
                                                       register (Section 8.2.2.6.1).
                                                       Writing a 1b to any bit sets it. Writing 0b has no impact.
                                                       Reading this register provides a map of those interrupts that are enabled.
RESERVED                  31         0b        RSV     Reserved.

642                                                                                                                           333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.6.6                      Extended Interrupt Mask Clear Register - EIMC
                               (0x00000888)

      Field                Bit(s)         Init.         Type                                        Description

INTERRUPT_MASK               30:0         0x0             WO     Interrupt Mask
                                                                 Writing a 1b to any bit clears its corresponding bit in the EIMS register
                                                                 (Section 8.2.2.6.5), disabling the corresponding interrupt in the EICR register
                                                                 (Section 8.2.2.6.1). Writing 0b has no impact.
                                                                 Reading this register provides no meaningful data.
RESERVED                     31            0b           RSV      Reserved.

8.2.2.6.7                      Extended Interrupt Auto Mask Enable Register - EIAM
                               (0x00000890)

    Field           Bit(s)        Init.         Type                                             Description

AUTO_MASK           30:0            0x0           RW       Auto-Mask Enable
                                                           At 1b, each bit enables auto-set and auto-clear of its corresponding bits in the EIMS
                                                           register (Section 8.2.2.6.5).
                                                           Note: If any of the AUTO_MASK enable bits are set, the GPIE.EIAME bit
                                                                    (Section 8.2.2.6.9) must be set as well.
RESERVED             31             0b          RSV        Reserved.

8.2.2.6.8                      MSIX to EITR Select - EITRSEL (0x00000894)

    Field           Bit(s)        Init.         Type                                             Description

VFSELECT            31:0            0x0           RW       Virtual Function Select
                                                           Each bit ‘n’ in this register selects the VF index (32+’n’) or PF interrupt source for the
                                                           EITR registers (VF 0-31 are not multiplexed as described in Section 7.3.4.3.3, “MSI-X
                                                           Vectors Mapping to EITR”).
                                                            0b = Selects the PF.
                                                            1b = Selects the VF.

8.2.2.6.9                      General Purpose Interrupt Enable - GPIE (0x00000898)

            Field                   Bit(s)        Init.        Type                                    Description

RESERVED                              0            0b          RSV     Reserved.
SDP0_GPIEN                            1            0b          RW      General Purpose Interrupt Detection Enable for SDP0
                                                                       If software-controllable I/O pin SDP0 is configured as an input, this bit
                                                                       (when 1b) enables use for GPI interrupt detection, resulting in setting
                                                                       EICR[25] bit.
SDP1_GPIEN                            2            0b          RW      General Purpose Interrupt Detection Enable for SDP1
                                                                       If software-controllable I/O pin SDP1 is configured as an input, this bit
                                                                       (when 1b) enables use for GPI interrupt detection., resulting in setting
                                                                       EICR[26] bit
SDP2_GPIEN                            3            0b          RW      General Purpose Interrupt Detection Enable for SDP2
                                                                       If software-controllable I/O pin SDP2 is configured as an input, this bit
                                                                       (when 1b) enables use for GPI interrupt detection, resulting in setting
                                                                       EICR[27] bit

333369-009                                                                                                                                         643
                                                  Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

          Field          Bit(s)         Init.        Type                                   Description

MULTIPLE_MSIX               4            0b          RW     MSI-X Mode
                                                            Selects between MSI-X interrupts and other interrupt modes.
                                                             0b = Legacy and MSI mode (non-MSI-X mode).
                                                             1b = MSI-X mode.
OCD                         5            0b          RW     Other Clear Disable
                                                             0b = The whole EICR register is cleared on read.
                                                             1b = Only Bits[29:16] of the EICR are cleared on read.
EIMEN                       6            0b          RW     EICS Immediate Interrupt Enable
                                                             0b = The EICS interrupt waits for EITR expiration
                                                             1b = Setting bit in the EICS causes a Low Latency Interrupt.
RESERVED                   10:7         0x0          RSV    Reserved.
RSC_DELAY                13:11          000b         RW     RCS Delay
                                                            Delay from RSC completion triggered by ITR and interrupt assertion.
                                                            The delay in 1 GbE or 10 GbE mode equals:
                                                             (RSC_DELAY + 1) x 4 s = 4, 8, 12...32 s
                                                            The delay in 100 Mb/s mode equals:
                                                             (RSC_DELAY + 1) x 40 s = 40, 80, 120...320 s
VT_MODE                  15:14          00b          RW     VT Mode
                                                            Specifies the number of active Virtual functions. Software must set this
                                                            field the same as GCR_EXT.VT_MODE (Section 8.2.2.4.4).
                                                              00b = Non IOV mode.
                                                              01b = 16 VF mode.
                                                              10b = 32 VF mode.
                                                              11b = 64 VF mode.
RESERVED                 29:16          0x0          RSV    Reserved.
EIAME                      30            0b          RW     Extended Interrupt Auto Mask Enable
                                                            When set, the EIMS register can be auto-cleared (depending on EIAM
                                                            setting) upon interrupt assertion. In any case, the EIMS register can be
                                                            auto-cleared (depending on EIAM setting) following a write-to-clear (or
                                                            read) to the EICR register.
                                                            Software might set the EIAME bit only in MSI-X mode.
PBA_SUPPORT                31            0b          RW     PBA Support
                                                            When set, setting one of the extended interrupts masks via EIMS causes
                                                            the PBA bit of the associated MSI-X vector to be cleared. Otherwise, the
                                                            device behaves in a way supporting legacy INT-x interrupts.
                                                            Note: Should be cleared when working in INT-x or MSI mode and set in
                                                                    MSI-X mode.

8.2.2.6.10              Interrupt Vector Allocation Registers - IVAR[n]
                        (0x00000900 + 0x4*n, n=0...63)

These registers map interrupt causes into EICR entries (legacy/MSI modes) or into MSI-X vectors
(MSI-X modes). See Section 7.3.4 for mapping and use of these registers. Transmit and receive queues
mapping to IVAR registers is shown here:

        Field     Bit(s)        Init.         Type                                       Description

INT_ALLOC_0        5:0            X             RW     Interrupt Allocation 0
                                                       The interrupt allocation for Rx queue (‘2xN’ for IVAR register ‘N’).
RESERVED            6             0b          RSV      Reserved.
INT_ALLOC_VAL_0     7             0b            RW     Interrupt Allocation Valid 0
                                                       Interrupt allocation valid indication for INT_ALLOC[0].
INT_ALLOC_1       13:8            X             RW     Interrupt Allocation 1
                                                       The interrupt allocation for Tx queue (‘2xN’ for IVAR register ‘N’).

644                                                                                                                           333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

        Field       Bit(s)      Init.         Type                                         Description

RESERVED              14            0b          RSV      Reserved.
INT_ALLOC_VAL_1       15            0b            RW     Interrupt Allocation Valid 1
                                                         Interrupt allocation valid indication for INT_ALLOC[1].
INT_ALLOC_2          21:16           X            RW     Interrupt Allocation 2
                                                         The interrupt allocation for Rx queue (‘2xN’+1 for IVAR register ‘N’).
RESERVED              22            0b          RSV      Reserved.
INT_ALLOC_VAL_2       23            0b            RW     Interrupt Allocation Valid 2
                                                         Interrupt allocation valid indication for INT_ALLOC[2].
INT_ALLOC_3          29:24           X            RW     Interrupt Allocation 3
                                                         The interrupt allocation for Tx queue (‘2xN’+1 for IVAR register ‘N’).
RESERVED              30            0b          RSV      Reserved.
INT_ALLOC_VAL_3       31            0b            RW     Interrupt Allocation Valid 3
                                                         Interrupt allocation valid indication for INT_ALLOC[3].

8.2.2.6.11                Miscellaneous Interrupt Vector Allocation - IVAR_MISC
                          (0x00000A00)

These register maps interrupt causes into MSI-X vectors (MSI-X modes). See Section 7.3.4 for mapping
and use of these registers.
Note:        The INT_ALLOC_VAL_1 bit default value is 1b to enable legacy driver functionality.

        Field       Bit(s)      Init.         Type                                         Description

INT_ALLOC_0           6:0            X            RW     Interrupt Allocation 0
                                                         Defines the MSI-X vector assigned to the TCP timer interrupt cause.
                                                         The value must be in the 0-63 range.
INT_ALLOC_VAL_0       7             0b            RW     Interrupt Allocation Valid 0
                                                         Valid bit for INT_ALLOC[0].
INT_ALLOC_1          14:8            X            RW     Interrupt Allocation 1
                                                         Defines the MSI-X vector assigned to the “Other” interrupt cause.
                                                         The value must be in the 0-63 range.
INT_ALLOC_VAL_1       15            1b            RW     Interrupt Allocation Valid 1
                                                         Valid bit for INT_ALLOC[1].
RESERVED             31:16          0x0         RSV      Reserved.

8.2.2.6.12                Extended Interrupt Cause Set Registers 1 - EICS1
                          (0x00000A90)

          Field             Bit(s)        Init.        Type                                   Description

INTERRUPT_CAUSE_SET          31:0         0x0          WO     Interrupt Cause Set
                                                              Setting any bit in this register sets its corresponding bit in the EICR[n]
                                                              register, and generates an interrupt if enabled by the EIMS[n] register.
                                                              Reading this register provides no meaningful data.

333369-009                                                                                                                                 645
                                          Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                             Programming Interface

8.2.2.6.13            Extended Interrupt Cause Set Registers 2 - EICS2
                      (0x00000A94)

        Field             Bit(s)          Init.        Type                                   Description

INTERRUPT_CAUSE_SET         31:0           0x0          WO    Interrupt Cause Set
                                                              Setting any bit in this register sets its corresponding bit in the EICR[n]
                                                              register, and generates an interrupt if enabled by the EIMS[n] register.
                                                              Reading this register provides no meaningful data.

8.2.2.6.14            Extended Interrupt Mask Set/Read Registers - EIMS1
                      (0x00000AA0)

      Field         Bit(s)         Init.          Type                                      Description

INTERRUPT_ENABLE     31:0           0x0           RWS     Interrupt Enable
                                                          Each bit at 1b enables its corresponding interrupt in the EICR[n] register.
                                                          Writing 1b to any bit sets it. Writing 0b has no impact.
                                                          Reading this register provides a map of those interrupts that are enabled.
                                                          Bits[15:0] of EIMS1 are mirrored in EIMS Bits[15:0].

8.2.2.6.15            Extended Interrupt Mask Set/Read Registers - EIMS2
                      (0x00000AA4)

      Field         Bit(s)         Init.          Type                                      Description

INTERRUPT_ENABLE     31:0           0x0           RWS     Interrupt Enable
                                                          Each bit at 1b enables its corresponding interrupt in the EICR[n] register.
                                                          Writing 1b to any bit sets it. Writing 0b has no impact.
                                                          Reading this register provides a map of those interrupts that are enabled.
                                                          Bits[15:0] of EIMS1 are mirrored in EIMS Bits[15:0].

8.2.2.6.16            Extended Interrupt Mask Clear Registers 1 - EIMC1
                      (0x00000AB0)

      Field        Bit(s)      Init.          Type                                         Description

INTERRUPT_MASK     31:0            0x0            WO     Interrupt Mask
                                                         Writing 1b to any bit clears its corresponding bit in the EIMS[n] register,
                                                         disabling the corresponding interrupt in the EICR[n] register. Writing 0b has no
                                                         impact.
                                                         Reading this register provides no meaningful data.

8.2.2.6.17            Extended Interrupt Mask Clear Registers 2 - EIMC2
                      (0x00000AB4)

      Field        Bit(s)      Init.          Type                                         Description

INTERRUPT_MASK     31:0            0x0            WO     Interrupt Mask
                                                         Writing 1b to any bit clears its corresponding bit in the EIMS[n] register,
                                                         disabling the corresponding interrupt in the EICR[n] register. Writing 0b has no
                                                         impact.
                                                         Reading this register provides no meaningful data.

646                                                                                                                            333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.6.18             Extended Interrupt Auto Mask Enable Registers 1 - EIAM1
                       (0x00000AD0)

    Field     Bit(s)    Init.   Type                                       Description

AUTO_MASK      31:0     0x0      RW    Auto-Mask
                                       At 1b, each bit enables auto-set and auto-clear of its corresponding bits in the
                                       EIMS[n] register. Bits[15:0] of EIAM1 are mirrored in EIAM Bits[15:0].
                                       Note: If any of the AUTO_MASK enable bits is set, the GPIE.EIAME bit must be set
                                                as well.

8.2.2.6.19             Extended Interrupt Auto Mask Enable Registers 2 - EIAM2
                       (0x00000AD4)

    Field     Bit(s)    Init.   Type                                       Description

AUTO_MASK      31:0     0x0      RW    Auto-Mask
                                       At 1b, each bit enables auto-set and auto-clear of its corresponding bits in the
                                       EIMS[n] register. Bits[15:0] of EIAM1 are mirrored in EIAM Bits[15:0].
                                       Note: If any of the AUTO_MASK enable bits is set, the GPIE.EIAME bit must be set
                                                as well.

8.2.2.6.20             RSC Enable Interrupt - RSCINT[n] (0x00012000 + 0x4*n,
                       n=0...128)

    Field     Bit(s)    Init.   Type                                       Description

RSCEN            0       1b      RW    RSC Enable
                                       This bit enables RSC on the receive queues associated with interrupt vector n.
RESERVED       31:1     0x0      RSV   Reserved.

333369-009                                                                                                              647
                                 Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                     Programming Interface

#### 8.2.2.7 PF - MSI-X Table Registers

The MSI-X capability is described in Section 9.2.3.3. The MSI-X table is described in Section 9.2.3.3.4,
and the Pending Bit Array (PBA) is described in Section 9.2.3.3.5. These registers are located in the
MSI-X BAR.

8.2.2.7.1                 MSI-X PBA Clear - PBACL[n] (0x000110C0 + 0x4*n,
                          n=0...7)

Note:         PBACL[0] is also mapped to address 0x11068 to maintain compatibility with previous
              products.

      Field      Bit(s)    Init.   Type                                         Description

PENBITCLR         31:0     0x0     RW     MSI-X Pending Bits Clear
                                          Writing 1b to any bit clears it's content. Writing 0b has no effect.
                                          Reading this register returns the MSIPBA.PENBIT value.

8.2.2.7.2                 VF MSI-X PBA Clear - VFPBACL[n] (0x000110C8 + 0x4*n,
                          n=0...5)

These registers reflect the VFPBACL bits of the VFs. This PBA is a vector of 192 bits. The vector starts at
Bit[31] of register p=5 and ends at Bit[0] of register p=0 (“reverse” ordering). Each VF has 3 bits in
this vector while, PENBIT[2:0] of VF=vi are mapped to bits vi * 3... vi * 3 + 2. Explicitly, PENBIT[2] of
VF0 is at Bit[31] of register p=5, and so on.

      Field      Bit(s)    Init.   Type                                         Description

PENBITCLR         31:0     0x0     RW     MSI-X Pending Bits Clear
                                          Writing 1b to any bit clears it's content. Writing 0b has no effect.
                                          Reading this register returns the MSIPBA.PENBIT value.

648                                                                                                              333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.8 PF - Receive Registers

8.2.2.8.1                 Receive Checksum Control - RXCSUM (0x00005000)

This register controls the receive checksum off-loading features of the X550.
Note:        This register should only be initialized (written) when the receiver is not enabled. For
             example, only write this register when RXCTRL.RXEN = 0 (Section 8.2.2.9.11).

    Field       Bit(s)     Init.    Type                                        Description

RESERVED         9:0       0x0      RSV     Reserved.
ICMPV6XSUM        10        0b      RW      ICMPv6 Checksum Enable
                                             0b = Disable ICMPv6 checksum calculation.
                                             1b = Enable ICMPv6 checksum calculation.
                                            Note: ICMPv6 checksum offload is supported only for packets sent to firmware for
                                                   Proxying.
RESERVED          11        0b      RSV     Reserved.
IPPCSE            12        0b      RW      IP Payload Checksum Enable
                                            If set, a partial checksum is calculated for fragmented UDP packets.
                                            Relevant only if PCSD bit = 0b
PCSD              13        0b      RW      RSS/Fragment Checksum Status Selection
                                            The Fragment Checksum and IP Identification fields are mutually exclusive with the
                                            RSS hash. Only one of the two options is reported in the Rx descriptor.
                                             0b = The extended descriptor write-back contains the fragment checksum.
                                             1b = The extended descriptor write-back has the RSS field.
RESERVED        31:14      0x0      RSV     Reserved.

8.2.2.8.2                 Receive Filter Control Register - RFCTL (0x00005008)

     Field       Bit(s)     Init.    Type                                        Description

RESERVED           4:0       0x0     RSV     Reserved.
RESERVED           5:0       0x0     RSV     Reserved.
NFSW_DIS           6         0b      RW      NFS Write Disable
                                             Disable filtering of NFS write request headers.
NFSR_DIS           7         0b      RW      NFS Read Disable
                                             Disable filtering of NFS read reply headers.
NFS_VER            9:8       00b     RW      NFS Version
                                             NFS version recognized by hardware.
                                              00b = NFS version 2.
                                              01b = NFS version 3.
                                              10b = NFS version 4.
                                              11b = Reserved for future use.
IPV6_DIS           10        0b      RW      IPv6 Disable
                                             Disable IPv6 packet filtering.
                                             Must always be set to 0b.
IP6XSUM_DIS        11        0b      RW      IPv6 Xsum Disable
                                             Disable XSUM on IPv6 packets.
                                             Must always be set to 0b.
RESERVED          13:12      00b     RSV     Reserved.
IPFRSP_DIS         14        0b      RW      IP Fragment Split Disable
                                             When this bit is set, the header of IP fragmented packets are not set.
                                             Must always be set to 0b.

333369-009                                                                                                                   649
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                     Programming Interface

      Field       Bit(s)    Init.    Type                                        Description

RESERVED            15       0b      RSV     Reserved.
IPV6_EXDIS          16       0b      RW      IPv6 Extension Header Disable
                                             Chicken bit to disable the IPv6 extension headers parsing for XSUM offload, Header
                                             split and Filtering:
                                              0b = Parse and recognize allowed IPV6 extension headers (Hop-by-Hop,
                                                     Destination Options, and Routing).
                                              1b = Reserved.
                                             Must always be set to 0b.
RESERVED          31:17      0x0     RSV     Reserved. Should be written with 0 to ensure future compatibility.

8.2.2.8.3                  VXLAN Control - VXLANCTRL (0x0000507C)

      Field      Bit(s)    Init.    Type                                        Description

UDPPORT           15:0     0x0      RW      UDP Port
                                            Defines the UDP port used to identify VXLAN traffic.
RESERVED         31:16     0x0      RSV     Reserved.

8.2.2.8.4                  Filter Control Register - FCTRL (0x00005080)

Note:         Before receive filters are updated/modified, the RXCTRL.RXEN bit should be set to 0b (refer
              to Section 8.2.2.9.11). Once the proper filters are set, the RXCTRL.RXEN bit can be set to 1b
              to re-enable the receiver. In FCoE mode, DDP contexts should be invalidated before clearing
              RXCTRL.RXEN bit.

      Field      Bit(s)    Init.    Type                                        Description

RESERVED           0        0b      RSV     Reserved.
SBP                1        0b      RW      Store Bad Packets
                                             0b = Do not store
                                             1b = Store.
                                            Notes:
                                             1. CRC errors before the SFD are ignored. Any packet must have a valid SFD
                                                (RX_DV with no RX_ER in the XGMII/GMII i/f) to be recognized by the device
                                                (even bad packets).
                                             2. Packets with errors are not routed to manageability even if this bit is set.
                                             3. Erroneous packets might be routed to the default queue rather than the
                                                originally-intended queue.
                                             4. In packets shorter than 64 bytes, the checksum errors might be hidden while
                                                MAC errors are reported.
                                             5. Packet with Valid Error (caused by Byte Error or Illegal Error) might have data
                                                contamination in the last 8 bytes when stored in the Host memory if the SBP bit is
                                                set.
RESERVED          6:2      0x0      RSV     Reserved.
TPE                7        0b      RW      Tag Promiscuous Enable
                                            When set, any packet with active tag is accepted.
                                            The active tag to accept is defined by the PFVTCTL.POOLING_MODE field
                                            (Section 8.2.2.22.12).
                                            If the PFVTCTL.POOLING_MODE field equals:
                                              01b    = Accept all packets with E-tag.
                                              10b    = Reserved.
                                              Other = Ignore this bit.

650                                                                                                                    333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field     Bit(s)        Init.          Type                                          Description

MPE               8             0b             RW     Multicast Promiscuous Enable
                                                       0b = Disabled
                                                       1b = Enabled
                                                      When set, all received multicast and broadcast packets pass L2 filtering and can be
                                                      directed to the MNG or Host by a one of the decision filters.
UPE               9             0b             RW     Unicast Promiscuous Enable
                                                       0b = Disabled
                                                       1b = Enabled
BAM              10             0b             RW     Broadcast Accept Mode
                                                       0b = Ignore broadcast packets to Host.
                                                       1b = Accept broadcast packets to Host.
RESERVED        31:11           0x0          RSV      Reserved.

8.2.2.8.5                  E-tag EtherType Register - ETAG_ETYPE (0x00005084)

      Field     Bit(s)        Init.          Type                                          Description

ETAG_ETYPE      15:0       0x893F              RW     E-tag EtherType Value
RESERVED        30:16           0x0          RSV      Reserved.
VALID            31             0b             RW     Valid Bit
                                                       0b = Entry is disabled.
                                                       1b = Entry is enabled.

8.2.2.8.6                  VLAN Control Register - VLNCTRL (0x00005088)

        Field          Bit(s)          Init.        Type                                      Description

VET                      15:0         0x8100        RW     VLAN Ether Type (the VLAN Tag Protocol Identifier - TPID)
                                                           This register contains the type field hardware that's matched against to
                                                           recognize an 802.1Q (VLAN) Ethernet packet.
                                                           For proper operation, software must not change the default setting of this field
                                                           (802.3ac standard defines it as 0x8100).
                                                           This field must be set to the same value as the VT field in the DMATXCTL
                                                           register (Section 8.2.2.10.2).
                                                           Note: This field appears in little endian order (the upper byte is first on the
                                                                     wire (VLNCTRL.VET[15:8]).
RESERVED               26:16           0x0          RSV    Reserved.
UP_FIRST_TAG_EN          27             1b          RW     UP First Tag Enable
                                                           If set, the UP used for traffic class determination is taken from the first tag with
                                                           UP,. Otherwise, it is taken from the inner VLAN.
DEI                      28             0b          RW     Drop Eligible Indicator Bit Value
                                                           If DEIEN is set to 1b, .1q packets with DEI equal to this field are accepted.
                                                           Otherwise, the .1q packet is discarded.
DEIEN                    29             0b          RW     Drop Eligible Indicator Enable
                                                            0b = Disabled (DEI bit not compared to decide packet acceptance).
                                                            1b = Enabled (DEI from packet must match the DEI field to accept a .1q
                                                                 packet).
VFE                      30             0b          RW     VLAN Filter Enable
                                                            0b = Disabled (VFTA filter table does not decide packet acceptance).
                                                            1b = Enabled (VFTA filter table decides packet acceptance for .1q packets).
RESERVED                 31             0b          RSV    Reserved.

333369-009                                                                                                                                  651
                                               Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

8.2.2.8.7                      Multicast Control Register - MCSTCTRL (0x00005090)

      Field           Bit(s)   Init.    Type                                           Description

MO                     00b     0x0      RW       Multicast Offset
                                                 This determines which bits of the incoming multicast address are used in looking up
                                                 the bit vector.
                                                   00b = [47:36]
                                                   01b = [46:35]
                                                   10b = [45:34]
                                                   11b = [43:32]
MFE                     2       0b      RW       Multicast Filter Enable
                                                  0b = The multicast table array filter (MTA[n]) is disabled.
                                                  1b = The multicast table array (MTA[n]) is enabled.
RESERVED              31:3     0x0      RSV      Reserved.

8.2.2.8.8                      EType Queue Filter - ETQF[n] (0x00005128 + 0x4*n,
                               n=0...7)

              Field            Bit(s)    Init.     Type                                     Description

ETYPE                           15:0     0x0        RW       EtherType
                                                             Identifies the protocol running on top of IEEE 802. Used to route Rx
                                                             packets containing this EtherType to a specific Rx queue.
                                                             Note: This field is defined in Little Endian (MS byte is first on the wire).
RESERVED                        19:16    0x0        RSV      Reserved.
POOL                            25:20    0x0        RW       Pool
                                                             In virtualization modes, determines the target pool for the packet.
POOL_ENABLE                      26       0b        RW       Pool Enable
                                                             In virtualization modes, enables the Pool field.
FCOE                             27       0b        RW       FCoE
                                                             When set, packets that match this filter are identified as FCoE packets.
CNM                              28       0b        RW       CNM
                                                             When set, a packet with this EType is identified as a CNM packet.
TX_ANTISPOOF                     29       0b        RW       Transmit Anti-spoof
                                                             If set, this EtherType is candidate for anti-spoof action on transmitted
                                                             packets. The actual action applied is set according to the
                                                             PFVFSPOOF.ETHERTYPEAS or PFVFSPOOF.ETHERTYPELB (refer to
                                                             Section 8.2.2.22.19).
IEEE_1588_TIME_STAMP             30       0b        RW       IEEE 1588 Time Stamp
                                                             When set, packets with this EType are time-stamped according to the IEEE
                                                             1588 specification.
FILTER_ENABLE                    31       0b        RW       Filter Enable
                                                              0b = The filter is disabled for any functionality.
                                                              1b = The filter is enabled. Exact actions are determined by separate bits.

652                                                                                                                           333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.8.9              Multicast Table Array - MTA[n] (0x00005200 + 0x4*n,
                       n=0...127)

This table should be initialized by software before transmit and receive are enabled.

    Field     Bit(s)    Init.   Type                                        Description

BIT_VECTOR     31:0      X       RW    Bit Vector
                                       Word wide bit vector specifying 32 bits in the multicast address filter table.
                                       This device provides multicast filtering for 4096 multicast addresses by providing
                                       single bit entry per multicast address. Those 4096 address locations organized in a
                                       Multicast Table Array (128 registers of 32 bits each).
                                       Only 12 bits out of the 48-bit destination address are considered as multicast address.
                                       Those 12 bits can be selected by MO field of MCSTCTRL register (Section 8.2.2.8.7).
                                       The 7 MS bits of the Ethernet MAC Address (out of the 12 bits) selects the register
                                       index, while the 5 LS bits (out of the 12 bits) selects the bit within a register.

8.2.2.8.10             Receive Address Low - RAL_ALIAS[n] (0x00005400 +
                       0x8*n, n=0...15; RW)

These registers are aliases to the first 16 RAL addresses.
Field definitions are the same as those defined in Section 8.2.2.8.14

8.2.2.8.11             Receive Address High - RAH_ALIAS[n] (0x00005404 +
                       0x8*n, n=0...15; RW)

These registers are aliases to the first 16 RAH addresses.
Field definitions are the same as those defined in Section 8.2.2.8.15

8.2.2.8.12             Multiple Receive Queues Command Register - MRQC_ALIAS
                       (0x00005818; RW)

This is an alias to the MRQC register.
Field definitions are the same as those defined in Section 8.2.2.8.23

8.2.2.8.13             VLAN Filter Table Array - VFTA[n] (0x0000A000 + 0x4*n,
                       n=0...127)

This table should be initialized by software before transmit and receive are enabled.

    Field     Bit(s)    Init.   Type                                        Description

VLAN_FLT       31:0      X       RW    VLAN Filter
                                       Each bit ‘i’ in register ‘n’ affects packets with VLAN VID equal to 32*n+i. 128 VLAN
                                       Filter registers compose a table of 4096 bits that cover all possible VIDs.
                                       Each bit when set, allows packets with the associated VID to pass. Each bit when
                                       cleared, blocks packets with this VID.

333369-009                                                                                                                 653
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.8.14                Receive Address Low - RAL[n] (0x0000A200 + 0x8*n,
                          n=0...127)

These registers contain the lower 32 bits of the 48-bit Ethernet MAC Address. All 32 bits are valid. If the
NVM is present, the first register (RAL0) is loaded from the NVM.
Note:         The first 16 MAC Addresses are also mapped to CSR addresses 0x5400-0x5478 for backward
              compatibility.

      Field      Bit(s)   Init.   Type                                        Description

RAL               31:0     X      RW     Receive Address Low
                                         The lower 32 bits of the 48-bit Ethernet MAC Address.
                                         Note: This field is defined in Big Endian (LS byte of RAL is first on the wire).

8.2.2.8.15                Receive Address High - RAH[n] (0x0000A204 + 0x8*n,
                          n=0...127)

These registers contain the upper 16 bits of the 48-bit Ethernet MAC Address. The complete address is
{RAH, RAL}. AV determines whether this address is compared against the incoming packet. The AV
field is cleared by a master reset.
Note:         The first receive address register (RAR0) is also used for exact match pause frame checking
              (DA matches the first register). RAR0 should always be used to store the individual Ethernet
              MAC Address of the adapter. After reset, if the NVM is present, the first register (Receive
              Address Register 0) is loaded from the IA field in the NVM, its Address Select field is 00b, and
              its Address Valid field is 1b. If no NVM is present, the Address Valid field is 0b. The Address
              Valid field for all of the other registers are 0b. The first 16 MAC Addresses are also mapped to
              CSR addresses 0x5404 - 0x547C for backward compatibility.

      Field      Bit(s)   Init.   Type                                        Description

RAH               15:0     X      RW     Receive Address High
                                         The upper 16 bits of the 48-bit Ethernet MAC Address.
                                         Note: This field is defined in Big Endian (MS byte of RAH is Last on the wire).
RESERVED         29:16    0x0     RSV    Reserved.
ADTYPE             30      0b     RW     Address Type
                                          0b = MAC
                                          1b = E-tag
                                         Fixed to zero in RAH[0].
AV                 31      0b     RW     Address Valid
                                         All Receive Addresses are not initialized by hardware and software should initialize
                                         them before receive is enabled. If the NVM is present, the Receive Address[0] is
                                         loaded from the NVM and its Address Valid field is set to 1b after a software or PCI
                                         reset or NVM read.

654                                                                                                                 333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.8.16             MAC Pool Select Array - MPSAR[n] (0x0000A600 + 0x4*n,
                       n=0...255)

Software should initialize these registers before transmit and receive are enabled.

    Field     Bit(s)    Init.   Type                                        Description

POOL_ENA       31:0      X       RW    Pool Enable bit array
                                       Each couple of registers ‘2*n’ and ‘2*n+1’ are associated with Ethernet MAC Address
                                       Filter ‘n’ as defined by RAL[n] and RAH[n]. Each bit when set, enables packet
                                       reception with the associated Pools as described here:
                                         Bit ‘i’ in register ‘2*n’ is associated with POOL ‘i’.
                                         Bit ‘i’ in register ‘2*n+1’ is associated with POOL ‘32+i’.

8.2.2.8.17             Packet Split Receive Type Register - PSRTYPE[n]
                       (0x0000EA00 + 0x4*n, n=0...63)

Notes:
 • This register must be initialized by software.
 • Packets are split according to the lowest-indexed entry that applies to the packet and that is
   enabled. For example, if bits 4 and 8 are set, an IPv4 packet that is not TCP is split after the IPv4
   header. The exception to this rule is for tunnel packets. If PSR_TYPE15 (split on tunnel) or
   PSR_TYPE16 (Split on outer L2 header) is set, they take precedence on the other filters. At most
   one of those should be set.
 • This bit mask table enables or disables each type of header to be split. A value of '1'b enables an
   entry.
 • In virtualization mode, a separate PSRTYPE register is provided per pool up to the number of pools
   enabled. In non-virtualization mode, only PSRTYPE[0] is used.
 • Additional address(es): 0x05480 + 4*n, n=0... 15

    Field     Bit(s)    Init.   Type                                        Description

RESERVED        3:0     0x0      RSV   Reserved.
PSR_TYPE4        4       0b      RW    PSR Type 4
                                       Split received TCP packets after TCP header.
PSR_TYPE5        5       0b      RW    PSR Type 5
                                       Split received UDP packets after UDP header.
RESERVED        7:6     00b      RSV   Reserved.
PSR_TYPE8        8       0b      RW    PSR Type 8
                                       Split received IPv4 packets after IPv4 header.
PSR_TYPE9        9       0b      RW    PSR Type 9
                                       Split received IPv6 packets after IPv6 header.
RESERVED       11:10    00b      RSV   Reserved.
PSR_TYPE12      12       0b      RW    PSR Type 12
                                       Split received L2 packets after L2 header.
RESERVED       14:13    00b      RSV   Reserved.
PSR_TYPE15      15       0b      RW    PSR Type 15
                                       Split on tunnel header
PSR_TYPE16      16       0b      RW    PSR Type 16
                                       Split on outer L2 header
RESERVED       18:17    00b      RSV   Reserved.

333369-009                                                                                                             655
                                 Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Programming Interface

      Field      Bit(s)   Init.   Type                                       Description

RESERVED         28:19     X      RSV    Reserved.
RQPL             31:29     X      RW     Receive Queue Pool
                                         Defines the number of bits to use for RSS redirection of packets dedicated to this
                                         pool.
                                         Valid values are:
                                           000b = All the traffic of the pool is sent to queue 0 of the pool.
                                           001b = Up to 2 queues can be enabled for this pool.
                                           010b = Up to 4 queues can be enabled for this pool.
                                         The default value should be 010b.
                                         This field is used only if MRQC.MRQE equals 1001b, 1010b, 1011b, 1110b or 1111b
                                         (refer to Section 8.2.2.8.23).

8.2.2.8.18                Redirection Table - RETA[n] (0x0000EB00 + 0x4*n,
                          n=0...31)

The redirection table has 128 entries in 32 registers.
Note:         The contents of the redirection table are not defined following reset of the Memory
              Configuration Registers. System software must initialize the table prior to enabling multiple
              receive queues. It might also update the redirection table during run time. Such updates of
              the table are not synchronized with the arrival time of received packets. Therefore, it is not
              guaranteed that a table update takes effect on a specific packet boundary.

      Field      Bit(s)   Init.   Type                                       Description

ENTRY0            5:0      X      RW     Entry 0
                                         Defines the RSS output index for hash value ‘4*n+0’, where ‘n’ is the register index
                                         equal to 0...31.
RESERVED          7:6     00b     RSV    Reserved.
ENTRY1            13:8     X      RW     Entry 1
                                         Defines the RSS output index for hash value ‘4*n+1’, where ‘n’ is the register index
                                         equal to 0...31.
RESERVED         15:14    00b     RSV    Reserved.
ENTRY2           21:16     X      RW     Entry 2
                                         Defines the RSS output index for hash value ‘4*n+2’, where ‘n’ is the register index
                                         equal to 0...31.
RESERVED         23:22    00b     RSV    Reserved.
ENTRY3           29:24     X      RW     Entry 3
                                         Defines the RSS output index for hash value ‘4*n+3’, where ‘n’ is the register index
                                         equal to 0...31.
RESERVED         31:30    00b     RSV    Reserved.

656                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.8.19                       RSS Random Key Register - RSSRK[n] (0x0000EB80 +
                                 0x4*n, n=0...9)

The RSS Random Key is 40 bytes wide. See Section 7.1.3.7.3, “RSS Hash Function”.
Note:         Additional address(es): 0x05C80 + 4*n, n=0...9

     Field        Bit(s)         Init.         Type                                             Description

K0                     7:0       0x0           RW          Key 0
                                                           RSS Key Byte ‘4*n+0’ of the RSS random key, for each register ‘n’.
K1                    15:8       0x0           RW          Key 1
                                                           RSS Key Byte ‘4*n+1’ of the RSS random key, for each register ‘n’.
K2                    23:16      0x0           RW          Key 2
                                                           RSS Key Byte ‘4*n+2’ of the RSS random key, for each register ‘n’.
K3                    31:24      0x0           RW          Key 3
                                                           RSS Key Byte ‘4*n+3’ of the RSS random key, for each register ‘n’.

8.2.2.8.20                       EType Queue Select - ETQS[n] (0x0000EC00 + 0x4*n,
                                 n=0...7)

              Field                 Bit(s)          Init.       Type                                   Description

RESERVED                               15:0          0x0         RSV     Reserved.
RX_QUEUE                               22:16         0x0         RW      Receive Queue
                                                                         Identifies the Rx queue associated with this EType.
RESERVED                               30:23         0x0         RSV     Reserved.
QUEUE_ENABLE                             31           0b         RW      Queue Enable
                                                                         When set, enables queueing of Rx packets by the EType defined in the
                                                                         matching ETQF register to the queue indicated in this register.

8.2.2.8.21                       SYN Packet Queue Filter - SYNQF (0x0000EC30)

      Field             Bit(s)     Init.         Type                                            Description

QUEUE_ENABLE                 0         0b        RW          Queue Enable
                                                             When set, enables routing of Rx packets to the queue indicated in this register.
RX_QUEUE                   7:1      0x0          RW          Receive Queue
                                                             Identifies an Rx queue associated with SYN packets.
RESERVED                31:8        0x0          RSV         Reserved.

8.2.2.8.22                       RSS Queues per Traffic Class Register - RQTC (0x0000EC70)

     Field        Bit(s)         Init.         Type                                             Description

RQTC0                  2:0       100b          RW          Receive Queue Traffic Class 0
                                                           Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                                           class 0. A value of zero means that all the traffic of TC0 is sent to queue 0 of the
                                                           traffic class.
                                                           This field is used only if MRQC.MRQE = 0100b or 0101b (see Section 8.2.2.8.23).
                                                           A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED               3          0b           RSV         Reserved.

333369-009                                                                                                                                      657
                                                Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

      Field   Bit(s)   Init.   Type                                        Description

RQTC1          6:4     100b    RW     Receive Queue Traffic Class 1
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 1. A value of zero means that all the traffic of TC1 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b or 0101b (see Section 8.2.2.8.23).
                                      A value of 7 in this field is not valid and is considered as if zero is written.
RESERVED        7       0b     RSV    Reserved.
RQTC2         10:8     100b    RW     Receive Queue Traffic Class 2
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 2. A value of zero means that all the traffic of TC2 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b or 0101b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       11       0b     RSV    Reserved.
RQTC3         14:12    100b    RW     Receive Queue Traffic Class 3
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 3. A value of zero means that all the traffic of TC3 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b or 0101b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       15       0b     RSV    Reserved.
RQTC4         18:16    100b    RW     Receive Queue Traffic Class 4
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 4. A value of zero means that all the traffic of TC4 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       19       0b     RSV    Reserved.
RQTC5         22:20    100b    RW     Receive Queue Traffic Class 5
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 5. A value of zero means that all the traffic of TC5 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       23       0b     RSV    Reserved.
RQTC6         26:24    100b    RW     Receive Queue Traffic Class 6
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 6. A value of zero means that all the traffic of TC6 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       27       0b     RSV    Reserved.
RQTC7         30:28    100b    RW     Receive Queue Traffic Class 7
                                      Defines the number of bits to use for RSS redirection of packets dedicated to traffic
                                      class 7. A value of zero means that all the traffic of TC7 is sent to queue 0 of the
                                      traffic class.
                                      This field is used only if MRQC.MRQE = 0100b (see Section 8.2.2.8.23).
                                      A value of 7 (111b) in this field is not valid and is considered to be zero (000b).
RESERVED       31       0b     RSV    Reserved.

658                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.8.23             Multiple Receive Queues Command Register - MRQC
                       (0x0000EC80)

       Field         Bit(s)   Init.     Type                                    Description

MRQE                  3:0     0x0        RW    Multiple Receive Queues Enable
                                               Defines allocation of the Rx queues per RSS, virtualization, and DCB.
                                                0000b = RSS disabled.
                                                0001b = RSS only — Single set of RSS 64 queues.
                                                0010b = DCB and RSS disabled — 8 TCs, each allocated 1 queue.
                                                0011b = DCB and RSS disabled — 4 TCs, each allocated 1 queue.
                                                0100b = DCB and RSS — 8 TCs, each allocated 16 RSS queues.
                                                0101b = DCB and RSS — 4 TCs, each allocated 32 RSS queues.
                                                0110b = Reserved.
                                                0111b = Reserved.
                                                1000b = Virtualization only — 64 pools, no RSS, each pool allocated 2
                                                          queues.
                                                1001b = Virtualization and RSS — 62 pools, each allocated 2 RSS queues —
                                                          1 pool allocated 4 queues.
                                                1010b = Virtualization and RSS — 32 pools, each allocated 4 RSS queues.
                                                1011b = Virtualization and RSS — 64 pools, each allocated 2 RSS queues.
                                                1100b = Virtualization and DCB — 16 pools, each allocated 8 TCs.
                                                1101b = Virtualization and DCB — 32 pools, each allocated 4 TCs.
                                                1110b = Virtualization, DCB and RSS — 16 pools, each allocated 4 TCs, each
                                                          allocated 2 RSS queues.
                                                1111b = Virtualization and RSS — 60 pools, each allocated 2 RSS queues —
                                                          2 pools, each allocated 4 queues.
RESERVED             12:4     0x0        RSV   Reserved.
MULTIPLE_RSS          13       0b        RW    Multiple RSS Enable
                                                0b = The device uses a single RSS Key (Legacy)
                                                1b = The device uses up to 64 RSS Keys (one per pool) each RSS has a
                                                       redirection table with 64 entries of 2 bits each.
                                               This bit is relevant only if MRQE = 1001b, 1010b, 1011b, 1110b, or 1111b
RSC_DIS_LP            14       0b        RW    RSC Disable LLI & Push Coalescing
                                               If set, RSC does not coalesce packets with LLI or PSH.
L3L4TXSWEN            15       0b        RW    Enable L3/L4 filtering for Tx Switched packets
                                                0b = L3/L4 filtering (including RSS, 5-Tuples, Flow Director) is disabled.
                                                     Packets are directed to the default queue (queue 0) per pool.
                                                1b = L3/L4 filtering is enabled.
RSS_FIELD_ENABLE     31:16    0x0        RW    RSS Field Enable
                                               Each bit, when set, enables a specific field selection to be used by the hash
                                               function.
                                               Several bits can be set at the same time.
                                                 Bit[16]      = Enable TcpIPv4 hash function.
                                                 Bit[17]      = Enable IPv4 hash function.
                                                 Bit[18]      = Reserved.
                                                 Bit[19]      = Reserved.
                                                 Bit[20]      = Enable IPv6 hash function.
                                                 Bit[21]      = Enable TcpIPv6 hash function.
                                                 Bit[22]      = Enable UdpIPV4.
                                                 Bit[23]      = Enable UdpIPV6.
                                                 Bit[24]      = Reserved.
                                                 Bits[31:25] = Reserved. Zero.
                                               Note: On Tunnel packets IPv4-IPv6, only the IPv4 header might be used for
                                                         the RSS filtering.

333369-009                                                                                                                   659
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Programming Interface

8.2.2.8.24                Extended Redirection Table - ERETA[n] (0x0000EE80 +
                          0x4*n, n=0...95)

The extended redirection table adds 384 entries to extend RETA in 96 registers.
Note:         The contents of the extended redirection table are not defined following reset of the Memory
              Configuration Registers. System software must initialize the Table prior to enabling multiple
              receive queues. It might also update the redirection table during run time. Such updates of
              the table are not synchronized with the arrival time of received packets. Therefore, it is not
              guaranteed that a table update takes effect on a specific packet boundary.

      Field      Bit(s)   Init.   Type                                       Description

ENTRY0            5:0      X      RW     Entry 0
                                         Defines the RSS output index for hash value ‘4*[n+32]’, where ‘n’ is the register
                                         index equal to 0...95.
RESERVED          7:6     00b     RSV    Reserved.
ENTRY1            13:8     X      RW     Entry 1
                                         Defines the RSS output index for hash value ‘4*[n+32]+1’, where ‘n’ is the register
                                         index equal to 0...95.
RESERVED         15:14    00b     RSV    Reserved.
ENTRY2           21:16     X      RW     Entry 2
                                         Defines the RSS output index for hash value ‘4*[n+32]+2’, where ‘n’ is the register
                                         index equal to 0...95.
RESERVED         23:22    00b     RSV    Reserved.
ENTRY3           29:24     X      RW     Entry 3
                                         Defines the RSS output index for hash value ‘4*[n+32]+3’, where ‘n’ is the register
                                         index equal to 0...95.
RESERVED         31:30    00b     RSV    Reserved.

8.2.2.8.25                Per-Pool RSS Random Key Register - VFRSSRK[n,m]
                          (0x00018000 + 0x4*n + 0x40*m, n=0...15, m=0...63)

The RSS Random Key is 40 bytes wide.
Note:         Only the 10 first registers in each VF array are implemented (0x00 - 0x24).

      Field      Bit(s)   Init.   Type                                       Description

K0                7:0     0x0     RW     Key 0
                                         RSS Key Byte ‘4*n+0’ of the RSS random key, for each register ‘n’.
K1                15:8    0x0     RW     Key 1
                                         RSS Key Byte ‘4*n+1’ of the RSS random key, for each register ‘n’.
K2               23:16    0x0     RW     Key 2
                                         RSS Key Byte ‘4*n+2’ of the RSS random key, for each register ‘n’.
K3               31:24    0x0     RW     Key 3
                                         RSS Key Byte ‘4*n+3’ of the RSS random key, for each register ‘n’.

660                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.8.26               Per-Pool Redirection Table - VFRETA[n,m] (0x00019000 +
                         0x4*n + 0x40*m, n=0...15, m=0...63)

The redirection table has 64 entries in 16 registers.
Note:        The content of the redirection tables are not defined following reset of the Memory
             Configuration registers. System software must initialize the table prior to enabling multiple
             receive queues. It might also update the redirection table during run time. Such updates of
             the table are not synchronized with the arrival time of received packets. Therefore, it is not
             guaranteed that a table update takes effect on a specific packet boundary.

    Field       Bit(s)   Init.   Type                                       Description

ENTRY0           1:0      X      RW     Entry 0
                                        Defines the RSS output index for hash value ‘4*n+0’, where ‘n’ is the register index
                                        equal to 0...31.
RESERVED         7:2     0x0     RSV    Reserved.
ENTRY1           9:8      X      RW     Entry 1
                                        Defines the RSS output index for hash value 4*n+1’, where ‘n’ is the register index
                                        equal to 0...31.
RESERVED        15:10    0x0     RSV    Reserved.
ENTRY2          17:16     X      RW     Entry 2
                                        Defines the RSS output index for hash value ‘4*n+2’, where ‘n’ is the register index
                                        equal to 0...31.
RESERVED        23:18    0x0     RSV    Reserved.
ENTRY3          25:24     X      RW     Entry 3
                                        Defines the RSS output index for hash value ‘4*n+3’, where ‘n’ is the register index
                                        equal to 0...31.
RESERVED        31:26    0x0     RSV    Reserved.

333369-009                                                                                                                 661
                                  Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                    Programming Interface

#### 8.2.2.9 PF - Receive DMA Registers

8.2.2.9.1                 Receive Descriptor Base Address Low - RDBAL[n]
                          (0x00001000 + 0x40*n, n=0...63 and 0x0000D000 +
                          0x40*(n-64), n=64...127)

This register contains the lower 32 bits of the 64-bit descriptor base address. The lower 7 bits are
always ignored. The Receive Descriptor Base Address must point to a 128-byte aligned block of data.

      Field      Bit(s)    Init.   Type                                         Description

ZERO              6:0      0x0     RW     Zero
                                          Ignored on writes. Returns 0 on reads. Bits[6:0]
RDBAL            31:7       X      RW     Receive Descriptor Base Address Low
                                          Bits[31:7]

8.2.2.9.2                 Receive Descriptor Base Address High - RDBAH[n]
                          (0x00001004 + 0x40*n, n=0...63 and 0x0000D004 +
                          0x40*(n-64), n=64...127)

This register contains the upper 32 bits of the 64-bit descriptor base address.

      Field      Bit(s)    Init.   Type                                         Description

RDBAH            31:0       X      RW     Receive Descriptor Base Address High
                                          Bits[63:32]

8.2.2.9.3                 Receive Descriptor Length - RDLEN[n] (0x00001008 +
                          0x40*n, n=0...63 and 0x0000D008 + 0x40*(n-64),
                          n=64...127)

Note:         Additional address(es): 0x0D008 + 0x40*(n-64), n=64...127

      Field      Bit(s)    Init.   Type                                         Description

LEN              19:0      0x0     RW     Descriptor Ring Length
                                          This register sets the number of bytes allocated for descriptors in the circular
                                          descriptor buffer. It must be 128-byte aligned (7 LS bits must be set to zero).
                                          Note: Validated lengths up to 512 K (32 K descriptors).
RESERVED         31:20     0x0     RSV    Reserved. Reads as 0. Should be written to 0 for future compatibility.

8.2.2.9.4                 Receive Descriptor Head - RDH[n] (0x00001010 + 0x40*n,
                          n=0...63 and 0x0000D010 + 0x40*(n-64), n=64...127)

Note:         Additional address(es): 0x0D010 + 0x40*(n-64), n=64...127

      Field      Bit(s)    Init.   Type                                         Description

RDH              15:0      0x0     RO     Receive Descriptor Head
                                          This register holds the head pointer for the receive descriptor buffer in descriptor
                                          units (16-byte datum). The RDH is controlled by hardware.
RESERVED         31:16     0x0     RSV    Reserved. Should be written with 0.

662                                                                                                                   333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.9.5                  Split Receive Control Registers - SRRCTL[n] (0x00001014 +
                           0x40*n, n=0...63 and 0x0000D014 + 0x40*(n-64),
                           n=64...127)

Note:         BSIZEHEADER must be bigger than 0 if DESCTYPE is equal to 010, 011 100 or 101.
              Additional address(es): 0x0D014 + 0x40*(n-64), n=64...127 / 0x02100 + 4*n, [n=0...15]

      Field       Bit(s)    Init.    Type                                         Description

BSIZEPACKET         4:0      0x2     RW      Receive Buffer Size for Packet Buffer
                                             The value is in 1-KB resolution. Value can be from 1 KB to 16 KB. Default buffer size
                                             is 2 KB.
                                             This field should not be set to 0. This field should be greater or equal to 2 in queues
                                             which RSC is enabled.
RESERVED            7:5     000b     RSV     Reserved. Should be written with 0 to ensure future compatibility.
BSIZEHEADER        13:8      0x4     RW      Receive Buffer Size for Header Buffer
                                             The value is in 64-byte resolution. Value can be from 64 bytes to 1024 bytes.
                                             The max supported header size is limited to 1023. Default buffer size is 256 bytes.
                                             This field must be greater than 0 if the value of DESCTYPE is greater than or equal to
                                             2. Values above 1024 bytes are reserved for internal use only.
RESERVED          21:14      0x0     RSV     Reserved.
RDMTS             24:22     000b     RW      Receive Descriptor Minimum Threshold Size
                                             An interrupt associated with this queue is asserted whenever the number of free
                                             descriptors is decreased to RDMTS * 64 (this event is considered as Rx ring buffer
                                             “almost empty”).
DESCTYPE          27:25     000b     RW      Descriptor Type
                                             Defines the descriptor type in Rx
                                              000b = Legacy
                                              001b = Advanced descriptor one buffer
                                              010b = Advanced descriptor header splitting
                                              011b = Reserved.
                                              100b = Reserved.)
                                              101b = Advanced descriptor header splitting always use header buffer.
                                              110b = Reserved.
                                              111b = Reserved.
DROP_EN             28       0b      RW      Drop Enabled
                                             If set to 1b, packets received to the queue when no descriptors are available to store
                                             them are dropped.
RESERVED          31:29     000b     RSV     Reserved. Should be written with 0 to ensure future compatibility.

8.2.2.9.6                  Receive Descriptor Tail - RDT[n] (0x00001018 + 0x40*n,
                           n=0...63 and 0x0000D018 + 0x40*(n-64), n=64...127)

Note:         Software should write an even number to the tail register, if the Packet Split feature is used.
              The tail pointer should be set to one descriptor beyond the last empty descriptor in Host
              Descriptor Ring. Additional address(es): 0x0D018 + 0x40*(n-64), n=64...127.

      Field      Bit(s)    Init.    Type                                         Description

RDT               15:0     0x0      RW      Receive Descriptor Tail
                                            This register contains the tail pointer for the receive descriptor buffer. The register
                                            points to a 16-byte datum. Software writes the tail register to add receive descriptors
                                            to the hardware free list for the ring.
RESERVED         31:16     0x0      RSV     Reserved. Reads as 0. Should be written to 0 for future compatibility.

333369-009                                                                                                                       663
                                     Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.9.7                 Receive Descriptor Control - RXDCTL[n] (0x00001028 +
                          0x40*n, n=0...63 and 0x0000D028 + 0x40*(n-64),
                          n=64...127)

Note:         Additional address(es): 0x0D028 + 0x40*(n-64), n=64...127

      Field      Bit(s)   Init.   Type                                         Description

RLPML            13:0     0x0     RW     Long Packet Size Filter
                                         Defined in bytes. Packets larger than the RLPML are discarded. The filter is enabled by
                                         the RLMPL_EN bit in this register. This field might not be supported per Rx queue in
                                         future products.
                                         Notes:
                                           1. The device closes active RSC flows when an LLI packet was dropped due to
                                              RLPML exceeded.
                                           2. The packet size compared to RLMPL includes any optional timestamp added into
                                              the packet.
RESERVED          14       0b     RSV    Reserved. Software might Read and Write maintaining backward compatibility.
RLPML_EN          15       0b     RW     Enable Long Packet Size Filter
                                          0b = Disable
                                          1b = Enable
RESERVED         22:16    0x0     RSV    Reserved. Software might Read and Write maintaining backward compatibility.
RESERVED         24:23    00b     RSV    Reserved.
ENABLE            25       0b     RW     Receive Queue Enable
                                         When set, the ENABLE bit enables the operation of the specific receive queue. On
                                         read, gets the actual status of the queue (internal indication that the queue is actually
                                         enabled/disabled).
RESERVED         29:26    0x0     RSV    Reserved.
VME               30       0b     RW     VLAN Mode Enable
                                          0b = Do not strip VLAN tag.
                                          1b = Strip VLAN tag from received 802.1Q packets destined to this queue.
RESERVED          31       0b     RSV    Reserved.

8.2.2.9.8                 RSC Control - RSCCTL[n] (0x0000102C + 0x40*n, n=0...63
                          and 0x0000D02C + 0x40*(n-64), n=64...127)

Note:         Additional address(es): 0x0D02C + 0x40*(n-64), n=64...127

      Field      Bit(s)   Init.   Type                                         Description

RSCEN              0       0b     RW     RSC Enable
                                         When the RSCEN bit is set, RSC is enabled on this queue.
RESERVED           1       0b     RSV    Reserved.
MAXDESC           3:2     00b     RW     Maximum Descriptors
                                         Maximum descriptors per large receive as follows:
                                          00b = Maximum of 1 descriptor per Large Receive.
                                          01b = Maximum of 4 descriptors per Large Receive.
                                          10b = Maximum of 8 descriptors per Large Receive.
                                          11b = Maximum of 16 descriptors per Large Receive.
                                         Note: MAXDESC * SRRCTL.BSIZEPACKET must not exceed 64 KB minus 1 (which is
                                                the maximum total length in the IP header), and must be larger than
                                                expected received MSS.
RESERVED         31:4     0x0     RSV    Reserved.

664                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.9.9                  Split Receive Control Registers - SRRCTL_ALIAS[n]
                           (0x00002100 + 0x4*n, n=0...15; RW)

Field definitions are the same as those defined in Section 8.2.2.9.5.

8.2.2.9.10                 Receive DMA Control Register - RDRXCTL (0x00002F00)

         Field            Bit(s)     Init.     Type                                        Description

RESERVED                   1:0       00b        RSV       Reserved.
PSP                         2         0b        RW        Pad Small Receive Packets
                                                          If this field is set, in virtualized operating mode, strip CRC
                                                          (HLREG0.RXCRCSTRP) should be set.
DMAIDONE                    3         0b        RO        DMA Initialization Done
                                                          When read as 1 indicates that the DMA initialization cycle is done (RO).
RESERVED                    4         0b        RSV       Reserved.
RSC_PUSH_DIS                5         0b        RW        RSC Push Disable
                                                          Disable coalescing of packets with PUSH flag asserted.
RESERVED                   7:6       00b        RSV       Reserved.
TPH_AUTOLEARN               8         0b        RSV       TPH hints auto learn
                                                          If set, the device learns the CPUID value in this register from the completer
                                                          ID in read completion of receive descriptors fetch.
                                                          Note: If TPH is disabled, this bit should not be set, as the learn capability
                                                                    is independent of the TPH capability.
RESERVED                  27:9      0x30044     RSV       Reserved. Must be set to 0x30044.
MBINTEN                    28         0b        RW        Malicious Behavior Interrupt Enable for DMA Rx errors.
                                                           0b = Disabled
                                                           1b = Enabled
MDP_EN                     29         0b        RW        Malicious Driver Protection Enable for DMA Rx
                                                           0b = Mechanism is disabled.
                                                           1b = Mechanism is enabled.
RESERVED                  31:30      00b        RSV       Reserved.

8.2.2.9.11                 Receive Control Register - RXCTRL (0x00003000)

      Field      Bit(s)     Init.    Type                                             Description

RXEN               0         0b       RW      Receive Enable
                                              When set to 0, packets are not received.
RESERVED         31:1       0x0       RSV     Reserved.

333369-009                                                                                                                           665
                                       Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                              Programming Interface

8.2.2.9.12             Receive Packet Buffer Size - RXPBSIZE[n] (0x00003C00 +
                       0x4*n, n=0...7)

      Field   Bit(s)   Init.   Type                                       Description

RESERVED       9:0      0x0    RSV    Reserved.
SIZE          19:10    0x180   RW     Size
                                      Receive packet buffer size for traffic class ‘n’, where ‘n’ is the register index.
                                      The size is defined in KB units, and the default size of PB[0] is 384 KB. The default
                                      size of PB[1-7] is also 384 KB, but it is meaningless in non-DCB mode.
                                      When DCB mode is enabled, the size of PB[1-7] must be set to meaningful values.
                                      The total meaningful allocated PB sizes plus the size allocated to the flow director
                                      filters should be equal to 384 KB.
                                      Possible PB allocation in DCB mode for 8 x TCs is 0x30 (48 KB) for all PBs. Other
                                      possible setting of 4 x TCs is 0x60 (96 KB) for all PB[0-3], and 0x0 for PB[4-7].
                                      Section 3.7.4.3.5, “Packet Buffer Size” for other optional settings with/without the
                                      flow director filters.
                                      Note: In any setting the RXPBSIZE[0] must always be enabled (greater than zero).
                                      Default value is 0x180 (384 KB).
RESERVED      31:20     0x0    RSV    Reserved.

666                                                                                                            333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.10 PF - Transmit Registers

8.2.2.10.1                  Tx Packet Buffer Threshold - TXPBTHRESH[n] (0x00004950
                            + 0x4*n, n=0...7)

     Field    Bit(s)         Init.         Type                                         Description

THRESH          9:0          0x96          RW      Threshold
                                                   Used for checking room in the Tx packet buffer of TCn.
                                                   Threshold is in KB units. When the packet buffer is filled up with payload over that
                                                   threshold, no more data read requests are sent.
                                                   Default values:
                                                     0x0    = (0 KB) for TXPBSIZE1-7.
                                                     0x96 = (150 KB) for TXPBSIZE0.
                                                   It should be set to: Packet Buffer Size - MSS
                                                   For example, if the packet buffer size is set to 20 KB in the corresponding
                                                   TXPBSIZE.SIZE field, and if an MSS of 9.5 KB Jumbo frames is supported for TCn, it is
                                                   set to 0xA (10 KB).
RESERVED       31:10         0x0           RSV     Reserved.

8.2.2.10.2                  DMA Tx Control - DMATXCTL (0x00004A80)

      Field       Bit(s)         Init.        Type                                        Description

TE                     0             0b          RW    Transmit Enable
                                                       When set, this bit enables the transmit operation of the DMA-Tx.
RESERVED              2:1          10b           RSV   Reserved.
GDV                    3             0b          RW    Global Double VLAN mode
                                                       When set, this bit enables the Double VLAN mode. Should be set to the same
                                                       value as CTRL_EXT.EXTENDED_VLAN (Section 8.2.2.1.3).
RESERVED               4             1b          RSV   Reserved.
MDP_EN                 5             0b          RW    Malicious Driver Protection Enable for DMA Tx
                                                        0b = Mechanism is disabled.
                                                        1b = Mechanism is enabled.
MBINTEN                6             0b          RW    Malicious Behavior Interrupt Enable for DMA Tx errors
                                                        0b = Disabled
                                                        1b = Enabled
TPH_AUTOLEARN          7             0b          RW    TPH Hints Auto-Learn
                                                       If set, the device learns the CPUID value in this register from the completer ID in
                                                       read completion of transmit descriptors fetch.
                                                       Note: If TPH is disabled, this bit should not be set, as the learn capability is
                                                                 independent of the TPH capability.
RESERVED              15:8           0x0         RSV   Reserved.
VT                31:16         0x8100           RW    VLAN Type
                                                       VLAN Ether-Type (the VLAN Tag Protocol Identifier - TPID). For proper operation,
                                                       software must not change the default setting of this field (802.3ac standard
                                                       defines it as 0x8100).
                                                       This field must be set to the same value as the VET field in the VLNCTRL register
                                                       (Section 8.2.2.8.6).

333369-009                                                                                                                             667
                                            Did this document help answer your questions?

                                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                                Programming Interface

8.2.2.10.3                  DMA Tx TCP Flags Control Low - DTXTCPFLGL (0x00004A88)

This register holds the “mask” bits for the TCP flags in Tx segmentation (described in Section 7.2.4.7.1
and Section 7.2.4.7.2).

         Field             Bit(s)        Init.        Type                                     Description

TCP_FLG_FIRST_SEG           11:0         0xFF6         RW      TCP Flags first Segment
                                                               Bits that make AND operation with the TCP flags at TCP header in the first
                                                               segment.
RESERVED                   15:12          0x0         RSV      Reserved.
TCP_FLG_MID_SEG            27:16         0xFF6         RW      TCP Flags Middle Segments
                                                               The low bits that make AND operation with the TCP flags at TCP header in the
                                                               middle segments.
RESERVED                   31:28          0x0         RSV      Reserved.

8.2.2.10.4                  DMA Tx TCP Flags Control High - DTXTCPFLGH
                            (0x00004A8C)

This register holds the “mask” bits for the TCP flags in Tx segmentation (described in
Section 7.2.4.7.3).

        Field           Bit(s)         Init.        Type                                      Description

TCP_FLG_LST_SEG           11:0         0xF7F        RW       TCP Flags Last Segment
                                                             Bits that make AND operation with the TCP flags at TCP header in the last
                                                             segment.
RESERVED                31:12          0x0          RSV      Reserved.

8.2.2.10.5                  Transmit Descriptor Base Address Low - TDBAL[n]
                            (0x00006000 + 0x40*n, n=0...127)

This register contains the lower 32 bits of the 64-bit descriptor base address. The lower 7 bits are
ignored. The Transmit Descriptor Base Address must point to a 128-byte aligned block of data.

      Field      Bit(s)      Init.         Type                                            Description

ZERO              6:0            0x0           RW     Zero
                                                      Ignored on writes. Returns 0 on reads. Bits[6:0]
TDBAL            31:7            X             RW     Transmit Descriptor Base Address Low
                                                      Bits[31:7]

8.2.2.10.6                  Transmit Descriptor Base Address High - TDBAH[n]
                            (0x00006004 + 0x40*n, n=0...127)

This register contains the upper 32 bits of the 64-bit descriptor base address.

      Field      Bit(s)      Init.         Type                                            Description

TDBAH            31:0            X             RW     Transmit Descriptor Base Address High
                                                      Bits[63:32]

668                                                                                                                             333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.10.7                Transmit Descriptor Length - TDLEN[n] (0x00006008 +
                          0x40*n, n=0...127)

      Field      Bit(s)    Init.    Type                                         Description

LEN             19:0      0x0      RW      Descriptor Ring Length
                                           This register sets the number of bytes allocated for descriptors in the circular
                                           descriptor buffer. It must be 128-byte aligned (7 LS bit must be set to zero).
                                           Note: Validated Lengths up to 512 K (32 K descriptors).
RESERVED        31:20     0x0      RSV     Reserved. Reads as 0. Should be written to 0.

8.2.2.10.8                Transmit Descriptor Head - TDH[n] (0x00006010 + 0x40*n,
                          n=0...127)

Note:         The values in these registers might point to descriptors that are still not in the host memory.
              As a result, the host cannot rely on these values to determine which descriptor to release.
Note:         The only time that software should write to this register is after a reset (hardware reset or
              CTRL.RST) and before enabling the transmit function (TXDCTL.ENABLE). If software were to
              write to this register while the transmit function was enabled, the on-chip descriptor buffers
              might be invalidated and hardware could become confused.

      Field      Bit(s)    Init.    Type                                         Description

TDH               15:0     0x0      RO     Transmit Descriptor Head
                                           This register contains the head pointer for the transmit descriptor ring. It points to a
                                           16-byte datum. Hardware controls this pointer.
RESERVED         31:16     0x0      RSV    Reserved. Should be written with 0.

8.2.2.10.9                Transmit Descriptor Tail - TDT[n] (0x00006018 + 0x40*n,
                          n=0...127)

Note:         Hardware attempts to transmit all packets referenced by descriptors between head and tail.

      Field      Bit(s)    Init.    Type                                         Description

TDT               15:0     0x0      RW     Transmit Descriptor Tail
                                           This register contains the tail pointer for the transmit descriptor ring. It points to a
                                           16B datum. Software writes the tail pointer to add more descriptors to the transmit
                                           ready queue.
RESERVED         31:16     0x0      RSV    Reserved. Reads as 0. Should be written to 0 for future compatibility.

333369-009                                                                                                                        669
                                     Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                     Programming Interface

8.2.2.10.10               Transmit Descriptor Control - TXDCTL[n] (0x00006028 +
                          0x40*n, n=0...127)

This register controls the fetching and write back of transmit descriptors. The three threshold values are
used to determine when descriptors are read from and written to host memory. For PTHRESH and
HTHRESH recommended settings, see Section 7.2.3.4, “Transmit Descriptor Fetching”.
Note:         When WTHRESH = 0b, only descriptors with the RS bit set are written back.

      Field      Bit(s)   Init.   Type                                          Description

PTHRESH           6:0     0x0     RW     Pre-Fetch Threshold
                                         Controls when a pre-fetch of descriptors is considered.
                                         This threshold refers to the number of valid, unprocessed transmit descriptors are in
                                         the on-chip buffer. If this number drops below PTHRESH, the algorithm considers pre-
                                         fetching descriptors from host memory. However, this fetch does not happen unless
                                         there are at least HTHRESH valid descriptors in host memory to fetch.
                                         Note: HTHRESH should be given a non-zero value each time PTHRESH is used.
RESERVED           7       0b     RSV    Reserved.
HTHRESH           14:8    0x0     RW     Host Threshold
RESERVED          15       0b     RSV    Reserved.
WTHRESH          22:16    0x0     RW     Write-Back Threshold
                                         Controls the write back of processed transmit descriptors.
                                         This threshold refers to the number of transmit descriptors in the on-chip buffer that
                                         are ready to be written back to host memory. In the absence of external events
                                         (explicit flushes), the write back occurs only after at least WTHRESH descriptors are
                                         available for write back.
                                         Notes:
                                          1. Since the default value for a write-back threshold is 0b, descriptors are normally
                                             written back as soon as they are processed. WTHRESH must be written to a non-
                                             zero value to take advantage of the write back bursting capabilities.
                                          2. When WTHRESH is set to a non-zero value, the software device driver should not
                                             set the RS bit in the Tx descriptors. When WTHRESH is set to zero, the software
                                             device driver should set the RS bit in the last Tx descriptors of every packet (if
                                             TSO is the last descriptor of the entire large send).
                                          3. When head write back is enabled (TDWBAL[n].HEAD_WB_EN = 1b), the
                                             WTHRESH must be set to zero (refer to Section 8.2.2.10.11).
RESERVED         24:23    00b     RSV    Reserved.
ENABLE            25       0b     RW     Transmit Queue Enable
                                         When set, this bit enables the operation of a specific transmit queue. The default
                                         value for all queues is 0b.
                                         Setting this bit initializes all the internal registers of a specific queue. Until then, the
                                         state of the queue is kept and can be used for debug purposes. When disabling a
                                         queue, this bit is cleared only after all activity at the queue stopped.
                                         Note:
                                          1. When setting the global Tx enable DMATXCTL.TE, the Enable bit of Tx queue zero
                                             is enabled as well (refer to Section 8.2.2.10.2).
                                          2. Following a write cycle by software, this bit is set by hardware only when the
                                             queue is actually enabled. When read, gets the actual status of the queue
                                             (internal indication that the queue is actually enabled/disabled).
SWFLSH            26       0b     RW     Transmit Software Flush
                                         This bit enables software to trigger descriptor write-back flushing, independent of
                                         other conditions. This bit is self-cleared by hardware.
RESERVED         31:27    0x0     RSV    Reserved.

670                                                                                                                      333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.10.11                 Tx Descriptor Completion Write Back Address Low -
                            TDWBAL[n] (0x00006038 + 0x40*n, n=0...127)

     Field       Bit(s)       Init.     Type                                        Description

HEAD_WB_EN          0          0b        RW     Head Write-Back Enable
                                                 0b = Head write-back is disabled.
                                                 1b = Head write-back is enabled.
                                                When HEAD_WB_EN is set, Tx descriptors are not written back.
RESERVED            1          0b       RSV     Reserved.
HEADWB_LOW        31:2        0x0        RW     Head Write-Back Low
                                                Lowest 32 bits of the head write-back memory location (DWORD aligned). The last
                                                two bits of this field are ignored and are always read as 00b, meaning that the actual
                                                address is QWORD aligned.

8.2.2.10.12                 Tx Descriptor Completion Write Back Address High -
                            TDWBAH[n] (0x0000603C + 0x40*n, n=0...127)

     Field         Bit(s)      Init.     Type                                        Description

HEADWB_HIGH        31:0         0x0       RW     Head Write-Back High
                                                 Highest 32 bits of Head write-back memory location (for 64-bit addressing).

8.2.2.10.13                 DMA Tx TCP Max Allow Size Requests - DTXMXSZRQ
                            (0x00008100)

This register limits the total number of data bytes that might be in outstanding PCIe requests from the
host memory. This allows requests to send low latency packets to be serviced in a timely manner, as
this request is serviced right after the current outstanding requests are completed.

         Field              Bit(s)     Init.    Type                                     Description

MAX_BYTES_NUM_REQ           11:0       0x10      RW     Max Allowed Number of Bytes Requests
                                                        The maximum allowed amount of 256 bytes outstanding requests. If the
                                                        total size request is higher than the amount in the field, no arbitration is
                                                        done and no new packet is requested.
RESERVED                    31:12      0x0      RSV     Reserved.

8.2.2.10.14                 Multiple Transmit Queues Command Register - MTQC
                            (0x00008120)

Note:        For permitted value and functionality of DCB_ENA, VT_ENA, and NUM_TC_OR_Q. For Tx
             queue assignment in DCB and VT modes, see Table 7-28 on page 420.
Note:        This register can be modified only as part of the initialization phase.

     Field         Bit(s)      Init.     Type                                        Description

DCB_ENA                 0       0b        RW     DCB Enabled Mode
VT_ENA                  1       0b        RW     Virtualization Enabled Mode
                                                 When set, the device supports either 16, 32, or 64 Pools. This bit should be set the
                                                 same as PFVTCTL.VT_ENA (Section 8.2.2.22.12).
NUM_TC_OR_Q         3:2         00b       RW     Number of TCs or Number of Tx Queues per Pools
                                                 See functionality in Section 7.2.1.2.1, “Tx Queues Assignment”.

333369-009                                                                                                                             671
                                        Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Programming Interface

       Field      Bit(s)         Init.          Type                                          Description

RESERVED           31:4           0x0           RSV        Reserved.

8.2.2.10.15                Transmit Packet Buffer Size - TXPBSIZE[n] (0x0000CC00 +
                           0x4*n, n=0...7)

      Field     Bit(s)      Init.          Type                                             Description

RESERVED         9:0            0x0        RSV         Reserved.
SIZE            19:10       0xA0               RW      Size
                                                       Transmit packet buffer size of TCn. At default (no DCB), only packet buffer 0 is
                                                       enabled and TXPBSIZE values for TC 1-7 are meaningless.
                                                       Other than the default configuration, the X550 supports partitioned configurations
                                                       when DCB is enabled.
                                                       Symmetrical 8 TCs partitioning: 0x14 (20KB) for TXPBSIZE[0...7].
                                                       Symmetrical 4 TCs partitioning: 0x28 (40KB) for TXPBSIZE[0...3] and 0x0 (0KB) for
                                                       TXPBSIZE[4...7].
                                                       Non-symmetrical partitioning are supported as well. To enable wire speed
                                                       transmission, it is recommended to set the transmit packet buffers to:
                                                         • At least 2 times MSS plus PCIe latency (approximate 1 KB) when IPsec AH is not
                                                           enabled (security block is not enabled or operates in path through mode).
                                                         • At least 3 times MSS plus PCIe latency when IPsec AH is enabled (security block
                                                           operates in store and forward mode).
                                                       The default value is 0xA0 (160 KB)
RESERVED        31:20           0x0        RSV         Reserved.

8.2.2.10.16                Manageability Transmit TC Mapping - MNGTXMAP
                           (0x0000CD10)

      Field     Bit(s)      Init.          Type                                             Description

MAP              2:0        000b               RW      MAP
                                                       Indicates the TC that the transmit Manageability traffic is routed to.
RESERVED        31:3            0x0        RSV         Reserved.

8.2.2.10.17                Tags EtherTypes - TAG_ETYPE (0x00017100)

        Field          Bit(s)          Init.        Type                                       Description

ETAG_ETHERTYPE           15:0         0x893F        RW       E-tag EtherType
                                                             The EtherType to use to identify E-tags.
RESERVED               31:16          0x8926        RSV      Reserved.

672                                                                                                                             333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.11 PF - DCB Registers

DCB registers are owned by the PF in an IOV mode.

8.2.2.11.1             DCB Receive Packet Plane T4 Config - RTRPT4C[n]
                       (0x00002140 + 0x4*n, n=0...7)

      Field   Bit(s)    Init.   Type                                         Description

CRQ             8:0     0x0      RW    Credit Refill Quantum
                                       Amount of credits to refill in 64-byte granularity.
                                       Possible values are 0x000 - 0x1FF (0 - 32,704 bytes)
BWG            11:9     000b     RW    Bandwidth Group Index
                                       Assignment of this PB to a bandwidth group.
MCL            23:12    0x0      RW    Max Credit Limit
                                       Max amount of credits for a configured PB in 64-byte granularity.
                                       Possible values are 0x000 - 0xFFF (0 - 262,080 bytes)
RESERVED       29:24    0x0      RSV   Reserved.
GSP             30       0b      RW    Group Strict Priority
                                       When set to 1b, enables strict priority to the appropriate PB over any traffic of other
                                       PBs within the Group.
LSP             31       0b      RW    Link Strict Priority
                                       If set to 1b, enables strict priority to the appropriate PB over any traffic of other PBs.

8.2.2.11.2             DCB Receive Packet Plane Control and Status - RTRPCS
                       (0x00002430)

      Field   Bit(s)    Init.   Type                                         Description

RESERVED         0       0b      RSV   Reserved.
RRM              1       0b      RW    Receive Recycle Mode
                                       Defines the recycle mode within a BWG.
                                        0b = No recycle.
                                        1b = Recycle within the BWG. It is the only supported mode when DCB is enabled.
RAC              2       0b      RW    Receive Arbitration Control
                                        0b = RR — Round Robin.
                                        1b = WSP — Weighted Strict Priority.
RESERVED        5:3     000b     RSV   Reserved.
ARBDIS           6       0b      RW    DCB Arbiter Disable
                                       When set to 1b, this bit pauses the Rx packet plane arbitration state-machine.
                                       Therefore, during nominal operation this bit should be set to 0b.
RESERVED       26:7     0x0      RSV   Reserved.
BWGC            27       0b      RW    BWG Credits
                                       This bit affects the Rx WSP arbiter described in Figure 7-35 on page 491.
                                        0b = The step “T5[BWG].Credits > 0? or no GSP in the BWG?” is taking affect
                                               (default operation).
                                        1b = Do not bypass BWG credits consideration before transmit, meaning the second
                                               part of the condition case “or no GSP in the BWG?” is not taking place.
                                       Note: Bit RTTPCS(27) has similar affect on the Tx Packet plane Control as the
                                                 BWGC on.
RESERVED       31:28    0x6      RSV   Reserved.

333369-009                                                                                                                    673
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.11.3             DCB Receive User Priority to Traffic Class - RTRUP2TC
                       (0x00003020)

      Field   Bit(s)   Init.   Type                                       Description

UP0MAP         2:0     000b    RW     Receive User Priority 0 to Traffic Class Mapping
                                      When set to n, User Priority 0 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 0
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 0 field and Class Enable Vector bit 0 set is sent.
UP1MAP         5:3     000b    RW     Receive User Priority 1 to Traffic Class Mapping
                                      When set to n, User Priority 1 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 1
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 1 field and Class Enable Vector bit 1 set is sent.
UP2MAP         8:6     000b    RW     Receive User Priority 2 to Traffic Class Mapping
                                      When set to n, User Priority 2 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 2
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 2 field and Class Enable Vector bit 2 set is sent.
UP3MAP        11:9     000b    RW     Receive User Priority 3 to Traffic Class Mapping
                                      When set to n, User Priority 3 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 3
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 3 field and Class Enable Vector bit 3 set is sent.
UP4MAP        14:12    000b    RW     Receive User Priority 4 to Traffic Class Mapping
                                      When set to n, User Priority 4 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 4
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 4 field and Class Enable Vector bit 4 set is sent.
UP5MAP        17:15    000b    RW     Receive User Priority 5 to Traffic Class Mapping
                                      When set to n, User Priority 5 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 5
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 5 field and Class Enable Vector bit 5 set is sent.
UP6MAP        20:18    000b    RW     Receive User Priority 6 to Traffic Class Mapping
                                      When set to n, User Priority 6 is bound to Traffic Class n.
                                      Used for two purposes:
                                       • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 6
                                         is routed.
                                       • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                         Control frame with the Timer 6 field and Class Enable Vector bit 6 set is sent.

674                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

    Field     Bit(s)    Init.   Type                                         Description

UP7MAP         23:21    000b     RW    Receive User Priority 7 to Traffic Class Mapping.
                                       When set to n, User Priority 7 is bound to Traffic Class n.
                                       Used for two purposes:
                                        • Define into which Rx Packet Buffer incoming traffic carrying 802.1p field set to 7
                                          is routed.
                                        • Define according to the filling status of which Rx Packet Buffer a Priority Flow
                                          Control frame with the Timer 7 field and Class Enable Vector bit 7 set is sent.
RESERVED       31:24    0x0      RSV   Reserved.

8.2.2.11.4             DCB Transmit Descriptor Plane Queue Select - RTTDQSEL
                       (0x00004904)

    Field     Bit(s)    Init.   Type                                         Description

TXDQ_IDX        6:0     0x0      RW    Tx Descriptor Queue Index or Tx Pool of Queues Index
                                       This register is used to set VM and BQCN transmit scheduler parameters that are
                                       configured per Tx queue or per Tx pool of queues via indirect access. It means that
                                       prior to read or write access such registers, software has to make sure this field
                                       contains the index of the Tx queue or Tx pool of queue to be accessed.
                                       When DCB is disabled, VM parameters include a pool of Tx queues. As a result, this
                                       field points to the index of the pool (and not a queue index).
                                       When DCB is enabled, and/or when programming rate limiters, this field points to a
                                       Tx queue index.
                                       The registers concerned by this index are:
                                         • RTTDT1C (Section 8.2.2.11.5)
                                         • RTTQCNRC (Section 8.2.2.11.8)
                                         • RTTQCNRS (Section 8.2.2.11.9)
RESERVED       31:7     0x0      RSV   Reserved.

8.2.2.11.5             DCB Transmit Descriptor Plane T1 Config - RTTDT1C
                       (0x00004908)

128 internal registers indirectly addressed via RTTDQSEL.TXDQ_IDX (refer to Section 8.2.2.11.4).
When DCB is disabled, configure the pool index with the credits allocated to the entire pool.

    Field     Bit(s)    Init.   Type                                         Description

CRQ            13:0      X       RW    Credit Refill Quantum
                                       Amount of credits to refill the VM in 64-byte granularity.
                                       Possible values are 0x000 - 0x3FFF (0 - 1,048,512 bytes)
RESERVED       31:14    0x0      RSV   Reserved.

8.2.2.11.6             DCB Transmit Descriptor Plane T2 Config - RTTDT2C[n]
                       (0x00004910 + 0x4*n, n=0...7)

    Field     Bit(s)    Init.   Type                                         Description

CRQ             8:0     0x0      RW    Credit Refill Quantum
                                       Amount of credits to refill the TC in 64-byte granularity.
                                       Possible values are 0x000 - 0x1FF (0 - 32,704 bytes)
BWG            11:9     000b     RW    Bandwidth Group Index
                                       Assignment of this TC to a bandwidth group.

333369-009                                                                                                                675
                                 Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

      Field   Bit(s)   Init.   Type                                        Description

MCL           23:12    0x0     RW     Max Credit Limit
                                      Max amount of credits for a configured TC in 64-byte granularity.
                                      Possible values are 0x000 - 0xFFF (0 - 262,080 bytes)
RESERVED      29:24    0x0     RSV    Reserved.
GSP            30       0b     RW     Group Strict Priority
                                      When set to 1b, enables strict priority to the appropriate TC over any traffic of other
                                      TCs within the group.
LSP            31       0b     RW     Link Strict Priority
                                      When set to 1b, enables strict priority to the appropriate TC over any traffic of other
                                      TCs.

8.2.2.11.7             DCB Transmit QCN Rate-Scheduler MMW - RTTQCNRM
                       (0x00004980)

      Field   Bit(s)   Init.   Type                                        Description

MMW_SIZE      10:0     0x0     RW     Max Memory Window Size
                                      max memory window size for the QCN rate-scheduler, for all Tx queues. It is the
                                      maximum amount of 1 KB units of payload compensation time that can be
                                      accumulated for Tx queues attached to TCn.
                                      This number must be multiplied by the QCN Rate-Factor of the Tx queue before
                                      performing the MMW saturation check for that queue.
RESERVED      31:11    0x0     RSV    Reserved.

8.2.2.11.8             DCB Transmit QCN Rate-Scheduler Config - RTTQCNRC
                       (0x00004984)

128 internal registers indirectly addressed via RTTDQSEL.TXDQ_IDX (refer to Section 8.2.2.11.4).

      Field   Bit(s)   Init.   Type                                        Description

RF_DEC        13:0      X      RW     Rate Factor Decimal
                                      Tx QCN rate scheduler rate factor hexadecimal part for the Tx queue indexed by
                                      TXDQ_IDX field in RTTDQSEL register. Rate factor bits that come after the
                                      hexadecimal point.
                                      Meaningful only if RS_ENA bit is set.
RF_INT        23:14     X      RW     Rate Factor Integral
                                      Tx QCN rate scheduler rate factor integral part for the Tx queue indexed by
                                      TXDQ_IDX field in RTTDQSEL register. Rate factor bits that come before the
                                      hexadecimal point.
                                      Rate factor is defined as the ratio between the nominal link rate (i.e. 10 Gb/s) and the
                                      maximum rate allowed to that queue via QCN.
                                      Minimum allowed bandwidth share for a queue is 0.1% of the link rate, i.e. 10 Mb/s
                                      for devices operated at 10 Gb/s, leading to a maximum allowed rate factor of 1000.
                                      Meaningful only if RS_ENA bit is set.
RESERVED      30:24    0x0     RSV    Reserved.

676                                                                                                               333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

    Field      Bit(s)        Init.         Type                                          Description

RS_ENA          31            0b           SC      Rate Scheduler Enable
                                                   Tx QCN rate scheduler enable for the Tx queue indexed by TXDQ_IDX field in
                                                   RTTDQSEL register.
                                                     0b = The QCN rate factor programmed in this register is meaningless, and the
                                                          switch for that queue is always forced to “on”. The queue is not rate-controlled
                                                          for QCN.
                                                     1b = The QCN rate programmed in this register is enforced (i.e., the queue is rate
                                                          controlled for QCN). At the time it is set, the current timer value is loaded into
                                                          the Timestamp stored for that entry.
                                                   Bandwidth Group Assignment of this TC to a bandwidth group. Each TC must be
                                                   assigned to a different BWG number, unless the TC is a member of a BWG. No more
                                                   than two TCs can share the same BWG.

8.2.2.11.9                  DCB Transmit QCN Rate-Scheduler Status - RTTQCNRS
                            (0x00004988)

128 internal registers indirectly addressed via RTTDQSEL.TXDQ_IDX (refer to Section 8.2.2.11.4).

    Field      Bit(s)        Init.         Type                                          Description

MIFS            31:0         0x0           RW      Minimum Inter-Frame Spacing
                                                   Tx QCN rate scheduler current minimum inter-frame spacing for the Tx queue indexed
                                                   by TXDQ_IDX field in RTTDQSEL register.
                                                   When read, it is the current algebraic value of the MIFS interval for the queue,
                                                   expressed in byte units (31 LS-bits taken), relative to the QCN rate scheduler. It is
                                                   obtained by hardware subtracting the current value of the timer associated to that
                                                   QCN rate-scheduler from the timestamp stored for that queue. A strict positive value
                                                   means a switch in “off” state. It is expressed in 2's complement format.

8.2.2.11.10                 DCB Transmit QCN Rate Reset - RTTQCNRR (0x0000498C)

       Field      Bit(s)           Init.        Type                                       Description

RESERVED                0            0b          RSV   Reserved.
QCN_CLEAR_ALL           1            0b          RW    QCN Clear All
                                                       Clear all QCN rate-limiters.
                                                       When set, the 128 RTTQCNRC.RS_ENA bits are cleared, releasing any active QCN
                                                       rate-limiter. This bit must be set by software whenever the link speed has
                                                       changed.
                                                       This bit is self-cleared by hardware.
RESERVED              31:2           0x0         RSV   Reserved.

8.2.2.11.11                 DCB Transmit QCN Tagging - RTTQCNTG (0x00004A90)

    Field      Bit(s)        Init.         Type                                          Description

CNTGI           7:0          0x0           RW      CN-tag Insertion enable per TC bitmap
                                                   When bit n is cleared, hardware does not insert any CN-tag in the transmitted frame
                                                   (rate-controlled or not) sent from the TCn. It is assumed that QCN is disabled for the
                                                   User Priorities mapped to that TC.
                                                   When bit n is set, hardware inserts the proper CN-tag in transmitted frames
                                                   (rate-controlled or not) sent from the TCn. It is assumed that QCN is enabled for the
                                                   User Priorities mapped to that TC.
RESERVED        31:8         0x0           RSV     Reserved.

333369-009                                                                                                                               677
                                            Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                        Programming Interface

8.2.2.11.12                Strict Low Latency Tx Queues - TXLLQ[n] (0x000082E0 +
                           0x4*n, n=0...3)

          Field            Bit(s)   Init.    Type                                       Description

STRICT_LOW_LATENCY         31:0     0x0       RW        Strict Low Latency Enable
                                                        When set, defines the relevant Tx queue as strict low latency. All queues
                                                        that belong to the LSP TC must be set as strict low latency queues. Bit ‘m’ in
                                                        register ‘n’ corresponds to Tx queue 32 x ‘n’ + ‘m’.

8.2.2.11.13                DCB Transmit User Priority to Traffic Class - RTTUP2TC
                           (0x0000C800)

      Field       Bit(s)   Init.    Type                                           Description

UP0MAP             2:0      0x0     RW      Transmit User Priority 0 to Traffic Class Mapping
                                            When set to n, User Priority 0 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 0 field and Class Enable Vector bit 0 set, to
                                            determine which traffic class is paused.
UP1MAP             5:3      0x0     RW      Transmit User Priority 1 to Traffic Class Mapping
                                            When set to n, User Priority 1 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 1 field and Class Enable Vector bit 1 set, to
                                            determine which traffic class is paused.
UP2MAP             8:6      0x0     RW      Transmit User Priority 2 to Traffic Class Mapping
                                            When set to n, User Priority 2 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 2 field and Class Enable Vector bit 2 set, to
                                            determine which traffic class is paused.
UP3MAP            11:9      0x0     RW      Transmit User Priority 3 to Traffic Class Mapping
                                            When set to n, User Priority 3 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 3 field and Class Enable Vector bit 3 set, to
                                            determine which traffic class is paused.
UP4MAP            14:12     0x0     RW      Transmit User Priority 4 to Traffic Class Mapping
                                            When set to n, User Priority 4 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 4 field and Class Enable Vector bit 4 set, to
                                            determine which traffic class is paused.
UP5MAP            17:15     0x0     RW      Transmit User Priority 5 to Traffic Class Mapping
                                            When set to n, User Priority 5 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 5 field and Class Enable Vector bit 5 set, to
                                            determine which traffic class is paused.
UP6MAP            20:18     0x0     RW      Transmit User Priority 6 to Traffic Class Mapping
                                            When set to n, User Priority 6 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 6 field and Class Enable Vector bit 6 set, to
                                            determine which traffic class is paused.
UP7MAP            23:21     0x0     RW      Transmit User Priority 7 to Traffic Class Mapping
                                            When set to n, User Priority 7 is bound to Traffic Class n. Used when receiving a
                                            Priority Flow Control frame with the Timer 7 field and Class Enable Vector bit 7 set, to
                                            determine which traffic class is paused.
RESERVED          31:24     0x0     RSV     Reserved.

678                                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.11.14                   DCB Transmit Packet Plane Control and Status - RTTPCS
                              (0x0000CD00)

        Field          Bit(s)          Init.        Type                                      Description

RESERVED                 4:0           0x0          RSV    Reserved.
TPPAC                     5             0b          RW     Transmit Packet Plane Arbitration Control
                                                            0b = RR — Round Robin (with respect to Stop Markers).
                                                            1b = SP — Strict Priority (with respect to Stop Markers).
ARBDIS                    6             0b          RW     DCB Arbiter Disable
                                                           When set to 1b this bit pauses the Tx Packet plane arbitration state-machine.
                                                           Therefore, during nominal operation this bit should be set to 0.
RESERVED                  7             0b          RSV    Reserved.
TPRM                      8             0b          RW     Transmit Packet Plane Recycle Mode
                                                           Defines the recycle mode within a BWG.
                                                            0b = No recycle.
                                                            1b = Recycle within the BWG.
RESERVED                 21:9          0x0          RSV    Reserved.
ARBD                   30:22           0x24         RW     Arbitration Delay
                                                           Minimum cycles delay between packets arbitration. When RTTPCS.TPPAC is set
                                                           to 1b, the arbitration delay is according to ARBD, otherwise the arbitration delay
                                                           is 0x0.
                                                           Should be kept at default in non EEDC mode. In EEDC mode, should be set to
                                                           0x004.
BYPASS_DCB_ARB           31             1b          RW     Bypass DCB Arbiter
                                                            0b = DCB arbiter is used.
                                                            1b = DCB arbiter is bypassed.
                                                           Must be cleared in DCB mode.

8.2.2.11.15                   DCB Transmit Packet Plane T2 Config - RTTPT2C[n]
                              (0x0000CD20 + 0x4*n, n=0...7)

      Field     Bit(s)         Init.         Type                                           Description

CRQ              8:0            0x0            RW     Credit Refill Quantum
                                                      Amount of credits to refill the TC in 64-byte granularity.
                                                      Possible values are 0x000 - 0x1FF (0 - 32,704 bytes).
BWG             11:9           000b            RW     Bandwidth Group
                                                      Assignment of this TC to a bandwidth group.
MCL             23:12           0x0            RW     Max Credit Limit
                                                      Max amount of credits for a configured TC in 64-byte granularity.
                                                      Possible values are 0x000 - 0xFFF (0 - 262,080 bytes).
RESERVED        29:24           0x0          RSV      Reserved.
GSP              30             0b             RW     Group Strict Priority
                                                      When set to 1. enables strict priority to the appropriate TC over any traffic of other
                                                      TCs within the Group.
LSP              31             0b             RW     Link Strict Priority
                                                      When set to 1b, enables strict priority to the appropriate TC over any traffic of other
                                                      TCs.

333369-009                                                                                                                                 679
                                               Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                              Programming Interface

#### 8.2.2.12 PF - TPH Registers

8.2.2.12.1           Rx TPH Control Register - TPH_RXCTRL[n] (0x0000100C +
                     0x40*n, n=0...63 and 0x0000D00C + 0x40*(n-64),
                     n=64...127)

Note:      Additional address(es): 0x0D00C + 0x40*(n-64), n=64...127

         Field         Bit(s)    Init.   Type                                   Description

RX_DESC_FETCH_TPH_EN     0        0b      RW    Receive Descriptor Fetch TPH Enable
                                                 0b = Hardware does not enable TPH for descriptor fetches.
                                                 1b = Hardware enables TPH for all Rx descriptors fetch from memory.
                                                This bit is cleared as a default.
RX_DESC_WB_TPH_EN        1        0b      RW    Receive Descriptor Writeback TPH Enable
                                                 0b = Hardware does not enable TPH for descriptor write-backs.
                                                 1b = Hardware enables TPH for all Rx descriptors written back into
                                                        memory.
                                                This bit is cleared as a default. The hint used is the hint set in the Socket
                                                ID field.
RX_HEADER_TPH_EN         2        0b      RW    Receive Header TPH Enable
                                                 0b = Hardware does not enable TPH for Rx headers.
                                                 1b = Hardware enables TPH for all received header buffers.
                                                This bit is cleared as a default. The hint used is the hint set in the Socket
                                                ID field.
RX_PAYLOAD_TPH_EN        3        0b      RW    Receive Payload TPH Enable
                                                 0b = Hardware does not enable TPH for Ethernet payloads.
                                                 1b = Hardware enables TPH for all Ethernet payloads written into
                                                        memory.
                                                This bit is cleared as a default. The hint used is the hint set in the Socket
                                                ID field.
RESERVED                8:4      0x0     RSV    Reserved.
RXDESCREADROEN           9        1b      RW    Rx Descriptor Read Relax Order Enable
RESERVED                 10       0b     RSV    Reserved.
RXDESCRWBROEN            11       0b      RW    Rx Descriptor Write Back Relax Order Enable
                                                This bit must be 0b to allow correct functionality of the descriptors write-
                                                back.
RESERVED                 12       0b     RSV    Reserved.
RXDATAWRITEROEN          13       1b      RW    Rx Data Write Relax Order Enable
RESERVED                 14       0b     RSV    Reserved.
RXREPHEADERROEN          15       1b      RW    Rx Split Header Relax Order Enable
                                                This bit impacts only the Relax Order setting of the header part writes.
                                                The Relax Order setting of the data part is controlled via the
                                                RXDATAWRITEROEN bit
RESERVED               23:16     0x0     RSV    Reserved.
CPUID                  31:24     0x0      RW    Physical ID
                                                On TPH-capable platforms, the device driver programs a value based on
                                                the relevant Socket ID associated with this receive queue.
                                                Note: For TPH platforms, Bits[31:27] of this field should always be set
                                                         to zero.

8.2.2.12.2           Rx TPH Control Register - TPH_RXCTRL_ALIAS[n]
                     (0x00002200 + 0x4*n, n=0...15; RW)

Field definitions are the same as those defined in Section 8.2.2.12.1

680                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.12.3             Tx TPH Control Registers - TPH_TXCTRL[n] (0x0000600C +
                       0x40*n, n=0...127)

Note:        Additional address(es): 0x0D00C + 0x40*(n-64), n=64...127

         Field            Bit(s)    Init.   Type                                   Description

TX_DESC_FETCH_TPH_EN        0        0b      RW    Transmit Descriptor Fetch TPH Enable
                                                    0b = Hardware does not enable TPH for descriptor fetches.
                                                    1b = Hardware enables TPH for all Tx descriptors fetch from memory.
                                                   This bit is cleared as a default.
TX_DESC_WB_TPH_EN           1        0b      RW    Transmit Descriptor Writeback TPH Enable
                                                    0b = Hardware does not enable TPH for descriptor write-backs.
                                                    1b = Hardware enables TPH for all Tx descriptors written back into
                                                           memory.
                                                   This bit is cleared as a default. The hint used is the hint set in the Socket
                                                   ID field.
RESERVED                    2        0b     RSV    Reserved.
TX_PACKET_TPH_EN            3        0b      RW    Transmit Packet TPH Enable
                                                    0b = Hardware does not enable TPH for Ethernet payloads.
                                                    1b = Hardware enables TPH for all Ethernet payloads read from
                                                           memory.
                                                   This bit is cleared as a default.
RESERVED                   8:4      0x0     RSV    Reserved.
TXDESCREADROEN              9        1b      RW    Tx Descriptor Read Relax Order Enable
RESERVED                   10        0b     RSV    Reserved.
TXDESCRWBROEN              11        0b      RW    Tx Descriptor Write Back Relax Order Enable
RESERVED                   12        0b     RSV    Reserved.
TXDATAREADROEN             13        1b      RW    Tx Data Read Relax Order Enable
RESERVED                  23:14     0x0     RSV    Reserved.
CPUID                     31:24     0x0      RW    Physical ID
                                                   On TPH-capable platforms, the device driver programs a value based on
                                                   the relevant Socket ID associated with this transmit queue.
                                                   Note: For TPH platforms, bits 31:27 of this field should always be set
                                                            to zero.

333369-009                                                                                                                   681
                                   Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

#### 8.2.2.13 PF - Timers Registers

8.2.2.13.1              TCP Timer - TCPTIMER (0x0000004C)

       Field     Bit(s)   Init.     Type                                      Description

DURATION          7:0     0x0        RW    Duration
                                           Duration (in ms) of the TCP interrupt interval.
KICKSTART          8       0b       RWS    Counter Kick-Start
                                            0b = No effect.
                                            1b = Kick-starts the counter down-count from the initial value defined in
                                                 Duration field.
TCPCOUNTEN         9       0b        RW    TCP Count Enable
                                             0b = TCP timer counting is disabled.
                                             1b = TCP timer counting is enabled.
                                           Upon enabling, TCP counter counts from its internal state. If the internal state is
                                           equal to zero, down-count does not restart until KICKSTART is activated.
                                           If the internal state is not 0b, down-count continues from the internal state. This
                                           enables a pause of the counting for debug purposes.
TCPCOUNTFINISH    10       0b       RWS    TCP Count Finish
                                           This bit enables software to trigger a TCP timer interrupt, regardless of the
                                           internal state.
                                             0b = No effect.
                                             1b = Triggers an interrupt, and resets the internal counter to its initial value.
                                                   Down-count does not restart until either KICKSTART is activated or Loop is
                                                   set.
LOOP              11       0b        RW    TCP Loop
                                            0b = TCP counter stops at zero value, and does not re-start until KICKSTART is
                                                 activated.
                                            1b = TCP counter reloads duration each time it reaches zero, and goes on
                                                 down-counting from this point without kick-starting.
RESERVED         31:12    0x0       RSV    Reserved.

682                                                                                                               333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.14 PF - FCoE Registers

8.2.2.14.1             FC Indirect DMA Context: User Descriptor PTR Low - FCPTRL
                       (0x00002410)

    Field     Bit(s)    Init.   Type                                         Description

PTR_LOW        31:0      X       RW    User Descriptor PTR Low
                                       Four least significant bytes of the physical pointer to the User Descriptor list. The
                                       pointer must be 16-byte aligned so the 4 LS bits are read-only as zeros.

8.2.2.14.2             FC Indirect DMA Context: User Descriptor PTR High -
                       FCPTRH (0x00002414)

    Field     Bit(s)    Init.   Type                                         Description

PTR_HI         31:0      X       RW    User Descriptor PTR High
                                       Four most significant bytes of the physical pointer to the User Descriptor list.

8.2.2.14.3             FC Indirect DMA Context: Buffer Control - FCBUFF
                       (0x00002418)

    Field     Bit(s)    Init.   Type                                         Description

VALID            0       0b      RW    DMA Context Valid
                                       When set to 1b, indicates that the context is valid. If software clears the VALID bit,
                                       the software should poll it until it is actually cleared by hardware before unlocking the
                                       user buffers.
FIRST            1       0b      RW    DMA First
                                       This bit is a status indication. Software should clear it during FC context
                                       programming. The DMA unit sets this bit when it receives a frame that matches the
                                       context and marked by the Filter unit as first.
LAST             2       0b      RW    DMA Last
                                       This bit is a status indication. Software should clear it during FC context
                                       programming. Hardware sets this bit when it exhausts the last user buffer.
BUFFSIZE        4:3     00b      RW    Buffer Size
                                       This field defines the user buffer size used in this context as follows:
                                        00b = 4 KB
                                        01b = 8 KB
                                        10b = 16 KB
                                        11b = 64 KB
WRCONTX          5       0b      RW    Write DDP Context
                                        0b = Rad exchange context aimed for initiator (originator) usage.
                                        1b = Write exchange context aimed for target (responder) usage.
BUFFCNT        15:6     0x0      RW    Buffer Count
                                       Defines the number of the user buffer while 0x00 equals 1024. It is programmed by
                                       the software and updated by hardware during reception.
OFFSET         31:16    0x0      RW    User Buffer Offset
                                       Byte offset within the user buffer to which the FC data of large FC receive should be
                                       posted.

333369-009                                                                                                                     683
                                 Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

8.2.2.14.4             FC Indirect DMA Context: Receive DMA RW - FCDMARW
                       (0x00002420)

      Field   Bit(s)   Init.   Type                                        Description

FCOESEL       10:0     0x0     RW     FCoE Context Select
                                      This field defines the FCoE Rx context index (equals the RX_ID for that context).
RESERVED      13:11    000b    RSV    Reserved.
WE             14       0b     RW     Write Enable
                                      When this bit is set, the content of the FCPTRL, FCPTRH, and FCBUFF registers are
                                      programmed to the FCoE DMA context of index FCOESEL. This bit should never be set
                                      together with the RE bit in this register
RE             15       0b     RW     Read Enable
                                      When this bit is set, the internal FCoE DMA context of index FCOESEL is fetched to the
                                      FCPTRL, FCPTRH, and FCBUFF registers. This bit should never be set together with the
                                      WE bit in this register.
LASTSIZE      31:16    0x0     RW     Last User Buffer Size
                                      Defines the size in bytes of the last user buffer. A value of 0 indicates a 64 KB
                                      buffer.

8.2.2.14.5             FC Receive Control - FCRXCTRL (0x00005100)

      Field   Bit(s)   Init.   Type                                        Description

RESERVED      11:0     0x0     RSV    Reserved.
SMAC_EN        12       1b     RW     SMAC Enable
                                       0b = SMAC is ignored.
                                       1b = SMAC field as part of the context matching of received FCoE packets.
DID_EN         13       1b     RW     D_ID Enable
                                       0b = D_ID is ignored.
                                       1b = Check D_ID field as part of the context matching of received FCoE packets.
RESERVED      31:14    0x0     RSV    Reserved.

8.2.2.14.6             FC Indirect Filter Context: Control - FCFLT (0x00005108)

      Field   Bit(s)   Init.   Type                                        Description

VALID           0       0b     RW     Filter Context Valid
                                      When set to 1b, indicates that the context is valid.
FIRST           1       0b     RW     Filter First
                                      This bit is a status indication. Software should clear it during FC context
                                      programming. The Filter unit sets this bit when it receives a first frame that matches
                                      the context.
RESERVED       7:2      X      RSV    Reserved.
SEQ_ID        15:8      X      RW     Sequence ID
                                      The sequence ID of the last received frame. Initialized to 0 by the driver at context
                                      programming.
SEQ_CNT       31:16     X      RW     Sequence Count
                                      The sequence Count of the expected received frame.
                                      Should be set to 0 for read contexts. Should be set to SEQ_CNT + 1 of the last packet
                                      of the same exchange received from the initiator for write contexts.

684                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.14.7               FC Indirect Filter Context: Source MAC Address - FCSMAC
                         (0x0000510C)

Note:        This register is stored in network ordering (big endian).

     Field      Bit(s)   Init.   Type                                          Description

FCSMAC           31:0    0x0     RW     Source MAC Address (low bits)
                                        Used to validate incoming FCoE exchange

8.2.2.14.8               FC Indirect Filter Context: RW Control - FCFLTRW
                         (0x00005110)

     Field      Bit(s)   Init.   Type                                          Description

FCOESEL          10:0    0x0     WO     FCoE context Select
                                        This field defines the FCoE Rx context index (equals the OX_ID or the RX_ID for that
                                        context).
RESERVED        12:11    00b     RSV    Reserved.
RE_VALIDATE       13      0b     WO     Re-Validate
                                        Fast re-validation of the filter context. Setting this bit together with the WE bit in this
                                        register validates the selected filter context. Hardware sets the VALID bit and clears
                                        the First bit (described in the FCFLT register in Section 8.2.2.14.6) while keeping all
                                        other filter parameters intact.
WE                14      0b     WO     Write Enable
                                        When this bit is set, the content of the FCFLT and FCSMAC registers, and portions of
                                        the FCFLTRW register are programmed to the Filter of index FCOESEL. This bit should
                                        never be set together with the RE bit in this register.
RE                15      0b     WO     Read Enable
                                        When this bit is set, the internal filter context of index FCOESEL is fetched to the
                                        FCFLT, FCSMAC, and FCFLTRW registers. This bit should never be set together with
                                        the WE bit in this register.
SMAC_HIGH       31:16    0x0     RW     Source MAC Address (high bits)
                                        Used to validate incoming FCoE exchange.
                                        This field is stored in network ordering (big endian).

8.2.2.14.9               FC Indirect Filter Context: D_ID Register - FCD_ID
                         (0x00005114)

     Field      Bit(s)   Init.   Type                                          Description

FCD_ID           23:0    0x0     RW     FCD ID
                                        The D_ID to validate incoming FCoE exchange.
RESERVED        31:24    0x0     RSV    Reserved.

8.2.2.14.10              FC Indirect Filter Context: Offset Parameter - FCPARAM
                         (0x000051D8)

     Field      Bit(s)   Init.   Type                                          Description

PARAM            31:0    0x0     RW     FC Parameter
                                        This field contains the expected FC Parameter in the next received frame. Initialized to
                                        0 by the driver at context programming.
                                        Note: This field is defined in Big Endian (LS byte is first on the wire).

333369-009                                                                                                                      685
                                  Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                       Programming Interface

8.2.2.14.11                 FCoE Redirection Control - FCRECTL (0x0000ED00)

      Field      Bit(s)      Init.     Type                                       Description

ENA                0          0b        RW     FC Redirection Enable
                                                0b = The redirection table is not active.
                                                1b = The FC redirection is enabled.
                                               Note: When FC redirection is enabled, the POOL_ENABLE and the QUEUE_ENABLE
                                                      in the ETQF and ETQS registers (respectively) must be cleared for FCoE data
                                                      packets.
RESERVED         31:1        0x0        RSV    Reserved.

8.2.2.14.12                 FCoE Redirection Table - FCRETA[n] (0x0000ED10 + 0x4*n,
                            n=0...31)

         Field            Bit(s)     Init.    Type                                   Description

TABLE_ENTRY                6:0       0x0      RW     Table Entry
                                                     Defines the redirection output queue number.
                                                     Register ‘n’ is the TABLE_ENTRY index ‘n’, which is the matched value to the 6
                                                     LS bits of the FC exchange ID (for exchange IDs where 6 LS bits are between 0
                                                     and 31).
RESERVED                  15:7       0x0      RSV    Reserved.
TABLE_ENTRY_HIGH          22:16      0x0      RW     Table Entry High
                                                     Defines the redirection output queue number.
                                                     Register ‘n’ is the TABLE_ENTRY high index ‘32+n’, which is the matched value
                                                     to the 6 LS bits of the FC exchange ID (for exchange IDs where 6 LS bits are
                                                     between 32 and 63).
RESERVED                  31:23      0x0      RSV    Reserved

8.2.2.14.13                 FCoE Direct DMA Context - FCDDC[n,m] (0x00020000 +
                            0x4*n + 0x10*m, n=0...3, m=0...2047)

      Field      Bit(s)      Init.     Type                                       Description

FCDDC            31:0        0x0        RW     FCoE Direct DMA Context
                                               Direct access to DMA context:
                                                DW[0x10*m] =          FCPTRL[m]
                                                DW[0x10*m+4] =        FCPTRH[m]
                                                DW[0x10*m+8] =        FCBUFF[m]
                                                DW[0x10*m+0xC] = FCDMARW[m] (LASTSIZE bits only)

8.2.2.14.14                 FCoE Direct Filter Context - FCDFC[n,m] (0x00028000 +
                            0x4*n + 0x10*m, n=0...3, m=0...2047)

      Field      Bit(s)      Init.     Type                                       Description

FCDFCFLT         31:0        0x0        RW     FCoE Direct Filter Context
                                               Direct access to filter context:
                                                DW[0x10*m] =             FCFLT[m]
                                                DW[0x10*m+0x4] = FCPARAM[m]
                                                DW[0x10*m+0x8] = FCSMAC[m]
                                                DW[0x10*m+0xC] = FCFLTRW[m] (SMAC_HIGH bits only)

686                                                                                                                     333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.14.15            FCoE Direct Filter Context D_ID - FCDFCD[n] (0x00030000
                       + 0x4*n, n=0...2047)

    Field     Bit(s)    Init.   Type                                    Description

D_ID           23:0     0x0      RW    D ID
                                       D_ID to validate incoming FCoE exchange
RESERVED       31:24    0x0      RSV   Reserved.

333369-009                                                                            687
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

#### 8.2.2.15 PF - Flow Director Registers

These registers are used to control the flow director functionality.

8.2.2.15.1             Flow Director Filters Control Register - FDIRCTRL
                       (0x0000EE00)

Note:       This register should be configured ONLY as part of the Flow Director initialization flow or
            Clearing the Flow Director table. Programming of this register with non zero value in the
            PBALLOC field initializes the Flow Director table.

          Field          Bit(s)    Init.   Type                                  Description

PBALLOC                    1:0     00b      RW    PB Allocation
                                                  Memory allocation for the Flow Director Filters.
                                                   00b = No memory allocation. Flow Director Filters are disabled.
                                                   01b = 64 KB (8K minus 1 signature filters or 2K minus 1 perfect match
                                                         filters)
                                                   10b = 128 KB (16K minus 1 signature filters or 4K minus 1 perfect
                                                         match filters)
                                                   11b = 256 KB (32K minus 1 signature filters or 8K minus 1 perfect
                                                         match filters)
RESERVED                   2        0b     RSV    Reserved.
INIT_DONE                  3        0b      RO    Initialization Done
                                                  Flow Director initialization completion indication (Read Only status).
                                                  Indicates that hardware initialized the Flow Director table according to
                                                  the PBALLOC setting. Software must not access any other Flow Director
                                                  filters registers before the INIT_DONE bit is set.
                                                  When Flow Director filters are enabled (PBALLOC > 0), the software must
                                                  wait for INIT_DONE indication before Rx is enabled.
PERFECT_MATCH              4        0b      RW    Perfect Match
                                                  Flow Director Filters Mode of operation.
                                                   0b = Hardware supports Signature filters according to the PBALLOC.
                                                   1b = Hardware supports Perfect Match filters according to the
                                                        PBALLOC.
REPORT_STATUS              5        0b      RW    Report Status
                                                  Report Flow Director filter's status in the RSS field of the Rx descriptor
                                                  for packets that matches a Flow Director filter. Enabling the Flow Director
                                                  filter's status, the RXCSUM.PCSD bit (Section 8.2.2.8.1)should be set as
                                                  well (disabling the fragment checksum).
                                                  Note: The Flow Director filter Status and Error bits in the Extended
                                                             Status and Error fields in the Rx descriptor are always enabled.
RESERVED                   6        0b     RSV    Reserved.
REPORT_STATUS_ALWAYS       7        0b      RW    Report Status Always
                                                  Report Flow Director status in the RSS field of the Rx descriptor on any
                                                  packet that can be a candidate for the Flow Director filters. This bit can
                                                  be set to 1b only when both the RXCSUM.PCSD bit and the
                                                  REPORT_STATUS bit in this register are set.
DROP_QUEUE                14:8     0x0      RW    Drop Queue
                                                  Absolute Rx queue index used for the dropped packets. Software might
                                                  set this queue to an empty one by setting the RDLEN[n] to 0x0.
DROP_NO_MATCH              15       0b      RW    Drop No Match
                                                  If set, send to the DROP_QUEUE packets that were candidates for Flow
                                                  Director and did not match any filters. Candidature of packets is defined
                                                  in Table 7-5 on page 377.
FLEX_OFFSET               20:16    0x0      RW    Flexible Offset
                                                  Offset within the first 64 bytes of the packet of a flexible 2-byte tuple.
                                                  The offset is defined in word units counted from the first byte in the
                                                  destination Ethernet MAC Address.

688                                                                                                               333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

            Field              Bit(s)     Init.       Type                                   Description

FILTERMODE                     23:21      000b         RW     Filter Mode
                                                              Defines the fields on which the Flow director acts:
                                                               000b = IPMODE — L3/L4 tuple.
                                                               001b = MACVLANMODE — Acts on the MAC and VLAN.
                                                               010b = Cloud: NVGRE — Based on TNI, inner MAC, inner VLAN.
                                                                               VXLAN — Based on VNI, inner MAC, inner VLAN.
                                                               All other values are reserved.
MAX_LENGTH                     27:24      0x0          RW     Max Linked List Length
                                                              This field defines the maximum recommended linked list associated to
                                                              any Hash value. Packets that match filters that exceed MAX_LENGTH are
                                                              reported with an active Length bit in the Extended Error field. In
                                                              addition, “Drop” filters that exceed the MAX_LENGTH are posted to the
                                                              Rx queue defined in the filter context rather than the DROP_QUEUE
                                                              defined in this register.
                                                              MAX_LENGTH is defined in units of 2 filters, and exceeding it reflects the
                                                              addition of two more filters.
                                                              Note: Software should set this field to a value that indicates
                                                                        exceptional long buckets. Supporting 32K filters with good hash
                                                                        scheme key, it is expected that a value of 0xA might be a good
                                                                        choice.
FULL_THRESH                    31:28      0x0          RW     Full Threshold
                                                              A recommended minimum number of flows that should remain unused
                                                              (defined in units of 16 filters). When software exceeds this threshold (too
                                                              low number of unused flows), hardware generates the Flow Director Full
                                                              interrupt. Software should avoid additional programming following this
                                                              interrupt.

8.2.2.15.2                   Flow Director Filters Source IPv6 - FDIRSIPV6[n]
                             (0x0000EE0C + 0x4*n, n=0...2)

    Field           Bit(s)   Init.      Type                                          Description

IP6SA               31:0     0x0        RW        IPv6 Source Address
                                                  Three LS DWords of the source IPv6 address.
                                                  The FDIRIPSA register contains the MS DWord of the IP6 address. The LS byte of the
                                                  FDIRIPSA register is first on the wire and the MS byte of FDIRSIPv6[2] is last on the
                                                  wire
                                                  In MACVLANMODE, FDIRSIPv6_0[31:0] and FDIRSIPv6_1[15:0] hold the destination
                                                  MAC Address value. FDIRSIPv6_1[31:16] and FDIRSIPv6_2[31:0] are reserved and
                                                  should be set to 0x0.

8.2.2.15.3                   Flow Director Filters IP SA - FDIRIPSA (0x0000EE18)

    Field           Bit(s)   Init.      Type                                          Description

IP4SA               31:0     0x0        RW        IPv4 Source Address
                                                  Source IPv4 address or MS DWord of the source IPv6 address, where the field is
                                                  defined in Big Endian (LS byte is first on the wire).
                                                  In MACVLANMODE, this field is reserved and should be set to 0x0.

333369-009                                                                                                                            689
                                         Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

8.2.2.15.4                      Flow Director Filters IP DA - FDIRIPDA (0x0000EE1C)

      Field           Bit(s)    Init.    Type                                            Description

IP4DA                 31:0      0x0      RW       IPv4 Destination Address
                                                  This field is defined in Big Endian (LS byte is first on the wire).
                                                  In MACVLANMODE, this field is reserved and should be set to 0x0.

8.2.2.15.5                      Flow Director Filters Port - FDIRPORT (0x0000EE20)

       Field           Bit(s)    Init.    Type                                            Description

SOURCE                  15:0      0x0     RW       Source Port Number
                                                   This field is defined in Little Endian (MS byte is first on the wire).
                                                   In MACVLANMODE and cloud modes (NVGRE/VXLAN), this field is reserved and
                                                   should be set to 0x0.
DESTINATION            31:16      0x0     RW       Destination Port Number
                                                   This field is defined in Little Endian (MS byte is first on the wire).
                                                   In MACVLANMODE and cloud modes (NVGRE/VXLAN), this field is reserved and
                                                   should be set to 0x0.

8.2.2.15.6                      Flow Director Filters VLAN and FLEX Bytes - FDIRVLAN
                                (0x0000EE24)

      Field           Bit(s)    Init.    Type                                            Description

VLAN                  15:0      0x0      RW       VLAN Tag
                                                  This field is defined in Little Endian (MS byte is first on the wire). The CFI bit must be
                                                  set to zero and it is not checked by hardware.
FLEX                  31:16     0x0      RW       Flexible
                                                  Flexible tuple data as defined by the FLEX_OFFSET field in the FDIRCTRL register,
                                                  where the field is defined in Big Endian (LS byte is first on the wire).

8.2.2.15.7                      Flow Director Filters Hash Signature - FDIRHASH
                                (0x0000EE28)

              Field             Bit(s)    Init.      Type                                      Description

HASH                             14:0     0x0         RW      Hash
                                                              Bucket hash value that identifies a filter's linked list
BUCKET_VALID                      15       0b         RW      Bucket Valid
                                                              The Valid bit is set by hardware whenever there is at least one filter
                                                              assigned to this hash.
SIGNATURE_SW_INDEX               30:16    0x0         RW      Signature/Software Index
                                                              Flow Director Filter Signature for Signature filters and SW-index for
                                                              perfect match filters.
                                                              In perfect match mode, the two MS bits should be zero.
RESERVED                          31       0b        RSV      Reserved.

690                                                                                                                             333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.15.8                Flow Director Filters Command Register - FDIRCMD
                          (0x0000EE2C)

       Field     Bit(s)     Init.    Type                                        Description

CMD               1:0       0x0      RW     Command
                                            Flow Director filter programming command.
                                             00b = No Action
                                             01b = Add Flow
                                             10b = Remove Flow
                                             11b = Query Command
                                            Following a command completion, hardware clears the CMD field. In a query
                                            command, all other parameters are valid when the CMD field is zero.
FILTER_VALID       2         0b      RW     Filter Valid
                                            Valid filter is found by the query command. This bit is set by the device following a
                                            “Query Command” completion.
FILTER_UPDATE      3         0b      RW     Filter Update
                                            This bit is relevant only for “Add Flow” command, and must be set to zero in any
                                            other commands.
                                             0b = The filter parameters do not override existing ones if exist while setting only
                                                    the collision bit.
                                             1b = The new filter parameters override existing ones if exist keeping the
                                                    collision bit as is.
IPV6DMATCH         4         0b      RW     IPv6 Destination Match
                                            IP destination match to IP6AT filter. This bit is meaningful only for perfect match
                                            IPv6 filters. Otherwise it should be cleared by software at programming time.
                                             0b = The Destination IPv6 address should not match the IP6AT.
                                             1b = The Destination IPv6 address should match the IP6AT.
                                            This field might never match local VM to VM traffic.
L4TYPE            6:5       00b      RW     L4 Packet Type
                                            Defines the packet as one of the following L4 types:
                                             00b = Reserved.
                                             01b = UDP
                                             10b = TCP
                                             11b = SCTP
IPV6               7         0b      RW     IPV6
                                             0b = IPv4 packet type.
                                             1b = IPv6 packet type.
                                            Relevant only if FDIRM.L3P is not set.
CLEARHT            8         0b      RW     Clear Flow Director Head and Tail Registers
                                            This bit is set only as part of Flow Director initialization. During nominal operation it
                                            must be kept at 0b.
DROP               9         0b      RW     Packet Drop Action
                                            Receive packets that match a filter with active DROP bit and do not exceed the
                                            maximum recommended linked list length defined in FDIRCTRL.MAX_LENGTH field
                                            are posted to the global queue defined by FDIRCTRL.DROP_QUEUE.
                                            Receive packets that match a filter with active DROP bit and exceeds the maximum
                                            recommended linked list length defined in FDIRCTRL.MAX_LENGTH field are posted
                                            to the queue defined by RX_QUEUE field in this register. The receive descriptor of
                                            such packets is reported with active FDIRErr(0) flag indicating that the
                                            MAX_LENGTH was exceeded.
                                            Note: As in some cases, packets matching this filter may still be forwarded, even
                                                     when the DROP bit is set. The QUEUE_EN flag must be set, and RX_QUEUE
                                                     in this register must be point to a valid queue. Otherwise, the result is
                                                     unexpected.
                                            The DROP flag is useful only for Perfect Match mode and it should not be set in
                                            Signature mode.
RESERVED           10        0b      RSV    Reserved.

333369-009                                                                                                                        691
                                    Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                        Programming Interface

       Field      Bit(s)     Init.     Type                                          Description

LAST                11         0b      RW       Last
                                                Last filter indication in the linked list.
                                                At Flow programming, the software should set the LAST bit to 1b. Hardware might
                                                modify this bit when adding or removing flows from the same linked list.
COLLISION           12         0b      RW       Collision Indication
                                                This field is set to 1b when software programs the same filter multiple times.
                                                In Signature-based filtering, it is set when software programs a filter with the same
                                                Hash and Signature multiple times. It should be cleared by software when it adds a
                                                Flow.
                                                It might be set by hardware when two flows collide with the same Hash and
                                                Signature.
                                                During reception, this bit is reported on the Rx descriptor of packets that match the
                                                filter.
RESERVED          14:13       00b      RSV      Reserved.
QUEUE_EN            15         0b      RW       Queue Enable
                                                Enable routing matched packet to the queue defined by the RX_QUEUE.
                                                Note: Packets redirection to the FDIRCTRL.DROP_QUEUE is not gated by the
                                                        QUEUE_EN bit.
RX_QUEUE          22:16       0x0      RW       Rx Queue Index
                                                This field defines the absolute Rx queue index in all modes of operation (regardless
                                                of DCB and VT enablement).
TUNNEL_FILTER       23         0b      RSV      Tunnel Filter
                                                If set, the filter is matched by NVGRE or VXLAN packets only. In this case, the L3
                                                and L4 parameters programmed should be of the tunneled (inner) header.
                                                This bit is valid, and should be set, only in IP filtering mode
                                                (FDIRCTRL.FILTERMODE = 000b)
POOL              29:24       0x0      RW       Pool Number
                                                Meaningful when VT mode is enabled. When VT is not enabled, this field must be
                                                set to zero by software.
RESERVED            30         0b      RSV      Reserved.
FD_EXCEPTION        31         0b      RW       Flow Director Exception
                                                If set after a command was given, indicates that a Flow Director exception
                                                occurred.
                                                This bit is a reflection of the EICR.FLOW_DIRECTOR bit (Section 8.2.2.6.1). Should
                                                be set to zero when a new command is given.

8.2.2.15.9                 Flow Director Filters Free - FDIRFREE (0x0000EE38)

      Field     Bit(s)     Init.     Type                                          Description

FREE            15:0       0x0       RW       Free
                                              Number of free (non programmed) filters in the Flow Director filters logic.
RESERVED        31:16      0x0       RSV      Reserved.

8.2.2.15.10                Flow Director Filters DIPv4 Mask - FDIRDIP4M
                           (0x0000EE3C)

      Field     Bit(s)     Init.     Type                                          Description

IPM             31:0       0x0       RW       Mask Destination IPv4 address
                                              Each cleared bit means that the associated bit of the destination IPv4 address is
                                              meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                              bit of the destination IPv4 address is ignored (masked out).
                                              The LS bit of this register matches the first byte on the wire.

692                                                                                                                         333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.15.11            Flow Director Filters Source IPv4 Mask - FDIRSIP4M
                       (0x0000EE40)

      Field   Bit(s)    Init.   Type                                         Description

IPM            31:0     0x0      RW    Mask Source IPv4 address
                                       Each cleared bit means that the associated bit of the source IPv4 address is
                                       meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                       bit of the source IPv4 address is ignored (masked out).The LS bit of this register
                                       matches the first byte on the wire.

8.2.2.15.12            Flow Director Filters TCP Mask - FDIRTCPM (0x0000EE44)

      Field   Bit(s)    Init.   Type                                         Description

SPORTM         15:0     0x0      RW    Mask TCP Source Port
                                       Each cleared bit means that the associated bit of the TCP source port is meaningful for
                                       the filtering functionality. Each bit set to 1b means that the associated bit of the TCP
                                       source port is ignored (masked out).
                                       This field is laid out as follows:
                                        • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                            FDIRPORT.SOURCE (Section 8.2.2.15.5).
                                        • Bit[1] in the mask affects Bit[14] in FDIRPORT.SOURCE.
                                        • ...and so on.
                                        • Bit[15] in the mask affects Bit[0] in FDIRPORT.SOURCE.
DPORTM         31:16    0x0      RW    Mask TCP Destination Port
                                       Each cleared bit means that the associated bit of the TCP destination port is
                                       meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                       bit of the TCP destination Port is ignored (masked out).
                                       This field is laid out as follows:
                                        • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                            FDIRPORT.DESTINATION (Section 8.2.2.15.5).
                                        • Bit[1] in the mask affects Bit[14] in FDIRPORT.DESTINATION.
                                        • ...and so on.
                                        • Bit[15] in the mask affects Bit[0] in FDIRPORT.DESTINATION.

8.2.2.15.13            Flow Director Filters UDP Mask - FDIRUDPM (0x0000EE48)

      Field   Bit(s)    Init.   Type                                         Description

SPORTM         15:0     0x0      RW    Mask UDP Source Port
                                       Each cleared bit means that the associated bit of the UDP source port is meaningful
                                       for the filtering functionality. Each bit set to 1b means that the associated bit of the
                                       UDP source port is ignored (masked out).
                                       This field is laid out as follows:
                                        • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                            FDIRPORT.SOURCE (Section 8.2.2.15.5).
                                        • Bit[1] in the mask affects Bit[14] in FDIRPORT.SOURCE.
                                        • ...and so on.
                                        • Bit[15] in the mask affects Bit[0] in FDIRPORT.SOURCE.

333369-009                                                                                                                    693
                                 Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Programming Interface

      Field    Bit(s)        Init.         Type                                             Description

DPORTM         31:16         0x0           RW          Mask UDP Destination Port
                                                       Each cleared bit means that the associated bit of the UDP destination port is
                                                       meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                                       bit of the UDP destination port is ignored (masked out).
                                                       This field is laid out as follows:
                                                        • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                                            FDIRPORT.DESTINATION (Section 8.2.2.15.5).
                                                        • Bit[1] in the mask affects Bit[14] in FDIRPORT.DESTINATION.
                                                        • ...and so on.
                                                        • Bit[15] in the mask affects Bit[0] in FDIRPORT.DESTINATION.

8.2.2.15.14                 Flow Director Filters Length - FDIRLEN (0x0000EE4C)

       Field       Bit(s)          Init.        Type                                           Description

MAXLEN                5:0            0x0          RC       Maximum Length
                                                           Longest linked list of filters in the table. This field records the length of the
                                                           longest linked list that is updated since the last time this register was read by the
                                                           software. The longest bucket reported by this field includes MAXLEN + 1 filters.
RESERVED              7:6            00b         RSV       Reserved.
BUCKET_LENGTH         13:8           0x0          RC       Bucket Length
                                                           The length of the linked list indicated by a query command. This field is valid
                                                           following a query command completion.
RESERVED           15:14             00b         RSV       Reserved.
MAXHASH            30:16             0x0          RC       Maximum Hash
                                                           The Lookup HASH value of the added filter that updated the value of the MAXLEN
                                                           field in this register.
RESERVED               31            0b          RSV       Reserved.

8.2.2.15.15                 Flow Director Filters Usage Statistics - FDIRUSTAT
                            (0x0000EE50)

      Field    Bit(s)        Init.         Type                                             Description

ADD            15:0          0x0           RC          Added
                                                       Number of added filters. This field counts the number of added filters to the Flow
                                                       Director filters logic. The counter is stuck at 0xFFFF and cleared on read.
REMOVE         31:16         0x0           RC          Removed
                                                       Number of removed filters. This field counts the number of removed filters to the Flow
                                                       Director filters logic. The counter is stuck at 0xFFFF and cleared on read.

8.2.2.15.16                 Flow Director Filters Failed Usage Statistics - FDIRFSTAT
                            (0x0000EE54)

      Field    Bit(s)        Init.         Type                                             Description

FADD            7:0          0x0           RC          Failed Added
                                                       Number of failed added filters due to no space in the filter table. The counter is stuck
                                                       at 0xFF and cleared on read.
FREMOVE        15:8          0x0           RC          Failed Removed
                                                       Number of failed removed filters. The counter is stuck at 0xFF and cleared on read.
RESERVED       31:16         0x0           RSV         Reserved.

694                                                                                                                                 333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.15.17            Flow Director Filters Match Statistics - FDIRMATCH
                       (0x0000EE58)

      Field   Bit(s)    Init.     Type                                          Description

PCNT           31:0     0x0       RC       Packet Count
                                           Number of packets that matched any Flow Director filter. The counter is stacked at
                                           0xFF...F and cleared on read.
                                           Note: This counter might include packets that match the L2 filters, 5 tuple filters, or
                                                    Syn filters, even if they are enabled for queue assignment.

8.2.2.15.18            Flow Director Filters Miss Match Statistics - FDIRMISS
                       (0x0000EE5C)

      Field   Bit(s)    Init.     Type                                          Description

PCNT           31:0     0x0       RC       Packet Count
                                           Number of packets that miss-matched any Flow Director filter. The counter is stacked
                                           at 0xFF...F and cleared on read.

8.2.2.15.19            Flow Director Filters Lookup Table HASH Key - FDIRHKEY
                       (0x0000EE68)

      Field   Bit(s)      Init.          Type                                      Description

KEY            31:0    0x80000001        RW     Key
                                                Programmable hash lookup table key.

8.2.2.15.20            Flow Director Filters Signature HASH Key - FDIRSKEY
                       (0x0000EE6C)

      Field   Bit(s)      Init.          Type                                      Description

KEY            31:0    0x80800101        RW     Key
                                                Programmable signature key.

8.2.2.15.21            Flow Director Filters Other Mask - FDIRM (0x0000EE70)

      Field   Bit(s)    Init.     Type                                          Description

VLANID           0       0b       RW       Mask VLAN ID Tag
                                           When cleared, the 12 bits of the VLAN ID tag are meaningful for the filtering
                                           functionality.
VLANP            1       0b       RW       Mask VLAN Priority Tag
                                           When cleared, the 3 bits of the VLAN Priority are meaningful for the filtering
                                           functionality.
POOL             2       0b       RW       Mask Pool
                                           When cleared, the target Pool number is meaningful for the filtering functionality.
L4P              3       0b       RW       Mask L4 Protocol
                                           When cleared, the UDP/TCP/SCTP protocol type is meaningful for the filtering
                                           functionality.
                                           Note: For the Flow Director filtering aspects, SCTP is treated as if it is TCP.

333369-009                                                                                                                       695
                                   Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

      Field   Bit(s)   Init.   Type                                         Description

FLEX            4       0b     RW     Mask Flexible Tuple
                                      When cleared, the 2 bytes of the Flexible Tuple are meaningful for the filtering
                                      functionality.
DIPV6           5       0b     RW     Mask Destination IPv6
                                      When cleared, the compare against the IP6AT filter is meaningful for IPv6 packets.
L3P             6       0b     RW     Mask IP Type Comparison
                                      To block all IP comparison, the following should also be set: DIPV6 field, FDIRIP6M
                                      register, FDIRSIP4M register, and FDIRDIP4M register (see Section 8.2.2.15.22,
                                      Section 8.2.2.15.11, and Section 8.2.2.15.10, respectively.
RESERVED      31:7     0x0     RSV    Reserved.

8.2.2.15.22            Flow Director Filters IPv6 Mask - FDIRIP6M (0x0000EE74)

      Field   Bit(s)   Init.   Type                                         Description

SIPM          15:0     0x0     RW     Mask Source IPv6 Address
                                      Each cleared bit means that the associated byte of the source IPv6 address is
                                      meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                      byte of the source IPv6 address is ignored (masked out). The LS bit of this register
                                      matches the first byte on the wire.
                                      When working in MACVLAN mode, this field defines the mask to be used to compare
                                      the MAC Address
                                      When working in VXLAN or NVGRE mode, should be used to allow comparison of
                                      TNI/VNI and inner MAC Address:.
DIPM          31:16    0x0     RW     Mask Destination IPv6 Address
                                      Each cleared bit means that the associated byte of the destination IPv6 address is
                                      meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                      byte of the destination IPv6 address is ignored (masked out).
                                      The whole field is meaningful only for the Hash function and the Signature based
                                      filters. The DIPv6 bit in the FDIRM register is meaningful for perfect match filters. The
                                      LS bit of this register matches the first byte on the wire.

8.2.2.15.23            Flow Director Filters SCTP Mask - FDIRSCTPM (0x0000EE78)

      Field   Bit(s)   Init.   Type                                         Description

SPORTM        15:0     0x0     RW     Mask SCTP Source Port
                                      Each cleared bit means that the associated bit of the SCTP source port is meaningful
                                      for the filtering functionality. Each bit set to 1b means that the associated bit of the
                                      SCTP source port is ignored (masked out).
                                      This field is laid out as follows:
                                       • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                           FDIRPORT.SOURCE (Section 8.2.2.15.5).
                                       • Bit[1] in the mask affects Bit[14] in FDIRPORT.SOURCE.
                                       • ...and so on.
                                       • Bit[15] in the mask affects Bit[0] in FDIRPORT.SOURCE.
DPORTM        31:16    0x0     RW     Mask SCTP Destination Port
                                      Each cleared bit means that the associated bit of the SCTP destination port is
                                      meaningful for the filtering functionality. Each bit set to 1b means that the associated
                                      bit of the SCTP destination port is ignored (masked out).
                                      This field is laid out as follows:
                                       • Bit[0] in the mask affects Bit[15] of the source port as defined in
                                           FDIRPORT.DESTINATION (Section 8.2.2.15.5).
                                       • Bit[1] in the mask affects Bit[14] in FDIRPORT.DESTINATION.
                                       • ...and so on.
                                       • Bit[15] in the mask affects Bit[0] in FDIRPORT.DESTINATION.

696                                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.16 PF - MAC Registers

8.2.2.16.1                Highlander Control 0 Register - HLREG0 (0x00004240)

       Field     Bit(s)     Init.    Type                                      Description

RESERVED          1:0       11b      RSV    Reserved.
JUMBOEN            2         0b      RW     Jumbo Frame Enable
                                            Allows frames up to the size specified in Bits[31:16] of the MAXFRS register
                                            (Section 8.2.2.16.6).
                                             0b = Disable jumbo frames (default).
                                             1b = Enable jumbo frames.
RESERVED          9:3       0x7F     RSV    Reserved. Must be set to 0x7F (1111111b).
TXPADEN            10        1b      RW     Tx Pad Frame Enable
                                            Pad short Tx frames to 64 bytes if requested by user.
                                             0b = Transmit short frames with no padding.
                                             1b = Pad frames (default).
RESERVED         14:11      0x5      RSV    Reserved. Must be set to 0x5 (0101b).
LPBK               15        0b      RW     Loopback
                                            Turn on loopback where transmit data is sent back through receiver.
                                             0b = Loopback disabled (default).
                                             1b = Loopback enabled.
MDCSPD             16        1b      RW     MDC Speed
                                            High or low speed MDC clock frequency to PCS, XGXS, WIS, etc.
                                             MDCSPD       Freq at 10 GbE   Freq at 1 GbE Freq at 100 Mb/s
                                                0b          2.4 MHz          240 KHz          240 KHz
                                                1b          24 MHz           2.4 MHz         240 KHz
CONTMDC            17        0b      RW     Continuous MDC
                                            Turn off MDC between MDIO packets.
                                             0b = MDC off between packets (default).
                                             1b = Continuous MDC.
RESERVED         19:18      00b      RSV    Reserved.
PREPEND          23:20      0x0      RW     Prepend Value
                                            Number of 32-bit words, starting after the preamble and SFD, to exclude from the
                                            CRC generator and checker (default = 0x0).
RESERVED         26:24      000b     RSV    Reserved.
RXLNGTHERREN       27        1b      RW     Rx Length Error Reporting
                                             0b = Disable reporting of all rx_length_err events.
                                             1b = Enable reporting of rx_length_err events if length field < 0x0600.
RXPADSTRIPEN       28        0b      RW     Rx Padding Strip Enable
                                             0b = Do not strip padding from Rx packets with length field < 64 (default).
                                             1b = Strip padding from Rx packets with length field < 64 (debug only).
                                            Note: This functionality should be used as debug mode only. If Rx Pad Stripping
                                                   is enabled, the Rx CRC Stripping needs to be enabled as well.
RESERVED         31:29      000b     RSV    Reserved.

333369-009                                                                                                                 697
                                    Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

8.2.2.16.2             Highlander Status 1 Register - HLREG1 (0x00004244)

      Field   Bit(s)   Init.    Type                                        Description

RESERVED       4:0      0x1     RSV    Reserved.
RXERRSYM        5       0b      RO     Rx Error Symbol
                                       Error symbol during Rx packet (latch high, clear on read).
                                        0b = No error symbol (default).
                                        1b = Error symbol received.
RXILLSYM        6       0b      RO     Rx Illegal Symbol
                                       Illegal symbol during Rx packet (latch high, clear on read).
                                         0b = No illegal symbol received (default).
                                         1b = Illegal symbol received.
RXIDLERR        7       0b      RO     Rx Idle Error
                                       Non-idle symbol during idle period (latch high, clear on read).
                                        0b = No idle errors received (default).
                                        1b = Idle error received.
RXLCLFLT        8       0b      RO     Rx Local Fault
                                       Fault reported from PMD, PMA, or PCS (latch high, clear on read).
                                        0b = No local fault (default).
                                        1b = Local fault is or was active.
RXRMTFLT        9       0b      RO     Rx Remote Fault
                                       Link partner reported remote fault (latch high, clear on read).
                                         0b = No remote fault (default).
                                         1b = Remote fault is or was active.
RESERVED      31:10     0x0     RSV    Reserved.

8.2.2.16.3             Pause and Pace Register - PAP (0x00004248)

      Field   Bit(s)   Init.    Type                                        Description

RESERVED      15:0     0xFFFF   RSV    Reserved.
PACE          19:16     0x0     RW     Pace
                                        0000b = 10 Gb/s (LAN)
                                        0001b = 1 Gb/s
                                        0010b = 2 Gb/s
                                        0011b = 3 Gb/s
                                        0100b = 4 Gb/s
                                        0101b = 5 Gb/s
                                        0110b = 6 Gb/s
                                        0111b = 7 Gb/s
                                        1000b = 8 Gb/s
                                        1001b = 9 Gb/s
                                        1010b = Reserved
                                        1011b = Reserved
                                        1100b = Reserved
                                        1101b = Reserved
                                        1110b = Reserved
                                        1111b = 9.294196 Gb/s (WAN)
RESERVED      31:20     0x0     RSV    Reserved.

698                                                                                                         333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.16.4             MDI Single Command and Address - MSCA (0x0000425C)

      Field   Bit(s)    Init.   Type                                         Description

MDIADD         15:0     0x0      RW    MDI Address
                                       Address used for MDI accesses (default = 0x0000).
DEVADD         20:16    0x0      RW    Device Address
                                       Five bits representing device address.
PORTADD        25:21    0x0      RW    Port Address
                                       The address of the PHY port. This field must be set to the port number as reflected in
                                       the STATUS.LAN_ID field (Section 8.2.2.1.2).
OPCODE         27:26    00b      RW    Op Code
                                       Two bits identifying operation to be performed (default - 00b).
                                        00b = Address cycle.
                                        01b = Write operation.
                                        10b = Read, increment address.
                                        11b = Read operation.
RESERVED       29:28    00b      RSV   Reserved. Reads as 00b. Must be written as 00b.
MDICMD          30       0b      RW    MDI Command
                                       Perform the MDI operation in this register. Cleared when done.
                                        0b = MDI ready / Operation complete (default).
                                        1b = Perform operation / Operation in progress.
RESERVED        31       0b      RSV   Reserved.

8.2.2.16.5             MDI Single Read and Write Data - MSRWD (0x00004260)

      Field   Bit(s)    Init.   Type                                         Description

MDIWRDATA      15:0     0x0      RW    MDI Write Data
                                       Write data.
MDIRDDATA      31:16    0x0      RW    MDI Read Data
                                       Read data (RO).

8.2.2.16.6             Max Frame Size - MAXFRS (0x00004268)

      Field   Bit(s)    Init.   Type                                         Description

RESERVED       15:0     0x0      RSV   Reserved.
MFS            31:16   0x5EE     RW    Maximum Frame Size
                                       This field defines the maximum frame size (MFS) in bytes units from Ethernet MAC
                                       Addresses up to and including the CRC. Frames received that are larger than this
                                       value are dropped.
                                       This field is meaningful when jumbo frames are enabled (HLREG0.JUMBOEN = 1b).
                                       When Jumbo frames are not enabled the device uses a hard-wired value of 1518 for
                                       this field.
                                       The MFS does not include the 4 bytes of the VLAN header. Packets with VLAN header
                                       might be as large as MFS + 4.
                                       When Double VLAN is enabled the device adds 8 to the MFS for any packet.
                                       When E-tags are enabled, the device adds 12 to the MFS for any packet.
                                       This value has no effect on transmit frames. It is the responsibility of software to limit
                                       the size of transmit frames.
                                       Note: Packets to/from MC are limited to 2 KB even when jumbo frames are
                                                 enabled.

333369-009                                                                                                                    699
                                 Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                             Programming Interface

8.2.2.16.7                     Link Status Register - LINKS (0x000042A4)

              Field            Bit(s)    Init.     Type                                      Description

FIFO_UNDERRUN                     0       0b         RO      FIFO Underrun
                                                             Indicates underrun condition in MAC elastic FIFO.
FIFO_OVERRUN                      1       0b         RO      FIFO Overrun
                                                             Indicates overrun condition in MAC elastic FIFO.
RF_STATE                          2       0b         RO      Remote Fault State
                                                             MAC is in Remote Fault state.
LF_STATE                          3       0b         RO      Local Fault State
                                                             MAC is in Local Fault state
RESERVED                         6:4     000b       RSV      Reserved.
LINK_STATUS                       7       0b         RO      Link Status
                                                              0b = Link is currently down, or link was down since last time read.
                                                              1b = Link is up, and there was no link down from last time read.
                                                             Self-cleared upon read if the link is low, and set if the link is up.
RESERVED                        26:8     0x0        RSV      Reserved.
NON_STANDARD_SPEED               27       0b         RO      Non-Standard Speed
                                                             If set, the LINK_SPEED field reflects non standard speeds (2.5/5 GbE)
LINK_SPEED                      29:28    00b         RO      Link Speed
                                                             MAC link speed status.
                                                             If NON_STANDARD_SPEED = 0:
                                                               00b = Reserved.
                                                               01b = 100 Mb/s
                                                               10b = 1 GbE
                                                               11b = 10 GbE
                                                             If NON_STANDARD_SPEED = 1:
                                                               00b = Reserved.
                                                               01b = 5 GbE
                                                               10b = Reserved.
                                                               11b = 2.5 GbE
LINK_UP                          30       0b         RO      Link Up
                                                              0b = Link is down.
                                                              1b = Link is up.
RESERVED                         31       0b        RSV      Reserved.

8.2.2.16.8                     MAC Manageability Control Register - MMNGC
                               (0x000042D0)

      Field           Bit(s)   Init.    Type                                           Description

MNG_VETO                0       0b      RO       Management Veto
                                                 MNG_VETO (default 0) access read/write by the management controller, read only to
                                                 the host.
                                                   0b = No specific constraints on link from management controller.
                                                   1b = Hold off any low-power link mode changes. This is done to avoid link loss and
                                                        interrupting management traffic/activity.
RESERVED              31:1     0x0      RSV      Reserved.

700                                                                                                                         333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.16.9             MAC Control Register - MACC (0x00004330)

         Field         Bit(s)   Init.       Type                                  Description

FLU                      0       0b         RW     Force Link Up
                                                    0b = Normal mode.
                                                    1b = MAC is forced to the link up state regardless to the PHY link status.
MAC_RX2TX_LPBK_EN        1       0b         RW     MAC Rx to Tx Loopback Enable
                                                    0b = 0No loopback, normal mode.
                                                    1b = Loopback enabled. Transmit path is driven from the receive path, at
                                                         the MAC internal XGMII interface.
SWIZZLE_TX_DATA          2       0b         RW     Swizzle Tx Data
                                                   Swizzle the bytes in all four MAC internal Tx XGMII lanes.
                                                    0b = Swizzle disabled, normal mode.
                                                    1b = Swizzle enabled.
SWAP_TX_DATA             3       0b         RW     Swap Tx Data
                                                   Swap the MAC internal Tx XGMII lanes.
                                                    0b = Swap disabled, normal mode.
                                                    1b = Swap enabled.
SWAP_TX_CONTROL          4       0b         RW     Swap Tx Control
                                                   Swap the MAC internal Tx XGMII controls.
                                                    0b = Swap disabled, normal mode.
                                                    1b = Swap enabled.
SWIZZLE_RX_DATA          5       0b         RW     Swizzle Rx Data
                                                   Swizzle the bytes in all four MAC internal Rx XGMII lanes.
                                                    0b = Swizzle disabled, normal mode.
                                                    1b = Swizzle enabled.
SWAP_RX_DATA             6       0b         RW     Swap Rx Data
                                                   Swap the MAC internal Rx XGMII lanes.
                                                    0b = Swap disabled, normal mode.
                                                    1b = Swap enabled.
SWAP_RX_CONTROL          7       0b         RW     Swap Rx Control
                                                   Swap the MAC internal Rx XGMII controls.
                                                    0b = Swap disabled, normal mode.
                                                    1b = Swap enabled.
FIFOHT                  11:8     0xD        RW     FIFO High Threshold
                                                   Determines the high threshold of the MAC elastic FIFO.
FIFOLT                 15:12     0x3        RW     FIFO Low Threshold
                                                   Determines the low threshold of the MAC elastic FIFO.
RESERVED               31:16     0x0        RSV    Reserved.

333369-009                                                                                                                  701
                                 Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                              Programming Interface

#### 8.2.2.17 PF - Statistics Registers

All Statistics registers are cleared on read. In addition, they stick at 0xFF...F when the maximum value
is reached.
For the receive statistics, a packet is indicated as received if it passes the device filters and is placed
into the packet buffer memory. A packet does not have to be DMA'd to host memory to be counted as
received.
Due to divergent paths between interrupt generation and logging of relevant statistics counts, it might
be possible to generate an interrupt to the system for a noteworthy event prior to the associated
statistics count actually being incremented. This is extremely unlikely due to expected delays
associated with the system interrupt collection and ISR delay, but might be an explanation for interrupt
statistics values that do not quite make sense. Hardware guarantees that any event noteworthy of
inclusion in a statistics count is reflected in the appropriate count within 1 s; a small time-delay prior
to reading the statistics might be required to avoid a potential mismatch between and interrupt and its
cause.
If RSC is enabled, statistics are collected before RSC is applied to the packets. If TSO is enabled,
statistics are collected after segmentation.
All byte (octet) counters composed of two registers can be fetched by two consecutive 32-bit accesses
while reading the low 32-bit register first, or a single 64-bit access.
All receive statistic counters count the packets and bytes before coalescing by the RSC logic or FCoE
DDP logic. All receive statistic counters in the filter unit might count packets that might be dropped by
the packet buffer or receive DMA. Same comment is valid for the byte counters associated with these
packet counters: PRC64, PRC127, PRC255, PRC511, PRC1023, PRC1522, BPRC, MPRC, GPRC,
RXNFGPC, RUC, and ROC.

8.2.2.17.1             Queue Packets Received Count - QPRC[n] (0x00001030 +
                       0x40*n, n=0...15)

      Field   Bit(s)    Init.   Type                                      Description

PRC           31:0      0x0     RC     Packets Received Count
                                       Number of packets received for the Queue.
                                       FCoE packets are counted in the QRPC even if they are posted only to the DDP queue
                                       (with no traces in the legacy queue).

8.2.2.17.2             Queue Bytes Received Count Low - QBRC_L[n] (0x00001034
                       + 0x40*n, n=0...15)

      Field   Bit(s)    Init.   Type                                      Description

BRC_L         31:0      0x0     RC     Bytes Received Count Low
                                       Lower 32 bits of the statistic counter.
                                       The QBRC_L[n] and QBRC_H[n] registers make up a logical 36-bit counter of received
                                       bytes that were posted to the programmed Rx queues of the packets counted by the
                                       QPRC[n]. The counter counts all bytes posted to the host before VLAN strip.
                                       Furthermore, bytes of RSC and FCoE are counted before coalescing or DDP.

702                                                                                                           333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.3             Queue Bytes Received Count High - QBRC_H[n]
                       (0x00001038 + 0x40*n, n=0...15)

    Field     Bit(s)    Init.   Type                                        Description

BRC_H           3:0     0x0      RC    Bytes Received Count High
                                       Higher 4 bits of the statistic counter described in QBRC_L (Section 8.2.2.17.2).
RESERVED       31:4     0x0      RSV   Reserved.

8.2.2.17.4             Queue Packets Received Drop Count - QPRDC[n]
                       (0x00001430 + 0x40*n, n=0...15)

    Field     Bit(s)    Init.   Type                                        Description

PRDC           31:0     0x0      RC    Packets Received Drop Count
                                       Number of receive packets dropped for the queue.
                                       Packets are dropped per queue in one of three cases:
                                        • Rx Queue is disabled in the RXDCTL[n] register (this includes packets sent to this
                                           queue due to the flow director drop no match mechanism or drop action).
                                        • No free descriptors in the Rx queue while hardware is set to DROP_EN in the
                                           SRRCTL[n] register or in the PFQDE register.
                                        • Packet size is larger than RLPML while RLPML_EN is set in the RXDCTL[n] register.

8.2.2.17.5             Receive Queue Statistic Mapping Registers - RQSMR[n]
                       (0x00002300 + 0x4*n, n=0...31)

These registers define the mapping of the receive queues to the per-queue statistics. Several queues
can be mapped to a single statistic register. Each statistic register counts the number of packets and
bytes of all the queues that are mapped to that statistics. The registers counting Rx queue statistics
are: QPRC, QBRC, and QPRDC. For example, setting RQSMR[0].Q_MAP[0] to “3” maps Rx queue 0 to
the counters QPRC[3], QBRC[3], and QPRDC[3]. Setting RQSMR[2].Q_MAP[1] to “5” maps Rx queue 9
to the QPRC[5], QBRC[5], and QPRDC[5].

    Field     Bit(s)    Init.   Type                                        Description

Q_MAP_0         3:0     0x0      RW    Queue Map 0
                                       For each register ‘n’, Q_MAP[0] defines the per queue statistic registers that are
                                       mapped to Rx queue ‘4*n+0’.
RESERVED        7:4     0x0      RSV   Reserved.
Q_MAP_1        11:8     0x0      RW    Queue Map 1
                                       For each register ‘n’, Q_MAP[1] defines the per queue statistic registers that are
                                       mapped to Rx queue ‘4*n+1’.
RESERVED       15:12    0x0      RSV   Reserved.
Q_MAP_2        19:16    0x0      RW    Queue Map 2
                                       For each register ‘n’, Q_MAP[2] defines the per queue statistic registers that are
                                       mapped to Rx queue ‘4*n+2’.
RESERVED       23:20    0x0      RSV   Reserved.
Q_MAP_3        27:24    0x0      RW    Queue Map 3
                                       For each register ‘n’, Q_MAP[3] defines the per queue statistic registers that are
                                       mapped to Rx queue ‘4*n+3’.
RESERVED       31:28    0x0      RSV   Reserved.

333369-009                                                                                                                  703
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.6             FCoE Rx Packets Dropped Count - FCOERPDC (0x0000241C)

      Field   Bit(s)   Init.   Type                                       Description

RPDC          31:0     0x0     RC     Received Packets Dropped Count
                                      Number of Rx packets dropped due to lack of descriptors.

8.2.2.17.7             Fiber Channel Last Error Count - FCLAST (0x00002424)

      Field   Bit(s)   Init.   Type                                       Description

LAST_CNT      15:0     0x0     RC     Last Count
                                      Number of packets received to valid FCoE contexts while their user buffers are
                                      exhausted.
RESERVED      31:16    0x0     RSV    Reserved.

8.2.2.17.8             FCoE Packets Received Count - FCOEPRC (0x00002428)

      Field   Bit(s)   Init.   Type                                       Description

PRC           31:0     0x0     RC     Packets Received Count
                                      Number of FCoE packets posted to the host.
                                      In nominal operation (no save bad frames) it equals to the number of good packets.

8.2.2.17.9             FCOE DWord Received Count - FCOEDWRC (0x0000242C)

      Field   Bit(s)   Init.   Type                                       Description

DWRC          31:0     0x0     RC     DWord Received Count
                                      Number of DWords count in good received packets with no Ethernet CRC nor FC CRC
                                      errors and that passed successfully DDP.
                                      The counter relates to FCoE packets starting at the FC header up to and including the
                                      FC CRC (it excludes the Ethernet encapsulation).

8.2.2.17.10            Rx DMA Statistic Counter Control - RXDSTATCTRL
                       (0x00002F40)

      Field   Bit(s)   Init.   Type                                       Description

QSEL           4:0     0x0     RW     Queue Select
                                      Controls which Rx queues are considered for the DMA Good Rx and DMA Duplicated
                                      counters as follows:
                                       00000b...01111b = The counters relates to the same queues that are directed to the
                                                           QPRC[QSEL] counter as defined by the RQSMR[n] registers.
                                       10000b =            The counters relates to all Rx queues.
                                       Else =              Reserved.
RESERVED      31:5     0x0     RSV    Reserved.

704                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.11            DMA Good Rx Packet Counter - RXDGPC (0x00002F50)

      Field   Bit(s)    Init.   Type                                       Description

GPC            31:0     0x0      RC    Good Packet Counter
                                       Number of good (non-erred) Rx packets from the Network posted to the host
                                       memory.
                                       In case of packet replication (or mirrored) the counter counts each packet only once.
                                       Note: The counter might count packets directed to ALL Rx queues or specific Rx
                                                queues as defined by the RXDSTATCTRL register (Section 8.2.2.17.10).

8.2.2.17.12            DMA Good Rx Byte Counter Low - RXDGBCL (0x00002F54)

      Field   Bit(s)    Init.   Type                                       Description

GBCL           31:0     0x0      RC    Good Byte Counter Low
                                       Low 32 bits of the 36-bit byte counter of good (non-erred) Rx packets that match the
                                       RXDGPC register (Section 8.2.2.17.11).
                                       The counter counts all bytes posted to the host before VLAN strip. Furthermore, bytes
                                       of RSC and FCoE are counted before coalescing or DDP.

8.2.2.17.13            DMA Good Rx Byte Counter High - RXDGBCH (0x00002F58)

      Field   Bit(s)    Init.   Type                                       Description

GBCH            3:0     0x0      RC    Good Byte Counter High
                                       High 4 bits of the 36-bit byte counter associated with the RXDGBCL register
                                       (Section 8.2.2.17.12).
RESERVED       31:4     0x0      RSV   Reserved.

8.2.2.17.14            DMA Duplicated Good Rx Packet Counter - RXDDPC
                       (0x00002F5C)

      Field   Bit(s)    Init.   Type                                       Description

GPC            31:0     0x0      RC    Good Packet Counter
                                       Number of replicated or mirrored packets that meet the RXDGPC conditions.
                                       The sum of RXDDPC and RXDGPC is the total good (non-erred) Rx packets from the
                                       Network that are posted to the host.
                                       Note: The counter might count packets directed to ALL Rx queues or specific Rx
                                              queues as defined by the RXDSTATCTRL register (Section 8.2.2.17.10).

8.2.2.17.15            DMA Duplicated Good Rx Byte Counter Low - RXDDBCL
                       (0x00002F60)

      Field   Bit(s)    Init.   Type                                       Description

GBCL           31:0     0x0      RC    Good Byte Counter Low
                                       Low 32 bits of the 36-bit byte counter of good (non-erred) Rx packets that match the
                                       RXDDPC register (Section 8.2.2.17.14).
                                       The counter counts all bytes posted to the host before VLAN strip. Furthermore, bytes
                                       of RSC and FCoE are counted before coalescing or DDP.

333369-009                                                                                                               705
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.16            DMA Duplicated Good Rx Byte Counter High - RXDDBCH
                       (0x00002F64)

      Field   Bit(s)   Init.   Type                                       Description

GBCH           3:0     0x0     RC     Good Byte Counter High
                                      High 4 bits of the 36-bit byte counter associated with the RXDDBCL register
                                      (Section 8.2.2.17.15).
RESERVED      31:4     0x0     RSV    Reserved.

8.2.2.17.17            DMA Good Rx LPBK Packet Counter - RXLPBKPC
                       (0x00002F68)

      Field   Bit(s)   Init.   Type                                       Description

GPC           31:0     0x0     RC     Good Packet Counter
                                      Number of good (non-erred) Rx packets from a local VM posted to the host memory.
                                      In case of packet replication (or mirrored) the counter counts each packet only once.
                                      Note: The counter might count packets directed to ALL Rx queues or specific Rx
                                               queues as defined by the RXDSTATCTRL register (Section 8.2.2.17.10).
                                      The counter is not affected by RSC and FCoE DDP, since both functions are not
                                      supported for LPBK traffic.

8.2.2.17.18            DMA Good Rx LPBK Byte Counter Low - RXLPBKBCL
                       (0x00002F6C)

      Field   Bit(s)   Init.   Type                                       Description

GBCL          31:0     0x0     RC     Good Byte Counter Low
                                      Low 32 bits of the 36-bit byte counter of good (non-erred) Rx packets that match the
                                      RXLPBKPC register (Section 8.2.2.17.17).
                                      The counter counts all bytes posted to the host before VLAN strip. Furthermore, bytes
                                      of RSC and FCoE are counted before coalescing or DDP.

8.2.2.17.19            DMA Good Rx LPBK Byte Counter High - RXLPBKBCH
                       (0x00002F70)

      Field   Bit(s)   Init.   Type                                       Description

GBCH           3:0     0x0     RC     Good Byte Counter High
                                      High 4 bits of the 36-bit byte counter associated with the RXLPBKBCL register
                                      (Section 8.2.2.17.18).
RESERVED      31:4     0x0     RSV    Reserved.

706                                                                                                             333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.20            DMA Duplicated Good Rx LPBK Packet Counter - RXDLPBKPC
                       (0x00002F74)

      Field   Bit(s)    Init.   Type                                       Description

GPC            31:0     0x0      RC    Good Packet Counter
                                       Number of replicated or mirrored packets that meet the RXLPBKPC conditions
                                       (Section 8.2.2.17.17).
                                       The sum of RXDLPBKPC and RXLPBKPC is the total good (non-erred) Rx packets from
                                       a local VM posted to the host.
                                       Note: The counter might count packets directed to ALL Rx queues or specific Rx
                                                queues as defined by the RXDSTATCTRL register (Section 8.2.2.17.10).

8.2.2.17.21            DMA Duplicated Good Rx LPBK Byte Counter Low -
                       RXDLPBKBCL (0x00002F78)

      Field   Bit(s)    Init.   Type                                       Description

GBCL           31:0     0x0      RC    Good Byte Counter Low
                                       Low 32 bits of the 36-bit byte counter of good (non-erred) Rx packets that match the
                                       RXDLPBKPC (Section 8.2.2.17.20).
                                       The counter counts all bytes posted to the host before VLAN strip. Furthermore, bytes
                                       of RSC and FCoE are counted before coalescing or DDP.

8.2.2.17.22            DMA Duplicated Good Rx LPBK Byte Counter High -
                       RXDLPBKBCH (0x00002F7C)

      Field   Bit(s)    Init.   Type                                       Description

GBCH            3:0     0x0      RC    Good Byte Counter High
                                       High 4 bits of the 36-bit byte counter associated to RXDLPBKBCL
                                       (Section 8.2.2.17.21).
RESERVED       31:4     0x0      RSV   Reserved.

8.2.2.17.23            BMC2OS Packets Received by Host - B2OGPRC
                       (0x00002F90)

      Field   Bit(s)    Init.   Type                                       Description

B2OGPRC        31:0     0x0      RC    BMC-to-OS Good Packets Received Counter
                                       Counts the total number of packets originating from the BMC that reached the host.
                                       When the internal switch is enabled, each replication of a BMC to host packet is
                                       counted.
                                       The counter is cleared when read by driver. The counter is also cleared by PCIe reset
                                       and software reset. When reaching maximum value, counter does not wrap-around.

333369-009                                                                                                               707
                                 Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

8.2.2.17.24            CRC Error Count - CRCERRS (0x00004000)

      Field   Bit(s)   Init.   Type                                         Description

CEC           31:0     0x0     RC     CRC Error Count
                                      Counts the number of receive packets with CRC errors. For a packet to be counted in
                                      this register, it must be 64 bytes or greater (from <Destination Address> through
                                      <CRC>, inclusively) in length.
                                      This registers counts all packets received, regardless of L2 filtering and receive
                                      enable. This register does not count packets with bad SFD, error control byte, or
                                      illegal code byte.

8.2.2.17.25            Illegal Byte Error Count - ILLERRC (0x00004004)

      Field   Bit(s)   Init.   Type                                         Description

IBEC          31:0     0x0     RC     Illegal Byte Error Count
                                      Counts the number of receive packets with illegal bytes errors (i.e., there is an illegal
                                      symbol in the packet).
                                      This registers counts all packets received, regardless of L2 filtering and receive
                                      enablement.

8.2.2.17.26            Error Byte Packet Count - ERRBC (0x00004008)

      Field   Bit(s)   Init.   Type                                         Description

EBC           31:0     0x0     RC     Error Byte Count
                                      Counts the number of receive packets with Error bytes (i.e., there is an error symbol
                                      in the packet).
                                      This registers counts all packets received, regardless of L2 filtering and receive
                                      enablement.

8.2.2.17.27            MAC Short Packet Discard Count - MSPDC (0x00004010)

      Field   Bit(s)   Init.   Type                                         Description

MSPDC         31:0     0x0     RC     MAC Short Packet Discard Count
                                      Counts the number of MAC short Packet Discard packets received.

8.2.2.17.28            Bad SFD Count - MBSDC (0x00004018)

      Field   Bit(s)   Init.   Type                                         Description

MBSDC         31:0     0x0     RW     MAC Bad SFD Count
                                      Counts the number of packets received with bad SFD.
                                      Does not count short packets not received

8.2.2.17.29            MAC Local Fault Count - MLFC (0x00004034)

      Field   Bit(s)   Init.   Type                                         Description

MLFC          31:0     0x0     RC     MAC Local Fault Count
                                      Counts the number of faults in the local MAC.
                                      This register is valid only when the link speed is 10 GbE.

708                                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.30            MAC Remote Fault Count - MRFC (0x00004038)

    Field     Bit(s)    Init.   Type                                        Description

MRFC           31:0     0x0      RC    MAC Remote Fault Count
                                       Counts the number of faults in the remote MAC.
                                       This register is valid only when the link speed is 10GbE.

8.2.2.17.31            Receive Length Error Count - RLEC (0x00004040)

    Field     Bit(s)    Init.   Type                                        Description

RLEC           31:0     0x0      RC    Receive Length Error Count
                                       Counts the number of packets with receive length errors.
                                       A length error occurs if an incoming Packet Length field in the MAC header does not
                                       match the packet length.
                                       To enable the receive length error count, the HLREG0.RXLNGTHERREN bit must be set
                                       to 1b. (see Section 8.2.2.16.1). This registers counts all packets received, regardless
                                       of L2 filtering and receive enablement.

8.2.2.17.32            Packets Received [64 Bytes] Count - PRC64 (0x0000405C)

    Field     Bit(s)    Init.   Type                                        Description

PRC64          31:0     0x0      RW    Packets Received Count (64 Bytes)
                                       Number of good packets received that are 64 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This registers counts packets that pass L2 filtering regardless of receive enablement,
                                       and does not include received flow control packets.

8.2.2.17.33            Packets Received [65-127 Bytes] Count - PRC127
                       (0x00004060)

    Field     Bit(s)    Init.   Type                                        Description

PRC127         31:0     0x0      RW    Packets Received Count (65-127 Bytes)
                                       Number of packets received that are 65-127 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This registers counts packets that pass L2 filtering regardless of receive enablement,
                                       and does not include received flow control packets.

8.2.2.17.34            Packets Received [128-255 Bytes] Count - PRC255
                       (0x00004064)

    Field     Bit(s)    Init.   Type                                        Description

PRC255         31:0     0x0      RW    Packets Received Count (128-255 Bytes)
                                       Number of packets received that are 128-255 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This registers counts packets that pass L2 filtering regardless of receive enablement,
                                       and does not include received flow control packets.

333369-009                                                                                                                 709
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.35            Packets Received [256-511 Bytes] Count - PRC511
                       (0x00004068)

      Field   Bit(s)   Init.   Type                                       Description

PRC511        31:0     0x0     RW     Packets Received Count (256-511 Bytes)
                                      Number of packets received that are 256-511 bytes in length (from <Destination
                                      Address> through <CRC>, inclusively).
                                      This registers counts packets that pass L2 filtering regardless of receive enablement,
                                      and does not include received flow control packets.

8.2.2.17.36            Packets Received [512-1023 Bytes] Count - PRC1023
                       (0x0000406C)

      Field   Bit(s)   Init.   Type                                       Description

PRC1023       31:0     0x0     RW     Packets Received Count (512-1023 Bytes)
                                      Number of packets received that are 512-1023 bytes in length (from <Destination
                                      Address> through <CRC>, inclusively).
                                      This registers counts packets that pass L2 filtering regardless of receive enablement,
                                      and does not include received flow control packets.

8.2.2.17.37            Packets Received [1024 to Max Bytes] Count - PRC1522
                       (0x00004070)

      Field   Bit(s)   Init.   Type                                       Description

PRC1522       31:0     0x0     RW     Packets Received Count (1024-Max Bytes)
                                      Number of packets received that are 1024-Max bytes in length (from <Destination
                                      Address> through <CRC>, inclusively).
                                      This registers counts packets that pass L2 filtering regardless on receive enablement
                                      and does not include received flow control packets.
                                      The maximum is dependent on the current receiver configuration and the type of
                                      packet being received. If a packet is counted in Receive Oversized Count, it is not
                                      counted in this register.
                                      Due to changes in the standard for maximum frame size for VLAN tagged frames in
                                      802.3, this device accepts packets which have a maximum length of 1522 bytes. The
                                      RMON statistics associated with this range has been extended to count 1522 byte long
                                      packets.

8.2.2.17.38            Good Packets Received Count - GPRC (0x00004074)

      Field   Bit(s)   Init.   Type                                       Description

GPRC          31:0     0x0     RO     Good Packets Received Count
                                      Number of good (non-erred) Rx packets (from the network) that pass L2 filtering and
                                      have legal length.
                                      This registers counts packets regardless of receive enable, and does not count flow
                                      control packets.

710                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.39            Broadcast Packets Received Count - BPRC (0x00004078)

    Field     Bit(s)    Init.   Type                                        Description

BPRC           31:0     0x0      RO    Broadcast Packets Received Count
                                       Number of good (non-erred) broadcast packets received.
                                       This register does not count received broadcast packets when the broadcast address
                                       filter is disabled. The counter counts packets regardless of receive enablement.

8.2.2.17.40            Multicast Packets Received Count - MPRC (0x0000407C)

    Field     Bit(s)    Init.   Type                                        Description

MPRC           31:0     0x0      RO    Multicast Packets Received Count
                                       Number of good (non-erred) multicast packets received that pass L2 filtering
                                       (excluding Broadcast packets).
                                       This register does not count received flow control packets. This register counts
                                       packets regardless of receive enablement.

8.2.2.17.41            Good Packets Transmitted Count - GPTC (0x00004080)

    Field     Bit(s)    Init.   Type                                        Description

GPTC           31:0     0x0      RC    Good Packets Transmitted Count
                                       Number of good packets transmitted. This register counts good (non-erred)
                                       transmitted packets.
                                       A good transmit packet is considered one that is 64 or more bytes (from <Destination
                                       Address> through <CRC>, inclusively) in length. The register counts transmitted
                                       clear packets, secure packets and FC packets.

8.2.2.17.42            Good Octets Received Count Low - GORCL (0x00004088)

    Field     Bit(s)    Init.   Type                                        Description

CNT_L          31:0     0x0      RC    Count Low
                                       Lower 32 bits of the “Good Octets Received” counter.
                                       The GORCL and GORCH registers make up a logical 36-bit octet counter of the
                                       packets counted by the GPRC (see Section 8.2.2.17.38). This register includes bytes
                                       received in a packet from the Destination Address field through the CRC field,
                                       inclusively.

8.2.2.17.43            Good Octets Received Count High - GORCH (0x0000408C)

    Field     Bit(s)    Init.   Type                                        Description

CNT_H           3:0     0x0      RC    Count High
                                       Higher 4 bits of the “Good Octets Received” counter associated with the GORCL
                                       register (Section 8.2.2.17.42).
RESERVED       31:4     0x0      RSV   Reserved.

333369-009                                                                                                                711
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.44            Good Octets Transmitted Count Low - GOTCL (0x00004090)

      Field   Bit(s)   Init.   Type                                       Description

CNT_L         31:0     0x0     RC     Count Low
                                      Lower 32 bits of the “Good Octets Transmitted” counter.
                                      The GOTCL and GOTCH registers make up a logical 36-bit counter of successfully
                                      transmitted octets (in packets counted by GPTC – see Section 8.2.2.17.41). This
                                      register includes transmitted bytes in a packet from the Destination Address field
                                      through the CRC field, inclusively.

8.2.2.17.45            Good Octets Transmitted Count High - GOTCH (0x00004094)

      Field   Bit(s)   Init.   Type                                       Description

CNT_H          3:0     0x0     RC     Count High
                                      Higher 4 bits of the “Good Octets Transmitted” counter associated with the GOTCL
                                      register (Section 8.2.2.17.44).
RESERVED      31:4     0x0     RSV    Reserved.

8.2.2.17.46            Receive Undersize Count - RUC (0x000040A4)

      Field   Bit(s)   Init.   Type                                       Description

RUC           31:0     0x0     RC     Receive Undersize Error
                                      This register counts the number of received frames that are shorter than minimum
                                      size (64 bytes from <Destination Address> through <CRC>, inclusively), and had a
                                      valid CRC.
                                      This register counts packets regardless of L2 filtering and receive enablement.
                                      This register does not count packets with SFD errors or packets discarded by the MAC
                                      layer (e.g. packets smaller than 12 bytes).

8.2.2.17.47            Receive Fragment Count - RFC (0x000040A8)

      Field   Bit(s)   Init.   Type                                       Description

RFC           31:0     0x0     RC     Receive Fragment Count
                                      Number of receive fragment errors (frame shorter than 64 bytes from <Destination
                                      Address> through <CRC>, inclusively) that have bad CRC (this is slightly different
                                      from the Receive Undersize Count (RUC) register).
                                      This register counts packets regardless of L2 filtering and receive enablement.

8.2.2.17.48            Receive Oversize Count - ROC (0x000040AC)

      Field   Bit(s)   Init.   Type                                       Description

ROC           31:0     0x0     RC     Receive Oversize Error
                                      This register counts the number of received frames that are longer than maximum
                                      size as defined by MAXFRS.MFS (from <Destination Address> through <CRC>,
                                      inclusively) and have valid CRC.
                                      This register counts packets regardless of L2 filtering and receive enablement.
                                      This register does not count packets with SFD errors or packets discarded by the MAC
                                      layer (e.g. packets smaller than 12 bytes).

712                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.49            Receive Jabber Count - RJC (0x000040B0)

      Field   Bit(s)    Init.   Type                                      Description

RJC            31:0     0x0      RC    Receive Jabber Count
                                       This register counts the number of received packets regardless of L2 filtering and
                                       receive enablement, and are greater than maximum size and have bad CRC (this is
                                       slightly different from the Receive Oversize Count register).
                                       The packets length is counted from <Destination Address> through <CRC>,
                                       inclusively. This register counts packets regardless of L2 filtering and receive
                                       enablement.

8.2.2.17.50            Management Packets Received Count - MNGPRC
                       (0x000040B4)

      Field   Bit(s)    Init.   Type                                      Description

MNGPRC         31:0     0x0      RO    Management Packets Received Count
                                       This register counts the total number of packets received that pass the management
                                       filters.
                                       Management packets include RMCP and ARP packets. SFD errors and short packets
                                       are not counted, except that packets dropped because the management receives a
                                       jumbo packet or because the receive FIFO is full are counted.

8.2.2.17.51            Management Packets Dropped Count - MNGPDC
                       (0x000040B8)

      Field   Bit(s)    Init.   Type                                      Description

MPDC           31:0     0x0      RO    Management Packets Dropped Count
                                       This register counts the total number of packets received that pass the management
                                       filters and then are dropped because of one of the following:
                                         • The management receive FIFO is full or disabled.
                                         • A packet bigger than the maximal allowed size is received.
                                         • A packet length mismatch.
                                       The maximum allowed size is 1518 + the size of any recognized L2 header (VLAN,
                                       extended VLAN, E-tag, etc.).
                                       Management packets include any packet directed to the manageability console (such
                                       as RMCP and ARP packets).

8.2.2.17.52            Total Octets Received Low - TORL (0x000040C0)

      Field   Bit(s)    Init.   Type                                      Description

CNT_L          31:0     0x0      RC    Counter Low
                                       Lower 32 bits of the “Total Octets Received” counter.
                                       The TORL and TORH registers make up a logical 36-bit counter of the total received
                                       octets (in the packets counted by the TPR counter – see Section 8.2.2.17.54). This
                                       register includes bytes received in a packet from the Destination Address field
                                       through the CRC field, inclusively.

333369-009                                                                                                              713
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.53            Total Octets Received High - TORH (0x000040C4)

      Field   Bit(s)   Init.   Type                                       Description

CNT_H          3:0     0x0     RC     Counter High
                                      Higher 4 bits of the “Total Octets Received” counter associated with the TORL register
                                      (Section 8.2.2.17.52).
RESERVED      31:4     0x0     RSV    Reserved.

8.2.2.17.54            Total Packets Received - TPR (0x000040D0)

      Field   Bit(s)   Init.   Type                                       Description

TPR           31:0     0x0     RC     Total Packets Received
                                      This register counts the total number of all packets received.
                                      All packets received are counted in this register, regardless of their length, whether
                                      they are erred, regardless on L2 filtering and receive being enabled but excluding
                                      Flow Control packets. The TPR might count packets interrupted by link disconnect
                                      although they have a CRC error.
                                      This register does not count packets with SFD errors, or packets discarded by the MAC
                                      layer (e.g. packets smaller than 12 bytes).

8.2.2.17.55            Total Packets Transmitted - TPT (0x000040D4)

      Field   Bit(s)   Init.   Type                                       Description

TPT           31:0     0x0     RC     Total Packets Transmitted
                                      This register counts the total number of all packets transmitted.
                                      This register counts all packets, including standard packets, secure packets, FC
                                      packets, and manageability packets.

8.2.2.17.56            Packets Transmitted [64 Bytes] Count - PTC64
                       (0x000040D8)

      Field   Bit(s)   Init.   Type                                       Description

PTC64         31:0     0x0     RC     Packets Transmitted Count (64 bytes)
                                      Number of packets transmitted that are 64 bytes in length (from <Destination
                                      Address> through <CRC>, inclusively).
                                      This register counts all packets, including standard packets, secure packets, FC
                                      packets, and manageability packets.

8.2.2.17.57            Packets Transmitted [65-127 Bytes] Count - PTC127
                       (0x000040DC)

      Field   Bit(s)   Init.   Type                                       Description

PTC127        31:0     0x0     RC     Packets Transmitted Count (65-127 bytes)
                                      Number of packets transmitted that are 65-127 bytes in length (from <Destination
                                      Address> through <CRC>, inclusively).
                                      This register counts all packets, including standard packets, secure packets, FC
                                      packets, and manageability packets.

714                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.58            Packets Transmitted [128-255 Bytes] Count - PTC255
                       (0x000040E0)

    Field     Bit(s)    Init.   Type                                       Description

PTC255         31:0     0x0      RC    Packets Transmitted Count (128-255 bytes)
                                       Number of packets transmitted that are 128-255 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This register counts all packets, including standard packets, secure packets, FC
                                       packets, and manageability packets.

8.2.2.17.59            Packets Transmitted [256-511 Bytes] Count - PTC511
                       (0x000040E4)

    Field     Bit(s)    Init.   Type                                       Description

PTC511         31:0     0x0      RC    Packets Transmitted Count (256-511 bytes)
                                       Number of packets transmitted that are 265-511 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This register counts all packets, including standard packets, secure packets, FC
                                       packets, and manageability packets.

8.2.2.17.60            Packets Transmitted [512-1023 Bytes] Count - PTC1023
                       (0x000040E8)

    Field     Bit(s)    Init.   Type                                       Description

PTC1023        31:0     0x0      RC    Packets Transmitted Count (512-1023 bytes)
                                       Number of packets transmitted that are 512-1023 bytes in length (from <Destination
                                       Address> through <CRC>, inclusively).
                                       This register counts all packets, including standard packets, secure packets, FC
                                       packets, and manageability packets.

8.2.2.17.61            Packets Transmitted [Greater than 1024 Bytes] Count -
                       PTC1522 (0x000040EC)

    Field     Bit(s)    Init.   Type                                       Description

PTC1522        31:0     0x0      RC    Packets Transmitted Count (Greater Than 1024 bytes)
                                       Number of packets transmitted that are 1024 or more bytes in length (from
                                       <Destination Address> through <CRC>, inclusively).
                                       This register counts all packets, including standard packets, secure packets, and
                                       manageability packets.
                                       Due to changes in the standard for maximum frame size for VLAN tagged frames in
                                       802.3, this device transmits packets which have a maximum length of 1522 bytes.
                                       The RMON statistics associated with this range has been extended to count 1522-byte
                                       long packets. This register counts all packets, including standard and secure packets.

333369-009                                                                                                                715
                                 Did this document help answer your questions?

                                                                             Intel® Ethernet Controller X550 Datasheet
                                                                                               Programming Interface

8.2.2.17.62            Multicast Packets Transmitted Count - MPTC (0x000040F0)

      Field   Bit(s)   Init.   Type                                       Description

MPTC          31:0     0x0     RC     Multicast Packets Transmitted Count
                                      This register counts the number of multicast packets transmitted.
                                      This register counts all packets, including standard packets, secure packets, FC
                                      packets and manageability packets.

8.2.2.17.63            Broadcast Packets Transmitted Count - BPTC (0x000040F4)

      Field   Bit(s)   Init.   Type                                       Description

BPTC          31:0     0x0     RC     Broadcast Packets Transmitted Count
                                      This register counts the number of broadcast packets transmitted. This register
                                      counts all packets, including standard packets, secure packets, FC packets and
                                      manageability packets

8.2.2.17.64            XSUM Error Count - XEC (0x00004120)

      Field   Bit(s)   Init.   Type                                       Description

XEC           31:0     0x0     RC     ESUM Error Count
                                      Number of receive IPv4, TCP, UDP or SCTP XSUM errors.
                                      Note: XSUM errors are not counted when a packet has any MAC error (CRC, length,
                                             under-size, over-size, byte error, or symbol error).

8.2.2.17.65            Priority XON Received Count - PXONRXCNT[n] (0x00004140
                       + 0x4*n, n=0...7)

      Field   Bit(s)   Init.   Type                                       Description

XONRXC        15:0     0x0     RC     XON Receive Count
                                      Number of XON packets received per UP. Sticks at 0xFFFF.
RESERVED      31:16    0x0     RSV    Reserved.

8.2.2.17.66            Priority XOFF Received Count - PXOFFRXCNT[n]
                       (0x00004160 + 0x4*n, n=0...7)

      Field   Bit(s)   Init.   Type                                       Description

XOFFRXC       15:0     0x0     RC     XOFF Receive Count
                                      Number of XOFF packets received per UP. Sticks at 0xFFFF.
RESERVED      31:16    0x0     RSV    Reserved.

716                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.67              Total Unicast Packets Received (BMC copy) - BUPRC
                         (0x00004180)

Note:        This register is available to the firmware only.

    Field       Bit(s)   Init.   Type                                        Description

BUPRC            31:0    0x0      RC    BMC Unicast Packets Received Count
                                        This register counts the number of good (no errors) unicast packets received from the
                                        network.
                                        This register does not count unicast packets received that fail to pass address
                                        filtering. This register does not count packets counted by the Missed Packet Count
                                        (MPC) register. This register does not count flow control packets. Packets sent to the
                                        manageability engine are included in this counter.

8.2.2.17.68              BMC Total Multicast Packets Received - BMPRC
                         (0x00004184)

Note:        This register counts the same events as the MPRC register (Section 8.2.2.17.40) for the BMC
             usage. This register is available to the firmware only.

    Field       Bit(s)   Init.   Type                                        Description

BMPRC            31:0    0x0      RC    BMC Multicast Packets Received Count
                                        Number of good (non-erred) multicast packets received that pass L2 filtering
                                        (excluding Broadcast packets).
                                        This register does not count received flow control packets. This registers counts
                                        packets regardless of receive enablement.

8.2.2.17.69              Total Broadcast Packets Received (BMC copy) - BBPRC
                         (0x00004188)

Note:        This register counts the same events as the BPRC register (Section 8.2.2.17.39) for the BMC
             usage. This register is available to the firmware only.

    Field       Bit(s)   Init.   Type                                        Description

BBPRC            31:0    0x0      RC    BMC Broadcast Packets Received Count
                                        Number of good (non-erred) broadcast packets received to BMC.
                                        This register does not count received broadcast packets when the broadcast address
                                        filter is disabled. The counter counts packets regardless on receive enablement.

8.2.2.17.70              Total Unicast Packets Transmitted (BMC copy) - BUPTC
                         (0x0000418C)

Note:        This register is available to the firmware only.

    Field       Bit(s)   Init.   Type                                        Description

BUPTC            31:0    0x0      RC    BMC Unicast Packets Transmitted Count
                                        Number of unicast packets transmitted.

333369-009                                                                                                                  717
                                  Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.17.71               BMC Total Multicast Packets Transmitted - BMPTC
                          (0x00004190)

Note:         This register counts the same events as the MPTC register (Section 8.2.2.17.62) for the BMC
              usage. This register is available to the firmware only.

      Field      Bit(s)   Init.   Type                                        Description

BMPTC             31:0    0x0     RC     BMC Multicast Packets Transmitted Count
                                         Number of multicast packets transmitted.
                                         This register counts the number of multicast packets transmitted. This register counts
                                         all packets, including standard packets, secure packets, FC packets and manageability
                                         packets.

8.2.2.17.72               Total Broadcast Packets Transmitted (BMC copy) - BBPTC
                          (0x00004194)

Note:         This register counts the same events as the BPTC register (Section 8.2.2.17.63) for the BMC
              usage. This register is available to the firmware only.

      Field      Bit(s)   Init.   Type                                        Description

BBPTC             31:0    0x0     RC     BMC Broadcast Packets Transmitted Count
                                         Number of broadcast packets transmitted count.
                                         This register counts all packets, including standard packets, secure packets, FC
                                         packets and manageability packets

8.2.2.17.73               BMC FCS Receive Errors - BCRCERRS (0x00004198)

Note:         This register counts the same events as the CRCERRS register (Section 8.2.2.17.24) for the
              BMC usage. This register is available to the firmware only.

      Field      Bit(s)   Init.   Type                                        Description

BCEC              31:0    0x0     RC     BMC CRC Error Count
                                         Counts the number of receive packets with CRC errors.
                                         For a packet to be counted in this register, it must be 64 bytes or greater (from
                                         <Destination Address> through <CRC>, inclusively) in length. This registers counts
                                         all packets received, regardless of L2 filtering and receive enablement.

8.2.2.17.74               BMC Pause XON Frames Received - BXONRXC (0x0000419C)

Note:         This register counts the same events as the LXONRXCNT register (Section 8.2.2.17.75) for
              the BMC usage. This register is available to the firmware only.

      Field      Bit(s)   Init.   Type                                        Description

BXONRXC           15:0    0x0     RC     BMC XON Received Count
                                         Number of XON packets received. Sticks at 0xFFFF.
                                         XON packets can use the global address, or the station address. This register counts
                                         any XON packet whether it is a legacy XON or a priority XON. Each XON packet is
                                         counted once even if it designated to a few priorities. If a priority FC packet contains
                                         both XOFF and XON, only the LXOFFRXCNT counter is incremented.
RESERVED         31:16    0x0     RC     Reserved

718                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.75            Link XON Received Count - LXONRXCNT (0x000041A4)

      Field   Bit(s)    Init.   Type                                        Description

XONRXC         15:0     0x0      RC    XON Received Count
                                       Number of XON packets Received. Sticks at 0xFFFF.
                                       XON packets can use the global address, or the station address. This register counts
                                       any XON packet whether it is a legacy XON or a priority XON. Each XON packet is
                                       counted once even if it designated to a few priorities. If a priority FC packet contains
                                       both XOFF and XON, only the LXOFFRXCNT counter is incremented.
RESERVED       31:16    0x0      RSV   Reserved.

8.2.2.17.76            Link XOFF Received Count - LXOFFRXCNT (0x000041A8)

      Field   Bit(s)    Init.   Type                                        Description

XOFFRXC        15:0     0x0      RC    XOFF Received Count
                                       Number of XOFF packets Received. Sticks at 0xFFFF.
                                       XOFF packets can use the global address, or the station address. This register counts
                                       any XOFF packet whether it is a legacy XOFF or a priority XOFF. Each XOFF packet is
                                       counted once even if it designated to a few priorities. If a priority FC packet contains
                                       both XOFF and XON, only this counter is incremented.
RESERVED       31:16    0x0      RSV   Reserved.

8.2.2.17.77            Good Rx Non-Filtered Packet Counter - RXNFGPC
                       (0x000041B0)

      Field   Bit(s)    Init.   Type                                        Description

GPC            31:0     0x0      RC    Good Packet Counter
                                       Number of good (non-erred with legal length) Rx packets (from the network)
                                       regardless of packet filtering and receive enablement.

8.2.2.17.78            Good Rx Non-Filter Byte Counter Low - RXNFGBCL
                       (0x000041B4)

      Field   Bit(s)    Init.   Type                                        Description

BCL            31:0     0x0      RC    Byte Counter Low
                                       Low 32 bits of the 36-bit byte counter of good (non-erred) Rx packets that match the
                                       RXNFGPC register (Section 8.2.2.17.77).
                                       The counter counts all bytes from Destination Address field through the CRC field,
                                       inclusively.

8.2.2.17.79            Good Rx Non-Filter Byte Counter High - RXNFGBCH
                       (0x000041B8)

      Field   Bit(s)    Init.   Type                                        Description

BCH             3:0     0x0      RC    Byte Counter High
                                       High 4 bits of the 36-bit byte counter associated with the RXFGBCL register
                                       (Section 8.2.2.17.78).
RESERVED       31:4     0x0      RSV   Reserved.

333369-009                                                                                                                  719
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.17.80               BMC2OS Packets Sent by BMC - B2OSPC (0x000041C0)

      Field      Bit(s)   Init.   Type                                        Description

B2OSPC            31:0    0x0     RC     BMC-to-OS Packet Count
                                         BMC2OS packets sent by BMC.
                                         This register counts the total number of transmitted packets sent from the
                                         manageability path that were sent to host. This includes packets received by the host
                                         and packet dropped in the device due to congestion conditions.
                                         Counter is cleared when read by driver. Counter is also cleared by PCIe reset and
                                         software reset. When reaching maximum value, counter does not wrap-around.

8.2.2.17.81               OS2BMC Packets Received by BMC - O2BGPTC
                          (0x000041C4)

      Field      Bit(s)   Init.   Type                                        Description

O2BGPTC           31:0    0x0     RC     OS-to-BMC Good Packets Transmitted Count
                                         This register counts the total number of packets originating from the host that
                                         reached the NC-SI interface. This includes packets sent from the host to the BMC or
                                         consumed by the internal manageability engine.
                                         Counter is cleared when read by driver. Counter is also cleared by PCIe reset and
                                         software reset. When reaching maximum value, counter does not wrap-around.

8.2.2.17.82               BMC Pause XOFF Frames Received - BXOFFRXC
                          (0x000041E0)

Note:         This register counts the same events as the LXOFFRXCNT register (Section 8.2.2.17.76) for
              the BMC usage. This register is available to the firmware only.

      Field      Bit(s)   Init.   Type                                        Description

BXOFFRXC          15:0    0x0     RC     BMC XOFF Received Count
                                         Number of XOFF packets received. Sticks at 0xFFFF.
                                         XOFF packets can use the global address, or the station address. This register counts
                                         any XOFF packet whether it is a legacy XOFF or a priority XOFF. Each XOFF packet is
                                         counted once even if it designated to a few priorities. If a priority FC packet contains
                                         both XOFF and XON, only this counter is incremented.
RESERVED         31:16    0x0     RC     Reserved

8.2.2.17.83               BMC Pause XON Frames Transmitted - BXONTXC
                          (0x000041E4)

      Field      Bit(s)   Init.   Type                                        Description

BXONTXC           15:0    0x0     RC     BMC XON Transmitted Count
                                         Number of XON packets Transmitted. Sticks at 0xFFFF.
                                         BXONTXC is incremented by one for each Link XON packet when MFLCN.RFCE is set
                                         and for each Priority XON packet when corresponding MFLCN.RPFCE bit is set (see
                                         Section 8.2.2.3.6).
RESERVED         31:16    0x0     RC     Reserved.

720                                                                                                                  333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.84              BMC Pause XOFF Frames Transmitted - BXOFFTXC
                         (0x000041E8)

    Field       Bit(s)   Init.   Type                                      Description

BXOFFTXC         15:0    0x0     RC     BMC XOFF Transmitted Count
                                        Number of XOFF packets Transmitted. Sticks at 0xFFFF.
                                        BXOFFTXC is incremented by one for each Link XOFF packet when MFLCN.RFCE is set
                                        and for each Priority XOFF packet when corresponding MFLCN.RPFCE bit is set (see
                                        Section 8.2.2.3.6).
RESERVED        31:16    0x0     RC     Reserved.

8.2.2.17.85              Sideband Receive Dropped Packet Count - B2OSDPC
                         (0x000041F0)

Note:        Although the name is B2OSDPC, this counter includes all drops from the BMC, even if sent to
             LAN. This counter is shared between all ports, and counts events of packets dropped
             regardless of their destination port.

    Field       Bit(s)   Init.   Type                                      Description

B2OSDPC          31:0    0x0     RW     BMC-to-OS Dropped Packet Count
                                        Counts the number of packets received from the BMC interface receive that were
                                        dropped.
                                        The following causes can create a drop:
                                         • Memory buffer full.
                                         • Pause packet.
                                         • PT packet without SA match or requires enables.
                                         • MCTP drop (unsupported message type).
                                         • Length error.
                                         • Reject by specific interface (SMBus abort, MCTP reject, RMII reject).

8.2.2.17.86              Fiber Channel CRC Error Count - FCCRC (0x00005118)

    Field       Bit(s)   Init.   Type                                      Description

CRC_CNT          15:0    0x0     RC     FC CRC Count
                                        Counts the number of packets with good Ethernet CRC and bad FC CRC.
RESERVED        31:16     X      RSV    Reserved.

8.2.2.17.87              Queue Packets Transmitted Count - QPTC_ALIAS[n]
                         (0x00006030 + 0x40*n, n=0...15; RC)

Field definitions are the same as those defined in Section 8.2.2.17.89.

333369-009                                                                                                               721
                                  Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.17.88               Transmit Queue Statistic Mapping Registers - TQSM[n]
                          (0x00008600 + 0x4*n, n=0...31)

These registers define the mapping of the transmit queues to the per-queue statistics. Several queues
can be mapped to a single statistic register. Each statistic register counts the number of packets and
bytes of all the queues that are mapped to that statistics. The registers counting Tx queue statistics are
QPTC and QBTC (refer to Section 8.2.2.17.89, Section 8.2.2.17.90, and Section 8.2.2.17.91).

      Field      Bit(s)   Init.   Type                                        Description

Q_MAP_0           3:0     0x0     RW     Queue Map 0
                                         For each register ‘n’, Q_MAP[0] defines the per queue statistic registers that are
                                         mapped to Tx queue ‘4*n+0’.
RESERVED          7:4     0x0     RSV    Reserved.
Q_MAP_1          11:8     0x0     RW     Queue Map 1
                                         For each register ‘n’, Q_MAP[1] defines the per queue statistic registers that are
                                         mapped to Tx queue ‘4*n+1’.
RESERVED         15:12    0x0     RSV    Reserved.
Q_MAP_2          19:16    0x0     RW     Queue Map 2
                                         For each register ‘n’, Q_MAP[2] defines the per queue statistic registers that are
                                         mapped to Tx queue ‘4*n+2’.
RESERVED         23:20    0x0     RSV    Reserved.
Q_MAP_3          27:24    0x0     RW     Queue Map 3
                                         For each register ‘n’, Q_MAP[3] defines the per queue statistic registers that are
                                         mapped to Tx queue ‘4*n+3’.
RESERVED         31:28    0x0     RSV    Reserved.

8.2.2.17.89               Queue Packets Transmitted Count - QPTC[n] (0x00008680
                          + 0x4*n, n=0...15)

Note:         Additional address(es): 0x06030 + 0x40*n, n=0...15

      Field      Bit(s)   Init.   Type                                        Description

PTC              31:0     0x0     RC     Packets Transmitted Count
                                         Number of packets transmitted for the Queue.
                                         A packet is considered as transmitted if it is forwarded to the MAC unit for
                                         transmission to the network and/or is accepted by the internal Tx-to-Rx switch
                                         enablement logic. Packets dropped due to anti-spoofing filtering, or traffic sent to the
                                         BMC and blocked due to security violations, or loopback packets that are rejected by
                                         the Tx-to-Rx switch, are not counted.

8.2.2.17.90               Queue Bytes Transmitted Count Low - QBTC_L[n]
                          (0x00008700 + 0x8*n, n=0...15)

      Field      Bit(s)   Init.   Type                                        Description

BTC_L            31:0     0x0     RC     Bytes Transmitted Count Low
                                         Lower 32 bits of the statistic counter.
                                         The QBTC_L and QBTC_H registers make up a logical 36-bit counter of transmitted
                                         bytes of the packets counted by the matched QPTC counter. These registers count all
                                         bytes in the packets from the Destination Address field through the CRC field,
                                         inclusively. These registers must be accessed as two consecutive 32-bit entities while
                                         QBTC_L register is read first, or a single 64-bit read cycle. Each register is read-
                                         cleared. In addition, it sticks at 0xFF...F to avoid overflow.

722                                                                                                                  333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.17.91            Queue Bytes Transmitted Count High - QBTC_H[n]
                       (0x00008704 + 0x8*n, n=0...15)

      Field   Bit(s)    Init.   Type                                       Description

BTC_H           3:0     0x0      RC    Bytes Transmitted Count High
                                       Higher 4 bits of the statistic counter described in QBTC_L (Section 8.2.2.17.90).
RESERVED       31:4     0x0      RSV   Reserved.

8.2.2.17.92            Switch Security Violation Packet Count - SSVPC
                       (0x00008780)

      Field   Bit(s)    Init.   Type                                       Description

SSVPC          31:0     0x0      RC    Switch Security Violation Packet Count
                                       This register counts all Tx packets dropped. For example, packets dropped due to
                                       switch security violations such as SA or VLAN anti-spoof filtering, or packet that has
                                       (inner) VLAN that contradicts with PFVMVIR register definitions. Valid only in VMDq or
                                       IOV mode.
                                       This counter includes also traffic sent to the BMC and blocked due to security
                                       violations. or packets dropped due to malicious events detection.

8.2.2.17.93            FCoE Packets Transmitted Count - FCOEPTC (0x00008784)

      Field   Bit(s)    Init.   Type                                       Description

PTC            31:0     0x0      RC    Packets Transmitted Count
                                       Number of FCoE packets transmitted.
                                       The counter does not include packets dropped due to anti-spoofing filtering or VLAN
                                       tag validation. This rule is applicable if FCoE traffic is sent by a VF.

8.2.2.17.94            FCoE DWord Transmitted Count - FCOEDWTC (0x00008788)

      Field   Bit(s)    Init.   Type                                       Description

DWTC           31:0     0x0      RC    DWord Transmitted Count
                                       Number of DWords count in transmitted packets.
                                       The counter relates to FCoE packets starting at the FC header up to and including the
                                       FC CRC (it excludes the Ethernet encapsulation).

8.2.2.17.95            DMA Good Tx Packet Counter - TXDGPC (0x000087A0)

      Field   Bit(s)    Init.   Type                                       Description

GPTC           31:0     0x0      RC    Good Packets Transmitted Count
                                       Number of Tx packets from host memory.
                                       This counter includes packets that are transmitted to the external network as well as
                                       packets that are transmitted only to local VMs. The later occurs only in VT mode when
                                       the local switch is enabled. Dropped packets counted in SSVPC register are not
                                       counted here.

333369-009                                                                                                                 723
                                 Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                              Programming Interface

8.2.2.17.96            DMA Good Tx Byte Counter Low - TXDGBCL (0x000087A4)

      Field   Bit(s)   Init.   Type                                       Description

BCL           31:0     0x0     RC     Byte Counter Low
                                      The low 32 bits of the 36-bit byte counter of the Tx packets that match the TXDGPC
                                      register (Section 8.2.2.17.95).
                                      The counter counts all bytes posted by the host and the VLAN (if bytes are added by
                                      hardware). Dropped packets counted in SSVPC register are not counted here.

8.2.2.17.97            DMA Good Tx Byte Counter High - TXDGBCH (0x000087A8)

      Field   Bit(s)   Init.   Type                                       Description

BCH            3:0     0x0     RC     Byte Counter High
                                      High 4 bits of the 36-bit byte counter associated with the TXDGBCL register
                                      (Section 8.2.2.17.96).
RESERVED      31:4     0x0     RSV    Reserved.

8.2.2.17.98            OS2BMC Packets Transmitted by Host - O2BSPC
                       (0x000087B0)

      Field   Bit(s)   Init.   Type                                       Description

O2BPC         31:0     0x0     RC     OS-to-BMC Packet Count
                                      OS2BMC packets transmitted count.
                                      Counts the total number of packets originating from the functions that were sent to
                                      the manageability path. This includes packets received by the BMC and packet
                                      dropped in the X550 due to congestion conditions or due to anti-spoof check.
                                      Counter is cleared when read by driver. Counter is also cleared by PCIe reset and
                                      software reset. When reaching maximum value counter does not wrap-around.

724                                                                                                            333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.18 PF - Wake-Up and Proxy Control Registers

8.2.2.18.1             Wake-Up Control Register - WUC (0x00005800)

The PME_EN and PME_STATUS bits are reset when LAN_PWR_GOOD is 0. When AUX_PWR=0, these
bits are also reset by the assertion of PE_RST_N.

      Field   Bit(s)    Init.   Type                                        Description

RESERVED         0       0b      RSV   Reserved.
PME_EN           1       0b      RW    PME Enable
                                       This bit is used by the software device driver to read the PME_En bit of the Power
                                       Management Control/Status Register (PMCSR) without writing to the PCIe
                                       configuration space.
                                       Writing a 1b to this bit clears it.
                                       Note: Software should not modify this bit while PME enablement is active.
PME_STATUS       2       0b     RW1C   PME Status
                                       This bit is set when the X550 receives a wake-up event. It is the same as the
                                       PME_Status bit in the Power Management Control/Status Register (PMCSR).
                                       Writing a 1b to this bit clears it. The PME_Status bit in the PMCSR register is also
                                       cleared.
RESERVED         3       0b      RSV   Reserved.
WKEN             4       1b      RW    Wake Enable
                                       This bit can be cleared to disable the PE_WAKE_N pin assertion (= 0) even if APM is
                                       enabled in the NVM. In this case, PMCSR and WUS wake-up statuses are invalid.
                                       Note: This bit should not be cleared while in ACPI mode.
RESERVED       31:5     0x0      RSV   Reserved.

8.2.2.18.2             Wake-Up Filter Control Register - WUFC (0x00005808)

This register is used to enable each of the pre-defined and flexible filters for wake-up support. A value
of 1b means the filter is turned on, and a value of 0b means the filter is turned off.

      Field   Bit(s)    Init.   Type                                        Description

LNKC             0       0b      RW    Link Status Change Wake-up Enable
MAG              1       0b      RW    Magic Packet Wake-up Enable
EX               2       0b      RW    Directed Exact Wake-up Enable
MC               3       0b      RW    Directed Multicast Wake-up Enable
                                       Setting this bit does not enable broadcast packets, which are enabled by the BC bit in
                                       this register.
BC               4       0b      RW    Broadcast Wake-up Enable
ARP              5       0b      RW    ARP/IPv4 Request Packet Wake-up Enable
IPV4             6       0b      RW    Directed IPv4 Packet Wake-up Enable
IPV6             7       0b      RW    Directed IPv6 Packet Wake-up Enable
RESERVED       14:8     0x0      RSV   Reserved.
NOTCO           15       0b      RW    No TCO
                                       Ignore TCO/managements packets for wake-up.
                                        0b = Ignore all TCO/management packets for wake-up, except packets that meet
                                              the criteria defined in the MNGONLY register via the Host Enable field (for
                                              example, criteria intended for the host as well as to the MC).
                                        1b = Ignore all TCO/management packets for wake-up. While in normal operation,
                                              this ignore is forwarded to the host as well as to the MC.
FLX0            16       0b      RW    Flexible Filter 0 Enable
                                       Controls the usage of the FHFT[0] register (0x9000).

333369-009                                                                                                                    725
                                 Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

      Field   Bit(s)   Init.   Type                                        Description

FLX1           17       0b     RW     Flexible Filter 1 Enable
                                      Controls the usage of the FHFT[1] register (0x9100).
FLX2           18       0b     RW     Flexible Filter 2 Enable
                                      Controls the usage of the FHFT[2] register (0x9200).
FLX3           19       0b     RW     Flexible Filter 3 Enable
                                      Controls the usage of the FHFT[3] register (0x9300).
FLX4           20       0b     RW     Flexible Filter 4 Enable
                                      Controls the usage of the FHFT[0] register (0x9600).
FLX5           21       0b     RW     Flexible Filter 5 Enable
                                      Controls the usage of the FHFT[5] register (0x9700).
FLX6           22       0b     RW     Flexible Filter 6 Enable
                                      Controls the usage of the FHFT[6] register (0x9800).
FLX7           23       0b     RW     Flexible Filter 7 Enable
                                      Controls the usage of the FHFT[7] register (0x9900).
RESERVED      30:24    0x0     RSV    Reserved.
FW_RST_WK      31       0b     RW     Enable Wake on Firmware Reset Assertion
                                      When set, a firmware reset causes a system wake-up that enables the software driver
                                      to resend proxying information to firmware.

8.2.2.18.3             Wake-Up Status Register - WUS (0x00005810)

This register is used to record statistics about all wake-up packets received. If a packet matches
multiple criteria, multiple bits are set by hardware. Software writing a 1b to any bit clears that bit.
This register is not cleared when PE_RST_N is asserted. It is only cleared when LAN_PWR_GOOD is
de-asserted, or when cleared by the driver.

      Field   Bit(s)   Init.   Type                                        Description

LNKC            0       0b     RW1C   Link Status Changed
                                      This bit can be set even if another event is already set.
MAG             1       0b     RW1C   Magic Packet Received
EX              2       0b     RW1C   Directed Exact Packet Received
                                      The packet's address matched one of the 16 pre-programmed exact values in the
                                      Receive Address registers.
MC              3       0b     RW1C   Directed Multicast Packet Received
                                      The packet was a multicast packet that's hashed to a value that corresponds to a 1 bit
                                      in the Multicast Table Array.
BC              4       0b     RW1C   Broadcast Packet Received
ARP             5       0b     RW1C   ARP/IPv4 Request Packet Received
IPV4            6       0b     RW1C   Directed IPv4 Packet Received
IPV6            7       0b     RW1C   Directed IPv6 Packet Received
MNG             8       0b     RW1C   Manageability
                                      Indicates that a manageability event that should cause a PME to happen.
RESERVED      15:9     0x0     RSV    Reserved.
FLX0           16       0b     RW1C   Flexible Filter 0 Match
FLX1           17       0b     RW1C   Flexible Filter 1 Match
FLX2           18       0b     RW1C   Flexible Filter 2 Match
FLX3           19       0b     RW1C   Flexible Filter 3 Match
FLX4           20       0b     RW1C   Flexible Filter 4 Match

726                                                                                                              333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field   Bit(s)    Init.   Type                                          Description

FLX5            21       0b     RW1C   Flexible Filter 5 Match
FLX6            22       0b     RW1C   Flexible Filter 6 Match
FLX7            23       0b     RW1C   Flexible Filter 7 Match
RESERVED       30:24    0x0      RSV   Reserved.
FW_RST_WK       31       0b     RW1C   Wake Due to Firmware Reset Assertion Event
                                       When set to 1b, indicates that asserting a firmware reset causes the system wake-up
                                       so the software driver can re-send proxying information to firmware.
                                       This bit can be set even if another event is already set.

8.2.2.18.4             IP Address Valid - IPAV (0x00005838)

This register indicates whether the IP Addresses in the IP Address Table are valid.

      Field   Bit(s)    Init.   Type                                          Description

V40              0       0b      RW    IPv4 Address 0 Valid
                                       Loaded from NVM.
V41              1       0b      RW    IPv4 Address 1 Valid
V42              2       0b      RW    IPv4 Address 2 Valid
V43              3       0b      RW    IPv4 Address 3 Valid
RESERVED       15:4     0x0      RSV   Reserved.
V60             16       0b      RW    IPv6 Address 0 Valid
V61             17       0b      RW    IPv6 Address 1 Valid
V62             18       0b      RW    IPv6 Address 2 Valid
V63             19       0b      RW    IPv6 Address 3 Valid
RESERVED       31:20    0x0      RSV   Reserved.

8.2.2.18.5             IPv4 Address Table - IP4AT[n] (0x00005840 + 0x8*n,
                       n=0...3)

4 x IPv4 addresses for ARP/IPv4 Request packet and Directed IPv4 packet wake-up. IPv4[0] is loaded
from MIPAF words in the NVM.

      Field   Bit(s)    Init.   Type                                          Description

IPV4ADDR       31:0      X       RW    IPv4 Address
                                       IPv4 Address ‘n’, where ‘n’ = 0...3.

8.2.2.18.6             IPv6 Address Table - IP6AT[n] (0x00005880 + 0x4*n,
                       n=0...3)

First IPv6 addresses for Neighbor Discovery packet filtering and Directed IPv6 packet wake-up.

      Field   Bit(s)    Init.   Type                                          Description

IPV6ADDR       31:0      X       RW    IPv6 Address
                                       4 x Register IPv6 filter. Register ‘n’ contains bytes ‘4*n’ up to ‘4*n+3’ of the IPv6
                                       address. LS byte of register ‘0’ is first on the wire.

333369-009                                                                                                                     727
                                 Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

8.2.2.18.7                   Wake-Up Packet Length - WUPL (0x00005900)

This register is de-featured and software should not access it (read or write).

8.2.2.18.8                   IPv6 Address Table Extended - IP6AT_EXT[n] (0x00005990
                             + 0x4*n, n=0...11)

3 x IPv6 addresses for Neighbor Discovery packet filtering.

      Field       Bit(s)     Init.      Type                                           Description

IPV6ADDR           31:0       X         RW       IPv6 Address
                                                 4 x Register IPv6 filter. Register ‘n’ contains bytes ‘4*n’ up to ‘4*n+3’ of the IPv6
                                                 address. LS byte of register '0' is first on the wire.

8.2.2.18.9                   Wake-Up Packet Memory (128 Bytes) - WUPM[n]
                             (0x00005A00 + 0x4*n, n=0...31)

      Field       Bit(s)     Init.      Type                                           Description

WUPD               31:0       X         RO       Wake-Up Packet Data
                                                 This register is used to store the first 128 bytes of the wake-up packet for software
                                                 retrieval after the system wakes up. It should not be cleared by any reset including
                                                 master reset.

8.2.2.18.10                  Proxying Status Register - PROXYS (0x00005F60)

This register is used to record statistics about all proxying packets received. If a packet matches
multiple criteria, multiple bits could be set. Writing a 1b to any bit clears that bit.
This register is not cleared when RST# is asserted. It is only cleared when LAN_PWR_GOOD is
de-asserted, or when cleared by the software device driver.
Note:          If additional packets are received that match one of the wake-up filters, after the original
               wake-up packet is received, the PROXYS register is updated with the matching filters
               accordingly.

       Field        Bit(s)     Init.      Type                                          Description

RESERVED              1:0         00b     RSV      Reserved.
EX                     2          0b     RW1C      Exact Packet Received
RESERVED              4:3         00b     RSV      Reserved.
ARP_DIRECTED           5          0b     RW1C      ARP Directed Received
                                                   ARP request packet with IP4AT filter match received.
                                                   When set to 1b, indicates a match on any ARP request packet that passed main
                                                   filtering and Target IP Address also matches one of the valid IP4AT filters.
RESERVED              8:6      000b       RSV      Reserved.
NS                     9          0b     RW1C      IPV6 Neighbor Solicitation Received
                                                   When set to 1b, indicates a match on NS packet that passed main filtering.
NS_DIRECTED           10          0b     RW1C      IPV6 Neighbor Solicitation with Directed DA Match Received.
                                                   When set to 1b, indicates a match on NS packet and Target IP Address also
                                                   matches IP6AT filter.
ARP                   11          0b     RW1C      ARP Request Packet Received
                                                   When set to 1b, indicates a match on ARP request packet that passed main
                                                   filtering.

728                                                                                                                           333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field      Bit(s)     Init.    Type                                     Description

MLD                12        0b     RW1C    IPv6 Multicast Listener Discovery (MLD) Packet Received
                                            When set to 1b, indicates a match on any of the following MLD packet types that
                                            passed main filtering:
                                             • Multicast Listener Query (ICMPv6 Type = decimal 130). Defined in MLDv1 and
                                                MLDv2.
                                             • Multicast Listener Report (ICMPv6 Type = decimal 131). Defined in MLDv1 and
                                                MLDv2.
                                             • Version 2 Multicast Listener Report Message (ICMPv6 Type = decimal 143).
                                                Defined in MLDv2 only.
RESERVED         31:13      0x0      RSV    Reserved.

8.2.2.18.11               Proxying Filter Control Register - PROXYFC (0x00005F64)

This register is used to enable each of the pre-defined filters for Proxying support. This register is not
cleared when RST# is asserted. It is only cleared when LAN_PWR_GOOD is de-asserted, or when
cleared by the software device driver.

      Field      Bit(s)     Init.    Type                                     Description

PPROXYE            0         0b      RW     Port Proxying Enable
                                            When set to 1b, proxying of packets is enabled when device is in D3 low power
                                            state. Proxy information and requirements is passed by software driver to firmware
                                            via the host interface.
RESERVED           1         0b      RSV    Reserved.
EX                 2         0b      RW     Exact Proxying Enable
RESERVED          4:3       00b      RSV    Reserved.
ARP_DIRECTED       5         0b      RW     ARP Request Packet and IP4AT MATCH Proxy Enable
                                            If set to 1b, forward to Management for proxying on match of any ARP request
                                            packet that passed main filtering and Target IP Address also matches one of the
                                            valid IP4AT filters.
RESERVED          8:6       000b     RSV    Reserved.
NS                 9         0b      RW     IPV6 Neighbor Solicitation Proxy Enable
                                            If set to 1b, forward to Management for proxying on match of any NS packet
                                            (ICMPv6 type 135) that passed main filtering.
NS_DIRECTED        10        0b      RW     IPV6 Neighbor Solicitation and Directed DA Match Proxy Enable
                                            If set to 1b, forward to Management for proxying on match of NS packet and
                                            Target IP Address also matches valid IP6AT filter.
ARP                11        0b      RW     ARP Request Packet Proxy Enable
                                            If set to 1b, forward to Management for proxying on match of any ARP request
                                            packet that passed main filtering.
MLD                12        0b      RW     IPv6 Multicast Listener Discovery (MLD) Proxy Enable
                                            If set to 1b, forward to Management for Proxying on match of any of the following
                                            MLD packet types that passed main filtering:
                                             • Multicast Listener Query (ICMPv6 Type = decimal 130). Defined in MLDv1 and
                                                 MLDv2.
                                             • Multicast Listener Report (ICMPv6 Type = decimal 131). Defined in MLDv1 and
                                                 MLDv2.
                                             • Version 2 Multicast Listener Report Message (ICMPv6 Type = decimal 143).
                                                 Defined in MLDv2 only.
RESERVED         14:13      00b      RSV    Reserved.
NOTCO              15        0b      RW     Ignore TCO/Management Packets For Proxying
                                             0b = Ignore only TCO/management packets for Proxying that meet the criteria
                                                  defined in the MNGONLY register (i.e., are intended only for the BMC and
                                                  not the Host).
                                             1b = Ignore any TCO/management packets for proxying, even if in normal
                                                  operation it is forwarded to the Host in addition to the BMC.

333369-009                                                                                                                 729
                                    Did this document help answer your questions?

                                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Programming Interface

      Field      Bit(s)         Init.           Type                                          Description

RESERVED         31:16           0x0            RSV      Reserved.

8.2.2.18.12               Filter DW Even - FHFT_FILTER_DW_EVEN[n,m]
                          (0x00009000 + 0x10*n + 0x100*m, n=0...15, m=0...3 and
                          0x00009600 + 0x10*(n-16) + 0x100*m, n=16...31,
                          m=0...3)

Notes:
 • The mask field must be 8 bytes aligned even if the length field is not 8 bytes aligned, as hardware
   implementation compares 8 bytes at a time. Therefore, it should get extra masks until the end of
   the next quad word. Any mask bit that is located after the length should be set to 0b, indicating no
   comparison should be done.
 • In case the actual length defined by the length field register and the mask bits is not 8 bytes
   aligned, there might be a case that a packet which is shorter than the actual required length passes
   the flexible filter. This might happen due to comparison of up to 7 bytes that come after the packet,
   but are not a real part of the packet.
 • The last DW of each filter contains a length field defining the number of bytes from the beginning of
   the packet compared by this filter. If actual packet length is less than length specified by this field,
   the filter fails. Otherwise, it depends on the result of actual byte comparison. The value should not
   be greater than 128.

       Field        Bit(s)          Init.          Type                                         Description

FHFT_FILTER0_DW0     31:0               X             RW      FHFT Filter DW Even
                                                              Even DW of the flex filter.

8.2.2.18.13               Filter DW Odd - FHFT_FILTER_DW_ODD[n,m] (0x00009004
                          + 0x10*n + 0x100*m, n=0...15, m=0...3 and 0x00009604 +
                          0x10*(n-16) + 0x100*m, n=16...31, m=0...3)

       Field        Bit(s)          Init.          Type                                         Description

FHFT_FILTER0_DW1     31:0               X             RW      FHFT Filter DW Odd
                                                              Odd DW of the flex filter.

8.2.2.18.14               Filter Mask - FHFT_FILTER_MASK[n,m] (0x00009008 +
                          0x10*n + 0x100*m, n=0...15, m=0...3 and 0x00009608 +
                          0x10*(n-16) + 0x100*m, n=16...31, m=0...3)

         Field        Bit(s)            Init.          Type                                      Description

FHFT_FILTER0_MASK         7:0               X          RW      FHFT Filter Mask
                                                               Bit mask for the 8 bytes of the filter (bit per byte).
RESERVED                  31:8          0x0            RSV     Reserved.

730                                                                                                                          333369-009
                                            Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.18.15            Filter Length - FHFT_FILTER_LENGTH[n,m] (0x0000900C +
                       0x10*n + 0x100*m, n=0...15, m=0...3 and 0x0000960C +
                       0x10*(n-16) + 0x100*m, n=16...31, m=0...3)

    Field     Bit(s)    Init.   Type                                         Description

LENGTH          7:0     0x0      RW    Flex Filter Length
                                       The LENGTH field is only valid on the last DW of the filter. All other length fields are
                                       reserved.
RESERVED       31:8     0x0      RSV   Reserved.

333369-009                                                                                                                    731
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

#### 8.2.2.19 PF - Management Filters Registers

The Management Filters registers are RO for the host. These registers are initialized at LAN Power Good
and can be loaded from the NVM by the manageability firmware.

8.2.2.19.1                Management VLAN TAG Value - MAVTV[n] (0x00005010 +
                          0x4*n, n=0...7)

      Field      Bit(s)    Init.   Type                                       Description

VID               11:0     0x0     RW     VLAN ID
                                          Contains the VLAN ID that should be compared with the incoming packet.
RESERVED         31:12     0x0     RSV    Reserved.

8.2.2.19.2                Management Flex UDP/TCP Ports - MFUTP[n] (0x00005030
                          + 0x4*n, n=0...7)

Note:         Each 32-bit register (n=0,...,7) refers to two port filters (register 0 refers to ports 0 and 1,
              register 2 refers to ports 2 and 3, etc.). SCTP packets do not match the MFUTP filters. MFUTP
              filters are programmed in Network order.

      Field      Bit(s)    Init.   Type                                       Description

MFUTP_2N          15:0     0x0     RW     Management Flex UDP/TCP Port 2n
                                          (2n)-th Management Flex UDP/TCP port.
MFUTP_2N_1       31:16     0x0     RW     Management Flex UDP/TCP Port 2n+1
                                          (2n+1)-th Management Flex UDP/TCP port.

8.2.2.19.3                BMC IP Address Register - BMCIP[n] (0x00005050 + 0x4*n,
                          n=0...3)

These registers contain the BMC IP Address table.

      Field      Bit(s)    Init.   Type                                       Description

IPADDR            31:0     0x0     RW     IP Address
                                          4 bytes of 16-bytes destination IP Address of the BMC.
                                           • n=0 contains the MSB for an IPv6 IP Address.
                                           • n=3 contains an IPv4 IP Address or the LSB for an IPv6 IP Address.
                                          For an IPv4 address, BMCIP 0...2 must be written with zeros.
                                          Note: This field is defined in Big Endian (LS byte is first on the wire).

732                                                                                                                   333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.19.4                BMC IP Valid Register - BMCIPVAL (0x00005060)

This register indicates the type of IP Address stored in the IPVAL register, and indicates if a valid
address is stored.

     Field       Bit(s)    Init.      Type                                       Description

IPADDR_TYPE          0      0b         RW     IP Address Type
                                               0b = IPv4
                                               1b = IPv6
IPADDR_VALID         1      0b         RW     IP Address Valid
                                               0b = IP Address in BMCIP is not valid.
                                               1b = IP Address in BMCIP is valid.
RESERVED         31:2      0x0        RSV     Reserved.

8.2.2.19.5                Manageability Decision Filters Ext - MDEF_EXT[n]
                          (0x00005160 + 0x4*n, n=0...7)

             Field                 Bit(s)    Init.    Type                                Description

L2_ETHERTYPE_AND                    3:0      0x0       RW     L2 EtherType AND
                                                              Controls the inclusion of L2 EtherType filtering in the manageability
                                                              filter decision (AND section).
L2_ETHERTYPE_OR                     7:4      0x0       RW     L2 EtherType OR
                                                              Controls the inclusion of L2 EtherType filtering in the manageability
                                                              filter decision (OR section).
FLEX_PORT                          23:8      0x0       RW     Flex Port
                                                              Controls the inclusion of Flex port filtering in the manageability
                                                              filter decision (OR section). Bit 8 corresponds to flex port 0, etc.
FLEX_TCO                            24        0b       RW     Flex TCO
                                                              Controls the inclusion of Flex TCO filtering in the manageability
                                                              filter decision (OR section). Bit 24 corresponds to Flex TCO filter 0.
                                                              Note: Supported only for Network traffic.
ND_135                              25        0b       RW     Neighbor Discovery 135
                                                              Controls the inclusion of Neighbor Solicitation neighbor Discovery
                                                              filtering in the manageability filter decision (OR section).
                                                              Notes:
                                                                1. Supported only for Network traffic.
                                                                2. Neighbor Discovery types supported by this bit is 0x87 (135d)
                                                                    - Neighbor Solicitation
ND_136                              26        0b       RW     Neighbor Discovery 136
                                                              Controls the inclusion of Neighbor Advertisement Neighbor
                                                              Discovery filtering in the manageability filter decision (OR section).
                                                              Notes:
                                                               1. Supported only for Network traffic.
                                                               2. Neighbor Discovery types supported by this bit is 0x88 (136d)
                                                                  - Neighbor Advertisement
ND_137                              27        0b       RW     Neighbor Discovery 137
                                                              Controls the inclusion of Redirect neighbor Discovery filtering in the
                                                              manageability filter decision (OR section).
                                                              Notes:
                                                               1. Supported only for Network traffic.
                                                               2. Neighbor Discovery types supported by this bit is 0x89 (137d)
                                                                  - Redirect
RESERVED                            28        0b       RSV    Reserved.

333369-009                                                                                                                           733
                                      Did this document help answer your questions?

                                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                                     Programming Interface

                Field                      Bit(s)         Init.      Type                                 Description

MLD                                            29          0b         RW      MLD
                                                                              Controls the inclusion of MLD packets.
                                                                              These are ICMPv6 packets with the following types: 130, 131, 132,
                                                                              143.
APPLY_TO_NETWORK_TRAFFIC                       30          0b         RW      Apply to Network Traffic
                                                                               0b = Do not apply this decision filter to traffic received from the
                                                                                    network.
                                                                               1b = Apply this decision filter to traffic received from the network.
APPLY_TO_HOST_TRAFFIC                          31          0b         RW      Apply to Host Traffic
                                                                               0b = This decision filter does not apply to traffic received from the
                                                                                    host.
                                                                               1b = This decision filter applies to traffic received from the host.

8.2.2.19.6                      Management Ethernet Type Filters - METF[n] (0x00005190
                                + 0x4*n, n=0...3)

      Field       Bit(s)         Init.         Type                                             Description

ETYPE              15:0          0x0           RW      EtherType
                                                       EtherType value to be compared against the L2 EtherType field in the Rx packet.
                                                       Note: Appears in Little Endian order (high byte first on the wire).
RESERVED           29:16         0x0           RSV     Reserved.
POLARITY            30            0b           RW      Polarity
                                                        0b = Positive filter — Filter enters the decision filters if a match occurred.
                                                        1b = Negative filter — Filter enters the decision filters if a match did not occur.
RESERVED            31            0b           RSV     Reserved.

8.2.2.19.7                      Management Control Register - MANC (0x00005820)

        Field           Bit(s)         Init.        Type                                           Description

FC_DISCARD                 0             0b          RW         Flow Control Discard
                                                                 0b = Apply filtering rules to packets with Flow Control EtherType.
                                                                 1b = Discard packets with Flow Control EtherType.
                                                                Note: Flow Control EtherType is 0x8808
NCSI_DISCARD               1             0b          RW         NC-SI Discard
                                                                 0b = Apply filtering rules to packets with NC-SI EtherType.
                                                                 1b = Discard packets with NC-SI EtherType.
                                                                Note: NC-SI EtherType is 0x88F8
RESERVED                 16:2            0x0         RSV        Reserved.
RCV_TCO_EN                 17            0b          RW         Receive TCO Packets Enabled
                                                                When this bit is set, it enables the receive flow to the manageability block. This
                                                                bit should be set only if at least one of EN_BMC2OS or EN_BMC2NET bits are set.
RESERVED                22:18            0x0         RSV        Reserved.
EN_XSUM_FILTER             23            0b          RW         Enable XSUM Filter
                                                                When this bit is set, enables XSUM filtering to Manageability, meaning only
                                                                packets that pass L3/L4 checksum are sent to the manageability block.
                                                                Note: This capability is not provided for tunneled packets.
EN_IPV4_FILTER             24            0b          RW         Enable IPv4 address Filters
                                                                 0b = These bits store a single IPv6 filter.
                                                                 1b = The last 128 bits of the MIPAF register (Section 8.2.2.19.10) are used to
                                                                      store 4 IPv4 addresses for IPv4 filtering.

734                                                                                                                                     333369-009
                                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field       Bit(s)         Init.         Type                                        Description

FIXED_NET_TYPE      25            0b           RW      Fixed Net Type
                                                        0b = Both tagged and un-tagged packets might be forwarded to manageability
                                                             engine.
                                                        1b = Only packets matching the net type defined by the NET_TYPE field pass to
                                                             manageability.
NET_TYPE            26            0b           RW      Net Type
                                                        0b = Pass only un-tagged packets.
                                                        1b = Pass only VLAN tagged packets.
                                                       Valid only if FIXED_NET_TYPE is set.
Reserved            27            0b           RSV     Reserved.
EN_BMC2OS           28            0b           RW      Enable BMC-to-OS and OS-to-BMC traffic
                                                         0b = The BMC cannot communicate with the OS.
                                                         1b = The BMC can communicate with the OS.
                                                       When cleared, the BMC traffic is not forwarded to the OS, even if the Host MAC
                                                       Address filter and VLANs (RAH/L, MTA, VFTA and PFVLVF registers) indicate that it
                                                       should.
                                                       When cleared the OS traffic is not forwarded to the BMC even if the decision
                                                       filters indicates it should. This bit does not impact the BMC to Network traffic.
                                                       Note: This bit can change while the host is sending or receiving traffic.
EN_BMC2NET          29            0b           RW      Enable BMC-to-Network and Network-to-BMC traffic
                                                         0b = The BMC cannot communicate with the network.
                                                         1b = The BMC can communicate with the network
                                                       When cleared the BMC traffic is not forwarded to the network and the network
                                                       traffic is not forwarded to the BMC even if the decision filters indicates it should.
                                                       This bit does not impact the host to BMC traffic.
                                                       Note: This bit can change while the host is sending or receiving traffic.
PROXYEN             30            0b           RW      Proxy Enable
                                                       Set by firmware to indicate that proxy offload is supported.
RESERVED            31            0b           RSV     Reserved.

8.2.2.19.8               Manageability Only Traffic - MNGONLY (0x00005864)

        Field           Bit(s)         Init.      Type                                       Description

EXCLUSIVE_TO_MNG         7:0             0x0         RW    Exclusive to MNG
                                                           When set, indicates that packets forwarded by the manageability filters to
                                                           manageability are not sent to the host. Bits 0...7 correspond to decision rules
                                                           defined in registers MDEF[0...7] and MDEF_EXT[0...7] (Section 8.2.2.19.9).
RESERVED                 31:8            0x0         RSV   Reserved

8.2.2.19.9               Manageability Decision Filters - MDEF[n] (0x00005890 +
                         0x4*n, n=0...7)

      Field       Bit(s)         Init.         Type                                        Description

EXACT_AND          3:0           0x0           RW      Exact AND
                                                       Controls the inclusion of Exact MAC Address 0 to 3.
                                                       In the manageability filter decision (AND section). Bit 0 corresponds to exact MAC
                                                       Address 0 (MMAL0 and MMAH0), etc.
BROADCAST_AND       4             0b           RW      Broadcast AND
                                                       Controls the inclusion of broadcast address filtering in the manageability filter
                                                       decision (AND section).

333369-009                                                                                                                                 735
                                          Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

      Field     Bit(s)   Init.     Type                                       Description

VLAN_AND        12:5     0x0        RW    VLAN AND
                                          Controls the inclusion of VLAN tag 0 to 7, respectively.
                                          In the manageability filter decision (AND section). Bit 5 corresponds to VLAN tag
                                          0, etc.
IPV4_ADDRESS    16:13    0x0        RW    IPv4 Address
                                          Controls the inclusion of IPV4 address 0 to 3 (MIPAF[3,n]) respectively in the
                                          manageability filter decision (AND section). Bit 13 corresponds to IPV4 address 0,
                                          etc.
                                          Notes:
                                           1. This field is relevant only if MANC.EN_IPv4_FILTER is set
                                               (Section 8.2.2.19.7).
                                           2. Supported only for Network traffic.
IPV6_ADDRESS    20:17    0x0        RW    IPv6 Address
                                          Controls the inclusion of IPV6 address 0 to 3 respectively (MIPAF[0:3,n]) in the
                                          manageability filter decision (AND section). Bit 17 corresponds to IPV6 address 0,
                                          etc
                                          Notes:
                                           1. Bit 20 is relevant only if MANC.EN_IPv4_FILTER is cleared
                                              (Section 8.2.2.19.7).
                                           2. Supported only for Network traffic.
EXACT_OR        24:21    0x0        RW    Exact OR
                                          Controls the inclusion of exact MAC Address 0 to 3.
                                          In the manageability filter decision (OR section). Bit 21 corresponds to exact MAC
                                          Address 0 (MMAL0 and MMAH0), etc.
BROADCAST_OR     25       0b        RW    Broadcast OR
                                          Controls the inclusion of broadcast address filtering in the manageability filter
                                          decision (OR section).
MULTICAST_AND    26       0b        RW    Multicast OR
                                          Controls the inclusion of Multicast address filtering in the manageability filter
                                          decision (AND section).
                                          Broadcast packets are not included by this bit.
ARP_REQUEST      27       0b        RW    ARP Request
                                          Controls the inclusion of ARP Request filtering in the manageability filter decision
                                          (OR section).
                                          Note: Supported only for Network traffic.
ARP_RESPONSE     28       0b        RW    ARP Response
                                          Controls the inclusion of ARP Response filtering in the manageability filter
                                          decision (OR section).
                                          Note: Supported only for Network traffic.
ND_134           29       0b        RW    Neighbor Discovery 134
                                          Controls the inclusion of Router Advertisement neighbor Discovery filtering in the
                                          manageability filter decision (OR section).
                                          Notes:
                                           1. Supported only for Network traffic.
                                           2. Neighbor Discovery types supported by this bit is 0x86 (134d) - Router
                                              Advertisement
PORT_0X298       30       0b        RW    Port 0x298
                                          Controls the inclusion of Port 0x298 filtering in the manageability filter decision
                                          (OR section).
                                          Note: Supported only for Network traffic.
PORT_0X26F       31       0b        RW    Port 0x26F
                                          Controls the inclusion of Port 0x26F filtering in the manageability filter decision
                                          (OR section).
                                          Note: Supported only for Network traffic.

736                                                                                                                333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.19.10            Manageability IP Address Filter - MIPAF[n,m] (0x000058B0
                       + 0x4*n + 0x10*m, n=0...3, m=0...3)

    Field     Bit(s)    Init.   Type                                       Description

IP_ADDR        31:0      X       RW    Manageability IP Address Filters
                                       For each n, m, m=0...3, n=0...3, while MANC.EN_IPv4_FILTER = 0, MIPAF[m,n]
                                       register holds DW ‘n’ of IPv6 filter ‘m’ (4 x IPv6 filters).
                                       For each n, m, m=0...3, n=0...3 while MANC.EN_IPv4_FILTER = 1, MIPAF[m,n]
                                       registers for m=0,1,2 is the same as the previous case (3 x IPv6 filters).
                                       And MIPAF[3,n] registers holds IPv4 filter ‘n’ (4 x IPv4 filters).
                                       Note: These registers appear in Big Endian order (LS byte, LS address is first on the
                                                wire).

8.2.2.19.11            Manageability Ethernet MAC Address Low - MMAL[n]
                       (0x00005910 + 0x8*n, n=0...3)

    Field     Bit(s)    Init.   Type                                       Description

MMAL           31:0      X       RW    Manageability Ethernet MAC Address Low
                                       The lower 32 bits of the 48-bit Ethernet MAC Address.
                                       Note: Appears in Big Endian order (LS byte of MMAL is first on the wire).

8.2.2.19.12            Manageability Ethernet MAC Address High - MMAH[n]
                       (0x00005914 + 0x8*n, n=0...3)

    Field     Bit(s)    Init.   Type                                       Description

MMAH           15:0      X       RW    Manageability Ethernet MAC Address High
                                       The upper 16 bits of the 48-bit Ethernet MAC Address.
                                       Note: Appears in Big Endian order (MS byte of MMAH is last on the wire).
RESERVED       31:16    0x0      RSV   Reserved. Reads as 0. Ignored on write.

8.2.2.19.13            FTFT Filter DW Even words - FTFT_FILTER_EVEN[n]
                       (0x00009400 + 0x10*n, n=0...15)

The Flexible TCO Filter Table registers (FTFT) contains a 128-byte pattern and a corresponding 128-bit
mask array. If enabled, the first 128 bytes of the received packet are compared against the non-
masked bytes in the FTFT register.
Each 128-byte filter is composed of 32 DW entries FTFT_FILTER_ODD and FTFT_FILTER_EVEN), where
each two DWs are accompanied by an 8-bit mask (FTFT_FILTER_MASK), one bit per filter byte. The
mask field is set so that bit 0 in the mask masks byte 0, bit 1 masks byte 1, and so on. A value of 1 in
the mask field means that the appropriate byte in the filter should be compared to the appropriate byte
in the incoming packet.
The FTFT_FILTER_LENGTH register indicates the number of bytes to compare.
Notes:
 • The mask field must be 8 bytes aligned even if the length field is not 8 bytes aligned, as hardware
   implementation compares 8 bytes at a time. Therefore, it should get extra masks until the end of
   the next quad word. Any mask bit that is located after the length should be set to 0b, indicating no
   comparison should be done.

333369-009                                                                                                               737
                                 Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                           Programming Interface

 • In case the actual length defined by the length field register and the mask bits is not 8 bytes
   aligned, there might be a case that a packet which is shorter than the actual required length passes
   the flexible filter. This might happen due to comparison of up to 7 bytes that come after the packet,
   but are not a real part of the packet.
 • The last DW of each filter contains a length field defining the number of bytes from the beginning of
   the packet compared by this filter. If actual packet length is less than length specified by this field,
   the filter fails. Otherwise, it depends on the result of actual byte comparison. The value should not
   be greater than 128.
 • FTFT registers are configured by firmware.

         Field            Bit(s)     Init.      Type                                      Description

FTFT_FILTER0_DW0          31:0        X         RW      FTFT Filter DW Even
                                                        Even DW filter value.

8.2.2.19.14                 FTFT Filter DW Odd words - FTFT_FILTER_ODD[n]
                            (0x00009404 + 0x10*n, n=0...15)

         Field            Bit(s)     Init.      Type                                      Description

FTFT_FILTER0_DW1          31:0        X         RW      FTFT Filter DW Odd
                                                        Odd DW filter value.

8.2.2.19.15                 FTFT Filter Mask - FTFT_FILTER0_MASK[n] (0x00009408 +
                            0x10*n, n=0...15)

         Field             Bit(s)     Init.      Type                                      Description

FTFT_FILTER0_MASK           7:0           X       RW     FTFT Filter Mask
                                                         Mask for the 8 bytes of the filter (bit per byte)
RESERVED                    31:8       0x0       RSV     Reserved.

8.2.2.19.16                 FTFT Filter Length - FTFT_FILTER0_LENGTH[n]
                            (0x0000940C + 0x10*n, n=0...15)

      Field      Bit(s)      Init.     Type                                            Description

LENGTH            7:0        0x0          RW     Flex Filter Length
                                                 LENGTH field is valid only on the last DW of the Filter all other fields are reserved
RESERVED         31:8        0x0          RSV    Reserved.

738                                                                                                                           333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.20 PF - Manageability (ARC Subsystem) HOST Interface

                         Registers
Host interface to the ARC subsystem is described in the Section 11.8, “Manageability Host Interface”.

8.2.2.20.1               Software Semaphore Register - SWSM (0x00010140)

Note:        This register is shared by both LAN ports.

    Field       Bit(s)    Init.   Type                                             Description

SMBI              0        0b     RW          Semaphore Bit
                                              This bit is set by hardware when this register is read by the device driver (one of the
                                              two PCIe functions), and cleared when the host driver writes 0b to it.
                                              The first time this register is read, the value is 0b. In the next read the value is 1b
                                              (hardware mechanism). The value remains 1b until the device driver clears it.
                                              This bit can be used as a semaphore between the two device's drivers, and is cleared
                                              on PCIe reset.
RESERVED         31:1     0x0     RSV         Reserved.

8.2.2.20.2               Firmware Semaphore Register - FWSM (0x00010148)

Note:        This register is shared by both LAN ports. This register should be written only by the
             manageability firmware. The device driver should only read this register. The firmware
             ignores the NVM semaphore in operating system hung states. Bits[15:0] are cleared on
             firmware reset.

                Field               Bit(s)          Init.    Type                               Description

TS_NVM_MODE                              0           0b        RW     Thermal Sensor NVM Mode
                                                                      Indication to host on the Thermal Sensor NVM-based mode.
                                                                       0b = TS NVM-based mode is disabled.
                                                                       1b = TS NVM-based mode is enabled.
FLASH_UPDATE_INITIALIZED                 1           0b        RW     Flash Update Initialized
                                                                      If set, the Flash update functionality is active.
PASS_THROUGH_INITIALIZED                 2           0b        RW     Pass-Through Initialized
                                                                      If set, the pass-through functionality is active.
RESERVED                                 3           0b       RSV     Reserved.
HOST_INTERFACE_INITIALIZED               4           0b        RW     Host Interface Initialized
                                                                      If set, the host interface functionality is active.
OPERATION_MODE                           5           0b        RW     NVM Recovery Mode
                                                                      Defines the operation mode of firmware:
                                                                       0b = Normal operation mode.
                                                                       1b = NVM recovery mode.
RESERVED                               14:6         0x0       RSV     Reserved.
FW_VAL_BIT                               15          0b        RW     Firmware Valid Bit
                                                                      Hardware clears this bit in reset de-assertion so software can
                                                                      know firmware modes (bits 1-4) are invalid.
                                                                      Firmware should set this bit to 1b when it is ready (end of
                                                                      boot sequence).
RESERVED                             18:16         000b        RW     Reserved.

333369-009                                                                                                                        739
                                   Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                         Programming Interface

              Field             Bit(s)   Init.   Type                           Description

EXT_ERR_IND                      24:19    0x0     RW    External Error Indication
                                                        Firmware uses this register to store the reason that the
                                                        firmware has reset/clock gated (such as NVM, patch
                                                        corruption).
                                                        Possible values are:
                                                          0x00 = No error.
                                                          0x01 = Unspecified error.
                                                          0x02 = No manageability (No NVM).
                                                          0x03 = TCO isolate mode active.
                                                          0x05 = Shadow RAM dump fault.
                                                          0x06 = Bad Flash contents. (for FW/RO update)
                                                          0x10 = NVM CRC error in “Test Configuration” module
                                                          0x11 = NVM CRC error in “Common FW Parameters”
                                                                   module
                                                          0x12 = NVM CRC error in “PT LAN 0 configuration” module
                                                          0x13 = NVM CRC error in “SideBand configuration” module
                                                          0x14 = NVM CRC error in “Flexible TCO filter configuration”
                                                                   module
                                                          0x15 = NVM CRC error in “PT LAN 1 configuration” module
                                                          0x16 = NVM CRC error in “OEM support structure” module
                                                          0x20 = Management memory parity/ECC error.
                                                          0x21 = SR ECC error
                                                          0x22 = NVM Firmware Module Header CRC error.
                                                          0x23 = PHY Auto-load section error.
                                                          0x3F = Reserved (max error value).
                                                          All other values are reserved.
RESERVED                          25      0b      RSV   Reserved.
PHY0_CONFIG__ERR_IND              26      0b      RW    PHY0 Configuration Error Indication
                                                        Set to 1b by firmware when it fails to configure PHY of LAN0.
                                                        Cleared by firmware upon successful configuration of PHY of
                                                        LAN0.
PHY1_CONFIG__ERR_IND              27      0b      RW    PHY1 Configuration Error Indication
                                                        Set to 1b by firmware when it fails to configure PHY of LAN1.
                                                        Cleared by firmware upon successful configuration of PHY of
                                                        LAN1
RESERVED                         30:28   000b     RSV   Reserved.
FACTORY_MAC_ADDRESS_RESTORED      31      0b      RW    Factory MAC Address Restored
                                                        When set, it indicates to software that the factory MAC
                                                        Address and the current MAC Addresses are identical after
                                                        the last power-up event.
                                                        This bit is cleared by the device at power up.

740                                                                                                       333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.20.3             Software-Firmware Synchronization - SW_FW_SYNC
                       (0x00010160)

Each bit represents different software semaphore agreed between software and firmware as follows:
Bits[4:0] and Bits[10:12] are owned by software, while Bits[9:5] and Bits[13:15] are owned by
firmware. Hardware does not lock access to these bits.
Note:        This register is shared by both LAN ports. For more details on software and firmware
             synchronization, see Section 11.8.4.

         Field           Bit(s)   Init.     Type                                   Description

SW_NVM_SM                  0       0b       RW     Software NVM Semaphore
                                                   If set, NVM access is owned by software.
SW_PHY0_SM                 1       0b       RW     Software PHY 0 Semaphore
                                                   If set, PHY 0 access is owned by software.
SW_PHY1_SM                 2       0b       RW     Software PHY 1 Semaphore
                                                   If set, PHY 1access is owned by software.
SW_MAC_CSR_SM              3       0b       RW     Software MAC CSR Semaphore
                                                   If set, MAC CSR access is owned by software.
RESERVED                   4       0b       RSV    Reserved.
FW_NVM_SM                  5       0b       RW     Firmware NVM Semaphore
                                                   If set, NVM access is owned by firmware.
FW_PHY0_SM                 6       0b       RW     Firmware PHY 0 Semaphore
                                                   If set, PHY 0 access is owned by firmware.
FW_PHY1_SM                 7       0b       RW     Firmware PHY1 Semaphore
                                                   If set, PHY 1access is owned by firmware.
FW_MAC_CSR_SM              8       0b       RW     Firmware MAC CSR Semaphore
                                                   If set, MAC CSR access is owned by firmware.
NVM_UPDATE_STARTED         9       0b       RW     NVM Update Started
                                                   If set, NVM update started, software should not write to NVM.
SW_MNG_SM                 10       0b       RW     Software Manageability Semaphore
                                                   If set, Manageability host interface is owned by software.
SW_I2C0_SM                11       0b       RW     Software I2C 0 Semaphore
                                                   If set, I2C of port 0 is owned by software.
SW_I2C1_SM                12       0b       RW     Software I2C 1 Semaphore
                                                   If set, I2C of port 1 is owned by software.
FW_I2C0_SM                13       0b       RW     Firmware I2C 0 Semaphore
                                                   If set, I2C of port 0 is owned by firmware.
FW_I2C1_SM                14       0b       RW     Firmware I2C 1 Semaphore
                                                   If set, I2C of port 1 is owned by firmware.
RESERVED                 30:15    0x0       RSV    Reserved.
REGSMP                    31       0b       RW     Register Semaphore
                                                   This bit is used to semaphore the access to this register between the
                                                   firmware and software with no hardware enforcement.
                                                   When the bit value is 0b and the register is read, the returned value is
                                                   zero and the bit setting reverts to 1b (for the next read cycle). Writing 0b
                                                   to this bit clears it.
                                                   A software or firmware driver that reads this register and gets the value of
                                                   zero for this bit, locks the access to this register until it clears this bit.

333369-009                                                                                                                    741
                                  Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                Programming Interface

8.2.2.20.4             Host ARC Data RAM - ARCRAM[n] (0x00015800 + 0x4*n,
                       n=0...447)

      Field   Bit(s)   Init.   Type                                        Description

RAM_SPACE     31:0      X      RW     RAM Space
                                      RAM Space area that spans on the CSR space: 0x15800 - 0x15EFC.

8.2.2.20.5             HOST Interface Control Register - HICR (0x00015F00)

      Field   Bit(s)   Init.   Type                                        Description

EN              0       0b     RW     Enable
                                      When set, indicates that a RAM area is provided for device driver accesses. This bit is
                                      read-only for the device driver.
C               1       0b     RW     Command
                                      The device driver sets this bit when it has finished putting a command block in the
                                      ARC internal data RAM.
                                      This bit should be cleared by the firmware when the command's processing is
                                      completed. Setting this bit causes an interrupt to the ARC.
SV              2       0b     RW     Status Valid
                                      Indicates that there is a valid status in CSR area that the device driver can read.
                                       0b = Status not valid.
                                       1b = Status valid.
                                      The value of the bit is valid only when the C bit is cleared. Only the device driver
                                      reads this bit.
RESERVED      31:3     0x0     RSV    Reserved.

8.2.2.20.6             Firmware Resets Count - FWRESETCNT (0x00015F40)

      Field   Bit(s)   Init.   Type                                        Description

FWRESETCNT    31:0     0x0     RO     Firmware Resets Count
                                      Updated by hardware. Saturates at 0xFFFF,FFFF.

742                                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.21 PF - Time Sync (IEEE 1588) Registers

8.2.2.21.1                Time Sync SDP Configuration Register - TSSDP
                          (0x0000003C)

This register defines the assignment of SDP pins to the time sync auxiliary capabilities.

      Field        Bit(s)    Init.      Type                                     Description

AUX0_SDP_SEL         1:0     00b         RW    Aux 0 SDP Select
                                               Select one of the SDPs to serve as the trigger for auxiliary timestamp in
                                               AUXSTMPL0 and AUXSTMPH0 registers (see Section 8.2.2.21.20 and
                                               Section 8.2.2.21.21, respectively).
                                                00b = SDP0 is assigned.
                                                01b = SDP1 is assigned.
                                                10b = SDP2 is assigned.
                                                11b = SDP3 is assigned.
AUX0_TS_SDP_EN        2       0b         RW    Aux 0 Timestamp SDP Enable
                                               When set, indicates that one of the SDPs can be used as an external trigger to
                                               Aux timestamp 0.
                                               Note: If this bit is set to one of the SDP pins, the corresponding pin should be
                                                       configured to input mode using SPD_DIR.
AUX1_SDP_SEL         4:3     00b         RW    Aux 1 SDP Select
                                               Select one of the SDPs to serve as the trigger for auxiliary timestamp 1 in
                                               AUXSTMPL1 and AUXSTMPH1 registers (see Section 8.2.2.21.22 and
                                               Section 8.2.2.21.23, respectively).
                                                00b = SDP0 is assigned.
                                                01b = SDP1 is assigned.
                                                10b = SDP2 is assigned.
                                                11b = SDP3 is assigned.
AUX1_TS_SDP_EN        5       0b         RW    Aux 1 Timestamp SDP Enable
                                               When set indicates that one of the SDPs can be used as an external trigger to
                                               Aux timestamp 1.
                                               Note: If this bit is set to one of the SDP pins, the corresponding pin should be
                                                       configured to input mode using SPD_DIR.
TS_SDP0_SEL          7:6     00b         RW    Timestamp SDP 0 Select
                                               SDP0 allocation to Tsync event. When TS_SDP0_EN is set, these bits select the
                                               Tsync event that is routed to SDP0.
                                                00b = Target Time 0 is output on SDP0.
                                                01b = Target Time 1 is output on SDP0.
                                                10b = Freq Clock 0 is output on SDP0.
                                                11b = Freq Clock 1 is output on SDP0.
TS_SDP0_EN            8       0b         RW    Timestamp SDP 0 Enable
                                               When set, indicates that SDP0 is assigned to Tsync.
TS_SDP1_SEL         10:9     00b         RW    Timestamp SDP 1 Select
                                               SDP1 allocation to Tsync event. When TS_SDP1_EN is set, these bits select the
                                               Tsync event that is routed to SDP1.
                                                00b = Target Time 0 is output on SDP1.
                                                01b = Target Time 1 is output on SDP1.
                                                10b = Freq Clock 0 is output on SDP1.
                                                11b = Freq Clock 1 is output on SDP1.
TS_SDP1_EN           11       0b         RW    Timestamp SDP 1 Enable
                                               When set, indicates that SDP1 is assigned to Tsync.

333369-009                                                                                                                   743
                                     Did this document help answer your questions?

                                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                                Programming Interface

        Field          Bit(s)         Init.        Type                                       Description

TS_SDP2_SEL            13:12           00b         RW        Timestamp SDP 2 Select
                                                             SDP2 allocation to Tsync event. When TS_SDP2_EN is set, these bits select the
                                                             Tsync event that is routed to SDP2.
                                                              00b = Target Time 0 is output on SDP2.
                                                              01b = Target Time 1 is output on SDP2.
                                                              10b = Freq Clock 0 is output on SDP2.
                                                              11b = Freq Clock 1 is output on SDP2.
TS_SDP2_EN               14            0b          RW        Timestamp SDP 2 Enable
                                                             When set, indicates that SDP2 is assigned to Tsync.
TS_SDP3_SEL            16:15           00b         RW        Timestamp SDP 3 Select
                                                             SDP3 allocation to Tsync event. When TS_SDP3_EN is set, these bits select the
                                                             Tsync event that is routed to SDP3.
                                                              00b = Target Time 0 is output on SDP3.
                                                              01b = Target Time 1 is output on SDP3.
                                                              10b = Freq Clock 0 is output on SDP3.
                                                              11b = Freq Clock 1 is output on SDP3.
TS_SDP3_EN               17            0b          RW        Timestamp SDP 3 Enable
                                                             When set, indicates that SDP3 is assigned to Tsync.
RESERVED               31:18           0x0         RSV       Reserved. Write 0, ignore on read.

8.2.2.21.2                   Rx Message Type Register Low - RXMTRL (0x00005120)

      Field     Bit(s)        Init.         Type                                           Description

CTRLT            7:0          0x0             RW        Control Timestamp
                                                        V1 control to timestamp.
MSGT            15:8          0x0             RW        Message Timestamp
                                                        V2 message type to timestamp.
UDPT            31:16        0x13F            RW        UDP Timestamp
                                                        UDP port number to timestamp.

8.2.2.21.3                   Rx Time Sync Control Register - TSYNCRXCTL (0x00005188)

        Field      Bit(s)           Init.       Type                                          Description

RXTT                     0            0b           RO       Rx Timestamp Valid
                                                            This bit is set to 1b when a valid value for Rx timestamp is captured in the Rx
                                                            timestamp register. This bit is cleared by read of Rx timestamp register RXSTMPH
                                                            (see Section 8.2.2.21.4).
TYPE                   3:1            0x0          RW       Type
                                                            Type of packets to timestamp.
                                                             000b = Timestamp L2 (V2) packets only (Sync or Delay_req depends on
                                                                      RXMTRL.MSGT and packets with message ID 2 and 3).
                                                             001b = Timestamp L4 (V1) packets only (Sync or Delay_req depends on
                                                                      RXMTRL.CTRLT).
                                                             010b = Timestamp V2 (L2 and L4) packets (Sync or Delay_req depends on
                                                                      RXMTRL.MSGT and packets with message ID 2 and 3).
                                                             100b = Timestamp all packets.
                                                             101b = Timestamp V2 packets in which message ID bit 3 is zero, which means
                                                                      timestamp all event packets.
                                                             All other values are reserved.
EN                       4            0b           RW       Enable Rx Timestamp
                                                             0b = Time stamping to TXSTMPH/L disabled.
                                                             1b = Time stamping to TXSTMPH/L enabled.

744                                                                                                                              333369-009
                                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

       Field      Bit(s)        Init.          Type                                      Description

RESERVED           22:5             0x0         RSV    Reserved.
TSIP_UT_EN             23           0b          RW     TSIP UT Enable
                                                       Defines if untagged packets are appended a timestamp.
TSIP_UP_EN         31:24            0x0         RW     TSIP UP Enable
                                                       Defines which UP timestamp is appended to the received packet (per UP bitmap).
                                                       For example, to require a timestamp on packets received with UP = 0 or UP = 3,
                                                       bits 24 and 26 should be set.

8.2.2.21.4                  Rx Timestamp High - RXSTMPH (0x000051A4)

     Field     Bit(s)       Init.         Type                                         Description

RXSTMPH        31:0         0x0           RO       Rx Timestamp High
                                                   Rx timestamp MSB value defined in seconds.

8.2.2.21.5                  Rx Timestamp Low - RXSTMPL (0x000051E8)

     Field     Bit(s)       Init.         Type                                         Description

RXSTMPL        29:0         0x0           RO       Rx Timestamp Low
                                                   Rx timestamp LSB value defined in ns units. The value in this field wraps around at
                                                   999999999 decimal.
RESREVED       31:30        00b           RO       Reserved.

8.2.2.21.6                  Tx Time Sync Control Register - TSYNCTXCTL (0x00008C00)

       Field     Bit(s)       Init.         Type                                        Description

TXTT                0           0b          ROS       Tx Timestamp Valid
                                                      This bit is set to 1b when a valid value for Tx timestamp is captured in the Tx
                                                      timestamp register. This bit is cleared by read of Tx timestamp register TXSTMPH
                                                      (see Section 8.2.2.21.8).
RESERVED           3:1        000b          RSV       Reserved.
EN                  4           0b          RW        Enable Tx Timestamp
                                                      0x0 = time stamping disabled.
                                                      0x1 = time stamping enabled.
RESERVED          31:5         0x0          RSV       Reserved.

8.2.2.21.7                  Tx Timestamp Value Low - TXSTMPL (0x00008C04)

     Field     Bit(s)       Init.         Type                                         Description

TXSTMPL        29:0         0x0           RO       Tx Timestamp Low
                                                   Tx timestamp LSB value defined in ns units. The value in this field wraps around at
                                                   999999999 decimal.
RESERVED       31:30        00b           RSV      Reserved.

333369-009                                                                                                                           745
                                           Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Programming Interface

8.2.2.21.8             Tx Timestamp Value High - TXSTMPH (0x00008C08)

      Field   Bit(s)   Init.   Type                                         Description

TXSTMPH       31:0     0x0     RO     Tx Timestamp High
                                      Tx timestamp MSB value defined in seconds.

8.2.2.21.9             System Time Register Low - SYSTIMEL (0x00008C0C)

      Field   Bit(s)   Init.   Type                                         Description

STL           29:0     0x0     RW     System Time Low
                                      System time LSB register defined in ns units. Writes of values above one second
                                      (above 0x3B9AC9FF) are ignored.
RESERVED      31:30    00b     RW     Reserved.

8.2.2.21.10            System Time Register High - SYSTIMEH (0x00008C10)

      Field   Bit(s)   Init.   Type                                         Description

STH           31:0     0x0     RW     System Time High
                                      System time MSB register defined in seconds.

8.2.2.21.11            Increment Attributes Register - TIMEINCA (0x00008C14)

      Field   Bit(s)   Init.   Type                                         Description

INCVALUE      30:0     0x0     RW     Increment Value
                                      Increment value to the SYSTIME registers on each 12.5 ns.
                                      This field is used to correct a fixed clock drift and should be kept at zero for an ideal
                                      clock.
ISGN           31       0b     RW     Increment Sign
                                       0b = Each 12.5 ns cycle add to SYSTIME a value of 12.5 ns + INCVALUE * 2^-32 ns.
                                       1b = Each 12.5 ns cycle add to SYSTIME a value of 12.5 ns - INCVALUE * 2^-32 ns.

8.2.2.21.12            Time Adjustment Offset Register - TIMADJ (0x00008C18)

      Field   Bit(s)   Init.   Type                                         Description

TADJL         30:0     0x0     RW     Time Adjustment
                                      Time adjustment value defined in ns units.
SIGN           31       0b     RW     Sign
                                       0b = ”+”
                                       1b = ”-”

746                                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.21.13               TimeSync Auxiliary Control Register - TSAUXC
                          (0x00008C20)

        Field      Bit(s)    Init.      Type                                      Description

EN_TT0                0       0b         RW    Enable Target Time 0
                                               Enable bit is set by software to 1b to enable pulse or level change generation as
                                               a function of the PLSG0 bit in this register.
                                               This bit is not auto-cleared by the hardware.
EN_TT1                1       0b         RW    Enable Target Time 1
                                               Enable bit is set by software to 1b to enable pulse or level change generation as
                                               a function of the PLSG0 bit in this register.
                                               This bit is not auto-cleared by the hardware.
EN_CLK0               2       0b         RW    Enable Configurable Frequency Clock 0
                                               Clock is generated according to frequency defined in the FREQOUT0 register on
                                               the SDP pin (0 to 3) that has both:
                                                1. TSSDP.TS_SDPx_SEL field with a value of 10b.
                                                2. TSSDP.TS_SDPx_EN value of 1b.
SAMP_AUT0             3       0b         SC    Sample Auxiliary Timestamp 0
                                               When this flag is set, the SYSTIMEL/H registers are latched to the AUXSTMPL0/
                                               AUXSTMPH0 registers. Then, the SAMP_AUT0 flag is auto-cleared by the
                                               hardware.
ST0                   4       0b         RW    Start Clock 0 Toggle on Target Time 0
                                               Enable Clock 0 toggle only after target time 0 (as defined in the TRGTTIML0 and
                                               TRGTTIMH0 registers) has passed.
EN_CLK1               5       0b         RW    Enable Configurable Frequency Clock 1
                                               Clock is generated according to frequency defined in the FREQOUT1 register on
                                               the SDP pin (0 to 3) that has both:
                                                1. TSSDP.TS_SDPx_SEL field with a value of 10b.
                                                2. TSSDP.TS_SDPx_EN value of 1b.
SAMP_AUT1             6       0b         SC    Sample Auxiliary Timestamp 1
                                               When this flag is set, SYSTIMEL/H registers are latched to the AUXSTMPL1/
                                               AUXSTMPH1 registers. Then, the SAMP_AUT1 flag is auto-cleared by the
                                               hardware.
ST1                   7       0b         RW    Start Clock 1 Toggle on Target Time 1
                                               Enable Clock 1 toggle only after Target Time 1 (as defined in the TRGTTIML1 and
                                               TRGTTIMH1 registers) has passed.
EN_TS0                8       0b         RW    Enable Hardware Timestamp 0
                                               Enable time-stamping occurrence of change in SDP pin into the AUXSTMPL0 and
                                               AUXSTMPH0 registers.
                                               SDP pin (0 to 3) is selected for time-stamping if the SDP pin is selected via the
                                               TSSDP.AUX0_SDP_SEL field and the TSSDP.AUX0_TS_SDP_EN bit is set to 1b.
AUTT0                 9       0b         RW    Auxiliary Timestamp Taken 0
                                               This is a read-only bit field. At 0b the Auxiliary Timestamp 0 is enabled. This bit
                                               is set to 1b by hardware following a level change of the input SDP. Reading the
                                               AUXSTMPH0 register clears this bit.
EN_TS1               10       0b         RW    Enable hardware time stamp 1
AUTT1                11       0b         RW    Auxiliary Timestamp Taken 1
                                               This is a read only bit field. At 0b the Auxiliary Time Stamp 1 is enabled. This bit
                                               is set to 1b by hardware following a level change of the input SDP. Reading the
                                               AUXSTMPH1 register clears this bit.
RESERVED            16:12     0x0       RSV    Reserved.

333369-009                                                                                                                      747
                                     Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

        Field          Bit(s)         Init.        Type                                     Description

PLSG0                    17            0b          RW     Pulse Generate
                                                          Use Target Time 0 to generate start of pulse and Target Time 1 to generate end
                                                          of pulse. SDP pin selected to drive pulse or level change is set according to the
                                                          TSSDP.TS_SDPx_SEL field with a value of 00b, and TSSDP.TS_SDPx_EN bit with
                                                          a value of 1b (see Section 8.2.2.21.1).
                                                           0b = Target Time 0 generates change in SDP level.
                                                           1b = Target time 0 generates start of pulse on SDP pin.
                                                          Note: Pulse or level change is generated when the EN_TT0 bit is set to 1b.
RESERVED               29:18          0x0          RSV    Reserved.
RESREVED                 30            1b          RSV    Reserved.
DISABLE_SYSTIME          31            1b          RW     Disable SYSTIME count operation
                                                           0b = SYSTIME timer activated.
                                                           1b = SYSTIME timer disabled. Value of SYSTIMEH, SYSTIMEL and SYSTIMER
                                                                remains constant.

8.2.2.21.14               Target Time Register 0 Low - TRGTTIMEL0 (0x00008C24)

      Field     Bit(s)        Init.         Type                                         Description

TTL             29:0          0x0             RW     Target Time Low
                                                     Target Time 0 LSB register defined in ns units.
RESERVED        31:30         00b             RW     Reserved.

8.2.2.21.15               Target Time Register 0 High - TRGTTIMEH0 (0x00008C28)

      Field     Bit(s)        Init.         Type                                         Description

TTH             31:0          0x0             RW     Target Time High
                                                     Target Time 0 MSB register defined in seconds.

8.2.2.21.16               Target Time Register 1 Low - TRGTTIMEL1 (0x00008C2C)

      Field     Bit(s)        Init.         Type                                         Description

TTL             29:0          0x0             RW     Target Time Low
                                                     Target Time 1 LSB register defined in ns units.
RESERVED        31:30         00b             RW     Reserved.

8.2.2.21.17               Target Time Register 1 High - TRGTTIMEH1 (0x00008C30)

      Field     Bit(s)        Init.         Type                                         Description

TTH             31:0          0x0             RW     Target Time High
                                                     Target Time 1 MSB register defined in seconds.

748                                                                                                                             333369-009
                                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.21.18            Frequency Out 0 Control Register - FREQOUT0
                       (0x00008C34)

    Field     Bit(s)    Init.   Type                                       Description

CHCT           29:0     0x0      RW    Clock Out Half Cycle Time
                                       Defines the Half Cycle time of Clock 0 in ns units.
                                       When clock output is enabled, permitted values are any value larger than 25 and any
                                       value below 1 second.
RESERVED       31:30    00b      RSV   Reserved

8.2.2.21.19            Frequency Out 1 Control Register - FREQOUT1
                       (0x00008C38)

    Field     Bit(s)    Init.   Type                                       Description

CHCT           29:0     0x0      RW    Clock Out Half Cycle Time
                                       Defines the Half Cycle time of Clock 1 in ns units.
                                       When clock output is enabled, permitted values are any value larger than 13 and up
                                       to including 999,999,900 decimal (slightly below 1 second).
RESERVED       31:30    00b      RSV   Reserved.

8.2.2.21.20            Auxiliary Timestamp 0 Register Low - AUXSTMPL0
                       (0x00008C3C)

    Field     Bit(s)    Init.   Type                                       Description

TST_LOW        29:0     0x0      RO    Timestamp Low
                                       Auxiliary Time Stamp 0 LSB value defined in ns units.
RESERVED       31:30    00b      RO    Reserved

8.2.2.21.21            Auxiliary Timestamp 0 Register High - AUXSTMPH0
                       (0x00008C40)

    Field     Bit(s)    Init.   Type                                       Description

TST_HI         31:0     0x0      RO    Timestamp High
                                       Auxiliary Time Stamp 0 MSB value defined in seconds.

8.2.2.21.22            Auxiliary Timestamp 1 Register Low - AUXSTMPL1
                       (0x00008C44)

    Field     Bit(s)    Init.   Type                                       Description

TST_LOW        29:0     0x0      RO    Timestamp Low
                                       Auxiliary Time Stamp 1 LSB value defined in ns units.
RESERVED       31:30    00b      RO    Reserved

333369-009                                                                                                             749
                                 Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Programming Interface

8.2.2.21.23               Auxiliary Timestamp 1 Register High - AUXSTMPH1
                          (0x00008C48)

      Field      Bit(s)   Init.   Type                                        Description

TST_HI            31:0    0x0      RO    Timestamp High
                                         Auxiliary Time Stamp 1 MSB value defined in seconds.

8.2.2.21.24               System Time Register Residue - SYSTIMR (0x00008C58)

      Field      Bit(s)   Init.   Type                                        Description

SYSTIMR           31:0    0x0      RW    System Time Residue
                                         System time Residue value defined in 2^(-32) ns resolution.

8.2.2.21.25               Time Sync Interrupt Cause Register - TSICR (0x00008C60)

Note:         Value of register is always read as 0x0. Once EICR.TIMESYNC is set, internal value of register
              should be cleared by write 1 to all bits, or cleared by read to enable reception of an additional
              EICR.TIMESYNC interrupt.

      Field      Bit(s)   Init.   Type                                        Description

SYS_WRAP           0       0b     RW1C   SYSTIMEL Wraparound
                                         Set when SYSTIME ns counter wraps around (SYSTIMEL). Wraparound occurrence can
                                         be used by software to update software time. This event should happen every second.
TXTS               1       0b     RW1C   Transmit Timestamp
                                         Set when new timestamp is loaded into TXSTMP register
RXTS               2       0b     RW1C   Receive Timestamp
                                         Set when new timestamp is loaded into RXSTMP register
TT0                3       0b     RW1C   Target Time 0 Trigger
                                         Set when Target Time 0 (TRGTTIML/H0) trigger occurs.
TT1                4       0b     RW1C   Target Time 1 Trigger
                                         Set when Target Time 1 (TRGTTIML/H1) trigger occurs.
AUTT0              5       0b     RW1C   Auxiliary Timestamp 0 Taken
                                         Set when new timestamp is loaded into AUXSTMP 0 (auxiliary timestamp 0) register.
AUTT1              6       0b     RW1C   Auxiliary Timestamp 1 Taken
                                         Set when new timestamp is loaded into AUXSTMP 1 (auxiliary timestamp 1) register.
TADJ               7       0b     RW1C   Time Adjust 0 Done
                                         Set when Time Adjust to clock out 0 or 1 completed
RESERVED          31:8    0x0     RSV    Reserved. Write 0, ignore on read.

750                                                                                                             333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.21.26            Time Sync Interrupt Mask Register - TSIM (0x00008C68)

      Field   Bit(s)    Init.   Type                                        Description

SYS_WRAP         0       0b      RW    SYSTIMEL Wraparound Mask
                                        0b = No Interrupt generated when TSICR.SYS_WRAP is set.
                                        1b = Interrupt generated when TSICR.SYS_WRAP is set.
TXTS             1       0b      RW    Transmit Timestamp Mask
                                        0b = No Interrupt generated when TSICR.TXTS is set.
                                        1b = Interrupt generated when TSICR.TXTS is set.
RXTS             2       0b      RW    Receive Timestamp Mask
                                        0b = No Interrupt generated when TSICR.RXTS is set.
                                        1b = Interrupt generated when TSICR.RXTS is set.
TT0              3       0b      RW    Target Time 0 Trigger Mask
                                        0b = No Interrupt generated when TSICR.TT0 is set.
                                        1b = Interrupt generated when TSICR.TT0 is set.
TT1              4       0b      RW    Target Time 1 Trigger Mask
                                        0b = No Interrupt generated when TSICR.TT1 is set.
                                        1b = Interrupt generated when TSICR.TT1 is set.
AUTT0            5       0b      RW    Auxiliary Timestamp 0 Taken Mask
                                        0b = No Interrupt generated when TSICR.AUTT0 is set.
                                        1b = Interrupt generated when TSICR.AUTT0 is set.
AUTT1            6       0b      RW    Auxiliary Timestamp 1 Taken Mask
                                        0b = No Interrupt generated when TSICR.AUTT1 is set.
                                        1b = Interrupt generated when TSICR.AUTT1 is set.
TADJ             7       0b      RW    Time Adjust 0 Done Mask
                                        0b = No Interrupt generated when TSICR.TADJ is set.
                                        1b = Interrupt generated when TSICR.TADJ is set.
RESERVED       31:8     0x0      RSV   Reserved. Write 0, ignore on read.

333369-009                                                                                        751
                                 Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                       Programming Interface

#### 8.2.2.22 PF - Virtualization PF Registers

8.2.2.22.1              PF VFLR Events Clear - PFVFLREC[n] (0x00000700 + 0x4*n,
                        n=0...1)

      Field   Bit(s)     Init.     Type                                           Description

CLEAR_VFLE    31:0       0x0       RW1C     Clear VLFR Events
                                            When set, bit ‘i’ in register ‘n’ reflects an FLR event on VF# 32*n+i. These bits are
                                            accessible only to the PF and are cleared by writing 1.

8.2.2.22.2              PF Mailbox Interrupt Causes Register - PFMBICR[n]
                        (0x00000710 + 0x4*n, n=0...3)

Each register handles 16 VFs as defined here.

      Field   Bit(s)     Init.     Type                                           Description

VFREQ         15:0       0x0       RW1C     VF Requested
                                            Each bit in the VFREQ field is set when VF number (16*n+j) wrote a message in its
                                            mailbox, where ‘n’ is the register index (n=0...3) and ‘j’ is the index of the bits in the
                                            VFREQ (j=0...15).
VFACK         31:16      0x0       RW1C     VF Acknowledged
                                            Each bit in the VFACK field is set when VF number (16*n+j) acknowledged a PF
                                            message, where ‘n’ is the register index (n=0...3) and ‘16+j’ is the index of the bits in
                                            the VFACK (j=0...15).

8.2.2.22.3              PF Mailbox Interrupt Mask Register - PFMBIMR[n]
                        (0x00000720 + 0x4*n, n=0...1)

      Field   Bit(s)       Init.       Type                                         Description

VFIM          31:0      0xFFFFFFFF      RW      VF Interrupt Mask
                                                Bit j - Mailbox indication from VF number (32*n+j) might cause an interrupt to
                                                the PF.

8.2.2.22.4              PF Queue Drop Enable Register - PFQDE (0x00002F04)

      Field    Bit(s)     Init.      Type                                          Description

PFQDE            0         0b        RW       PF Queue Drop Enable
                                              Enable drop of packets from Rx queue QUEUE_INDEX. This bit overrides the
                                              SRRCTL.DROP_EN bit (Section 8.2.2.9.5) of each queue. In other words, if either of
                                              the bits is set, a packet received when no descriptor is available is dropped.
HIDE_VLAN        1         0b        RW       Hide VLAN
                                              If this bit is set, the RXDCTL.VME setting is ignored (Section 8.2.2.9.7), the VLAN is
                                              always stripped, a value of zero is written in the RDESC.VLAN tag and in the
                                              RDESC.STATUS.VP fields of the received descriptor.
STRIP_TAG        2         0b        RW       Strip Tag
                                              If this bit is set, the E-tag is stripped from the packet.
                                              If only one type of tag should be stripped, the other tag’s EtherType should be
                                              invalidated using the ETAG_ETYPE.VALID field (Section 8.2.2.8.5).
RESERVED        7:3        0x0       RSV      Reserved.

752                                                                                                                       333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

     Field        Bit(s)         Init.         Type                                              Description

QUEUE_INDEX       14:8            0x0            RW      Queue Index
                                                         Indicates the queue referenced upon WE/RE commands.
RESERVED           15             0b           RSV       Reserved.
WE                 16             0b             RW      Write Enable
                                                         When this bit is set, the content of Bits[2:0] are written into the relevant queue
                                                         context. Bit[3] is reserved.
                                                         This bit should never be set together with the RE bit in this register.
RE                 17             0b             RW      Read Enable
                                                         When this bit is set, the content of Bits[2:0] are read from the relevant queue
                                                         context. Bit[3] is reserved.
                                                         This bit should never be set together with the WE bit in this register.
RESERVED          31:18           0x0          RSV       Reserved.

8.2.2.22.5                  Last Malicious VM - Rx - LMVM_RX (0x00002FA4)

         Field           Bit(s)          Init.         Type                                         Description

MALICIOUS_QUEUE            6:0           0x0           RW          Malicious Queue
                                                                   The Rx queue on which the malicious behavior reported in LVMMC was
                                                                   detected. The queue number is the absolute number in the PF space.
RESERVED                   16:7          0x0           RSV         Reserved.
MAL_PF                     17             0b           RW          Malicious Driver on PF
                                                                   Malicious driver behavior detected on current PF.
                                                                    0b = Malicious event was on a queue belonging to a VF.
                                                                    1b = Malicious event was on a queue belonging to the PF.
RESERVED                 31:18           0x0           RSV         Reserved.

8.2.2.22.6                  Last VM Misbehavior Cause - Rx - LVMMC_RX (0x00002FA8)

Bits in the LVMMC_RX register define the cause for blocking the malicious queue that was reported in
the LMVM_RX.MALICIOUS_QUEUE field when RDRXCTL.MDP_EN is set. For details of the different bits,
refer to Section 7.8.4.3, “Malicious Driver Detection”.

          Field              Bit(s)            Init.      Type                                        Description

INV_MACC                          0              0b           RC       Invalid Memory Access
                                                                       A PCIe DMA access initiated by a VF ended with Unsupported Request (UR)
                                                                       or Completer Abort (CA), or a read access was blocked due to out of range
                                                                       address. When a Malicious DMA access is detected, the Rx queue (VF) that
                                                                       initiated the access is disabled and corresponding WQBR_RX bit is set.
INVALID_RXQ_CONTEXT               1              0b           RC       Invalid Receive Queue Context
                                                                       An invalid receive queue context was detected when queue was enabled,
                                                                       or an attempt to change the static part of the queue context on the fly was
                                                                       detected.
RESERVED                         31:2            0x0         RSV       Reserved.

333369-009                                                                                                                                     753
                                               Did this document help answer your questions?

                                                                               Intel® Ethernet Controller X550 Datasheet
                                                                                                 Programming Interface

8.2.2.22.7             Wrong Queue Behavior Register - Rx - WQBR_RX[n]
                       (0x00002FB0 + 0x4*n, n=0...3)

      Field   Bit(s)   Init.   Type                                         Description

WVBR          31:0     0x0     RW1C   Wrong Behavior Receive Queue
                                      Bitmap indicating against which Rx queue a malicious action was taken. The queue is
                                      released only by a reset of the VF or by clearing the corresponding bit in WQBR_RX
                                      register.

8.2.2.22.8             PF Mailbox - PFMAILBOX[n] (0x00004B00 + 0x4*n,
                       n=0...63)

      Field   Bit(s)   Init.   Type                                         Description

STS             0       0b     WO     Status
                                      Status/Command from PF ready.
                                      Setting this bit, causes an interrupt to the relevant VF. This bit always read as zero.
                                      Setting this bit sets the PFSTS bit in the VFMAILBOX register (Section 8.3.2.1.5).
ACK             1       0b     WO     Acknowledge
                                      VF message received.
                                      Setting this bit, causes an interrupt to the relevant VF. This bit always read as zero.
                                      Setting this bit sets the PFACK bit in VFMAILBOX register.
VFU             2       0b     RW     VFU
                                      Buffer is taken by VF.
                                      This bit is RO for the PF and is a mirror of the VFU bit of the VFMAILBOX register.
PFU             3       0b     RW     PFU
                                      Buffer is taken by PF.
                                      This bit can be set only if the VFU bit is cleared and is mirrored in the PFU bit of the
                                      VFMAILBOX register.
RVFU            4       0b     WO     Reset VFU
                                      Setting this bit clears the VFU bit in the corresponding VFMAILBOX register. This bit
                                      should be used only if the VF driver is stuck. Setting this bit also resets the
                                      corresponding bits in the VFREQ and VFACK fields of the PFMBICR register
                                      (Section 8.2.2.22.2).
RESERVED      31:5     0x0     RSV    Reserved.

8.2.2.22.9             Filter Local Packets Low - PFFLPL (0x000050B0)

      Field   Bit(s)   Init.   Type                                         Description

FLP           31:0     0x0     RW     Filter Local Packets
                                      Filter incoming packets whose MAC source address matches one of the LAN port DA
                                      MAC Addresses. If the SA of the received packet matches one of the DA in the
                                      RAH/RAL registers, the VM tied to this DA does not receive the packet. Other VMs can
                                      still receive it. (Bit per Pool)

8.2.2.22.10            Filter Local Packets High - PFFLPH (0x000050B4)

      Field   Bit(s)   Init.   Type                                         Description

FLP           31:0     0x0     RW     Filter Local Packets
                                      Filter incoming packets whose MAC source address matches one of the LAN port DA
                                      MAC Addresses. If the SA of the received packet matches one of the DA in the
                                      RAH/RAL registers, the VM tied to this DA does not receive the packet. Other VMs can
                                      still receive it. (Bit per Pool)

754                                                                                                                 333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.22.11               PF VM Tx Switch Loopback Enable - PFVMTXSW[n]
                          (0x00005180 + 0x4*n, n=0...1)

      Field    Bit(s)     Init.     Type                                          Description

LLE            31:0       0x0       RW       Local Loopback Enable
                                             For each register ‘n’, and bit ‘i’ (where i=0..31), enables Local loopback for pool
                                             32*n+1.
                                             When set, a packet originating from a specific pool and destined to the same pool is
                                             allowed to be looped back. If cleared, the packet is dropped.

8.2.2.22.12               PF Virtual Control Register - PFVTCTL (0x000051B0)

       Field     Bit(s)     Init.     Type                                         Description

VT_ENA              0         0b      RW       Virtualization Enabled Mode
                                                0b = Rx traffic is handled internally as if it belongs to VF zero while VF zero is
                                                       enabled.
                                                1b = The X550 supports either 16, 32, or 64 Pools.
                                               This bit should be set the same as MTQC.VT_ENA (see Section 8.2.2.10.14).
RESERVED           6:1       0x0      RSV      Reserved.
DEF_PL            12:7       0x0      RW       Default Pool
                                               Pool assignment for packets that do not pass any pool queuing decision. Enabled
                                               by the DIS_DEF_POOL bit.
RESERVED         15:13      000b      RSV      Reserved.
POOLING_MODE     17:16       00b      RW       Pooling Mode
                                                00b = Pool select by MAC Address.
                                                01b = Pool select by MAC Address or E-tag.
                                                10b = Reserved.
                                                11b = Reserved.
RESERVED         28:18       0x0      RSV      Reserved.
DIS_DEF_POOL       29         0b      RW       Disable Default Pool
                                               Determines the behavior of an Rx packet that does not match any Rx filter and is
                                               therefore not allocated a destination pool.
                                                0b = Packet is assigned to the Default Pool (see DEF_PL above).
                                                1b = Packet is dropped.
RPL_EN             30         0b      RW       Replication Enable
                                               Replication is enabled when set to 1b.
                                               When set, MRQC.MRQE should be set to one of the virtualization modes (1000b -
                                               1111b)
RESERVED           31         0b      RSV      Reserved.

8.2.2.22.13               PF VF Receive Enable - PFVFRE[n] (0x000051E0 + 0x4*n,
                          n=0...1)

This register is reset on common reset cases, and on per-function reset cases. Respective bits per VF
are reset on VFLR, BME bit clear, or on VF software reset. For more information, see
Section 8.2.2.22.16.

      Field    Bit(s)     Init.     Type                                          Description

PFVFRE         31:0       0x0       RW       PF VF Receive Enable
                                             Bit j - Enables receiving packets to VF# (32*n+j).
                                             Each bit is cleared by the relevant VFLR.

333369-009                                                                                                                           755
                                     Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                        Programming Interface

8.2.2.22.14                   PF VM VLAN Insert Register - PFVMVIR[n] (0x00008000 +
                              0x4*n, n=0...63)

       Field         Bit(s)     Init.    Type                                       Description

PORT_VLAN_ID         15:0       0x0       RW    Port VLAN ID
                                                Port VLAN tag to insert if the VLANA field = 01b.
RESERVED             26:16      0x0      RSV    Reserved.
TAGA                 28:27      00b       RW    Tag Action
                                                 00b = Do not insert any outer tag.
                                                 01b = Insert an E-tag.
                                                 10b = Reserved.
                                                 11b = Reserved.
RESERVED              29         0b      RSV    Reserved.
VLANA                31:30      00b       RW    VLAN Action
                                                 00b = Use descriptor command.
                                                 01b = Always insert Default VLAN.
                                                 10b = Never insert VLAN.
                                                 11b = Reserved.

8.2.2.22.15                   Last VM Misbehavior Cause - Tx - LVMMC_TX (0x00008108)

Bits in this register define the cause for blocking the malicious queue that was reported in the
LMVM_TX.MALICIOUS_QUEUE field (Section 8.2.2.22.17) when the DMATXCTL.MDP_EN bit is set
(Section 8.2.2.10.2). For details of the different bits, refer to Section 7.8.4.3, “Malicious Driver
Detection”.
Note:          Only the first malicious event is registered for each packet. Therefore, if a bit is not set, it
               does not mean that this event did not occur, only that another malicious behavior was
               detected first.

          Field               Bit(s)    Init.   Type                                     Description

MAC_HEADER                      0        0b      RC     MAC Header
                                                        Illegal MAC header size.
IPV4_HEADER                     1        0b      RC     IPv4 Header
                                                        Illegal IPv4 header size.
IPV6_HEADER                     2        0b      RC     IPv6 Header
                                                        Illegal IPv6 header size.
WRONG_MAC_IP                    3        0b      RC     Wrong MAC IP
                                                        Wrong MAC +IP header size.
TCP_LSO                         4        0b      RC     TCP Long Send Operation
                                                        Illegal TCP header was detected in a large send operation.
IPSEC_OFFLOAD                   5        0b      RC     IPsec Offload
                                                        A VF requested an IPsec offload.
UDP_LSO                         6        0b      RC     UDP Long Send Operation
                                                        Illegal UDP header was detected in a large send operation.
STCP_CS                         7        0b      RC     STCP Checksum
                                                        Illegal STCP header was detected in an SCTP checksum offload operation.
SIZE                            8        0b      RC     Size
                                                        Illegal packet size (> 15.5K).
RESERVED                        9        0b     RSV     Reserved.
OFF_ILL                        10        0b      RC     Offload Illegal
                                                        Illegal offload request.

756                                                                                                                  333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

          Field         Bit(s)    Init.     Type                                  Description

SCTP_ALIGNED              11       0b       RC     SCTP Aligned
                                                   SCTP CRC request of non 4 byte aligned data.
ZERO_MSS                  12       0b       RC     Zero MSS
                                                   A request for large send with zero MSS was detected.
CONTEXT_IN_PACKET         13       0b       RC     Context in Packet
                                                   A context descriptor was detected in the middle of a packet.
LSO_MORE_THAN_4           14       0b       RC     Large Send Operation More Than Four
                                                   Large send with more than 4 header buffers misbehavior was detected.
OOS_SSO                   15       0b       RC     Out of Synch Single Send Operation
                                                   Out of sync during Single Send.
OOS_LSO                   16       0b       RC     Out of Synch Large Send Operation
                                                   Out of sync during Large Send.
SSO_UDP                   17       0b       RC     Single Send Operation UDP
                                                   Wrong parameter of headers for UDP SSO.
SSO_TCP                   18       0b       RC     Single Send Operation TCP
                                                   Wrong parameter of headers for TCP SSO.
INV_MACC                  19       0b       RC     Invalid Memory Access
                                                   A PCIe DMA access initiated by a VF ended with Unsupported Request (UR)
                                                   or Completer Abort (CA), or was prevented from being sent if out of range.
                                                   When a Malicious DMA access is detected the Tx queue (VF) that initiated
                                                   the access is disabled and corresponding WQBR_TX bit is set.
DESC_TYPE                 20       0b       RC     Descriptor Type
                                                   Wrong descriptor type (other than 2,3) or CC bit not set in virtualization
                                                   mode.
WRONG_NULL                21       0b       RC     Wrong Null
                                                   Null without EOP.
NO_EOP                    22       0b       RC     No End of Packet
                                                   Packet without EOP (i.e. bigger than the ring size).
CONTEXT_BURST             23       0b       RC     Context Burst
                                                   Contiguous context descriptor burst that exceeds 3 Contexts.
RESERVED                  24       0b       RSV    Reserved.
MAC_VLAN_SPOOF            25       0b       RC     MAC/VLAN Spoof
                                                   A MAC spoof or VLAN spoof attempt was detected.
VLAN_IERR                 26       0b       RC     VLAN Insertion Error
                                                   VLE bit set in Tx descriptor when VMVIR[n].VLANA register field is not 0
                                                   causing drop of Tx packets.
LEGACY_DESC_IOV           27       0b       RC     Legacy Descriptor IOV
                                                   A legacy descriptor in IOV was detected.
FCOE_OFFLOAD              28       0b       RC     FCoE Offload
                                                   A VF requested an FCoE offload.
INVALID_TXQ_CONTEXT       29       0b       RC     Invalid Transmit Queue Context
                                                   An invalid transmit queue context was detected when queue was enabled,
                                                   or an attempt to change the static part of the queue context on the fly was
                                                   detected.
RESERVED                 31:30    00b       RSV    Reserved.

333369-009                                                                                                                  757
                                 Did this document help answer your questions?

                                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                                  Programming Interface

8.2.2.22.16                 PF VF Transmit Enable - PFVFTE[n] (0x00008110 + 0x4*n,
                            n=0...1)

This register is reset on common reset cases, and on per-function reset cases. Respective bits per VF
are reset on VFLR, BME bit clear, or on VF software reset. For more information, see
Section 8.2.2.22.13.

      Field      Bit(s)      Init.         Type                                              Description

PFVFTE           31:0        0x0            RW         PF VF Transmit Enable
                                                       Bit j - Enables transmitting packets from VF# (32*n+j).
                                                       Each bit is cleared by the relevant VFLR.

8.2.2.22.17                 Last Malicious VM - Tx - LMVM_TX (0x00008124)

         Field            Bit(s)         Init.        Type                                       Description

MALICIOUS_QUEUE            6:0           0x0          RW      Malicious Queue
                                                              The Tx queue on which the malicious behavior reported in LVMMC was
                                                              detected. The queue number is the absolute number in the PF space.
RESERVED                   16:7          0x0          RSV     Reserved.
MAL_PF                     17             0b          RW      Malicious PF
                                                              Malicious driver behavior detected on current PF.
                                                               0b = Malicious event was on a queue belonging to a VF.
                                                               1b = Malicious event was on a queue belonging to the PF.
RESERVED                  31:18          0x0          RSV     Reserved.

8.2.2.22.18                 Wrong Queue Behavior Register - Tx - WQBR_TX[n]
                            (0x00008130 + 0x4*n, n=0...3)

      Field      Bit(s)      Init.         Type                                              Description

WVBR             31:0        0x0           RW1C        Wrong Behavior Transmit Queue
                                                       Bitmap indicating against which Tx queue an anti-spoof action or malicious action was
                                                       taken. The queue is released only by a reset of the VF or by clearing the
                                                       corresponding bit in the WQBR_TX register

8.2.2.22.19                 PFVF Anti-Spoof Control - PFVFSPOOF[n] (0x00008200 +
                            0x4*n, n=0...7)

      Field       Bit(s)         Init.         Type                                           Description

MACAS              7:0            0x0            RW     MAC Anti-Spoof
                                                        For each register ‘n’, and bit ‘i’ (where i=0..7), enables anti-spoofing filter on
                                                        Ethernet MAC Addresses for VF(8*n+i).
VLANAS             15:8           0x0            RW     VLAN Anti-Spoof
                                                        For each register ‘n’, and bit ‘8+i’ (where i=0..7), enables anti-spoofing filter on
                                                        VLAN tag for VF(8*n+i).
                                                        Note: If VLANAS is set for a specific pool, the respective MACAS bit must be set as
                                                                well.
ETHERTYPEAS       23:16           0x0            RW     EtherType Anti-Spoof
                                                        For each register ‘n’, and bit ‘16+i’ (where i=0..7), enables anti-spoofing filter on
                                                        EtherType for VF(8*n+i).

758                                                                                                                                  333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

      Field     Bit(s)    Init.    Type                                          Description

ETHERTYPELB     31:24      0x0     RW       EtherType Loopback
                                            For each register ‘n’, and bit ‘24+i’ (where i=0..7), enables loopback filter on
                                            EtherType for VF(8*n+i).

8.2.2.22.20              PF DMA Tx General Switch Control - PFDTXGSWC
                         (0x00008220)

      Field   Bit(s)     Init.    Type                                          Description

LBE              0        0b      RW      Loopback Enable
                                          Enables VMDQ loopback.
RESERVED       31:1      0x0      RSV     Reserved.

8.2.2.22.21              PF VM 0:31 Error Count Mask - PFVMECM0 (0x00008790)

      Field   Bit(s)     Init.    Type                                          Description

FILTER         31:0      0x0      RW      Filter
                                          Defines if a packet dropped from pools 0 to 31, respectively, is counted in the SSVPC
                                          counter.

8.2.2.22.22              PF VM 32:63 Error Count Mask - PFVMECM1 (0x00008794)

      Field   Bit(s)     Init.    Type                                          Description

FILTER         31:0      0x0      RW      Filter
                                          Defines if a packet dropped from pools 32 to 63, respectively, is counted in the SSVPC
                                          counter.

8.2.2.22.23              PF VM L2Control Register - PFVML2FLT[n] (0x0000F000 +
                         0x4*n, n=0...63)

This register controls per VM Inexact L2 Filtering.

      Field   Bit(s)     Init.    Type                                          Description

RESERVED       21:0      0x0      RSV     Reserved.
UPE             22        0b      RW      Unicast Promiscuous Enable
VPE             23        0b      RW      VLAN Promiscuous Enable
AUPE            24        0b      RW      Accept Untagged Packets Enable
                                          When set, packets without a VLAN tag can be forwarded to this queue, assuming they
                                          pass the Ethernet MAC Address queuing mechanism.
ROMPE           25        0b      RW      Receive Overflow Multicast Packets
                                          Accept packets that match the MTA table.
ROPE            26        0b      RW      Receive MAC Filters Overflow
                                          Accept packets that match the PFUTA table.
BAM             27        0b      RW      Broadcast Accept Mode
MPE             28        0b      RW      Multicast Promiscuous Enable
RESERVED       31:29     000b     RSV     Reserved.

333369-009                                                                                                                     759
                                   Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.2.22.24               PF VM VLAN Pool Filter - PFVLVF[n] (0x0000F100 + 0x4*n,
                          n=0...63)

Note:         Software should initialize these registers before transmit and receive are enabled.

      Field      Bit(s)   Init.   Type                                        Description

VLAN_ID           11:0     X      RW     VLAN ID
                                         Defines a VLAN tag for pool VLAN filter n.
                                         The bitmap defines which pools belong to this VLAN.
                                         Note: Appears in Little Endian order (LS byte last on the wire).
RESERVED         30:12     X      RSV    Reserved.
VI_EN              31      0b     RW     VLAN ID Enable
                                         This filter is valid.

8.2.2.22.25               PF VM VLAN Pool Filter Bitmap - PFVLVFB[n] (0x0000F200 +
                          0x4*n, n=0...127)

Note:         Software should initialize these registers before transmit and receive are enabled.

      Field      Bit(s)   Init.   Type                                        Description

POOL_ENA          31:0     X      RW     Pool Enable bit array
                                         Each couple of registers ‘2*n’ and ‘2*n+1’ enables routing of packets that match a
                                         PFVLVF[n] filter to a Pool list (see Section 8.2.2.22.24).
                                         Each bit when set, enables packet reception with the associated Pools as follows:
                                          • Bit ‘i’ in register ‘2*n’ is associated with POOL ‘i’.
                                          • Bit ‘i’ in register ‘2*n+1’ is associated with POOL ‘32+i’.

8.2.2.22.26               PF Unicast Table Array - PFUTA[n] (0x0000F400 + 0x4*n,
                          n=0...127)

There is one register per 32 bits of the Unicast Address Table for a total of 128 registers (the
PFUTA[127:0] designation). Software must mask to the desired bit on reads, and supply a 32-bit word
on writes. The first bit of the address used to access the table is set according to the MCSTCTRL.MO
field (Section 8.2.2.8.7). The 7 MS bits of the Ethernet MAC Address (out of the 12 bits) selects the
register index, while the 5 LS bits (out of the 12 bits) selects the bit within a register.
Note:         All accesses to this table must be 32 bit. The lookup algorithm is the same one used for the
              MTA table. This table should be zeroed by software before start of work.

      Field      Bit(s)   Init.   Type                                        Description

BIT_VECTOR        31:0     X      RW     Bit Vector
                                         Word wide bit vector specifying 32 bits in the unicast destination address filter table.

760                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.22.27            PF Mirror Rule Control - PFMRCTL[n] (0x0000F600 + 0x4*n,
                       n=0...3)

This register defines mirroring rules for each of four destination pools.

     Field    Bit(s)    Init.   Type                                         Description

VPME             0       0b      RW    Virtual Pool Mirroring Enable
                                       Enables mirroring of certain pools as defined in the PFMRVM registers
                                       (Section 8.2.2.22.29).
UPME             1       0b      RW    Uplink Port Mirroring Enable
                                       Enables mirroring of all traffic received from the network.
DPME             2       0b      RW    Downlink Port Mirroring Enable
                                       Enables mirroring of all traffic transmitted to the network.
VLME             3       0b      RW    VLAN Mirroring Enable
                                       Enables mirroring of a set of given VLANs as defined in the PFMRVLAN registers
                                       (Section 8.2.2.22.28).
RESERVED        7:4     0x0      RSV   Reserved.
MP             13:8     0x0      RW    Mirror Pool
                                       Defines the destination pool for this mirror rule.
RESERVED       31:14    0x0      RSV   Reserved.

8.2.2.22.28            PF Mirror Rule VLAN - PFMRVLAN[n] (0x0000F610 + 0x4*n,
                       n=0...7)

This register defines the VLAN values as listed in the PFVLVF table (Section 8.2.2.22.24) taking part in
the VLAN mirror rule. Registers 0 and 4 correspond to rule 0, registers 1 and 5 correspond to rule 1,
etc. Registers 0..3 correspond to the LSB in the PFVLVF table (e.g. register 0 corresponds to VLAN
filters 31:0, while register 4 corresponds to VLAN filters 63:32).

     Field    Bit(s)    Init.   Type                                         Description

VLAN           31:0     0x0      RW    VLAN
                                       Bitmap listing which VLANs participate in the mirror rule.

8.2.2.22.29            PF Mirror Rule Pool - PFMRVM[n] (0x0000F630 + 0x4*n,
                       n=0...7)

This register defines which pools are being mirrored to the destination pool. Registers 0 and 4
correspond to rule 0, registers 1 and 5 correspond to rule 1, etc. Registers 0..3 correspond to the LSB
in the pool list (e.g. register 0 corresponds to pools 31:0, while register 4 corresponds to pools 63:32).

     Field    Bit(s)    Init.   Type                                         Description

POOL           31:0     0x0      RW    Pool
                                       Bitmap listing which pools participate in the mirror rule.

333369-009                                                                                                              761
                                 Did this document help answer your questions?

                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                            Programming Interface

8.2.2.22.30            PF VM Tag Insert Register - PFVMTIR[n] (0x00017000 +
                       0x4*n, n=0...63)

      Field   Bit(s)    Init.   Type                                    Description

PORT_TAG_ID   31:0      0x0     RW     Port Tag ID
                                       Port tag to insert if PFVMVIR.TAGA field = 01b. EtagEtype-PFVMTIR[31:0]-0x0000

762                                                                                                         333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.23 PF - Power Management Registers

8.2.2.23.1               DMA Coalescing Control Register - DMACR (0x00002400)

             Field                Bit(s)    Init.    Type                                Description

DMACWT                            15:0      0x20      RW     DMA Coalescing Watchdog Timer
                                                             When in DMA coalescing, defines the upper limit in 40.960 s units
                                                             between arrival of coalescing exit event condition and actual exit
                                                             from DMA coalescing.
                                                             The programmed value should be non zero.
HIGH_PRI_TC                       23:16      0x0      RW     High Priority Traffic Class
                                                             This field defines which TC is considered high priority, and a packet
                                                             received for this TC causes exit from DMA Coalescing. When a TC bit
                                                             is set, it indicates this TC is high priority.
                                                               Bit 16 TC0
                                                               Bit 17 TC1
                                                               ...
                                                               Bit 23 TC7
RESERVED                          27:24      0x0      RSV    Reserved.
EN_MNG_IND                         28        1b       RW     Enable Management Indications for DMAC operation
                                                             When set, DMA Coalescing functionality is affected from the MCTP
                                                             management buffer status indications.
RESERVED                           29        0b       RSV    Reserved.
LX_COALESCING_INDICATION           30        0b       RW     Lx Coalescing Indication
                                                             Defines whether to move in/out of DMA coalescing when the PCIe
                                                             link moves in/out of L1/L0s.
                                                               0b = DMA coalescing can also start in L0. DMA coalescing stops
                                                                    when any TLP transactions are executed on the PCIe.
                                                               1b = DMA coalescing conditions are met only when PCIe is in L1/
                                                                    L0s.
DMAC_EN                            31        0b       RW     DMA Coalescing Enable
                                                              0b = Disable DMA Coalescing.
                                                              1b = Enable DMA Coalescing.

8.2.2.23.2               DMA Coalescing Time to Lx Request - DMCTLX
                         (0x00002404)

    Field       Bit(s)    Init.      Type                                         Description

TTLX             11:0     0x20        RW     Time to LX Request
                                             Controls the time between detection of DMA Coalescing condition to actual entry into
                                             DMA Coalescing state. Timer counts is in 1.28 s intervals.
                                              • For link speed of 10 GbE, minimum value should be 0x1.
                                              • For link speed of 1 GbE, minimum value should be 0x2.
                                              • For link speed of 100 Mb/s minimum value should be 0x20.
                                             This limitation is enforced by the hardware.
                                             Note: Timer adds delay to decision on when to enter DMA Coalescing state.
RESERVED        31:12     0x0        RSV     Reserved. Write 0. Ignore on read.

333369-009                                                                                                                     763
                                        Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                              Programming Interface

8.2.2.23.3             DMA Coalescing Threshold - DMCTH[n] (0x00003300 +
                       0x4*n, n=0...7)

      Field   Bit(s)   Init.   Type                                      Description

DMACRXT        8:0     0x20    RW     DMA Coalescing Receive Threshold Rx PB TC[n]
                                      This value defines the DMA coalescing Receive threshold in 1 KB units. When amount
                                      of data in internal receive buffer exceeds DMACRXT[n] value, DMA coalescing is
                                      stopped.
                                      Value written to the field should take into account:
                                       • Latency tolerance requirements (LTR) sent over the PCIe and XOFF receive
                                          threshold values, to avoid needless generation of flow control packets when in
                                          DMA coalescing operating mode and flow control is enabled.
                                       • The maximum size of the receive buffer.
RESERVED      31:9     0x0     RSV    Reserved.

8.2.2.23.4             EEE Tx LPI Count - TLPIC (0x000041F4)

This register counts EEE Tx LPI entry events. A EEE Tx LPI event occurs when the transmitter enters
EEE (IEEE802.3az) LPI state. This register only increments if transmits are enabled and EEE operation
is enabled.

      Field   Bit(s)   Init.   Type                                      Description

ETLPIC        31:0     0x0     RC     EEE Transmit LPI Count
                                      Number of EEE Tx LPI events.
                                      Register cleared on read. Register does not wrap around at 0xFFFFFFFF.

8.2.2.23.5             EEE Rx LPI Count - RLPIC (0x000041F8)

This register counts EEE Rx LPI entry events. A EEE Rx LPI event occurs when the receiver detects link
partner entry into EEE (IEEE802.3az) LPI state. This register only increments if receives are enabled
and EEE operation is enabled.

      Field   Bit(s)   Init.   Type                                      Description

ERLPIC        31:0     0x0     RC     EEE Receive LPI Count
                                      Number of EEE Rx LPI events.
                                      Register cleared on read. Register does not wrap around at 0xFFFFFFFF.

764                                                                                                            333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.23.6                Energy Efficient Ethernet (EEE) Setup Register - EEE_SU
                          (0x00004380)

     Field       Bit(s)     Init.    Type                                        Description

DTW_MIN           7:0       0x0      RW     DTW Minimum
                                            Time to add to minimum Tw_sys_tx value defined in IEEE802.3az clause 78.5. This
                                            additional time should be configured according to the link speed/type and is in
                                            addition to the specification definition:
                                             • For 1000BASE-T operation (16.5 s)
                                             • For 100BASE-TX operation (30 s)
                                             • For 10GBASE-T operation (7.36 s for Case-1 and, 4.48 s for Case-2)
                                            The minimum Tw_sys_tx value defines the duration where no data is transmitted
                                            following move out of EEE LPI Tx state.
                                            Time to add defined in this field is expressed in 0.1 s resolution.
                                            Note: The idle time value defined by this field plus the Tw_sys_tx value defined
                                                     in IEEE802.3az clause 78.5 is used when moving out of EEE Tx LPI state to
                                                     transmit flow control frames even if value specified in EEER.TW_SYSTEM
                                                     field is higher (see Section 8.2.2.23.8).
RESERVED          15:8      0x0      RSV    Reserved
TW_WAKE_MIN      21:16      0x0      RW     TW Wake Minimum
                                            Minimum time, expressed in 1 s, between sending a request to move into EEE Tx
                                            LPI and sending a request to move back to active state.
                                            Note: If conditions to exit LPI during the Tw_wake_min interval cease to exist,
                                                    the device does not move out of Tx LPI after timer has expired.
RESERVED         23:22      00b      RW     Reserved
TX_LU_LPI_DLY    25:24      11b      RW     Transmit Link-Up LPI Delay
                                            Delay to enable entry of Tx EEE LPI state following Link-up indication.
                                             00b = No delay
                                             01b = 10 ms
                                             10b = 100 ms
                                             11b = 1 Second
                                            Note: IEEE802.3az clause 78.1.2.1 defines delay of 1 second following link-up.
TEEE_DLY         31:26      0x2      RW     Tx EEE LPI Entry Delay
                                            Defines the delay to EEE entry once conditions to enter EEE LPI are detected. Field
                                            resolution is 1 s.
                                            Note: If conditions to enter LPI during the TEEE_DLY interval cease to exist, the
                                                     device does not enter Tx LPI and continues normal operation.

8.2.2.23.7                Energy Efficient Ethernet (EEE) STATUS - EEE_STAT
                          (0x00004398)

     Field       Bit(s)     Init.    Type                                        Description

RESERVED          28:0      0x0      RSV    Reserved/ Write 0. Ignore on read.
EEE_NEG            29        0b       RO    EEE support Negotiated on link
                                             0b = EEE operation not supported on link.
                                             1b = EEE operation supported on link.
RX_LPI_STATUS      30        0b       RO    Rx Link in LPI Status
                                             0b = Rx in Active state
                                             1b = Rx in LPI state
TX_LPI_STATUS      31        0b       RO    Tx Link in LPI Status
                                             0b = Tx in Active state
                                             1b = Tx in LPI state

333369-009                                                                                                                  765
                                    Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                       Programming Interface

8.2.2.23.8     Energy Efficient Ethernet (EEE) Register - EEER
               (0x000043A0)

      Field   Bit(s)   Init.   Type                                    Description

TW_SYSTEM     15:0     0x0     RW     TW System
                                      Time expressed in s that no data is transmitted following move from EEE Tx
                                      LPI link state to Link Active state. Field holds the Transmit Tw_sys_tx value
                                      negotiated during EEE LLDP negotiation.
                                      Notes:
                                       1. If value is lower than minimum Tw_sys_tx value defined in IEEE802.3az
                                           clause 78.5, the interval where no data is transmitted following move out
                                           of EEE Tx LPI state defaults to minimum Tw_sys_tx.
                                       2. Following link disconnect or auto-negotiation, the value of this field
                                           returns to default value, until software re-negotiates new tw_sys_tx
                                           value via EEE LLDP.
                                       3. Fast Retrain and Local/Remote Fault indication are not considered link
                                           disconnect, and do not cause the field to return to the default value.
                                       4. When transmitting flow control frames, the device waits the minimum
                                           time defined in the IEEE802.3az standard before transmitting the flow
                                           control packet. the device does not wait the Tw_system time following
                                           exit of LPI before transmitting the flow control frame.
TX_LPI_EN      16       0b     RW     Transmit LPI Enable
                                      Enable entry into EEE LPI on Tx path.
                                       0b = Disable entry into EEE LPI on Tx path.
                                       1b = Enable entry into EEE LPI on Tx path.
                                      Notes:
                                       1. Even when TX_LPI_EN is 1b, the device does not enable entry into Tx LPI
                                          state for at least 1 second following the change of link_status to OK as
                                          defined in IEEE802.3az clause 78.1.2.1.
                                       2. Even if the TX_LPI_EN bit is set, the device initiates entry into Tx EEE LPI
                                          link state only if EEE support at the link speed was negotiated during
                                          auto-negotiation.
RX_LPI_EN      17       1b     RW     Receive LPI Enable
                                      Enable entry into EEE LPI on Rx path
                                       0b = Disable entry into EEE LPI on Rx path.
                                       1b = Enable entry into EEE LPI on Rx path.
                                      Note: Even if the RX_LPI_EN bit is set, the device recognizes entry into Rx
                                              EEE LPI link state only if EEE support at the link speed was
                                              negotiated during auto-negotiation.
RESERVED      27:18    0x0     RSV    Reserved. Write 0. Ignore on read.
EEE_FRC_AN     28       0b     RW     Force EEE Auto-Negotiation
                                      When bit is set to 1b, enables EEE operation in internal MAC logic even if link
                                      partner does not support EEE.
                                      Note: Should be set to 1b to enable testing of EEE operation via MAC
                                              loopback.
RESERVED      31:29    000b    RSV    Reserved. Write 0. Ignore on read.

766                                                                                                       333369-009
                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.23.9             Latency Tolerance Reporting (LTR) Control - LTRC
                       (0x00011708)

         Field        Bit(s)   Init.   Type                                    Description

SLTRV                  9:0      0x5     RW    Snoop Latency Value
                                              Along with the Max Snoop Latency Scale field (SSCALE), this register
                                              specifies the maximum snoop latency this function wants to request.
                                              Software should set this only if it is set to a lower number than the platform’s
                                              maximum supported latency.
SSCALE                12:10    010b     RW    Snoop Latency Scale
                                              This field provides a scale for the value contained within the Snoop Latency
                                              Value field (SLTRV).
                                                000b = Value times 1 ns.
                                                001b = Value times 32 ns.
                                                010b = Value times 1,024 ns.
                                                011b = Value times 32,768 ns.
                                                100b = Value times 1,048,576 ns.
                                                101b = Value times 33,554,432 ns.
                                                All other values are not permitted
                                              It is advised that the software driver use the same scale as configured in the
                                              LTR capability.
RESERVED              14:13     00b     RSV   Reserved. Write 0. Ignore on read.
LTRS_REQUIREMENT        15      0b      RW    LTR Snoop Requirement
                                               0b = No Latency requirements in Snoop memory access.
                                               1b = Latency tolerance in Snoop memory access specified in the SLTRV
                                                    field.
NSLTRV                25:16     0x5     RW    No Snoop Latency Value
                                              Along with the Max No Snoop Latency Scale field (NSSCALE), this field
                                              specifies the maximum no snoop latency this function wants to request.
                                              Software should set this only if it is set to a lower number than the platform’s
                                              maximum supported latency.
NSSCALE               28:26    010b     RW    No Snoop Latency Scale
                                              This field provides a scale for the value contained within the No Snoop
                                              Latency Value field.
                                                000b = Value times 1 ns.
                                                001b = Value times 32 ns.
                                                010b = Value times 1,024 ns.
                                                011b = Value times 32,768 ns.
                                                100b = Value times 1,048,576 ns.
                                                101b = Value times 33,554,432 ns.
                                                All other values are reserved.
                                              It is advised that the software driver use the same scale as configured in the
                                              LTR capability.
RESERVED                29      0b      RSV   Reserved. Write 0. Ignore on read.
LTR_SEND                30      0b      RW    LTR Send
                                              Indication to send an LTR message.
                                              This bit is set by the software (indicates to hardware to send an LTR message
                                              update to the system), and cleared by hardware after the message is sent.
                                              This bit is not sent as part of the LTR message.
LTRNS_REQUIREMENT       31      0b      RW    LTR No Snoop Requirement
                                               0b = No Latency requirements in No Snoop memory access.
                                               1b = Latency tolerance in No Snoop memory access specified in the
                                                    NSLTRV field.

333369-009                                                                                                                 767
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                             Programming Interface

8.2.2.23.10            DMA Coalescing Management Threshold - DMCMNGTH
                       (0x00015F20)

      Field   Bit(s)   Init.   Type                                      Description

RESERVED       3:0      0x0    RSV    Reserved.
DMCMNGTHR     19:4     0x100   RW     DMA Coalescing Management Threshold
                                      BMC Tx DMAC Threshold. This value defines the DMA coalescing management
                                      threshold in 16 byte units. When amount of empty space in internal transmit buffer
                                      exceeds DMCMNGTHR value, DMA coalescing is stopped and PCIe moves to L0 state.
                                      Note: If value is 0x0 condition to move out of DMA Coalescing due to passing the
                                              DMA Coalescing Management Threshold level is disabled.
RESERVED      31:20     0x0    RSV    Reserved.

768                                                                                                          333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

#### 8.2.2.24 PF - Security Registers

Security registers are mainly concerned with the internal settings of the AES crypto engine used by
IPsec. They are owned by the PF in an IOV mode.

8.2.2.24.1                 Security Tx Control - SECTXCTRL (0x00008800)

      Field        Bit(s)      Init.       Type                                        Description

SECTX_DIS              0           1b       RW      Security Transmit Disable
                                                    Tx security offload disable bit.
                                                     0b = The AES crypto engine used in Tx by LinkSec or IPsec offload is enabled.
                                                            Normal operating mode when a security off load is enabled.
                                                     1b = The AES crypto engine used in Tx by LinkSec and IPsec offloads is
                                                            disabled. This mode must be used to save the X550’s power consumption
                                                            when no security offload is enabled.
                                                    This bit is RW/RO if fused-off.
TX_DIS                 1           0b       RW      Transmit Disable
                                                    Disable security Tx path.
                                                     0b = Tx data path is enabled. Normal operating mode.
                                                     1b = No new packet is fetched out from the Tx Packet Buffers, so that the Tx
                                                           Security block can be internally emptied prior to changing the security
                                                           mode. The SECTXSTAT.SECTX_RDY bit is de-asserted until the path is
                                                           emptied by hardware (see Section 8.2.2.24.2).
STORE_FORWARD          2           0b       RW      Store and Forward
                                                    Tx security buffer mode.
                                                     0b = Tx sec buffer is operated in pass-through mode. Operating mode when
                                                          LinkSec is enabled or when no security off load is enabled.
                                                     1b = A complete frame is stored in the internal security Tx buffer prior to
                                                          being forwarded to the MAC. Operating mode when IPsec off load is
                                                          enabled (as requested to overwrite ICV field in AH frames). Note that it
                                                          increases the Tx internal latencies (for all TCs).
RESERVED            31:3        0x0        RSV      Reserved.

8.2.2.24.2                 Security Tx Status - SECTXSTAT (0x00008804)

     Field       Bit(s)      Init.       Type                                        Description

SECTX_RDY          0          0b          RO      Security Transmit Ready
                                                  Tx security block ready for mode change.
                                                   0b = Indicates that the internal data path from the Tx Packet Buffers to the Tx
                                                          security block is not empty, and thus software cannot change the security
                                                          mode.
                                                   1b = Indicates that the internal data path from the Tx Packet Buffers to the Tx
                                                          security block has been emptied, and thus the security mode can be
                                                          changed by software.
                                                  This bit is polled by software once the SECTXCTRL.TX_DIS bit is set
                                                  (Section 8.2.2.24.1).
SECTX_OFF_DIS      1          0b          RO      Security Transmit Off Disable
                                                  Tx security offload disabled.
                                                  When set, indicates that the Tx security offload feature is disabled by fuse or
                                                  strapping pin.
ECC_TXERR          2          0b          RO      ECC Transmit Error
                                                  Unrecoverable ECC error occurred in the Tx SA Table or SEC Tx FIFO.
                                                   0b = No ECC error occurred on the Tx SA Table since the last time device was
                                                        reset.
                                                   1b = Indicates that an unrecoverable ECC error occurred when accessing
                                                        internally the Tx SA Table. The ECC interrupt is set as well, until the device
                                                        is reset by software.

333369-009                                                                                                                          769
                                        Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                        Programming Interface

       Field     Bit(s)     Init.     Type                                           Description

RESERVED          31:3       0x0      RSV       Reserved.

8.2.2.24.3                Security Tx Buffer Almost Full - SECTXBUFFAF
                          (0x00008808)

      Field    Bit(s)     Init.     Type                                           Description

FULLTHRESH      9:0       0x250     RW       Full Threshold
                                             Tx security buffer almost full threshold (relatively to full capacity).
                                             The size of the security buffer is 0x274 lines of 16 bytes. In LinkSec offload, the buffer
                                             operates in path-through mode, and the recommended threshold is 0x250. It means
                                             that the almost full indication is generated very soon while only a fraction of a packet
                                             is stored in the buffer.
                                             In IPsec mode the buffer operates in a store-and-forward mode, and the
                                             recommended threshold is 0x15. It means that the almost full indication is generated
                                             only after the buffer contains at least a whole jumbo packet.
RESERVED       31:10       0x0      RSV      Reserved.

8.2.2.24.4                Security Tx Buffer Minimum IFG - SECTXMINIFG
                          (0x00008810)

      Field    Bit(s)     Init.     Type                                           Description

MINSECIFG       3:0        0x1      RW       Minimum Security IFG
                                             Minimum IFG between packets.
                                             It is the minimum gap between consecutive frames from the DBU-Tx required for the
                                             security block. The MINSECIFG is measured in Wake DMA clock units (equal to 6.4 ns
                                             in 10 GbE).
RESERVED        7:4        0x0      RSV      Reserved.
MRKRINSERT     18:8       0x10      RW       This field is used to configure the Security Tx Buffer.
                                             When in DCB mode, it should be modified as follows:
                                              • PFC disabled — Set to 0x1F.
                                              • PFC enabled and 9.5 KB Jumbo supported — Set to 0x640 (it represents a PFC
                                                 XOFF recovery delay of ~10 s in 10 GbE).
                                              • PFC enabled and 9.5 KB Jumbo not supported — Set to 0x1A0 (it represents a
                                                 PFC XOFF recovery delay of ~2.6 s in 10 GbE).
RESERVED       31:19       0x0      RSV      Reserved.

770                                                                                                                        333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.24.5              Security Rx Control - SECRXCTRL (0x00008D00)

         Field             Bit(s)      Init.      Type                                    Description

SECRX_DIS                    0          1b        RW      Security Receive Disable
                                                          Rx security offload disable bit.
                                                           0b = The AES crypto engine used in Rx by LinkSec or IPsec offload is
                                                                enabled. Normal operating mode when a security off load is
                                                                enabled.
                                                           1b = The AES crypto engine used in Rx by LinkSec and IPsec offloads is
                                                                disabled. This mode must be used to save the X550's power
                                                                consumption when no security off load is enabled.
RX_DIS                       1          0b        RW      Transmit Disable
                                                          Disable security Rx path.
                                                           0b = Rx data path is enabled. Normal operating mode.
                                                           1b = Any new packet received from the Rx MAC is filtered out, so that
                                                                  the Rx Security block can be internally emptied prior to changing
                                                                  the security mode. The SECRXSTAT.SECRX_RDY bit is de-asserted
                                                                  until the path is emptied by hardware (see Section 8.2.2.24.6).
                                                          This bit is RW/RO if fused-off.
RESERVED                   31:2        0x0        RSV     Reserved.

8.2.2.24.6              Security Rx Status - SECRXSTAT (0x00008D04)

      Field       Bit(s)      Init.      Type                                         Description

SECRX_RDY           0            0b          RO    Security Receive Ready
                                                   Rx security block ready for mode change.
                                                    0b = Indicates that the internal data path from the Rx MAC to the Rx security
                                                           block is not empty, and thus software cannot change the security mode.
                                                    1b = Indicates that the internal data path from the Rx MAC to the Rx security
                                                           block has been emptied, and thus the security mode can be changed by
                                                           software.
                                                   This bit is polled by software once the SECRXCTRL.RX_DIS bit is set
                                                   (Section 8.2.2.24.5).
SECRX_OFF_DIS       1            0b          RO    Security Receive Off Disable
                                                   Rx security offload disabled.
                                                   When set, it indicates that the Rx security offload feature is disabled by the
                                                   internal fuse or by strapping pin.
ECC_RXERR           2            0b          RO    ECC Receive Error
                                                   Unrecoverable ECC error occurred in an Rx SA Table.
                                                    0b = No ECC error occurred on the Rx SA Table since the last time device was
                                                         reset.
                                                    1b = Indicates that an unrecoverable ECC error occurred when accessing
                                                         internally one Rx SA Table. The ECC interrupt is set as well, until the
                                                         device is reset by software.
RESERVED           31:3          0x0      RSV      Reserved.

333369-009                                                                                                                          771
                                       Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                       Programming Interface

#### 8.2.2.25 PF - IPsec Registers

IPsec registers are owned by the PF in an IOV mode. There is no added value here to encrypt the SA
contents when being read by software, because the SA contents is available in clear text from system
memory, like for any IPsec flow handled in software.

8.2.2.25.1                 IPsec Tx Index - IPSTXIDX (0x00008900)

Notes:        WRITE and READ bits must not be set at the same time by software.
              IPS_TX_EN is RW, but it is RO if fused-off and/or if SECTXCTRL.SECTX_DIS is set to 1b.

      Field      Bit(s)     Init.    Type                                         Description

IPS_TX_EN          0         0b      RW      IPsec Tx Enable
                                             IPsec Tx off-load enable bit.
                                              0b = IPsec off-load ability is disabled for Tx path, regardless of the contents of the
                                                    Tx SA table.
                                              1b = IPsec of-load ability is enabled for Tx path.
RESERVED          2:1       00b      RSV     Reserved.
SA_IDX            12:3      0x0      RW      SA Index
                                             SA index for indirect access into the Tx SA table.
RESERVED         29:13      0x0      RSV     Reserved.
READ              30         0b      RW      READ command
                                             When set, the contents of the Tx SA table entry pointed by the SA_IDX field is loaded
                                             into the IPSTXKEY 0...3 and IPSTXSALT registers. Immediately self-cleared by
                                             hardware once the entry contents has been loaded into the registers.
WRITE             31         0b      RW      WRITE command
                                             When set, the contents of the IPSTXKEY 0...3 and IPSTXSALT registers are loaded into
                                             the Tx SA table entry pointed to by the SA_IDX field. Immediately self-cleared by
                                             hardware once the entry contents have been loaded into the memory.

8.2.2.25.2                 IPsec Tx Salt Register - IPSTXSALT (0x00008904)

      Field       Bit(s)     Init.    Type                                         Description

AES_128_SALT       31:0       0x0     RW      AEA 128 Salt
                                              4 bytes salt that has been read/written from/to the Tx SA entry pointed to by
                                              SA_IDX.

8.2.2.25.3                 IPsec Tx Key Registers - IPSTXKEY[n] (0x00008908 +
                           0x4*n, n=0...3)

      Field       Bit(s)     Init.    Type                                         Description

AES_128_KEY        31:0       0x0     RW      AES 128 Key
                                              4 bytes of a 16-byte key that has been read/written from/to the Tx SA entry pointed
                                              to by SA_IDX.
                                                n=0 contains the LSB of the key.
                                                n=3 contains the MSB of the key.

772                                                                                                                      333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.25.4               IPsec Rx Index - IPSRXIDX (0x00008E00)

Notes:       WRITE and READ bits must not be set at the same time by software.
             IPS_RX_EN is RW, but it is RO if fused-off and/or if SECRXCTRL.SECRX_DIS is set to 1b.
             Software is not allowed to write/read access registers that belong to different Rx SA tables
             without writing the IPSRXIDX register in between for setting the WRITE/READ bit. Refer to Rx
             SA tables access rules described in Section 7.13.9.
             Software should not make changes in the Rx SA tables while changing the IPS_RX_EN bit.

    Field       Bit(s)   Init.   Type                                         Description

IPS_RX_EN         0       0b     RW     IPsec Rx Enable
                                        IPsec Rx off load enable bit.
                                         0b = IPsec off load ability is disabled for Rx path, regardless of the contents of Rx
                                               SA tables.
                                         1b = IPsec off load ability is enabled for Rx path.
TABLE            2:1     00b     RW     TABLE select bits
                                         00b = No Rx SA table is accessed.
                                         01b = IP Address table is accessed.
                                         10b = SPI table is accessed.
                                         11b = KEY table is accessed.
TB_IDX           12:3    0x0     RW     Table Index
                                        Table index bits for indirect access into the Rx SA table selected by TABLE bits.
                                        When accessing the IP Address table, only the 7 least significant bits of this field are
                                        meaningful.
RESERVED        29:13    0x0     RSV    Reserved.
READ              30      0b     RW     READ command
                                        When set, the contents of the Rx SA table entry as pointed to by the [TABLE, TB_IDX]
                                        fields is loaded into the corresponding registers. Immediately self-cleared by
                                        hardware once the entry contents have been loaded into the corresponding registers.
                                        For instance, if this bit is set together with TABLE=10b and TB_IDX=0x9, the SPI
                                        value stored in entry 9 is loaded into the IPSRXSPI 0...3 registers.
                                        Rx SA registers related to another Rx SA table (e.g. IPSRXKEY 0...3 registers) must
                                        not be read when TABLE=01b.
WRITE             31      0b     RW     WRITE command
                                        When set, the contents of the registers concerned by the Rx SA table pointed to by
                                        the TABLE field is loaded into the table entry pointed to by the TB_IDX field.
                                        Immediately self-cleared by hardware once the entry contents have been loaded into
                                        the memory.
                                        For instance, if this bit is set together with TABLE=10b and TB_IDX=0x9, the value
                                        written in IPSRXSPI 0...3 registers is loaded into the SPI table entry 9.

8.2.2.25.5               IPsec Rx IP Address Register - IPSRXIPADDR[n]
                         (0x00008E04 + 0x4*n, n=0...3)

These registers are related to the IP Address table.

    Field       Bit(s)   Init.   Type                                         Description

IPADDR           31:0    0x0     RW     IP Address
                                        4 bytes of 16-byte destination IP Address for the associated Rx SA(s).
                                         n=0 contains the MSB for an IPv6 IP Address.
                                         n=3 contains an IPv4 IP Address or the LSB for an IPv6 IP Address.
                                        For an IPv4 address, IPSRXIPADDR 0...2 must be written with zeros.
                                        Note: This field is defined in Big Endian (LS byte is first on the wire).

333369-009                                                                                                                    773
                                  Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                    Programming Interface

8.2.2.25.6               IPsec Rx SPI Register - IPSRXSPI (0x00008E14)

This register is related to the Rx SPI table.

      Field    Bit(s)    Init.    Type                                         Description

SPI            31:0      0x0      RW      SPI
                                          SPI field for the SPI entry.
                                          Note: This field is defined in Big Endian (LS byte is first on the wire).

8.2.2.25.7               IPsec Rx SPI Register IP Index - IPSRXIPIDX (0x00008E18)

This register is related to the Rx SPI table.

      Field    Bit(s)    Init.    Type                                         Description

IP_IDX          6:0      0x0      RW      IP Index
                                          Index in the IP Address table where the destination IP Address associated to that SPI
                                          entry is found.
RESERVED       31:7      0x0      RSV     Reserved.

8.2.2.25.8               IPsec Rx Key Register - IPSRXKEY[n] (0x00008E1C +
                         0x4*n, n=0...3)

These registers are related to the Rx KEY table.

      Field     Bit(s)    Init.    Type                                         Description

AES_128_KEY      31:0      0x0     RW      AES 128 Key
                                           4 bytes of 16-byte key of the KEY entry.
                                            n=0 contains the LSB of the key.
                                            n=3 contains the MSB of the key.

8.2.2.25.9               IPsec Rx Salt Register - IPSRXSALT (0x00008E2C)

This register is related to the Rx KEY table.

      Field     Bit(s)    Init.    Type                                         Description

AES_128_SALT     31:0      0x0     RW      AES 128 Salt
                                           4 bytes salt associated to the KEY entry.

774                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.25.10            IPsec Rx Mode Register - IPSRXMOD (0x00008E30)

This register is related to the Rx KEY table.

    Field     Bit(s)    Init.   Type                                       Description

VALID            0       0b      RW    Valid bit
                                        0b = The KEY entry is not valid.
                                        1b = The KEY entry is valid.
RESERVED         1       0b      RSV   Reserved.
PROTO            2       0b      RW    IPsec Protocol select
                                        0b = The KEY entry off-loads AH packets.
                                        1b = The KEY entry off-loads ESP packets.
DECRYPT          3       0b      RW    Decryption bit
                                       When set, hardware performs decryption off load for this KEY entry.
                                       Meaningful only if PROTO bit is set (i.e. ESP mode).
IPV6             4       0b      RW    IPv6 type
                                       When set, only matched IPv6 packet are off-loaded for that KEY
                                       entry.
                                       When cleared, only matched IPv4 packets are off-loaded for that
                                       KEY entry.
RESERVED       31:5     0x0      RSV   Reserved.

333369-009                                                                                                   775
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                       Programming Interface

#### 8.2.2.26 VF Registers Mapping in the PF Space

8.2.2.26.1           VF Control Register - VFCTRL[n] (0x00000300 + 0x4*n,
                     n=0...63; WO)

This register array is the mapping of the VFs VFCTRL registers.
Field definitions are the same as those defined in Section 8.3.2.1.1.

8.2.2.26.2           VF Extended Interrupt Cause - VFEICR[n] (0x00000B00 +
                     0x4*n, n=0...63; RC/W1C)

Field definitions are the same as those defined in Section 8.3.2.2.1.

8.2.2.26.3           VF Extended Interrupt Cause Set - VFEICS[n] (0x00000C00
                     + 0x4*n, n=0...63; WO)

Field definitions are the same as those defined in Section 8.3.2.2.2.

8.2.2.26.4           VF Extended Interrupt Mask Set/Read - VFEIMS[n]
                     (0x00000D00 + 0x4*n, n=0...63; RWS)

Field definitions are the same as those defined in Section 8.3.2.2.3.

8.2.2.26.5           VF Extended Interrupt Mask Clear - VFEIMC[n]
                     (0x00000E00 + 0x4*n, n=0...63; WO)

Field definitions are the same as those defined in Section 8.3.2.2.4.

8.2.2.26.6           VF Good Packets Received Count - VFGPRC[n] (0x0000101C
                     + 0x40*n, n=0...63; RW)

PF mirror of the VFGPRC register.
Field definitions are the same as those defined in Section 8.3.2.6.1.

8.2.2.26.7           VF Good Octets Received Count Low - VFGORC_LSB[n]
                     (0x00001020 + 0x40*n, n=0...63; RW)

PF mirror of the VFGORC_LSB register.
Field definitions are the same as those defined in Section 8.3.2.6.2.

8.2.2.26.8           VF Multiple Receive Queues Command Register - VFMRQC[n]
                     (0x00003400 + 0x4*n, n=0...63; RW)

PF mirror of VFMRQC registers of the VFs.
Field definitions are the same as those defined in Section 8.3.2.3.10.

776                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.2.2.26.9             VF Mailbox - VFMAILBOX[n] (0x00004C00 + 0x4*n,
                       n=0...63; RW)

This register array is the mapping of the VFMAILBOX registers of the VFs.
Field definitions are the same as those defined in Section 8.3.2.1.5.

8.2.2.26.10            VF Extended Interrupt Auto Mask Enable - VFEIAM[n]
                       (0x00004D00 + 0x4*n, n=0...63; RW)

Field definitions are the same as those defined in Section 8.3.2.2.5.

8.2.2.26.11            VF Interrupt Vector Allocation Registers Misc -
                       VFIVAR_MISC[n] (0x00004E00 + 0x4*n, n=0...63; RW)

These registers map the mailbox interrupt into MSI-X vector (PF mirror). For more details, refer to
Section 7.3.4, “Mapping of Interrupt Causes”.
Field definitions are the same as those defined in Section 8.3.2.2.7.

8.2.2.26.12            VF Good Packets Transmitted Count - VFGPTC[n]
                       (0x00008300 + 0x4*n, n=0...63; RO)

PF mirror of the VFGPTC register.
Field definitions are the same as those defined in Section 8.3.2.6.5.

8.2.2.26.13            VF Good Octets Transmitted Count LSB - VFGOTC_LSB[n]
                       (0x00008400 + 0x8*n, n=0...63; RO)

PF mirror of the VFGOTC_LSB register.
Field definitions are the same as those defined in Section 8.3.2.6.6.

8.2.2.26.14            VF Good Octets Transmitted Count MSB - VFGOTC_MSB[n]
                       (0x00008404 + 0x8*n, n=0...63; RO)

PF mirror of the VFGOTC_MSB register.
Field definitions are the same as those defined in Section 8.3.2.6.7.

8.2.2.26.15            VF Multicast Packets Received Count - VFMPRC[n]
                       (0x0000D01C + 0x40*n, n=0...63; RO)

PF mirror of the VFMPRC register.
Field definitions are the same as those defined in Section 8.3.2.6.4.

333369-009                                                                                            777
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                       Programming Interface

8.2.2.26.16          VF Good Octets Received Count High - VFGORC_MSB[n]
                     (0x0000D020 + 0x40*n, n=0...63; RW)

PF mirror of the VFGORC_MSB register.
Field definitions are the same as those defined in Section 8.3.2.6.3.

8.2.2.26.17          VF Interrupt Vector Allocation Registers - VFIVAR[n]
                     (0x00012500 + 0x4*n, n=0...63; RW)

These registers map VF interrupt causes into MSI-X vectors (PF mirror). For more details, refer to
Section 7.3.4, “Mapping of Interrupt Causes”.
Field definitions are the same as those defined in Section 8.3.2.2.6.

8.2.2.26.18          PF Mailbox Memory - PFMBMEM[n,m] (0x00013000 + 0x4*n
                     + 0x40*m, n=0...15, m=0...63; RW)

Mailbox Memory for PF and VF Driver Communications. The mailbox size for each VM is 64 bytes
accessed by 16 x 32-bit registers. Locations can be accessed as 32- or 64-bit words. This is the
mapping of this memory in the PF space.
Field definitions are the same as those defined in Section 8.3.2.1.4.

778                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

### 8.2.3 BAR3 Registers Summary

Table 8-30. PF - MSI-X Table Registers Summary
                                                                                                                      Section
       Offset/Alias Offset         Abbreviation                                 Name
                                                                                                                      Number

0x00000000 + 0x10*n, n=0...255    MSIXTADD[n]        MSI-X Table Entry Lower Address                                  8.2.4.1.1

0x00000004 + 0x10*n, n=0...255    MSIXTUADD[n]       MSI-X Table Entry Upper Address                                  8.2.4.1.2

0x00000008 + 0x10*n, n=0...255    MSIXTMSG[n]        MSI-X Table Entry Message                                        8.2.4.1.3

0x0000000C + 0x10*n, n=0...255    MSIXVCTRL[n]       MSI-X Table Entry Vector Control                                 8.2.4.1.4

0x00002000 + 0x4*n, n=0...7       MSIXPBA[n]         MSIXPBA Bit Description                                          8.2.4.1.5

### 8.2.4 Detailed Register Descriptions - PF BAR3

#### 8.2.4.1 PF - MSI-X Table Registers

The MSI-X capability is described in Section 9.2.3.3. The MSI-X table is described in Section 9.2.3.3.4
and the Pending Bit Array (PBA) is described in Section 9.2.3.3.5. These registers are located in the
MSI-X BAR.

8.2.4.1.1              MSI-X Table Entry Lower Address - MSIXTADD[n]
                       (0x00000000 + 0x10*n, n=0...255)

    Field     Bit(s)    Init.    Type                                         Description

MSIXTADD10      1:0      00b     RW     Message Address 1:0
                                        For proper DWord alignment, software must always write zeros to these two bits;.
                                        Otherwise, the result is undefined. The state of these bits after reset must be 0b.
                                        These bits are permitted to be read-only or read/write.
MSIXTADD       31:2      0x0     RW     Message Address
                                        System-specified message lower address.
                                        For MSI-X messages, the contents of this field from an MSI-X table entry specifies the
                                        lower portion of the DWord-aligned address (AD[31:02]) for the memory write
                                        transaction. This field is read/write.

8.2.4.1.2              MSI-X Table Entry Upper Address - MSIXTUADD[n]
                       (0x00000004 + 0x10*n, n=0...255)

    Field     Bit(s)    Init.    Type                                         Description

MSIXTUADD      31:0      0x0     RW     Message Upper Address
                                        System-specified message upper address bits.
                                        If this field is zero, Single Address Cycle (SAC) messages are used. If this field is non-
                                        zero, Dual Address Cycle (DAC) messages are used. This field is read/write.

333369-009                                                                                                                    779
                                  Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

8.2.4.1.3                 MSI-X Table Entry Message - MSIXTMSG[n] (0x00000008 +
                          0x10*n, n=0...255)

      Field      Bit(s)   Init.   Type                                         Description

MSIXTMSG          31:0    0x0     RW     Message Data
                                         System-specified message data.
                                         For MSI-X messages, the contents of this field from an MSI-X table entry specifies the
                                         data driven on AD[31:0] during the memory write transaction's data phase. This field
                                         is read/write.

8.2.4.1.4                 MSI-X Table Entry Vector Control - MSIXVCTRL[n]
                          (0x0000000C + 0x10*n, n=0...255)

      Field      Bit(s)   Init.   Type                                         Description

MSIXVCTRL          0       1b     RW     Mask Bit
                                         When this bit is set, the function is prohibited from sending a message using this
                                         MSI-X table entry. However, any other MSI-X table entries programmed with the same
                                         vector are still capable of sending an equivalent message unless they are also
                                         masked.
                                         This bit's state after reset is 1b (entry is masked). This bit is read/write.
RESERVED          31:1    0x0     RSV    Reserved.
                                         After reset, the state of these bits must be 0b. However, for potential future use,
                                         software must preserve the value of these reserved bits when modifying the value of
                                         other Vector Control bits. If software modifies the value of these reserved bits, the
                                         result is undefined.

8.2.4.1.5                 MSIXPBA Bit Description - MSIXPBA[n] (0x00002000 +
                          0x4*n, n=0...7)

Note:         Registers 2...7 are usable only by the VFs in IOV mode. These registers are not exposed to
              the operating system by the Table Size field in the MSI-X Message Control word.

      Field      Bit(s)   Init.   Type                                         Description

PENBIT            31:0    0x0     RO     MSI-X Pending Bits
                                         Each bit is set to 1b when the appropriate interrupt request is set, and cleared to 0b
                                         when the appropriate interrupt request is cleared. Bit ‘i’ in register ‘N’ is associated
                                         with MSI-X vector 32*N+i, where N = 0...3.

780                                                                                                                   333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface
