## 14.9 Thermal Enhancements

Important:    Information contained in this section is preliminary and subject to change without notice.
One method frequently used to improve thermal performance is to increase the device surface area by
attaching a metallic heat sink to the component top. Increasing the surface area of the heat sink
reduces the thermal resistance from the heat sink to the air, which increases heat transfer.

### 14.9.1 Clearances

To be effective, a heat sink should have a pocket of air around it that is free of obstructions. Though
each design can have unique mechanical restrictions, the recommended clearances for a heat sink used
with the X550 are shown in Figure 14-1 assuming one of the 40 x 40 mm reference heat sinks is
selected. Retention clip selection is open, and example keep-outs and board through holes are shown in
Figure 14-1 and Figure 14-2 for a torsion retention clip.

Figure 14-1. X550 Heat Sink Keep Out Restrictions (Top Side Keep Out)

1180                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Thermal Design Recommendations

Figure 14-2. X550 Heat Sink Keep Out Restrictions (Bottom Side Keep Out)

### 14.9.2 Default Enhanced Thermal Solution

If you have no control over the end-user's thermal environment, or if you wish to bypass the thermal
modeling and evaluation process, use the default enhanced thermal solutions (see Figure 14-2 and
Figure 14-3). These solutions replicate the performance listed in Figure 14-3 at the TDP. If, after
implementing the recommended enhanced thermal solution, the case temperature continues to exceed
allowable values, additional cooling is needed. This additional cooling can be achieved by improving
airflow to the component and/or adding additional thermal enhancements.

333369-009                                                                                      1181
                                 Did this document help answer your questions?

                                                                                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                                                                                               Thermal Design Recommendations

### 14.9.3 Extruded Heat Sinks

If required, the following extruded heat sinks are the suggested X550 thermal solutions (Figure 14-3).
Also, see Figure 14-1and Figure 14-2 for heat sink information.

                                                       &                                                                                                     ;
                                                                                                                                                           ,11(5),16
                                                                                                                                                                          ;
                                                                                                                                                                         287(5),16

                                                                                                                                                    ;

                                                       5;            $
       $

                                                                                                                 
;
                                                                                               

                                              

                                                       5;
                                                                                                                                                        '(7$,/$
                                                                                                                                                         6&$/(


                                                                      
                                 ;

                                                                 

                                                       
                        


   %
           ;

                                                                                     

                                                                                                        

                                                                                                                              
           ;

                                                                
                                                                                                  ;
                                                                                   6,=(72),7)$67(1(562/87,21

                                                       &

Figure 14-3. X550 Extruded Heat Sink

1182                                                                                                                                                                    333369-009
                                                                 Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Thermal Design Recommendations

### 14.9.4 Attaching the Extruded Heat Sink

The extruded heat sink can be attached using clips or pins with a phase change thermal interface
material.

#### 14.9.4.1 Clips

A well-designed clip, in conjunction with a thermal interface material (tape, grease, etc.) often offers
the best combination of mechanical stability and rework ability. Use of a clip requires significant
advance planning as mounting holes are required in the PCB.

#### 14.9.4.2 Thermal Interface (PCM45 Series)

The recommended thermal interface is PCM45 Series from Honeywell*. The PCM45 Series thermal
interface pads are phase change materials formulated for use in high performance devices requiring
minimum thermal resistance for maximum heat sink performance and component reliability. These
pads consist of an electrically non-conductive, dry film that softens at device operating temperatures
resulting in greasy-like performance. However, Intel has not fully validated the PCM45 Series TIM.
Each PCA, system and heat sink combination varies in attach strength. Carefully evaluate the reliability
of double sided thermal interface tape attachments prior to high-volume use (see Section 14.9.5).

#### 14.9.4.3 Avoid Damaging Die-side Capacitors with Heat Sink

                      Attach
Capacitors on the die side are not protected and can be damaged during heat sink attach. If the heat
sink is tilted from the die, it is possible that the heat sink will make contact with the capacitors prior to
making contact with the package substrate. Figure 14-4 shows how the capacitors can be exposed to
heat sink contact by drawing a plane from the die edge to the substrate edge. Figure 14-5 shows an
example of the damage caused by heat sink contact. It is recommended that heat sinks be attached
vertically, with the heat sink bottom surface parallel to the die surface to avoid contact with the
capacitors.

Figure 14-4. Die-Side Capacitors Exposed to Heat Sink Contact

333369-009                                                                                               1183
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                            Thermal Design Recommendations

Figure 14-5. Damage Caused by Heat Sink Contact

#### 14.9.4.4 Maximum Static Normal Load

The X550 has a bare die that is capable of sustaining a maximum static normal load of 15 lbf (67N).
This load is a uniform compressive load in a direction perpendicular to the die top surface. This
mechanical load limit must not be exceeded during heat sink installation, mechanical stress testing,
standard shipping conditions, and/or any other use condition. Note that the heat sink attach solution
must not include continuous stress to the package, with the exception of a uniform load to maintain the
heat-sink-to-package thermal interface. This load specification is based on limited testing for design
characterization, and is for the package only.

1184                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Thermal Design Recommendations

### 14.9.5 Reliability

Each PCA, system and heat sink combination varies in attach strength and long-term adhesive
performance. Carefully evaluate the reliability of the completed assembly prior to high-volume use.
Some reliability recommendations are listed in Table 14-4.

Table 14-4. Reliability Validation
            Test1                                  Requirement                                      Pass/Fail Criteria2

 Mechanical Shock          50 G trapezoidal, board level                                   Visual and Mechanical Check.
                           11 ms, 3 shocks/axis

 Random Vibration          7.3 G, board level                                              Visual and Mechanical Check.
                           45 minutes/axis, 50 to 2000 Hz

 High-Temperature Life     85 °C                                                           Visual and Mechanical Check.
                           2000 hours total
                           Checkpoints occur at 168, 500, 1000, and 2000 hours

 Thermal Cycling           Per-target environment                                          Visual and Mechanical Check.
                           (for example: -40 °C to +85 °C)
                           500 cycles

 Humidity                  85% relative humidity                                           Visual and Mechanical Check.
                           85 °C, 1000 hours

1. These tests were performed on a sample size of at least 12 assemblies from 3 lots of material (total = 36 assemblies).
2. Additional pass/fail criteria can be added at your discretion.

### 14.9.6 Thermal Interface Management for Heat Sink

                     Solutions
To optimize the X550 heat sink design, it is important to understand the interface between the silicon
die and the heat sink base. Thermal conductivity effectiveness depends on the following:
 • Bond line thickness.
 • Interface material area.
 • Interface material thermal conductivity.

#### 14.9.6.1 Bond Line Management

The gap between the silicon die and the heat sink base impacts heat sink solution performance. The
larger the gap between the two surfaces, the greater the thermal resistance. The thickness of the gap is
determined by the flatness of both the heat sink base and the silicon die, plus the thickness of the
thermal interface material (for example, PSA, thermal grease, epoxy) used to join the two surfaces.

#### 14.9.6.2 Interface Material Performance

The following factors impact the performance of the interface material between the silicon die and the
heat sink base:
 • Thermal resistance of the material.
 • Wetting/filling characteristics of the material.

333369-009                                                                                                                  1185
                                      Did this document help answer your questions?

                                                                       Intel® Ethernet Controller X550 Datasheet
                                                                               Thermal Design Recommendations

14.9.6.2.1            Thermal Resistance of the Material

Thermal resistance describes the ability of the thermal interface material to transfer heat from one
surface to another. The higher the thermal resistance, the less efficient the heat transfer. The thermal
resistance of the interface material has a significant impact on the thermal performance of the overall
thermal solution. The higher the thermal resistance, the larger the temperature drop required across
the interface.

14.9.6.2.2            Wetting/Filling Characteristics of the Material

The wetting/filling characteristic of the thermal interface material is its ability to fill the gap between the
silicon die top surface and the heat sink. Since air is an extremely poor thermal conductor, the more
completely the interface material fills the gaps, the lower the temperature-drop across the interface,
increasing the efficiency of the thermal solution.
