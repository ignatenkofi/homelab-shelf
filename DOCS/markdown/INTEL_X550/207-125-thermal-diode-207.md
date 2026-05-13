## 12.5 Thermal Diode

The X550 incorporates an on-die diode that can be used to monitor the die temperature (junction
temperature). An external thermal sensor located on the motherboard or a stand-alone measurement
device can also be used to monitor the die temperature of the X550 for thermal management or
characterization. Table 12-20 lists the parameters that pertain to the X550's thermal diode pins
(THERM_D1_P, THERM_D1_N).

Table 12-20. Thermal Diode Parameters
       Symbol             Min.          Typical          Max             Unit          Notes

I forward bias             50             100            1000             A              1

n_ideality                1.03            1.05           1.08                             3

ESR                                       2.77                                           2

Notes:
 1. Intel does not support or recommend operation of the thermal diode under reverse bias.
 2. ESR: Effective Series Resistance - needed for various TD measurement tools.
 3. n_ideality is the diode ideality factor parameter, as represented by the diode equation:

Note:        The X550's thermal diode has a -10 °C offset from the Tj at the center of the die. An external
             thermal sensor should add this offset for accurate measurement.

1132                                                                                                              333369-009
                                     Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification
