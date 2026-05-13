## 3.5 Configurable I/O Pins — Software-Definable

                   Pins (SDPs)
The X550 has four software-defined pins (SDP pins) per port that can be used for miscellaneous
hardware or software-controllable purposes. Unless specified otherwise, these pins and their function
are bound to a specific LAN device. The use, direction, and values of SDP pins are controlled and
accessed by the Extended SDP Control (ESDP) register. To avoid signal contention, following power-up,
all four pins are defined as input pins.
Some SDP pins have specific functionality:
 • The default direction of the SDP pins is loaded from the SDP Control word in the NVM.
 • The lower SDP pins (SDP0-SDP2) can also be configured for use as External Interrupt Sources
   (GPI). To act as GPI pins, the desired pins must be configured as inputs and enabled by the GPIE
   register. When enabled, an interrupt is asserted following a rising-edge detection of the input pin
   (rising-edge detection occurs by comparing values sampled at the internal clock rate, as opposed to
   an edge-detection circuit). When detected, a corresponding GPI interrupt is indicated in the EICR
   register.
Note:        An SDP configured as output can also generate interrupts, but this is not a recommended
             configuration.
The bit mappings are shown in Table 3-25 for clarity.

Table 3-25. GPI to SDP Bit Mappings
                                                 ESDP Field Settings
 SDP Pin to be Used as GPI                                                             Resulting EICR Bit (GPI)
                                     Directionality          Enable as GPI Interrupt

# 2 SDP2_IODIR                   SDP2_GPIEN

# 1 SDP1_IODIR                   SDP1_GPIEN

# 0 SDP0_IODIR                   SDP0_GPIEN

 • SDP1 pins can also be used to (electrically) disable both PCIe functions altogether. Also, if the MC is
   present, the MC-to-LAN path(s) remain fully functional. This PCIe-Function-Off mode is entered
   when SDP1 pin of a port is driven high while PE_RST_N is de-asserted. For correct capturing, it is
   therefore recommended to set SDP1 pins to their desired levels while the PE_RST_N pin is driven
   low and to maintain the setting on the (last) rising edge of PE_RST_N. This ability is enabled by
   setting bit 11 in NVM Control Word 2 (global NVM offset 0x01 - Section 6.2.2.1).
    Note:          The PCIe-Function-Off is activated regardless of the SDP1 direction defined in the NVM
                   SDP Control word.
 • The lowest SDP pins (SDP0_0) of port 0 can be used to encode the NC-SI package ID of the X550.
   This ability is enabled by setting bit 15 in NC-SI Configuration 2 word (offset 0x05 -
   Section 6.2.17.6) of the NVM. The 3-bit package ID is encoded as follows: Package ID = {0,
   SDP0_0, 0}.
 • When the SDP pins are used as IEEE1588 auxiliary signals they can generate an interrupt on any
   transition (rising or falling edge), refer to Section 7.7.4.
 • A pair of SDPs can be used to create an I2C interface as described in Section 3.5.1.
All SDP pins can be allocated to hardware functions. See more details on IEEE1588 auxiliary
functionality in Section 7.7.4 while I/O pins functionality are programmed by the TimeSync Auxiliary
Control (TSAUXC) register.

333369-009                                                                                                    109
                                   Did this document help answer your questions?

                                                                              Intel® Ethernet Controller X550 Datasheet
                                                                                                          Interconnects

If mapping of these SDP pins to a specific hardware function is not required, the pins can be used as
general purpose software defined I/Os. For any of the function-specific usages, the SDP I/O pins should
be set to native mode by software setting of the SDPxxx_NATIVE bits in the ESDP register. Native mode
in those SDP I/O pins, defines the pin functionality at inactive state (reset or power down) while
behavior at active state is controlled by the software. The hardware functionality of these SDP I/O pins
differs mainly by the active behavior controlled by software.
Table 3-26 summarize the setup required to achieve each of the possible SDP configurations.

Table 3-26. SDP Settings
                                                                                  ESDP
 SDP          Usage               NVM Setting
                                                     SDPx_NATIVE   SDPx_IODIR        SDP1_Function    SDP23_function

       SDP                            N/A                 0        Input/Output

                                 Bit 15 in NC-SI
       NC-SI package ID
                               Configuration 2 NVM        0           Input
       (Port #0 only)
  0                                   word                                                         N/A

       1588 functionality as
       defined by the TSSDP           N/A                 1        Input/Output
       register

       SDP                            N/A                 0        Input/Output            0

                               NVM Control Word 2,
       PCI disable             SDP_FUNC_OFF_EN           N/A           N/A                N/A
                                      bit

       1588 functionality as
       defined by the TSSDP           N/A                 1        Input/Output            0

    1 N/A

       register

                               TS NVM-based Mode
                                 Enable bit in the
       Thermal Sensor                                     0           Output               1
                                Common Firmware
                                 Parameters word

       Reserved                       N/A                 1            N/A                 1

       SDP                                                0        Input/Output                             N/A

       1588 functionality as
  2    defined by the TSSDP           N/A                 1        Input/Output           N/A                0
       register

       I2C clock                                          1            N/A                                   1

       SDP                                                0        Input/Output                             N/A

       1588 functionality as
  3    defined by the TSSDP           N/A                 1        Input/Output           N/A                0
       register

       I2C data                                           1            N/A                                   1

110                                                                                                         333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

### 3.5.1 I2C Over SDP

The I2C usage of SDP pins is enabled by setting the SDP23_function bit and the SDP[23]_NATIVE bits
to 1b in ESDP register. This relates to the SDPx_2 and SDPx_3 pins, which operate as I2C_CLK and
I2C_DATA, respectively.
The I2C interface operates via the I2CCMD and I2CPARAMS register set. Since this register set can be
used by either software or firmware in alternation, its ownership must be acquired/released via the
semaphore ownership taking/release flows described in Section 4.7.
The I2C interface can be used in two methods, a hardware based access, where the device initiate a
transaction following a software device driver request via the I2CCMD register (Section 8.2.2.1.16) or a
software controlled bit-banging using the I2CPARAMS register (Section 8.2.2.1.17).

#### 3.5.1.1 Hardware Based I2C Access

The following flows should be used to access an I2C register.
As part of device initialization, or anytime before the actual access, the following parameters should be
set:
 • I2CPARAMS.PHYADD — the address of the device to access.
 • I2CPARAMS.ACCESS_WIDTH — the width of the data to read or write (byte or word).
Note:        The I2CPARAMS register should not be modified during an I2C transaction.
To execute a write access, the following steps should be done:
1. Check that register is ready: Poll I2CCMD.R bit until it is read as 1b.
2. Command — The I2CCMD register is initialized with the appropriate PHY register address in
   REGADD field, the data to write in the DATA field and the operation (write) to the OP field (0b).
     a. If an interrupt is required, set the I2CCMD.I field
3. Check that command is done: Poll I2CCMD.R bit until it is read as 1b.
     a. Check that no error is indicated in the I2CCMD.E field.
To execute a read access, the following steps should be done:
1. Check that register is ready: Poll I2CCMD.R bit until it is read as 1b.
2. Command — The I2CCMD register is initialized with the appropriate PHY register address in the
   REGADD field, and the operation (read) to the OP field (1b).
     a. If an interrupt is required, set the I2CCMD.I field
3. Check that command is done: Poll I2CCMD.R bit until it is read as 1b.
     a. Check that no error is indicated in the I2CCMD.E field.
4. Read the data returned from the I2CCMD.DATA field. If a byte access is done
   (I2CPARAMS.ACCESS_WIDTH = 0), only DATA[7:0] is valid.
See Section 3.5.1.3 below for the I2C commands supported when using the built in read and write
commands. All the transactions uses a clock of 100 KHz. When using the bit-bang method any
command can be given to the I2C device.

333369-009                                                                                             111
                                 Did this document help answer your questions?

                                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                                                               Interconnects

#### 3.5.1.2 Bit-Bang Based I2C Access

In this mode, the software device driver controls the I2C interface directly using the I2CPARAMS
register according to the following table:

                            Field Controlling the Output     Field Reflecting the Input        Field Controlling the Output
          Pad
                                       Value                            Value                         Enable Value1

 SDPx_2 (I2C clock)                   CLK_OUT                             CLK_IN                         CLK_OE_N
           2
 SDPx_3 (I C data)                   DATA_OUT                         DATA_IN                            DATA_OE_N

1. 0b = Pad is output. 1b = Pad is input.

#### 3.5.1.3 Supported Commands

Note:          The gray columns below denotes cycles driven by the I2C device. White columns denotes
               cycles driven by the X550.
When a word read command (I2CPARAMS.ACCESS_WIDTH = 1b, I2CCMD.OP =1b) is given the
following sequence is done by the X550:

Table 3-27. I2C Read Transaction - Dummy Write
  1                   7                 1   1                 8                    1

  S             Device Address         Wr   A          Register Address            A

          From I2CCMD.PHYADD            0   0       From I2CCMD.REGADD             0

Table 3-28. I2C Read Transaction - Word Read
  1                   7                 1   1                 8                    1               8                   1    1

  S             Device Address         Rd   A               Data                   A              Data                 A    P

        From I2CPARAMS.PHYADD           1   0    Stored in I2CCMD.DATA[7:0]        0   Stored in I2CCMD.DATA[15:8]     0

When a byte read command (I2CPARAMS.ACCESS_WIDTH = 0b, I2CCMD.OP =1b) is given the
following sequence is done by the X550:

Table 3-29. I2C Read Transaction - Dummy Write
  1                   7                 1   1                 8                    1

  S             Device Address         Wr   A          Register Address            A

        From I2CPARAMS.PHYADD           0   0       From I2CCMD.REGADD             0

Table 3-30. I2C Read Transaction - Byte Read
  1                   7                 1   1                 8                    1   1

  S             Device Address         Rd   A               Data                   A   P

        From I2CPARAMS.PHYADD           1   0    Stored in I2CCMD.DATA[7:0]        0

112                                                                                                                  333369-009
                                      Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

When a word write command (I2CPARAMS.ACCESS_WIDTH = 1b, I2CCMD.OP =0b) is given the
following sequence is done by the X550:

Table 3-31. I2C Write Transaction - Word Write
 1             7              1           8               1              8           1               8           1   1

 S       Device Address       Wr   Register Address       A             Data         A           Data            A   P

           From               0         From              0           From in        0          From in          0
     I2CPARAMS.PHYADD              I2CCMD.REGADD                 I2CCMD.DATA[7:0]          I2CCMD.DATA[15:8]

When a byte write command (I2CPARAMS.ACCESS_WIDTH = 0b, I2CCMD.OP =0b) is given the
following sequence is done by the X550:

Table 3-32. I2C Write Transaction - Byte Write
 1                 7                1                 8             1                8                   1   1

 S           Device Address        Wr         Register Address      A               Data                 A   P

        From I2CPARAMS.PHYADD       0      From I2CCMD.REGADD       0     From in I2CCMD.DATA[7:0]       0
