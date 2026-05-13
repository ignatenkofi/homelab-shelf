## 13.7 Connecting the Light Emitting Diodes (LEDs)

The X550 provides four programmable high-current sink (active high) outputs per port to directly drive
LEDs for link activity and speed indication. Each LAN device provides an independent set of LED
outputs; these pins and their function are bound to a specific LAN device. Each of the four LED outputs
can be individually configured to select the particular event, state, or activity, which is indicated on that
output. In addition, each LED can be individually configured for output polarity, as well as for blinking
versus non-blinking (steady-state) indication.
The LED ports are fully programmable through the Flash interface (LEDCTL register). In addition, the
hardware-default configuration for all LED outputs can be specified via a Flash field, thus supporting
LED displays configurable to a particular OEM preference.
Provide separate current limiting resistors for each LED connected.

1154                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

Since the LEDs are likely to be placed close to the board edge and to external interconnect, take care to
route the LED traces away from potential sources of EMI noise. In some cases, it might be desirable to
attach filter capacitors.
