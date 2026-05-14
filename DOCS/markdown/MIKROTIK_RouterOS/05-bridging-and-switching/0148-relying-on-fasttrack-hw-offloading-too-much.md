## Relying on Fasttrack HW Offloading too much 

Since Fasttrack HW Offloading offers near-the-wire-speed performance at zero configuration overhead, the users are tempted to use it as the default solution. However, the number of HW Fasttrack connections is very limited, leaving the other traffic for the CPU. Try using the hardware routing as much as possible, reduce the CPU traffic to the minimum via switch ACL rules, and then fine-tune which Fasttrack connections to offload with firewall filter rules.
