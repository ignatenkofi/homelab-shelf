## 7.8 Virtualization

### 7.8.1 Overview

I/O virtualization is a mechanism that can be used to share I/O resources among several consumers.
For example, in a virtual system, multiple operating systems are loaded and each operates as though
the entire system's resources were at its disposal. However, for the limited number of I/O devices, this
presents a problem because each operating system might be in a separate memory domain and all the
data movement and device management has to be done by a Virtual Machine Monitor (VMM). VMM
access adds latency and delay to I/O accesses and degrades I/O performance. Virtualized devices are
designed to reduce the burden of the VMM by making certain functions of an I/O device shared among
multiple guest operating systems or a Virtual Machine (VM), thereby allowing each VM direct access to
the I/O device.
The X550 supports two modes of operations of virtualized environments:
1. Direct assignment of part of the port resources to different guest operating systems using the PCI
   SIG SR IOV standard. Also known as native mode or pass-through mode. This mode is referenced
   as IOV mode throughout this section.
2. Central management of the networking resources by an IOVM or by the VMM. Also known as
   software switch acceleration mode. This mode is referred to as VMDq2 mode in this section.
The virtualization offloads capabilities provided by the X550 apart from the replication of functions
defined in the PCI SIG IOV specification are part of VMDq2.
A hybrid model, where part of the VMs are assigned a dedicated share of the port and the rest are
serviced by an IOVM is also supported. However, in this case the offloads provided to the software
switch might be more limited. This model can be used when parts of the VMs run operating systems for
which VF drivers are available and thus can benefit from an IOV and others that run older operating
systems for which VF drivers are not available and are serviced by an IOVM. In this case, the IOVM is
assigned one VF and receives all the packets with Ethernet MAC Addresses of the VMs behind it.
The following section describes the support the X550 provides for these modes.
This section assumes a single-root implementation of IOV and no support for multi-root.

#### 7.8.1.1 Direct Assignment Model

The direct assignment support in the X550 is built according to the following model of the software
environment.
It is assumed that one of the software drivers sharing the port hardware behaves as a master driver
(Physical Function or PF driver). This driver is responsible for the initialization and the handling of the
common resources of the port. All the other drivers (Virtual Function drivers or VF drivers) might
read part of the status of the common parts but cannot change them. The PF driver might run either in
the VMM or in some service operating system. It might be part of an IOVM or part of a dedicated
service operating system.
In addition, part of the non time-critical tasks are also handled by the PF driver. For example, access to
CSR through the I/O space or access to the configuration space are available only through the master
interface. Time-critical CSR space like control of the Tx and Rx queue or interrupt handling is replicated
per VF, and directly accessible by the VF driver.

333369-009                                                                                              503
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

Note:     In some systems with a thick hypervisor, the service operating system might be an integral
          part of the VMM. For these systems, each reference to the service operating system in the
          sections that follow refer to the VMM.

7.8.1.1.1            Rationale

The direct assignment model enables each of the VMs to receive and transmit packets with minimum of
overhead. Non time-critical operations such as initialization and error handling can be done via the PF
driver. In addition, it is important that the VMs can operate independently with minimal disturbance. It
is also preferable that the VM interface to hardware should be as close as possible to the native
interface in non-virtualized systems to minimize the software development effort.
The main time critical operations that require direct handling by the VM are:
 • Maintenance of the data buffers and descriptor rings in host memory. To support this, the DMA
   accesses of the queues associated to a VM should be identified as such on the PCIe using a different
   requester ID.
 • Handling of the hardware ring (tail bump and head updates)
 • Interrupts handling
The capabilities needed to provide independence between VMs are:
 • Per-VM reset and enable capabilities
 • Tx rate control
 • Allocating separate CSR space per VM. This CSR space is organized as close as possible to the
   regular CSR space to enable sharing of the base driver code.
Note:     The rate control and VF enable capabilities are controlled by the PF.

#### 7.8.1.2 System Overview

The following drawings show the various elements involved in the I/O process in a virtualized system.
Figure 7-38 shows the flow in software VMDq2 mode and Figure 7-39 shows the flow in IOV mode.
This section assumes that in IOV mode, the driver on the guest operating system is aware that it
operates in a virtual system (para-virtualized) and there is a channel between each of the VM drivers
and the PF driver allowing message passing such as configuration request or interrupt messages. This
channel can use the mailbox system implemented in the X550 or any other means provided by the VMM
vendor.

504                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

                                   Data
               Packet switch                    Guest      Guest
                                  Control
                  IOVM                          OS 1       OS n

                                   VMM                                                        SW

        Translated                                                                            HW
           Mem                                          Translated
        Accesses                                           Mem                    Host
          (VT-x)                   CPUs
                                                        Accesses                 memory
                                                          (VT-x)
              Init +                                                             DMA packet
             control                                                              Buffers

                                IOH (VT-d)      Translated DMA           Physical address
                                                Accesses (VT-d)

                                              IOVI     IOVI
                                             Physical Physical
                                             Address Address

                 Shared
                                            VM-1        VM-n
                  part

                                            VMDq queuing

         LAN Controller

Figure 7-38. System Configuration for VMDq2 Mode

333369-009                                                                                         505
                                 Did this document help answer your questions?

                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                  Inline Functions

                                                    Guest                      Guest
                        IOVM        Control
                                                    OS 1                       OS n

                                                                                                                  SW
                                           VMM

                                                                                                      Host
                                                                                                     memory
                                                                                                                  HW

            Translated                                                    Translated
               Mem                         CPU                               Mem               VM n PB
            Accesses                                                      Accesses
              (VT-x)                                                        (VT-x)            IOVM PB

                                                                                               VM 1 PB

                                                            Guest 1
                               Real time                    Physical
                                Control           Real time Address      Real time
                 Init                              Control                Control

         IOH (VT-d)                                  Translated DMA
                                                     Accesses (VT-d)
                                                                                         Physical addresses

                                        IOVM         Guest 1           Guest n
                                       Physical      Physical          Physical
                                       Address       Address           Address

                      Shared
                                      PF              VM-1              VM-n
                       part

                                                      VMDq queuing

         LAN Controller

Figure 7-39. System Configuration for IOV Mode

506                                                                                                                    333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

### 7.8.2 PCI-SIG SR-IOV Support

#### 7.8.2.1 SR-IOV Concepts

SR-IOV defines the following entities in relation to I/O virtualization:
 • Virtual Image (VI) — Part of the I/O resources are assigned to a A VM.
 • I/O Virtual Intermediary (IOVI) or I/O Virtual Machine (IOVM) — A special VM that owns
   the physical device and is responsible for the configuration of the physical device.
 • Physical function (PF) — A function representing a physical instance — One port for the X550.
   The PF driver is responsible for the configuration and management of the shared resources in the
   function.
 • Virtual Function (VF) — A part of a PF assigned to a VI.

#### 7.8.2.2 Configuration Space Replication

The SR-IOV specification defines a reduced configuration space for the virtual functions. Most of the
PCIe configuration of the VFs comes from the PF.
This section describes the expected handling of the different parts of the configuration space for virtual
functions. It deals only with the parts relevant to the X550.
Details of the configuration space for virtual functions can be found in Section 9.3.

7.8.2.2.1              Legacy PCI Configuration Space

The legacy configuration space is allocated to the PF only and emulated for the VFs. A separate set of
BARs and one bus master enable bit is allocated in the SR-IOV capability structure in the PF and is used
to define the address space used by the entire set of VFs.
All the legacy error reporting bits are emulated for the VF. See Section 7.8.2.4 for details.

7.8.2.2.2              Memory BARs Assignment

The SR-IOV specification defines a fixed stride for all the VF BARs, so that each VF can be allocated part
of the memory BARs at a fixed stride from a basic set of BARs. In this method, only two decoders per
replicated BAR per PF are required and the BARs reflected to the VF are emulated by the VMM.
The only BARs that are useful for the VFs are BAR0 and BAR3, so only those are replicated. Table 7-62
lists the existing BARs and the stride used for the VFs:

Table 7-62. BARs in the X550 (64-bit BARs)
  BAR        Type        Usage                                 Requested Size per VF (=Stride)

   0, 1      Mem       CSR space      Maximum (16 KB, page size). For page size see Section 9.2.4.4.8 for more details.

    2        n/a        Not used      N/A

   3, 4      Mem         MSI-X        Maximum (16 KB, page size).

    5        n/a        Not used      N/A

BAR0 of the VFs are a sparse version of the original PF BAR and include only the register relevant to the
VF. For more details see Section 7.8.2.7.

333369-009                                                                                                                507
                                   Did this document help answer your questions?

                                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                                 Inline Functions

Figure 7-40 shows the different BARs in an IOV-enabled system:

                                 PF configuration space
                                                                     128K CSR + FLASH
                                                                           Space
              64 bit BARs mode

                                     BAR0, BAR 1                     32 bytes I/O Space
                                         BAR2
                                      BAR3 (Null)                       MSI-X Space
                                     BAR4, BAR 5                     Max (16K, Page Size)

                                                                                                 VF0 – CSR Space
                                                                                                Max (16K, Page Size)
                                                                                                 VF1 – CSR Space
                                         ...                                                    Max (16K, Page Size)
          IOV capability

                                    VF BAR0, BAR1
                                                                      VF0 – MSI-X Space                 ...
            structure

                                    VF BAR2 (Null)
                                                                     Max (16K, Page Size)
                                    VF BAR3, BAR4                                                VF63 – CSR Space
                                                                      VF1 – MSI-X Space         Max (16K, Page Size)
                                    VF BAR5 (Null)
                                                                     Max (16K, Page Size)
                                          ...
                                                                             ...

                                                                     VF63 – MSI-X Space
                                                                     Max (16K, Page Size)

Figure 7-40. BARs in an IOV-enabled System

7.8.2.2.3                          PCIe Capability Structure

The PCIe capability structure is shared between the PF and the VFs. The only relevant bits that are
replicated are:
 • Transaction pending.
 • Function Level Reset (FLR). See Section 7.8.2.3 for details.

7.8.2.2.4                          MSI and MSI-X Capabilities

Both MSI and MSI-X are implemented in the X550. MSI-X vectors can be assigned per VF. MSI is not
supported for the VFs.
See Table 9-16 for more details of the MSI-X and PBA tables implementation.

7.8.2.2.5                          VPD Capability

VPD is implemented only once and is accessible only from the PF.

7.8.2.2.6                          Power Management Capability

The X550 does not support power management per VF. The power management registers exist for each
VF, but only the D0 power state is supported.

508                                                                                                                    333369-009
                                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.8.2.2.7              Serial ID

Serial ID capability is not exposed in VFs.

7.8.2.2.8              Error Reporting Capabilities (Advanced and Legacy)

All the bits in this capability structure are implemented only for the PF. Note that the VMs see an
emulated version of this capability structure. See Section 7.8.2.4 for details.

#### 7.8.2.3 FLR Capability

The FLR bit is required per VF. Setting of this bit resets only a part of the logic dedicated to the specific
VF and does not influence the shared part of the port. This reset should disable the queues, disable
interrupts and the stop receive and transmit process per VF.
Setting the PF FLR bit resets the entire function.

#### 7.8.2.4 Error Reporting

Error reporting includes legacy error reporting and Advanced Error Reporting (AER) or role-based
capability.
The legacy error management includes the following functions:
 • Error capabilities enablement — These are set by the PF for all the VFs. Narrower error
   reporting for a given VM can be achieved by filtering of the errors by the VMM. This includes:
     — SERR# Enable
     — Parity Error Response
     — Correctable Reporting Enable
     — Non-Fatal Reporting Enable
     — Fatal Reporting Enable
     — UR Reporting Enable
 • Error status in the configuration space — These should be set separately for each VF. This
   includes:
     — Master Data Parity Error
     — Signaled Target Abort
     — Received Target Abort
     — Master Abort
     — SERR# Asserted
     — Detected Parity Error
     — Correctable Error Detected
     — Non-Fatal Error Detected
     — Unsupported Request Detected

333369-009                                                                                                509
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

AER capability includes the following functions:
 • Error capabilities enablement — The Error Mask, and Severity bits are set by the PF for all the
   VFs. Narrower error reporting for a given VM can be achieved by filtering of the errors by the VMM.
   These includes:
      — Uncorrectable Error Mask Register
      — Uncorrectable Error Severity Register
      — Correctable Error Mask Register
      — ECRC Generation Enable
      — ECRC Check Enable
 • Non-Function Specific Errors Status in the configuration space
      — Non-Function Specific Errors are logged in the PF
      — Error logged in one register only
      — VI avoids touching all VFs to clear device level errors
      — The following errors are not function specific
          • All Physical Layer errors
          • All Link Layer errors
          • ECRC Fail
          • UR, when caused by no function claiming a TLP
          • Receiver Overflow
          • Flow Control Protocol Error
          • Malformed TLP
          • Unexpected Completion
 • Function Specific Errors Status in the configuration space
      — Allows Per-VF error detection and logging
      — Help with fault isolation
      — The following errors are function specific:
          • Poisoned TLP received
          • Completion Timeout
          • Completer Abort
          • UR, when caused by a function that claims a TLP
          • ACS Violation
 • Error logging — Each VF has it’s own header log.
 • Error messages — To ease the detection of the source of the error, the error messages should be
   emitted using the requester ID of the VF in which the error occurred.

510                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.8.2.5 Alternative Routing ID (ARI) and IOV Capability

                      Structures
To allow more than eight functions per end point without requesting an internal switch, as usually
needed in virtualization scenarios, the PCI-SIG defines the ARI capability structure. This is a new
capability that enables an interpretation of the Device and Function fields as a single identification of a
function within the bus. In addition, a new structure used to support the IOV capabilities reporting and
control is defined. Both structures are described in sections Section 9.2.4.3 and Section 9.2.4.4. Refer
to the following section for details on the Requester ID (RID) allocation to VFs.

#### 7.8.2.6 RID Allocation

RID allocation of the VF is done using the Offset field in the IOV structure. This field should be
replicated per VF and is used to do the enumeration of the VFs.
Each PF includes an offset to the first associated VF. This pointer is a relative offset to the Bus/Device/
Function (BDF) of the first VF. The Offset field is added to PF’s requester ID to determine the requester
ID of the next VF. An additional field in the IOV capability structure describes the distance between two
consecutive VF’s requester IDs.

7.8.2.6.1              Bus Device Function Layout

7.8.2.6.1.1             ARI Mode

ARI allows interpretation of the device ID part of the RID as part of the function ID inside a device.
Thus, a single device can span up to 256 functions. To ease the decoding, the least significant bit of the
function number points to the physical port number. The Next bits indicate the VF number. Table 7-63
lists the VF RIDs.
The layout of RID’s used by the X550 is reported to the operating system via the PCIe IOV capability
structure. See Section 9.2.4.4.6.

Table 7-63. RID per VF — ARI Mode
    Port        VF#          B,D,F            Binary                                   Notes

    0 PF          B,0,0          B,00000,000   PF

    1 PF          B,0,1          B,00000,001   PF

     0           1          B,16,0          B,10000,000   Offset to first VF from PF is 128.

     1           1          B,16,1          B,10000,001

     0           2          B,16,2          B,10000,010

     1           2          B,16,3          B,10000,011

     0           3          B,16,4          B,10000,100

     1           3          B,16,5          B,10000,101

     ...

     0           64         B,31,6          B,11111,110

     1           64         B,31,7          B,11111,111   Last

333369-009                                                                                              511
                                 Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                    Inline Functions

7.8.2.6.1.2             Non-ARI Mode

When ARI is disabled, non-zero devices in the first bus cannot be used, thus a second bus is needed to
provide enough RIDs. In this mode, the RID layout is as follows:

Table 7-64. RID per VF — Non-ARI Mode
      Port       VF#         B,D,F          Binary                                    Notes

    0 PF         B,0,0        B,00000,000    PF

    1 PF         B,0,1        B,00000,001    PF

       0          0        B+1,16,0     B+1,10000,000    Offset to first VF from PF is 384.

       1          0        B+1,16,1     B+1,10000,001

       0          1        B+1,16,2     B+1,10000,010

       1          1        B+1,16,3     B+1,10000,011

       0          2        B+1,16,4     B+1,10000,100

       1          2        B+1,16,5     B+1,10000,101

       ...

       0          63       B+1,31,6     B+1,11111,110

       1          63       B+1,31,7     B+1,11111,111    Last

Note:        When the device ID of a physical function changes (because of LAN disable or LAN function
             select settings), the VF device IDs changes accordingly.

#### 7.8.2.7 Hardware Resources Assignment

The main resources to allocate per VM are queues and interrupts. The assignment is static. If a VM
requires more resources, it might be allocated to more than one VF. In this case, each VF gets a specific
Ethernet MAC Address/VLAN tag to enable forwarding of incoming traffic. The two VFs are then teamed
in software.

7.8.2.7.1              PF Resources

A possible use of the PF is for a configuration setting without transmit and receive capabilities. In this
case, it is not allocated to any queues but is allocated to one MSI-X vector.
The PF has access to all the resources of all VMs, but it is not expected to make use of resources
allocated to active VFs.

7.8.2.7.2              Assignment of Queues to VF

See Section 7.2.1.2.1 for allocating Tx queues.
See Section 7.1.3.2 for allocating Rx queues.
Table 7-65 lists the Tx and Rx queues to VF allocation.

