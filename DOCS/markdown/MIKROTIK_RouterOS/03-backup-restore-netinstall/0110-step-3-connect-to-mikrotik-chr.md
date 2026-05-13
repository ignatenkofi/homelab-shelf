## Step 3: Connect to MikroTik CHR 

1.  Navigate to the server's settings page. 2.  Choose the Custom ISO menu, then click Remove ISO . The server will reboot. 3.  Connect to the web console. 4.  Log in as admin. There is no password set, so press Enter at the prompt. 5.  View the software license, then choose a new, strong password. 

6.  Close the web console, then open a terminal on your local computer. 7.  SSH as admin to the server's IP address. 

```
$ ssh admin@192.0.2.2
```

8.  Enter the strong password you set in the prior step. 

This completes the basic installation. Please secure your MikroTik CHR router and consult the documentation to configure the server for production use. Visit Vultr site for configuration manual and for their firewall features. 

141
