## Step 1: Storage Selection 

Choose the storage disk for application installation. The system automatically detects available formatted disks (nvme1, usb1, disk1, etc.). If no suitable disk appears, it must be formatted with ext4 or btrfs and mounted via `/disk` menu. 

Requirements: 

Minimum 100MB/s sequential read/write speed and 10K random IOPS recommended 

Use `/disk/test` command to verify storage performance External storage highly recommended for optimal performance
