## 3.4 Non-Volatile Memory (NVM)

### 3.4.1 General Overview

The X550 uses a Flash device to store product configuration information. The Flash is divided into three
general regions:
 • Hardware Accessed — Loaded by the the X550 hardware after power-up, PCI reset de-assertion,
   D3 to D0 transition, or software reset. Different hardware sections in the Flash are loaded at
   different events. For more details on power-up and reset sequences, see Section 4.1 and
   Section 4.2.
 • Firmware Area — Includes firmware code and structures used by the firmware for management
   configuration in its different modes.
 • Software Accessed — This region is used by software entities such as LAN drivers, option ROM
   software and tools, PCIe bus drivers, VPD software, etc.

#### 3.4.1.1 NVM Protection

The NVM protection method implemented in the X550 relies on an “authenticate on update” concept. It
means that the protected modules are not authenticated after initialization, but prior to committing a
module update operation only. NVM protection is guaranteed by an inductive authentication chain, that
assumes an initial secured NVM image and requires that any NVM update must be secure as well. This
method mandates the following limitations and restricting working assumptions:
1. An initial ‘good’ image is loaded into the flash at the manufacturing site which is assumed to be
   safe.
     — It assumes customers (OEM and end-user) know the source of the installed components, the
       supply chain producing these components is not compromised during manufacturing, and that
       the NIC/LOM is physically protected from modification after deployment.
     — The possibility exists that unauthorized firmware may be loaded into the NVM via physical
       modification post manufacturing, as well as through supply chain vulnerabilities. However,
       firmware updates via programmatic (software) methods are enhanced to require authentication
       prior to updating NVM settings. Furthermore, host software can independently detect whether
       the firmware image has an invalid digital signature.
2. In a normal operating mode, NVM write accesses are controlled by the device (firmware) and
   cannot be performed via the memory mapped accesses, EEWR register, or bit-banging. Memory
   mapped NVM access remains available for NVM read accesses only. For simplicity and flexibility
   reasons, NVM write accesses from the host can be initiated via host interface commands
   (Section 11.8.3.3), VPD write interface, or via a BMC command, which are all handled by firmware.
   Memory BAR writes, EEWR and FLA bit-banging accesses are blocked by hardware when the NVM is
   protected.

333369-009                                                                                             95
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

3. All the supported Flash parts share the same set of op-codes as described in Section 3.4.1.2. A
   blank Flash programming mode is provided (besides the normal programming mode previously
   mentioned in item 2), where the Flash can be programmed directly without firmware involvement
   via the FLA bit-banging or Flash BAR interfaces. This mode is indicated by FLA.LOCKED = 0b.

#### 3.4.1.2 Flash Device Requirements

The X550 supports Flash devices with a sector erase size of 4 KB and an address width of 24 bits (up to

    4 MB). Note that many Flash vendors are using the term sector differently. This document uses the

term Flash sector for a logic section of 4 KB.
The X550 supports Flash devices that are either write-protected by default after power-up or not. The
X550 is responsible to remove the protection by sending the write-protection removal Op-Code to the
Flash after power up.
The following Op-Codes are supported by the X550 as they are common to all supported Flash devices:
1. Write Enable (0x06)
2. Read Status Register (0x05) - used by hardware internally.
3. Write Status Register (0x01). The written data is 0x00 to cancel the Flash default protection. Used
   by hardware internally.
4. Read Data (0x03). Burst read is supported.
5. Byte Program (0x02). To program a data byte.
6. 4 KB Sector-Erase (0x20)
7. Chip-Erase (0xC7)
8. Read JEDEC ID (0x9F)

3.4.1.2.1            Flash Identification

The Flash connected to the X550 can be identified by its JEDEC ID that can be read using the Flash Info
host interface command (Section 11.8.3.3.9). This identification is available only if a valid Flash is
installed. If the Flash is empty or with an invalid signature, software can read the JEDEC ID by applying
an RDID command (opcode 0x9F) or a Read SFDP command (opcode 0x5A) via the bit-bang interface.

### 3.4.2 Shadow RAM

The first eight 4 KB sectors of the X550’s Flash are allocated to create two 16 KB sections (section 0 and
section 1), for the configuration content. At least one of these two sections must be valid at any given
time or else the X550 is set to hardware default. Following a Power On Reset (POR), the X550 copies
the valid section of the Flash device into an internal Shadow RAM. Any further read accesses of the
software or firmware to the lower 16 KB addresses of the NVM (not through flash BAR) are directed to
the internal Shadow RAM. Modifications made to the Shadow RAM content are copied by the X550 into
the other 16 KB section of the NVM, circularly flipping the valid section between sections 0 and 1 in the
NVM.

96                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

This mechanism provides the following advantages:
1. A way to protect the image-update procedure from power down events by establishing a double-
   image policy. See Section 3.4.8.1 for a description of the double-image policy. It relies on having
   pointers to NVM modules stored in the NVM section mirrored in the internal Shadow RAM.
2. A way to ensure hardware auto-load during a PCIe reset event can be completed within PCIe timing
   constraints (100 ms), even if the Flash is busy performing an erase operation initiated prior to that
   reset event.
Figure 3-5 shows the Shadow RAM mapping and interface.

                 Flash                                              X550
                             0xFFFFFF
                                                                            0xFFFFFF -
                                                                            0x000000
                                                                      1:1
                                                                                         Flash-Mode
                                                                                           Access

                             0x008000
                             0x007FFF
              16
              KB
                 Section 1
                             0x004000
                             0x003FFF                                       0x003FFF -
              16                                              0x003FFF      0x000000
              KB
                 Section 0                                                                EEPROM-
                                                 Shadow RAM
                             0x000000
                                                              0x000000
                                                                                         Mode Access

                             Physical Byte                 Internal RAM     Logical
                             address                          address       address

Figure 3-5.     NVM Shadow RAM

#### 3.4.2.1 Shadow RAM Update Flow

Following a write access by the software device driver to update the Shadow RAM, the data should be
updated in the Flash as well. The X550 updates the Flash from the Shadow RAM when software
explicitly requests to update the Flash using the Shadow RAM Dump host interface command
(Section 11.8.3.3.8). To reduce Flash update operations, software is expected to request a dump only
once its last Shadow RAM update access completes. The X550 then copies the content of the Shadow
RAM to the non valid configuration section and makes it the valid one.

### 3.4.3 NVM Clients and Interfaces

There are different software clients that can access the NVM: driver, tools, BIOS, VPD, etc.
Table 3-21 lists the different accesses to the NVM.

333369-009                                                                                               97
                                        Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               Interconnects

Table 3-21. Clients and Access Types to the NVM
                                            Logical
                NVM Access         NVM
                                              Byte
     Client       Method          Access                   NVM Access Interface               Protection and Enforcement
                                            Address
               (Data Width)       Target
                                             Range

              Memory BAR          Flash    0x000000 -   Memory mapped read/write via      Write access is limited to a single byte,
              (parallel 32-bit)            0xFFFFFF     BARs.                             and is allowed only if hardware
                                                                                          protection is disabled (FLA.LOCKED =
                                                                                          0).

              FLA bit-banging     Flash    0x000000 -   Software accesses to Flash by     FLA interface access is available only if
              (serial 1-bit)               0xFFFFFF     toggling the SPI pins.            hardware protection is disabled
                                                                                          (FLA.LOCKED = 0).

              Host interface      Shado    0x000000 -   Access to Shadow RAM through      Requires a valid firmware image.
              Shadow RAM          w RAM    0x003FFF     the Shadow RAM Read/Write         Write protection is enforced by
              Read/Write                                command                           firmware.
              command

   Host       Host interface      Flash    0x000000 -   Software read from Flash via      Requires a valid firmware image.
 Software     Flash read                   0xFFFFFF     Flash Read command.
              command

              Host interface      Flash    0x008000 -   Software write to sector/Flash    Requires a valid firmware image.
              Flash write                  0xFFFFFF     erase                             Writes to protected areas are dropped
              command/Flash                                                               when protection (enforced by firmware)
              block erase                                                                 is enabled. Protected sector erase or a
              command                                                                     complete Flash erase requests are
                                                                                          rejected when protection (enforced by
                                                                                          firmware) is enabled.

              VPD access          Shado    0x000000 -   VPD Address and Data              Write accesses are enabled to the R/W
              (parallel 32-bit)   w RAM    0x0003FF     registers.                        area of the VPD
                                                                                          If the VPD structure is not valid, the
                                                                                          entire 1024 bytes area is RO.

Firmware      FLMNG               Flash    0x000000 -   FLMNGCTL and FLMNGDATA            Software access is available only when
or            Parallel                     0xFFFFFF     registers accesses to the FLASH   protection is disabled.
Software      (Read: 32-bits
              Write: 8-bits)

#### 3.4.3.1 Memory Mapped Host Interface

Using the legacy Flash transactions, the Flash is accessed by the X550 each time the host CPU performs
a read or a write operation to a memory location mapped to the Flash address space, or upon boot via
accesses in the space indicated by the Expansion ROM Base Address register. Accesses to the Flash are
based on a direct decode of CPU accesses to a memory window defined in either:
 • Memory CSR + Flash Base Address Register (PCIe Control Register at offset 0x10).
 • The Expansion ROM Base Address Register (PCIe Control Register at offset 0x30).
 • The X550 is responsible to map accesses via the Expansion ROM BAR to the physical NVM. The
   offset in the NVM of the Expansion ROM module is defined by the PCIe Expansion/Option ROM
   Pointer (NVM word address 0x05). This pointer is loaded by the X550 from the NVM before enabling
   any access to the Expansion ROM memory space.
The X550 controls accesses to the Flash when it decodes a valid access. Attempt to out of range read
access the PCIe Expansion/Option ROM module (according to NVM Size field in NVM Control Word 1)
would return a value of 0xDEADBEEF. Attempt to memory-mapped write accesses to the Flash when
protection is enabled or via expansion ROM BAR are ignored.

98                                                                                                                      333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

### 3.4.4 Flash Access Contention

Flash accesses initiated through different LAN functions might occur concurrently. The X550 does not
synchronize between entities accessing the Flash, so a contention caused from one entity reading and
another modifying the same location is possible.
To avoid such contention between software LANs or between software and firmware accesses, these
entities are required to make use of the semaphore registers. Refer to Section 11.8.4. Any read or write
access to the NVM made by software/firmware must be preceded by acquiring ownership over the NVM.
This is also useful to avoid the time out of a PCIe transaction made to a memory mapped Flash address
while the Flash is busy performing a sector erase operation.
However, two software entities cannot use this semaphore mechanism: BIOS access through expansion
ROM and VPD software.
 • Since VPD software accesses only the VPD module, which is located in the configuration section of
   the NVM, VPD accesses are always performed against the Shadow RAM. Firmware must take NVM
   ownership before dumping the VPD changes to the Flash. The Shadow RAM dump sequence is
   described in Section 3.4.2.1.
 • No contention can occur between the BIOS access through expansion ROM and other software
   entities (including VPD) as it accesses the NVM while the operating system is down.
 • Contentions between BIOS and firmware can however happen if a system reboot occurs while the
   MC is accessing the NVM.
     — If a system reboot is caused by a user pressing the standby button, it is required to route the
       wake-up signal from the standby button to the MC and not to the chipset. The MC issues a
       system reboot signal to the chipset only after the NVM write access completes. Firmware is
       responsible to respond with a “busy” error code to MC NC-SI commands while other NVM writes
       are in progress.
     — If a system reboot is issued by a local user on the host, there is no technical way to prevent
       NVM access contentions between the BIOS and the MC.
Caution:       It is the user’s responsibility when remotely accessing the NVM via the MC, to make sure
               another user is not currently initiating a local host reboot.
