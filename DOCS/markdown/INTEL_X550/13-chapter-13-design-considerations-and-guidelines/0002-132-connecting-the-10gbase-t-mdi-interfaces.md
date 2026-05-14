## 13.2 Connecting the 10GBASE-T MDI Interfaces

In 10GBASE-T mode, the line interface on the X550 is capable of driving up to 100 meters of CAT-6a
unshielded twisted pair or 100 meters of CAT-7 shield cable (100 Ω differential impedance). It can also
drive 55 meters of CAT-6 cable. In 100BASE-TX and 100MBASE-TX modes, it can drive 130 meters of
CAT-5e (or better) cable. It is designed to drive this via a quad, 50 Ω center tapped 1:1 transformer
connected to an RJ-45 PCB-mount jack. Solutions that combine the transformer and RJ-45 jack into a
single device are also supported.
The line interface on the X550 supports automatic A/B and C/D pair swaps and inversions (MDI-X). It
also supports provisioned ABCD to DCBA pair reversal for ease of routing via an NVM setting, which sets
this configuration at power up.
Note:     This reversal does not swap polarities thus A+ maps to D+, etc.

1140                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

### 13.2.1 MDI Circuit Guidelines

The MDI discrete design and integrated magnetic components were chosen for inclusion in the
reference design and Bill of Material (BOM). Refer to Section 13.13 for more details. These components
are capable of delivering the performance required for this demanding application.

### 13.2.2 Magnetics Module

The magnetics module has a critical effect on overall IEEE and emissions conformance. The X550
should meet the performance required for a design with reasonable margin to allow for manufacturing
variation. Carefully qualifying new magnetics modules prevents problems that might arise because of
interactions with other components or the Printed Circuit Board (PCB) itself. The magnetics specified
should comply with the specifications listed in the Intel® 10-GBASE-T Magnetic Specification Electrical/
Mechanical Requirements for 10GBASE-T Magnetic Components, which includes separate specifications
for discrete and integrated magnetics modules.
These have five channels of 3-wire choke / transformer pairs in them, with four facing the choke
towards the line (RJ45), and one facing the choke towards the X550.
The steps involved in magnetics module qualification are:
1. Verify that the vendor’s published specifications in the component datasheet meet or exceed the
   required IEEE 802.3an specifications and the internal specifications listed in the Intel® 10-GBASE-T
   Magnetic Specification Electrical/Mechanical Requirements for 10GBASE-T Magnetic Components.
2. Independently measure the component’s electrical parameters on a test bench, checking samples
   from multiple lots. Check that the measured behavior is consistent from sample-to-sample and that
   measurements meet the published specifications.
3. Perform physical layer conformance testing and EMC (FCC and EN) testing in real systems. Vary
   temperature and voltage while performing system level tests.
Magnetics modules for 10GBASE-T Ethernet as used by the X550 are similar to those designed for
1GBASE-T, except that the electrical requirements for the board layout and magnetics are more
stringent. Refer to Section 12 for specific electrical requirements that the magnetics need to meet.

13.2.3            5th Channel
To sense and cancel common-mode noise, the X550 provides a 5th channel designed for this purpose.
It is very similar to the receivers on Pairs A - D, with the exception that it does not have a driver and
only receives. Its input impedance is 100 .
When discrete magnetics are in use, this channel should be connected to a common-mode sense point.
In this design, the common-mode sense point is the Bob Smith termination of Pair D. This sense point
is run through a transformer to convert the signal to differential for pick-up by the 5th channel receiver.
To match the 100  impedance of the receiver input with the required 75  Bob Smith termination, a
300  parallel resistor is used.
Integrated magnetics perform the required termination internally. As a result, the Bob Smith
termination used in the discrete case is not necessary.
If a different choice of magnetics is required they should comply with the specifications listed in
Section 13.13.

333369-009                                                                                             1141
                                 Did this document help answer your questions?

                                                                      Intel® Ethernet Controller X550 Datasheet
                                                                           Design Considerations and Guidelines

### 13.2.4 Board Noise Cancellation

An advantage of the 5th channel is that in addition to canceling received common-mode interference
from the line, it also cancels noise picked up on the PCB. This is especially important if the RJ-45 is
located any significant distance from the X550. Consequently, every effort should be made to route the
5th channel traces along the same path as the other four MDI traces.

### 13.2.5 MDI Layout Guidance

The MDI that was chosen for X550 designs consist of an RJ-45 right-angle PCB jack, Bob Smith
termination and discrete magnetics (see Figure 13-1). The magnetics can be implemented either as a
discrete module or an integrated solution combining the magnetics and the RJ-45 jack.
Minimizing the amount of space needed for the PHY is important because other interfaces compete for
physical space on a Network Interface Card (NIC) or LAN on Motherboard (LOM) near the connector.
The PHY circuits need to be as close as possible to the connector.
Figure 13-1 illustrates some basic placement distance guidelines. It shows four differential pairs and
the layout can be generalized for a 10 GbE system with four analog pairs. The ideal placement for the
X550 is approximately two inches behind the magnetics module for both the discrete and integrated
solutions.

#### 13.2.5.1 Discrete Magnetics

The X550 uses a common-mode sensing circuit on the MDI of each channel to cancel in-band common-
mode interference that couples into the differential receive signals. This common-mode sense circuitry
is referred to as the 5th channel. This is where the sense circuitry sits in series with the Bob Smith
termination for Channel D. The signal runs through a transformer to perform the common-to-
differential conversion where it is followed by the X550-facing common-mode choke. This provides
isolation from board noise being radiated on Channel D. In addition, the impedance of the Bob Smith
termination is 75  Channel A, B, C and 300  Channel D, whereas the PHY input impedance is 100 .

                                                                                X550
                                   A                            A
                                   B                            B
                                   C         10GBaseͲT
               RJ45Connector                                   C         Port0MDIInterface
                                   D          Magnetic          D
                                                                E

                                                                A
                                   A                            B
                                   B         10GBaseͲT         C
               RJ45Connector      C                                      Port1MDIInterface
                                              Magnetic          D
                                   D                            E

Figure 13-1. Basic MDI Placement Guidelines

1142                                                                                                333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

The X550, referred as a LAN silicon in Figure 13-2 and Figure 13-3, must be at least 1.5 inches from the
I/O back panel. To help reduce EMI, the following recommendations should be followed:
 • Minimize the length of the MDI interface.
 • Place the MDI traces no closer than 0.5 inch (1.3 cm) from the board edge.

Figure 13-2. Effect of Device Placed Less Than One Inch from the RJ-45 Connector

The associated grounding scheme (blue) with the front-end of the chip is shown in the microstrip traces
between the transformer and the RJ-45 (see Figure 13-3).

Figure 13-3. Transformer Bypass Components

333369-009                                                                                          1143
                                 Did this document help answer your questions?

                                                                    Intel® Ethernet Controller X550 Datasheet
                                                                         Design Considerations and Guidelines

Figure 13-4. MDI Grounds

From these figures (Figure 13-3 and Figure 13-4), the following should be noted:
 • The ground is split underneath the magnetics, with the chassis ground being present under the
   front-end (Figure 13-3), and the circuit ground under the X550 side of the magnetics. Thus, the
   MDI traces on the line side are referenced to chassis ground.
 • The magnetic module is used with the common mode choke facing the X550. This enables a Bob
   Smith termination to be implemented from the line side transformer center taps to chassis ground.
 • Bob Smith termination and the shield of the RJ-45 jack are both connected to chassis ground, which
   are the two large circular metalizations in the MDI (see Figure 13-4).
 • The resistors in the Bob Smith termination are required to be 0805s to handle the cable discharge
   voltages.
 • Similarly, the magnetics should be placed as close as possible to the RJ-45 jack.
 • In Figure 13-3, the Hi-POT clearance for cable discharge is shown and designed with ≥80 mils of
   clearance from the ground. Note that the breakdown voltage in FR-4 is lowest in the x-y axes planar
   to the PCB and highest in the z-axis between layers.

1144                                                                                              333369-009
                              Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

#### 13.2.5.2 Integrated Magnetics

The 5th MDI channel previously described in discrete magnetics implementation is still realized when
using integrated magnetics, with some notable exceptions (see Figure 13-5). The required termination,
reference ground-plane division, and 5th channel wiring to the 4th channel center-tap occur within the
integrated magnetics module. The guidance on MDI trace implementation between the X550 and the
integrated module remains the same as with discrete magnetics, including length requirements and
target impedance.

                                                                                   X550
                                      A                            A
                                      B                            B
                                      C          10GBaseͲT
                  RJ45Connector                                   C         Port0MDIInterface
                                      D           Magnetic         D
                                                                   E

                                                                   A
                                      A                            B
                                      B          10GBaseͲT        C
                  RJ45Connector      C                                      Port1MDIInterface
                                                  Magnetic         D
                                      D                            E

