## 1.8 Architecture and Basic Operation

### 1.8.1 Transmit (Tx) Data Flow

Tx data flow provides a high-level description of all data/control transformation steps needed for
sending Ethernet packets over the wire.

Table 1-8.     Tx Data Flow
     Step                                                          Description

# 1 The software device driver creates a descriptor ring and configures one of the X550’s transmit queues with the

               address location, length, head, and tail pointers of the ring (one of 128 available Tx queues).

# 2 The software device driver is requested by the TCP/IP stack to transmit a packet, it gets the packet data within

               one or more data buffers.

# 3 The software device driver initializes the descriptor(s) that point to the data buffer(s) and have additional control

               parameters that describes the needed hardware functionality. The host places that descriptor in the correct
               location in the appropriate Tx ring.

# 4 The software device driver updates the appropriate Queue Tail Pointer (TDT).

# 5 The X550’s DMA senses a change of a specific TDT and as a result sends a PCIe request to fetch the descriptor(s)

               from host memory.

# 6 The descriptor(s) content is received in a PCIe read completion and is written to the appropriate location in the

               descriptor queue.

# 7 The DMA fetches the next descriptor and processes its content. As a result, the DMA sends PCIe requests to fetch

               the packet data from system memory.

# 8 The packet data is received from PCIe completions and passes through the transmit DMA that performs all

               programmed data manipulations (various CPU offloading tasks as checksum offload, TSO offload, etc.) on the
               packet data on the fly.

# 9 While the packet is passing through the DMA, it is stored into the transmit FIFO.

               After the entire packet is stored in the transmit FIFO, it is then forwarded to transmit switch module.

# 10 The transmit switch arbitrates between host and management packets and eventually forwards the packet to the

               security module.

# 11 The security module optionally encrypts the packet and authenticates it using IPsec and passes the packet to the

               MAC.

# 12 The MAC appends the L2 CRC to the packet and delivers the packet to the integrated PHY.

# 13 The PHY performs the PCS encoding, scrambling, Low-Density Parity Check (LDPC) encoding, and the other

               manipulations required to deliver the packet over the copper wires at the selected speed.

# 14 When all the PCIe completions for a given packet are complete, the DMA updates the appropriate descriptor(s).

# 15 The descriptors are written back to host memory using PCIe posted writes. The head pointer is updated in host

               memory as well if the X550 is configured to do so.

# 16 An interrupt is generated to notify the software device driver that the specific packet has been read to the X550

               and the driver can then release the buffer(s).

333369-009                                                                                                                         47
                                     Did this document help answer your questions?

                                                                                  Intel® Ethernet Controller X550 Datasheet
                                                                                                                Introduction

### 1.8.2 Receive (Rx) Data Flow

Rx data flow provides a high-level description of all data/control transformation steps needed for
receiving Ethernet packets.

Table 1-9.    Rx Data Flow
     Step                                                         Description

# 1 The software device driver creates a descriptor ring and configures one of the X550’s receive queues with the

             address location, length, head, and tail pointers of the ring (one of 128 available Rx queues).

# 2 The software device driver initializes descriptor(s) that point to empty data buffer(s). The software device driver

             places these descriptor(s) in the correct location at the appropriate Rx ring.

# 3 The software device driver updates the appropriate Queue Tail Pointer (RDT).

    4 A packet enters the PHY through the copper wires.

# 5 The PHY performs the required manipulations on the incoming signal such as LDPC decoding, de-scrambling, PCS

             decoding, etc.

# 6 The PHY delivers the packet to the Rx MAC.

# 7 The MAC forwards the packet to the security block.

# 8 If the packet is identified as a IPsec packet, it is decrypted.

# 9 If the packet matches the pre-programmed criteria of the Rx filtering, it is forwarded to an Rx FIFO.

# 10 The receive DMA fetches the next descriptor from the appropriate host memory ring to be used for the next

             received packet.

# 11 After the entire packet is placed into an Rx FIFO, the receive DMA posts the packet data to the location indicated

             by the descriptor through the PCIe interface.
             If the packet size is greater than the buffer size, more descriptor(s) are fetched and their buffers are used for the
             received packet.

# 12 When the packet is placed into host memory, the receive DMA updates all the descriptor(s) that were used by the

             packet data.

# 13 The receive DMA writes back the descriptor content along with status bits that indicate the packet information

             including what offloads were done on that packet.

# 14 The X550 initiates an interrupt to the software device driver to indicate that a new received packet is ready in host

             memory.

# 15 The software device driver reads the packet data and sends it to the TCP/IP stack for further processing. The

             software device driver releases the associated buffer(s) and descriptor(s) once they are no longer in use.

48                                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Pin Interface

Chapter 2                        Pin Interface
