## Running More than One Instance 

As we already know for best path selection to work properly, BGP routes must be received from the same instance. But in certain scenarios it is necessary to run multiple BGP instances with their own separate tables. 

BGP determines whether sessions belongs to the same instance by comparing configured local router IDs. 

For example config below will run each peer in its own BGP instance
