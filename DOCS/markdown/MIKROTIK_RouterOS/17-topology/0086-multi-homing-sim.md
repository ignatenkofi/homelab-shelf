## Multi-homing Sim 

Two DUT devices establish eBGP sessions to simulated x86 upstream routers. Both DUTs are interconnected with the iBGP session. Each DUT receives routes from upstream and readvertises routes over iBGP. On ROSv7 affinity, settings are set to "alone" and early-cut disabled. 

**==> picture [504 x 272] intentionally omitted <==**

Route Provider: CHR (ROSv6 585K routes) DUT_1: CCR1036 DUT_2: CCR1036 

v7.1beta3 1:11 v7.1beta2 1:29 v6.xx 1:02 - 8:30 

Route Provider: CHR (ROSv6 585K routes) DUT_1: CCR2004 DUT_2: RB1100AHx2 

v7.1beta3 0:36 v6.xx 0:59 

Route Provider: CCR2216 (ROSv7.16 1008427 routes) DUT_1: CCR2216 DUT_2: CCR2116 

Time 

M em 

1072 

**==> picture [516 x 196] intentionally omitted <==**

**----- Start of picture text -----**<br>
v7.15.3 0:59 28<br>5<br>MB<br>v7.16 0:48 29<br>7<br>MB<br>Route Server<br>Time M<br>em<br>v7.15.3 - -<br>MB<br>v7.16 - -<br>MB<br>**----- End of picture text -----**<br>
