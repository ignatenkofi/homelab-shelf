## 13.9 Connecting the JTAG Port

The X550 contains a test access port (3.3 V only) conforming to the IEEE 1149.1-2001 Edition (JTAG)
specification. To use the test access port, connect these balls to pads accessible by specific test
equipment.
For proper operation, a pull-down resistor should be connected to the JTCK and JRST_N signals and pull
up resistors to the JTDO, JTMS and JTDI signals.
A Boundary Scan Definition Language (BSDL) file describing the X550 is available for use in specific test
environments.
