## 14.7 Thermal Specifications

Important:     Information contained in this section is preliminary and subject to change without notice.
To ensure proper operation of the X550, the thermal solution must maintain a case temperature at or
below the values listed in Table 14-2. System-level or component-level thermal enhancements are
required to dissipate the generated heat to ensure the case temperature never exceeds the maximum
temperatures listed in Table 14-2. Table 14-1 lists the thermal performance parameters per JEDEC
JESD51-2 standard. In Table 14-1 the JA values should be used as reference only and can vary by
system environment. JT values also can vary by system environment, and are listed in Table 14-1 as
the maximum value for the X550 simulations.
Analysis indicates that real applications are unlikely to cause the X550 to be at Tcase-max for sustained
periods of time, given that Tcase should reasonably be expected to be a distribution of temperatures.
Sustained operation at Tcase-max might affect long-term reliability of the X550 and the system. Also,
sustained operation at Tcase-max should be evaluated during the thermal design process and steps
taken to further reduce the Tcase temperature.
Good system airflow is critical to dissipate the highest possible thermal power. The size and number of
fans, vents, and/or ducts as well as their placement in relation to components and airflow channels
within the system determine airflow. Acoustic noise constraints might limit the size and types of fans,
vents and ducts that can be used in a particular design.

333369-009                                                                                            1177
                                 Did this document help answer your questions?

                                                                                 Intel® Ethernet Controller X550 Datasheet
                                                                                         Thermal Design Recommendations

To develop a reliable, cost-effective thermal solution, all of the system variables must be considered.
Use system-level thermal characteristics and simulations to account for individual component thermal
requirements.

Table 14-1. Package Thermal Characteristics in Standard JEDEC Environment for Reference
                Package                                  JA (°C/W)                                JT (°C/W)

 25 mm FCBGA without IHS1                                   16.52                                      N/A
                               3                            7.514                                     0.175
 25 mm FCBGA without IHS –HS

 17 mm FCBGA without IHS1                                    TBD                                       N/A
                               3
 17 mm FCBGA without IHS -HS                                7.51                                       0.17

1. Integrated Heat Spreader. the X550 is bare die.
2. Integrated Circuit Thermal Measurement Method-Electrical Test Method EIA/JESD51-1, Integrated Circuits Thermal Test Method
   Environmental Conditions - Natural Convection (Still Air), No Heat sink attached EIAJESD51-2.
3. Heat sink dimensions are specified in Section 14.9.3.
4. Natural Convection (Still Air), Heat sink attached.
5. Psi_JT is given as maximum value for a worst-case X550 scenario and might vary to a lesser value in some scenarios.

Table 14-2. The X550 Absolute Thermal Maximum Rating (°C)
               Application                          Estimated TDP (W)1                          Tcase Max2 (°C)3

                  X550                              11.5 W @ 105 Tj max                                103

1. Power value listed here is estimated maximum power, also known as TDP. TDP is a system design target associated with the
   maximum component operating temperature specifications. Maximum power values are determined based on typical DC electrical
   specification and maximum ambient temperature for a worst-case realistic application running at maximum utilization.
2. Tcase Max-hs is defined as the maximum case temperature with the default enhanced thermal solution attached.
3. This is a not to exceed maximum allowable case temperature.

### 14.7.1 Case Temperature

The X550 is designed to operate properly as long as the Tcase rating is not exceeded. Section 14.10.1
discusses proper guidelines for measuring the case temperature.
