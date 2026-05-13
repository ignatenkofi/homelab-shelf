## Backup 

VR must contain at least one Backup router. A backup router must be configured with the same virtual IP as the Master for that VR. The default priority for Backup routers is 100. When the current master router is no longer available, a backup router with the highest priority will become a current master. Every time when a router with higher priority becomes available it is switched to master. Sometimes this behavior is not necessary. To override it preemption mode should be disabled.
