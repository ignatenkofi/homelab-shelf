## Usable Network and Disk interfaces on various hypervisors: 

ESX: Network: vmxnet3, E1000 Disk: IDE, VMware paravirtual SCSI, LSI Logic SAS, LSI Logic Parallel Hyper-V: Network: Network adapter, Legacy Network adapter Disk: IDE, SCSI Qemu/KVM: Network: Virtio, E1000, vmxnet3 (optional) Disk: IDE, Sata, Virtio VirtualBox Network: E1000, rtl8193 Disk: IDE, Sata, SCSI, SAS 

Note: SCSI controller Hyper-V and ESX are usable just for secondary disks, system image must be used with IDE controller! 

Warning: We do not recommend using the E1000 network interface if better synthetic interface options are available on a specific Hypervisor!
