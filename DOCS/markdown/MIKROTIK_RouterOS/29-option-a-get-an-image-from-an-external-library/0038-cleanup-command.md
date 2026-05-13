## Cleanup Command 

The cleanup command provides complete application removal, including all associated data. This operation is destructive and irreversible: 

```
/app> cleanup pihole
```

```
App data will be lost, continue? [y/N]:
```

Cleanup Process: 

1.  Stops the running container 

2.  Removes all application data and configuration files 

3.  Deletes container image from storage 

4.  Resets application to uninstalled state (empty APP-SIZE and DATA-SIZE) 

5.  Removes network configuration specific to the application 

Warning: All user data, configuration settings, and application state will be permanently lost. The application will return to its original catalog state and require complete reconfiguration if reinstalled.
