## CWMP Session 

CWMP client usually starts communication(Session) with ACS on different events - first boot, reboot, periodic interval, remote request, value change etc. In each session, CPE and ACS can call RPCs to be "executed" on the other side. CPE always starts with Inform RPC, which contains connection reason, device info and some Parameter values depending on configuration. When CPE has nothing more to say, then ACS executes its RPCs (which most of the time are Parameter management RPCs).
