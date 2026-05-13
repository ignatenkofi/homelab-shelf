## QoS Device Support 

**==> picture [514 x 421] intentionally omitted <==**

**----- Start of picture text -----**<br>
Switch Chip Models QoS Profiles QoS Maps Tx Managers WRED ECN PFC Profiles  [1] Port/Queue Usage Stats<br>98DX3236 CRS305-1G-4S+IN 128 1 8 - Current values<br>CRS326-24G-2S+ (RM/IN)<br>CRS328-24P-4S+RM<br>CRS328-4C-20S-4S+RM<br>98DX226S CRS305-1G-4S+OUT (FiberBox Plus) 128 1 8 - Current values<br>CRS310-1G-5S-4S+ (netFiber 9/IN)<br>CRS310-8G+2S+IN<br>CRS318-16P-2S+OUT (netPower 16P)<br>CRS320-8P-8B-4S+RM<br>CRS418-8P-8G-2S+RM<br>98DX224S CRS318-1Fi-15Fr-2S-OUT (netPower 15FR) 128 1 8 - Current values<br>98DX2528 CRS304-4XG-IN 128 1 8 - Current values<br>98DX8525 CCR2216-1G-12XS-2XQ 1024 12 15 ✔ ✔ 8 Max fill  [2]<br>CRS518-16XS-2XQ-RM<br>98DX4310 CRS504-4XQ (IN/OUT) 1024 12 15 ✔ ✔ 8 Max fill  [2]<br>CRS510-8XS-2XQ-IN<br>RDS2216-2XG-4S+4XS-2XQ<br>98DX8208 CRS309-1G-8S+IN 1024 12 15 ✔ ✔ 8 Current values  [3]<br>98DX8212 CRS312-4C+8XG-RM 1024 12 15 ✔ ✔ 8 Current values  [3]<br>98DX8216 CRS317-1G-16S+RM 1024 12 15 ✔ ✔ 8 Current values  [3]<br>98DX8332 CRS326-24S+2Q+RM 1024 12 15 ✔ ✔ 8 Current values  [3]<br>CRS326-4C+20G+2Q+RM<br>98DX3257 CRS354-48G-4S+2Q+RM 1024 12 15 ✔ ✔ 8 Current values  [3]<br>CRS354-48P-4S+2Q+RM<br>98DX3255 CCR2116-12G-4S+ 1024 12 15 ✔ ✔ 8 Current values  [3]<br>98CX8410 CRS520-4XS-16XQ-RM 1024 12 15 ✔ ✔ 8 Unavailable  [4]<br>**----- End of picture text -----**<br>


> 1 The devices without PFC profiles do not support Priority-based Flow Control. 

> 2 The device gathers max queue fill statistics instead of displaying the current usage values. Use the reset-counters command to reset those stats. 

459 

3 Due to hardware limitations, some switch chip models may break traffic flow while accessing QoS port/queue usage data. 

4 Usage data for individual queues on a port are unavailable, only the total usage for the entire port can be accessed.
