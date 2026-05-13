## CHR ProxMox installation 

Create a new guest with the system disk and other devices as required. 

Then you have to manually upload the CHR disk (in qcow format) on the ProxMox host. 

- Use scp or any other comparable tool as that will use SSH for the upload and it does not require any additional configuration. 

- Either copy the file to the server and then manually edit the VM's .conf file or replace the previously created system image file used for booting the guest. 

Local storage on ProxMox is in /var/lib/vz directory. There should be a subdirectory called images with a directory for each VM (named by the VM number). You can copy the files directly there. 

To add the existing file to the VM, edit the VM's .conf file directly. Look in /etc/pve/qemu-server/ for a file with the VM number followed by .conf. 

Note: It's a good idea to create a second test VM so you can refer to it's.conf file to make sure you get the syntax right
