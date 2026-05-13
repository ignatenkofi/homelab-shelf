## Quiescing/backup 

Guest filesystem quiescing is performed only if requested. 

127 

freeze script is executed before freezing the filesystem 

- freeze-fail script is executed if the hypervisor failed to prepare for a snapshot or if freeze script failed thaw script is executed after the snapshot has been taken 

Script run time is limited to 60 seconds 

- freeze script timeouts and errors result in the backup operation being aborted FAT32 disks are not quiesced 

Failed script output is saved to a file (e. g. 'freeze-script.log', 'freeze-fail-script.log', 'thaw-script.log')
