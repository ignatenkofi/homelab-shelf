## auto-on mode 

If auto-on is selected on PoE-Out interface, then port operates in this strict order: 

PSE with low voltage checks for resistance on the connected port. If the detected resistance range is between (3kΩ to 26.5kΩ) power is turned on; When power is applied, the PSE continuously checks if the overload limit is not reached or short circuit detected If the cable is unplugged, the port returns in detection state and will remain off until suitable PD is detected
