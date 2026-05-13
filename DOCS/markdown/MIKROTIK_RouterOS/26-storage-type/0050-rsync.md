## RSYNC 

`rsync` (Remote Sync) is a powerful file synchronization and file transfer program used in Unix-based systems. It allows for efficient transfer and synchronization of files and directories between different systems or within the same system. 

If you make changes in a file only changes to files are transferred, reducing data transfer volume. RouterOS RSYNC implementation uses ipsec for data transfer (if password is set). When configured you will see dynamic ipsec entries. 

Rsync settings can be found in file/sync menu 

**==> picture [13 x 13] intentionally omitted <==**

Port TCP/8291 is used for the control connection (if not open in the status (file sync print) you will be stuck at making control connection to 192.1 68.88.2) 

Port UDP/500 and protocol 50 (ipsec-esp) is used to create a secure connection and start the transfer (if not open in the status (file sync print) you will be stuck at initializing transfer) 

IPSec dynamic entry example: 

```
#     PEER                     TUNNEL  SRC-ADDRESS       DST-ADDRESS       PROTOCOL  ACTION   LEVEL    PH2-COUNT
;;; file-sync-10.155.145.11
1  D  file-sync-10.155.145.11  no      10.155.145.17/32  10.155.145.11/32  tcp       encrypt  require          1
```
