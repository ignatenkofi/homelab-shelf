## System Requirements 

Package version: RouterOS v6.34 or newer 

Host CPU: x86-64 Architecture (64-bit) 

RAM: 512MB or more 

- Disk: 128MB or more 

RouterOS version 6: The maximum supported hard drive size is 16GB RouterOS version 7: The maximum amount of RAM and disk space is limited by the Linux kernel 5.6.3 and depends on the specific hardware. 

The minimum required RAM depends on interface count and CPU count. You can get an approximate number by using the following formula: 

RouterOS v6 - RAM = 128 + [ 8 × (CPU_COUNT) × (INTERFACE_COUNT - 1) ] RouterOS v7 - RAM = 512 + [ 8 × (CPU_COUNT) × (INTERFACE_COUNT - 1) ]
