## 13.4 Connecting the Flash Interface

### 13.4.1 Connecting the Flash

The X550 provides support for a Serial Peripheral Interface (SPI) Flash device that is made accessible to
the system through the following:
 • Flash Base Address register (PCIe Control register at offset 0x14 or 0x18).
 • An address range of the IOADDR register, defined by the I/O Base Address register (PCIe Control
   register at offset 0x18 or 0x20).
 • Expansion ROM Base Address register (PCIe Control register at offset 0x30)

### 13.4.2 Supported Flash Devices

The X550 uses a SPI Flash. Several words of the Flash are accessed automatically by the X550 after
reset to provide pre-boot configuration data before it is accessed by host software. The remainder of
the Flash space is available to software for storing the MAC address, serial numbers, and additional
information. For a complete description of the content stored in the Flash refer to Section 6.
Supported Op Code:
 • Write Enable (06)
 • Read Status Register (05)
 • Write Status Register (01)
 • Read Data (03)
 • Byte/Page Program (02) (program 1 to 256 data bytes)
 • 4 KB Sector Erase (20)
 • Chip Erase (C7)
Note:     For the Write Status register op code, the written data is 0x00 (to cancel the default
          protection).
The X550 contains a 3.3V Flash I/O.

1150                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines
