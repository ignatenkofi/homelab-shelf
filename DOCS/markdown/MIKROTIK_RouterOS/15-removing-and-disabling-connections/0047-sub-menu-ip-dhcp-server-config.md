## Sub-menu: `/ip dhcp-server config` 

Store Leases On Disk: The configuration of how often the DHCP leases will be stored on disk. If they would be saved on a disk on every lease change, a lot of disk writes would happen which is very bad for Compact Flash (especially, if lease times are very short). To minimize writes on disk, all changes are saved on disk every store-leases-disk seconds. Additionally, leases are always stored on disk on graceful shutdown and reboot. 

Manual changes to leases - addition/removal of a static lease, removal of a dynamic lease will cause changes to be pushed for this lease to storage. 

Accounting: The accounting parameter in the DHCP server configuration enables or disables accounting for DHCP leases. When accounting is enabled, the DHCP server logs information about IP address assignments and lease renewals. This information can be useful for tracking and monitoring network usage, analyzing traffic patterns, or generating reports on IP address allocations. 

Interim-update: The interim-update parameter determines whether the DHCP server sends periodic updates to the accounting server during a lease. These updates provide information about the lease duration, usage, and other relevant details. Enabling interim updates allows for more accurate tracking of lease activity. 

Radius-password: The radius-password parameter is used to set the password for the RADIUS (Remote Authentication Dial-In User Service) server. RADIUS is a networking protocol commonly used for providing centralized authentication, authorization, and accounting for network access. When configuring the DHCP server to communicate with a RADIUS server for authentication or accounting purposes, you need to specify the correct password to establish a secure connection. This parameter ensures that the DHCP server can authenticate with the RADIUS server using the specified password.
