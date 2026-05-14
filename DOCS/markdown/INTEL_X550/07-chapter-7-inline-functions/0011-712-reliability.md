## 7.12 Reliability

### 7.12.1 Memory Integrity Protection

All X550 internal memories are protected against soft errors. Most of them are covered by ECC that
correct single error per memory line and detect double errors per memory line. Few of the smaller
memories are covered by parity protection that detects a single error per memory line.
Single errors in memories with ECC protection are named also as correctable errors. Such errors are
silently corrected. Two errors in memories with ECC protection or single error in memories with parity
protection are also named as un-correctable errors. Un-correctable errors are considered as fatal
errors. If an un-correctable error is detected in Tx packet data, the packet is transmitted with a CRC
error. If un-correctable error is detected in Rx packet data, the packet is reported to the host (or
manageability) with a CRC error. If an un-correctable error is detected anywhere else, the X550 halts
the traffic and sets the ECC error interrupt. Software is then required to initiate a complete initialization
cycle to resume normal operation.

### 7.12.2 PCIe Error Handling

For PCIe error events and error reporting see Section 3.1.5.

333369-009                                                                                                                       565
                                      Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions
