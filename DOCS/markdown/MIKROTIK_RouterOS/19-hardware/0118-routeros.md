## RouterOS 

Sub-menu : `interface ethernet poe monitor` 

**==> picture [509 x 83] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>name  () Name of an interface<br>poe-out  () Shows PoE-Out state<br>poe-out- Shows the current PoE-Out status on the port<br>**----- End of picture text -----**<br>

1730 

**==> picture [509 x 418] intentionally omitted <==**

**----- Start of picture text -----**<br>
status  () powered-on - Power is applied to the port, and PoE-Out is operating normally.<br>waiting-for-load - PSE attempts to detect if power can be applied to the port. For powering, there should be resistance in the<br>range from 3kΩ to 26.5kΩ;<br>short-circuit - Short-circuit is detected on the PoE-Out port, power is switched off, and only the detection with low voltage takes<br>place. This can also mean that PoE is not supported on the connected device.<br>overload - The PoE-Out current limit is exceeded, and power is switched off on the PoE-Out port. For port limits, see each<br>model's specifications.<br>voltage-too-low - PD can not be powered with the voltage provided from PSE.<br>voltage-too-high - The connected device is detected as a PoE-In device, but the output voltage from the PSE is higher than the<br>range supported by the PD;<br>current-too-low - current-too-low means that PD draws too low current  (<10mA) than the normal PoE-Out device should<br>voltage_on_poe-in - Shows the voltage currently present on the PoE-Out port.<br>This status indicates that the PoE-Out port has detected an unexpected voltage input, which can occur in two cases:<br>a.   External Power Source  – Another device is supplying power to the port (PoE-In voltage).<br>b.   Internal Fault  – The PoE-Out circuitry on the port may be damaged,<br>The delivered voltage at PD is too low for normal powering (for example, Vmin =>30V, but provided 24V);<br>PD uses a second power source which has a higher voltage than PSE, so all current is taken from the second DC source, not the PSE<br>PoE-Out port.<br>off - all detection and power is turned off for this port;<br>power_reset - PSE controller resetting the power, for example, when executing the power cycle command or when pings fail<br>(power-cycle-ping);<br>controller_init - PSE controller initialization;<br>controller_upgrade - PSE controller is being upgraded;<br>controller_error - PSE controller does not respond.<br>poe-out- Displays PoE Voltage which is applied to the PD.<br>voltage  ()<br>poe-out- Displays the port current (mA) which is drawn by the PD.<br>current  ()<br>poe-out- Displays PD power consumption<br>power  ()<br>poe-out- Displays on which power pair PSE is delivering power to PD. ( a  = 1,2(+)  3,6(-) ;  = 4,5(+)  7,8(-) ;  b bt  = all 4 pairs).<br>power-pair()<br>**----- End of picture text -----**<br>

If `power-cycle-ping` feature is used, `/interface ethernet poe monitor [find]` will show additional fields:
