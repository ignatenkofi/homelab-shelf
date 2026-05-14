## Scripting language manual 

This manual provides an introduction to RouterOS's built-in powerful scripting language. 

Scripting host provides a way to automate some router maintenance tasks by means of executing user-defined scripts bounded to some event occurrence. 

Scripts can be stored in the Script repository or can be written directly to the console. The events used to trigger script execution include, but are not limited to the System Scheduler, the Traffic Monitoring Tool, and the Netwatch Tool generated events. 

If you are already familiar with scripting in RouterOS, you might want to see our Tips & Tricks. 

Line structure 

1092 

The RouterOS script is divided into a number of command lines. Command lines are executed one by one until the end of the script or until a runtime error occurs.
