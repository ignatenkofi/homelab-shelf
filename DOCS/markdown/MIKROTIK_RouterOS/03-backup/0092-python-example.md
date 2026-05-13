## Python example 

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
```

```
import sys,time
from pyVim import connect
from pyVmomi import vmodl,vim
```

```
def runInline(content,vm,creds,source):
    ''' Execute script source on vm '''
    if isinstance(source, list):
        source = '\n'.join(source)
    ps = vim.vm.guest.ProcessManager.ProgramSpec(
                programPath = 'console',
                arguments = source
        )
    return content.guestOperationsManager.processManager.StartProgramInGuest(vm,creds,ps)
def runFromFile(content,vm,creds,fileName):
    ''' Execute script file located on CHR '''
    ps = vim.vm.guest.ProcessManager.ProgramSpec(
                programPath = 'import',
                arguments = fileName
    )
    return content.guestOperationsManager.processManager.StartProgramInGuest(vm,creds,ps)
```

128 

```
def findDatastore(content,name):
    sessionManager = content.sessionManager
    dcenterObjView = content.viewManager.CreateContainerView(content.rootFolder, [vim.Datacenter], True)
```

```
    datacenter = None
    datastore = None
    for dc in dcenterObjView.view:
        dstoreObjView = content.viewManager.CreateContainerView(dc, [vim.Datastore], True)
        for ds in dstoreObjView:
            if ds.info.name == name:
                datacenter = dc
                datastore = ds
                break
        dstoreObjView.Destroy()
```

```
    dcenterObjView.Destroy()
    return datacenter,datastore
def _FAILURE(s,*a):
    print(s.format(*a))
    sys.exit(-1)
#------------------------------------------------------------------------------#
if __name__ == '__main__':
    host = sys.argv[1] # ip or something
    user = 'root'
    pwd = 'MikroTik'
    vmName = 'chr-test'
    dataStoreName = 'datastore1'
```

```
    service = connect.SmartConnectNoSSL(host=host,user=user,pwd=pwd)
    if not service:
        _FAILURE("Could not connect to the specified host using specified username and password")
    content = service.RetrieveContent()
    #---------------------------------------------------------------------------
    # Find datacenter and datastore
```

```
    datacenter,datastore = findDatastore(content,dataStoreName)
```

```
    if not datacenter or not datastore:
        connect.Disconnect(service)
        _FAILURE('Could not find datastore \'{}\'',dataStorename)
    #---------------------------------------------------------------------------
    # Locate vm
    vmxPath = '[{0}] {1}/{1}.vmx'.format(dataStoreName, vmName)
    vm = content.searchIndex.FindByDatastorePath(datacenter, vmxPath)
    if not vm:
        connect.Disconnect(service)
        _FAILURE("Could not locate vm")
    #---------------------------------------------------------------------------
    # Setup credentials from user name and pasword
    creds = vim.vm.guest.NamePasswordAuthentication(username = 'admin', password = '')
    #---------------------------------------------------------------------------
    # Run script
    pm = content.guestOperationsManager.processManager
    try:
        # Run script
        src = [':ip address add address=192.168.0.1/24 interface=ether1;']
        jobID = runInline(content, vm, creds, src)
        # Or run file (from FTP root)
        # jobID = runFromFile(content,vm,creds, 'scripts/provision.rsc')
```

129 

```
        #---------------------------------------------------------------------------
        # Wait for job to finish
```

```
        pm = content.guestOperationsManager.processManager
        jobInfo = pm.ListProcessesInGuest(vm, creds, [jobID])[0]
        while jobInfo.endTime is None:
            time.sleep(1.0)
            jobInfo = pm.ListProcessesInGuest(vm, creds, [jobID])[0]
```

```
        if jobInfo.exitCode != 0:
            _FAILURE('Script failed!')
    except:
        raise
    else:
        connect.Disconnect(service)
```
