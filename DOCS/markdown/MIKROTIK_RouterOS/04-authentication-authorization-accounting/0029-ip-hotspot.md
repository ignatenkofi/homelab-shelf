## IP HotSpot 

```
/ip/hotspot
```

The menu is designed to manage the HotSpot servers of the router. It is possible to run HotSpot on Ethernet, wireless, VLAN, and bridge interfaces. One HotSpot server is allowed per interface. When HotSpot is configured on the bridge interface, set HotSpot interface as bridge interface, not as bridge port, do not add public interfaces to bridge ports. You can add HotSpot servers manually to the /ip/hotspot menu, but it is advised to run /ip/hotspot/setup, which adds all necessary settings. 

**==> picture [516 x 328] intentionally omitted <==**

**----- Start of picture text -----**<br>
Parameters Description<br>name  (text) HotSpot server's name or identifier<br>address-pool  (name/ address space used to change HotSpot client any IP address to a valid address. Useful for providing public network access to<br>none; default: none) mobile clients that are not willing to change their networking settings<br>idle-timeout  (time period of inactivity for unauthorized clients. When there is no traffic from this client (literally client computer should be switched<br>/none; default: 5m)  off), once the timeout is reached, a user is dropped from the HotSpot host list, its used address becomes available<br>keepalive-timeout  (ti Value of how long host can stay out of reach to be removed from the HotSpot<br>me/none; default: no<br>ne)<br>login-timeout  (time Period of time after which if a host hasn't been authorized itself with a system the host entry gets deleted from host table. Loop<br>/none; default: none) repeats until the host logs in the system. Enable if there are situations where a host cannot log in after being too long in the host<br>table unauthorized.<br>interface  (name of  Interface to run HotSpot on<br>an interface)<br>addresses-per-mac  (i Number of IP addresses allowed to be bind with the MAC address, when multiple HotSpot clients connected with one MAC-<br>nteger / unlimited;  address<br>default: 2)<br>profile  (name;  HotSpot server default HotSpot profile, which is located in /ip/hotspot/profile<br>default:  default)<br>Read-only<br>Parameters Description<br>**----- End of picture text -----**<br>

293 

keepalive-timeout (readThe exact value of the keepalive-timeout, that is applied to the user. Value shows how long the host can stay out of reach only; time) to be removed from the HotSpot
