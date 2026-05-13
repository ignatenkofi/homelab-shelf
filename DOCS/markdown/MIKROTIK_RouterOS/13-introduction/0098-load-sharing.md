## Load sharing 

In the basic configuration example, R2 is completely idle during the Backup state. This behavior may be considered a waste of valuable resources. In such circumstances, the R2 router can be set as the gateway for some clients. 

The obvious advantage of this configuration is the establishment of a load-sharing scheme. But by doing so R2 router is not protected by the current VRRP setup. 

To make this setup work we need two virtual routers. 

793 

**==> picture [505 x 428] intentionally omitted <==**

Configuration for V1 virtual router will be identical to a configuration in basic example - R1 is the Master and R2 is the Backup router. In V2 Master is R2 and Backup is R1. 

With this configuration, we establish load-sharing between R1 and R2; moreover, we create a protection setup by having two routers acting as backups for each other.
