## 11.9 Host Isolate Support

If a BMC decides that a malicious software prevents its usage of the LAN, it may decide to isolate the
NIC from its driver. This is done using the TCO reset command (Section 11.6.3.14).
If TCO isolate is enabled in the NVM (Section 6.2.16), The TCO Isolate command disables PCIe write
operations to the LAN port. As the driver needs to access the CSR space to provide descriptors to the
NIC, this operation also stops the network traffic including OS-to-BMC and BMC-to-OS traffic as soon as
the existing transmit and receive descriptor queues are exhausted.

1112                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

Chapter 12 Electrical/Mechanical
           Specification
