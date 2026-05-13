## 12.6 Crystal Specification

            Parameter Name                        Symbol                    Recommended Value        Conditions

Frequency                                 fo                     50.000 MHz                      @25 °C

Vibration Mode                                                   Fundamental

Cut                                                              AT

Operating /Calibration Mode                                      Parallel

Frequency Tolerance @25 °C                Df/fo @25 °C           ±10 ppm / ±15 ppm (see note)    @25 °C

Temperature Tolerance                     Df/fo                  ±10 ppm ±15 ppm (see note)

Operating Temperature                     Topr                   0 to +70 °C

Non Operating Temperature Range           Topr                   -40 to +90 °C

Equivalent Series Resistance (ESR)        Rs                     50  maximum                    @50 MHz

Load Capacitance                          Cload                  16 pF

Shunt Capacitance                         Co                     <5 pF maximum

Max Drive Level                           DL                     300 W

Insulation Resistance                     IR                     500 M minimum                  @ 100 Vdc

Aging                                     Df/fo                  (±5 ppm/year) / (±2 ppm/year)
                                                                 (see note)

CL1/CL2                                                          18 pF

Note: To provide some flexibility in the Bill Of Materials (BOM), two options are supported:
 1. Crystal parameters option 1:
    a. Frequency tolerance @ 25 °C ±15 ppm
    b. Temperature tolerance ±15 ppm
    c. Aging ±2 ppm/year
 2. Crystal parameters option 2:
    a. Frequency tolerance @ 25 °C ±10 ppm
    b. Temperature tolerance ±10 ppm
    c. Aging ±5 ppm/year

                           CL1
                                                                                 XTAL_I

    50 MH z                           X550

                           CL2                    R – 0 ohm
                                                                                 X T A L _O

Figure 12-8. Crystal Specification Schematic

333369-009                                                                                                        1133
                                     Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                               Electrical/Mechanical Specification
