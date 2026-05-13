## Overload protection 

When a PoE-Out port is powered-on, it is constantly checked for overload. If the overload is detected, PoE-Out is turned off on the port to avoid damage to the PD or PSE. 

In seconds the PoE Out feature will be turned on again to see if the environment has changed and PD can be supplied with power again. That is important for configurations that are not connected to mains (solar installations, equipment running on batteries due to mains failure) so that when voltage drops - overload will be detected and connected devices turned off. After a while when the voltage level returns to usual operating value - connected equipment can be powered up again.