Figure 13-5. Basic MDI Placement Guidelines

Note:        The RJ-45 jack and 10GBase-T Magnetics (red outline) are included in the integrated
             magnetics module.
The differences between the discrete and integrated magnetics implementations are as follows:
 • The ground split that occurs underneath discrete magnetics modules is performed internally when
   using integrated magnetics. As a result, this ground split does not need to be addressed.
 • The required Bob Smith termination is implemented internally when using integrated magnetics.

#### 13.2.5.3 MDI Differential Pair Trace Routing for LAN Design

Trace routing considerations are important to minimize the effects of crosstalk and propagation delays
on sections of the board where high-speed signals exist. Signal traces should be kept as short as
possible to decrease interference from other signals, including those propagated through power and
ground planes.

#### 13.2.5.4 Signal Trace Geometry

One of the key factors in controlling trace EMI radiation are the trace length and the ratio of trace-width
to trace-height above the reference plane. To minimize trace inductance, high-speed signals and signal
layers that are close to a reference or power plane should be as short and wide as practical. Ideally, the
trace-width to trace-height above the ground plane ratio is between 1:1 and 3:1. To maintain trace
impedance, the width of the trace should be modified when changing from one board layer to another if
the two layers are not equidistant from the neighboring planes.
Each pair of signals should target a differential impedance of 100 . ±15%.
A set of trace length calculation tools are made available from Intel to aid with MDI topology design.
Contact your Intel representative for tool availability.

333369-009                                                                                             1145
                                   Did this document help answer your questions?

                                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                                          Design Considerations and Guidelines

When designing a board layout, the automatic router feature of the CAD tool must not route the
differential pairs without intervention. In most cases, the differential pairs require manual routing.
Note:        Measuring trace impedance for layout designs targeting 100  often results in lower actual
             impedance due to over-etching. Designers should verify actual trace impedance and adjust
             the layout accordingly. If the actual impedance is consistently low, a target of 105  to 110 
             should compensate for over-etching.

13.2.5.4.1                  Matching Traces within a Pair (P and N)

P and N for each MDI pair should be matched to within 5 mils on the PCB to prevent common-to-
differential and differential-to-common conversion due to the length mismatch.
If in-pair length matching is not possible using bends or small loops, serpentine routing (zig-zag of a
shorter trace) is acceptable if only one to three meanders are routed within 200 mils of the source of
the skew or the end(s) of any otherwise unmatched lengths of a differential trace segment. For
example, near device pins and/or at or near the connector pins and possibly at differential signal vias.
Refer to the Intel® Ethernet Controller X550 Checklists for more details.

Table 13-1. MDI Routing Summary
                                                                                                    Breakout
                        Parameter                               Main Route Guidelines                                    Notes
                                                                                                   Guidelines1

 Signal group                                              MDI_P[3:0]
                                                           MDI_N[3:0]

 Microstrip*/Stripline* uncoupled single-ended             50  ±10%
 impedance specification
                                                                                                                     2,3
 Microstrip/Stripline uncoupled differential impedance     100  ±15%
 specification

 Microstrip nominal trace width                            Design dependent                     Design dependent
                                                                                                                     3
 Microstrip nominal trace space                            Design dependent                     Design dependent

 Microstrip/Stripline trace length                         < 8 inches                                                Table 13-2

 Microstrip/Stripline pair-to-pair space (edge-to-edge)     7 times the dielectric thickness

 Microstrip/Stripline bus-to-bus spacing                    7 times the dielectric thickness

 Matching traces within a pair (P and N)                   < 5 mils

 Keep pair-to-pair length differences                      < 2 inches

1. Pair-to-pair spacing  7 times the dielectric thickness for a maximum distance of 500 mils from the pin. The phase tolerance
   between MDI_P and MDI_N is <5mils.
2. Board designers should ideally target 100  10%. If it’s not feasible (due to board stackup) it is recommended that board
   designers use a 95  10% target differential impedance for MDI with the expectation that the center of the impedance is always
   targeted at 95 The 10% tolerance is provided to allow for board manufacturing process variations and not lower target
   impedances. The minimum value of impedance cannot be lower than 90 .
3. Simulation shows 80  differential trace impedances degrade MDI return loss measurements by approximately 1 dB from that of
   90 .

