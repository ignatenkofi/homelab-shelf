## Properties 

interval (time; default: 0s) - interval between two script executions, if time interval is set to zero, the script is only executed at its start time, otherwise it is executed repeatedly at the time interval is specified 

name name) - name of the task 

on-event (name) - name of the script to execute. It must be presented at /system script 

- run-count (read-only: integer) - to monitor script usage, this counter is incremented each time the script is executed start-date (date) - date of the first script execution 

start-time (time) - time of the first script execution 

startup - execute the script 3 seconds after the system startup.
