## Summary 

The RouterOS backup feature allows cloning a router configuration in binary format, which can then be re-applied on the same device. The system's backup file also contains the device's MAC addresses, which are restored when the backup file is loaded. 

We recommend restoring the backup on the same version of RouterOS. 

**==> picture [13 x 13] intentionally omitted <==**

If The Dude or User-manager or installed on the router, then the system backup will not contain configuration from these services, therefore, additional care should be taken to save configuration from these services. Use the provided tool mechanisms to save/export configuration if you want to save it. 

**==> picture [13 x 12] intentionally omitted <==**

System backups contain sensitive information about your device and its configuration, always consider encrypting the backup file and keeping the backup file in a safe place.
