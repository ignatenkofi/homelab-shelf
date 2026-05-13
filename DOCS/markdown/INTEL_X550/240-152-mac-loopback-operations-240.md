## 15.2 MAC Loopback Operations

Loopback operations are supported by the X550 to assist with system and the X550 debug. Loopback
operation can be used to test transmit and receive aspects of software drivers, as well as to verify
electrical integrity of the connections between the X550 and the system (such as PCIe bus connections,
etc.).

### 15.2.1 Tx->Rx MAC Loopback

This loopback is closed on the internal XGMII interface of the MAC core.
To configure the X550 for Tx->Rx loopback operation:
 • Disable auto-negotiation in PHY register bit 7.0.C.
 • Operate only at 10 GbE speed while no link partner is present. For other speeds, establish the link
   with a link partner at the desired speed while performing Tx -> Rx MAC loopback.
 • In the MACC register, set the FLU bit to 1b to force link up.
 • In the HLREG0 register, set the LPBK bit to 1b.

### 15.2.2 Rx->Tx MAC Loopback

This loopback is closed in the internal XGMII interface.
To configure the X550 for Rx->Tx loopback operation, the MAC_RX2TX_LPBK_EN bit in the MACC
register should be set to 1b.
For loopback to be functional a functional link (with the partner) should be achieved (sync and
alignment).
Link configuration should be done as in regular functional mode (see Section 4.6.3). All link modes can
be configured.
Loopback limitation notes:
 • Short preamble with minimal IPG is not supported with loopback operation.
 • Transmitted data might violate the minimum IPG specification requirements.

1190                                                                                                                333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Diagnostics