1146                                                                                                                  333369-009
                                        Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

Table 13-2. Maximum Trace Lengths Based on Trace Geometry and Board Stackup
   Dielectric        Dielectric         Width /          Pair-to-Pair        Nominal          Impedance        Maximum Trace
   Thickness       Constant (DK)      Space/ Width          Space           Impedance          Tolerance           Length
     (mils)          at 1 MHz            (mils)             (mils)             ()              (+/-%)           (inches)1

       2.7               4.05           4 / 10 / 4            19                952               172                 3.5

       2.7               4.05           4 / 10 / 4            19                952               152                  4

       2.7               4.05           4 / 10 / 4            19                95                 10                  5
                                                                                     2            172
       3.3               4.1           4.2 / 9 / 4.2          23               100                                     4

       3.3               4.1           4.2 / 9 / 4.2          23                100                15                 4.6

       3.3               4.1           4.2 / 9 / 4.2          23                100                10                  6
                                                                                     2               2
        4                4.2             5/9/5                28               100                17                  4.5

        4                4.2             5/9/5                28                100                15                 5.3

        4                4.2             5/9/5                28                100                10                  7

1. Longer MDI trace lengths can be achievable, but might make it more difficult to achieve IEEE conformance. Simulations have shown
   deviations are possible if traces are kept short. Longer traces are possible; use cost considerations and stackup tolerance for
   differential pairs to determine length requirements.
2. Deviations from 100  nominal and/or tolerances greater than 15% decrease the maximum length for IEEE conformance.

Note:        Use the MDI Differential Trace Calculator to determine the maximum MDI trace length for
             your trace geometry and board stackup. Contact your Intel representative for access.
The following factors can limit the maximum MDI differential trace lengths for IEEE conformance:
 • Dielectric thickness
 • Dielectric constant
 • Nominal differential trace impedance
 • Trace impedance tolerance
 • Copper trace losses
 • Additional devices, such as switches, in the MDI path might impact IEEE conformance.
Board geometry should also be factored in when setting trace length.

#### 13.2.5.5 Ground Planes Under a Magnetics Module

The magnetics module chassis or output ground (secondary side of transformer) should be separated
from the digital or input ground (primary side) by a physical separation of 80 mils minimum. Splitting
the ground planes beneath the transformer minimizes noise coupling between the primary and
secondary sides of the transformer and between the adjacent coils in the magnetics. This arrangement
also improves the common mode choke functionality of magnetics module.
Integrated magnetics perform this ground plane separation internally. As a result, the ground plane
split previously described is not needed when using integrated magnetics.

333369-009                                                                                                                    1147
                                      Did this document help answer your questions?

                                                                           Intel® Ethernet Controller X550 Datasheet
                                                                                Design Considerations and Guidelines

### 13.2.6 PHY MDI Lane Swap Configuration

The X550 provides flexible MDI LAN swaps for MDI board routing (see Figure 13-6) via an NVM setting.
 • Default configuration - 0, 1, 2, 3 <-> A, B, C, D
 • MDI swap configuration - 3, 2, 1, 0 <-> A, B, C, D
 • 5th channel swap not supported (MDIx_4_P and MDIx_4_N)

                                                           Port0–NoMDISwap
                                                           0,1,2,3ÅÆA,B,C,D
                                                                                          X550
                                   A                       A                     0
                                   B                       B                     1
                                   C          10GBaseͲT
               RJ45Connector                              C                     2 Port0MDIInterface
                                   D           Magnetic    D                     3
                                                           E                     4

                                                           A                     3
                                   A
                                                           B                     2
                                   B          10GBaseͲT
               RJ45Connector                              C                     1 Port1MDIInterface
                                   C
                                               Magnetic    D                     0
                                   D
                                                           E                     4

                                                            Port1–MDISwap
                                                           0,1,2,3ÅÆA,B,C,D

Figure 13-6. MDI Lane Swap Configuration

### 13.2.7 Center Tap Connection Via Capacitors to Ground

The X550 has a voltage-mode driver. When using it in 10GBASE-T applications, it is required that a
center tap be de-coupled to ground. When using an integrated magnetic, a 0.1 F capacitor should be
connected from each center tap pin to ground. Similarly, when using a discrete magnetic, add a 0.1 µF
capacitor to each center tap pin for a total of five capacitors, as previously described.

1148                                                                                                      333369-009
                                Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines
