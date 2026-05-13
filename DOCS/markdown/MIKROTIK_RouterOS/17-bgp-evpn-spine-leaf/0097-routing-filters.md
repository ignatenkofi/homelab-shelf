## Routing Filters 

Starting from ROSv7.1beta4, the routing filter configuration is changed to a script-like configuration. The rule now can have "if .. then" syntax to set parameters or apply actions based on conditions from the "if" statement. 

Multiple rules without action are stacked in a single rule and executed in order like a firewall, the reason is that the "set" parameter order is important and writing one "set"s per line, allows for an easier understanding from top to bottom on what actions were applied. 

For example, match static default route and apply action accept can be written in one config rule:
