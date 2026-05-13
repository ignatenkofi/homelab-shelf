## Guest info 

Networking, disk, and OS info are reported to the hypervisor every 30 seconds (GuestStats (memory) are disabled by default, and can be enabled by setting 'guestinfo.disable-perfmon = "FALSE"' in VM config). 

The order, in which network interfaces are reported, can be controlled by setting 'guestinfo.exclude-nics', 'guestinfo.primary-nics' and 'guestinfo. low-priority-nics' options. Standard wildcard patterns can be used.
