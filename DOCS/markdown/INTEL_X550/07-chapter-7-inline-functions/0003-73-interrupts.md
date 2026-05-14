## 7.3 Interrupts

The X550 supports the following interrupt modes. Mapping of interrupts causes is different in each of
these modes as described in this section.
 • PCI legacy interrupts or MSI or MSI-X and only a single vector is allocated — Selected when
   GPIE.MULTIPLE_MSIX is set to 0b.
 • MSI-X with multiple MSI-X vectors in non-IOV mode — Selected when GPIE.MULTIPLE_MSIX is set
   to 1b and GPIE.VT_MODE is set to 00b.
 • MSI-X in IOV mode — Selected when GPIE.MULTIPLE_MSIX is set (as previously stated) and
   GPIE.VT_MODE DOES NOT equal 00b.
The following sections describe the interrupt registers and device functionality at all operation modes.

### 7.3.1 Interrupt Registers

#### 7.3.1.1 Physical Function (PF) Registers

The PF interrupt logic consists of the registers listed in the Table 7-46 followed by their description:

Table 7-46. PF Interrupt Registers
    Acronym                                                      Complete Name

      EICR       Extended Interrupt Cause register

      EICS       Extended Interrupt Cause Set register (enables software to initiate interrupts)

      EIMS       Extended Interrupt Mask Set/Read register

      EIMC       Extended Interrupt Mask Clear register

      EIAC       Extended Interrupt Auto Clear register (following interrupt assertion)

      EIAM       Extended Interrupt Auto Mask register (auto set/clear of the EIMS)

      EITR       Extended Interrupt Throttling register (throttling)

      IVAR       Interrupt Vector Allocation Registers (described in Section 7.3.4)

   IVAR_MISC     Miscellaneous Interrupt Vector Allocation Register (described in Section 7.3.4)

These registers are extended to 64 bits by an additional set of two registers. EICR has an additional two
registers EICR(1)... EICR(2) and so on for the EICS, EIMS, EIMC, EIAM and EITR registers. The EIAC
register is not extended to 64 bits as this extended interrupt causes are always auto cleared. Any
reference to EICR... EIAM registers as well as any global interrupt settings in the GPIE register relates
to their extended size of 64 bits.
The legacy EICR[15:0] mirror the content of EICR(1)[15:0]. In the same manner the lower 16 bits of
EICS, EIMS, EIMC, EIAM mirror the lower 16 bits of EICS(1), EIMS(1), EIMC(1), EIAM(1). For more
details on the use of these registers in the various interrupt modes (legacy, MSI, MSI-X) see
Section 7.3.4.

333369-009                                                                                                 455
                                    Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

#### 7.3.1.2 Virtual Function (VF) Registers

The VF interrupt logic has the same set of interrupt registers while each of them has three entries for
three interrupt causes. The names and functionality of these registers are the same as those of the PF
with a prefix of VT as follows: VFEICR, VFEICS, VFEIMS, VFEIMC, VFEIAM, VFEITR. The interrupt causes
are always auto cleared. Although each VF can generate up to three interrupts, only the first two
registers are capable of interrupt throttling and are associated to VFEITR registers (see
Section 7.3.4.3.2 for its proper usage). Each VF also has the mapping registers VFIVAR and
VFIVAR_MISC. Note that any global interrupt setting by the GPIE register affect both interrupt settings
of the PF as well as the VFs.

#### 7.3.1.3 Extended Interrupt Cause (EICR) Registers

This register records the interrupt causes to provide software information on the interrupt source. Each
time an interrupt cause happens, the corresponding interrupt bit is set in the EICR registers. An
interrupt is generated each time one of the bits in these registers is set, and the corresponding
interrupt is enabled via the EIMS registers. The possible interrupt causes are as follows:
 • Each RTxQ bit represents the following events: Tx or Rx descriptor write back; Rx queue full and Rx
   descriptor queue minimum threshold.
 • Interrupts can be throttled by ITR as configured in the EITR register.
 • Mapping the Tx and Rx queues to EICR is done by the IVAR registers as described in Section 7.3.4.
   Each bit might represent an event on a single Tx or Rx queue or could represent multiple queues
   according to the IVAR setting. In the later case, software might not be able to distinguish between
   the interrupt causes other than checking all associated Tx and Rx queues.
 • The MULTIPLE_MSIX = 1b setting is useful when multiple MSI-X vectors are assigned to the device.
   When the GPIE.MULTIPLE_MSIX bit is set, the RTxQ bits are associated with dedicated MSI-X
   vectors. Bit 0 is Tx/Rx interrupt associated with MSI-X vector 0 and bit 15 is Tx/Rx interrupt
   associated with MSI-X vector 15.
Writing a 1b to any bit in the register clears it. Writing a 0b to any bit has no effect. The EICR is also
cleared on read if GPIE.OCD bit is cleared. When the GPIE.OCD bit is set, only bits 16...29 are cleared
on read. The later setting is useful for MSI-X mode in which the Tx and Rx and possibly the timer
interrupts do not share the same interrupt with the other causes. Bits in the register can be auto
cleared depending on the EIAC register setting (see Section 7.3.1.6).

#### 7.3.1.4 Extended Interrupt Cause Set (EICS) Register

This register enables software to initiate a hardware interrupt. Setting any bit on the EICS sets its
corresponding bit in the EICR register while bits written to 0b have no impact. It then causes an
interrupt assertion if enabled by the EIMS register. Setting any bit generates throttled interrupt
depending on the GPIE.EIMEN setting: When the EIMEN bit is set, setting the EICS register causes an
LLI interrupt; When the EIMEN bit is cleared, setting the EICS register causes an interrupt after the
corresponding interrupt throttling timer expires.
Note:     The EIMEN bit can be set high only when working in auto-mask mode (EIAM bit of the
          associated interrupt is set).

456                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.3.1.4.1               EICS Affect on RSC Functionality

Setting EICS bits causes interrupt assertion (if enabled). EICS settings have the same impact on RSC
functionality as nominal operation:
 • In ITR mode (GPIE.EIMEN = 0b), setting the EICS bits impact the RSC completion and interrupt
   assertion the same as any Rx packet. The functionality depends on the EICS setting schedule
   relative to the ITR intervals as described in Section 7.3.2.1.1.
 • In LLI mode (GPIE.EIMEN = 1b), setting the EICS bits impact the RSC completion and interrupt
   assertion as follows:
     — Interrupt is asserted.
     — Concurrently, hardware triggers RSC completion in all Rx queues associated with the same
       interrupt.
     — Most likely these RSC(s) are completed to host memory after the interrupt is already asserted.
       In his case, it is guaranteed that an additional interrupt is asserted when the ITR expires.