512                                                                                                     333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-65. Queue to VF Allocation
      VF           Queues in 16 VMs Mode              Queues in 32 VMs Mode         Queues in 64 VMs Mode

      0                      0-7                                0-3                          0-1

      1                      8-15                               4-7                          2-3

      ...                     ...                               ...                          ...

      15                   120-127                              ...                          ...

      ...                                                       ...                          ...

      31                                                      124-127                        ...

      ...                                                                                    ...

      63                                                                                   126-127

7.8.2.7.3              Assignment of MSI-X Vector to VF

See Section 7.3.4.3 for allocating MSI-X vectors in IOV mode.

#### 7.8.2.8 CSR Organization

CSRs can be divided into three types:
 • Global Configuration registers that should be accessible only to the PF — For example, link control
   and LED control. These types of registers also include all of the debug features such as the mapping
   of the packet buffers and is responsible for most of the CSR area requested by the X550. This
   includes per VF configuration parameters that can be set by the PF without performance impact.
 • Per-VF parameters — For example, per VF reset, interrupt enable, etc. Multiple instances of these
   parameters are used only in an IOV system and only one instance is needed for non IOV systems.
 • Per-queue parameters that should be replicated per queue — For example, head, tail, Rx buffer
   size, TPH tag, etc. These parameters are used by both a VF in an IOV system and by the PF in a
   non-IOV mode.
To support IOV without distributing the current drivers operation in legacy mode, the following method
is used:
 • The PF instance of BAR0 continues to contain the legacy and control registers. It is accessible only
   to the PF. The BAR enables access to all the resources including the VF queues and other VF
   parameters. However, it is expected that the PF driver does not access these queues in IOV mode.
 • The VF instances of BAR0 provide control on the VF specific registers. These BARs have the same
   mapping as the original BAR0 with the following exceptions:
     — Fields related to the shared resources are reserved.
     — The queues assigned to a VF are mapped at the same location as the first same number of
       queues of the PF.
 • Assuming some backward compatibility is needed for IOV drivers, The PF/VF parameters block
   should contain a partial register set as described in VF Device Registers section.

333369-009                                                                                                  513
                                    Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Inline Functions

#### 7.8.2.9 SR IOV Control

To control the IOV operation, the physical driver is provided with a set of registers. These include:
 • The mailbox mechanism described in the next section.
 • The switch and filtering control registers described in Section 7.8.3.9.
 • PFVFLREC register indicating that a VFLR reset occurred in one of the VFs (bitmap).

7.8.2.9.1                  VF-to-PF Mailbox

The VF drivers and the PF driver require some means of communication between them. This channel
can be used for the PF driver to send status updates to the VFs (such as link change, memory parity
error, etc.) or for the VF to send requests to the PF (add to VLAN).
Such a channel can be implemented in software, but requires enablement by the VMM vendors. To
avoid the need for such an enablement, the X550 provides such a channel that enables direct
communication between the two drivers.
The channel consists of a mailbox. Each driver can then receive an indication (either poll or interrupt)
when the other side wrote a message.
Assuming a maximum message size of 64 bytes (one cache line), a memory of 64 bytes x 64 VMs = 4
KB is provided per port. The RAM is organized as follows:

Table 7-66. Mailbox Memory
            RAM Address                        Function                      PF BAR 0 Mapping1             VF BAR 0 Mapping2

              0 — 63                          VF0 <-> PF                             0 — 63                    VF0 + MBO

             64 — 127                         VF1 <-> PF                         64 — 127                      VF1 + MBO

                                                                   ....

       (4 KB-64) — (4 KB-1)                   VF63<-> PF                    (4 KB-64) — (4 KB-1)               VF63 + MBO

1.    Relative to mailbox offset.
2.    MBO = mailbox offset in VF CSR space.

In addition for each VF, the VFMailbox and PFMailbox registers are defined to coordinate the
transmission of the messages. These registers contain a semaphore mechanism to enable coordination
of the mailbox usage.
The PF driver can decide which VFs are allowed to interrupt the PF to indicate a mailbox message using
the PFMBIMR mask register.
The following flows describe the usage of the mailbox:

Table 7-67. PF-to-VF Messaging Flow
      Step                    PF Driver                                   Hardware                         VF #n driver

# 1 Set PFMAILBOX[n].PFU.

# 2 Set PFU bit if PFMAILBOX[n].VFU is

                                                          cleared.

# 3 Read PFMAILBOX[n] and check that

                PFU bit was set. Otherwise wait and
                go to Step 1.

# 4 Write message to relevant location in

                VFMBMEM.

514                                                                                                                       333369-009
                                          Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-67. PF-to-VF Messaging Flow [continued]
    Step                  PF Driver                             Hardware                           VF #n driver

# 5 Set the PFMAILBOX[n].STS bit and

              wait for ACK1.

# 6 Indicate an interrupt to VF #n.

# 7 Read the message from VFMBMEM.

# 8 Set the VFMAILBOX[n].ACK bit.

# 9 Indicate an interrupt to PF.

# 10 Clear PFMAILBOX[n].PFU.

1. The PF might implement a timeout mechanism to detect non-responsive VFs.

Table 7-68. VF-to-PF Messaging Flow
    Step                  PF Driver                             Hardware                           VF #n Driver

# 1 Set VFMAILBOX.VFU.

# 2 Set VFU bit if VFMAILBOX[n].PFU is

                                                   cleared.

# 3 Read VFMAILBOX[n] and check that

                                                                                        VFU bit was set. Otherwise wait and
                                                                                        go to Step 1.

# 4 Write message to relevant location in

                                                                                        VFMBMEM.

# 5 Set the VFMAILBOX[n].REQ bit.

# 6 Indicate an interrupt to PF.

# 7 Read PFMBICR to detect which VF

              caused the interrupt.

# 8 Read the adequate message from

              VFMBMEM.

# 9 Set the PFMAILBOX[n].ACK bit.

# 10 Indicate an interrupt to VF #n.

# 11 Clear VFMAILBOX[n].VFU.

The content of the message is hardware independent and is determined by software.
The messages currently assumed by this specification are:
 • Registration to VLAN/multicast packet/broadcast packets — A VF can request to be part of a given
   VLAN or to get some multicast/broadcast traffic.
 • Reception of large packet — Each VF should notify the PF driver what is the largest packet size
   allowed in receive.
 • Get global statistics — A VF can request information from the PF driver on the global statistics.
 • Filter allocation request — A VF can request allocation of a filter for queuing/immediate interrupt
   support.
 • Global interrupt indication.
 • Indication of errors.

333369-009                                                                                                                515
                                      Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

#### 7.8.2.10 DMA

7.8.2.10.1           RID

Each VF is allocated a RID. Each DMA request should use the RID of the VM that requested it. See
Section 7.8.2.6 for details.

7.8.2.10.2           Sharing of the DMA Resources

The outstanding requests and completion credits are shared between all the VFs. The tags attached to
read requests are assigned the same way as in a non-virtualized setting, although in VF systems tags
can be re-used for different RIDs.

7.8.2.10.3           TPH

The TPH enable is common to all the devices (all PFs and VFs). Given a TPH enabled device, each VM
might decide for each queue, on which type of traffic (data, headers, Tx descriptors, Rx descriptors) the
TPH should be asserted and what is the CPU ID assigned to this queue.
Note:     There are no plans to virtualize TPH in the IOH. Thus, the physical CPU ID should be used in
          the programming of the CPUID field.

#### 7.8.2.11 Timers

7.8.2.11.1           TCP Timer

The TCP timer is available only to the PF. It might indicate an interrupt to the VFs via the mailbox
mechanism.

7.8.2.11.2           IEEE 1588

IEEE 1588 is a per-link function and thus is controlled by the PF driver. The VMs have access to the real
time clock register.

7.8.2.11.3           Free Running Timer

The free running timer is a PF driver resource the VMs can access. This register is read only to all VFs
and is reset only by the PCI reset.

#### 7.8.2.12 Power Management and Wake-Up

Power management is a PF resource and is not supported per VF.

516                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

#### 7.8.2.13 Link Control

The link is a shared resource and as such is controllable only by the PF. This includes interface settings,
speed and duplex settings, flow control settings, etc. The flow control packets are sent with the station
Ethernet MAC Address stored in the NVM. The watermarks of the flow control process and the time-out
value are also controllable by the PF only. In a DCB environment, the parameters of the per TC flow
control are also part of the PF responsibilities.
Double VLAN is a network setting and as such should be common to all VFs.

7.8.2.13.1             Special Filtering Options

Pass bad packets is a debug feature. As such, pass bad packets is available only to the PF. Bad packets
are passed according to the same filtering rules of the regular packets.
Note:        Pass bad packets might cause guest operating systems to get unexpected packets. As a
             result, it should be used only for debug purposes of the entire system.
Receiving long packets is enabled separately per Rx queue in the RXDCTL registers. As this impacts the
flow control thresholds, the PF should be made aware of the decision of all the VMs. Because of this, the
setup of TSO packets is centralized by the PF and each VF might request this setting.

### 7.8.3 Packet Switching

#### 7.8.3.1 Assumptions

The following assumptions are made:
 • The required bandwidth for the VM-to-VM loopback traffic is low. That is, the PCIe bandwidth is not
   congested by the combination of the VM-to-VM and the regular incoming traffic. This case is
   handled but not optimized for. Unless specified otherwise, Tx and Rx packets should not be dropped
   or lost due to congestion caused by loopback traffic.
 • If the buffer allocated for the VM-to-VM loopback traffic is full, it is acceptable to back pressure the
   transmit traffic of the same TC. This means that the outgoing traffic might be blocked if the
   loopback traffic is congested.
 • The decision on local traffic is done only according to the Ethernet DA address and the VLAN tag.
   There is no filtering according to other parameters (IP, L4, etc.). The switch has no learning
   capabilities. In case of double VLAN mode, the inner VLAN is used for the switching functionality.
 • The forwarding decisions are based on the receive filtering programming.
 • No packet switching between TCs.
 • Coexistence with TimeSync: time stamp is not sampled for any VM-to-VM loopback traffic.
 • Coexistence with Double VLAN: When double VLAN is enabled by DMATXCTL.GDV and it is expected
   to transmit untagged packets by software, transmit to receive packet switching should not be
   enabled.

333369-009                                                                                              517
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

#### 7.8.3.2 Pool Selection

Pool selection is described in the following sections. A packet might be forwarded to a single pool or
replicated to multiple pools. Multicast and broadcast packets are cases of replication, as is mirroring.
The following capabilities determine the destination pools of each packet:
 • 128 Ethernet MAC Address filters (RAH/RAL registers) for both unicast and multicast filtering. These
   are shared with L2 filtering. For example, the same Ethernet MAC Addresses are used to determine
   if a packet is received by the switch and to determine the forwarding destination. In “E-tag pool
   select” mode RAL registers bits [13:0] are used for E-tag filtering {GRP, E-CID_base} and pool
   selection.
 • 64 shared VLAN filters (PFVLVF and PFVLVFB registers) — Each VM can be made a member of each
   VLAN.
 • Hash filtering of unicast and multicast addresses (if the direct filters previously mentioned are not
   sufficient).
 • Forwarding of broadcast packets to multiple pools.
 • Forwarding by EtherType.
 • Mirroring by pool, VLAN, or link.
Receive pool/queue allocation refer to Section 7.1.3.2.

#### 7.8.3.3 Rx Packets Switching

Rx packet switching is the second of three stages that determine the destination of a received packet.
The three stages are defined in Section 7.1.3.
As far as switching is concerned, it does not matter whether the X550’s virtual environment operates in
IOV mode or in VMDq2 mode.
When operating in replication mode, broadcast and multicast packets can be forwarded to more than
one pool, and is replicated to more than one Rx queue. Replication is enabled by the Rpl_En bit in the
PFVTCTL register.
Note:     For the following algorithms packets with no E-tag in PFVTCTL.POOLING_MODE = 01b (E-tag
          mode), or all packets in PFVTCTL.POOLING_MODE = 00b (MAC mode) are defined as packets
          with no external tags.

7.8.3.3.1            Replication Mode Enabled

When replication mode is enabled, each broadcast/multicast packet can go to more than one pool.
Finding the pool list of any packet is provided in the following steps:
1. Exact unicast or multicast match — If there is a match in one of the exact filters (RAL/RAH), for
   unicast or multicast packets, use the MAC Pool Select Array (MPSAR[n]) bits as a candidate for the
   pool list. Note that MPSAR[n] must not enable more than one pool for unicast RAL/RAH filters. The
   compared field differs according to the filtering mode (PFVTCTL.POOLING_MODE):
      a. If POOLING_MODE = 00b (MAC mode) or for packets with no external tags, the Destination MAC
         Address is compared to {RAH[15:0], RAL[31:0]} for all the registers for which
         RAH.ADTYPE = 0 (MAC)

518                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

     b. If POOLING_MODE = 01b (E-tag mode) and the packet has an E-tag, the E-tag E-PID (as
        extracted from offset 47:34, starting from the EtherType, in the tag identified by the
        ETAG_ETYPE register) is compared to RAL[13:0] for all the registers for which RAH.ADTYPE = 1
        (E-tag)
2. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list.
3. Broadcast — If the packet is a broadcast packet with no external tag, add pools for which their
   PFVML2FLT.BAM bit (Broadcast Accept Mode) is set.
4. Unicast hash — If the packet is a unicast packet with no external tag, and the prior steps yielded
   no pools, check it against the Unicast Hash Table (PFUTA). If there is a match, add pools for which
   their PFVML2FLT.ROPE bit (Accept Unicast Hash) is set.
5. Multicast hash — If the packet is a multicast packet with no external tag and the prior steps
   yielded no pools, check it against the Multicast Hash Table (MTA). If there is a match, add pools for
   which their PFVML2FLT.ROMPE bit (Receive Multicast Packet Enable) is set.
6. Multicast promiscuous — If the packet is a multicast packet with no external tag, take the
   candidate list from prior steps and add pools for which their PFVML2FLT.MPE bit (Multicast
   Promiscuous Enable) is set.
7. Unicast Promiscuous - If the packet is a unicast packet with no external tag, take the candidate
   list from prior steps and add pools for which their PFVML2FLT.UPE bit (Unicast Promiscuous Enable)
   is set.
8. VLAN groups — This step is relevant only when VLAN filtering is enabled by the VLNCTRL.VFE bit.
     a. Tagged packets: enable only pools in the packet’s VLAN group as defined by the VLAN filters —
        PFVLVF[n] and their pool list — PFVLVFB[n] or pools for which the PFVML2FLT.VPE (VLAN
        Promiscuous Enable) is set.
     b. Untagged packets: enable only pools with their PFVML2FLT.AUPE bit set.
     c. If there is no match, the pool list should be empty.
    Note:      In a VLAN network, un-tagged packets are not expected. Such packets received by the
               switch should be dropped, unless their destination is a virtual port set to receive these
               packets. The setting is done through the PFVML2FLT.AUPE bit. It is assumed that VMs for
               which this bit is set are members of a default VLAN and thus only MAC queuing is done on
               these packets.
9. Default Pool — If the pool list is empty at this stage and the PFVTCTL.DIS_DEF_POOL bit is
   cleared, set the default pool bit in the target pool list (from PFVTCTL.DEF_PL).
10. EtherType filters — If one of the EtherType filters (ETQF) is matched by the packet and pooling
    action is requested and the Pool Enable bit in the ETQF is set, the pool list is set to the pool pointed
    to by the filter.
11. Filter Local Packets (source address pruning) - The pruning operation depends on the filtering
    mode (PFVTCTL.POOLING_MODE):
     a. If POOLING_MODE = 00b (MAC mode) or for packets with no external tag, the Source MAC
        Address is compared to {RAH[15:0], RAL[31:0]} for all the registers for which RAH.ADTYPE = 0
        (MAC).
     b. If POOLING_MODE = 01b (E-tag mode) and the packet has an E-tag, {00,E-tag ingress-E-
        CID_base} (as extracted from offset 31:20, starting from the EtherType, in the tag identified by
        the ETAG_ETYPE register) is compared to RAL[13:0] for all the registers for which
        RAH.ADTYPE = 1 (E-tag).

333369-009                                                                                               519
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                  Inline Functions

      If there is a match to one of the RAL[n]/RAH[n] clear all the pools that are set in both the matching
      MPSAR[n] and the PFFLP from the pool list. This prunes multicast packets from getting back to the
      sender in VEPA mode.
12. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list. The
    PFVFRE register blocks reception by a VF while the PF configures its registers.
13. Mirroring — Each of the four mirroring rules adds its destination pool (PFMRCTL.MP) to the pool
    list if the following applies:
      a. Pool mirroring — PFMRCTL.VPME is set and one of the bits in the pool list matches one of the
         bits in the PFMRVM register.
      b. VLAN port mirroring — PFMRCTL.VLME is set and the index of the VLAN of the packet in the
         PFVLVF table matches one of the bits in the PFMRVLAN register.
      c. Uplink port mirroring — PFMRCTL.UPME is set, the pool list is not empty.
14. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list. The
    PFVFRE register blocks reception by a VF while the PF configures its registers. Note that this stage
    appears twice to handle mirroring cases.

7.8.3.3.2              Replication Mode Disabled

When replication mode is disabled, software should take care of multicast and broadcast packets and
check which of the VMs should get them. In this mode, the pool list of any packet always contains one
pool only according to the following steps:
1. Exact unicast or multicast match — The compared field differs according to the filtering mode
   (PFVTCTL.POOLING_MODE):
      a. If POOLING_MODE = 00b (MAC mode) or for packets with no external tags, the Destination MAC
         Address is compared to {RAH[15:0], RAL[31:0]} for all the registers for which RAH.ADTYPE =

# 0 (MAC)

      b. If POOLING_MODE = 01b (E-tag mode) and the packet has an E-tag, the E-tag E-PID (as
         extracted from offset 47:34, starting from the EtherType, in the tag identified by the
         ETAG_ETYPE register) is compared to RAL[13:0] for all the registers for which RAH.ADTYPE = 1
         (E-tag)
      If the compared field matches one of the exact filters (RAL/RAH), use the MAC Pool Select Array
      (MPSAR[n]) bits as a candidate for the pool list. Note that MPSAR[n] must not enable more than
      one pool for unicast RAL/RAH filters.
2. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list.
3. Unicast hash — If the packet is a unicast packet with no external tag, and the prior steps yielded
   no pools, check it against the Unicast Hash Table (PFUTA). If there is a match, add the pool for
   which their PFVML2FLT.ROPE (Accept Unicast Hash) bit is set. Refer to the software limitations
   described after Step 8.
4. VLAN groups — This step is relevant only when VLAN filtering is enabled by the VLNCTRL.VFE bit.
      a. Tagged packets: enable only pools in the packet’s VLAN group as defined by the VLAN filters —
         PFVLVF[n] and their pool list — PFVLVFB[n] or pools for which the PFVML2FLT.VPE (VLAN
         Promiscuous Enable) is set.
      b. Untagged packets: enable only pools with their PFVML2FLT.AUPE bit set.
      c. If there is no match, the pool list should be empty.

520                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

5. Default Pool — If the pool list is empty at this stage and the PFVTCTL.DIS_DEF_POOL bit is
   cleared, set the default pool bit in the target pool list (from PFVTCTL.DEF_PL).
6. Multicast or Broadcast — If the packet is a multicast or broadcast packet with no external tag
   and was not forwarded in Step 1 and Step 2, set the default pool bit in the pool list (from
   PFVTCTL.DEF_PL).
7. EtherType filters — If one of the EtherType filters (ETQF) is matched by the packet and queuing
   action is requested and the Pool Enable bit in the ETQF is set, the pool list is set to the pool pointed
   by the filter.
8. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list. The
   PFVFRE register blocks reception by a VF while the PF configures its registers.
The following software limitations apply when replication is disabled:
 • Software must not set more than one bit in the bitmaps of the exact filters. Note that multiple bits
   can be set in an RAH register as long as it’s guaranteed that the packet is sent to only one queue by
   other means (such as VLAN).
 • Software must not set per-VM promiscuous bits (multicast or broadcast).
 • Software must not set the ROPE bit in more than one PFVML2FLT register.
 • Software should not activate mirroring.
 • Software should not filter out local packets by setting PFFLP bits

#### 7.8.3.4 Tx Packets Switching

Tx switching is used only in a virtualized environment to serve VM-to-VM traffic. Packets that are
destined to one or more local VMs are directed back (loopback) to the Rx packet buffers. Enabling Tx
switching is done by setting the PFDTXGSWC.LBE bit. Tx to Rx switching always avoids packet drop as if
flow control is enabled. Therefore, the software must set the FCRTH[n].RTH fields regardless if flow
control is activated on the X550.
Tx switching rules are very similar to Rx switching in a virtualized environment, with the following
exceptions:
 • If a target pool is not found, the default pool is used only for broadcast and multicast packets.
 • A unicast packet that matches an exact filter is not sent to the LAN.
 • Broadcast and multicast packets are always sent to the external LAN.
 • A packet might not be sent back to the originating pool (even if the destination address is equal to
   the source address) unless loopback is enabled for that pool by the PFVMTXSW[n] register.
The detailed flow for pool selection as well as the rules that apply to loopback traffic is as follows:
 • Loopback is disabled when the network link is disconnected. It is expected (but not required) that
   system software (including VMs) does not post packets for transmission when the link is
   disconnected.
 • Loopback is disabled when the RXEN (Receive Enable) bit is cleared.
 • Loopback packets are identified by the LB bit in the receive descriptor.
Notes:       When Tx switching is enabled, the host must avoid sending packets longer than 9.5 KB.
             Tx Switching should be enabled only if PFVTCTL.POOLING_MODE = 00b (MAC mode).

333369-009                                                                                                521
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

7.8.3.4.1             Replication Mode Enabled

When replication mode is enabled, the pool list for any packet is determined according to the following
steps:
1. Exact unicast or multicast match — If there is a match in one of the exact filters (RAL/RAH), for
   unicast or multicast packets, take the MPSAR[n] bits as a candidate for the pool list. Note that
   MPSAR[n] must not enable more than one pool for unicast RAL/RAH filters.
2. Ether-type filters — If one of the enabled (ETQF.TX_ANTISPOOF) Transmit Ether-type filters
   (ETQF.ETYPE) is matched by the packet and the appropriate Pool loopback/anti-spoof bit in the
   PFVFSPOOF is set (PFVFSPOOF.ETHERTYPELB/PFVFSPOOF.ETHERTYPEAS), the pool list is set to the
   pool pointed to by the ETQS matching register (loopback) or the packet is dropped (anti-spoof). All
   the subsequent steps after Step 3 are skipped.
      Note:    Loopback on ETQF match is possible even if the general loopback enable bit
               (PFDTXGSWC.LBE) is clear.
3. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list.
4. Broadcast — If the packet is a broadcast packet, add pools for which their PFVML2FLT.BAM bit
   (Broadcast Accept Mode) is set.
5. Unicast hash — If the packet is a unicast packet, and the prior steps yielded no pools, check it
   against the Unicast Hash Table (PFUTA). If there is a match, add pools for which their
   PFVML2FLT.ROPE bit (Accept Unicast Hash) is set.
6. Multicast hash — If the packet is a multicast packet and the prior steps yielded no pools, check it
   against the Multicast Hash Table (MTA). If there is a match, add pools for which their
   PFVML2FLT.ROMPE bit (Receive Multicast Packet Enable) is set.
7. Unicast Promiscuous — If the packet is a unicast packet, take the candidate list from prior steps
   and add pools for which their PFVML2FLT.UPE bit (Unicast Promiscuous Enable) is set.
8. Multicast Promiscuous — If the packet is a multicast packet, take the candidate list from prior
   steps and add pools for which their PFVML2FLT.MPE bit (Multicast Promiscuous Enable) is set.
9. Filter source pool — The pool from which the packet was sent is removed from the pool list unless
   the PFVMTXSW.LLE bit is set.
10. VLAN groups — This step is relevant only when VLAN filtering is enabled by the VLNCTRL.VFE bit.
      a. Tagged packets: enable only pools in the packet’s VLAN group as defined by the VLAN filters —
         PFVLVF[n] and their pool list — PFVLVFB[n] or pools for which the PFVML2FLT.VPE (VLAN
         Promiscuous Enable) is set.
      b. Untagged packets: enable only pools with their PFVML2FLT.AUPE bit set.
      c. If there is no match, the pool list should be empty.
11. Forwarding to the network — Packets are forwarded to the network in the following cases:
      a. All broadcast and multicast packets.
      b. Unicast packets that do not match any exact filter. A match of an exact filter that also points to
         a pool disabled via PFVFRE is not considered a match.
12. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list (pre
    mirroring step).

522                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

13. Mirroring — Each of the following three mirroring rules adds its destination pool (PFMRCTL.MP) to
    the pool list if the following applies:
     a. Pool mirroring — PFMRCTL.VPME is set and one of the bits in the pool list matches one of the
        bits in the PFMRVM register.
     b. VLAN port mirroring — PFMRCTL.VLME is set and the index of the VLAN of the packet in the
        PFVLVF table matches one of the bits in the PFMRVLAN register.
     c. Downlink port mirroring — PFMRCTL.DPME is set and the packet is sent to the network.
14. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list (post
    mirroring step).

7.8.3.4.2              Replication Mode Disabled

When replication mode is disabled, software should take care of multicast and broadcast packets and
check which of the VMs should get them. In this mode the pool list for any packet always contains one
pool only according to the following steps:
1. Exact unicast or multicast match — If the packet DA matches one of the exact filters (RAL/
   RAH), take the MPSAR[n] bits as a candidate for the pool list. Note that MPSAR[n] must not enable
   more than one pool for unicast RAL/RAH filters.
2. Ether-type filters - if one of the enabled (ETQF.TX_ANTISPOOF) Transmit Ether-type filters
   (ETQF.ETYPE) is matched by the packet and the appropriate Poll loopback/anti-spoof bit in the
   PFVFSPOOF is set (PFVFSPOOF.ETHERTYPELB/PFVFSPOOF.ETHERTYPEAS), the pool list is set to the
   pool pointed to by the ETQS matching register (loopback) or the packet is dropped (anti-spoof). All
   the subsequent steps after Step 3 are skipped.
Note:        Loopback on EtherType match is possible even if the general loopback enable bit
             (PFDTXGSWC.LBE) is clear.
3. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list.
4. Unicast hash — If the packet is a unicast packet, and the prior steps yielded no pools, check it
   against the Unicast Hash Table (PFUTA). If there is a match, add the pool for which their
   PFVML2FLT.ROPE bit (Accept Unicast Hash) is set. Refer to the software limitations that follow.
5. VLAN groups — This step is relevant only when VLAN filtering is enabled by the VLNCTRL.VFE bit.
     a. Tagged packets: enable only pools in the packet’s VLAN group as defined by the VLAN filters —
        PFVLVF[n] and their pool list — PFVLVFB[n] or pools for which the PFVML2FLT.VPE (VLAN
        Promiscuous Enable) is set.
     b. Untagged packets: enable only pools with their PFVML2FLT.AUPE bit set.
     c. If there is no match, the pool list should be empty.
6. Multicast or Broadcast — If the packet is a multicast or broadcast packet and was not forwarded
   in Step 1 and Step 2, set the default pool bit in the pool list (from PFVTCTL.DEF_PL).
7. Filter source pool — The pool from which the packet was sent is removed from the pool list unless
   the PFVMTXSW.LLE bit is set.
8. Forwarding to the Network — Packets are forwarded to the network in the following cases:
     a. All broadcast and multicast packets.
     b. Unicast packets that do not match any exact filter. A match of an exact filter that also points to
        a pool disabled via PFVFRE is not considered a match.
9. PFVFRE — If any bit in the PFVFRE register is cleared, clear the respective bit in the pool list.

333369-009                                                                                             523
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

The following software limitations apply when replication is disabled:
1. It is software’s responsibility not to set more than one bit in the bitmaps of the exact filters. Note
   that multiple bits can be set in an RAH register as long as it is guaranteed that the packet is sent to
   only one queue by other means (such as VLAN)
2. Software must not set per-VM promiscuous bits (multicast or broadcast).
3. Software must not set the ROPE bit in more than one PFVML2FLT register.
4. Software should not activate mirroring.

#### 7.8.3.5 Mirroring Support

The X550 supports four separate mirroring rules, each associated with a destination pool (mirroring can
be done in up to four pools). Each rule is programmed with one of the four mirroring types:
 • Pool Mirroring — Reflects all the packets received to a pool from the network.
 • Uplink Port Mirroring — Reflects all the traffic received from the network that reached any pool.
 • Downlink Port Mirroring — Reflects all the traffic transmitted to the network.
 • VLAN Mirroring — Reflects all the traffic received from the network in a set of given VLANs (either
   from the network or from local VMs).
Note:     Reflecting all the traffic received by any of the pools (either from the network or from local
          VMs) is supported by enabling mirroring of all pools.
Note:     To get all traffic irrespective of the filtering rules, the mirroring pool should be set to
          promiscuous mode and promiscuous VLAN mode.
Note:     Mirroring and replication on FCoE traffic is not supported on receive if the ETQF filters define
          FCoE packets and on transmit if the packets are indicated as FCoE (by setting the FCoE bit in
          the TUCMD field in the Transmit Context Descriptor).
Mirroring modes are controlled by a set of rule control registers:
 • PFMRCTL — Controls the rules to be applied and the destination port.
 • PFMRVLAN — Controls the VLAN ports as listed in the PFVLVF table taking part in the VLAN mirror
   rule.
 • PFMRVM — Controls the pools taking part in the pool mirror rule.

#### 7.8.3.6 Offloads

The general rule is that offloads are executed as configured for the pool and queue associated with the
receive packet. Some special cases:
 • If a packet is directed to a single pool, offloads are determined by the pool and queue for that
   packet.
 • If a packet is replicated to more than one pool, each copy of the packet is offloaded according to the
   configuration of its pool and queue.
 • If replication is disabled, offloads are determined by the unique destination of the packet.
The following subsections describe exceptions to the previously described special cases.

524                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

7.8.3.6.1              Local Traffic Offload

The following capabilities are not supported on the loopback path:
 • The RSS and VLAN strip offload capabilities are only supported if the CC bit in the transmit
   descriptor of the packet is set and if it is a tunnel packet, the TUNNEL.OUTERIPCS is set also. The
   reason is that when these bits are not set, software does not provide the necessary offload offsets
   with the Tx packet.
 • Receive Side Coalescing (RSC) is not supported.
 • FCoE offloads are not supported.

7.8.3.6.2              Rx Traffic Offload

 • CRC offload is a global policy. CRC strip is enabled or disabled for all received packets.

#### 7.8.3.7 Rate Control Features

7.8.3.7.1              Congestion Control

Tx packets going through the local switch are stored in the Rx packet buffer, similar to packets received
from the network. Tx to Rx switching always avoids packet drop as if flow control is enabled. Therefore,
the software must set the FCRTH[n].RTH fields regardless if flow control is activated on the X550.
The X550 guarantees that one TC flow is not affected by congestion in another TC.
Receive and local traffic are provided with the same priority and performance expectations. Packets
from the two sources are merged in the Rx packet buffers, which can in general support both streams
at full bandwidth. Any congestion further in the pipeline (such as lack of PCIe bandwidth) evenly affects
Rx and local traffic.

7.8.3.7.2              Tx Queue Arbitration and Rate Control

To guarantee each pool with adequate bandwidth, a per-pool bandwidth control mechanism is added to
the X550. Each Tx pool gets a percentage of the transmit bandwidth and is guaranteed it can transmit
within its allocation. This arbitration is combined with the TC arbitration. See additional details on DCB
Tx capabilities in Section 7.6.2.1.

7.8.3.7.3              Receive Priority

As the switch might decide to loopback packets from the transmit path to the receive path, in case the
receive path is full, the transmit path might be blocked (including the traffic to the LAN). The X550
guarantees that packets are not dropped because of that and that one traffic class flow is not affected
by congestion in another traffic class. The PF driver might decide to program the X550 to drop packets
from receive queues without available descriptors.
To keep the congestion effect locality, receive traffic from the LAN have higher priority than loop back
traffic. This way large loopback traffic does not impact the network.

333369-009                                                                                             525
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                 Inline Functions

#### 7.8.3.8 Small Packets Padding

In Virtualized systems, the driver receiving the packet in the VM might not be aware of all the hardware
offloads applied to the packet. Thus, in case of stripping actions by the hardware (VLAN strip), it might
receive packets which are smaller than a legal packet. The X550 provides an option to pad small
packets in such cases so that all packets have a legal size. This option can be enabled only if the CRC is
stripped. In these cases, all small packets are padded to 60 bytes (legal packet - 4 bytes CRC). The
padding is done with zero data. This function is enabled via the RDRXCTL.PSP bit.
Packet padding is done after tag extractions and do not take into account if tags are exposed in the Rx
descriptor status.
Notes:     FCoE DDP packets are not padded.
           The packet length reported in the descriptor reflects the packet length before padding.
           If a timestamp is added, it is part of the padding data.

#### 7.8.3.9 Switch Control

The PF driver has some control of the switch logic. The following registers are available to the PF for this
purpose:
 • PFVTCTL (PF Virtual Control Register)
      — RPL_EN (Replication Enable) — Enables replication of multicast and broadcast packets —
        both in incoming and local traffic. If this bit is cleared, Tx multicast and broadcast packets are
        sent only to the network and Rx multicast and broadcast packets are sent to the default pool.
      — DEF_PL (Default Pool) — Defines the target pool for packets that passed L2 filtering but did
        not pass any of the pool filters. This field is invalid when the DIS_DEF_POOL bit is set.
      — DIS_DEF_POOL (Disable Default Pool) — Disables acceptance of packets that failed all pool
        filters.
 • PFVFRE (PF VF Receive Enable) — Enables/disables reception of packets from the link to a
   specific VF. Used during initialization of the VF. See Section 4.2.2.2 for more details.
 • PFDTXGSWC (PF DMA Tx General Switch Control)
      — LBE (Loopback Enable) — VMDQ loopback enables switching of Tx traffic to the Rx path for
        VM-to-VM communication.
 • PFVFSPOOF (PFVF Anti-Spoof Control)
      — MACAS (MAC Anti-Spoof Enable) — Enables filtering of Tx packet for anti-spoof.
 • PFVMTXSW (PF VM Tx Switch Loopback Enable)
      — LLE (Local Loopback Enable) — Local Loopback Enable defines whether to allow loopback of
        a packet from a certain pool into itself.
 • PFQDE (PF Queue Drop Enable Register) — A register defining global policy for drop enable
   functionality when no descriptors are available. It lets the PF override the per-queue SRRCTL[n]
   DROP_EN setting. PFQDE should be used in SR-IOV mode as described in Section 4.6.11.3.1.
 • PFVML2FLT (PF VM L2Control Register)
      — ROMPE (Receive Overflow Multicast Packets) — Accept multicast hash. Defines whether a
        pool accepts packets that match the multicast MTA table.

526                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

     — ROPE (Receive MAC Filters Overflow) — Accept unicast hash. Defines whether a pool
       accepts packets that match the unicast PFUTA table.
     — BAM (Broadcast Accept) — Defines whether a pool accepts broadcast packets.
     — MPE (Multicast Promiscuous Enable) — Defines whether or pool accepts all multicast
       packets.
     — AUPE (Accept Untagged Packets Enable) — Defines whether a pool accepts untagged VLAN
       packets.
 • Mirror Control — See Section 7.8.3.5.
 • PFVFTE (PF VF Transmit Enable) — Enables/disables transmission of packets to the link to a
   specific VF. Used during initialization of the VF. See Section 4.2.2.2 for more details.
 • PFVLVF/PFVLVFB (PF VM VLAN Pool Filter/Bitmap) — VLAN queuing table. A set of 64 VLAN
   entries with an associated bitmap, one bit per pool. Bits are set for each pool that participates in
   this VLAN.
 • PFUTA (PF Unicast Table Array) — A 4 Kb array that covers all combinations of 12 bits from the
   MAC destination address. A received unicast packet that misses the MAC filters is compared against
   the PFUTA. If the relevant bit in the PFUTA is set, the packet is routed to all pools for which the
   ROPE bit is set.
 • MTA (Multicast Table Array) — A 4 Kb array that covers all combinations of 12 bits from the MAC
   destination address. A received multicast packet that misses the MAC filters is compared against
   the MTA. If the relevant bit in the MTA is set, the packet is routed to all pools for which the ROMPE
   bit is set.
In addition, the rate-control mechanism is programmed as described in Section 7.6.2.1.

### 7.8.4 Security Features

The X550 allows some security checks on the inbound and outbound traffic of the switch.

#### 7.8.4.1 Inbound Security

Each incoming packet (either from the LAN or from a local VM) is filtered according to the VLAN tag so
that packets from one VLAN cannot be received by pools that are not members of that VLAN.

#### 7.8.4.2 Outbound Security

7.8.4.2.1              MAC Anti-Spoofing

Each pool is associated with one or more Ethernet MAC Addresses on the receive path. The association
is determined through the MPSAR registers. The MAC anti-spoofing capability insures that a VM always
uses a source Ethernet MAC Address on the transmit path that is part of the set of Ethernet MAC
Addresses defined on the Rx path. A packet with a non-matching SA is dropped, preventing spoofing of
the Ethernet MAC Address. This feature is enabled in the PFVFSPOOF.MACAS field, and can be enabled
per Tx pool.
Note:        Anti-spoofing is not available for VMs that hide behind other VMs whose Ethernet MAC
             Addresses are not part of the RAH/RAL Ethernet MAC Address registers. In this case, anti-
             spoofing should be done by software switching, handling these VMs.

333369-009                                                                                               527
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

7.8.4.2.2            VLAN Anti-Spoofing

Each pool is associated with one or more VLAN tags on the receive path. The association is determined
through the PFVLVF and PFVLVFB registers. The VLAN anti-spoofing capability insures that a VM always
uses a VLAN tag on the transmit path that is part of the set of VLAN tags defined on the Rx path. A
packet with a non-matching VLAN tag is dropped, preventing spoofing of the VLAN tag. This feature is
enabled in the PFVFSPOOF.VLANAS field, and can be enabled per Tx pool.
Notes:    If VLAN anti-spoofing is enabled, MAC anti-spoofing must be enabled as well.
          When double VLAN is enabled by DMATXCTL.GDV and it is expected to transmit untagged
          packets by software, VLAN anti-spoofing should not be enabled.
          Un-tagged packets are not checked by VLAN anti-spoofing.

7.8.4.2.3            VLAN Tag Validation

In PCI-SIG IOV scenarios the driver might be malicious, and thus might fake a VLAN tag. The X550
provides the ability to force a specific VLAN value for a VM. The possible behaviors are controlled by the
PFVMVIR[n] registers as follows:
 • Use descriptor value — To be used in case of a trusted VM that can decide which VLAN to send.
   This option should also be used in case one VM is member of multiple VLANs.
 • Always insert default VLAN — This mode should be used for non-trusted or non-VLAN aware
   VMs. In this case, any VLAN insertion command from the VM is ignored. If a packet is received with
   a VLAN, the packet should be dropped.
 • Never insert VLAN — This mode should be used in a non-VLAN network. In this case, any VLAN
   insertion command from the VM is ignored. If a packet is received with a VLAN, the packet should
   be dropped.
Notes:    The VLAN insertion settings should be done before any of the queues of the VM are enabled.
          When double VLAN is enabled by DMATXCTL.GDV and it is expected to transmit untagged
          packets by software, VLAN validation should not be enabled.

7.8.4.2.4            E-tag Insertion

In addition to the VLAN insertion described above, the device can add an E-tag to the packets sent by a
VF. The PFVMVIR[n].TAGA bit defines if a tag should be added. If this bit is set, the added tag is as
follows:
 • TAGA = 00b (MAC mode) or 11b (Reserved): Insert no tag.
 • TAGA = 01b (E-tag mode): An E-tag is added as follows:
         {TAG_ETYPE.ETAG_ETHERTYPE[15:0], PFVMTIR.PORT_TAG_ID[31:0], 0x0000}

Notes:    The E-tag insertion settings should be done before any of the queues of the VM are enabled.

7.8.4.2.5            Ether-type Anti-Spoofing/Pruning

Each pool can be set to drop packets associated with one or more (up to 8) Ether-types on the transmit
path. The Ether-types are defined using the ETQF registers. The Ether-type pruning (anti-spoof)
capability ensures that a VM does not send out LLDP/ECP control frames to external switches. The
Ether-type loopback capability enables the loopback of link layer packets to a pre defined pool
destination.

528                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Ether-type pruning (anti-spoof) feature is enabled in the PFVFSPOOF.ETHERTYPEAS field, and can be
enabled per transmit pool. Ether-type loopback feature is enabled in the PFVFSPOOF.ETHERTYPELB
field, and can be enabled per transmit pool.

#### 7.8.4.3 Malicious Driver Detection

The hardware can be programmed to take some action as a result of some misbehavior of a VM. These
actions might hint to the fact that some VM is malicious and the VMM should remedy the situation. To
inform the VMM of this fact, The Mailbox bit (EICR.MAILBOX bit) may be set to indicate the occurrence
of such behavior. The LMVM_RX and LMVM_TX register contains information on which queue
(LMVM_TX.LAST_Q or LMVM_RX.LAST_Q) and port (LMVM_TX.MAL_PF and LMVM_RX.MAL_PF) the
malicious behavior was detected. The LVMMC_TX and LVMMC_RX registers contain information on the
type of error detected and are clear by read.
Malicious driver behavior detection is enabled by setting the DMATXCTL.MDP_EN and
RDRXCTL.MDP_EN bits to 1. This capability should be enabled before queues are exposed to non
trusted virtual machines.
On detection of a malicious driver event the X550 stops activity of the offending queue, and sets the bit
matching the offending queue in WQBR_RX and WQBR_TX registers. If DMATXCTL.MBINTEN or
RDRXCTL.MBINTEN are set, the X550 generates an interrupt for transmit or receive errors respectively
by asserting the EICR.MAILBOX bit. Cause of Malicious driver activation is reported in the LVMMC_TX
and LVMMC_RX registers. To re-activate offending queue, driver should release it by setting the
matching bit in WQBR_RX or WQBR_TX register.
The WQBR_RX and WQBR_TX registers keeps track of all the queues on which a malicious activity was
detected and can be used by the driver to track multiple events.
After the queue is disabled the initialization flow defined in Section 4.6.7.1 for receive queues and in
Section 4.6.8.1 for transmit queues should be applied.

7.8.4.3.1               Queue Context Validation

The X550 checks that the queue context submitted when a queue is enabled is valid. It also prevents
change to static configuration while the queue is enabled. These checks are done both for receive and
transmit queues. The table below describes the checks done on the queue context:

     Check type                          Description                     Bit in LVMMC_TX/RX          Action

