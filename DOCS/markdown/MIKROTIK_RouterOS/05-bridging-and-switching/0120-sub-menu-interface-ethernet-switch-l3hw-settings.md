## Sub-menu: `/interface ethernet switch l3hw-settings` 

**==> picture [516 x 143] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>autorestart (ye Automatically restarts the l3hw driver in case of an error. Otherwise, if an error occurs, l3-hw-offloading gets disabled, and the<br>s | no; Default:  error code is displayed in the switch settings and #monitor. Autorestart does not work for system failures, such as OOM (Out Of<br>no ) Memory).<br>fasttrack-hw (y Enables or disables FastTrack HW Offloading. Keep it enabled unless HW TCAM memory reservation is required, e.g., for dynamic<br>es | no;  switch ACL rules creation. Not all switch chips support FastTrack HW Offloading (see hw-supports-fasttrack ).<br>Default:  yes  (if<br>supported))<br>ipv6-hw (yes |  Enables or disables IPv6 Hardware Offloading. Since IPv6 routes occupy a lot of HW memory, enable it only if IPv6 traffic speed is<br>no; Default:  no ) significant enough to benefit from hardware routing.<br>**----- End of picture text -----**<br>

434 

icmp-reply-onSince the hardware cannot send ICMP messages, the packet must be redirected to the CPU to send an ICMP reply in case of an error error (yes | no; (e.g., "Time Exceeded", "Fragmentation required", etc.). Enabling icmp-reply-on-error helps with network diagnostics but may open Default: yes ) potential vulnerabilities for DDoS attacks. Disabling icmp-reply-on-error silently drops the packets on the hardware level in case of an error. 

Read-Only Properties 

Property Description 

hw-supports-fasttrack (yes | no) Indicates if the hardware (switch chip) supports FastTrack HW Offloading.
