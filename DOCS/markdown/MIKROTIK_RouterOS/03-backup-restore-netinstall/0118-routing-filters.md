## Routing filters 

All supported options are upgraded without any issue, in the case of an unsupported option - an empty entry is created. The routing filter configuration is changed to a script-like configuration. 

The rule now can have "if .. then" syntax to set parameters or apply actions based on conditions from the "if" statement. 

Multiple rules without action are stacked in a single rule and executed in order like a firewall, the reason is that the "set" parameter order is important, and writing one "set"s per line, allows for an easier understanding from top to bottom on what actions were applied. 

More RouterOSv7 routing filter examples are here.