Receive queue context   Check that:                                     INVALID_RXQ_CONTEXT   Prevent Enable of
validity                 • RDLEN >0                                                           queue
                         • SRRCTL.BSIZEPACKET > 0
                         • SRRCTL.BSIZEHEADER > 0 if DESCTYP
                           requires header split
                         • SRRCTL.BSIZEHEADER <= 1024
                         • SRRCTL.DESCTYPE is valid

Receive queue context   Attempt to write RDBAL, RDBAH, RDLEN, or                              Disable queue.
change on the fly       SRRCTL while queue is enabled

Transmit queue          Check that:                                     INVALID_TXQ_CONTEXT   Prevent Enable of
context validity         • TDLEN >0                                                           queue

Transmit queue          Attempt to write TDBAL, TDBAH, TDLEN, TDWBAL,                         Disable queue.
context change on the   or TDWBAH while queue is enabled
fly

Note:        Queue zero is enabled by default. Thus, if malicious driver protection is enabled, to change
             Queue zero configuration, the queue should be disabled.

333369-009                                                                                                        529
                                   Did this document help answer your questions?

                                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                                    Inline Functions

7.8.4.3.2                  Transmit Descriptor Validity Checks

The table below describes the checks are done by the X550 to define if a transmit packet descriptor is
valid. All the checks are done on the descriptors. The checks on the packet header are described in the
previous sections.

Table 7-69. Malicious Driver - TX Descriptor Checks
      Check type                                 Description                            Bit in LVMMC_TX              Action

Mac Header size            Checks that the MAC header size in the context              MAC_HEADER            Drop Packet and stop
                           descriptor is at least 14 (or 18 in case of offloaded                             offending queue
                           packet and double VLAN).

IPV4 Header                If a checksum or TSO offload is required, checks that       IPV4_HEADER           Drop Packet and stop
                           the IPv4 header size in the context descriptor is at                              offending queue
                           least 20.

IPV6 Header                If a TSO offload is required, checks that the IPv6          IPV6_HEADER           Drop Packet and stop
                           header size in the context descriptor is at least 40.                             offending queue

Wrong MAC_IP               Check that the MAC+ IP (+ OUTERIP + TUNNEL)                 WRONG_MAC_IP          Drop Packet and stop
                           header size is not bigger than the packet size.                                   offending queue

TCP header size            If a TCP TSO offload is required, checks that the TCP       TCP_LSO               Drop Packet and stop
                           header size in the context descriptor is at least 20.                             offending queue

UDP header size            If a UDP TSO offload is required, checks that the TCP       UDP_LSO               Drop Packet and stop
                           header size in the context descriptor is at least 8.                              offending queue

SCTP data size             If a SCTP checksum offload is required, checks that         STCP_CS               Drop Packet and stop
                           the SCTP L4 packet size (including header and data)                               offending queue
                           is at least 12.

Packet too big             In case of a single send, check that the packet is not      SIZE                  Drop Packet and stop
                           larger than 15.5KBytes.                                                           offending queue

Packet too small           Check that the total length of the packet transmitted,      N/A                   Silently drop packet.
                           not including FCS is at least 13 bytes.

Illegal offload request.   Check that TSO is no requested for SCTP or that a           OFF_ILL               Drop Packet and stop
                           checksum offload is not requested for IPv6 packets.                               offending queue

Illegal IPsec offload      Check that a VF had not requested IPsec offload             IPSEC_OFFLOAD         Drop Packet and stop
request by VF                                                                                                offending queue

Illegal FCoE offload       Check that a VF had not requested FCoE offload              FCOE_OFFLOAD          Drop Packet and stop
request by VF                                                                                                offending queue

SCTP alignment             If an SCTP CRC offload is requested, check that the         SCTP_ALIGNED          Drop Packet and stop
                           data size is 4 byte aligned.                                                      offending queue

Zero MSS                   Check that the MSS size is larger than zero.                ZERO_MSS              Drop Packet and stop
                                                                                                             offending queue

Context in middle of       Check that a context descriptor is not sent in the          CONTEXT_IN_PACKET     Drop Packet and stop
packet                     middle of a packet.                                                               offending queue

Number of large send       Check that the Large send header is contained in at         LSO_MORE_THAN_4       Drop Packet and stop
header buffers             most 4 buffers.                                                                   offending queue

Buffers size and length    For single send, check that the total of all buffers size   OOS_SSO               Drop Packet and stop
match - Single Send        and the packet length match.                                                      offending queue

Buffers size and length    For LSO, check that the total of all buffers size and       OOS_LSO               Drop Packet and stop
match - Large Send         the packet length match.                                                          offending queue

LSO wrong header size      For LSO, check that the size of the header fetched          N/A                   Silently drop packet.
                           actually match the expected header size.                                          Counted in SSVPC

UDP data size              If a UDP checksum offload is required, checks that the      SSO_UDP               Drop Packet and stop
                           UDP L4 packet size in the context descriptor is at least                          offending queue
                           8.

530                                                                                                                      333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Inline Functions

Table 7-69. Malicious Driver - TX Descriptor Checks [continued]
      Check type                               Description                            Bit in LVMMC_TX                  Action

 TCP data size            If a TCP checksum offload is required, checks that the     SSO_TCP                   Drop Packet and stop
                          TCP L4 packet size in the context descriptor is at least                             offending queue
                          20.

 Descriptor Type          Check that only descriptor types 2 (context) or 3                                    Drop Packet and stop
                          (advanced data descriptor) are used.                                                 offending queue
                                                                                     DESC_TYPE
 CC bit not set when      CC (Check Context) bit in descriptor is not set in                                   Drop Packet and stop
 needed                   virtualization mode.                                                                 offending queue

 Null packet check        Check that a Null packet has the EOP bit set.              WRONG_NULL                Drop Packet and stop
                                                                                                               offending queue

 Packet without EOP       Check that a only entire packets are provided by the       NO_EOP                    Drop Packet and stop
                          driver                                                                               offending queue

 Burst of contexts        Check that less than 4 Contiguous context descriptor       CONTEXT_BURST             Drop Packet and stop
                          are sent by the driver.                                                              offending queue

 Legacy Descriptor in     Legacy descriptor used when SR-IOV is enabled.             LEGACY_DESC_IOV           Drop Packet and stop
 SR-IOV                                                                                                        offending queue

7.8.4.3.3                 Reactive Malicious Behavior Detection

The table below describes the checks are done by the X550 to detect a malicious behavior, even if the
packet seems valid.

Table 7-70. Reactive Malicious Checks
      Check type                               Description                           Bit in LVMMC_TX/RX                Action

 Malicious VF memory      A PCIe DMA access initiated by a VF ended with             INV_MACC                  Drop Packet and stop
 access                   Unsupported Request (UR) or Completer Abort (CA).                                    offending queue
                          This check is done for both Tx and Rx queues.

                          A Queue attempt to read memory outside of the              INV_MACC                  Drop PCIe read
                          active memory range of the system. See                                               transaction. Stop
                          Section 3.1.5.7 for details.                                                         queue that requested
 DMA access outside of                                                                                         the transaction
 active memory 1
                          A Queue attempt to write memory outside of the             N/A                       Silently drop PCIe
                          active memory range of the system. See                                               write transaction.
                          Section 3.1.5.7 for details.

 VLAN not expected in     A packet where VLAN should be added by device is in        VLAN_IERR                 Drop Packet
 packet                   Tx descriptor. See Section 7.8.4.2.3

 Anti-spoof checks        See Section 7.8.4.2.1 and Section 7.8.4.2.2 and            MAC_VLAN_SPOOF            Drop Packets.
                          Section 7.8.4.2.5 for details

1. A PCIe error interrupt can be asserted when such a transaction is dropped. See Section 3.1.5 for details.

333369-009                                                                                                                          531
                                       Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions

### 7.8.5 Virtualization of Hardware

This section describes additional features used in both IOV and VMDq2 modes.

#### 7.8.5.1 Per-Pool Statistics

Part of the statistics are by definition shared and cannot be allocated to a specific VM. For example, CRC
error count cannot be allocated to a specific VM, as the destination of such a packet is not known if the
CRC is wrong.
All the non-specific statistics are handled by the PF driver in the same way it is done in non-virtualized
systems. A VM might request a statistic from the PF driver but might not access it directly.
The conceptual model used to gather statistics in a virtualization context is that each queue pool is
considered as a virtual link and the Ethernet link is considered as the uplink of the switch. Thus, any
packet sent by a pool is counted in the Tx statistics, even if it was forwarded to another pool internally
or was dropped by the MAC for some reason. In the same way, a replicated packet is counted in each of
the pools receiving it.
The following statistics are provided per pool:
 • Good packet received count
 • Good packet transmitted count
 • Good octets received count
 • Good octets transmitted count
 • Multicast packets received count
Note:     All the per VF statistics are read only and wrap around after reaching their maximum value.
