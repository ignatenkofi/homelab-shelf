## Bash script approach 

If you have access to the ProxMox host then CHR VM can also be created quickly via BASH script. Below is an example of one such script. 

What this script does: 

- Stores tmp files in: /root/temp dir. Downloads raw image archive from MikroTik download page. Converts image file to qcow format. Creates a basic VM that is attached to the MGMT bridge. 

138 

```
#!/bin/bash
#vars
version="nil"
vmID="nil"
echo "############## Start of Script ##############
