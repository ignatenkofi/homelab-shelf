## 11.8 Manageability Host Interface

This section details host interaction with the manageability portion of the X550. The information within
this section is only available to the host driver, the BMC does not have access.

### 11.8.1 HOST CSR Interface (Function 1/0)

The software device driver of all functions communicates with the manageability block through CSR
access. The manageability is mapped to address space 0x15800 to 0x15FFF on the slave bus of each
function.
Note:     Writing to address 0x15800 from any function is targeted to the same address in the RAM.

### 11.8.2 Host Slave Command Interface to Manageability

This interface is used by the software device driver for several of the commands and for delivering
various types of data in both directions (Manageability-to-Host and Host-to-Manageability).
The address space is separated into two areas:
 • Direct access to the internal data RAM: The internal shared (between firmware and software) RAM
   is mapped to address space 0x15800 to 0x15EFF. Writing/reading to this address space goes
   directly to the RAM.
 • Control register is located at address 0x15F00.

#### 11.8.2.1 Host Slave Command Interface Low Level Flow

This interface is used for the external host software to access the manageability subsystem. Host
software writes a command block or read data structure directly from the data RAM. Host software
controls these transactions through a slave access to the HICR control register (see
Section 8.2.2.20.5).
The following flow shows the process of initiating a command to the manageability block:
1. The software clears the FWSTS.FWRI flag (clear by write one) to clear any previous firmware reset
   indications.
2. The software device driver takes ownership of the Management Host interface using the flow
   described in Section 4.7.
3. The software device driver reads the HOST Interface Control register (see Section 8.2.2.20.5) and
   checks that the Enable (HICR.EN) bit is set.
4. The software device driver writes the relevant command block into the RAM area that is mapped to
   addresses 0x15800-0x15EFF.
5. The software device driver sets the Command (HICR.C) bit in the HOST Interface Control register
   (see Section 8.2.2.20.5). Setting this bit causes an interrupt to the ARC.
6. The software checks the FWSTS.FWRI flag to make sure a firmware reset didn’t occur during the
   command processing. If this bit is set, the command may have failed.
7. The software device driver polls the HOST Interface Control register for the Command (HICR.C) bit
   to be cleared by firmware. The command should complete within half a second.

1100                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

8. When firmware finishes with the command, it clears the Command (HICR.C) bit (if firmware replies
   with data, it should clear the bit only after the data is placed in the shared RAM area where the
   software device driver can read it).
If the software device driver reads the HOST Interface Control register and the HICR.SV bit is set to 1b,
there is a valid status of the last command in the shared RAM. If the HICR.SV bit is not set, the
command has failed with no status in the RAM.
On completion of access to the shared RAM software device driver should release ownership of the
shared RAM using the flow described in Section 4.7.

#### 11.8.2.2 Host Interface Structure

11.8.2.2.1                   Host Interface Command Structure

Table 11-47 describes the structure used by the software device driver to send a command to firmware
using the Host slave command interface (shared RAM mapped to addresses 0x15800-0x15EFF).

Table 11-47. Host Driver Command Structure
 Byte(s)       Description      Bit(s)          Value                                  Description

# 0 Command             7:0     Command Dependent    Specifies which host command to process.

# 1 Buffer Length       7:0     Command Length       Command Data Buffer length: 0 to 252, not including 32 bits of

                                                              header.

# 2 Reserved            7:0                          Reserved.

# 3 Checksum            7:0     Defined Below        Checksum signature. If the value is 0xFF, the checksum is not

                                                              checked by the firmware.

  255:4      Data Buffer         7:0     Command Dependent    Command Specific Data
                                                               Minimum buffer size = 0
                                                               Maximum buffer size = 252

11.8.2.2.2                   Host Interface Status Structure

Table 11-48 lists the structure used by firmware to return a status to the software device driver via the
Host slave command interface. A status is returned after a command has been executed.

Table 11-48.        Status Structure Returned to Host Driver
 Byte(s)       Description      Bit(s)          Value                                  Description

# 0 Command             7:0     Command Dependent    Command ID.

# 1 Buffer Length       7:0     Status Dependent     Status buffer length: 252:0

# 2 Return Status       7:0     Depends on Command   0x1 =       Status OK

                                         Executing Results    0x2 =       Illegal command ID
                                                              0x3 =       Unsupported command
                                                              0x4 =       Illegal payload length
                                                              0x5 =       Checksum failed
                                                              0x6 =       Data Error
                                                              0x7 =       Invalid parameter
                                                              0x8–0x7F = Reserved
                                                              0x80–0xFF = Command Specific Errors. May be used by
                                                                          individual commands for command specific errors

333369-009                                                                                                              1101
                                       Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                       System Manageability

Table 11-48.        Status Structure Returned to Host Driver [continued]
 Byte(s)      Description       Bit(s)           Value                                     Description

# 3 Checksum             7:0     Defined Below          Checksum signature.

  255:4     Data Buffer                  Status Dependent       Status configuration parameters
                                                                  Minimum Buffer Size = 0
                                                                  Maximal Buffer Size = 252
                                                                If Return Status is not “Status OK” the Data Buffer is empty.

11.8.2.2.3                   Checksum Calculation Algorithm

The Host Command/Status structure is summed with this field cleared to 0b. The calculation is done
using 8-bit unsigned math with no carry. The inverse of this sum is stored in this field (0b minus the
result). Result: The current sum of this buffer (8-bit unsigned math) is 0b.

### 11.8.3 Host Interface Commands

#### 11.8.3.1 Driver Info Host Command

This command is used to provide the driver information in NC-SI mode.

Table 11-49. Driver Info Host Command
 Byte(s)         Name           Bit(s)         Value                                     Description

# 0 Command              7:0           0xDD         Driver info command.

# 1 Buffer Length        7:0        0x5 + driver    Port Number + 4 bytes of the Driver info + driver string length (total

                                            string length   length can be up to 255 bytes).

# 2 Reserved             7:0            0x0         Reserved.

# 3 Checksum             7:0                        Checksum signature of the Host command.

# 4 Function Number      7:0      Function Number   Indicates the function currently reporting its driver info.

   8:5      Driver Version       7:0       Driver Version   Numerical for driver version - should be:
                                                             Byte 8 = Major
                                                             Byte 7 = Minor
                                                             Byte 6 = Build
                                                             Byte 5 = SubBuild
                                                            Note: The old version is kept to support CEM version 1
                                                                    commands.

  9:9 +     Driver String                   Driver String   Driver string (not null terminated) as reported by driver.
  driver                                                    For example, in Linux the DRV_VERSION #define, or in NDIS, the
   string                                                   OID_GEN_VENDOR_DRIVER_VERSION. Can be up to 250 bytes.
  length

Following is the status returned on this command:

1102                                                                                                                      333369-009
                                       Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

Table 11-50. Driver Info Host Status
 Byte(s)          Name        Bit(s)    Value                                      Description

# 0 Command           7:0      0xDD       Driver Info command.

# 1 Buffer Length     7:0       0x0       No data in return status.

# 2 Return Status     7:0       0x1       See Table 11-48.

# 3 Checksum          7:0                 Checksum signature.

#### 11.8.3.2 Disable RXEN Command

This command is used to enable the driver to request a safe disable of Receive Enable.

Table 11-51.        Disable RXEN Command
 Byte(s)          Name        Bit(s)       Value                                      Description

# 0 Command           7:0         0xDE         Driver info command.

# 1 Buffer Length     7:0          0x1         1 data byte attached to this command (the port number).

# 2 Reserved          7:0          0x0         Reserved.

# 3 Checksum          7:0                      Checksum signature of the Host command.

# 4 Port Number       7:0      Port Number     Indicates the port for which the operation is requested.

Following is the status returned on this command:

Table 11-52. OS2BMC Control Status
 Byte(s)          Name        Bit(s)    Value                                      Description

# 0 Command           7:0       0xDE      Driver Info command.

# 1 Buffer Length     7:0       0x0       No data in return status.

# 2 Return Status     7:0       0x1       See Table 11-48.

# 3 Checksum          7:0                 Checksum signature.

The firmware should execute the following flow when receiving this command:
 • Store OS2BMC enable bit.
 • Clear OS2BMC enable bit.
 • Clear RXEN
 • Restore OS2BMC enable bit to original value.
 • Return from command.

333369-009                                                                                                         1103
                                     Did this document help answer your questions?

                                                                                          Intel® Ethernet Controller X550 Datasheet
                                                                                                              System Manageability

#### 11.8.3.3 Flash I/F interface

These commands allow buffers of up to 1Kbyte of data. To do this, the Buffer Length field is expanded
to 2 bytes.
Note:            This Buffer Length field in the command is in big endian order. For example, byte 1 contains
                 the MSB part of the buffer length and byte 2 contains the LSB part of the buffer length. The
                 buffer length in the response is in the reverse order (byte 1 contains the LSB and byte 2 [7:5]
                 contains the MS bits).

11.8.3.3.1                    Flash Read

This command is used to request a read from the flash. This command allows access to the region of
the flash owned by the device (in case of non-shared SPI, it is the entire flash).
This command always returns the value from the flash, even if read within the Shadow RAM
boundaries.

Table 11-53.            Flash Read Command
 Byte(s)             Name          Bit(s)       Value                                     Description

# 0 Command                  7:0       0x30   Flash Read.

   2:1        Buffer Length           15:0       0x6

# 3 Checksum                 7:0              Checksum signature.

   7:4        Address                 31:0              Address to read from the flash.

   9:8        Length to Read          15:0              How many bytes to read. Can be up to 1024.

Table 11-54. Flash Read Response
           Byte(s)                     Name              Bit(s)    Value                             Description

# 0 Command                       7:0         0x30    Flash Read.

# 1 Buffer Length (LS Byte)       7:0                 Buffer length[7:0].

# 2 Buffer Length (MS Byte)       7:5                 Buffer length[10:8].

# 2 Return Status                 4:0                 See Table 11-48.

# 3 Checksum                      7:0                 Checksum signature.

             7:4            Address                       31:0                Address to read from the flash.

             9:8            Length Read                   15:0                How many bytes where actually read.

            11:10           Reserved                                          Reserved.

 12: Length Read+12         Read Data                                         The Requested Data read from flash.

1104                                                                                                                    333369-009
                                             Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.8.3.3.2                   Shadow RAM Read

This command is used to request a read from the Shadow RAM. Requesting addresses above Shadow
RAM boundaries causes an error.

Table 11-55. Shadow RAM Read Command
 Byte(s)            Name          Bit(s)        Value                                           Description

# 0 Command                  7:0       0x31          Shadow RAM Read.

   2:1       Buffer Length           15:0        0x6

# 3 Checksum                 7:0                     Checksum signature.

   7:4       Address                 31:0                     Address to read from the Shadow RAM.

   9:8       Length to Read          15:0                     How many bytes to read. Can be up to 1024.

Table 11-56. Shadow RAM Read Response
         Byte(s)                      Name                    Bit(s)    Value                              Description

# 0 Command                             7:0       0x31       Shadow RAM Read.

# 1 Buffer Length (LS Byte)             7:0                  Buffer length[7:0].

# 2 Buffer Length (MS bits)             7:5                  Buffer Length[10:8].

# 2 Return Status                       4:0                  See Table 11-48.

# 3 Checksum                            7:0                  Checksum signature.

           7:4             Address                             31:0                 Address to read from the Shadow RAM.

           9:8             Length Read                         15:0                 How many bytes where actually read.

          11:10            Reserved                                                 Reserved.

 12: Length Read+12        Read Data                                                The Requested Data read from Shadow RAM.

11.8.3.3.3                   Flash Write

This command is used to update the flash sections out of the Shadow RAM. This command allows
access to the writable region of the flash owned by the device that is not part of the Shadow RAM. If not
all the area to erase is writable, the command returns an error.

Table 11-57. Flash Write Command
          Byte(s)                    Name          Bit(s)                Value                                Description

# 0 Command                   7:0               0x32              Flash Write.

            2:1               Buffer Length            15:0       0x8 + Length to Write

# 3 Checksum                  7:0                                 Checksum signature.

            7:4               Address                  31:0                                 Address to write to the Shadow RAM.

            9:8               Length to Write          15:0                                 How many bytes to write. Can be up to 1024.

           11:10              Reserved                                                      Reserved.

 12: Length to Write +12      Write Data                                                    The data to write to the flash.

333369-009                                                                                                                           1105
                                            Did this document help answer your questions?

                                                                                        Intel® Ethernet Controller X550 Datasheet
                                                                                                            System Manageability

Table 11-58.           Flash Write Response
 Byte(s)            Name         Bit(s)       Value                                     Description

# 0 Command              7:0         0x32       Flash Write.

# 1 Buffer Length        7:0          0x6

# 2 Return Status        7:0                    See Table 11-48.

# 3 Checksum             7:0                    Checksum signature.

   7:4       Address              31:0                   Address to write to the Shadow RAM.

   9:8       Data Written         15:0                   How many bytes where actually written.

11.8.3.3.4                   Shadow RAM Write

This command is used to update the Shadow RAM. It allows write to the writable parts of the Shadow
RAM. If not all the area to write is writable, or not all the area is in the Shadow RAM range, the
command returns an error.

Table 11-59. Shadow RAM Write Command
           Byte(s)                 Name               Bit(s)            Value                            Description

# 0 Command                  7:0              0x33             Shadow RAM write.

             2:1              Buffer Length           15:0      0x8 + Length to Write

# 3 Checksum                 7:0                               Checksum signature.

             7:4              Address                 31:0                               Address to write to the flash.

             9:8              Length to Write         15:0                               How many bytes to write. Can be up to
                                                                                         1024.

            11:10             Reserved

 12: Length to Write+12       Write Data                                                 The data to write to the Shadow RAM

Table 11-60. Shadow RAM Write Response
 Byte(s)            Name         Bit(s)       Value                                     Description

# 0 Command              7:0         0x33       Shadow RAM Write.

# 1 Buffer Length        7:0          0x6

# 2 Return Status        7:0                    See Table 11-48.

# 3 Checksum             7:0                    Checksum signature.

   7:4       Address              31:0                   Address to write to the Shadow RAM.

   9:8       Data Written         15:0                   How many bytes where actually written.

1106                                                                                                                      333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.8.3.3.5                   Flash Module Update

This command is used to update a secured module. After a successful response to this command, for a
firmware code update, an Apply Update command (Section 11.8.3.3.6) is sent to activate the new
firmware.

Table 11-61. Flash Module Update Command
 Byte(s)          Name          Bit(s)    Value                                    Description

# 0 Command             7:0       0x34   Flash Module Update.

   2:1       Buffer Length      15:0       0x1

# 3 Checksum            7:0              Checksum signature.

# 4 Module ID           7:0              Which module to update:

                                                   Firmware code =        0x1
                                                   PHY Firmware Image = 0x5
                                                   Option ROM =           0xFE

Table 11-62.        Flash Module Update Response
 Byte(s)          Name          Bit(s)    Value                                    Description

# 0 Command             7:0       0x34   Flash Module Update.

# 1 Buffer Length       7:0       0x0

# 2 Return Status       7:0              See Table 11-48.

                                                  If the Authentication failed, an Authentication Error (0x80) is returned

# 3 Checksum            7:0              Checksum signature.

11.8.3.3.6                   Apply Update

This command is used to request the firmware to switch to the new uploaded code. This command
involves a firmware reset, so no response should be expected after this command is given. The
software device driver may read the FWRESETCNT register before and after the command is given to
check if the reset took place.
Note:        An Apply Update command sent not after a successful Flash Module Update Command is
             ignored.
If after 100 ms the FWRESETCNT register has not increase, the software should assume the command
failed.

Table 11-63. Apply Update Command
 Byte(s)          Name          Bit(s)    Value                                    Description

# 0 Command             7:0       0x38   Apply Update.

   2:1       Buffer Length      15:0       0x0

# 3 Checksum            7:0              Checksum signature.

333369-009                                                                                                                   1107
                                       Did this document help answer your questions?

                                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                                               System Manageability

11.8.3.3.7                 Flash Block Erase

This command is used to erase some of the flash sections. This command allows access to the writable
region of the flash owned by the device that is not part of the Shadow RAM. If not all the area to erase
is writable, the command returns an error.

Table 11-64. Flash Block Erase Command
 Byte(s)          Name              Bit(s)        Value                                      Description

# 0 Command                       7:0      0x35          Flash Block Erase.

   2:1     Buffer Length                15:0          0x5

# 3 Checksum                      7:0                    Checksum signature.

   7:4     Address                      31:0                    Address of block to erase – must be 4K bytes aligned.

# 8 Number of sectors to          7:0                    How many 4KB sectors to erase. To avoid a too long command, this

           erase                                                number should be no larger than 3.

Table 11-65.         Flash Block Erase Response
 Byte(s)        Name          Bit(s)           Value                                       Description

# 0 Command                7:0          0x35         Flash Block Erase.

# 1 Buffer Length          7:0           0x5