#### 7.3.1.5 Extended Interrupt Mask Set and Read (EIMS) Register,

                       and Extended Interrupt Mask Clear (EIMC) Register
The Extended Interrupt Mask Set and Read (EIMS) register enables the interrupts in the EICR. When
set to 1b, each bit in the EIMS register, enables its corresponding bit in the EICR. Software might
enable each interrupt by setting bits in the EIMS register to 1b. Reading EIMS returns its value.
Software might clear any bit in the EIMS register by setting its corresponding bit in the Extended
Interrupt Mask Clear (EIMC) register. Reading the EIMC register does not return any meaningful data.
This independent mechanism of setting and clearing bits in the EIMS register saves the need for read
modify write and also enables simple programming in multi-thread, multi-CPU core systems.
Note:        The EICR register stores the interrupt events regardless of the state of the EIMS register.

#### 7.3.1.6 Extended Interrupt Auto Clear Enable (EIAC) Register

Each bit in this register enables auto clearing of its corresponding bit in EICR following interrupt
assertion. It is useful for Tx and Rx interrupt causes that have dedicated MSI-X vectors. When the Tx
and Rx interrupt causes share an interrupt with the other or a timer interrupt, the relevant EIAC bits
should not be set. Bits in the EICR register that are not enabled by auto clear, must be cleared by either
writing a 1b to clear or a read to clear.
Note that there are no EIAC(1)...EIAC(2) registers. The hardware setting for interrupts 16...63 is
always auto clear.
Note:        Bits 29:16 should never be set to auto clear since they share the same MSI-X vector.
             Writing to the EIAC register changes the setting of the entire register. In IOV mode, some of
             the bits in this register might affect VF functionality (VF-56...VF-63). It is recommended that
             software set the register in PF before VF’s are enabled. Otherwise, a software semaphore
             might be required between the VF and the PF to avoid setting corruption.

333369-009                                                                                                 457
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

#### 7.3.1.7 Extended Interrupt Auto Mask Enable (EIAM) Register

Each bit in this register enables auto clearing and auto setting of its corresponding bit in the EIMS
register as follows:
 • Following a write of 1b to any bit in the EICS register (interrupt cause set), its corresponding bit in
   the EIMS register is auto set as well enabling its interrupt.
 • A write to clear the EICR register clears its corresponding bits in the EIMS register masking further
   interrupts.
 • A read to clear the EICR register, clears the EIMS bits (enabled by the EIAM) masking further
   interrupts. Note that if the GPIE.OCD bit is set, Tx and Rx interrupt causes are not cleared on read
   (bits 0:15 in the EICR). In this case, bits 0:15 in the EIMS are not cleared as well.
 • In MSI-X mode the auto clear functionality can be driven by MSI-X vector assertion if GPIE.EIAME is
   set.
Note:     Bits 29:16 should never be set to auto clear since they share the same MSI-X vector.
          Writing to the EIAM register changes the setting of the entire register. In IOV mode, some of
          the bits in this register might affect VF functionality. It is recommended that software set the
          register in PF before VF’s are enabled. Otherwise, a software semaphore might be required
          between the VF and the PF to avoid setting corruption.
          If any of the Auto Mask Enable bits is set in the EIAM registers, the GPIE.EIAME bit must be
          set as well.

### 7.3.2 Interrupt Moderation

Interrupt rates can be tuned by the EITR register for reduced CPU utilization while minimizing CPU
latency. In MSI or legacy interrupt modes, only EITR register 0 can be used. In MSI-X, non-IOV mode,
the X550 includes 64 EITR registers 0...63 that are mapped to MSI-X vectors 0...63, respectively. In
IOV mode, there are an additional 65 EITR registers that are mapped to the MSI-X vectors of the virtual
functions. The mapping of MSI-X vectors to EITR registers are described in Section 7.3.1.3.

#### 7.3.2.1 Time-Based Interrupt Throttling — ITR

Time-based interrupt throttling is useful to limit the maximum interrupt rate regardless of network
traffic conditions. The ITR logic is targeted for Rx/Tx interrupts only. It is assumed that the software
device driver does not moderate the timer, other and mail box (IOV mode) interrupts. In non-IOV
mode, all 64 interrupts can be associated with ITR logic. In IOV mode, the ITR logic is shared between
the PF and VFs as shown in Figure 7-23. The ITR mechanism is based on the following parameters:
 • ITR Interval field in the EITR registers — The minimum inter-interrupt interval is specified in
   2.048 s units (at 1 Gb/s or 10 Gb/s link). When the ITR Interval equals zero, interrupt throttling is
   disabled and any event causes an immediate interrupt. The field is composed of nine bits enabling a
   range of 2.048 s up to 1046.528 s. These ITR interval times correspond to interrupt rates in the
   range of 488 K INT/sec to 955 INT/sec. When operating at 100 Mb/s link, the ITR interval is
   specified in 20.48 s units.
      — Due to internal synchronization issues, the ITR interval can be shortened by up to 1 s at

# 10 Gb/s or 1 Gb/s link and up to 10 s at 100 Mb/s link when it is triggered by packet write

        back or interrupt enablement.

458                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

 • ITR Counter partially exposed in the EITR registers — Down counter that is loaded by the ITR
   interval each time the associated interrupt is asserted.
     — The counter is decremented by one each 1.024 s (at 1 Gb/s or 10 Gb/s link) and stops
       decrementing at zero. At 100 Mb/s link, the speed of the counter is decremented by one each
       10.24 s.
     — If an event happens before the counter is zero, it sets the EICR. The interrupt can be asserted
       only when the ITR time expires (counter is zero).
     — Else (no events during the entire ITR interval), the EICR register is not set and the interrupt is
       not asserted on ITR expiration. The next event sets the EICR bit and generates an immediate
       interrupt. See Section 7.3.2.1.1 for interrupt assertion when RSC is enabled.
     — Once the interrupt is asserted, the ITR counter is loaded by the ITR interval and the entire cycle
       re-starts. The next interrupt can be generated only after the ITR counter expires once again.

7.3.2.1.1              ITR Affect on RSC Functionality

Interrupt assertion is one of the causes for RSC completion (see Section 7.10.6). When RSC is enabled
on specific Rx queues, the associated ITR interval with these queues must be enabled and must be
larger (in time units) than RSC delay. The ITR is divided to the two time intervals that are defined by
the ITR interval and RSC delay. RSC completion is triggered after the first interval completes and the
interrupt is asserted when the second interval completes.
The RSC Delay field is defined in the GPIE registers. RSC Delay can have one of the following eight
values: 4 s, 8 s, 12 s... 32 s.
 • The first ITR interval equals ITR interval minus RSC delay. The internal ITR counter starts at ITR
   interval value and counts down until it reaches the RSC delay value. Therefore, the ITR interval
   must be set to a larger value than the RSC delay.
 • The second ITR interval equals RSC delay. The internal ITR counter continues to count down until it
   reaches zero.
 • RSC completion can take some time (usually in the range of a few micro seconds). This time is
   composed by completing triggering latency and completing process latency. These delays should be
   considered when tuning the RSC delay. The clock frequency of the RSC completion logic depends on
   the link speed. As a result, the completion delay can as high as ~0.8 s at 10 Gb/s link and
   ~8 s at 1 Gb/s link. The RSC completion logic might take additional ~50 ns at 10 Gb/s link and
   ~0.5 s at 1 Gb/s link per RSC. In addition, there is the PCIe bus arbitration latency as well as
   system propagation latencies from the device up to host memory.
 • Recommended RSC delay numbers are: 8 s at 10 Gb/s link and 28 s at 1 Gb/s link.
 • RSC is not recommended when operating at 100 Mb/s link.
Following are cases of packet reception with respect to the ITR intervals:
 • Packets are received and posted (including their status) to the Rx queue in the first ITR interval. In
   this case, RSC completion is triggered at the end of the first ITR interval and the interrupt is
   asserted at the second interval expiration.
 • A packet (and its status) is received and posted to the Rx queue only after the first ITR interval has
   expired (either on the second interval or after the entire ITR interval has expired). In this case, RSC
   completion is triggered almost instantly (other than internal logic latencies). The interrupt is
   asserted at RSC delay time after the non-coalesced Rx status is queued to be posted to the host.
 • Due to internal synchronization issues, the RSC delay can be shorten by up to 1 s when it is
   triggered by packet write back.

333369-009                                                                                              459
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

#### 7.3.2.2 Immediate Interrupt

The X550 might initiate an immediate interrupt when the receive descriptor ring is almost empty (Rx
descriptors below a specific threshold). The threshold is defined by SRRCTL[n].RDMTS per Rx queue.
This mechanism can protect against memory resources being used up during reception of a long burst
of short packets.

### 7.3.3 TCP Timer Interrupt

#### 7.3.3.1 Introduction

To implement TCP timers, software needs to take action periodically (every 10 ms). Today, the driver
must rely on software-based timers, whose granularity can change from platform to platform. This
software timer generates a software NIC interrupt, which then enables the driver to perform timer
functions, avoiding cache thrash and enabling parallelism. The timer interval is system-specific.
It would be more accurate and more efficient for this periodic timer to be implemented in hardware.
The driver would program a timeout value (usual value of 10 ms), and each time the timer expires,
hardware sets a specific bit in the EICR register. When an interrupt occurs (due to normal interrupt
moderation schemes), software reads the EICR register and discovers that it needs to process timer
events.
The timeout should be programmable by the driver, and the driver should be able to disable the timer
interrupt if it is not needed.

#### 7.3.3.2 Description

A stand-alone, down-counter is implemented. An interrupt is issued each time the value of the counter
is zero.
Software is responsible for setting an initial value for the timer in the Duration field. Kick-starting is
done by writing a 1b to the KickStart bit.
Following kick starting, an internal counter is set to the value defined by the Duration field. Then the
counter is decreased by one each ms. When the counter reaches zero, an interrupt is issued. The
counter re-starts counting from its initial value if the Loop field is set.

### 7.3.4 Mapping of Interrupt Causes

The following sections describe legacy, MSI and MSI-X interrupt modes.

#### 7.3.4.1 Legacy and MSI Interrupt Modes

In legacy and MSI modes, an interrupt cause is reflected by setting one of the bits in the EICR register,
where each bit reflects one or more causes. All interrupt causes are mapped to a single interrupt signal:
either legacy INTA/B or MSI. This section describes the mapping of interrupt causes (that is a specific
Rx or Tx queue event or any other event) to bits in the EICR.
The TCP timer and all other interrupt causes are mapped directly to EICR[30:16]. Note that the
IVAR_MISC register is not used in legacy and MSI modes.

460                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Mapping the Tx and Rx queues to interrupt bits in the EICR register is programmed in the IVAR
registers as shown in Figure 7-23. Each entry in the IVAR registers is composed of two fields that
identify the associated bit in the EICR[15:0] register. Software might map multiple Tx and Rx queues to
the same EICR bit.
 • INT_Alloc — Defines one of the bits (0...15) in the EICR register that reflects the interrupt status
   indication.
 • INT_Alloc_val — Valid bit for the this interrupt cause.

                                 Cause 0                           0

                                                                          (reflect causes)
                                     .                                                                 EITR 0

                                                Registers
             Queue

                                                                                EICR
                                                 IVAR
             Related                 .
             causes                  .
                                Cause 255                          15                                  INT(A/B)
                                                                                                         / MSI
           Timer                                                   16     Other
          and all                    .                                  Interrupt
           Other
         Interrupt
                                     .                                   causes

          causes                     .                                  TCP timer
                                                                   30

Figure 7-23. Cause Mapping in Legacy and MSI Modes

Mapping between the Tx and Rx queue to the IVAR registers is hard-wired as shown in the Figure 7-24.

                       IVAR 0        IVAR 1          IVAR 2                   IVAR 62        IVAR 63

                        Rx 0             Rx 2          Rx 4                     Rx 124       Rx 126

                                                               ...
                        Tx 0             Tx 2          Tx 4                     Tx 124       Tx 126
                        Rx 1             Rx 3          Rx 5                     Rx 125       Rx 127
                        Tx 1             Tx 3          Tx 5                     Tx 125       Tx 127

Figure 7-24. Rx and Tx Queue Mapping to IVAR Registers

#### 7.3.4.2 MSI-X Mode in Non-IOV Mode

 • MSI-X defines a separate optional extension to basic MSI functionality. Hardware indicates the
   number of requested MSI-X vectors in the table size in the MSI-X capability structure in the
   configuration space. The number of requested MSI-X vectors is loaded from NVM in the
   PCI_CNF2.MSI_X_PF_N field up to maximum of 64 MSI-X vectors. The operating system might
   allocate any number of MSI-X vectors to the device from a minimum of one up to the requested
   number of MSI-X vectors.
 • Enables interrupts causes allocation to the assigned MSI-X vectors. Interrupt allocation is
   programmed by the IVAR registers and are described in this section.
 • Each vector can use an independent address and data value as programmed directly by the
   operating system in the MSI-X vector table.
 • Each MSI-X vector is associated to an EITR register with the same index (MSI-X 0 to EITR[0],
   MSI-X 1 to EITR[1],...).
For more information on MSI-X, refer to the PCI Local Bus Specification, Revision 3.0.

333369-009                                                                                                        461
                                     Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

MSI-X vectors can be used for several purposes:
1. Dedicated MSI-X vectors per interrupt cause (avoids the need to read the interrupt cause register).
2. Load balancing by MSI-X vectors assignment to different CPUs.
3. Optimized interrupt moderation schemes per MSI-X vector using the EITR registers.
The MSI-X vectors are used for Tx and Rx interrupt causes as well as the other and timer interrupt
causes. The remainder of this section describes the mapping of interrupt causes (such as a specific Rx
or Tx queue event or any other event) to the interrupts registers and the MSI-X vectors.
The TCP timer and other events are reflected in EICR[30:16] the same as the legacy and MSI mode. It
is then mapped to the MSI-X vectors by the IVAR_MISC register as shown in Figure 7-25. The
IVAR_MISC register includes two entries for the timer interrupt and an additional entry for all the other
causes. The structure of each entry is as follows:
 • INT_Alloc — Defines the MSI-X vector (0...63) assigned to this interrupt cause.
 • INT_Alloc_val — Valid bit for the this interrupt cause.
The Tx and Rx queues are associated to the IVAR0...IVAR63 the same as legacy and MSI mode shown
in Figure 7-24. The Tx and Rx queues are mapped by the IVAR registers to EICR(1),...EICR(2) registers
and MSI-X vectors 0...63 illustrated in Figure 7-25. The IVAR entries have the same structure as the
IVAR_MISC register previously shown. Each bit in EICR(1...2) registers is associated to MSI-X vector
0...63 as follows:
 • EICR(i).bit_num is associated to MSI-X vector (i x 32 + bit_num).
 • The legacy EICR[15:0] mirror the content of EICR(1)[15:0]. In the same manner the lower 16 bits
   of EICS, EIMS, EIMC, EIAM mirror the lower 16 bits of EICS(1), EIMS(1), EIMC(1), EIAM(1). The
   use of these registers depends on the number of assigned MSI-X interrupts as follows:
 • 16 Tx and Rx Interrupts — When using up to 16 Tx and Rx interrupts, software might access the
   Tx and Rx interrupt bits in the legacy EICR, EICS,... registers.
 • More than 16 Tx and Rx Interrupts — When using more than 16 Tx and Rx interrupts, software
   must use EICS(1)...EICS(2), EIMS(1)...EIMS(2),... In the later case, software should avoid
   modifying the lower 16 bits in the EICS, EIMS... registers when it accesses the higher bits of these
   registers as follows:
      — EICR, EICS, EIMS and EIMC — When software programs the higher 16 bits of these registers, it
        should set their lower 16 bits to zero’s keeping the EICR(1), EICS(1), EIMS(1) and EIMC(1)
        unaffected.
      — EIAM — When software programs the higher 16 bits, it should keep the lower 16 bits at their
        previous setting so the EIAM(1) is unaffected.
      — EIAC — When software programs the higher 16 bits, it should set the lower 16 bits to one’s.
 • Single MSI-X vector — If the operating system allocates only a single MSI-X vector, the driver
   might use the non-MSI-X mapping method (setting the GPIE.Multiple_MSIX to 0b). In this case, the
   INT_Alloc field in the IVAR registers might define one of the lower 16 bits in the EICR register while
   using MSI-X vector 0. The IVAR_MISC should be programmed to MSI-X vector 0.

462                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                                                                                               EITR 0...63

                              Cause 0

                                                                      EICR1 … EICR2
                                                                0

                                                                      (reflect causes)
         Queue
                                  .

                                                 Registers
         Related                                                                                MSI-X

                                                  IVAR
         causes:                  .                                                             Vectors
        Rx 0...127                .                                                              0...63
        Tx 0...127
                             Cause 255                         63

          Timer                             16       Other

                                                                                   IVAR_MISC
         and all                  .                Interrupt
          Other
        Interrupt
                                  .                 causes

         causes                   .              TCP timer
                                            30

                                                     EICR

Figure 7-25. Cause Mapping in MSI-X Mode (non-IOV)

#### 7.3.4.3 MSI-X Interrupts in IOV Mode

In IOV mode, interrupts must be implemented by MSI-X vectors. The X550 supports up to 64 virtual
functions VF(0...63). Each VF can generate up to three MSI-X vectors. The number of requested MSI-X
vectors per VF is loaded from NVM in the PCI_CNF2.MSI_X_VF_N field. It is reflected in the Table Size
field in the PCIe MSI-X capability structure of the VF’s. In addition, the PF requires its own interrupts.
The number of requested MSI-X vectors is loaded from NVM in the PCI_CNF2.MSI_X_PF_N field up to
maximum of 64 MSI-X vectors. It is reflected in the Table Size field in the PCIe MSI-X capability
structure.

7.3.4.3.1               MSI-X Vectors Used by Physical Function (PF)

PF is responsible for the timer and other interrupt causes that include the VM to PF mailbox cause
(explained in the virtualization sections). These events are reflected in EICR[30:16] and MSI-X vectors
are the same as the non-IOV mode (illustrated in Figure 7-23). When there are less than the maximum
possible active VF’s, some of the Tx and Rx queues can be associated with the PF. These queues can be
used for the sake of additional VM’s serviced by the hypervisor (the same as VMDq mode) or some
Kernel applications handled by the hypervisor. Tx and Rx mapping to the IVAR registers is shown in
Figure 7-24 and mapping to the EICR, EICR(1),...EICR(2) registers as well as the MSI-X vectors is
shown in Figure 7-25. See Section 7.3.4.3.3 for MSI-X vectors mapping of PF and VF’s to the EITR
registers.
Note:        Software should not assign MSI-X vectors in the PF to Tx and Rx queues that are assigned to
             other VF’s. In the case that VF’s become active after the PF used the relevant Tx and Rx
             queues, it is the responsibility of the PF driver to clear all pending interrupts of the associated
             MSI-X vectors.

7.3.4.3.2               MSI-X Vectors Used by Virtual Functions (VFs)

Each of the VFs in IOV mode is allocated separate IVAR(s) called VFIVAR registers, and a separate
IVAR_MISC called VFIVAR_MISC register. The VFIVAR_MISC maps the mailbox interrupt of the VF to its
VFEICR and the MSI-X vector. The VFIVAR registers map the Tx and Rx interrupts of the VF to its
VFEICR and the MSI-X vector. The mapping is similar to the mapping in the PF as shown in Figure 7-26
with the following comments:

333369-009                                                                                                   463
                                   Did this document help answer your questions?

                                                                                Intel® Ethernet Controller X550 Datasheet
                                                                                                           Inline Functions

 • Each VF cannot have more than three MSI-X vectors. It has only three active bits in the VFEICR
   register while VFEICR.bit_num is associated with MSI-X vector (bit_num).
 • The Tx and Rx interrupt can be mapped only to MSI-X 0 and MSI-X 1 (associated with VFEICR.0 and
   VFEICR.1).
 • The mailbox interrupt can be mapped to any of the three MSI-X vectors. However, when all three of
   them are allocated by the operating system, software should map the mailbox to MSI-X 2
   (associated with VFEICR.2). This rule should be kept since only VFEICR.0 and VFEICR.1 have ITR
   registers (VFEITR-0 and VFEITR-1).
 • Association between the Tx and Rx queues and the VFIVAR registers is shown in the Figure 7-26,
   Figure 7-27 and Figure 7-28 for IOV-64 (64 VF’s), IOV-32 and IOV-16. The colored boxes in the
   figures show the mapping between VF Rx and Tx queues to VFIVAR registers while the dashed
   boxes show the physical IVAR registers and the associated physical Rx and Tx queues.

                                Cause 0
          Queue                                                                                                         EITR 0
                                       .
                                                 Registers
                                                 VTIVAR
          Related                                                                                                       EITR 1
          causes:                      .
                                                                            0
          Rx 0...7                     .

                                                                                  (reflect causes)
                                                                                                                        MSI-X 0
          Tx 0...7

                                                                                      VTEICR
                                Cause 15
                                                                                                                        MSI-X 1
                                                 VTIVAR_MISC

                                                                                                                        MSI-X 2
                                                    Register

         Mail-Box                                                           2
         Interrupt

Figure 7-26. VF Interrupt Cause Mapping (MSI-X, IOV)

                       VF 0                                VF 1                                             VF 63
                     VTIVAR 0                         VTIVAR 0                                          VTIVAR 0
            VF Queues    HW Queeus           VF Queues         HW Queeus                  VF Queues            HW Queeus
                Rx 0          Rx 0              Rx 0              Rx 2                               Rx 0           Rx 126
                Tx 0
                Rx 1
                              Tx 0
                              Rx 1
                                                Tx 0
                                                Rx 1
                                                                  Tx 2
                                                                  Rx 3
                                                                           ...                       Tx 0
                                                                                                     Rx 1
                                                                                                                    Tx 126
                                                                                                                    Rx 127
                Tx 1          Tx 1              Tx 1              Tx 3                               Tx 1           Tx 127

Figure 7-27. VF Mapping of Rx and Tx Queue to VFIVAR in 64 VF’s Mode

                    VF 0                             VF 1                                         VF 31
                  VTIVAR 0                         VTIVAR 0                                     VTIVAR 0
            VF Queues HW Queeus              VF Queues HW Queeus                          VF Queues HW Queeus
                Rx 0          Rx 0              Rx 0              Rx 4                               Rx 0           Rx 124
                Tx 0
                Rx 1
                              Tx 0
                              Rx 1
                                                Tx 0
                                                Rx 1
                                                                  Tx 4
                                                                  Rx 5     ...                       Tx 0
                                                                                                     Rx 1
                                                                                                                    Tx 124
                                                                                                                    Rx 125
                Tx 1          Tx 1              Tx 1              Tx 5                               Tx 1           Tx 125

                  VTIVAR 1                         VTIVAR 1                                     VTIVAR 1
            VF Queues HW Queeus              VF Queues HW Queeus                          VF Queues HW Queeus
                Rx 2          Rx 2              Rx 2              Rx 6                               Rx 2           Rx 126
                Tx 2
                Rx 3
                              Tx 2
                              Rx 3
                                                Tx 2
                                                Rx 3
                                                                  Tx 6
                                                                  Rx 7     ...                       Tx 2
                                                                                                     Rx 3
                                                                                                                    Tx 126
                                                                                                                    Rx 127
                Tx 3          Tx 3              Tx 3              Tx 7                               Tx 3           Tx 127

Figure 7-28. VF Mapping of Rx and Tx Queue to VFIVAR in 32 VF’s Mode

