## 13.1 Connecting the PCIe Interface

The X550 connects to the host system using a PCIe interface. The interface can be configured to
operate in several link modes as detailed in Section 3. A link between the ports of two devices is a
collection of lanes. Each lane has to be AC-coupled between its corresponding transmitter and receiver,
with the AC-coupling capacitor located close to the transmitter side (within 1 inch). Each end of the link
is terminated on the die into nominal 100 differential DC impedance. Board termination is not required.
Refer to the PCI Express* Base Specification, Revision 3.0 and PCI Express* Card Electromechanical
Specification, Revision 2.0.

### 13.1.1 Link Width Configuration

The X550 supports link widths of x8, x4, or x1 as determined by the Flash Lane_Width field in the PCIe
initialization configuration. The configuration is loaded using bits 9:4 in the Max Link Width field of the
Link Capabilities register (0xAC); default setting is 0x08. The X550-AT2 default link width is x4. The
X550-BT2 default link width is x8.
During link configuration, the platform and the X550 negotiate a common link width. For proper
operation, the selected maximum number of PCIe lanes must be connected to the host system.

### 13.1.2 Polarity Inversion and Lane Reversal

To ease routing, designers have the flexibility to the lane reversal modes supported by the X550.
Polarity inversion can also be used, since the polarity of each differential pair is detected during the link
training sequence.
When lane reversal is used, some of the down-shift options are not available. For a description of
available combinations, see Section 3.

333369-009                                                                                               1139
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                         Design Considerations and Guidelines

### 13.1.3 PCIe Reference Clock

The X550 requires a 100 MHz differential reference clock called PE_CLK_p and PE_CLK_n. These signals
are typically generated on the system board and routed to the PCIe connector. For add-in cards, the
clock is furnished at the PCIe connector.
Note:     The frequency tolerance for the PCIe reference clock is +/- 300 ppm.

### 13.1.4 Bias Resistor

For proper biasing of the PCIe analog interface, a 4.75 K 0.1% resistor needs to be connected
between PE_RSENSE and PE_RBIAS. To avoid noise coupled onto this reference signal, place the bias
resistor close to the X550 and keep traces as short as possible.

### 13.1.5 Miscellaneous PCIe Signals

The X550 signals power management events to the system by pulling low the PE_WAKE_N signal. This
signal operates like the PCI PME# signal. Note that somewhere in the system, this signal has to be
pulled high to the auxiliary 3.3 V supply rail.
The PE_RST# signal, which serves as the familiar reset function for the X550, needs to be connected to
the host system’s corresponding signal.

### 13.1.6 PCIe Layout Recommendations

For information regarding the PCIe signal routing, refer to the Intel PCIe Design Guide.
