## Introduction 

The introduction of the container feature into the RouterOS made it possible to run all kinds of servers for all sorts of tasks inside the router. This is especially relevant for people, who want to reduce the number of devices in their network. Instead of running a server on a separate device/machine, why not run it inside the router? 

Radius is short for Remote Authentication Dial-In User Service. RouterOS has a RADIUS client feature supported that can authenticate for HotSpot, PPP, P PPoE, PPTP, L2TP, and ISDN connections. Basically, this feature allows you to connect RouterOS to a Radius Server, and then, utilize the user database from the server for client authentication. 

In our example, we will showcase freeradius/freeradius-server image installation.