464                                                                                                                               333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                       VF 0                         VF 1                            VF 15
                     VTIVAR 0                     VTIVAR 0                        VTIVAR 0
               VF Queues HW Queeus          VF Queues HW Queeus             VF Queues
                  Rx 0        Rx 0            Rx 0      Rx 8                     Rx 0   Rx 120
                  Tx 0
                  Rx 1
                              Tx 0
                              Rx 1
                                              Tx 0
                                              Rx 1
                                                        Tx 8
                                                        Rx 9      ...            Tx 0
                                                                                 Rx 1
                                                                                        Tx 120
                                                                                        Rx 121
                  Tx 1        Tx 1            Tx 1      Tx 9                     Tx 1   Tx 121

                     VTIVAR 1                     VTIVAR 1                        VTIVAR 1
               VF Queues HW Queeus          VF Queues HW Queeus             VF Queues
                  Rx 2        Rx 2            Rx 2      Rx 10                    Rx 2   Rx 122
                  Tx 2
                  Rx 3
                              Tx 2
                              Rx 3
                                              Tx 2
                                              Rx 3
                                                        Tx 10
                                                        Rx 11     ...            Tx 2
                                                                                 Rx 3
                                                                                        Tx 122
                                                                                        Rx 123
                  Tx 3        Tx 3            Tx 3      Tx 11                    Tx 3   Tx 123

                     VTIVAR 2                     VTIVAR 2                        VTIVAR 2
               VF Queues HW Queeus          VF Queues HW Queeus             VF Queues
                  Rx 4        Rx 4            Rx 4      Rx 12                    Rx 4   Rx 124
                  Tx 4
                  Rx 5
                              Tx 4
                              Rx 5
                                              Tx 4
                                              Rx 5
                                                        Tx 12
                                                        Rx 13     ...            Tx 4
                                                                                 Rx 5
                                                                                        Tx 124
                                                                                        Rx 125
                  Tx 5        Tx 5            Tx 5      Tx 13                    Tx 5   Tx 125

                     VTIVAR 3                     VTIVAR 3                        VTIVAR 3
               VF Queues HW Queeus          VF Queues HW Queeus             VF Queues
                  Rx 6        Rx 6            Rx 6      Rx 14                    Rx 6   Rx 126
                  Tx 6
                  Rx 7
                              Tx 6
                              Rx 7
                                              Tx 6
                                              Rx 7
                                                        Tx 14
                                                        Rx 15     ...            Tx 6
                                                                                 Rx 7
                                                                                        Tx 126
                                                                                        Rx 127
                  Tx 7        Tx 7            Tx 7      Tx 15                    Tx 7   Tx 127

Figure 7-29. VF Mapping of Rx and Tx Queue to VFIVAR in 16 VF’s Mode

7.3.4.3.3                MSI-X Vectors Mapping to EITR

EITR registers are aimed for Tx and Rx interrupt throttling. In IOV mode, the Tx and Rx queues might
belong to either the PF or to the VF’s. EITR(1...63) are multiplexed between the PF and the VF’s as
configured by the EITRSEL register. Figure 7-30 and Table 7-47 show the multiplexing logic and
required software settings. For any active VF (starting from VF32 and above), software should program
the matching bit in the EITRSEL to 1b. For any EITR that belongs to a VF, software should not map any
interrupt causes in the PF to an MSI-X vector that is associated with the same EITR register.
Any RSCINT[n] register is associated with an MSI-X vector ‘n’. As indicated above, the EITRSEL setting
affects the MSI-X mapping. It also maps their associated RSCINT registers to either the PF or the VFs.

333369-009                                                                                         465
                                 Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Inline Functions

                                                                             PF EITR          VF EITR
                                                                             Registers        Registers

                                         MSI-X 0                               EITR 0
                                         MSI-X 1
                                         MSI-X 2
                             PF                                                EITR 1        EITR 0
                                           …
                           Vectors                                                                        VF 63
                                           …
                                         MSI-X 62                              EITR 2        EITR 1
                                         MSI-X 63
                                         MSI-X 0                      Sel
                            VF 63        MSI-X 1                               EITRSEL
                                         MSI-X 2
                                            ...
                                                                               EITR 63       EITR 0
                                          MSI-X 0                                                         VF 32
                            VF 32         MSI-X 1                              EITR 64       EITR 1
                                          MSI-X 2
                                          MSI-X 0                              EITR 65       EITR 0
                            VF 31         MSI-X 1                              EITR 66       EITR 1       VF 31
                                          MSI-X 2
                                            ...
                                          MSI-X 0                              EITR 127      EITR 0
                             VF 0         MSI-X 1                              EITR 128      EITR 1       VF 0
                                          MSI-X 2

                      MSI-X 2 on each VF has no associated EITR register. It is useful
                      for the mailbox interrupts that do not require interrupt moderation.

Figure 7-30. PF/VF MSI-X Vectors Mapping to EITR

Table 7-47. PF/VF MSI-X Vectors Mapping Table to EITR Registers
       VM Active                 EITRSEL.N Setting                                       MSI-X Routing to EITR

     Non-IOV or
                           EITRSEL must be set to 0x0000                             MSI-X(1...63) -> EITR(1...63)
 VF(32...63) inactive

      VF(32) active         EITRSEL[0] must be set to 1b                             VF(32) MSI-X(0) -> EITR(63)

      VF(33) active         EITRSEL[1] must be set to 1b              VF(33) MSI-X(1) -> EITR(62) VF(33) MSI-X(0) -> EITR(61)

      VF(34) active         EITRSEL[2] must be set to 1b              VF(34) MSI-X(1) -> EITR(60) VF(34) MSI-X(0) -> EITR(59)

           ...                             ...                                                     ...

      VF(62) active         EITRSEL[30] must be set to 1b              VF(62) MSI-X(1) -> EITR(4) VF(62) MSI-X(0) -> EITR(3)

      VF(63) active         EITRSEL[31] must be set to 1b              VF(63) MSI-X(1) -> EITR(2) VF(63) MSI-X(0) -> EITR(1)

466                                                                                                                     333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.4                802.1q VLAN Support
The X550 provides several specific mechanisms to support 802.1q VLANs:
 • Optional adding (for transmits) and stripping (for receives) of IEEE 802.1q VLAN tags.
 • Optional ability to filter packets belonging to certain 802.1q VLANs.

7.4.1                802.1q VLAN Packet Format
The following table compares an untagged 802.3 Ethernet packet with an 802.1q VLAN tagged packet:

        802.3 Packet                    #Octets              802.1q VLAN Packet              #Octets

              DA                            6                         DA                        6

              SA                            6                         SA                        6

         Type/Length                        2                     802.1q Tag                    4

              Data                      46-1500                   Type/Length                  2

              CRC                           4                        Data                    46-1500

                                                                     CRC*                      4

Note:        The CRC for the 802.1q tagged frame is re-computed, so that it covers the entire tagged
             frame including the 802.1q tag header. Also, maximum frame size for an 802.1q VLAN packet
             is 1522 octets as opposed to 1518 octets for a normal 802.3z Ethernet packet.

7.4.2                802.1q Tagged Frames
For 802.1q, the Tag Header field consists of four octets comprised of the Tag Protocol Identifier (TPID)
and Tag Control Information (TCI); each taking two octets. The first 16 bits of the tag header makes up
the TPID. It contains the protocol type that identifies the packet as a valid 802.1q tagged packet.
The two octets making up the TCI contain three fields as follows:
 • User Priority (UP)
 • Drop Eligible Indicator (DEI) — Should be set to 0b for transmits. For receives, the device has the
   capability to filter out packets that have this bit set. See the DEIEN and DEI bits in the VLNCTRL.
 • VLAN Identifier (VID)

                         Octet 1                                                   Octet 2

         UP            DEI                                           VID

333369-009                                                                                             467
                                   Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

### 7.4.3 Transmitting and Receiving 802.1q Packets

Since the 802.1q tag is only four bytes, adding and stripping of tags can be done completely in
software. In other words, for transmits, software inserts the tag into packet data before it builds the
transmit descriptor list, and for receives, software strips the 4-byte tag from the packet data before
delivering the packet to upper layer software. However, because adding and stripping of tags in
software adds overhead for the host, the X550 has additional capabilities to add and strip tags in
hardware. See Section 7.4.3.1 and Section 7.4.3.2.

#### 7.4.3.1 Adding 802.1q Tags on Transmits

The inner VLAN header can be added by software in one of the following methods:
 • The header is included in the transmit data buffers.
 • Software might instruct the X550 to insert an 802.1q VLAN tag on a per-packet basis. If the VLE bit
   in the transmit descriptor is set to 1b, the X550 inserts a VLAN tag into the packet that it transmits
   over the wire. The Tag Protocol Identifier — TPID (VLAN Ether Type) field of the 802.1q tag comes
   from the DMATXCTL.VT, and the Tag Control Information (TCI) of the 802.1q tag comes from the
   VLAN field of the legacy transmit descriptor or the VLAN Tag field of the advanced data transmit
   descriptor.
 • In IOV mode, the priority tag, DEI and VLAN ID can be taken from the PFVMVIR (see details in
   Section 7.8.4.2)

#### 7.4.3.2 Stripping 802.1q Tags on Receives

Software might instruct the X550 to strip 802.1q VLAN tags from received packets. The policy whether
to strip the VLAN tag is configurable per queue.
If the RXDCTL.VME bit for a given queue is set to 1b, and the incoming packet is an 802.1q VLAN
packet (that is, its Ethernet Type field matched the VLNCTRL.VET), the X550 strips the 4-byte VLAN tag
from the packet, and stores the TCI in the VLAN Tag field of the receive descriptor.
The X550 also sets the VP bit in the receive descriptor to indicate that the packet had a VLAN tag that
was stripped. If the RXDCTL.VME bit is not set, the 802.1q packets can still be received if they pass the
receive filter, but the VLAN tag is not stripped and the VP bit is not set. If PFQDE.HIDE_VLAN is set, the
VLAN tag is stripped as above, but the VLAN Tag field and the STATUS.VP bit in the Rx descriptor are
cleared.

7.4.4            802.1q VLAN Packet Filtering
VLAN filtering is enabled by setting the VLNCTRL.VFE bit to 1b. If enabled, hardware compares the Type
field of the incoming packet to a 16-bit field in the VLAN Ether Type (VET) register. If the VLAN Type
field in the incoming packet matches the VET register, the packet is compared against the VLAN Filter
Table Array for acceptance.
The VLAN filter register VTFA, is a vector array composed of 4096 bits. The VLAN ID (VID) is a 12-bit
field in the VLAN tag that is used as an index pointer to this vector. If the VID in a received packet
points to an active bit (set to 1b), the packet matches the VLAN filter. The 4096-bit vector is comprised
of 128 x 32 bit registers. The upper 7 bits of the VID selects one of the 128 registers while the lower 5
bits map the bit within the selected register.

468                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Two other bits in the VLNCTRL register, DEIEN and DEI, are also used in conjunction with 802.1q VLAN
filtering operations. DEIEN enables the comparison of the value of the DEI bit in the 802.1q packet to
the Receive Control register DEI bit as acceptance criteria for the packet.
Note:        The VFE bit does not effect whether the VLAN tag is stripped. It only effects whether the
             VLAN packet passes the receive filter.

### 7.4.5 Double VLAN and Single VLAN Support

The X550 supports a mode where all received and sent packets have at least one VLAN tag in addition
to the regular tagging that might optionally be added. In this document, when a packet carries two
VLAN headers, the first header is referred to as an outer VLAN and the second header as an inner VLAN
header (as listed in the table that follows). This mode is used for systems where the near end switch
adds the outer VLAN header containing switching information. This mode is enabled by the following
configuration:
 • This mode is activated by setting the DMATXCTL.GDV and the EXTENDED_VLAN bit in the
   CTRL_EXT register.
 • The EtherType of the VLAN tag used for the additional VLAN is defined in the VET_EXT field in the
   EXVET and EXVET_T registers.

#### 7.4.5.1 Cross Functionality with Manageability

The X550 does not provide any stripping or adding VLAN header(s) to manageability packets.
Therefore, packets that are directed to/from the manageability controller should include the VLAN
headers as part of the Rx/Tx data. The manageability controller should know if the X550 is set to double
VLAN mode as well as the VLAN EtherType(s).

Table 7-48. Double VLAN Packet Format
     MAC Address          Outer VLAN        Inner VLAN                L2 Payload             Ethernet CRC

#### 7.4.5.2 Transmit Functionality

7.4.5.2.1               Transmit Functionality on the Outer VLAN Header

 • A packet with a single VLAN header is assumed to have only the outer VLAN.
 • The outer VLAN header must be added by software as part of the Tx data buffers.
 • Hardware does not relate to the outer VLAN header other than the capability of skipping it for
   parsing inner fields.
 • Hardware expects that any transmitted packet (see the disclaimer that follows) has at least the
   outer VLAN added by software. For any offload that hardware might provide in the transmit data
   path, hardware assumes that the outer VLAN is present. For those packets that an outer VLAN is
   not present, any offload that relates to inner fields to the EtherType might not be provided.

333369-009                                                                                               469
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                               Inline Functions

7.4.5.2.2            Transmit Functionality on the Inner VLAN Header

 • Inner VLAN insertion is handled as described in Section 7.4.3.1.
 • Hardware identifies and skips the VLAN header for parsing inner fields.
 • DCB — The traffic class is dictated by the Tx queue.
 • Pool Filtering — Destination pool(s) and anti-spoofing functionality is based on the Ethernet MAC
   Address and inner VLAN (if present) as described in Section 7.8.3.4 and Section 7.8.4.2.

#### 7.4.5.3 Receive Handling of Packets with VLAN Header(s)

