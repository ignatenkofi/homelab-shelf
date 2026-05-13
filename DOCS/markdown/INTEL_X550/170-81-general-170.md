## 8.1 General

The X550's address space is mapped into four regions with PCI Base Address Registers listed in
Table 8-1 and explained more in Section 9.2.2.16 and Section 9.2.2.17.

Table 8-1.          X550 Address Regions
                       Addressable Content                                    Mapping Style                   Region Size

 Internal registers memories and NVM (Memory BAR)                     Direct memory mapped             128 KB + NVM Size1

 FLASH (optional)2                                                    Direct memory mapped             2 MB - 4 MB

 Expansion ROM (optional)                                             Direct memory mapped             64 KB - 512 KB

    3 I/O window mapped                32 bytes

 Internal registers and memories (optional)

 MSI-X (optional)                                                     Direct memory mapped             16 KB4

1. The Flash size is defined by the BARCTRL register.
2. The Flash space in the Memory CSR and Expansion ROM Base Address are mapped to different Flash memory regions. Accesses to
   the Memory BAR at offset 256 KB are mapped to the Flash device at offset 0x0, while accesses to the Expansion ROM at offset 0x0
   are mapped to the Flash region pointed by the PXE Driver Module Pointer (read from NVM word address 0x05). See Section 6.1.
   The Expansion ROM region has a size limited to 512 KB.
3. The internal registers and memories can be accessed though I/O space as explained in the sections that follow.
4. See Section 9.2.2.16 for the MSI-X BAR offset in 32-bit and 64-bit BAR options.

### 8.1.1 Memory-Mapped Access

#### 8.1.1.1 Memory-Mapped Access to Internal Registers and

                         Memories
The internal registers and memories can be accessed as direct memory-mapped offsets from the
Memory CSR BAR. See the following sections for detailed description of the Device registers.
In IOV mode, this area is partially duplicated per VF. All replications contain only the subset of the
register set that is available for VF programming.

#### 8.1.1.2 Memory-Mapped Accesses to Flash

The external Flash can be accessed using direct memory-mapped offsets from the CSR base address
register (BAR0/BAR1).

#### 8.1.1.3 Memory-Mapped Access to MSI-X Tables

The MSI-X tables can be accessed as direct memory-mapped offsets from the base address register
(BAR3). The MSI-X registers are described in Section 8.2.4.1, “PF - MSI-X Table Registers”.
In IOV mode, this area is duplicated per VF.

333369-009                                                                                                                    583
                                      Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                   Programming Interface

#### 8.1.1.4 Memory-Mapped Access to Expansion ROM

The option ROM module located in the external Flash can also be accessed as a memory-mapped
expansion ROM. Accesses to offsets starting from the Expansion ROM Base address reference the Flash,
provided that access is enabled through the NVM Initialization Control Word, and if the Expansion ROM
Base Address register contains a valid (non-zero) base memory address.

### 8.1.2 I/O-Mapped Access

All internal registers and memories can be accessed using I/O operations. I/O accesses are supported
only if an I/O Base Address is allocated and mapped (BAR2), the BAR contains a valid (non-zero value),
and I/O address decoding is enabled in the PCIe configuration.
When an I/O BAR is mapped, the I/O address range allocated opens a 32-byte window in the system I/
O address map. Within this window, two I/O addressable registers are implemented: IOADDR and
IODATA. The IOADDR register is used to specify a reference to an internal register or memory, and then
the IODATA register is used to access it at the address specified by IOADDR:

Table 8-2.      I/O Map
      Offset    Abbreviation                                      Name                                        RW      Size

0x00           IOADDR          Internal Register, Internal Memory, or Flash Location Address.                 RW     4 bytes
                                0x00000-0x1FFFF – Internal registers/memories
                                0x20000-0x7FFFF – Undefined

0x04           IODATA          Data field for reads or writes to the internal register, internal memory, or   RW     4 bytes
                               Flash location as identified by the current value in IOADDR. All 32 bits of
                               this register are read/write-able.

0x08-0x1F      Reserved        Reserved.                                                                      O      4 bytes

