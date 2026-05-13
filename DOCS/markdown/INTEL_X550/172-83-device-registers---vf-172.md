## 8.3 Device Registers - VF

### 8.3.1 BAR0 Registers Summary

Table 8-31. VF - General Control Registers Summary
                                                                                                      Section
      Offset/Alias Offset        Abbreviation                                 Name
                                                                                                      Number

0x00000000                      VFCTRL           VF Control Register                                  8.3.2.1.1

0x00000008                      VFSTATUS         VF Device Status Register                            8.3.2.1.2

0x00000010                      VFLINKS          Link Status Register                                 8.3.2.1.3

0x00000200 + 0x4*n, n=0...15    VFMBMEM[n]       VF Mailbox Memory                                    8.3.2.1.4

0x000002FC                      VFMAILBOX        VF Mailbox                                           8.3.2.1.5

Table 8-32. VF - Interrupt Registers Summary
                                                                                                      Section
     Offset/Alias Offset       Abbreviation                                   Name
                                                                                                      Number

0x00000100                     VFEICR           VF Extended Interrupt Cause                           8.3.2.2.1

0x00000104                     VFEICS           VF Extended Interrupt Cause Set                       8.3.2.2.2

0x00000108                     VFEIMS           VF Extended Interrupt Mask Set/Read                   8.3.2.2.3

0x0000010C                     VFEIMC           VF Extended Interrupt Mask Clear                      8.3.2.2.4

0x00000114                     VFEIAM           VF Extended Interrupt Auto Mask Enable                8.3.2.2.5

0x00000120 + 0x4*n, n=0...3    VFIVAR[n]        VF Interrupt Vector Allocation Registers              8.3.2.2.6

0x00000140                     VFIVAR_MISC      VF Interrupt Vector Allocation Registers Misc         8.3.2.2.7

0x00000148                     VFPBACL          VF MSI-X PBA Clear                                    8.3.2.2.8

0x00000180 + 0x4*n, n=0...1    VFRSCINT[n]      VF RSC Enable Interrupt                               8.3.2.2.9

0x00000820 + 0x4*n, n=0...1    VFEITR[n]        VF Extended Interrupt Throttle Registers              8.3.2.2.10

Table 8-33. VF - Receive Registers Summary
                                                                                                      Section
      Offset/Alias Offset        Abbreviation                                 Name
                                                                                                      Number

0x00000300                      VFPSRTYPE        VF Replication Packet Split Receive Type Register    8.3.2.3.1

0x00001000 + 0x40*n, n=0...7    VFRDBAL[n]       VF Receive Descriptor Base Address Low               8.3.2.3.2

0x00001004 + 0x40*n, n=0...7    VFRDBAH[n]       VF Receive Descriptor Base Address High              8.3.2.3.3

0x00001008 + 0x40*n, n=0...7    VFRDLEN[n]       VF Receive Descriptor Length                         8.3.2.3.4

0x00001010 + 0x40*n, n=0...7    VFRDH[n]         VF Receive Descriptor Head                           8.3.2.3.5

0x00001014 + 0x40*n, n=0...7    VFSRRCTL[n]      VF Split and Replication Receive Control Registers   8.3.2.3.6

0x00001018 + 0x40*n, n=0...7    VFRDT[n]         VF Receive Descriptor Tail                           8.3.2.3.7

0x00001028 + 0x40*n, n=0...7    VFRXDCTL[n]      VF Receive Descriptor Control                        8.3.2.3.8

0x0000102C + 0x40*n, n=0...7    VFRSCCTL[n]      VF RSC Control                                       8.3.2.3.9

0x00003000                      VFMRQC           VF Multiple Receive Queues Command Register          8.3.2.3.10

333369-009                                                                                                    781
                                  Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                     Programming Interface

Table 8-33. VF - Receive Registers Summary [continued]
                                                                                                                 Section
      Offset/Alias Offset       Abbreviation                                     Name
                                                                                                                 Number

0x00003100 + 0x4*n, n=0...9     VFRSSRK[n]         VF RSS Random Key Register                                    8.3.2.3.11

0x00003200 + 0x4*n, n=0...15    VFRETA[n]          VF Redirection Table                                          8.3.2.3.12

Table 8-34. VF - Transmit Registers Summary
                                                                                                                 Section
      Offset/Alias Offset       Abbreviation                                     Name
                                                                                                                 Number

