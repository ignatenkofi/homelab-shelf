## 3.3 Network Controller — Sideband Interface

              (NC-SI)
The NC-SI interface in the X550 is a connection to an external MC. It operates as a single interface with
an external BMC, where all traffic between the X550 and the BMC flows through the interface.
The X550 NC-SI interface meets the NC-SI version 1.0.0 specification as a PHY-side device.

### 3.3.1 Electrical Characteristics

The X550 complies with the electrical characteristics defined in the NC-SI specification.

### 3.3.2 NC-SI Transactions

The NC-SI link supports both pass-through traffic between the BMC and the X550 LAN functions, as well
as configuration traffic between the BMC and the X550 internal units as defined in the NC-SI protocol.
Refer to Section 11.6.2 for information.

94                                                                                                 333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Interconnects

### 3.3.3 MCTP (Over PCIe or SMBus)

The X550 supports MCTP protocol for management. MCTP runs over PCIe or SMBus. The X550
implements NC-SI over MCTP protocol for command and pass-through traffic. See Section 11.7 for
details.