A received frame is analyzed for the existence of the outer and inner VLAN headers. The procedure is as
follows:
  Check the EtherType against the outer VLAN ID. If match then
  {
       Check the next EtherType against the inner VLAN ID. If match
       {
            This is the double VLAN case. Process both outer and inner VLANs as described below
       }
       Else
       {
            Only an outer VLAN exists. Process the outer as described below. Assume no inner VLAN
       }
  }
  Else
  {
       Check the EtherType against the inner VLAN ID. If match
       {
            This is the case of an inner VLAN only. Handle the frame as an unknown frame – device
            does not provide any offloads
       }
       Else
       {
            This is the case of no VLAN. Process the frame (ignore outer and inner VLAN processing)
       }
  }

7.4.5.3.1            Receive Functionality on the Outer VLAN Header

 • Hardware checks the EtherType of the outer VLAN header against the programmed value in the
   EXVET register. VLAN header presence is indicated in the STATUS.VEXT bit in the Rx descriptor.
 • The outer VLAN header is posted as is to the receive data buffers.

7.4.5.3.2            Receive Functionality on the Inner VLAN Header

 • Hardware checks the EtherType of the inner VLAN header against the programmed value in the
   VLNCTRL.VET. VLAN header presence is indicated in the STATUS.VP bit in the Rx descriptor.
 • L2 packet filtering is based on the VLAN ID in the inner VLAN header.
 • Pool Filtering — Destination pool(s) are defined by the Ethernet MAC Address and inner VLAN (if
   presence) as described in Section 7.8.3.3.
 • Inner VLAN tag striping is handled as described in Section 7.4.3.2.

470                                                                                                333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.4.5.4 Packets with No VLAN Headers in Double VLAN Mode

There are some cases when packets might not carry any VLAN headers, even when extended VLAN is
enabled. A few examples for packets that might not carry any VLAN header are: flow control and
priority flow control, LACP, LLDP, GMRP, and optional 802.1x packets. When it is expected to transmit
untagged packets by software in Double VLAN Mode the software must not enable VLAN anti-spoofing
and VLAN validation nor transmit to receive switching.

7.4.5.4.1              Transmit Functionality

DCB — The TC in the Tx data path is directed by the Tx queue of the transmitted packet.
Transmit offload functionality — Software should not enable any offload functions.

7.4.5.4.2              Receive Functionality

Receive offload functionality — pool and queue are selected by the Ethernet MAC Address or ETQF/
ETQS registers. Filtering to host and manageability remains functional.

#### 7.4.5.5 Packets with Two VLAN Headers Not in Double VLAN

                      Mode
When the EXTENDED_VLAN bit in the CTRL_EXT register and DMATXCTL.GDV are not set, hardware
expects that Rx and Tx packets might not carry a VLAN header or a single VLAN header. Hardware does
not relate to the programming of the VET_EXT field in the EXVET register. Tx and Rx handling of
packets with double VLAN headers is unexpected.

### 7.4.6 E-tag and VLAN

In some systems an additional external tag (E-tag) can be present before the VLAN. This section
describes the support for VLANs in presence of external tags.This mode is used for systems where the
device adds a tag to identify a subsystem (usually a VM) and the near end switch adds a tag indicating
the destination subsystem. External tags may be present on part of the packets and missing in others.

#### 7.4.6.1 Transmit Functionality

7.4.6.1.1              Transmit Functionality on the External Tag

The X550 supports insertion of an external tag from a per pool register (PFVMTIR -
Section 8.2.2.22.30) and a VLAN tag from a per pool register (PFVMVIR - Section 8.2.2.22.14) or from
the descriptor as indicated by the VLE bit. The following options are supported:

                                              Hardware Register -
  VLAN source/External Tag Source                                                Embedded in Packet
                                              PFVMTIR/PFVMVIR

Hardware register - PFVMVIR                        Supported                        Not supported

Descriptor                                         Supported                        Not supported

Embedded in Packet                                 Supported                         Supported

333369-009                                                                                            471
                                 Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                             Inline Functions

After the tags are inserted in the packet, the X550 uses the VLAN tag and the EtherType as part of the
forwarding decision as described in Section 7.8.3.4. In a packet with at most one external tag and one
VLAN, the VLAN and EtherType are identified correctly.

#### 7.4.6.2 Receive Handling of Packets with External Tags

External tags can be extracted from the packet according to the PFQDE.STRIP_TAG field
(Section 8.2.2.22.4). Inner tag extraction is handled as described above (Section 7.4.3.2).

7.4.6.2.1                   Packet Priority in Presence of External Tags

The user priority used to define the traffic class of a packet is always taken from the inner VLAN

#### 7.4.6.3 Cross Functionality with Manageability

The X550 does not provide any stripping or adding VLAN header(s) to manageability packets.
Therefore, packets that are directed to/from the manageability controller should include the L2 headers
as part of the Rx/Tx data. The manageability controller should know if it is expected to add/receive an
external tag as part of the packet.

#### 7.4.6.4 Packet User Priority (802.1P) Bits Handling

The user priority bits may be used by the device for multiple purposes:
1. Defining the traffic class to which the traffic is associated (Section 7.6.3.1).
2. Defining which packets get a Timestamp in Buffer (Section 7.1.6.2).
3. Defining if a packet matches and EtherType filter (Section 7.1.3.3).
For all these purposes, the UP bits are taken from the outermost tag with UP bits (E-tag or VLAN),
unless the VLNCTRL.UP_FIRST_TAG_EN bit is cleared, in which case, it is always taken from the inner
VLAN.
The table below summarize the tag from which the user priority is extracted from the packets.

Table 7-49. UP Extraction Rules
          Packet Type                 VLNCTRL.UP_FIRST_TAG_EN = 1b                   VLNCTRL.UP_FIRST_TAG_EN = 0b

Un-tagged Packet                  User priority = 0                               User priority = 0

Packet with a single VLAN         The user priority field from the VLAN header.   Single VLAN mode:
                                                                                   The user priority field from the VLAN header.
                                                                                  Double VLAN mode:
                                                                                   User priority = 0

Packet with a VLAN and an outer   The user priority field from the outer VLAN     The user priority field from the inner VLAN
tag (outer VLAN or E-tag)         header                                          header.

Packet with E-tag only            The user priority field from the E-tag          User priority = 0

472                                                                                                                  333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions
