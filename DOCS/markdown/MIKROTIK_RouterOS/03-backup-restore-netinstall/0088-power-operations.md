## Power operations 

- poweron and resume scripts are executed (if present and enabled) after power on and resume operations respectively. poweroff and suspend scripts are executed before power off and suspend operations respectively. If scripts take longer than 30 seconds or contain errors, the operation fails 

- In case of failure, retrying the same operation will ignore any errors and complete it successfully Failed script output is saved to a file (e. g. 'poweroff-script.log', 'resume-script.log' etc) 

- Scripts can be enabled/disabled from hypervisor GUI ('run VMware Tools Scripts') or by enabling/disabling scripts from the console
