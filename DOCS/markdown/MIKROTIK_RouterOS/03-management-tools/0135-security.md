## Security 

HTTP should only be used when testing initial setup in the secured/private network because Man-in-the-middle attacker could read/change configuration parameters. In the production environment, HTTPS is a MUST . CWMP's incoming connection validation by design is safe because CPE will not communicate with any other device except previously configured ACS. Connection Request only signals CPE to start a new connection + new session with previously configured ACS.
