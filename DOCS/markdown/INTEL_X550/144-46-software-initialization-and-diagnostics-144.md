## 4.6 Software Initialization and Diagnostics

### 4.6.1 Introduction

This section discusses general software notes for the X550, especially initialization steps. These include:
 • General hardware power-up state
 • Basic device configuration
 • Interrupts initialization
 • Initialization of transmit
 • Receive initialization
 • Link configuration
 • Software reset capability
 • Statistics
 • Diagnostic hints
 • FCoE initialization
 • Virtualization support initialization
 • DCB configuration
 • Security (IPsec) support initialization

### 4.6.2 Power-Up State

When the X550 powers up, it automatically reads the NVM. The NVM contains sufficient information to
bring the link up and configure the X550 for manageability and/or APM wake-up. However, software
initialization is required for normal operation.

156                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

### 4.6.3 Initialization Sequence

The following sequence of commands is typically issued to the device by the software device driver to
initialize the X550 to normal operation. The major initialization steps are:
1. Disable interrupts.
2. Issue a global reset and perform general configuration — see Section 4.6.3.2.
3. Wait for the NVM auto-read completion.
4. Wait for manageability configuration done indication (EEMNGCTL.CFG_DONE0/1).
5. Wait until the DMA initialization completes (RDRXCTL.DMAIDONE).
6. Setup the PHY and the link — see Section 3.7.3.2 and Section 3.7.3.3.
7. Initialize all statistical counters — see Section 4.6.5.
8. Initialize receive — see Section 4.6.7.
9. Initialize transmit — see Section 4.6.8.
10. Initialize FCoE — see Section 4.6.9
11. Initialize Virtualization support — see Section 4.6.10
12. Configure DCB — see Section 4.6.11
13. Configure Security (IPsec) — see Section 4.6.12.
14. Enable interrupts — see Section 4.6.3.1.

#### 4.6.3.1 Interrupts During Initialization

Most drivers disable interrupts during initialization to prevent re-entrance. Interrupts are disabled by
writing to the EIMC register. Note that the interrupts need to also be disabled after issuing a global
reset, so a typical driver initialization flow is:
1. Disable interrupts.
2. Issue a global reset.
3. Disable interrupts (again).
After initialization completes, a typical driver enables the desired interrupts by writing to the EIMS
register.

#### 4.6.3.2 Global Reset and General Configuration

Global reset = software reset + link reset.
Device initialization typically starts with a software reset that puts the device into a known state and
enables the device driver to continue the initialization sequence. Following a global reset the software
driver should poll the CTRL.RST until it is cleared and then wait at least 10 ms to enable a smooth
initialization flow.
To enable flow control, program the FCTTV, FCRTL, FCRTH, FCRTV and FCCFG registers. If flow control is
not enabled, these registers should be written with 0x0. If Tx flow control is enabled, Tx CRC by
hardware should be enabled as well (HLREG0.TXCRCEN = 1b). Refer to Section 3.7.4.3.2 through
Section 3.7.4.3.5 for recommended settings of the Rx packet buffer sizes and flow control thresholds.

333369-009                                                                                               157
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

Note:     FCRTH[n].RTH fields must be set by default regardless if flow control is enabled or not.
          FCRTH[n].FCEN should be set to 0b if flow control is not enabled as all the other registers
          previously indicated.
The link inter-connect configuration according to the electrical specification of the relevant electrical
interface should be set prior to the link setup. This configuration is done through the PHY image section
of the NVM by applying the appropriate settings to the link interconnect block.

4.6.4            100 Mb/s, 1 GbE, and 10 GbE Link Initialization
Refer to Section 3.7.3.3 and Section 3.7.3.2 for the initialization and link setup steps. The device driver
uses the MDIO register to initialize the PHY and setup the link. Section 3.7.3 describes the usage of the
MDIO register.

#### 4.6.4.1 MAC Settings Automatically Based on Speed Resolved

                    by PHY
FCCFG.RFCE              Must be set by software after reading flow control resolution from PHY
                        registers.
FCCFG.TFCE              Must be set by software after reading flow control resolution from PHY
                        registers.
MAC Speed               Speed setting is established from the PHY's internal indication to the MAC after
                        the PHY has auto-negotiated a successful link up.
PHY Speed               The speed resolution by the PHY with a link partner according to the setup
                        made in the PHY Auto-negotiation registers.
STATUS.LINKUP           Must be set by the PF to reflect a link indication from the LINKS register. This is
                        useful for IOV mode.
LINKS.LINK_STATUS       Reflects the PHY internal indication to the MAC.
LINKS.LINK_SPEED        Reflects the actual speed setting negotiated by the PHY and indicated to the
                        MAC.

### 4.6.5 Initialization of Statistics

Statistics registers are hardware-initialized to values as detailed in each particular register's
description. The initialization of these registers begins upon transition to a D0 active power state (when
internal registers become accessible, as enabled by setting the Memory Access Enable field of the PCIe
Command register), and is guaranteed to complete within 1 ms of this transition. Note that access to
statistics registers prior to this interval might return indeterminate values.
All statistical counters are cleared on read and a typical device driver reads them (thus making them
zero) as a part of the initialization sequence.
Queue counters are mapped using the RQSMR registers for Rx queues, and TQSM registers for Tx
queues. Refer to the RQSMR register section for RQSMR setup, and to the TQSM register section for
TQSM setup. Note that if software requires the queue counters, the RQSMR and TQSM registers must
be reprogrammed following a device reset.

158                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

### 4.6.6 Interrupt Initialization

#### 4.6.6.1 Working with Legacy or MSI Interrupts

 • Software driver associates between Tx and Rx interrupt causes and the EICR register by setting the
   IVAR[n] registers
 • Program the SRRCTL[n].RDMTS per receive queue if software uses the Receive Descriptor Minimum
   Threshold Interrupt (RDMTI).
 • All interrupts should be set to zero — no auto clear in the EIAC register. Following an interrupt
   software can read the EICR register to check for the interrupt causes.
 • Set the auto mask in the EIAM register according to the preferred mode of operation.
 • Set the interrupt throttling in the EITR[n] and GPIE according to the preferred mode of operation.
 • The software enable the required interrupt causes by setting the EIMS register.

#### 4.6.6.2 Operating with MSI-X

 • The operating system/BIOS sets hardware to MSI-X mode and programs the MSI-X table as part of
   the device enumeration procedure.
 • The software driver associates between interrupt causes and MSI-X vectors and the throttling
   timers EITR[n] by programming the IVAR[n] and IVAR_MISC registers.
 • Program the SRRCTL[n].RDMTS (per receive queue) if software uses the receive descriptor
   minimum threshold interrupt.
 • The EIAC[n] registers should be set to auto clear for transmit and receive interrupt causes (for best
   performance). The EIAC bits that control the other and TCP timer interrupt causes should be set to
   0b — no auto clear.
 • Set auto mask in the EIAM, EIAM[n] registers according to the preferred mode of operation.
 • Set the interrupt throttling in the EITR[n] and GPIE registers according to the preferred mode of
   operation.
 • Software clears EICR by writing all ones to clear old interrupt causes.
 • Software enables the required interrupt causes by setting the EIMS[n] registers.

### 4.6.7 Receive Initialization

