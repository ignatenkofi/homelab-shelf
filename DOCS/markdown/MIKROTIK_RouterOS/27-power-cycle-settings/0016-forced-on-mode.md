## forced-on mode 

If forced-on is selected then port operates in this strict order: 

PSE disables resistance check on the port, and apply power on pins depending on the poe-out() state, even if no cable is attached When power is applied, PSE still continuously checks if an overload or short circuit is not detected After the cable is unplugged, the power still remains enabled on the port.
