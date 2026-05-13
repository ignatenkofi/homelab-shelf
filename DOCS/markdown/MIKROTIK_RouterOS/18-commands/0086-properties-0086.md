## Properties 

**==> picture [316 x 80] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>contents  (string; Default: ) File contents that must be added. Works only for type=file<br>name  (string; Default: ) File/directory name<br>type  (file | directory; Default: file) Specifies type<br>**----- End of picture text -----**<br>


1142 

**==> picture [13 x 13] intentionally omitted <==**

If the device has a directory named "flash" in its file list, then files which you want to be kept after the system reboot/power cycle must be stored within it. As anything outside of it is kept within a RAM disk and will be lost upon reboot. This does not include .npk upgrade files as they will be applied by the upgrade process before the system discards the RAM drive content. 

**==> picture [13 x 13] intentionally omitted <==**

For multicore devices with a NAND flash memory (e.g. CCR series routers, RB4011iGS), RouterOS uses a write-back that will cache file changes into RAM memory instead of writing them straight away into flash media. The file changes will be stored on the flash when it is absolutely necessary, the writing can be delayed by up to 40 seconds. This helps to reduce CPU cycles which results in better performance. However, this can cause empty or zero-length files when a device experiences a sudden power loss, because files were not fully saved on a flash.
