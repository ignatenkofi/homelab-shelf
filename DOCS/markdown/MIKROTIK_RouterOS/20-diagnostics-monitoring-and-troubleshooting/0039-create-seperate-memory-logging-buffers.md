## Create seperate memory logging buffers 

Create new memory logging buffers, which will store specified logs seperately from default memory logs. 

```
/system logging action add name=dhcpMemoryLog target=memory memory-lines=300
```

```
/system logging action add name=wirelessLog target=memory memory-lines=500
```

Assign topics to created buffers. This rule sends all DHCP logs to dhcpMemoryLog, and wireless logs to wirelessLog buffer. 

- `/system logging add topics=dhcp action=dhcpMemoryLog` 

```
/system logging add topics=wireless action=wirelessLog
```

View content of each buffer seperately 

- `# View only DHCP related logs stored in its dedicated buffer /log print where buffer=dhcpMemoryLog` 

- `# View only non-info Wireless logs stored in its dedicated buffer /log print where buffer=wirelessLog` 

Clear all memory logs from specifc memory buffer 

1776 

```
/system logging action clear action=dhcpMemoryLog
```
