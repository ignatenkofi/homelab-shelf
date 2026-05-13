## Provisioning 

You can use the ProcessManager from Vim API to execute scripts. Python bindings are available 

Main data structure: GuestProgramSpec 

The workingDirectory and envVariables members are ignored programPath must be set to either 'inline' or 'import' If programPath is ' inline' , arguments are interpreted as script text If programPath is ' import' , arguments are interpreted as file path 

After using GuestProgramSpec together with an instance of GuestAuthentication as arguments to StartProgramInGuest unique JobID is obtained. 

Script progress can be tracked by using the ListProcessesInGuest command. ListProcessesInGuest accepts an array of job id's; passing an empty array will report on all jobs started from the API 

ListProcessesInGuest returns an array of GuestProcessInfo instances: pid field is set to JobID endTime is only set after completion exitCode is set to 0 on success and -1 on error 

- name is set to 'inline' or 'import' (same as programPath in GuestProgramSpec) 

Information about completed jobs is kept around for ~1 minute, or until ListProcessesInGuest (with the corresponding JobID) is called. If the script fails, a file named 'vix_job_$JobID$ .txt' containing the script output is created. Script run time is limited to 120 seconds and script output is not saved on timeout, 

The vmrun command runScriptInGuest can also be used The PowerCLI cmdlet Invoke-VMScript is not supported Host/guest file transfer is not supported