0x00002000 + 0x40*n, n=0...7    VFTDBAL[n]         VF Transmit Descriptor Base Address Low                       8.3.2.4.1

0x00002004 + 0x40*n, n=0...7    VFTDBAH[n]         VF Transmit Descriptor Base Address High                      8.3.2.4.2

0x00002008 + 0x40*n, n=0...7    VFTDLEN[n]         VF Transmit Descriptor Length                                 8.3.2.4.3

0x00002010 + 0x40*n, n=0...7    VFTDH[n]           VF Transmit Descriptor Head                                   8.3.2.4.4

0x00002018 + 0x40*n, n=0...7    VFTDT[n]           VF Transmit Descriptor Tail                                   8.3.2.4.5

0x00002028 + 0x40*n, n=0...7    VFTXDCTL[n]        VF Transmit Descriptor Control                                8.3.2.4.6

0x00002038 + 0x40*n, n=0...7    VFTDWBAL[n]        VF Tx Descriptor Completion Write Back Address Low            8.3.2.4.7

0x0000203C + 0x40*n, n=0...7    VFTDWBAH[n]        VF Tx Descriptor Completion Write Back Address High           8.3.2.4.8

Table 8-35. VF - TPH Registers Summary
                                                                                                                 Section
      Offset/Alias Offset           Abbreviation                                  Name
                                                                                                                 Number

0x0000100C + 0x40*n, n=0...7    VFTPH_RXCTRL[n]       VF Rx TPH Control Register                                 8.3.2.5.1

0x0000200C + 0x40*n, n=0...7    VFTPH_TXCTRL[n]       VF Tx TPH Control Registers                                8.3.2.5.2

Table 8-36. VF - Statistic Registers Summary
                                                                                                                 Section
 Offset/Alias Offset   Abbreviation                                       Name
                                                                                                                 Number

0x0000101C             VFGPRC          VF Good Packets Received Count                                            8.3.2.6.1

0x00001020             VFGORC_LSB      VF Good Octets Received Count Low                                         8.3.2.6.2

0x00001024             VFGORC_MSB      VF Good Octets Received Count High                                        8.3.2.6.3

0x00001034             VFMPRC          VF Multicast Packets Received Count                                       8.3.2.6.4

0x0000201C             VFGPTC          VF Good Packets Transmitted Count                                         8.3.2.6.5

0x00002020             VFGOTC_LSB      VF Good Octets Transmitted Count LSB                                      8.3.2.6.6

0x00002024             VFGOTC_MSB      VF Good Octets Transmitted Count MSB                                      8.3.2.6.7

782                                                                                                              333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

### 8.3.2 Detailed Register Descriptions - VF BAR0

#### 8.3.2.1 VF - General Control Registers

8.3.2.1.1                 VF Control Register - VFCTRL (0x00000000)

      Field    Bit(s)     Init.     Type                                           Description

RESERVED       25:0       0x0       RSV      Reserved.
RST             26         0b       WO       VF Reset
                                             This bit performs a reset of the queue enable and the interrupt registers of the VF.
RESERVED       31:27      0x0       RSV      Reserved.

8.3.2.1.2                 VF Device Status Register - VFSTATUS (0x00000008; RO)

This register is a mirror of the PF status register.
Field definitions are the same as those defined in Section 8.2.2.1.2.

8.3.2.1.3                 Link Status Register - VFLINKS (0x00000010; RO)

This register is the mapping of the PF's LINKS register.
Field definitions are the same as those defined in Section 8.2.2.16.7.

8.3.2.1.4                 VF Mailbox Memory - VFMBMEM[n] (0x00000200 + 0x4*n,
                          n=0...15)

Mailbox Memory for PF and VF driver communications. The mailbox size for each VM is 64 bytes
accessed by 16 x 32-bit registers. Locations can be accessed as 32- or 64-bit words.

       Field     Bit(s)     Init.     Type                                           Description

MAILBOX_DATA      31:0          X     RW        Mailbox Data
                                                Mailbox data is composed of 16 x 4 byte registers.

8.3.2.1.5                 VF Mailbox - VFMAILBOX (0x000002FC)

This register is cleared by VLFR (excluding the RSTI bit).

      Field    Bit(s)     Init.     Type                                           Description

REQ              0         0b       WO       Request
                                             Request for PF Ready.
                                             Setting this bit, causes an interrupt to the PF. This bit always reads as 0b. Setting this
                                             bit sets the corresponding bit in the VFREQ field in PFMBICR register
                                             (Section 8.2.2.22.2).