#### 8.1.2.1 IOADDR (I/O Offset 0x00; RW)

The IOADDR register must always be written as a DWord access. Writes that are less than 32 bits are
ignored. Reads of any size returns a DWord of data. However, the chipset or CPU might only return a
subset of that DWord.
For software programmers, the IN and OUT instructions must be used to cause I/O cycles to be used on
the PCIe bus. Because writes must be to a 32-bit quantity, the source register of the OUT instruction
must be EAX (the only 32-bit register supported by the OUT command). For reads, the IN instruction
can have any size target register, but it is recommended that the 32-bit EAX register be used.
Bits 31 through 20 are ignored by the device and should be set to zero by the software. At hardware
reset (LAN_PWR_GOOD) or PCI reset, this register value resets to 0x00000000. Once written, the value
is retained until the next write or reset.

#### 8.1.2.2 IODATA (I/O Offset 0x04; RW)

The IODATA register must always be written as a DWord access when the IOADDR register contains a
value for the internal register and memories (such as 0x00000-0x1FFFC). In this case, writes that are
less than 32 bits are ignored.
Writes and reads to IODATA when the IOADDR register value is in an undefined range (0x20000-
0x7FFFC) should not be performed. Results cannot be determined.

584                                                                                                                333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

Note:        There are no special software timing requirements on accesses to IOADDR or IODATA. All
             accesses are immediate except when data is not readily available or acceptable. In this case,
             the X550 delays the results through normal bus methods (like split transaction or transaction
             retry).
             Because a register/memory read or write takes two I/O cycles to complete, software must
             provide a guarantee that the two I/O cycles occur as an atomic operation. Otherwise, results
             can be non-deterministic from the software viewpoint.

#### 8.1.2.3 Undefined I/O Offsets

I/O offsets 0x08 through 0x1F are considered to be reserved offsets with the I/O window. DWord reads
from these addresses return 0xFFFF, while writes to these addresses are discarded.

### 8.1.3 Configuration Access to Internal Registers and

                    Memories
To support legacy pre-boot 16-bit operating environments without requiring I/O address space, the
X550 enables accessing CSRs via the configuration address space by mapping IOADDR and IODATA
registers into the configuration address space. The register mapping in this case is listed in Table 8-3.

Table 8-3.        IOADDR and IODATA in Configuration Address Space
  Configuration
                    Abbreviation                                   Name                                    RW    Size
    Address

0x98               IOADDR           Internal register or internal memory location address.                 RW   4 bytes
                                     0x00000-0x1FFFF – Internal registers and memories.
                                     0x20000-0x7FFFFF – Undefined.

0x9C               IODATA           Data field for reads or writes to the internal register or internal    RW   4 bytes
                                    memory location as identified by the current value in IOADDR. All 32
                                    bits of this register can be read from or written to.

Software writes data to an internal CSR via the configuration space in the following manner:
1. CSR address is written to the IOADDR register where:
       • Bit 31 (IOADDR.Configuration IO Access Enable) of the IOADDR register should be set to 1b.
       • Bits 30:0 of IOADDR should hold the actual address of the internal register or memory being
         written to.
2. Data to be written is written into the IODATA register.
       • The IODATA register is used as a window to the register or memory address specified by
         IOADDR register. As a result, the data written to the IODATA register is written into the CSR
         pointed to by bits 30:0 of the IOADDR register.
3. IOADDR.Configuration IO Access Enable is cleared to avoid unintentional CSR read operations (that
   might cause clear by read) by other applications scanning the configuration space.

333369-009                                                                                                           585
                                   Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                      Programming Interface

Software reads data from an internal CSR via the configuration space in the following manner:
1. CSR address is written to the IOADDR register where:
      — Bit 31 (IOADDR.Configuration IO Access Enable) of the IOADDR register should be set to 1b.
      • Bits 30:0 of IOADDR should hold the actual address of the internal register or memory being
        read.
2. CSR value is read from the IODATA register.
      • The IODATA register is used as a window to the register or memory address specified by the
        IOADDR register. As a result, the data read from the IODATA register is the data of the CSR
        pointed to by bits 30:0 of the IOADDR register.
