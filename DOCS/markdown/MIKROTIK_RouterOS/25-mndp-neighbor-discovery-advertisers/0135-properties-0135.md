## Properties 

**==> picture [516 x 168] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>eject  () Safely unmounts (ejects) drive of your selection by using "slot" that is assigned to it. After issuing this command it can be removed<br>from host device.<br>format  () Command to initiate disk formatting process. Contains additional properties of its own. Such as "file-system" and "label".<br>select disk (slot) that should be formatted<br>file-system ('exfat', 'ext4', 'fat32' or 'wipe') - Format disk with type ExFAT, FAT32 or EXT4 or securely wipe all data<br>label<br>mbr-partition-table - make mbr partition table<br>reset-counters Resets disk (slot) statistics<br>monitor-traffic Check real time disk performance and health stats<br>**----- End of picture text -----**<br>


1660 

**==> picture [516 x 358] intentionally omitted <==**

**----- Start of picture text -----**<br>
test allows performing performance tests of selected device (Available from RouterOS 7.16)<br>disk - device or devices for test<br>direction - ('read','write')<br>duration - (int)<br>pattern - ('random', 'sequential')<br>thread-count - (int)<br>block-size - size of block to be used for testing<br>type - ('device', 'filesystem')<br>mount-read-only Sets the mounted disk in read only mode when set to yes.<br>mount-point- Sets the mounting point for the file system. It is possible to set the mount point as the following parameters based on the disk:<br>template<br>[slot] (default) - sets the mount point as the slot name.<br>[model] - sets the mount point as the device's model name.<br>[serial] - sets the mount point as the device serial<br>[fw-version] - sets the mount point as the device's firmware version.<br>[fs-label] - sets the mount point as the device's file system label.<br>[fs-uuid] - sets the mount point as the device's UUID<br>[fs] - sets the mount point as the device's file system<br>/disk set nvme1 mount-point-template="[model]"<br>Additionally, it is possible to combine multiple variables to create a single mount point:<br>/disk set nvme1 mount-point-template="[model]-[fs]"<br>**----- End of picture text -----**<br>