Initialize the following register tables before receive and transmit is enabled:
 • Set CTRL_EXT.Extended_VLAN bit if needed
 • Receive Address (RAL[n] and RAH[n]) for used addresses and Receive Address High —
   RAH[n].VAL=0b for unused addresses
 • Unicast Table Array — PFUTA[n]
 • VLAN Filter Table Array — VFTA[n]
 • VLAN Pool Filter — PFVLVF[n]
 • MAC Pool Select Array — MPSAR[n]

333369-009                                                                                             159
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   Initialization

 • VLAN Pool Filter Bitmap — PFVLVFB[n].
Program the Receive Address register(s) (RAL[n], RAH[n]) per the station address. This can come from
the NVM or from any other means (for example, it could be stored anywhere in the NVM or even in the
platform PROM for a LOM design).
Set up the Multicast Table Array — MTA registers. Assuming the entire table was zeroed by the last
reset, only the desired multicast addresses should be permitted (by writing 0x1 to the corresponding bit
location). Set the MCSTCTRL.MFE bit if multicast filtering is required.
Set up the VLAN Filter Table Array — VFTA if VLAN support is required. Assuming the entire table was
zeroed by the last reset, only the desired VLAN addresses should be permitted (by writing 0x1 to the
corresponding bit location). Set the VLNCTRL.VFE bit if VLAN filtering is required.
Initialize the flexible filters 0…7 — Flexible Host Filter Table (FHFT_FILTER) registers.
After all memories in the filter units previously indicated are initialized, enable ECC reporting by setting
the RXFECCERR0.ECCFLT_EN bit.
Program the different Rx filters and Rx offloads via registers FCTRL, VLNCTRL, MCSTCTRL, RXCSUM,
RQTC, RFCTL, MPSAR, RSSRK, RETA, SDPQF, FTQF, SYNQF, ETQF, ETQS, RDRXCTL, RSCDBU.
Note:     As NFS detection is not supported, the RFCTL.NFSW_DIS and RFCTL.NFSR_DIS bits should be
          set to 1b.
Program RXPBSIZE, MRQC, PFQDE, RTRUP2TC, MFLCN.RPFCE, MFLCN.RPFCM, and MFLCN.RFCE
according to the DCB and virtualization modes. Refer to Section 4.6.11.3.
Enable receive jumbo frames by setting HLREG0.JUMBOEN in the following case:
1. Jumbo packets are expected. Set MAXFRS.MFS to the expected maximum packet size.
Enable receive coalescing if required as described in Section 4.6.7.2.

#### 4.6.7.1 Receive Queues Enable

The following should be done for each receive queue:
1. Allocate a region of memory for the receive descriptor list.
2. Receive buffers of appropriate size should be allocated and pointers to these buffers should be
   stored in the descriptor ring.
3. Program the descriptor base address with the address of the region (registers RDBAH, RDBAL).
4. Set the length register to the size of the descriptor ring (register RDLEN).
5. Program SRRCTL associated with this queue according to the size of the buffers and the required
   header control.
6. Set RXDCTL[n].RLPML field enabled by the RXDCTL[n].RLPML_EN limiting the maximum Rx packet
   size. This setting is optional enabling the software to use smaller buffers than the size defined by
   the SRRCTL[n].BSIZEPACKET. Software may not use smaller buffers than defined by the SRRCTL[n]
   on Rx queues that enables RSC.
7. If header split is required for this queue, program the appropriate PSRTYPE for the appropriate
   headers.
8. Program RSC mode for the queue via RSCCTL register.
9. Program RXDCTL with appropriate values including the queue Enable bit. Note that packets directed
   to a disabled queue are dropped.

160                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

10. Poll the RXDCTL register until the Enable bit is set. The tail should not be bumped before this bit
    was read as 1b.
11. Bump the tail pointer (RDT) to enable descriptors fetching by setting it to the ring length minus
    one.
Enable the receive path by setting RXCTRL.RXEN. This should be done only after all other settings are
done. If software uses the receive descriptor minimum threshold interrupt, that value should be set.

4.6.7.1.1               Dynamic Enabling and Disabling of Receive Queues

Receive queues can be enabled or disabled dynamically using the following procedure.
Enabling:
Follow the per-queue initialization described in the previous section.
Disabling:
1. Disable the routing of packets to this queue by re-configuring the Rx filters.
2. If RSC is enabled on the specific queue and VLAN strip is enabled as well, wait two ITR expiration
   times (ensure all open RSCs completed).
3. All FCoE DDP flows related to this queue must be invalidated by the software device driver prior to
   disabling the queue.
4. Disable the queue by clearing the RXDCTL.ENABLE bit. The X550 stops fetching and writing back
   descriptors from this queue. Any further packet that is directed to this queue is dropped. If a packet
   is being processed, the X550 completes the current buffer write. If the packet spreads over more
   than one data buffer, all subsequent buffers are not written.
5. The X550 clears the RXDCTL.ENABLE bit only after all pending memory accesses to the descriptor
   ring are done. The driver should poll this bit before releasing the memory allocated to this queue.
6. Once the RXDCTL.ENABLE bit is cleared the driver should wait an additional amount of time
   (~100 s) before releasing the memory allocated to this queue.
The Rx path can be disabled only after all the receive queues are disabled.
Note:        As there could be additional packets in the receive packet buffer targeted to the disabled
             queue and the arbitration could be such that it would take a long time to drain these packets,
             if software re-enables a queue before all packets to that queue were drained, the enabled
             queue could potentially get packets directed to the old configuration of the queue. For
             example, VM goes down and a different VM gets the queue. The software device driver should
             delay the re-enablement of the queue until it is guaranteed there are no more packets
             directed to this queue in the packet buffer.

#### 4.6.7.2 RSC Enablement

RSC enablement as well as RSC parameter settings are assumed as static. It should be enabled prior
receiving and can be disabled only after the relevant Rx queue(s) are disabled.

4.6.7.2.1               RSC Global Setting

 • Enable global CRC stripping via the HLREG0 register (hardware default setting).
 • Software device driver should set the RDRXCTL.RSCACKC bit that forces RSC completion on any
   change of the ACK bit in the Rx packet relative to the RSC context.

333369-009                                                                                              161
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                   Initialization

 • The SRRCTL[n].BSIZEHEADER (header buffer size) bit must be larger than the packet header (even
   if header split is not enabled). A minimum size of 128 bytes for the header buffer addresses this
   requirement.

4.6.7.2.2             RSC per Queue Setting

 • Enable RSC and configure the maximum allowed descriptors per RSC by setting the MAXDESC and
   RSCEN fields in the RSCCTL[n] register.
 • Use a non-legacy descriptor type by setting the SRRCTL[n].DESCTYPE bit to non-zero values.
 • TCP header recognition: the PSR_TYPE4 bit in the PSRTYPE[n] registers should be set.
 • The SRRCTL[n].BSIZEPACKET (packet buffer size) must be 2 KB at minimum.
 • Interrupt setting:
      — Interrupt moderation must be enabled by setting the EITR[n].ITR_INTERVAL bit to a value
        greater than zero. The ITR_INTERVAL bit must be larger than the RSC Delay field described
        later. Note that if the CNT_WDIS bit is cleared (write enable), the ITR_COUNTER bit should be
        set to 0b.
      — The RSC_DELAY field in the GPIE register should be set to the expected system latency
        descriptor write-back cycles. 4 to 8 s should be sufficient in most cases. If software sees cases
        where RSC did not complete as expected (following EITR interrupt assertion), the RSC_DELAY
        field might need to be increased.
      — Map the relevant Rx queues to an interrupt by setting the relevant IVAR registers.

#### 4.6.7.3 Flow Director Initialization

Flow Director initialization is described in Section 7.1.3.6.11.

### 4.6.8 Transmit Initialization

 • Program the HLREG0 register according to the MAC behavior needed.
 • Program the TCP segmentation parameters via registers DMATXCTL (while keeping the TE bit
   cleared), DTXTCPFLGL, DTXTCPFLGH, and TPH parameters via TPH_TXCTRL.
 • Refer to the IPG description in Section 3.7.5 for more details.
 • Set RTTDCS.ARBDIS to 1.
 • Program the DTXMXSZRQ, TXPBSIZE, TXPBTHRESH, MTQC, and MNGTXMAP registers according to
   the DCB and virtualization modes. Refer to Section 4.6.11.3.
 • Clear RTTDCS.ARBDIS to 0.
 • Legacy drivers that uses queue zero and assumes it is enabled by default, should at this stage, set
   queue zero parameters as described below.
 • Enable the transmit path by setting the DMATXCTL.TE bit.

162                                                                                                  333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

#### 4.6.8.1 Transmit Queues Enable

The following steps should be done once for each transmit queue:
1. Allocate a region of memory for the transmit descriptor list.
2. Program the descriptor base address with the address of the region (TDBAL and TDBAH).
3. Set the length register to the size of the descriptor ring (TDLEN).
4. If needed, set TDWBAL/TWDBAH to enable head write back.
5. Program the TXDCTL register with the desired Tx descriptor write-back policy (see the
   recommended values in the register description).
6. Enable the queue using the TXDCTL.ENABLE bit. Poll the TXDCTL register until the ENABLE bit is
   set.
Note:        Queue 0 is enabled by default when the DMATXCTL.TE bit is set. If transmit is already enabled
             (DMATXCTL.TE bit is set), this queue should be disabled (clear TXDCTL.ENABLE bit) before
             changing the basic queue parameters (TDBAL, TDBAH, TDLEN, TDWBAL/TWDBAH).
Note:        The tail register of the queue (TDT) should not be bumped until the queue is enabled.

4.6.8.1.1               Dynamic Enabling and Disabling of Transmit Queues

Transmit queues can be enabled or disabled dynamically given the following procedure is followed.
Enabling:
Follow the per-queue initialization described in the previous section.
Disabling:
1. Stop storing packets for transmission in this queue.
2. The completion of the last transmit descriptor must be visible to software to guarantee that packets
   are not lost in step 5 (Section 4.6.8). Therefore, its RS bit must be set or WTHRESH must be
   greater than zero. If none of the previous conditions are met, software should add a null Tx data
   descriptor with an active RS bit.
3. Wait until the software head of the queue (TDH) equals the software tail (TDT) indicating the queue
   is empty.
4. Wait until all descriptors are written back (polling the DD bit in ring or polling the Head_WB
   content). It might be required to flush the transmit queue by setting the TXDCTL[n].SWFLSH bit if
   the RS bit in the last fetched descriptor is not set or if WTHRESH is greater than zero.
5. Disable the queue by clearing TXDCTL.ENABLE.
6. Any packets waiting for transmission in the packet buffer would still be sent at a later time.
The transmit path can be disabled only after all transmit queues are disabled.

333369-009                                                                                             163
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

### 4.6.9 FCoE Initialization Flow

Ordering between the following steps is not critical as long as it is done before transmit and receive
starts.
1. The FCoE DDP context table should be initialized clearing the FCBUFF.VALID bit and the
   FCFLT.VALID bit of all contexts.
2. EType Queue Filter — ETQF[n]: Select a filter by setting the FCOE bit. The ETYPE field should be set
   to 0x8906 (FCoE Ethernet Type).
3. EType Queue Select — ETQS[n]: Each ETQF filter is associated to a queue select register. The ETQS
   registers can be used to direct the FCoE traffic to specific receive queues. Up to one queue per
   Traffic Class (TC) as programmed in the ETQF.
4. Multiple receive queues can be enabled by setting the FCRECTL.ENA bit and programming the
   FCRETA[n] registers.
5. Set the RDRXCTL.FCOE_WRFIX bit that forces a DDP write exchange context closure after receiving
   the last packet in a sequence with an active Sequence Initiative bit in the F_CTL field.
6. Follow the rules described in Section 7.11.2.1 and Section 7.11.3.1 for Tx and Rx cross-
   functionality requirements. These sections include requirements on Ethernet CRC and padding
   handling, legacy Rx buffers, etc.

### 4.6.10 Virtualization Initialization Flow

#### 4.6.10.1 VMDq Mode

4.6.10.1.1           Global Filtering and Offload Capabilities

 • Select one of the VMDQ pooling and queuing methods
      — Pool Selection can be based on MAC/VLAN, and optionally E-tag. The filtering mode is defined
        using the PFVTCTL.POOLING_MODE field.
 • Queue in poll can be based either on DCB or RSS. Potential values for MRQC.MRQE to set VMDq
   modes are 1000b to 1111b.
 • DCB should be initiated as described in Section 4.6.11. In RSS mode, the RSS key (VFRSSRK) and
   redirection table (VFRETA) of the pool should be programmed. The usage of DCB can be controlled
   per pool.
 • Configure the PFVTCTL register to define the default pool.
 • Enable replication via the PFVTCTL.RPL_EN bit.
 • If needed, enable padding of small packets via the HLREG0.TXPADEN bit.
 • The MPSAR registers are used to associate Ethernet MAC Addresses to pools. Using the MPSAR
   registers, software must reprogram RAL[0] and RAH[0] by their values (software could read these
   registers and then write them back with the same content).

164                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

4.6.10.1.2             Mirroring Rules

For each mirroring rule to be activated:
 • Set the type of traffic to be mirrored in the PFMRCTL[n] register. Only one type of traffic can be
   selected in each rule.
 • Set the mirror pool by setting the PFMRCTL[n].MP bit.
 • For pool mirroring, set the PFMRVM[n] register with the pools to be mirrored.
 • For VLAN mirroring, set the PFMRVLAN[n] register with the indexes from the PFVLVF registers of
   the VLANs to be mirrored.

4.6.10.1.3             Security Features

For each pool, the driver might activate the MAC, VLAN and EtherType anti-spoof features via the
relevant bit in the PFVFSPOOF.MACAS, PFVFSPOOF.VLANAS, PFVFSPOOF.ETHERTYPEAS, and
PFVFSPOOF.ETHERTYPELB fields, respectively.
In addition, stripping and hiding of VLAN and external tag (E-tag) may also be requested via the
PFQDE.HIDE_VLAN and PFQDE.STRIP_TAG flags, respectively.

4.6.10.1.4             Per-Pool Settings

As soon as a pool of queues is associated to a VM, software should set the following parameters:
 • Associate the unicast Ethernet MAC Address of the VM by enabling the pool in the MPSAR registers.
 • If all the Ethernet MAC Addresses are used, the Unicast Hash Table (PFUTA) can be used. Pools
   servicing VMs whose address is in the hash table should be declared as so by setting the
   PFVML2FLT.ROPE bit. Packets received according to this method didn’t pass perfect filtering and are
   indicated as such.
 • Enable the pool in all RAH/RAL registers representing the multicast Ethernet MAC Addresses this VM
   belongs to.
 • If all the Ethernet MAC Addresses are used, the Multicast Hash Table (MTA) can be used. Pools
   servicing VMs using multicast addresses in the hash table should be declared as so by setting the
   PFVML2FLT.ROMPE bit. Packets received according to this method did not pass perfect filtering and
   are indicated as such.
 • Define whether this VM should get all multicast/broadcast packets in the same VLAN via
   PFVML2FLT.MPE and PFVML2FLT.BAM, and whether it should accept un-tagged packets via
   PFVML2FLT.AUPE.
 • Enable the pool in each of the PFVLVF and PFVLVFB registers this VM belongs to.
 • A VM might be set to receive it’s own traffic in case the source and the destination are in the same
   pool via the PFVMTXSW.LLE bit.
 • Whether VLAN header and CRC should be stripped from the packet. Note that even if the CRC is
   kept, it might not match the actual content of the forwarded packet, because of other offloading
   applications such as VLAN strip.
     — A striped VLAN may be also hidden from the VM.
 • Set which header split is required via the PSRTYPE register.

333369-009                                                                                              165
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    Initialization

 • In RSS mode, define if the pool uses RSS via the proper MRQC.MRQE mode.
      — Enable the Pool in the PFVFRE register to allow Rx Filtering
      — To Enable Multiple Tx queues, Set the MTQC as described in Section 7.2.1.2.1
      — Enable the Pool in the PFVFTE register to allow Tx Filtering
 • Enable Rx and Tx queues as described in Section 4.6.7 and Section 4.6.8.
 • For each Rx queue a drop/no drop flag can be set in SRRCTL.DROP_EN and via the PFQDE register,
   controlling the behavior in cases no receive buffers are available in the queue to receive packets.
   The usual behavior is to allow a drop to avoid head of line blocking. Setting the PFQDE (per queue)
   is done by using the QUEUE_INDEX field in the PFQDE register.

#### 4.6.10.2 IOV Initialization

4.6.10.2.1            PF Driver Initialization

The PF driver is responsible for the link setup and handling of all the filtering and offload capabilities for
all the VFs as described in Section 4.6.10.1.1 and the security features as described in
Section 4.6.10.1.3. It should also set the bandwidth allocation per transmit queue for each VF as
described in Section 4.6.10.
Note:      Link setup might include the authentication process (802.1X or other) and setup of the DCB
           parameters.
After all the common parameters are set, the PF driver should set all the VFMailbox[n].RSTD bits by
setting the CTRL_EXT.PFRSTD bit.
PF enables VF traffic via the PFVFTE and PFVFRE registers after all VF parameters are set as defined in
Section 4.6.10.1.4.
Note:      If the operating system changes the NumVF setting in the PCIe SR-IOV Num VFs register
           after the device was active, it is required to initiate a PF software reset following this change.

4.6.10.2.1.1           VF Specific Reset Coordination

After the PF driver receives an indication of a VF FLR via the PFVFLREC register, it should enable the
receive and transmit for the VF only once the device is programmed with the right parameters as
defined in Section 4.6.10.1.4. The receive filtering is enabled using the PFVFRE register and the
transmit filtering is enabled via the PFVFTE register.
Note:      The filtering and offloads setup might be based on a central IT settings or on requests from
           the VF drivers.

4.6.10.2.2            VF Driver Initialization

At initialization, after the PF indicated that the global initialization was done via the VFMailbox.RSTD bit,
the VF driver should communicate with the PF, either via the mailbox or via other software mechanisms
to assure that the right parameters of the VF are programmed as described in Section 4.6.10.1.4. The
PF driver might then send an acknowledge message with the actual setup done according to the VF
request and the IT policy.
The VF driver should then setup the interrupts and the queues as described in Section 4.6.6,
Section 4.6.7, and Section 4.6.8.

166                                                                                                   333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

4.6.10.2.3             Full Reset Coordination

A mechanism is provided to synchronize reset procedures between the PF and the VFs. It is provided
specifically for PF software reset but can be used in other reset cases as described later in this section.
The procedure is as follows:
One of the following reset cases takes place:
 • LAN Power Good
 • PCIe reset (PE_RST_N and in-band)
 • D3hot --> D0
 • FLR
 • Software reset by the PF
The X550 sets the RSTI bits in all VFMailbox registers. Once the reset completes, each VF might read its
VFMailbox register to identify a reset in progress.
Once the PF completes configuring the device, it clears the CTRL_EXT.PFRSTD bit. As a result, the X550
clears the RSTI bits in all VFMailbox registers and sets the Reset Done (RSTD) bits are set in all
VFMailbox registers.
Until a RSTD condition is detected, the VFs should only access the VFMailbox register and should not
attempt to activate the interrupt mechanism or the transmit and receive process.

### 4.6.11 DCB Configuration

After power-up or device reset, DCB and any type of FC are disabled by default, and a unique TC and
packet buffer (such as PB0) is used. In this mode, the host might exchange information via DCX
protocol to determine the number of TCs to be configured. Before setting the device to multiple TCs, it
should be reset (software reset).
The registers concerned with setting the number of TCs are: RXPBSIZE[0-7], TXPBSIZE[0-7],
TXPBTHRESH, MRQC, MTQC, and RTRUP2TC registers as well as the following bits RTRPCS.RAC,
RTTDCS.TDPAC, RTTDCS.VMPAC and RTTPCS.TPPAC.
They cannot be modified on the fly, but only after device reset. Packet buffers with a non-null size must
be allocated from PB0 and up.
Rate parameters and bandwidth allocation to VMs can be modified on the fly without disturbing traffic
flows.

#### 4.6.11.1 CPU Latency Considerations

When the CPU detects an idle period of some length, it enters a low-power sleep state. When traffic
arrives from the network, it takes time for the CPU to wake and respond (such as to snoop). During that
period, Rx packets are not posted to system memory.
If the entry time-to-sleep state is too short, the CPU might be getting in and out of its sleep state in
between packets, therefore impacting latency and throughput. 100 s is defined as a safe margin for
entry time to avoid such effects.

333369-009                                                                                              167
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

Each time the CPU is in low power, received packets need to be stored (or dropped) in the X550 for the
duration of the exit time. Given 64 KB Rx packet buffers per TC in the X550, (i.e. assuming typically 4
TCs per port) PFC does not spread (or the packet is not dropped) provided the CPU exits its low power
state within 50 s.

#### 4.6.11.2 Link Speed Change Procedure

Each time the link status or speed is changed, hardware automatically updates the rates that were
loaded by software relatively to the new link speed. This means that if a rate limiter was set by software
to 500 Mb/s for a 10 GbE link speed, it is changed by hardware to 50 Mb/s if the link speed has changed
to 1 GbE.
Since rates must be considered as absolute rate limitations (expressed in Mb/s, regardless of the link
speed), in such cases software is responsible to either clear all the rate-limiters and/or re-load each
rate with the correct value relatively to the new link speed. In the previous example, the new rate value
to be loaded by software must be multiplied by 10 to maintain the rate limitation to 500 Mb/s.

#### 4.6.11.3 Initial Configuration Flow

Only the following configuration modes are allowed.

4.6.11.3.1           General Case: DCB-On, VT-On

