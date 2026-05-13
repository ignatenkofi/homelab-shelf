## 3.3 V should be powered on at 90% before any other rails.

The following power-up sequence is recommended for the X550.

         XTAL-Ref Clock (50MHz)

             3.3V

                             1

             2.1V
                                            5

                                  2

             1.2V

                                      3

             0.83V

                                                                                                              6

Figure 12-1. Power On/Off Sequence Flow

Table 12-1. Notes for Power On/Off Sequence Diagram
  Note                                                             Description

# 1 The 2.1 V rail does not start to ramp before the 3.3 V rail is 80% of its final value.

# 2 The 1.2 V rail does not start to ramp before the 2.1 V rail is 80% of its final value. Tmax(2.1 V to 1.2 V) should be less

           than 5 ms.

# 3 The 0.83 V rail does not start to ramp before the 1.2 V rail is 80% of its final value.

# 4 Tramp for each power rail. as defined in Section 12.3.3 through Section 12.3.6.

# 5 Total power-up time from the start of the 3.3 V rail raising until the 0.83 V rail gets to its final level is < 170 ms.

# 6 When powering off, all power rails must get to a 0 V level within 20 ms from the point the first power rail starts powering

           off.

### 12.3.8 Power On Reset

The X550 internal power-on reset circuitry initiates a full chip reset when voltage levels of power
supplies reach certain thresholds at power-up.

                                                                                          Specification
        Symbol                            Parameter                                                                            Units
                                                                               Min             Typ                Max
