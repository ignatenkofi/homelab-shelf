## 13.11 Crystal Design Considerations

This section provides information regarding crystals for use with the X550.
All designs require an external clock. The only option for this clock source is a 50 MHz external crystal.
The X550 uses the crystal to generate clocks for the high speed interfaces.
The chosen crystal vendor should be consulted early in the design cycle. Crystal manufacturers familiar
with networking equipment clock requirements might provide assistance in selecting an optimum, low-
cost solution.

### 13.11.1 Quartz Crystal

Quartz crystals are the mainstay of frequency components due to low cost and ease of implementation.
They are available from numerous vendors in many package types with various specification options.

### 13.11.2 Vibrational Mode

Crystals are available in both fundamental and third overtone. Unless there is a special need for third
overtone, use fundamental mode crystals. At any operating frequency, third overtone crystals are
thicker and more rugged than fundamental mode crystals. Third overtone crystals are more suitable for
use in military or harsh industrial environments. Third overtone crystals require a trap circuit (extra
capacitor and inductor) in the load circuitry to suppress fundamental mode oscillation as the circuit
powers up. Selecting values for these components is beyond the scope of this document.

### 13.11.3 Frequency Tolerance

The frequency tolerance for an Ethernet Platform LAN Connect is dictated by the IEEE 802.3
specification as ±50 parts per million (ppm). This measurement is referenced to a standard
temperature of 25° C. It is recommended that a frequency tolerance of ±10 ppm be used.

### 13.11.4 Temperature Stability and Environmental

                    Requirements
Temperature stability is a standard measure of how the oscillation frequency varies over the full
operational temperature range (and beyond). Several optional temperature ranges are currently
available, including -10 °C to +70 °C for industrial environments. Some vendors separate operating
temperatures from temperature stability. Manufacturers can also list temperature stability as 50 ppm in
their data sheets.
Note:        Crystals also carry other specifications for storage temperature, shock resistance, and reflow
             solder conditions. Crystal vendors should be consulted early in the design cycle to discuss the
             application and its environmental requirements.

333369-009                                                                                              1157
                                  Did this document help answer your questions?

                                                                            Intel® Ethernet Controller X550 Datasheet
                                                                                 Design Considerations and Guidelines

### 13.11.5 Calibration Mode

The terms series-resonant and parallel-resonant are used to describe crystal oscillator circuits.
Specifying parallel mode is critical to determining how the crystal frequency is calibrated at the factory.
A crystal specified and tested as series resonant oscillates without problem in a parallel-resonant
circuit, but the frequency is higher than nominal by several hundred parts per million. The purpose of
adding load capacitors to a crystal oscillator circuit is to establish resonance at a frequency higher than
the crystal’s inherent series resonant frequency.

### 13.11.6 Reference Crystal Circuit

Figure 13-12 illustrates a simplified schematic of the internal oscillator circuit. Pin X1 and X2 refers to
XTAL1 and XTAL2 in the X550, respectively. The crystal and the capacitors form a feedback element for
the internal inverting amplifier. This combination is called parallel-resonant, because it has positive
reactance at the selected frequency. In other words, the crystal behaves like an inductor in a parallel LC
circuit. Oscillators with piezoelectric feedback elements are also known as Pierce oscillators.

                                                              X1   XTAL_I

                                      CL1–18pF
                                                   50MHz
                                                                            X550

                                                              X2
                                                                   XTAL_O
                                   CL2–18pF        RͲ0ɏ

Figure 13-12. Oscillator Circuit

### 13.11.7 Crystal Load Capacitance

The formula for crystal load capacitance is as follows:

where C1 = C2 = 18 pF and Cstray = allowance for additional capacitance in pads, traces and the chip
carrier within the Ethernet device package An allowance of 3 pF to 7 pF accounts for lumped stray
capacitance. The calculated load capacitance is 16 pF with an estimated stray capacitance of about 5 pF.
Individual stray capacitance components can be estimated and added. For example, surface mount
pads for the load capacitors add approximately 2.5 pF in parallel to each capacitor. This technique is
especially useful if Y1, C1 and C2 must be placed farther than approximately one-half (0.5) inch from
the device. Thin circuit boards generally have higher stray capacitance than thick circuit boards.
Oscillator frequency should be measured with a precision frequency counter where possible. The load
specification or values of C1 and C2 should be fine-tuned for the design. As the actual capacitance load
increases, the oscillator frequency decreases.
Note:     C1 and C2 can vary by as much as 5% (approximately 1 pF) from their nominal values.

1158                                                                                                      333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines

### 13.11.8 Shunt Capacitance

The shunt capacitance parameter is relatively unimportant compared to load capacitance. Shunt
capacitance represents the effect of the crystal’s mechanical holder and contacts. The shunt
capacitance should equal a maximum of 5 pF.

### 13.11.9 Equivalent Series Resistance (ESR)

ESR is the actual component of the crystal’s impedance at the calibration frequency, which the inverting
amplifier’s loop gain must overcome. ESR varies inversely with frequency for a given crystal family. The
lower the ESR, the faster the crystal starts up. Use crystals with an ESR value of 50  or better.

### 13.11.10 Driver Level

Drive level refers to power dissipation in use. The allowable drive level for a Surface Mounted
Technology (SMT) crystal is less than its through-hole counterpart, because surface mount crystals are
typically made from narrow, rectangular AT strips, rather than circular AT quartz blanks. Some crystal
data sheets list crystals with a maximum drive level of 1 mW. However, Intel Ethernet controllers drive
crystals to a level less than the suggested 0.3 mW value. This parameter does not have much value for
on-chip oscillator use.

### 13.11.11 Aging

Aging is a permanent change in frequency (and resistance) occurring over time. This parameter is most
important in its first year because new crystals age faster than old crystals. Use crystals with a
maximum of ±5 ppm per year aging.

### 13.11.12 Reference Crystal

The normal tolerances of the discrete crystal components can contribute to small frequency offsets with
respect to the target center frequency. To minimize the risk of tolerance-caused frequency offsets
causing a small percentage of production line units to be outside of the acceptable frequency range, it is
important to account for those shifts while empirically determining the proper values for the discrete
loading capacitors, C1 and C2. Even with a perfect support circuit, most crystals oscillate slightly higher
or slightly lower than the exact center of the target frequency. Therefore, frequency measurements
(which determine the correct value for C1 and C2) should be performed with an ideal reference crystal.
When the capacitive load is exactly equal to the crystal’s load rating, an ideal reference crystal is
perfectly centered at the desired target frequency.

333369-009                                                                                             1159
                                 Did this document help answer your questions?

                                                                     Intel® Ethernet Controller X550 Datasheet
                                                                          Design Considerations and Guidelines

### 13.11.13 Reference Crystal Selection

There are several methods available for choosing the appropriate reference crystal. These are listed
below.
 • If a Saunders and Associates (S&A) crystal network analyzer is available, discrete crystal
   components can be tested until one is found with zero or nearly zero ppm deviation (with the
   appropriate capacitive load). A crystal with zero or near zero ppm deviation is a good reference
   crystal to use in subsequent frequency tests to determine the best values for C1 and C2.
 • If a crystal analyzer is not available, the selection of a reference crystal can be done by measuring
   a statistically valid sample population of crystals, which has units from multiple lots and approved
   vendors. The crystal, which has an oscillation frequency closest to the center of the distribution,
   should be the reference crystal used during testing to determine the best values for C1 and C2.
 • It might also be possible to ask the approved crystal vendors or manufacturers to provide a
   reference crystal with zero or nearly zero deviation from the specified frequency when it has the
   specified CLoad capacitance.
When choosing a crystal, keep in mind that to comply with IEEE specifications for 100/ 1000/10GBase-
T Ethernet LAN, the transmitter reference frequency must be precise within ±50 ppm. Intel®
recommends using a transmitter reference frequency that is accurate to within ±10 ppm to account for
variations in crystal accuracy due to crystal manufacturing tolerance.

### 13.11.14 Circuit Board

Since dielectric layers of the circuit board are allowed some reasonable variation in thickness, stray
capacitance from the printed board (to the crystal circuit) also vary. If the thickness tolerance for the
outer layers of dielectric are controlled within ±17 percent of nominal, the circuit board should not
cause more than ±2 pF variation to the stray capacitance at the crystal. When tuning crystal frequency,
it is recommended that at least three circuit boards are tested for frequency. These boards should be
from different production lots of bare circuit boards. Alternatively, a larger sample population of circuit
boards can be used. A larger population increases the probability of obtaining the full range of possible
variations in dielectric thickness and the full range of variation in stray capacitance. Next, the exact
same crystal and discrete load capacitors (C1 and C2) must be soldered onto each board and the LAN
reference frequency should be measured on each circuit board. The circuit board, which has a LAN
reference frequency closest to the center of the frequency distribution, should be used while performing
the frequency measurements to select the appropriate value for C1 and C2.

### 13.11.15 Temperature Changes

Temperature changes can cause crystal frequency to shift. Frequency measurements should be done in
the final system chassis across the system’s rated operating temperature range.

1160                                                                                               333369-009
                               Did this document help answer your questions?

Intel® Ethernet Controller X550 Datasheet
Design Considerations and Guidelines