3. IOADDR.Configuration IO Access Enable is cleared to avoid un-intentional CSR read operations
   (that might cause clear by read) by other applications scanning the configuration space.
Notes:
 • When functioning in a D3 state, software should not attempt to access CSRs via the IOADDR and
   IODATA configuration registers.
 • To enable CSR access via configuration space, software should set bit 31 to 1b
   (IOADDR.Configuration IO Access Enable) in the IOADDR register. Software should clear bit 31 of
   the IOADDR register after completing CSR access to avoid an unintentional clear-by-read operation
   by another application scanning the configuration address space.
 • Bit 31 of the IOADDR register (IOADDR.Configuration IO Access Enable) has no effect when
   initiating access via I/O address space.
 • Configuration access to 0x9C (IODATA) without setting bit 31 of the IOADDR register
   (IOADDR.Configuration Access Enable) must not result in an unsupported request.
 • I/O-mapped access and CSR access via PCIe configuration space are mutually exclusive operating
   modes, and therefore PCIE_CNF.IO_SUP NVM bit must be cleared when the
   PCIE_CAPSUP.CSR_CONF_EN NVM bit is set, and vice versa.

586                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface

### 8.1.4 Register Terminology

      Type                                                             Description

RC               Read Clear
                 A register bit with this attribute is cleared after read. Writes have no effect on the bit value.

RO               Read Only
                 If a register is read only, writes to this register have no effect.

ROS              Read Only Status
                 Writes to ROS fields has no effect. The value of the field can change due to hardware events.

RSV              Reserved
                 Field can return any value on read access and must be set to its initialized value on write access unless specified
                 differently in the field description.

RW               Read/Write
                 A register with this attribute can be read and written. If written since reset, the value read reflects the value
                 written.

RW1C             Read/Write Clear
                 A register with this attribute can be read and written. However, a write of a 1b clears (sets to 0b) the
                 corresponding bit and a write of a 0b has no effect.

RW/RC            Read/Write and Read Clear

RWS              Read Write Set
                 Register that is set to 1b by software by writing a 1b to the register, and cleared to 0b by hardware.

WO               Write Only
                 Reading this register might not return a meaningful value.

### 8.1.5 VF Registers Allocated per Queue

Depending on configuration, each pool has 2, 4, or 8 queues allocated to it. Note that in IOV mode, any
queues not allocated to a VF are allocated to the PF. The registers assigned to a queue are accessible
both in its VF address space and in the PF address space. This section describes the address mapping of
registers that belong to queues.
Section 7.8.2.7.2 defines the correspondence of queue indices between the PF and the VFs. For
example, when in configuration for 32 VFs, queues 124-127 in the PF correspond to queues [3:0] of
VF# 31.
Note:        The queue pair of one VF should be assigned to the PF, therefore the maximum usable
             number of VFs is 63.
The queues are enumerated in each VF from 0 (i.e. [1:0], [3:0], or [7:0]). If a queue is allocated to a
VF, its corresponding registers are accessible in the VF CSR space. Each register is allocated an address
in the VF (relative to its base) according to its index in the VF space. Therefore, the registers of queue
0 in each VF are allocated the same addresses, which equal the addresses of the same registers for
queue 0 in the PF. For example, RDH[0] in the VF space has the same relative address in each VF and in
the PF (address 0x01010).

333369-009                                                                                                                           587
                                       Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                      Programming Interface

### 8.1.6 Non-Queue VF Registers

Registers that do not correspond to a specific queue are allocated addresses in the VF space according
to these rules:
 • Registers that are read-only by the VF (e.g. STATUS) have the same address in the VF space as in
   the PF space.
 • Registers allocated per pool are accessed in the VF in the same location as pool [0] in the PF
   address space.
 • Registers that are RW by the VF (e.g. CTRL) are replicated in the PF, one per VF, in adjacent
   addresses.
Note:    Since the VF address space is limited to 16 KB, any register that resides above that address in
         the PF space cannot reside in the same address in the VF space and is therefore allocated in
         another location in the VF.

588                                                                                               333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Programming Interface
