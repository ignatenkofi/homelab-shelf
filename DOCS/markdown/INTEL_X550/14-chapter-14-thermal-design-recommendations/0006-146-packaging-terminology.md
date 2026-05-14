## 14.6 Packaging Terminology

The following is a list of packaging terminology used in this section:
 • FCBGA Flip Chip Ball Grid Array — A surface-mount package using a combination of flip chip and
   BGA structure whose PCB-interconnect method consists of Pb-free solder ball array on the
   interconnect side of the package. The die is flipped and connected to an organic build-up substrate
   with C4 bumps. An Integrated Heat Spreader (IHS) might be present for larger FCBGA packages for
   enhanced thermal performance (but IHS is not present for the X550).
 • Junction — Refers to a P-N junction on the silicon. In this section, it is used as a temperature
   reference point (for example, JA refers to the junction-to-ambient thermal resistance).
 • Ambient — Refers to local ambient temperature of the bulk air approaching the component. It can
   be measured by placing a thermocouple approximately 1inch upstream from the component edge.
 • Lands — The pads on the PCB to which BGA balls are soldered.
 • Printed Circuit Board — PCB.
 • Printed Circuit Assembly (PCA) — An assembled PCB.
 • Thermal Design Power (TDP) — The estimated maximum possible/expected power generated in
   a component by a realistic application. Use the maximum power requirements listed in Table 14-2.
 • Linear Feet Per Minute — LFM (airflow).
 • JA (Theta JA) — Thermal resistance junction-to-ambient, °C/W.
 • JT (Psi JT) — Junction-to-top (of package) thermal characterization parameter, °C/W. JT does
   not represent thermal resistance, but instead is a characteristic parameter that can be used to
   convert between Tj and Tcase when knowing the total TDP. JT is easy to characterize in
   simulations or measurements, and is equal to Tj minus Tcase divided by the total TDP. This
   parameter can vary by environment conditions like heat sink and airflow.
