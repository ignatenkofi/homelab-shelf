## 7.5 TLP Processing Hints (TPH)

The X550 supports the TPH capability defined in the PCI Express specification. It does not support
Extended TPH requests.
On the PCIe link existence of a TLP Process Hint (TPH) is indicated by setting the TH bit in the TLP
header. Using the PCIe TLP Steering Tag (ST) and Processing Hints (PH) fields, the X550 can provide
hints to the root complex about the destination (socket ID) and about data access patterns (locality in
Cache), when executing DMA memory writes or read operations. Supply of TLP Processing Hints
facilitates optimized processing of transactions that target Memory Space.
To enable TPH usage:
 1. For a given function, the TPH Requester Enable bit in the PCIe configuration TPH Requester Control
    Register should be set.
 2. Appropriate TPH Enable bits in TPH_RXCTRL or TPH_TXCTRL registers should be set.
 3. Processing hints should be programmed in the TPH_CTRL.DESC_PH and TPH_CTRL.DATA_PH
    Processing hints (PH) fields.
 4. Steering information should be programed in the CPUID fields in the TPH_RXCTRL and TPH_TXCTRL
    registers.
The Processing hints (PH) and Steering Tags (ST) are set according to the characteristics of the traffic
as described in Table 7-50.
Note:         To enable TPH usage, all the memory reads are done without setting any of the byte enable
              bits.
Note:         Per queue, the TPH features are exclusive. Software can enable the TPH feature for a given
              queue.

### 7.5.1 Steering Tag and Processing Hint Programming

Table 7-50 describes how the Steering tag (socket ID) and Processing hints are generated and how TPH
operation is enabled for different types of DMA traffic.

Table 7-50. Steering Tag and Processing Hint Programming
             Traffic type                  ST Programming                 PH value                        Enable

 Transmit descriptor write back or       TPH_TXCTRL.CPUID1          TPH_CTRL.DESC_PH2     Tx Descriptor Writeback TPH EN field in
 head write back                                                                          TPH_TXCTRL.

 Receive data buffers write              TPH_RXCTRL.CPUID1          TPH_CTRL.DATA_PH3     Rx Header TPH EN or Rx Payload TPH EN
                                                                                          fields in TPH_RXCTRL.

 Receive descriptor writeback            TPH_RXCTRL.CPUID1          TPH_CTRL.DESC_PH2     Rx Descriptor Writeback TPH EN field in
                                                                                          TPH_RXCTRL.

 Transmit descriptor fetch               TPH_TXCTRL.CPUID4          TPH_CTRL.DESC_PH2     Tx Descriptor Fetch TPH EN field in
                                                                                          TPH_TXCTRL.

 Receive descriptor fetch                TPH_RXCTRL.CPUID2          TPH_CTRL.DESC_PH2     Rx Descriptor fetch TPH EN field in
                                                                                          TPH_RXCTRL.

 Transmit packet read                    TPH_TXCTRL.CPUID2          TPH_CTRL.DATA_PH3     Tx Packet TPH EN field in TPH_TXCTRL.

1.   The driver should always set bits [7:3] to zero and place Socket ID in bits [2:0].
2.   Default is 00b (Bidirectional data structure).
3.   Default is 10b (Target).
4.   The hints are always zero.

333369-009                                                                                                                      473
                                         Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                                Inline Functions
