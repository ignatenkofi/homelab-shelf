## 13.12 PCB Guidelines

This section describes the general PCB design guidance targeted as supplementary information in
addition to the specific requirements and recommendations for individual interfaces. For items not
directly covered in the specific interface sections, these guidance recommendations apply to the design.

### 13.12.1 Board Stack-Up Example

PCBs for these designs typically have six, eight, or more layers. Although the X550 does not dictate
stackup, the following examples show typical stack-up options.
Microstrip Example:
 • Layer 1 is a signal layer.
 • Layer 2 is a ground layer.
 • Layer 3 is used for power planes.
 • Layer 4 is a signal layer. Careful routing is necessary to prevent crosstalk with layer 5.
 • Layer 5 is a signal layer. Careful routing is necessary to prevent crosstalk with layer 4.
 • Layer 6 is used for power planes.
 • Layer 7 is a signal ground layer.
 • Layer 8 is a signal layer.
Note:        Layers 4 and 5 should be used mostly for low-speed signals because they are referenced to
             potentially noisy power planes that might also be slotted.
Stripline Example:
 • Layer 1 is a signal layer.
 • Layer 2 is a ground layer.
 • Layer 3 is a signal layer.
 • Layer 4 is used for power planes.
 • Layer 5 is used for power planes.
 • Layer 6 is a signal layer.
 • Layer 7 is a signal ground layer.
 • Layer 8 is a signal layer.
Note:        To avoid the effect of the potentially noisy power planes on the high-speed signals, use offset
             stripline topology. The dielectric distance between the power plane and signal layer should be
             three times the distance between ground and signal layer.
This board stack-up configuration can be adjusted to conform to company-specific design rules.

333369-009                                                                                              1161
                                  Did this document help answer your questions?

                                                      Intel® Ethernet Controller X550 Datasheet
                                                           Design Considerations and Guidelines

### 13.12.2 Customer Reference Board Stack-Up Example

1162                                                                                333369-009
                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

### 13.12.3 Intel Reference Board Stack-Up Example

333369-009                                                                       1163
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                Design Considerations and Guidelines

### 13.12.4 Via Usage

Use vias to optimize signal integrity. Figure 13-13 shows correct via usage. Figure 13-14 shows the
type of topology that should be avoided.

Figure 13-13. Correct Via Usage

                                            Incorrect via usage creating
                                                large electrical stub.

Figure 13-14. Incorrect Via Usage

Any via stubs on the MDI differential signal traces must be less than 35 mils in length. Keeping MDI
signal via stubs less than or equal to 20 mils is preferable.
Place ground vias adjacent to signal vias used for the MDI interface. DO NOT embed vias between the
high-speed signals, but place them adjacent to the signal vias. This helps to create a better ground
path for the return current of the AC signals, which also helps address impedance mismatches and EMC
performance.
It is recommend that, in the breakout region between the via and the capacitor pad, target a Z0 for the
via to capacitor trace equal to 50 . This minimizes impedance imbalance.

1164                                                                                                     333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

                                                                 Incorrect usage of
                                                                 via buried between
                                                                 differential signals

Figure 13-15. Incorrect Via Usage for Differential Pair

### 13.12.5 Reference Planes

Do not cross plane splits with the MDI high-speed differential signals. This causes impedance
mismatches and negatively affects the return current paths for the board design and layout. See
Figure 13-16.

                                                                 Differential signals should
                                                                 not cross splits in either
                                                                 GND or PWR plane
                                                                 reference.

Figure 13-16. Improper Differential Signal Routing - Plane Split

Traces should not cross power or ground plane splits if at all possible. Traces should stay seven times
the dielectric height away from plane splits or voids. If traces must cross splits, capacitive coupling
should be added to stitch the two planes together to provide a better AC return path for the high-speed
signals. To be effective, the capacitors should be have low ESR and low equivalent series inductance.

333369-009                                                                                         1165
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                          Design Considerations and Guidelines

Note:     Even with plane split stitching capacitors, crossing plane splits is extremely high risk for
          10GBASE-T designs.

                              Differential signals should be > 6
                              x dielectric height away from
                              PWR and GND plane splits.

Figure 13-17. Differential Signal Routing - Plane split and Void Proximity

It is recommended that the MDI signals stay at least seven times the dielectric height away from any
power or ground plane split. This improves impedance balance and return current paths.
If a high-speed signal needs to reference a power plane, ensure that the height of the secondary
(power) reference plane is at least 3 x the height of the primary (ground) reference plane.

### 13.12.6 Reducing Circuit Inductance

Traces should be routed over a continuous reference plane with no interruptions. If there are vacant
areas on a reference or power plane, the signal conductors should not cross the vacant area. Routing
over a void in the reference plane causes impedance mismatches and usually increases radiated noise
levels. Noisy logic grounds should NOT be located near or under high-speed signals or near sensitive
analog pin regions of the LAN silicon. If a noisy ground area must be near these sensitive signals or IC
pins, ensure sufficient decoupling and bulk capacitance in these areas. Noisy logic and switching power
supply grounds can sometimes affect sensitive DC subsystems such as analog to digital conversion,
operational amplifiers, etc.

1166                                                                                               333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

All ground vias should be connected to every ground plane; and similarly, every power via should be
equally potential power planes. This helps reduce circuit inductance. Another recommendation is to
physically locate grounds to minimize the loop area between a signal path and its return path. Rise and
fall times should be as slow as possible while still meeting the relevant electrical requirements because
signals with fast rise and fall times contain many high frequency harmonics, which can radiate
significantly. The most sensitive signal returns closest to the chassis ground should be connected
together. This results in a smaller loop area and reduces the likelihood of crosstalk. The effect of
different configurations on the amount of crosstalk can be studied using electronics modeling and
simulation software.

### 13.12.7 Signal Isolation

To maintain the best signal integrity, keep digital signals far away from the analog traces. A good rule to
follow is no digital signal should be within 7x to 10x dielectric height of the differential pairs. If digital
signals on other board layers cannot be separated by a ground plane, they should be routed at a right
angle (90 degrees) to the differential signal traces. If there is another Ethernet controller on the board,
take care to keep the differential pairs away from that circuit. The same thing applies to switching
regulator traces.
Rules to follow for signal isolation:
 • Separate and group signals by function on separate board layers if possible. Maintain a separation
   that is at least seven times the thinnest adjacent dielectric height between all differential pairs
   (Ethernet) and other nets, but group associated differential pairs together.
 • Over the length of the trace run, each differential pair should be at least seven times the thinnest
   adjacent dielectric height away from any parallel signal traces.
 • Physically group together all components associated with one clock trace to reduce trace length and
   radiation.
 • Isolate other I/O signals from high-speed signals to minimize crosstalk. Crosstalk can increase
   radiated EMI and can also increase susceptibility to EMI from other signals.
 • Avoid routing high-speed LAN traces near other high-frequency signals associated with a video
   controller, cache controller, processor, or other similar devices.

### 13.12.8 Traces for Decoupling Capacitors

Traces between decoupling and I/O filter capacitors should be as short and wide as practical. Long and
thin traces are more inductive and reduce the intended effect of decoupling capacitors. Also, for similar
reasons, traces to I/O signals and signal terminations should be as short as possible. Vias to the
decoupling capacitors should be sufficiently large in diameter to decrease series inductance.

333369-009                                                                                                1167
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                          Design Considerations and Guidelines

### 13.12.9 Power and Ground Planes

Good grounding requires minimizing inductance levels in the interconnections and keeping ground
returns short, signal loop areas small, and locating decoupling capacitors at or near power inputs to
bypass to the signal return. This significantly reduces EMI radiation.
These guidelines reduce circuit inductance in NICs and LOMs:
 • Route traces over a continuous plane with no interruptions. Do not route over a split power or
   ground plane. If there are vacant areas on a ground or power plane, avoid routing signals over the
   vacant area. Routing signals over power or ground voids increases inductance and increases
   radiated EMI levels.
 • Use distance and/or extra decoupling capacitors to separate noisy digital grounds from analog
   grounds to reduce coupling. Noisy digital grounds can affect sensitive DC subsystems.
 • All ground vias should be connected to every ground plane, and every power via should be
   connected to all power planes at equal potential. This helps reduce circuit inductance.
 • Physically locate grounds between a signal path and its return. This minimizes the loop area.
 • Avoid fast rise/fall times as much as possible. Signals with fast rise and fall times contain many high
   frequency harmonics, which can radiate EMI.
 • Do not route high-speed signals near switching regulator circuits.
 • It’s acceptable to put ground fill or thieving on the trace layers, but preferably not closer than 50
   mils to the differential traces and the connector pins.
 • If differential traces must be routed on another layer, the signal vias should carry the signal to the
   opposite side of the PCB (to be near the top of the PCB), AND if the high-speed signals are being
   routed between two connectors on the same board, before the signal traces reach the second
   connector, they must return to the original signal layer (before reaching the connector pin). This
   strategy keeps via stubs short without requiring back drilling.
 • Each time differential traces make a layer transition (pass through a pair of signal vias), there must
   be at least one ground via located near each signal via. Two ground vias near each signal via is
   better. See Figure 13-18 and Figure 13-19.

1168                                                                                               333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

                                                                         GND vias
                                                                         are located
                                                                         near each
                                                                         signal via to
                                                                         improve the
                                                                         current
                                                                         return path.

Figure 13-18. Return Path Vias for Differential Signals - Acceptable Example

333369-009                                                                               1169
                                 Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                Design Considerations and Guidelines

                   GND vias are                                                     GND vias are
                   located near                                                     located near each
                   each signal                                                      signal via to
                   via to improve                                                   improve the
                   the current                                                      current return
                   return path                                                      path.

Figure 13-19. Return Path Vias for Differential Signals - Optimal Example

If the PCB fabrication process permits it, it’s best to remove signal via pads on unconnected metal
layers. See Figure 13-20 and Figure 13-21.

                                                   The unused via pads have not been
                                                   removed, and could degrade signal quality.

Figure 13-20. Signal Vias: Improper Padstack Example

1170                                                                                                     333369-009
                                    Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

                                                  The unused via pads degrade the signal
                                                  integrity of the signal path and have been
                                                  removed.

Figure 13-21. Signal Vias: Optimal Padstack

On metal layers where signal vias need to have via pads, it is desirable to reduce capacitance between
the signal vias and ground-plane layers. The anti-pad diameters should be up to 20 mils larger than the
via pad diameters. See Figure 13-22. Clearance between the pad and the surrounding metal should be
>= 10 mils.

                                                                      Via anti-pad

                                                                       Via pad

                                            Anti-pad diameter = Via
                                            pad diameter + 20 mils

Figure 13-22. Anti-Pad Geometry

Each time differential signal vias pass through a plane layer, within each differential pair, the anti-pads
should overlap. See Figure 13-23, Figure 13-24 and Figure 13-25.

333369-009                                                                                             1171
                                 Did this document help answer your questions?

                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                        Design Considerations and Guidelines

                                            Via anti-pad

                                               Via pad

                                        Differential via pads
                                      should not be separated
                                              by metal.

Figure 13-23. Differential Signal Vias: Improper Anti-pad Geometry

                                             Via anti-pad
                                               Via pad

                                      Better differential signal
                                        anti-pad via usage.

Figure 13-24. Differential Signal Vias: Acceptable Example

1172                                                                                             333369-009
                           Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

                                                   Via anti-pad
                                                     Via pad

                                             Best differential signal
                                              anti-pad via usage.

Figure 13-25. Differential Signal Vias: Optimal Example

### 13.12.10 Recommended Simulations

10GBASE-T signaling frequencies have frequency content in the range of 800 MHz and below so
relatively short stubs, small discontinuities, and fairly small in-pair trace length differences can cause
an undesirable increase in bit errors. Before ordering PCBs, verify that:
 • Planned 10GBASE-T signal trace routing on the PCB complies with the interconnect characteristics
   recommended in IEEE 802.3an.
 • With sufficient advance notice, Intel engineers can provide assistance under these conditions:
     — Trace routing should be optimized prior to the next steps – request a layout review (must be
       willing to provide board stack-up information and the MDI traces CAD artwork).
     — After MDI traces have been optimized, if the IEEE recommended electrical characteristics are
       still not being met, end-to-end MDI board channels S-parameter models should be extracted
       (preferably in Touchstone* S4p format) for additional investigative simulations by Intel signal
       integrity engineers. Please request the required S-parameter frequency range, step size, etc.,
       before extracting Touchstone S-parameter models.

333369-009                                                                                             1173
                                 Did this document help answer your questions?

                                                                   Intel® Ethernet Controller X550 Datasheet
                                                                        Design Considerations and Guidelines