# 2 Return Status          7:0                       See Table 11-48.

# 3 Checksum               7:0                       Checksum signature.

   7:4     Address                31:0                      Address of block to erase.

# 8 Erased Blocks          7:0                       How many blocks where actually erased.

11.8.3.3.8                 Shadow RAM Dump

This command is used to trigger a Shadow RAM dump. It should be used after updating a module in
Shadow RAM.

Table 11-66. Shadow RAM Dump Command
 Byte(s)        Name          Bit(s)           Value                                       Description

# 0 Command                7:0          0x36         Shadow RAM dump.

   2:1     Buffer Length          15:0          0x0

# 3 Checksum               7:0                       Checksum signature.

Table 11-67. Shadow RAM Dump Response
 Byte(s)        Name          Bit(s)           Value                                       Description

# 0 Command                7:0          0x36         Shadow RAM dump.

# 1 Buffer Length          7:0           0x0

# 2 Return Status          7:0                       See Table 11-48.

# 3 Checksum               7:0                       Checksum signature.

1108                                                                                                                       333369-009
                                         Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

11.8.3.3.9                   Flash Info

This command is used to provide information about the Flash.
Note:        If the connected Flash does not support SFDP, the JEDEC ID information – Valid field is not
             set.

Table 11-68. Flash Info Command
 Byte(s)          Name          Bit(s)           Value                                      Description

# 0 Command                7:0          0x37      Flash Info.

   2:1       Buffer Length      15:0              0x0

# 3 Checksum               7:0                    Checksum signature.

Table 11-69. Flash Info Response
 Byte(s)             Name                 Bit(s)        Value                                  Description

# 0 Command                       7:0           0x37   Flash Info.

# 1 Buffer Length                 7:0           0x8

# 2 Return Status                 7:0                  See Table 11-48.

# 3 Checksum                      7:0                  Checksum signature.

   7:4       Flash Size                   31:0                  Size of flash available to this device in bytes. In case on non-shared SPI,
                                                                it is the size of the flash.
                                                                In case of SFDP flash, the size from the SFDP data is reported, otherwise
                                                                the value from NVM is reported.

    8 JEDEC ID information          6:0                  Defines the bank number of the manufacturer ID (number of 0x7F

             – Bank                                             read).

             JEDEC ID information           7                   The JEDEC ID information is valid (is not set in shared SPI modes).
             – Valid

    9 JEDEC ID information          7:0                  Returns the manufacturer ID read by RDID command.

             – Manufacturer ID

    10 JEDEC ID information          7:0                  First byte of the device ID read by RDID command (Family and Density

             – Device ID 1st byte                               fields).

    11 JEDEC ID information          7:0                  Second byte of the device ID read by RDID command (Sub version and

             – Device ID 2nd byte                               Revision).

### 11.8.4 Software and Firmware Synchronization

Software and firmware synchronize accesses to shared resources in the X550 through a semaphore
mechanism and a shared configuration register between the software device driver of the two ports and
the firmware. This semaphore enables synchronized accesses to the following shared resources:
 • NVM
 • PHY 0 and PHY 1 registers
 • MAC (LAN controller) shared registers. This semaphore protects the MAC registers described in
   Section 8.2.2.16.
 • I2C

333369-009                                                                                                                             1109
                                          Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                           System Manageability

The SW_FW_SYNC.REGSMP bit is used as a semaphore mechanism between software and firmware.
Once software or firmware takes control over this semaphore flag, it can access the SW_FW_SYNC
Register and claim ownership over specific resources. The SW_FW_SYNC includes pairs of bits (one
owned by software and the other by firmware), where each pair of bits controls a different resource. A
resource is owned by software or firmware when its respective bit is set. It is illegal to have both pair
bits set at the same time. Described below are the required sequences for gaining and releasing control
over shared resources.

#### 11.8.4.1 Gaining Control of Shared Resource by Software

1. The software device driver checks that the software device driver of the other LAN function does not
   use the software/firmware semaphore.
       — The software device driver polls the SWSM.SMBI bit till it is read as 0b, or time expires
         (recommended expiration is ~10 ms + expiration time used for the SW_FW_SYNC.REGSMP).
       — If the SWSM.SMBI is found at 0b, the semaphore is taken. Note that following this read cycle
         the hardware auto sets the bit to 1b.
       — If time expired, it is assumed that the software device driver of the other function
         malfunctioned. The software proceeds to the next step.
2. The software device driver checks that the firmware does not use the software/firmware semaphore
   and then takes its control.
       — Software polls the SW_FW_SYNC.REGSMP bit till it is read as 0b, or time expires
         (recommended expiration is ~50 ms). If time has expired the software assumes that the
         firmware malfunctioned and proceeds to the next step, while ignoring the firmware bits in the
         SW_FW_SYNC register.
3. The software takes control of the requested resource(s).
       — The software device driver reads the firmware and software bit(s) of the requested resource(s)
         in the SW_FW_SYNC register. If the bit(s) is cleared, the resource(s) is accessible (i.e. no other
         entity owns the resource(s)). In this case the software device driver sets the software bit(s) of
         the requested resource(s) in the SW_FW_SYNC register. The software then clears the
         SW_FW_SYNC.REGSMP and SWSM.SMBI bits (releasing the software/firmware semaphore
         register), and can use the specific resource(s).
       — Otherwise (i.e. either firmware or software of the other LAN function owns the resource), the
         software clears the SW_FW_SYNC.REGSMP and SWSM.SMBI bits and then repeats the entire
         process after some delay (recommended 5-10 ms).
           • If the resources are not released by the software device driver of the other LAN function in
             a timely manner (recommended expiration time is ~1 sec), the software device driver can
             assume that the other software device driver malfunctioned. In that case the software
             device driver should clear all software flags that it does not own (including
             SW_FW_SYNC.REGSMP bit) and then repeat the entire process once again.
           • If the resource is not released by the firmware (recommended expiration time for firmware
             is ~50 ms) the software device driver can assume that the firmware malfunctioned. In that
             case the software device driver should sets the software bit(s) of the requested
             resource(s), while ignoring the corresponding firmware bits in the SW_FW_SYNC register.
Note:       The firmware initializes its semaphore flags as part of its init flow. The software semaphores
            are not reset.

1110                                                                                                 333369-009
                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
System Manageability

#### 11.8.4.2 Releasing a Shared Resource by Software

1. The software device driver takes control over the software/firmware semaphore as described above
   for gaining shared resources.
2. The software device driver clears the bit(s) of the released resource(s) in the SW_FW_SYNC
   register.
3. The software device driver releases the software/firmware semaphore by clearing the
   SW_FW_SYNC.REGSMP and SWSM.SMBI bits
4. The software device driver should delay (recommended 5-10 ms) before trying to gain the
   semaphore immediately following its release.

#### 11.8.4.3 Gaining Control of Shared Resource by Firmware

1. The firmware takes control over the software/firmware semaphore (SW_FW_SYNC register)
     — The firmware polls the SW_FW_SYNC.REGSMP bit till it is read as 0b, or timeout expires
       (recommended expiration time is ~10 ms).
     — If timeout has expired the firmware clears the SW_FW_SYNC.REGSMP bit (it is assumed the
       software device driver is not functional).
2. The firmware takes ownership of the requested resources
     — The firmware reads the software bit(s) corresponding to the requested firmware resource(s) in
       the SW_FW_SYNC register.
     — If the software bit is cleared (i.e. the software device driver does not own the resource), the
       firmware sets the firmware bit(s) of the requested resource(s). The firmware then clears the
       SW_FW_SYNC.REGSMP bit (releasing the software/firmware semaphore) and can use the
       specific resource(s).
     — Otherwise (i.e. software owns the resource), the firmware clears the SW_FW_SYNC.REGSMP bit
       and then repeats the above process after some delay (recommended delay of 5-10 ms).
          • If the resources owned by software are not released in a timely manner (~1 sec), the
            firmware “forces” its ownership over the requested resources. The firmware clears the
            software flags of the requested resources in the SW_FW_SYNC register (assuming the
            software that set those flags is not functional).

#### 11.8.4.4 Releasing a Shared Resource by the Firmware

1. The firmware takes control over the software/firmware semaphore as described above for gaining
   shared resources.
2. The firmware clears the bit(s) of the selected resource(s) in the SW_FW_SYNC register.
3. The firmware releases the software/firmware semaphore by clearing the SW_FW_SYNC.REGSMP
   bit.
4. The firmware should delay before trying to gain the selected resource semaphore immediately
   following its release (recommended 5-10 ms).

333369-009                                                                                          1111
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                                        System Manageability
