## 9.3 Virtual Functions Configuration Space

The configuration space reflected to each of the VF is a sparse version of the physical function
configuration space. Table 9-36 describes the behavior of each register in the VF configuration space.

Table 9-36. VF PCIe Configuration Space
    Section        Offset               Name              VF behavior                          Notes

# 0 Vendor ID               RO — 0xFFFF

# 2 Device ID               RO — 0xFFFF

# 4 Command                 Per VF                 See Section 9.3.1.1.

# 6 Status                  Per VF                 See Section 9.3.1.2.

# 8 RevisionID              RO as PF

# 9 Class Code              RO as PF

                     C       Cache Line Size         RO — 0x0

                     D       Latency Timer           RO — 0x0

                     E       Header Type             RO — 0x0
PCI Mandatory
                     F       Reserved                RO — 0x0
Registers
                  10 — 27    BARs                    RO — 0x0               Emulated by VMM.

# 28 CardBus CIS             RO — 0x0               Not used.

                    2C       Sub Vendor ID           RO as PF

                    2E       Sub System              RO as PF

# 30 Expansion ROM           RO — 0x0               Emulated by VMM.

# 34 Cap Pointer             RO — 0x70              Next = MSI-X capability.

                    3C       Int Line                RO — 0x0

                    3D       Int Pin                 RO — 0x0

                    3E       Max Lat/Min Gnt         RO — 0x0

    70 MSI-X Header            RO — 0xA011            Next = PCIe capability.

    72 MSI-x Message Control   Per VF                 See Section 9.3.2.1.1.

MSI-X
Capability          74       MSI-X table Address     RO — as PF             See Section 9.3.2.1.2

    78 MSI-X PBA Address       RO                     See Section 9.3.2.1.3

333369-009                                                                                             853
                                    Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                             PCIe Programming Interface

Table 9-36. VF PCIe Configuration Space [continued]
      Section      Offset              Name                VF behavior                              Notes

                     A0       PCIe Header             RO — 0x0010                Next = Last capability.

                     A2       PCIe Capabilities       RO — as PF

                     A4       PCIe Dev Cap            RO — as PF

                                                                                 As PF apart from FLR — See
                     A8       PCIe Dev Ctrl           RW
                                                                                 Section 9.3.2.2.1.

                     AA       PCIe Dev Status         Per VF                     See Section 9.3.2.2.2.

PCIe Capability      AC       PCIe Link Cap           RO — as PF

                     B0       PCIe Link Ctrl          RO — 0x0

                     B2       PCIe Link Status        RO — 0x0

                     C4       PCIe Dev Cap 2          RO — as PF

                     C8       PCIe Dev Ctrl 2         RO — 0x0

                     D0       PCIe Link Ctrl 2        RO — 0x0

                     D2       PCIe Link Status 2      RO — 0x0

                    100       AER — Header            RO — 0x15010001            Next = ARI structure.

                    104       AER — Uncorr Status     Per VF                     See Section 9.3.3.1.1.

                    108       AER — Uncorr Mask       RO — 0x0

                    10C       AER — Uncorr Severity   RO — 0x0
AER Capability
                    110       AER — Corr Status       Per VF                     See Section 9.3.3.1.2.

                    114       AER — Corr Mask         RO — 0x0

                    118       AER — Cap/Ctrl          RO as PF

                                                      Shared two logs for all    Same structure as in PF. In case of
                  11C — 128   AER — Error Log
                                                      VFs                        overflow, the header log is filled with ones.

                    150       ARI — Header            0x1A01000E                 Next = TPH.
ARI Capability
                    154       ARI — Cap/Ctrl          RO — 0X0

                    1A0       TPH - Header            RO - 0x1B010017            Next = ACS.

TPH Capability      1A4       TPH - Capability        RO - 0x00000005            No ST Table.

                    1A8       TPH - Control           Per VF                     Same structure as PF.

                    1B0       ACS - Header            RO - 0x0001000D            Last extended capability.
ACS capability
                    1B4       ACS - Capability        RO - 0x00000000

854                                                                                                                333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

### 9.3.1 Mandatory Configuration Space

#### 9.3.1.1 VF Command Register (0x4; RW)

 Bit(s)      Init.   Type                                               Description

   0          0b     RO     IOAE
                            I/O Access Enable. RO as zero field.
   1          0b     RO     MAE
                            Memory Access Enable. RO as zero field.
   2          0b     RW     BME
                            Bus Master Enable.
                            Disabling this bit prevents the associated VF from issuing any memory or I/O requests. Note that as
                            MSI/MSI-X interrupt messages are in-band memory writes, disabling the bus master enable bit
                            disables MSI/MSI-X interrupt messages as well.
                            Requests other than memory or I/O requests are not controlled by this bit.
                            Note: The state of active transactions is not specified when this bit is disabled after being enabled.
                                     The device can choose how it behaves when this condition occurs. Software cannot count on
                                     the device retaining state and resuming without loss of data when the bit is re-enabled.
                            Transactions for a VF that has its Bus Master Enable set must not be blocked by transactions for VFs
                            that have their Bus Master Enable cleared.
   3          0b     RO     SCM
                            Special Cycle Enable. Hard-wired to 0b
   4          0b     RO     MWIE
                            MWI Enable. Hard-wired to 0b.
   5          0b     RO     PSE
                            Palette Snoop Enable. Hard-wired to 0b.
   6          0b     RO     PER
                            Parity Error Response. Zero for VFs.
   7          0b     RO     WCE: Wait Cycle Enable
                            Hard-wired to 0b.
   8          0b     RO     SERRE
                            SERR# Enable. Zero for VFs.
   9          0b     RO     FB2BE
                            Fast Back-to-Back Enable. Hard-wired to 0b.
   10         0b     RO     INTD
                            Interrupt Disable. Hard-wired to 0b.
 15:11       0x0     RO     Reserved.

#### 9.3.1.2 VF Status Register (0x6; RW)

 Bit(s)      Init.   Type                                                 Description

  2:0        0x0      RO     Reserved.
   3          0b      RO     IS.
                             Interrupt Status. Hard-wired to 0b.
   4          1b      RO     NC
                             New Capabilities.
                             Indicates that the X550 VFs implement extended capabilities. X550 VFs implement a capabilities list,
                             to indicate that it supports MSI-X and PCIe extensions.
   5          0b      RO     66E

# 66 MHz Capable. Hard-wired to 0b.

   6          0b      RO     Reserved.

333369-009                                                                                                                     855
                                    Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                PCIe Programming Interface

 Bit(s)     Init.     Type                                                Description

      7      0b        RO      FB2BC
                               Fast Back-to-Back Capable. Hard-wired to 0b.
      8      0b       RW1C     MPERR
                               Data Parity Reported.
  10:9      00b        RO      DEVSEL
                               DEVSEL Timing. Hard-wired to 0b.
   11        0b       RW1C     STA
                               Signaled Target Abort.
   12        0b       RW1C     RTA
                               Received Target Abort.
   13        0b       RW1C     RMA
                               Received Master Abort.
   14        0b       RW1C     SSERR
                               Signaled System Error.
   15        0b       RW1C     DSERR
                               Detected Parity Error.

### 9.3.2 PCI Capabilities

#### 9.3.2.1 MSI-X Capability

The only registers with a different layout than the PF for MSI-X, is the control register.
Note:       The message address and data registers in enhanced mode use the first MSI-X entry of each
            VF in the regular MSI-X table.
See Section 8.3.4.1 for details of the MSI-X registers in BAR 3 of the VF.

9.3.2.1.1                  VF MSI-X Control Register (0x72; RW)

 Bit(s)     Init.     Type                                               Description

    1 RO      TS

  10:0      0x2
                              Table Size.
 13:11      000b      RO      Reserved.
   14        0b       RW      Mask
                              Function Mask.
   15        0b       RW      En
                              MSI-X Enable.

1. Default value is read from the NVM. This field is loaded from the PCI_CNF2.MSI_X_VF_N register field.

856                                                                                                              333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.3.2.1.2                 MSI-X Table Offset Register (0x74; RW)

 Bit(s)      Init.   Type                                                Description

  2:0        011b    RO      Table BIR
                             Indicates which one of a function’s BARs, beginning at 0x10 in the configuration space, is used to map
                             the function’s MSI-X table into the memory space. BIR values: 0...5 correspond to BARs 0x10…0x24,
                             respectively. BIR equals 3 to indicate BAR 3 and 4 are used for MSI-X vectors.
  31:3       0x0     RO      Table Offset
                             Used as an offset from the address contained in one of the function’s BARs to point to the base of the
                             MSI-X table. The lower three Table BIR bits are masked off (set to 0b) by software to form a 32-bit
                             QWord-aligned offset.
                             This field is read only.

9.3.2.1.3                 MSI-X PBA Register (0x78; RO)

 Bit(s)      Init.   Type                                                Description

  2:0        011b    RO      PBA BIR
                             Indicates which one of a function’s BARs, located beginning at 0x10 in configuration space, is used to
                             map the function’s MSI-X PBA into memory space. BIR values: 0...5 correspond to BARs 0x10…0x24,
                             respectively. BIR equals 3 to indicate BAR 3 and 4 are used for MSI-X PBA.
  31:3    0x400      RO      PBA Offset
                             Used as an offset from the address contained by one of the function’s BARs to point to the base of the
                             MSI-X PBA. The lower three PBA BIR bits are masked off (set to zero) by software to form a 32-bit
                             QWord-aligned offset.
                             This value is changed by hardware to be half of the value programmed to the IOV System Page Size
                             register.

#### 9.3.2.2 PCIe Capability Registers

The Device Control and Device Status registers have some fields which are specific per VF.

9.3.2.2.1                   VF Device Control Register (0xA8; RW)

 Bit(s)      Init.   Type                                                Description

   0          0b     RO      Correctable Error Reporting Enable
                             Zero for VFs.
   1          0b     RO      Non-Fatal Error Reporting Enable
                             Zero for VFs.
   2          0b     RO      Fatal Error Reporting Enable
                             Zero for VFs.
   3          0b     RO      Unsupported Request Reporting Enable
                             Zero for VFs.
   4          0b     RO      Enable Relaxed Ordering
                             Zero for VFs.
  7:5        000b    RO      Max Payload Size
                             Zero for VFs.
  9:8        00b     RO      Reserved.
   10         0b     RO      Auxiliary Power PM Enable
                             Zero for VFs.
   11         0b     RO      Enable No Snoop
                             Zero for VFs.

333369-009                                                                                                                      857
                                     Did this document help answer your questions?

                                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                                 PCIe Programming Interface

 Bit(s)   Init.   Type                                                 Description

 14:12    000b    RO     Max Read Request Size
                         Zero for VFs.
  15       0b     RW     Initiate Function Level Reset
                         Specific to each VF.

9.3.2.2.2              VF Device Status Register (0xAA; RW1C)

 Bit(s)   Init.   Type                                                  Description

      0    0b     RW1C    Correctable Detected
                          Indicates status of correctable error detection. Zero for VF.
      1    0b     RW1C    Non-Fatal Error Detected
                          Indicates status of non-fatal error detection. Zero for VF.
      2    0b     RW1C    Fatal Error Detected
                          Indicates status of fatal error detection. Zero for VF.
      3    0b     RW1C    Unsupported Request Detected
                          Indicates that the X550 received an unsupported request. This field is identical in all functions. The
                          X550 cannot distinguish which function caused an error. Zero for VF.
      4    0b      RO     Aux Power Detected
                          Zero for VFs.
      5    0b      RO     Transaction Pending
                          Specific per VF. When set, indicates that a particular function (PF or VF) has issued non-posted
                          requests that have not been completed. A function reports this bit cleared only when all completions
                          for any outstanding non-posted requests have been received.
  15:6    0x0      RO     Reserved.

### 9.3.3 PCIe Extended Capabilities

#### 9.3.3.1 AER Registers

The following registers in the AER capability have a different behavior in a VF function.
Unlike the PF AER registers, these registers are not sticky since the VF is reset on FLR and on in-band
reset.

858                                                                                                                  333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PCIe Programming Interface

9.3.3.1.1               Uncorrectable Error Status Register (0x104; RW1C)

 Bit(s)      Init.   Type                                             Description

  3:0        0x0      RO    Reserved.
   4          0b      RO    Data Link Protocol Error Status
   5          0b      RO    Surprise Down Error Status (Optional)
  11:6       0x0      RO    Reserved.
   12         0b     RW1C   Poisoned TLP Status
   13         0b      RO    Flow Control Protocol Error Status
   14         0b     RW1C   Completion Timeout Status
   15         0b     RW1C   Completer Abort Status
   16         0b     RW1C   Unexpected Completion Status
   17         0b      RO    Receiver Overflow Status
   18         0b      RO    Malformed TLP Status
   19         0b      RO    ECRC Error Status
   20         0b     RW1C   Unsupported Request Error Status
                            When caused by a function that claims a TLP.
   21         0b      RO    ACS Violation Status
 31:22       0x0      RO    Reserved.

9.3.3.1.2               Correctable Error Status Register (0x110; RW1C)

The Correctable Error Status register reports error status of individual correctable error sources on a
PCIe device. When an individual error status bit is set to 1b it indicates that a particular error occurred;
software can clear an error status by writing a 1b to the respective bit.

 Bit(s)      Init.   Type                                             Description

   0          0b     RW1C   Receiver Error Status
  5:1        0x0      RO    Reserved.
   6          0b     RW1C   Bad TLP Status
   7          0b     RW1C   Bad DLLP Status
   8          0b     RW1C   REPLAY_NUM Rollover Status
  11:9       000b     RO    Reserved.
   12         0b     RW1C   Replay Timer Timeout Status
   13         0b     RW1C   Advisory Non-Fatal Error Status
 31:14       0x0      RO    Reserved.

333369-009                                                                                               859
                                   Did this document help answer your questions?

                                                             Intel® Ethernet Controller X550 Datasheet
                                                                          PCIe Programming Interface

NOTE:   This page intentionally left blank.

860                                                                                        333369-009
                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
PHY Registers

Chapter 10 PHY Registers
