## Port Forwarding 

Some client devices may need direct access to the internet over specific ports. For example, a client with an IP address 192.168.88.254 must be accessible by Remote desktop protocol (RDP). 

After a quick search on Google, we find out that RDP runs on TCP port 3389. Now we can add a destination NAT rule to redirect RDP to the client's PC. 

```
/ip firewall nat
```

```
  add chain=dstnat protocol=tcp port=3389 in-interface=ether1 \
    action=dst-nat to-address=192.168.88.254
```

**==> picture [13 x 13] intentionally omitted <==**

If you have set up strict firewall rules then RDP protocol must be allowed in the firewall filter forward chain.
