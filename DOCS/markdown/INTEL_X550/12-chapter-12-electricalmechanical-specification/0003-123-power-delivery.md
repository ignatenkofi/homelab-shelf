## 12.3 Power Delivery

### 12.3.1 Power Delivery Definitions

 • DC Voltage Regulation — DC accuracy with respect to the nominal voltage specification. Includes
   controller feedback accuracy and resistive losses in the power distribution network.
 • AC Voltage Regulation — Minimum/maximum noise voltage based on mid-to-high frequency
   (~1-20 MHz) AC load currents (excluding ripple voltage). Note that this specification is met by
   following the system design recommendations/considerations related to the recommended
   decoupling design (see Chapter 13, “Design Considerations and Guidelines”).
 • Total Line Regulation — The sum of DC and AC voltage regulation.

### 12.3.2 Power Supply Specifications

                          Description                                               Parameter

                                                      VCC3P3V

Nominal Voltage                                            3.3 V

DC Voltage Regulation                                      ± 5% DC Regulation

AC Voltage Regulation                                      ± 4% AC Regulation (132 mV Pk-Pk)

Total Line Regulation                                      ± 9%

                                                      VCC2P1

Nominal Voltage                                            2.1 V

DC Voltage Regulation                                      ± 3% DC Regulation

AC Voltage Regulation                                      ± 0.6% AC Regulation (13 mV Pk-Pk)

Total DC/AC Voltage Regulation                             ± 3.6%

Step Load Size                                             64 mA

Step Load Slew Rate di/dt                                  200 mA/1 s

                                                      VCC1P2

Nominal Voltage                                            1.2 V

DC Voltage Regulation                                      ± 3% DC Regulation

AC Voltage Regulation                                      ± 2% AC Regulation (24 mV Pk-Pk)

Total DC/AC Voltage Regulation                             ± 5%

Step Load Size                                             125 mA

Step Load Slew Rate di/dt                                  125 mA/1 s

                                                      VCC0P83

Nominal Voltage                                            0.83 V

DC Voltage Regulation                                      ± 3% DC Regulation

AC Voltage Regulation                                      ± 2% AC Regulation (16.6 mV Pk-Pk)

1114                                                                                                      333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

                          Description                                                    Parameter

Total DC/AC Voltage Regulation                                      ± 5%

Step Load Size                                                      2A

Step Load Slew Rate di/dt                                           587 mA/1 s

### 12.3.3 VCC3P3 External Power Supply Specification

                    (3.3 V)

        Parameter                                     Description                           Min      Max     Units

Rise Time                   Time from 10% to 90% mark.                                       0.1      50      ms

Monotonicity                Voltage dip allowed in ramp.                                     N/A       0      mV

Slope                       Ramp rate at any given time between 10% and 90%.                 48      28800   V/S
                             Min = 0.8*V(min)/rise time (max)
                             Max = 0.8*V(max)/rise time (min)

Operational Range           Voltage range for normal operating conditions.                    3       3.6     V

Overshoot                   Maximum overshoot allowed.                                       N/A     100      mV

Overshoot Settling Time     Maximum overshoot allowed duration.                              N/A     0.05     ms
                            Note: At that time delta voltage should be lower than 5 mV
                                  from steady state voltage.

Suggested Decoupling        Capacitance range.                                               25       N/A     F
Capacitance

### 12.3.4 VCC2P1 External Power Supply Specification

                    (2.1 V)

            Title                                     Description                           Min      Max     Units

Rise Time                   Time from 10% to 90% mark.                                       0.1      50      ms

Monotonicity                Voltage dip allowed in ramp.                                     N/A       0      mV

Slope                       Ramp rate at any given time between 10% and 90%                  32      17600   V/S
                             Min = 0.8*V(min)/rise time (max)
                             Max = 0.8*V(max)/rise time (min)

Operational Range           Voltage range for normal operating conditions.                   2.0      2.2     V

Overshoot                   Maximum overshoot allowed.                                       N/A     100      mV

Overshoot Settling Time     Maximum overshoot allowed duration.                              N/A      0.1     ms
                            Note: At that time delta voltage should be lower than 5 mV
                                  from steady state voltage.

Suggested Decoupling        Capacitance range.                                               200      N/A     F
Capacitance

333369-009                                                                                                         1115
                                       Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                    Electrical/Mechanical Specification

### 12.3.5 VCC1P2 External Power Supply Specification

                     (1.2 V)

            Title                               Description                             Min        Max        Units

Rise Time              Time from 10% to 90% mark.                                       0.1         50         ms

Monotonicity           Voltage dip allowed in ramp.                                     N/A          0         mV

Slope                  Ramp rate at any given time between 10% and 90%                  18        10080        V/S
                        Min = 0.8*V(min)/rise time (max)
                        Max = 0.8*V(max)/rise time (min)

Operational Range      Voltage range for normal operating conditions.                  1.14        1.26         V

Overshoot              Maximum overshoot allowed.                                       N/A         60         mV

Overshoot Duration     Maximum overshoot allowed duration.                              0.0        0.05        ms
                       Note: At that time delta voltage should be lower than 5 mV
                             from steady state voltage.

Suggested Decoupling   Capacitance range.                                               200        N/A          F
Capacitance

### 12.3.6 VCC0P83 External Power Supply Specification

                     (0.83 V)

            Title                               Description                             Min        Max        Units

Rise Time              Time from 10% to 90% mark.                                       0.1         20         ms

Monotonicity           Voltage dip allowed in ramp.                                     N/A          0         mV

Slope                  Ramp rate at any given time between 10% and 90%                  13         7136        V/S
                        Min = 0.8*V(min)/rise time (max)
                        Max = 0.8*V(max)/rise time (min)

Operational Range      Voltage range for normal operating conditions.                  0.788      0.871         V

Overshoot              Maximum overshoot allowed.                                       N/A         40         mV

Overshoot Duration     Maximum overshoot allowed duration.                              N/A        0.05        ms
                       Note: At that time delta voltage should be lower than 5 mV
                             from steady state voltage.

Suggested Decoupling   Capacitance range.                                               500        N/A          F
Capacitance

1116                                                                                                       333369-009
                                  Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Electrical/Mechanical Specification

### 12.3.7 Power On/Off Sequence
