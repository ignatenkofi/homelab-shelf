## Backup 

It is possible to store your device's backup on MikroTik's Cloud server. The backup service allows you to upload an encrypted backup file, download it and apply the backup file to your device as long as your device is able to reach MikroTik's Cloud server. Below you can find operation details that are relevant to the IP/Cloud's backup service: 

1 free backup slot for each device Allowed backup size: 15MB Sends encrypted packets to cloud2.mikrotik.com using UDP/15252 and TCP/15252 port 

869 

To create a new backup and upload it the MikroTik's Cloud server: 

```
[admin@MikroTik] > /system backup cloud upload-file action=create-and-upload password=test123!!!
[admin@MikroTik] > /system backup cloud print
```

```
 0 name="cloud-20180921-162649" size=13.2KiB ros-version="6.44beta9" date=sep/21/2018 16:26:49 status="ok"
secret-download-key="AbCdEfGhIjKlM1234567890"
```

**==> picture [13 x 13] intentionally omitted <==**

The `create-and-upload` action command will create a new system's backup file, encrypt the backup file with AES using the provided password and upload it. For `upload` action command the password property has no effect since the `upload` action command uploads only already created system's backup files. 

To download the uploaded backup file and save it to the device's memory: 

```
[admin@MikroTik] > /system backup cloud download-file action=download number=0
```

```
### OR
```

```
[admin@MikroTik] > /system backup cloud download-file action=download secret-download-
key=AbCdEfGhIjKlM1234567890
```

**==> picture [13 x 13] intentionally omitted <==**

Warning: The secret-download-key is a unique identifier that can be used to download your encrypted backup to your other devices. Since you can download your encrypted backup from any location and any device by using the secret-download-key, then you should try to keep this identifier a secret. The downloaded backup is still encrypted using AES, nevertheless, make sure you are using a strong password! 

To remove the uploaded backup: 

```
/system backup cloud remove-file number=0
```

To replace an existing file with a new backup file, use the following command: 

```
/system/backup/cloud/upload-file action=create-and-upload replace=_your_previously_created_backup_file_
password=test123!!!
```

To upload an existing backup file (created previously): 

```
[admin@MikroTik] > /system backup save encryption=aes-sha256 name=old_backup password=test123!!!
```

```
[admin@MikroTik] > /system backup cloud upload-file action=upload src-file=old_backup.backup
[admin@MikroTik] > /system backup cloud print
```

```
 0 name="cloud-20180921-164044" size=13.2KiB ros-version="6.44beta9" date=sep/21/2018 16:40:44 status="ok"
secret-download-key="AbCdEfGhIjKlM1234567890"
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure that the backup was encrypted using AES, otherwise, the IP/Cloud will reject the backup upload. Since there is only 1 free backup slot per device, then you need to remove the existing backup before uploading a new one.
