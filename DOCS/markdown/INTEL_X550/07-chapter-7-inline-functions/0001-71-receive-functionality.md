## 7.1 Receive Functionality

Packet reception consists of:
 • Recognizing the presence of a packet on the wire (Section 7.1.1)
 • Performing address filtering (Section 7.1.2)
 • Optional IPsec decryption and authentication (Section 7.13)
 • Checksum off-loads (Section 7.1.6)
 • DMA queue assignment (Section 7.1.3)
 • Storing the packet in the receive data FIFO (Section 7.6.3.1)
 • Transferring the data to assigned receive queues in host memory (Section 7.1.4)
 • Optional Receive Side Coalescing (Section 7.10)
 • Updating the state of a receive descriptor (Section 7.1.5).

### 7.1.1 MAC Layer - Receive

#### 7.1.1.1 Packet Acceptance Criteria

In addition to the filtering rules described in the next sections, a packet must also meet the following
criteria to be accepted by the device:
1. Normally, only good packets are received (packets with none of the following errors: Under Size
   Error, Over Size Error, Packet Error, Length Error and CRC Error). However, if the Store Bad Packets
   bit is set (FCTRL.SBP), bad packets that don't pass the filter function are stored in host memory.
   Packet errors are indicated by error bits in the receive descriptor (RDESC.ERRORS). It is possible to
   receive all packets, regardless of whether they are bad, by setting the promiscuous enables bit and
   the Store Bad Packets bit. In this case, bad packets are queued according to the same rules as
   regular packets.
2. Min. Packet Size (Runt packets) — Rx packets, smaller than 48 bytes, cannot be posted to host
   memory regardless of save bad frame setting.
3. Max Packet Size — Any Rx packet posted from the MAC unit to the DMA unit cannot exceed
