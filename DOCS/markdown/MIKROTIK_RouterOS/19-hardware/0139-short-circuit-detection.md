## Short circuit detection 

When power is enabled on PoE-Out port, PSE continuously checks for a short circuit. If it is detected to ensure that there is no additional damage to PD and PSE, the power is turned off on all ports. PSE will continue to check PoE-Out port until the environment returns to normal. 

**==> picture [13 x 13] intentionally omitted <==**

Warning: Make sure that non-standard incompatible PD which does not have the resistance range 3kΩ to 26.5kΩ are not attached, so the PSE would not try to apply power on them