Notes:       The PHY auto-load process from the Flash device is made up of short read bursts (32-bits)
             that can be inserted by hardware in between other NVM clients’ accesses, at the lowest
             priority. It is the user’s responsibility to avoid initiating a PHY auto-load while updating the
             PHY NVM modules.
             The MAC auto-load from the Flash device itself occurs after power-up only, before host or
             firmware can attempt to access the Flash. The host must wait until PCIe reset is de-asserted
             (after ~1 second, which is enough time for the MAC auto-load to complete), and firmware
             starts its auto-load after the EEC.MNG_READY bit is asserted by hardware.
             Other MAC auto-load events are performed from the internal Shadow RAM and do not
             compete with memory mapped accesses to the Flash device. During such MAC auto-loads,
             accesses from other clients via EEPROM-Mode registers are delayed until the auto-load
             process completes.
             Software and firmware should avoid holding Flash ownership (via the dedicated semaphore
             bit) for more than 500 ms.

333369-009                                                                                                      99
                                  Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

#### 3.4.4.1 Flash Deadlock Avoidance

The Flash is a shared resource between the following clients:
1. Hardware auto-load of Shadow RAM (at power up).
2. LAN port 0 and LAN port 1 software accesses.
3. Manageability/firmware accesses.
4. Software tools.
All clients can access the Flash using parallel access. Hardware implements the actual access to the
Flash. Hardware arbitrates between the different clients and schedules these accesses, avoiding
starvation of any client.
However, the software and firmware clients can access the Flash using bit-banging. In this case, there is
a request/grant mechanism that locks the Flash to the exclusive use of one client. If one client is stuck
without releasing the lock, the other clients can no longer access the Flash. To avoid this deadlock, the
X550 implements a time-out mechanism, which revokes the grant from a client that does not toggle the
Flash bit-bang interface (FLA.FL_SCK bit) for more than 2 seconds. If any client fails to release the
Flash interface, hardware clears its grant, enabling the other clients to use the interface.
The deadlock timeout mechanism is enabled by the Deadlock Timeout Enable bit in NVM Control Word 2
in the Flash.

### 3.4.5 Signature Field

The only way the X550 can tell if a Flash is present is by trying to read the Flash. The X550 first reads
the Control word at word address 0x0 and at word address 0x2000. It then checks the signature value
at bits 7 and 6 in both addresses.
If bit 7 is 0b and bit 6 is 1b in (at least) one of the two addresses, it considers the Flash to be present
and valid. It then reads the additional Flash words from that section and programs its internal registers
based on the values read. Otherwise, it ignores the values read from that location and does not read
additional words.
If the signature bits are valid at both addresses the X550 assumes that the first section is the valid one.

### 3.4.6 VPD Support

The Flash image can contain an area for VPD. This area is managed by the OEM vendor and does not
influence the behavior of hardware. Word 0x2F of the Flash image contains a pointer to the VPD area in
the Flash. A value of 0xFFFF means VPD is not supported and the PCI_CAPCTRL.VPD_EN bit should be
cleared in the PCI NVM section (Section 6.2.6.9), to prevent the VPD capability from appearing in the
configuration space.
The maximal area size is 1024 bytes but can be smaller. The VPD block is built from a list of resources.
A resource can be either large or small. The structure of these resources are listed Table 3-22 and
Table 3-23.

100                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

Table 3-22. Small Resource Structure
Offset                                         0                                                     1—n

                   Tag = 0xxx,xyyyb (Type = Small(0), Item Name = xxxx,
Content                                                                                               Data
                                     length = yy bytes)

Table 3-23. Large Resource Structure
Offset                                    0                                       1—2                        3—n

                       Tag = 1xxx,xxxxb (Type = Large(1),
Content                                                                           Length                       Data
                            Item Name = xxxxxxxx)

The X550 parses the VPD structure during the auto-load process following PCIe reset to detect the read
only and read/write area boundaries. The X550 assumes the following VPD fields with the limitations
listed:

Table 3-24. VPD Structure
      Tag            Length (Bytes)                 Data                          Resource Description

     0x82        Length of identifier string   Identifier    Identifier string.

     0x90           Length of RO area              RO data   VPD-R list containing one or more VPD keywords.

                                                             VPD-W list containing one or more VPD keywords. This part is
     0x91           Length of RW area              RW data
                                                             optional.

     0x78                   n/a                      n/a     End tag.

VPD structure limitations:
 • The structure should start with a Tag = 0x82. If the X550 does not detect a value of 0x82 in the
   first byte of the VPD area or the structure does not follow the description of Table 3-24, it assumes
   the area is not programmed and the entire 1024 bytes area is read only.
 • The RO area and RW area are both optional and can appear in any order. A single area is supported
   per tag type. Refer to Appendix I in the PCI 3.0 specification for details of the different tags.
 • If a VPD-W tag is found, the area defined by its size is writable via the VPD structure.
 • The structure should end with a Tag = 0x78. The tag must be word aligned.
 • The VPD area can be accessed through the PCIe configuration space VPD capability structure listed
   in Table 3-24. Write accesses to a read only area or any access to an offset outside of the VPD area
   via this structure are ignored.
 • VPD area must be mapped in the first 16 KB section of the Flash mapped to the Shadow RAM.
 • VPD software does not check the semaphores before attempting to access the Flash via dedicated
   VPD registers. Even if the Flash is owned by another entity, VPD software read access to the VPD
   area in the Flash might complete immediately since it is first performed against the Shadow RAM.
   However, VPD software write access might not complete immediately since the VPD changes are
   committed to the Flash device at the X550’s initiative, once the other entity releases Flash
   ownership, which may take up to several seconds.

333369-009                                                                                                                  101
                                     Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                   Interconnects

#### 3.4.6.1 VPD Access Flows

3.4.6.1.1              First VPD Area Programming

The VPD capability is exposed in the PCIe configuration space only if the PCI_CAPCTRL.VPD_EN bit is
set, regardless of any other sanity checks that are performed on the VPD area contents.
The VPD content and pointer can be written on a blank Flash without any limitation, such as for any
other NVM module when in the blank Flash programming mode. After protection is enabled, if VPD
Write Enable bit in NVM Control Word 1 is cleared, only the RW area of the VPD is writable and only via
the VPD interface.

3.4.6.1.2              VPD Area Update Flow

1. The host initiates a VPD write by programming the offset and data fields of the VPD capability
   register set, and then setting the capability's Flag bit.(bit 15 in VPD Address Register - 0xE2).
2. Firmware checks if the VPD write is allowed - it checks that the write offset falls within the VPD-RW
   area.
      a. If writing is not allowed, firmware clears the VPD flag in the configuration space to notify the VPD
         software that the transaction completed, and then it exits the flow.
3. Firmware indicates VPD access completion by clearing the VPD flag in the configuration space.
Note:      In case the Flash is occupied with a previous sector erase operation, or if NVM ownership is
           held by software, the completion indication (Step 3) might be delayed. Additional writes
           should not be attempted before the completion of Step 3.

### 3.4.7 NVM Read, Write, and Erase Sequences

Refer to Section 3.4.8.1 for the flow required to update secure NVM modules.
Any software flow described in this section must be preceded by taking NVM ownership via semaphores
as described in Section 11.8.4.

#### 3.4.7.1 Flash Block Erase Flow by Software

1. Send a Flash Block Erase host interface command (Section 11.8.3.3.7) with the aligned address of
   the block to erase.
2. Wait for the command to complete before releasing the NVM semaphore.

#### 3.4.7.2 X550 Software Flow to the Bit-Banging Interface

To directly access the Flash when Flash is blank or not protected, software should follow these steps:
1. Write a 1b to the Flash Request bit (FLA.FL_REQ).
2. Poll the Flash Grant bit (FLA.FL_GNT) until it becomes 1b. It remains 0b as long as there are other
   accesses to the Flash.
3. Write or read the Flash using the direct access to the 4-wire interface as defined in the FLA register.
   The exact protocol used depends on the Flash placed on the board.

102                                                                                                  333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

4. Write a 0b to the Flash Request bit (FLA.FL_REQ).
5. Following a write or erase instruction, software should clear the Request bit only after it has
   checked that the cycles were completed by the NVM. This can be checked by reading the BUSY bit
   in the Flash device STATUS register. Refer to Flash data sheet for the op-code to be used for reading
   the STATUS register.
Note:        The bit-banging interface is blocked during normal operation (protection enabled). Software
             should use the Host Interface commands. The firmware can use this interface all the time.

#### 3.4.7.3 Erase Flow Using the FLA Register

To directly erase a sector in the Flash when Flash is blank or not protected, software should follow these
steps:
1. Take ownership of NVM semaphore.
2. Set the Flash Address (FLA.FL_ADDR) to the index of the 4 KB sector to erase and Sector Erase bit
   (FLA.FL_SER) bit.
3. Read the FLA register until Flash Busy bit (FLA.FL_BUSY) is cleared.
4. Release ownership of NVM semaphore.
To directly erase the entire Flash when Flash is blank or not protected, software should follow these
steps:
1. Take ownership of NVM semaphore
2. Set Device Erase bit (FLA.FL_DER) bit.
3. Read the FLA register until Flash Busy bit (FLA.FL_BUSY) is cleared.
4. Release ownership of NVM semaphore.

#### 3.4.7.4 Software Access Flow to Shadow RAM

3.4.7.4.1              Read Interface

Software can read from the Shadow RAM using the following flow:
1. Send a Shadow RAM Read host interface command (Section 11.8.3.3.2) with the address and
   length to read.
2. Wait for the command to complete.
3. Read the data from the response buffer.

3.4.7.4.2              Write Interface

Software can write to the Shadow RAM using the following flow:
1. Send a Shadow RAM Write host interface command (Section 11.8.3.3.4) with the address, length
   and data to write.
2. Wait for the command to complete.

333369-009                                                                                              103
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                 Interconnects

#### 3.4.7.5 Software Access to Flash via Memory Mapped Interface

3.4.7.5.1            Read Access

Software can always use the Flash BAR for read accesses.
Note:     Software should take semaphore ownership before executing the flow.

3.4.7.5.2            Write Access

When Flash is blank or protection is disabled, software might initiate a write cycle via the Flash BAR as
follows:
1. Take semaphore ownership before executing the flow.
2. Write the data byte to the Flash through the Flash BAR.
3. Poll the FL_BUSY flag in the FLA register until cleared.
4. Repeat Step 2 and Step 3 to write additional bytes.
5. Release NVM semaphore ownership
As a response, hardware executes the following steps for each write access:
1. Set the FL_BUSY bit in the FLA register.
2. Initiate autonomous write enable instruction.
3. Initiate the program instruction right after the enable instruction.
4. Poll the Flash status until programming completes.
5. Clear the FL_BUSY bit in the FLA register.
Note:     Software must erase the sector prior to programming it.

#### 3.4.7.6 Software Flash Programming via Host Interface

                    Command
Software must take semaphore ownership before executing the flow.
Software can write to non write protected areas of the flash using the following flow:
1. Send a Flash Write host Interface command (Section 11.8.3.3.3) with the address, length and data
   to write.
2. Wait for the command to complete.

104                                                                                                333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

#### 3.4.7.7 Software Flash Read via Host Interface Command

Software must take semaphore ownership before executing the flow.
Software can read from the flash using the following flow:
1. Send a Flash Read host Interface command (Section 11.8.3.3.1) with the address and length of the
   data to read.
2. Wait for the command to complete.
3. Read the data from the completion of the command.

### 3.4.8 Extended NVM Flows

#### 3.4.8.1 Flow for Updating Secured Modules

This section describes the flow to use to update the firmware image (Section 6.1.4), Option ROM
(Section 6.1.5) or PHY module (Section 6.1.6).
To protect the Flash update procedure from power-down events, a double image policy is used for each
of the updated modules. The software flow to update a module is as follows:
1. Take ownership over the NVM via the semaphore bits. Refer to Section 11.8.4.
     a. If SW_FW_SYNC.NVM_UPDATE_STARTED bit is read as clear, set this bit together with setting
        NVM semaphore bit. It is used to notify other entities that a long NVM update process which may
        take up to several minutes has started. During this time, other entities can not perform a write
        access to the firmware or PHY modules, but reading these modules in between update write
        bursts is allowed using the flash memory mapping. Legacy EEPROM Modules are not concerned
        by this limitation.
     b. Otherwise, release NVM semaphore ownership and restart the update process later on.
2. Read the pointer to the free provisioning area (NVM word 0x40). Check that the free provisioning
   area size read from NVM word 0x41 is greater or equal to the size of the new firmware/PXE/PHY
   image to be loaded in NVM.
     a. If not, release NVM semaphore ownership, clear the SW_FW_SYNC.NVM_UPDATE_STARTED bit
        and exit the flow.
3. Initiate sector erase instructions (Section 3.4.7.1) to the entire free space provisioning segment.
     a. To guarantee NVM semaphore ownership time does not exceed the 1 sec timeout, it is
        recommended to perform at this step no more than four 4 KB sector erase operations at once in
        a burst, releasing semaphore ownership for 200 s in between. This way, other entities can insert
        NVM read accesses in between burst without waiting for the entire update process completion,
        which might take minutes.
4. Write the new firmware/Option ROM/PHY module to the free provisioning area via Flash-mode
   access.
     a. Same as Step 3a, it is recommended to write at this step no more than four 4 KB sectors at once
        in a burst, releasing semaphore ownership for 200 s in between.

333369-009                                                                                            105
                                 Did this document help answer your questions?

                                                                         Intel® Ethernet Controller X550 Datasheet
                                                                                                     Interconnects

5. Send a Flash Module Update host Interface command (Section 11.8.3.3.5) with the module ID of
   the section to update.The encoding of the modules is:

                                                           Section
                   Module                     ID
                                                           Number

      Firmware code                           0x1           6.1.4

      Reserved                                0x2

      Reserved                                0x3

      Reserved                                0x4

      PHY Firmware Image                      0x5           6.1.6

      Reserved                             0x6-0xFD

      Option ROM                             0xFE           6.1.5

      Reserved (Full Shadow RAM)              0xFF

6. Release the NVM semaphore and clear the SW_FW_SYNC.NVM_UPDATE_STARTED bit.
      a. Software must avoid taking the NVM semaphore again until the firmware command has
         completed. Any attempt to write the NVM until then is not performed by the device.
7. Firmware swaps between the Free Provisioning Area Pointer (word 0x40) and the Firmware Code
   Module pointer, PXE module pointer or the PHY pointer located at the Shadow RAM word address
   0x3A/0x5/0x4 respectively
8. Software waits for the command to complete.
      a. If the update process failed due to a security check failure or a flash write fault, an Authentication
         Error (0x80) or Data Error (0x6) respectively is returned. Software must then exit the flow, prior
         to attempt another update.
9. If the updated module is the PHY image, the PHY should be instructed to reload the image using the
   following flow:
      a. Update the PHY firmware version number at NVM word address 0x19 (Section 6.2.2.26) using
         the Legacy EEPROM Module Update flow (Section 3.4.7.6).
      b. Read-modify-write SRAMREL register for setting LATCH_IMAGE_VLD bit to 1b.
      c. Read-modify-write SRAMREL register for setting LATCH_IMAGE_VLD bit to 0b.
      d. Write PHY register bit 1E.C474.0 bit to 0b.
      e. Force PHY image reload by setting PHY register bit 1E.C442.0 to 1b.
10. If the updated module is the firmware image, the firmware should be instructed to reload the image
    using the Apply Update command (Section 11.8.3.3.6).

106                                                                                                    333369-009
                                   Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

#### 3.4.8.2 Flow for Updating One of the RW Legacy EEPROM

                      Modules
When updating one or several fields from a legacy EEPROM module there is a risk that a hardware auto-
load event occurs in the middle of the operation (fox example, due to a sudden PCIe reset), leading to
the auto-load of an invalid or inconsistent content from the internal Shadow RAM into the device
registers or memory. Therefore unless the field(s) can be updated by a single EEPROM-mode access,
the updating software must repeatedly use the following procedure for each legacy EEPROM module to
be updated:
1. Take ownership over the NVM via semaphore bits. Refer to Section 11.8.4.
2. Invalidate the pointer to the module to be modified by setting it to 0xFFFF using Shadow RAM Write
   command. This way, if a hardware auto-load of the module is attempted, the associated register
   defaults are loaded instead. Do not invalidate pointers to firmware modules, only to hardware
   auto-load modules.
3. Modify the contents of the module via Shadow RAM Write command.
4. Restore the pointers modified in Step 2 via Shadow RAM Write command.
5. Compute and update the software checksum (word 0x3F) if the contents covered by the software
   checksum was modified.
6. Release the NVM semaphore.
7. Send a Shadow RAM dump command (Section 11.8.3.3.8) to ask the device firmware to load the
   internal Shadow RAM into the Flash.
Note:        Depending on the modified RO items, a system reset is generally required for loading the
             modifications into the device.

### 3.4.9 NVM Authentication Procedure

NVM update integrity feature ensures that only Intel approved firmware code (or other protected NVM
module) is able to be updated on the X550 devices after manufacturing. This procedure is performed
whenever attempting to update one of the protected modules.
Integrity validation of NVM updates is provided by a digital signature. The digital signature is a SHA256
Hash computed over the protected content (long by 256-bits) which is then encrypted by a 2048-bits
RSA encryption using an Intel private key. This digital signature is stored in the manifest in the NVM
module image. Also stored in the manifest is the corresponding RSA modulus (public key) and RSA
exponent to be used to decrypt the digital signature.
To verify the authenticity of the digital signature, firmware must first verify that the RSA Modulus and
RSA Exponent fields in the new firmware image loaded are identical to those in the old firmware image.
If the RSA Modulus and Exponent fields are the same, firmware decrypts the digital signature using the
2048-bit RSA Modulus and Exponent fields stored in the manifest of the old firmware image to extract
the expected SHA256 Hash of content (stored hash). Firmware then performs an independent SHA256
Hash over the protected content (computed hash). If the stored hash matches the computed hash, the
digital signature is accepted, and the NVM update is applied.
NVM updates are validated prior to invalidating the old NVM configuration, such that the old NVM
configuration is still usable if the update fails to validate. After the new NVM is successfully verified, the
updated image is committed to device flash.

333369-009                                                                                                 107
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                                                  Interconnects

                               Sign                               Verify
                                              SHA256                              SHA256
                                               Hash                                Hash
                             CSS Header                          CSS Header
                              2048-bits                           2048-bits
  Module’s                   RSA Modulus                         RSA Modulus                   New = Old ?
                             RSA Exponent     Private key        RSA Exponent
  Manifest
                  Digital                   RSA encryption
                 Signature                                                        Public key
                             Protected                           Protected      RSA decryption
                              Module                              Module
                             Contents                            Contents                             =?

                                                       Digest                                Digest
Figure 3-6.   Sign & Verify Procedures for Authenticated NVM Modules

#### 3.4.9.1 Digital Signature Algorithm Details

As described the digital signature generation is a hash computation followed by an RSA encryption. This
is performed within Intel as part of the NVM update image generation process and not performed by
Intel software in the field, nor by the X550.
The different algorithms used are described in the following locations:
 • PKCS #1 v2.1: RSA Cryptography Standard, RSA Laboratories, June 14, 2002
        www.rsa.com
 • SHA family definition
        http://csrc.nist.gov/publications/fips/fips180-3/fips180-3_final.pdf
 • SHA usage with digital signatures
        http://csrc.nist.gov/publications/nistpubs/800-107/NIST-SP-800-107.pdf
 • SHA validation vectors
        http://csrc.nist.gov/groups/STM/cavp/documents/shs/SHAVS.pdf

108                                                                                                   333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects
