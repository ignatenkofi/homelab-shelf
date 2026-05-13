## Alternative approach 

Create Basic VM via ProxMox web GUI. 

- Make sure that VM storage is on local storage (this way there will be no need to work with the LVM config side, and the disk image can be moved later on to LVM or other desired storage if needed). 

Log into ProxMox host via SSH and navigate to the VM image directory. Default local storage is located in: var/lib/vz/images/(VM_ID) Via scp, wget or any other tool download CHR raw image (.img file) into this directory. 

Now convert the CHR raw image to qcow2 format using qemu-img tool: 

```
qemu-img convert -f raw -O qcow2 chr-6.40.3.img vm-(VM_ID)-disk-1.qcow2
```
