## No physical connection to a backbone 

The area may not have a physical connection to the backbone, a virtual link is used to provide a logical path to the backbone of the disconnected area. A link has to be established between two ABRs that have a common area with one ABR connected to the backbone. 

We can see that both R1 and R2 routers are ABRs and R1 is connected to the backbone area. Area2 will be used as a transit area and R1 is the entry point into the backbone area. A virtual link has to be configured on both routers. 

Virtual link configuration is added in OSPF interface templates. If we take the example setup from the "no physical connection" illustration, then the virtual link configuration would look like this:
