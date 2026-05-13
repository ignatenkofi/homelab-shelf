## Setup Overview 

Let's assume that our gateway has two public network uplinks ("ISP1", "ISP2"). First uplink should be preferred and second one should act as a backup. 

Then we mark traffic in two parts, one with the name "ISP1" and the second as "ISP2" which goes through the ether1 and ether2 accordingly. In this setup, we want to monitor two hosts: Host1 and Host2. We will use Google DNS servers with IP 8.8.8.8 (Host1) and 8.8.4.4 (Host2), but it is not mandatory to use specifically these addresses. 

**==> picture [504 x 147] intentionally omitted <==**
