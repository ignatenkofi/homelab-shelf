## 13.3 Connecting the Power Supply Delivery

               Network
For the X550, it is necessary to provide an adequate power supply delivery network such that the
performance of the device meets expected performance requirements. To achieve this goal, both high
speed and bulk decoupling capacitor networks are required in the design to ensure that frequency
performance of the power supply delivery network is flat across the frequency spectrum. For details on
how many high frequency and bulk decoupling capacitors are necessary to achieve this requirement
along with the associated values of these capacitors, refer to the X550 10GBASE-T Dual Port Ethernet
Controller Reference Design schematics.
To further ensure that these specific high frequency and bulk decoupling capacitors are placed in
locations around and under the X550, Figure 13-7 breaks out the five required voltage supplies and
color codes them according to power supply domain as a potential reference placement. Around the
outside of the X550, highlighted bulk decoupling capacitors can be seen and because of their
capacitance value and relative size, should be placed outside the BGA landing pattern. These decoupling
capacitors still provide efficient bulk decoupling performance, as their capacitance value, along with the
inductance of copper connecting them, still perform optimally.

                                                                                         3P3V

                                                                                         2P1V

                                                                                         1P2V

                                                                                         0P85V

                                                                                         0P85V

Figure 13-7. Power Supply Delivery Network

333369-009                                                                                            1149
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                           Design Considerations and Guidelines

Within the BGA landing pattern it is recommended that the high speed decoupling capacitors be placed
directly below the X550 on the secondary side of the PCB to ensure a low inductance path connection.
For each power supply domain, the associated high speed decoupling capacitors should be placed in a
way to provide coverage for all BGA locations. It is not Intel’s recommendation that each power supply
domain ball have a unique high-speed decoupling capacitor, but rather that the high speed decoupling
capacitors required from the reference schematic for each power supply domain provide consistent
coverage across the targeted BGA connection locations.
