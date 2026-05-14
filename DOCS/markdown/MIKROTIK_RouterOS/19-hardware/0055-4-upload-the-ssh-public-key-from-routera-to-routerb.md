## 4.  Upload the SSH public key from `RouterA` to `RouterB` : 

```
/file/sync/add local-path=admin_ed25519_pub.pem remote-address=RouterB user=admin mode=upload
/file/sync/remove [find where local-path=admin_ed25519_pub.pem]
```

5.  On `RouterB` create a new user, for example `btrsfstransfer` and set a secure password for it: 

```
/user/add name=btrfstransfer group=write
```

**==> picture [13 x 13] intentionally omitted <==**

While the password is not going to be used for the Btrfs transfer feature, you still need to use a secure password to prevent unauthorized access to your device. 

6.  On `RouterB` import the uploaded SSH public key and set it for user `btrfstransfer` : 

```
/user/ssh-keys/import public-key-file=admin_ed25519_pub.pem user=btrfstransfer
```
