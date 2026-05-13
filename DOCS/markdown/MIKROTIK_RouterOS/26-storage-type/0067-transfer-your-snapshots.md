## Transfer your snapshots 

Btrfs allows to easily send a snapshot between two devices that is using Btrfs. In this example we will use two RouterOS devices running ROSE-storage package. The RouterOS device containing snapshots that need to be backed up is going to be called `RouterA` and the RouterOS device that is going to receive backups is going to be called `RouterB` . 

1690 

**==> picture [13 x 13] intentionally omitted <==**

This guide only shows an example how to use Btrfs transfer between RouterOS devices, but you can transfer snapshots between RouterOS and Linux devices as well. If you require such functionality, then make sure to check the documentation of your Linux distribution on how to use Btrfs transfer on it. 

**==> picture [13 x 13] intentionally omitted <==**

This guide will use the SSH host key for a SSH user key on the same RouterOS device. If you wish to use your own key for the SSH user, then you can use these commands on a Linux computer and later import the key pair under `/user/ssh-keys` : 

```
openssl genpkey -outform PEM -out btrfstransfer_key.pem -algorithm ED25519
openssl pkey -in btrfstransfer_key.pem -pubout -out btrfstransfer_key_pub.pem
```

1.  OPTIONAL: Increase the security level of your SSH server, run the following commands on 

`RouterA` and `RouterB` : 

```
/ip ssh/set host-key-type=ed25519 strong-crypto=yes
/ip/ssh/regenerate-host-key
```

**==> picture [13 x 13] intentionally omitted <==**

Regenerating the host key will create a error message next time you try to connect to the RouterOS device using SSH. You will need to adjust your SSH client's configuration (usually in `~/.ssh/known_hosts` ) to trust the new host key.
