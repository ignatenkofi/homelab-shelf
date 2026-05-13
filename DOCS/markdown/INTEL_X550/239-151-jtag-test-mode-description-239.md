## 15.1 JTAG Test Mode Description

The X550 includes a JTAG (TAP) port compliant with the IEEE Standard Test Access Port and Boundary
Scan Architecture 1149.1 Specification. The TAP controller is accessed serially through five dedicated
pins: TCK, TMS, TDI, TDO, and TRST_N. TMS, TDI, and TDO operate synchronously with TCK. TCK is
independent of all other device clocks.
This interface can be used for test and debug purposes. System board interconnects can be DC tested
using the boundary scan logic in pads. Table 15-1 shows TAP controller related pin descriptions.
Table 15-2 describes the TAP instructions supported.

Table 15-1. TAP Controller Pins
 Signal      I/O                                                       Description

TCK          In      Test clock input for the test logic defined by IEEE1149.1. If utilizing JTAG, connect to this signal ground
                     through a 1 K pull-down resistor.

TDI          In      Test Data Input. Serial test instructions and data are received by the test logic at this pin. If utilizing JTAG,
                     connect this signal to VCC33 through a 1 K pull-up resistor.

TDO          O/D     Test Data Output. The serial output for the test instructions and data from the test logic defined in
                     IEEE1149.1. If utilizing JTAG, connect this signal to VCC33 through a 1 K pull-up resistor.

TMS          In      Test Mode Select input. The signal received at JTMS is decoded by the TAP controller to control test
                     operations.

TRST_N       In      JTAG Reset Input. Active low reset for the JTAG port.

Table 15-2. Main TAP Instructions Supported
   Instruction                                      Description                                                  Comment

BYPASS             The BYPASS command selects the Bypass Register, a single bit register              IEEE 1149.1 Std. Instruction
                   connected between TDI and TDO pins. This allows more rapid movement of
                   test data to and from other components in the system.

EXTEST             The EXTEST Instruction allows circuitry or wiring external to the devices to be    IEEE 1149.1 Std. Instruction
                   tested. Boundary-scan Register Cells at outputs are used to apply stimulus
                   while Boundary-scan cells at input pins are used to capture data.

SAMPLE /           The SAMPLE/PRELOAD instruction is used to allow scanning of the boundary           IEEE 1149.1 Std. Instruction
PRELOAD            scan register without causing interference to the normal operation of the
                   device. Two functions can be performed by use of the Sample/Preload
                   instruction.
                     • SAMPLE – allows a snapshot of the data flowing into and out of a device to
                        be taken without affecting the normal operation of the device.
                     • PRELOAD – allows an initial pattern to be placed into the boundary scan
                        register cells. This allows initial known data to be present prior to the
                        selection of another boundary-scan test operation.

333369-009                                                                                                                         1189
                                     Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                                               Diagnostics

Table 15-2. Main TAP Instructions Supported [continued]
  Instruction                                    Description                                               Comment

IDCODE          The IDCODE instruction is forced into the parallel output latches of the          IEEE 1149.1 Std. Instruction
                instruction register during the Test-Logic-Reset TAP state. This allows the
                device identification register to be selected by manipulation of the broadcast
                TMS and TCK signals for testing purposes, as well as by a conventional
                instruction register scan operation.
                The ID code value for the X550 A0 is 0x11562013 (Intel's Vendor ID = 0x09,
                Device ID = 0x1562, Rev ID = 0x0)
                The ID code value for the X550 B0 is 0x21562013 (Intel's Vendor ID = 0x09,
                Device ID = 0x1562, Rev ID = 0x1)

HIGHZ           The HIGHZ instruction is used to force all outputs of the device (except TDO)     IEEE 1149.1 Std. Instruction
                into a high impedance state. This instruction selects the Bypass Register to be
                connected between TDI and TDO in the Shift-DR controller state.
