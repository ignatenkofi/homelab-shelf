## Root path cost example 

**==> picture [505 x 244] intentionally omitted <==**

This example outlines how the root path cost works. SW1 will be the root bridge, due to it having the lowest priority of 0x1000, as the root bridge. Each bridge will calculate the path cost to the root bridge. When calculating root path cost bridges take into account the configured path cost on their ports + root path cost advertised by neighboring bridges. 

SW1 : due to it being the root bridge, it advertises a root path cost of 0 to its neighbors, even though it has a configured path cost of 10. 

SW2:  ether1 . has a root path cost of 0 + 25= 25 . On the ether2 path cost will be 10+10+10+0= 30 

SW3: ether2 , has a root path cost of 0 + 10= 10 . On the ether4 path cost will be 10+5+25+0= 40 

SW4: ether1 , has a root path cost of 0+25+5= 30 . On ether4 path cost will be 10+10+0= 20 

The Port with the lowest path cost will be elected as the root port. Every bridge in STP topology needs a path to the root bridge, after the best path has been found, the redundant path will be blocked, in this case, the path between SW2 and SW4. 

**==> picture [13 x 13] intentionally omitted <==**

You can configure path cost on the root bridge, but it will only be taken into account when the bridge loses its root status.