ACK              1         0b       WO       Acknowledge
                                             PF message received.
                                             Setting this bit, causes an interrupt to the PF. This bit always reads as 0b. Setting this
                                             bit sets the corresponding bit in the VFACK field in PFMBICR register.

333369-009                                                                                                                          783
                                     Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                  Programming Interface

      Field   Bit(s)    Init.   Type                                         Description

VFU             2        0b     RW     VFU
                                       Buffer is taken by VF.
                                       This bit can be set only if the PFU bit is cleared and is mirrored in the VFU bit of the
                                       PFMAILBOX register (Section 8.2.2.22.8).
PFU             3        0b     RW     PFU
                                       Buffer is taken by PF.
                                       This bit is RO for the VF and is a mirror of the PFU bit of the PFMAILBOX register.
PFSTS           4        0b      RC    PF Status
                                       PF wrote a message in the mailbox.
PFACK           5        0b      RC    PF Acknowledge
                                       PF acknowledged the VF previous message.
RSTI            6        1b      RO    Reset Indication
                                       Indicates that the PF reset the shared resources and the reset sequence is in
                                       progress. This bit is not affected by VFLR.
RSTD            7        0b      RC    Reset Done
                                       Indicates that a PF software reset completed.
RESERVED      31:8      0x0     RSV    Reserved.

#### 8.3.2.2 VF - Interrupt Registers

8.3.2.2.1              VF Extended Interrupt Cause - VFEICR (0x00000100)

      Field   Bit(s)    Init.   Type                                         Description

MSIX           2:0      000b    RW1C   MSI-X
                                       Indicates an interrupt cause mapped to MSI-X vectors 2:0.
RESERVED      31:3      0x0     RSV    Reserved.

8.3.2.2.2              VF Extended Interrupt Cause Set - VFEICS (0x00000104)

      Field   Bit(s)    Init.   Type                                         Description

MSIX           2:0      000b    WO     MSI-X
                                       Sets to the corresponding EICR bit of MSI-X vectors 2:0.
RESERVED      31:3      0x0     RSV    Reserved.

8.3.2.2.3              VF Extended Interrupt Mask Set/Read - VFEIMS
                       (0x00000108)

      Field   Bit(s)    Init.   Type                                         Description

MSIX           2:0      000b    RWS    MSI-X
                                       Sets the Mask bit for the corresponding EICR bit of MSI-X vectors 2:0.
RESERVED      31:3      0x0     RSV    Reserved.

784                                                                                                                  333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.3.2.2.4                    VF Extended Interrupt Mask Clear - VFEIMC (0x0000010C)

    Field      Bit(s)         Init.         Type                                         Description

MSIX            2:0           000b            WO     MSI-X
                                                     Clears the Mask bit for the corresponding EICR bit of MSI-X vectors 2:0.
RESERVED       31:3            0x0          RSV      Reserved.

8.3.2.2.5                    VF Extended Interrupt Auto Mask Enable - VFEIAM
                             (0x00000114)

    Field      Bit(s)         Init.         Type                                         Description

MSIX            2:0           000b            RW     MSI-X
                                                     Auto-mask bit for the corresponding EICR bit of MSI-X vectors 2:0.
RESERVED       31:3            0x0          RSV      Reserved.

8.3.2.2.6                    VF Interrupt Vector Allocation Registers - VFIVAR[n]
                             (0x00000120 + 0x4*n, n=0...3)

These registers map VF interrupt causes into MSI-X vectors. For more details, refer to Section 7.3.4,
“Mapping of Interrupt Causes”.

       Field          Bit(s)          Init.        Type                                     Description

INT_ALLOC_0              0             0b          RW     Interrupt Allocation 0
                                                          Defines the MSI-X vector (0 or 1) assigned to Rx queue ‘2*N’ for IVAR ‘N’
                                                          register (N=0...3).
RESERVED                6:1           0x0          RSV    Reserved.
INT_ALLOC_VAL_0          7             0b          RW     Interrupt Allocation Valid 0
                                                          Valid bit for INT_ALLOC[0].
INT_ALLOC_1              8             0b          RW     Interrupt Allocation 1
                                                          Defines the MSI-X vector (0 or 1) assigned to Tx queue ‘2*N’ for IVAR ‘N’
                                                          register (N=0...3).
RESERVED                14:9          0x0          RSV    Reserved.
INT_ALLOC_VAL_1         15             0b          RW     Interrupt Allocation Valid 1
                                                          Valid bit for INT_ALLOC[1].
INT_ALLOC_2             16             0b          RW     Interrupt Allocation 2
                                                          Defines the MSI-X vector (0 or 1) assigned to Rx queue ‘2*N+1’ for IVAR ‘N’
                                                          register (N=0...3).
RESERVED              22:17           0x0          RSV    Reserved.
INT_ALLOC_VAL_2         23             0b          RW     Interrupt Allocation Valid 2
                                                          Valid bit for INT_ALLOC[2].
INT_ALLOC_3             24             0b          RW     Interrupt Allocation 3
                                                          Defines the MSI-X vector (0 or 1) assigned to Tx queue ‘2*N+1’ for IVAR ‘N’
                                                          register (N=0...3).
RESERVED              30:25           0x0          RSV    Reserved.
INT_ALLOC_VAL_3         31             0b          RW     Interrupt Allocation Valid 3
                                                          Valid bit for INT_ALLOC[3].

333369-009                                                                                                                              785
                                              Did this document help answer your questions?

                                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                                              Programming Interface

8.3.2.2.7                     VF Interrupt Vector Allocation Registers Misc -
                              VFIVAR_MISC (0x00000140)

This register maps the mailbox interrupt into MSI-X vector. For more details, refer to Section 7.3.4,
“Mapping of Interrupt Causes”.

        Field          Bit(s)          Init.        Type                                    Description

INT_ALLOC_0              1:0            X           RW     Interrupt Allocation 0
                                                           Defines the MSI-X vector assigned to the mailbox interrupt.
RESERVED                 6:2           0x0          RSV    Reserved.
INT_ALLOC_VAL_0           7             0b          RW     Interrupt Allocation Valid 0
                                                           Valid bit for INT_ALLOC[0].
RESERVED                 31:8          0x0          RSV    Reserved.

8.3.2.2.8                     VF MSI-X PBA Clear - VFPBACL (0x00000148)

      Field     Bit(s)         Init.         Type                                         Description

PENBIT           2:0            0x0          RW1C     MSI-X Pending Bits Clear
                                                      MSI-X Pending Bits Clear.
                                                      Writing a 1b to any bit clears the corresponding MSIXPBA bit. Writing a 0b has no
                                                      effect. Reading this register returns the PBA vector.
RESERVED        31:3            0x0          RSV      Reserved.

8.3.2.2.9                     VF RSC Enable Interrupt - VFRSCINT[n] (0x00000180 +
                              0x4*n, n=0...1; RW)

Field definitions are the same as those defined in Section 8.2.2.6.20.

8.3.2.2.10                    VF Extended Interrupt Throttle Registers - VFEITR[n]
                              (0x00000820 + 0x4*n, n=0...1; RW)

Field definitions are the same as those defined in Section 8.2.2.6.4.

#### 8.3.2.3 VF - Receive Registers

8.3.2.3.1                     VF Replication Packet Split Receive Type Register -
                              VFPSRTYPE (0x00000300; RW)

Field definitions are the same as those defined in Section 8.2.2.8.17.

8.3.2.3.2                     VF Receive Descriptor Base Address Low - VFRDBAL[n]
                              (0x00001000 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.1.

786                                                                                                                            333369-009
                                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.3.2.3.3              VF Receive Descriptor Base Address High - VFRDBAH[n]
                       (0x00001004 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.2.

8.3.2.3.4              VF Receive Descriptor Length - VFRDLEN[n] (0x00001008 +
                       0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.3.

8.3.2.3.5              VF Receive Descriptor Head - VFRDH[n] (0x00001010 +
                       0x40*n, n=0...7; RO)

Field definitions are the same as those defined in Section 8.2.2.9.4.

8.3.2.3.6              VF Split and Replication Receive Control Registers -
                       VFSRRCTL[n] (0x00001014 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.5.

8.3.2.3.7              VF Receive Descriptor Tail - VFRDT[n] (0x00001018 +
                       0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.6.

8.3.2.3.8              VF Receive Descriptor Control - VFRXDCTL[n] (0x00001028
                       + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.7.

8.3.2.3.9              VF RSC Control - VFRSCCTL[n] (0x0000102C + 0x40*n,
                       n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.9.8.

8.3.2.3.10             VF Multiple Receive Queues Command Register - VFMRQC
                       (0x00003000)

       Field         Bit(s)   Init.     Type                                  Description

RSSE                   0       0b        RW    RSS Enable
                                               This bit enables the VF RSS mechanism.
                                                0b = VF RSS disabled.
                                                1b = VF RSS enable.
RESERVED             15:1     0x0        RSV   Reserved.

333369-009                                                                                  787
                                    Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                             Programming Interface

      Field        Bit(s)   Init.   Type                                    Description

RSS_FIELD_ENABLE   31:16    0x0      RW     RSS Field Enable
                                            Each bit, when set, enables a specific field selection to be used by the hash
                                            function. Several bits can be set at the same time.
                                              Bit[16]      = Enable TcpIPv4 hash function.
                                              Bit[17]      = Enable IPv4 hash function.
                                              Bit[18]      = Reserved.
                                              Bit[19]      = Reserved.
                                              Bit[20]      = Enable IPv6 hash function.
                                              Bit[21]      = Enable TcpIPv6 hash function.
                                              Bit[22]      = Enable UdpIPV4.
                                              Bit[23]      = Enable UdpIPV6.
                                              Bit[24]      = Reserved.
                                              Bits[31:25] = Reserved; 0x0.
                                            Note: On Tunnel packets IPv4-IPv6, only the IPv4 header might be used for
                                                      the RSS filtering.

8.3.2.3.11           VF RSS Random Key Register - VFRSSRK[n] (0x00003100 +
                     0x4*n, n=0...9; RW)

PF mirror of VFRSSK registers of the VFs.
Field definitions are the same as those defined in Section 8.2.2.8.25.

8.3.2.3.12           VF Redirection Table - VFRETA[n] (0x00003200 + 0x4*n,
                     n=0...15; RW)

VF version of VFRETA registers. The redirection table has 64 entries in 16 registers.
Field definitions are the same as those defined in Section 8.2.2.8.26.

#### 8.3.2.4 VF - Transmit Registers

8.3.2.4.1            VF Transmit Descriptor Base Address Low - VFTDBAL[n]
                     (0x00002000 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.5.

8.3.2.4.2            VF Transmit Descriptor Base Address High - VFTDBAH[n]
                     (0x00002004 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.6.

8.3.2.4.3            VF Transmit Descriptor Length - VFTDLEN[n] (0x00002008
                     + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.7.

788                                                                                                           333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.3.2.4.4              VF Transmit Descriptor Head - VFTDH[n] (0x00002010 +
                       0x40*n, n=0...7; RO)

Field definitions are the same as those defined in Section 8.2.2.10.8.

8.3.2.4.5              VF Transmit Descriptor Tail - VFTDT[n] (0x00002018 +
                       0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.9.

8.3.2.4.6              VF Transmit Descriptor Control - VFTXDCTL[n] (0x00002028
                       + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.10.

8.3.2.4.7              VF Tx Descriptor Completion Write Back Address Low -
                       VFTDWBAL[n] (0x00002038 + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.11.

8.3.2.4.8              VF Tx Descriptor Completion Write Back Address High -
                       VFTDWBAH[n] (0x0000203C + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.10.12.

#### 8.3.2.5 VF - TPH Registers

8.3.2.5.1              VF Rx TPH Control Register - VFTPH_RXCTRL[n]
                       (0x0000100C + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.12.1.

8.3.2.5.2              VF Tx TPH Control Registers - VFTPH_TXCTRL[n]
                       (0x0000200C + 0x40*n, n=0...7; RW)

Field definitions are the same as those defined in Section 8.2.2.12.3.

333369-009                                                                       789
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

#### 8.3.2.6 VF - Statistics Registers

Registers in this section are RO by VF and RW by PF. Statistics are reset by PF clearing the register.

8.3.2.6.1               VF Good Packets Received Count - VFGPRC (0x0000101C)

      Field   Bit(s)     Init.    Type                                         Description

VFGPRC        31:0       0x0      RW      VF Good Packets Received Count
                                          Number of good packets received for this VF (of any length). This counter includes
                                          loopback packets or replications of multicast packets. The counter is not cleared on
                                          read. Furthermore, the register is a cyclic counter incrementing from 0xFFFF to
                                          0x0000.

8.3.2.6.2               VF Good Octets Received Count Low - VFGORC_LSB
                        (0x00001020)

      Field    Bit(s)     Init.    Type                                        Description

VFGORC_LSB      31:0       0x0     RW      VF Good Octets Received Count LSB
                                           Number of good octets received (32 LSB of a 36-bit counter) by the queues
                                           allocated to this VF.
                                           The counter includes loopback packets or replications of multicast packets.
                                           This register includes bytes received in a packet from the Destination Address field
                                           through the CRC field, inclusively. Octets are counted on the VF interface rather than
                                           on the network interface. For example, LinkSec octets are not counted.
                                           Bytes of RSC are counted before coalescing. The counter is not cleared on read.
                                           Furthermore, the register is a cyclic counter incrementing from 0xFFFF to 0x0000.

8.3.2.6.3               VF Good Octets Received Count High - VFGORC_MSB
                        (0x00001024)

      Field    Bit(s)     Init.    Type                                        Description

VFGORC_MSB      3:0        0x0     RW      VF Good Octets Received Count MSB
                                           Number of good octets received (4 MSB of a 36-bit counter) by the queues allocated
                                           to this VF (see Section 8.3.2.6.2 for more details).
                                           The counter is not cleared on read. Furthermore, the register is a cyclic counter
                                           incrementing from 0xF to 0x0.
RESERVED        31:4       0x0     RSV     Reserved.

8.3.2.6.4               VF Multicast Packets Received Count - VFMPRC
                        (0x00001034)

      Field   Bit(s)     Init.    Type                                         Description

VFMPRC        31:0       0x0      RO      VF Multicast Packets Received Count
                                          Number of multicast good packets received by this VF (of any length) that pass the
                                          Ethernet MAC Address filtering (excluding broadcast packets).
                                          The counter does not count received flow control packets. This register increments
                                          only if receives are enabled. This register does not count packets counted by the
                                          Missed Packet Count (MPC) register.
                                          This counter also includes loopback packets or replications of multicast packets. The
                                          counter is not cleared on read. Furthermore, the register is a cyclic counter
                                          incrementing from 0xFFFF to 0x0000.

790                                                                                                                  333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.3.2.6.5              VF Good Packets Transmitted Count - VFGPTC (0x0000201C)

    Field     Bit(s)    Init.   Type                                        Description

VFGPTC         31:0     0x0      RO    VF Good Packets Transmitted Count
                                       Number of good packets sent by the queues allocated to this VF.
                                       A packet is considered as transmitted if it is was forwarded to the MAC unit for
                                       transmission to the network and/or is accepted by the internal Tx to Rx switch
                                       enablement logic. Packets dropped due to anti-spoofing filtering or loopback packets
                                       that are rejected by the Tx to Rx switch are not counted.
                                       The counter is not cleared on read. Furthermore, the register is a cyclic counter
                                       incrementing from 0xFFFF to 0x0000.

8.3.2.6.6              VF Good Octets Transmitted Count LSB - VFGOTC_LSB
                       (0x00002020)

    Field     Bit(s)    Init.   Type                                        Description

VFGOTC_LSB     31:0     0x0      RO    VF Good Octets Transmitted Count LSB
                                       Number of good octets transmitted (32 LSB of a 36-bit counter) by the queues
                                       allocated to this VF.
                                       This register includes bytes transmitted in a packet from the Destination Address field
                                       through the CRC field, inclusively. This register counts octets of the packets counted
                                       by the VFGPTC register. Octets are counted on the VF interface rather than on the
                                       network interface. For example, LinkSec octets are not counted.
                                       The counter is not cleared on read. Furthermore, the register is a cyclic counter
                                       incrementing from 0xFFFF to 0x0000.

8.3.2.6.7              VF Good Octets Transmitted Count MSB - VFGOTC_MSB
                       (0x00002024)

    Field     Bit(s)    Init.   Type                                        Description

VFGOTC_MSB      3:0     0x0      RO    VF Good Octets Transmitted Count MSB
                                       Number of good octets transmitted (4 MSB of a 36-bit counter) by the queues
                                       allocated to this VF (see Section 8.3.2.6.6 for more details).
                                       The counter is not cleared on read. Furthermore, the register is a cyclic counter
                                       incrementing from 0xF to 0x0.
RESERVED       31:4     0x0      RSV   Reserved.

333369-009                                                                                                                 791
                                 Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                       Programming Interface

### 8.3.3 BAR3 Registers Summary

Table 8-37. VF - MSI-X Table Registers Summary
                                                                                                                          Section
       Offset/Alias Offset            Abbreviation                                  Name
                                                                                                                          Number

0x00000000 + 0x10*n, n=0...2         VFMSIXTADD[n]       MSI-X Table Entry Lower Address                                 8.3.4.1.1

0x00000004 + 0x10*n, n=0...2         VFMSIXTUADD[n]      MSI-X Table Entry Upper Address                                 8.3.4.1.2

0x00000008 + 0x10*n, n=0...2         VFMSIXTMSG[n]       MSI-X Table Entry Message                                       8.3.4.1.3

0x0000000C + 0x10*n, n=0...2         VFMSIXVCTRL[n]      MSI-X Table Entry Vector Control                                8.3.4.1.4

0x00002000                           VFMSIXPBA           MSIXPBA Bit Description                                         8.3.4.1.5

### 8.3.4 Detailed Register Descriptions - VF BAR3

#### 8.3.4.1 VF - MSI-X Table Registers

8.3.4.1.1                 MSI-X Table Entry Lower Address - VFMSIXTADD[n]
                          (0x00000000 + 0x10*n, n=0...2)

      Field      Bit(s)      Init.     Type                                        Description

MSIXTADD_10       1:0         00b      RW      Message Address 1:0
                                               For proper DWord alignment, software must always write zeros to these two bits.
                                               Otherwise, the result is undefined. The state of these bits after reset must be 0b.
                                               These bits are permitted to be read-only or read/write.
MSIXTADD          31:2        0x0      RW      Message Address
                                               System-specified message lower address.
                                               For MSI-X messages, the contents of this field from an MSI-X table entry specifies
                                               the lower portion of the DWord-aligned address (AD[31:02]) for the memory write
                                               transaction. This field is read/write.

8.3.4.1.2                 MSI-X Table Entry Upper Address - VFMSIXTUADD[n]
                          (0x00000004 + 0x10*n, n=0...2)

      Field     Bit(s)     Init.     Type                                          Description

MSIXTUADD       31:0         0x0      RW      Message Upper Address
                                              System-specified message upper address bits. If this field is zero, Single Address
                                              Cycle (SAC) messages are used. If this field is non-zero, Dual Address Cycle (DAC)
                                              messages are used. This field is read/write.

792                                                                                                                      333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

8.3.4.1.3                   MSI-X Table Entry Message - VFMSIXTMSG[n] (0x00000008
                            + 0x10*n, n=0...2)

    Field       Bit(s)      Init.     Type                                         Description

MSIXTMSG         31:0       0x0       RW       Message Data
                                               System-specified message data.
                                               For MSI-X messages, the contents of this field from an MSI-X table entry specifies the
                                               data driven on AD[31:0] during the memory write transaction's data phase. This field
                                               is read/write.

8.3.4.1.4                   MSI-X Table Entry Vector Control - VFMSIXVCTRL[n]
                            (0x0000000C + 0x10*n, n=0...2)

    Field       Bit(s)      Init.     Type                                         Description

MSIXVCTRL         0          1b       RW       Mask Bit
                                               When this bit is set, the function is prohibited from sending a message using this
                                               MSI-X table entry. However, any other MSI-X table entries programmed with the same
                                               vector are still capable of sending an equivalent message unless they are also
                                               masked.
                                               This bit's state after reset is 1b (entry is masked). This bit is read/write.
RESERVED         31:1       0x0       RSV      Reserved.
                                               After reset, the state of these bits must be 0b. However, for potential future use,
                                               software must preserve the value of these reserved bits when modifying the value of
                                               other Vector Control bits. If software modifies the value of these reserved bits, the
                                               result is undefined.

8.3.4.1.5                   MSIXPBA Bit Description - VFMSIXPBA (0x00002000)

Note:        If a page size larger than 8 K is programmed in the IOV structure, the address of the MSIX
             PBA table moves to be page aligned.

     Field        Bit(s)      Init.     Type                                         Description

PENDING_BITS          2:0     000b       RO      Pending Bits
                                                 For each pending bit that is set, the function has a pending message for the
                                                 associated MSI-X Table entry.
                                                 Pending bits that have no associated MSI-X table entry are reserved.
RESERVED           31:3        0x0      RSV      Reserved.

333369-009                                                                                                                        793
                                       Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                               Programming Interface

NOTE:   This page intentionally left blank.

794                                                                                        333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

Chapter 9                     PCIe Programming Interface
