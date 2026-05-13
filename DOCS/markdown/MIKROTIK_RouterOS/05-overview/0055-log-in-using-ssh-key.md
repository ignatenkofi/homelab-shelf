## Log-in using SSH key 

Example of importing RSA private key for user admin. 

First, export currently generated SSH keys to a file: 

```
/ip ssh export-host-key key-file-prefix=admin
```

Two files admin_rsa and admin_rsa.pub will be generated. The pub file needs to be trusted on the SSH server side (how to enable SSH PKI on RouterOS) The private key has to be added for the particular user. 

```
/user ssh-keys private import user=admin private-key-file=admin_rsa
```

**==> picture [13 x 13] intentionally omitted <==**

Only user with full rights on the router can change 'user' attribute value under /user ssh-keys private 

After the public key is installed and trusted on the SSH server, a PKI SSH session can be created. 

```
/system ssh 192.168.1.1
```
