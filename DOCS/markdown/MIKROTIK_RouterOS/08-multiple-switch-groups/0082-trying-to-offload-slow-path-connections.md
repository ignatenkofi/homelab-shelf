## Trying to offload slow-path connections 

Using certain configurations (e.g. enabling bridge " use-ip-firewall " setting, creating bridge nat/filter rules) or running specific features like sniffer or torch can disable RouterOS FastPath, which will affect the ability to properly FastTrack and HW offload connections. If HW offloaded Fasttrack is required, make sure that there are no settings that disable the FastPath and verify that connections are getting the "H" flag or use the L3HW monitor command to see the amount of HW offloaded connections.
