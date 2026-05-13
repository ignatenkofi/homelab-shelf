## Example: Simple crypted file system 

To create a crypted file-system: 

```
add crypted-backend=usb1 encryption-key=<secret_key> slot=crypted-usb1 type=crypted
```

After it's created format the file system and it's ready to go. 

```
disk format crypted-usb1 file-system=ext4
```