1. Configure packet buffers, queues, and traffic mapping:
      • 8 TCs mode — Packet buffer size and threshold, typically RXPBSIZE[0-7].SIZE = 0x30, 0x28, or
        0x20, depending on the size of the flow director table. Refer to rules in Section 3.7.4.3.5 for a
        non-symmetrical sizing.
            TXPBSIZE[0-7].SIZE = 0x14
        but non-symmetrical sizing is also allowed (see rules in the TXPBSIZE register)
            TXPBTHRESH.THRESH[0-7] = TXPBSIZE[0-7].SIZE — Max expected Tx packet length in
            this TC.
      • 4 TCs mode — Packet buffer size and threshold, typically RXPBSIZE[0-3].SIZE = 0x60, 0x50, or
        0x40, depending on the size of the flow director table. Refer to rules in Section 3.7.4.3.5 for a
        non-symmetrical sizing.
            RXPBSIZE[[4-7].SIZE = 0x0
            TXPBSIZE[0-3].SIZE = 0x28
            TXPBSIZE[4-7].SIZE = 0x0
        but non-symmetrical sizing among TCs[0-3] is also allowed (see rules in TXPBSIZE register)
            TXPBTHRESH.THRESH[0-3] = TXPBSIZE[0-3].SIZE — Maximum expected Tx packet length
            in this TC.
            TXPBTHRESH.THRESH[4-7] = 0x0
      • Multiple Receive and Transmit Queue Control (MRQC and MTQC)
         — Set MRQC.MRQE to 1xxxb, with the 3 LS bits set according to the number of VFs, TCs, and
           RSS mode as listed in the MRQC register section.
         — Set both DCB_ENA and VT_ENA bits in the MTQC register.

168                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

         — Set MTQC.NUM_TC_OR_Q according to the number of TCs/VFs enabled as described in the
           MTQC register section.
      • Set the PFVTCTL.VT_ENA bit (as the MRQC.VT_ENA bit) Queue Drop Enable (PFQDE): In
        SR-IOV the PFQDE bit should be set to 1b in the PFQDE register for all queues. In VMDq mode,
        the PFQDE bit should be set to 0b for all queues.
      • Split Receive Control (SRRCTL[0-127]): DROP_EN = 1b — drop policy for all the queues, to
        avoid crosstalk between VMs
      • Rx User Priority (UP)-to-TC (RTRUP2TC)
      • Tx UP-to-TC (RTTUP2TC)
      • DMA Tx TCP Max Allow Size Requests (DTXMXSZRQ) — set MAX_BYTE_NUM_REQ = 0x010 =

    4 KB.

      • Operate the SEC-TX buffer in DCB mode by setting SECTXMINIFG.MRKRINSERT to 0x640 or to
        0x1A0 depending if 9.5 KB Jumbo frames are supported or not, respectively.
2. Enable PFC and disable legacy flow control:
      • Enables transmit priority flow control via: FCCFG.TFCE = 10b, and for the TC(s) where no drop
        behavior is required by FCRTH.FCEN = 1b and appropriate setting in corresponding FCRTL.RTL
        and FCRTH.RTH.
        Note:      FCRTL.RTL must be set to a non zero value when FCRTH.FCEN = 1b.
      • Enables receive priority flow control via MFLCN.RPFCM = 1b and MFLCN.RPFCE set for the UP(s)
        where no drop behavior is required.
      • Disable receive legacy flow control via MFLCN.RFCE = 0b.
      • Refer to Section 8.2.2.3 for other registers concerned with flow control
3. Configure arbiters, per TC[0-1]:
      • Tx Descriptor Plane T1 Config (RTTDT1C) per queue, via setting RTTDQSEL first
      • Tx Descriptor Plane T2 Config (RTTDT2C[0-7])
      • Tx Packet Plane T2 Config (RTTPT2C[0-7])
      • Rx Packet Plane T4 Config (RTRPT4C[0-7])
4. Enable TC and VM arbitration layers:
      • Tx Descriptor Plane Control and Status (RTTDCS), bits: TDPAC = 1b, VMPAC = 1, TDRM = 1b,
        BDPM = 0b, BPBFSM = 0b.
      • Tx Packet Plane Control and Status (RTTPCS): TPPAC = 1b, TPRM = 1b, ARBD = 0x004,
        BYPASS_DCB_ARB = 0
      • Rx Packet Plane Control and Status (RTRPCS): RAC = 1b, RRM = 1b

333369-009                                                                                         169
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

4.6.11.3.2           DCB-On, VT-Off

Set the configuration bits as specified in Section 4.6.11.3.1 with the following exceptions:
 • Configure packet buffers, queues, and traffic mapping:
      — MRQC and MTQC
          • Set MRQE to 0xxxb, with the 3 LS bits set according to the number of TCs, and RSS mode
          • Set the DCB_ENA bit and clear the VT_ENA bit in the MTQC register.
          • Set MTQC.NUM_TC_OR_Q according to the number of TCs enabled
      — Clear the PFVTCTL.VT_ENA bit (as the MRQC.VT_ENA bit)
 • Allow no-drop policy in Rx:
      — PFQDE: The PFQDE bit should be set to 0b in the PFQDE register for all queues enabling per
        queue policy by the SRRCTL[n] setting.
      — Split Receive Control (SRRCTL[0-127]): The DROP_EN bit should be set (per receive queue)
        according to the required drop / no-drop policy of the TC of the queue.
 • Disable VM arbitration layer:
      — Clear the RTTDT1C register, per each queue, via setting RTTDQSEL first
      — RTTDCS.VMPAC = 0b

4.6.11.3.3           DCB-Off, VT-On

Set the configuration bits as specified in Section 4.6.11.3.1 with the following exceptions:
 • Disable multiple packet buffers and allocate all queues to PB0:
      — RXPBSIZE[0].SIZE = 0x180, RXPBSIZE[1-7].SIZE = 0x0
      — TXPBSIZE[0].SIZE = 0xA0, TXPBSIZE[1-7].SIZE = 0x0
      — TXPBTHRESH.THRESH[0] = 0xA0 — Max expected Tx packet length in this TC
        TXPBTHRESH.THRESH[1-7] = 0x0
      — MRQC and MTQC
          • Set MRQE to 1xxxb, with the 3 LS bits set according to the number of VFs and RSS mode
          • Clear DCB_ENA bit and set the VT_ENA bit in the MTQC register.
          • Set MTQC.NUM_TC_OR_Q according to the number of VFs enabled
      — Set the PFVTCTL.VT_ENA bit (as the MRQC.VT_ENA bit) Rx UP-to-TC (RTRUP2TC), UPnMAP=0,
        n=0,...,7
      — Tx UP-to-TC (RTTUP2TC), UPnMAP=0, n=0,...,7
      — DMA Tx TCP Max Allow Size Requests (DTXMXSZRQ) — set MAX_BYTE_NUM_REQ = 0xFFF =
        1 MB
      — Operate the SEC-TX buffer in non-DCB mode by setting SECTXMINIFG.MRKRINSERT to 0x10
 • Disable PFC and enabled legacy flow control:
      — Disable receive priority flow control via: MFLCN.RPFCM = 0b and MFLCN.RPFCE[7:0] = 0x00
      — Enable transmit legacy flow control via: FCCFG.TFCE = 01b

170                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

     — Enable receive legacy flow control via: MFLCN.RFCE = 1b
 • Configure VM arbiters only, reset others:
     — Tx Descriptor Plane T1 Config (RTTDT1C) per pool, via setting RTTDQSEL first for the pool
       index. Clear RTTDT1C for other queues.
     — Clear RTTDT2C[0-7] registers
     — Clear RTTPT2C[0-7] registers
     — Clear RTRPT4C[0-7] registers
 • Disable TC arbitrations while enabling the PB Free Space Monitor:
     — Tx Descriptor Plane Control and Status (RTTDCS), bits: TDPAC = 0b, VMPAC = 1b, TDRM = 0b,
       BDPM = 1b, BPBFSM = 0b
     — Tx Packet Plane Control and Status (RTTPCS): TPPAC = 0b, TPRM = 0b, ARBD = 0x24,
       BYPASS_DCB_ARB = 1.
     — Rx Packet Plane Control and Status (RTRPCS): RAC = 0b, RRM = 0b

4.6.11.3.4             DCB-Off, VT-Off

Set the configuration bits as specified in Section 4.6.11.3.1 with the following exceptions:
 • Disable multiple packet buffers and allocate all queues and traffic to PB0:
     — RXPBSIZE[0].SIZE = 0x180, RXPBSIZE[1-7].SIZE = 0x0
     — TXPBSIZE[0].SIZE = 0xA0, TXPBSIZE[1-7].SIZE = 0x0
     — TXPBTHRESH.THRESH[0] = 0xA0 — Max expected Tx packet length in this TC
       TXPBTHRESH.THRESH[1-7] = 0x0
     — MRQC and MTQC
          • Set MRQE to 0xxxb, with the 3 LS bits set according to the RSS mode
          • Clear both DCB_ENA and VT_ENA bits in the MTQC register.
          • Set MTQC.NUM_TC_OR_Q to 00b.
     — Clear the PFVTCTL.VT_ENA bit (as the MRQC.VT_ENA bit) Rx UP-to-TC (RTRUP2TC),
       UPnMAP=0, n=0,...,7
     — Tx UP-to-TC (RTTUP2TC), UPnMAP=0, n=0,...,7
     — DMA Tx TCP Max Allow Size Requests (DTXMXSZRQ) — set MAX_BYTE_NUM_REQ = 0xFFF =
       1 MB
     — Operate the SEC-TX buffer in non-DCB mode by setting SECTXMINIFG.MRKRINSERT to 0x10
 • Allow no-drop policy in Rx:
     — PFQDE: The PFQDE bit should be set to 0b in the PFQDE register for all queues enabling per
       queue policy by the SRRCTL[n] setting.
     — Split Receive Control (SRRCTL[0-127]): The DROP_EN bit should be set (per receive queue)
       according to the required drop / no-drop policy of the TC of the queue.

333369-009                                                                                          171
                                 Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                    Initialization

 • Disable PFC and enable legacy flow control:
       — Disable receive priority flow control via: MFLCN.RPFCM = 0b and MFLCN.RPFCE[7:0] = 0x00
       — Enable receive legacy flow control via: MFLCN.RFCE = 1b
       — Enable transmit legacy flow control via: FCCFG.TFCE = 01b
 • Reset all arbiters:
       — Clear the RTTDT1C register, per each queue, via setting RTTDQSEL first
       — Clear RTTDT2C[0-7] registers
       — Clear RTTPT2C[0-7] registers
       — Clear RTRPT4C[0-7] registers
 • Disable TC and VM arbitration layers:
       — Tx Descriptor Plane Control and Status (RTTDCS), bits: TDPAC = 0b, VMPAC = 0b, TDRM = 0b,
         BDPM = 1b, BPBFSM = 1b
       — Tx Packet Plane Control and Status (RTTPCS): TPPAC = 0b, TPRM = 0b, ARBD = 0x224
       — Rx Packet Plane Control and Status (RTRPCS): RAC = 0b, RRM = 0b

#### 4.6.11.4 Configuration Rules

4.6.11.4.1             TC Parameters

Traffic Class (TC):
      Per 802.1p priority #7 is the highest priority.
      A specific TC can be configured to receive or transmit a specific amount of the total bandwidth
      available per port.
      Bandwidth allocation is defined as a fraction of the total available bandwidth, which can be less than
      the full Ethernet link bandwidth (if it is bounded by the PCIe bandwidth or by flow control).
      Low latency TC should be configured to use the highest priority TC possible (TC 6, 7); the lowest
      latency is achieved using TC7.

Bandwidth Groups (BWGs):
      BWGs are used to represent different traffic types. A traffic type (such as storage, IPC LAN, or
      manageability) can have more than one TC. For example, one for control traffic and one for the raw
      data. By grouping these two TCs to a BWG, the end user can allocate bandwidth to the storage
      traffic so that unused bandwidth by the control could be used by the data and vise versa. This BWG
      concept supports the converged fabric as each traffic type, that’s used to run on a different fabric,
      can be configured as a BWG and gets its resources as if it was on a different fabric.
      1. To configure DCB not to share bandwidth between TCs, each TC should be configured as a
         separate BWG.
      2. There are no limits on the TCs that can be bundled together as a BWG. All TCs can be configured
         as a single BWG.
      3. BWG numbers should be sequential starting from zero until the total number of BWG minus one.
      4. BWG numbers do not imply priority; priority is only set according to TCs.

172                                                                                                   333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

Refill Credits:
    Refill credits regulate the bandwidth allocated to BWGs and TCs. The ratio between the credits of
    the BWG’s represents the relative bandwidth percentage allocated to each BWG. The ratio between
    the credits of the TCs represents the relative bandwidth percentage allocated to each TC within a
    BWG.
    Credits are configured and calculated using 64-byte granularity.
     1. In any case, the number of refill credits assigned per TC should be as small as possible but still
        larger than the maximum frame size used and larger than 1.5 KB. Using a lower refill value
        causes more refill cycles before a packet can be sent. These extra cycles unnecessarily increase
        the latency.
     2. Refill credits ratio between TCs should be equal to the desired ratio of bandwidth allocation
        between the different TCs. Applying rule #1, means bandwidth shares are sorted from the
        smaller to the bigger, and just one maximum sized frame is allocated to the smallest.
     3. The ratio between the refill credits of any two TCs should not be greater than 100.
     4. Exception to rule #2 — TCs that require low latency should be configured so that they are under
        subscribed. For example, the credit refill value should provide these TCs somewhat more
        bandwidth than what they actually need. Low latency TCs should always have credits so they can
        be next in line for WSP arbitration.
        This exception causes the low latency TC to always have maximum credits (as it starts with
        maximum credits and on average cycle uses less than the refill credits).
    The end point that is sending/receiving packets of 127 bytes eventually get double the bandwidth it
    was configured to, as all credits calculated by rounding the values down to the next 64 byte-aligned
    value.

Max Credit Limit:
    The maximum credit limit value establishes a limit for the number of credits that a TC or BWG can
    own at any given time. This value prevents stacking up stale credits that can be added up over a
    relatively long period of time and then used by TCs all at once, altering fairness and latency.
    Max credit limits are configured and calculated using 64-byte granularity.
     1. Maximum credit limit should be bigger than the refill credits allocated to the TC.
     2. Maximum limit should be set to be as low as possible while still meeting other rules to minimize
        the latency impact on low latency TCs.
     3. If a low latency TC generates a burst that is larger than its maximum credit limit, this TC might
        experience higher latency since the TC needs to wait for allocation of additional credits because
        it finished all its credits for this cycle. Therefore, maximum credit limit for a low latency TC must
        be set bigger than the maximum burst length of traffic expected on that TC — for all VMs at once.
        If TC7 and TC6 are for low latency traffic, it leads to:
             Max(TC7,6) >= MaxBurst(TC7,6) served with low latency

     4. An arbitration cycle can be extended when one or more TCs accumulate credits more than their
        refill values (up to their maximum credit limit). For such a case a low latency TC should be
        provided with enough credits to cover for the extended cycle duration. Since the low latency TC
        operates at maximum credits (see rule #3) its maximum credit limit should meet the following
        formula.
             {Max(TCx)/SUMi=0..7[Max(TCi)]} >= {BW(TCx)/Full BW}

        The formula applies to both the descriptor arbiter and data arbiter.

333369-009                                                                                                173
                                 Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                      Initialization

      5. To ensure bandwidth for a low priority TC (when those are allocated with most of the bandwidth)
         the maximum credit value of the low priority TC in the data arbiter needs to be high enough to
         ensure sync between the two arbiters. In the following equation the bandwidth numbers are from
         the descriptor arbiter while the maximum values are of the data arbiter.
              {Max(TCx)/SUMi=x+1..7[Max(TCi)]} >= {BW(TCx)/Full_PCIE_BW}

          Note that the previous equation is worst case and covers the assumption that all higher TCs have
          the full maximum to transmit.
      Tip:    A simplified maximum credits allocation scheme would be to find the minimum number N
              >= 2 such that rules #3 and #5 are respected, and allocate:
                  Max(TCi) = N x Refill(TCi), for i=0..7

      By maintaining the same ratios between the maximum credits and the bandwidth shares, the
      bandwidth allocation scheme is made more immune to disturbing events such as receiving priority
      pause frames with short timer values.

GSP and LSP:
      Bit TC.LSP (TC Link Strict Priority): This bit specifies that the configured TC can transmit without
      any restriction of credits. This effectively means that the TC can take up the entire link bandwidth,
      unless preempted by higher priority traffic. The Tx queues associated with a LSP TC must be set as
      strict low latency in the TXLLQ[n] registers.
      Bit TC.GSP (TC Strict Priority within Group): This bit defines whether strict priority is enabled or
      disabled for this TC within its BWG. If bit TC.GSP is set to 1b, the TC is scheduled for transmission
      using strict priority. It does not check for availability of credits in the TC. It does; however, check
      whether the BWG of this TC has credits. For example, the amount of traffic generated from this TC
      is still limited by the bandwidth allocated for the BWG.
      1. TCs with the LSP bit set should be the first to be considered by the scheduler. This implies that
         the LSP bit should be configured to the highest priority TCs. For example, starting from priority
         7 and down; the other TCs should be used for groups with bandwidth allocation. It is
         recommended to use LSP only for one TC (TC7) as the first LSP TC takes its bandwidth and there
         are no guarantees to the lower priority LSPs.
      2. The GSP bit can be set to more than one TC in a BWG, always from the highest priority TC within
         that BWG downward. For the LAN scenario, all TCs could be configured to be GSP as their
         bandwidth needs are not known.
      3. For a low latency TC where the GSP bit is set, non-null refill credits must be set for at least one
         maximum-sized frame. This ensures that even after its been quiet for a while, some BWG credits
         are left available to the GSP TC, for serving it with minimum latency (without waiting for
         replenishing). Bigger refill credits values ensure longer bursts of GSP traffic served with
         minimum latency.

4.6.11.4.2             VM Parameters

Refill Credits:
      Refill credits regulate the fraction of the TC’s bandwidth that is allocated to a VM. The ratio between
      the credits of the VMs represent the relative TC bandwidth percentage allocated to each VM.
      Credits are configured and calculated using 64-byte granularity.

174                                                                                                     333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

     1. In any case, the number of refill credits assigned per VM should be as small as possible but still
        larger than the maximum frame size used and larger than 1.5 KB. Using a lower refill value
        causes more refill cycles before a packet can be sent. These extra cycles increase the latency
        unnecessarily.
     2. The refill credits ratio between VMs should be equal to the desired ratio of bandwidth allocation
        between the different TCs. Applying rule #1, means bandwidth shares are sorted from the
        smaller to the bigger, and just one maximum sized frame is allocated to the smallest.
     3. The ratio between the refill credits of any two VMs within the TC should not be greater than 10.
    VMs that send/receive packets of 127 bytes eventually get double the bandwidth it was configured
    to as all credits are calculated by rounding the values down to the next 64 byte-aligned value.

Refill and Maximum Credits (MaxCredits) Setting Example:
This example assumes a system with only four TCs and three VMs present, along with the following
bandwidth allocation scheme. Also, note that full PCIe bandwidth is evaluated to 15 G.

    Table 4-9.         Bandwidth Share Example
                                                Bandwidth
                   TCs and VMs                                                           Note
                                                 Share%

                                 Total              40                       9.5 KB jumbo frames allowed.

                                 VM0                60
             TC0
                                 VM1                30

                                 VM2                10

                                 Total              20                             No jumbo frames.

                                 VM0                34
             TC1
                                 VM1                33

                                 VM2                33

                                                                           Low latency TC. No jumbo frames.
                                 Total              30                     Bandwidth share already increased.
                                                                                 MaxBurstTC2=120 KB
             TC2                 VM0                80

                                 VM1                10

                                 VM2                10

                                                                                  Low latency LSP TC.
                                 Total              10                             No jumbo frames.
                                                                                  MaxBurstTC3=36 KB
             TC3                 VM0                20

                                 VM1                60

                                 VM2                20

    The ratios between TC refills are driven by TC0, which was set as 152 for supporting 9.5 KB jumbo
    frames.
    The ratio between MaxCredits and Refill were taken as 17 for all the TCs, as driven by the TC2
    relation between MaxCredits and MaxBurstTC2.

333369-009                                                                                                      175
                                         Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                           Initialization

      Table 4-10. Refill and MaxCredits Settings
                                                  Refill                            MaxCredits
                  TCs and VMs
                                             (64-Byte Units)                      (64-Byte Units)

                                Total              152                                  2584

                                VM0                912
            TC0
                                VM1                456

                                VM2                152

                                Total              76                                   1292

                                VM0                25
            TC1
                                VM1                24

                                VM2                24

                                Total              114                                  1938

                                VM0                192
            TC2
                                VM1                24

                                VM2                24

                                Total              38                                   646

                                VM0                24
            TC3
                                VM1                72

                                VM2                24

4.6.11.4.3               Rate Limiters

It might be useful to setup rate limiters on Tx queues (rate-limiting VF traffic). Setting a rate-limiter on
Tx queue N to a Target Rate requires the following settings:
 • Use of advanced Tx descriptors
 • RTTQCNRM.MMW_SIZE set to the amount of back-to-back compensation to be granted to a quiet
   item.
 • RTTDQSEL.TXQ_IDX set to N.
 • Compute the Rate Factor = Link Speed / Target Rate, where Link Speed is either 10 Gb/s or

# 1 Gb/s. The fractional binary number obtained is broken down into its 2n components as follows:

         b9b8b7b6b5b4b3b2b1b0.b-1b-2b-3b-4b-5b-6b-7b-8b-9b-10b-11b-12b-13b-14
      where bn is the binary coefficient of the 2n component.
 • Set RTTQCNRC register with
      — Set RTTQCNRC[13:0] = RTTQCNRC.RF_DEC[13:0] = [b-1b-2b-3b-4b-5b-6b-7b-8b-9b-10b-11b-12
        b-13b-14]
      — RTTQCNRC[23:14] = RTTQCNRC.RF_INT[9:0] = [b9b8b7b6b5b4b3b2b1b0]
      — RTTQCNRC[31] = RTTQCNRC.RS_ENA = 1b

176                                                                                                          333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

Numerical Example:
 • Target Rate = 4 Gb/s
 • Link Speed = 10 Gb/s
    Rate Factor = 10 / 4 = 2.5 = 1x21 + 1x2-1 = 0000000010.10000000000000b
     — RTTQCNRC[13:0] = [10000000000000]
     — RTTQCNRC[23:14] = [0000000010]
     — RTTQCNRC = [1000 0000 0000 0000 1010 0000 0000 0000] = 0x8000A000

### 4.6.12 Security Initialization

After power up or device reset, security offload is disabled by default (IPsec), and the content of the SA
tables must be cleared by software.
Security offload cannot be enabled when either the security fuses are blown (set to zero), or the
ENCRYPTION_EN pin is set to 0b. In this case, IPsec is disabled and the following security-related fields
are not writable:
• SECTXCTRL.SECTX_DIS is set to 1b and read as 1b
• SECRXCTRL.SECRX_DIS is set to b1 and read as 1b
• IPSTXIDX.IPS_TX_EN is cleared to 0b and read as 0b
• IPSRXIDX.IPS_RX_EN is cleared to 0b and read as 0b
Security offload can be used when the security offload internal fuse is enabled and the ENCRYPTION_EN
pin set to 1b. In this case, the security offload can be enabled/disabled via the flows that are described
in the sections that follow.

#### 4.6.12.1 Security Enable Flow

To enable one of the security modes do the following:
1. Stop the data paths by setting the SECTXCTRL.TX_DIS and SECRXCTRL.RX_DIS bits.
2. Wait for the data paths to be emptied by hardware. Poll the SECTXSTAT.SECTX_RDY and
   SECRXSTAT.SECRX_RDY bits until they are both asserted by hardware.
3. Clear the SECTXCTRL.SECTX_DIS and SECRXCTRL.SECRX_DIS bits to enable the Tx and Rx crypto
   engines.
      • When enabling IPsec offload, set the SECTXMINIFG.MINSECIFG bits to 0x3, extending back-to-
        back gap to the security block required for its functionality.
      • When enabling IPsec, set the SECTXCTRL.STORE_FORWARD bit, since a store and forward
        IPsec buffer is required for the processing of AH packets (ICV field insertion is done at the
        beginning of the frame). Otherwise, clear this bit.
      • When enabling IPsec, write the SEC buffer almost full threshold register
        SECTXBUFFAF.FULLTHRESH with the value of 0x15.
4. Enable SA lookup:
      • For IPsec, set the IPSTXIDX.IPS_TX_EN and the IPSRXIDX.IPS_RX_EN bits.
5. Restart the data paths by clearing the SECTXCTRL.TX_DIS and SECRXCTRL.RX_DIS bits.

333369-009                                                                                              177
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                  Initialization

#### 4.6.12.2 Security Disable Flow

To disable one of the security modes do the following:
1. Stop the data paths by setting the SECTXCTRL.TX_DIS and SECRXCTRL.RX_DIS bits.
2. Wait for the data paths to be emptied by hardware. Poll the SECTXSTAT.SECTX_RDY and
   SECRXSTAT.SECRX_RDY bits until they are both asserted by hardware.
3. Disable SA lookup:
      • For IPsec, clear the IPSTXIDX.IPS_TX_EN and the IPSRXIDX.IPS_RX_EN bits.
4. Set the SECTXCTRL.SECTX_DIS and SECRXCTRL.SECRX_DIS bits to disable the Tx and Rx crypto
   engines.
      • When disabling IPsec, clear the SECTXCTRL.STORE_FORWARD bit to avoid using the IPsec
        buffer and thus reducing Tx internal latency.
      • When disabling IPsec, write the SEC buffer almost full threshold register
        SECTXBUFFAF.FULLTHRESH with the value of 0x250.
5. Restart the data paths by clearing the SECTXCTRL.TX_DIS and SECRXCTRL.RX_DIS bits.
Note:     Disabling the crypto engine reduces the X550’s power consumption.

### 4.6.13 Alternate MAC Address Support

In some systems, the MAC Address used by a port needs to be replaced with a temporary MAC Address
in a way that is transparent to the software layer. One possible usage is in blade systems, to allow a
standby blade to use the MAC Address of another blade that failed, so that the network image of the
entire blade system does not change.
To allow this mode, a management console might change the MAC Address in the NVM image. It is
important in this case to be able to keep the original MAC Address of the device as programmed at the
factory.
To support this mode, the X550 provides the Alternate Ethernet MAC Address structure in the NVM to
store the original MAC Addresses. This structure is described in Section 6.2.2.56.
In some systems, it might be advantageous to restore the original MAC Address at power on reset, to
avoid conflicts where two network controllers would have the same MAC Address.
The X550 supports replacement of the MAC Address with an alternate MAC Address via the NC-SI
interface using the BIOS CLP interface as described in the BIOS CLP document.

#### 4.6.13.1 LAN MAC Address Restore

The X550 restores the LAN MAC Addresses stored in the Alternate Ethernet MAC Address structure to
the regular LAN MAC Address location (see Section 6.2.5.3) if the following conditions are met:
1. The restore MAC Address bit in the Common Firmware Parameters NVM word is set.
2. The value in word 0x37 is not 0xFFFF.
3. The MAC Address set in the regular MAC Address location is different than the address stored in the
   Alternate Ethernet MAC Address structure.

178                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Initialization

4. The addresses stored in the Alternate Ethernet MAC Address structure are valid (not all zeros or all
   ones).
If the value at word 0x37 is valid, but the MAC Addresses in the Alternate MAC structure are not valid
(0xFFFFFFFF or all zeros) and restore MAC Address NVM bit is set, the regular MAC Address is backed
up in the Alternate MAC structure.

#### 4.6.13.2 SAN MAC Address Restore

The X550 restores the SAN MAC Addresses (word 0x28 - see Section 6.2.2.41) at power on reset by
copying the values from the Alternate SAN MAC Address structure (word 0x27; Section 6.2.2.40) to the
SAN MAC Addresses if the following conditions are met:
1. The Restore MAC Address bit in the Common Firmware Parameters NVM word is set.
2. The pointer to the SAN MAC Address structure is valid (value in word 0x28 in not 0xFFFF - see
   Section 6.2.2.41).
3. The addresses stored in the Alternate SAN MAC Address structure (word 0x27 - see Section 6.2.11)
   are valid (not all zeros or all ones).
If the value at word 0x27 is valid, but the MAC Addresses in the Alternate SAN MAC structure are not
valid (0xFFFFFFFF or all zeros), the regular SAN MAC Address (pointed by word 0x28) is backed up in
the Alternate SAN MAC structure (pointed by word 0x27).

#### 4.6.13.3 Restore Reporting

If after the power up cycle, the alternate SAN and LAN address equals to the SAN and LAN Factory MAC
Addresses (either they were restored by the internal firmware or they were originally equal), the
FWSM.FACTORY_MAC_ADDRESS_RESTORED bit is set. This bit is common to all ports.
