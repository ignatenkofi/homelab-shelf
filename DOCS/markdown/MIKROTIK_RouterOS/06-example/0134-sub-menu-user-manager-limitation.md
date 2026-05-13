## Sub-menu: `/user-manager limitation` 

Limitations are used by Profiles and are linked together by Profile-Limitations. RADIUS accounting and Interim updates must be enabled to seamlessly switch between multiple limitations or disconnect active sessions when download-limit, upload-limit or uptime-limit is reached. 

To disconnect already active sessions from User Manager, accept must be set to yes on the RADIUS client side. If simultaneous session limits are not unlimited (shared-users) and it has reached the maximum allowed number, then the router will try to disconnect the older user session first. 

User-Manager attempts to disconnect an active session before a new user will be accepted (when the appropriate limit is set), that's why in such setups it is suggested to use 1s for /radius client timeout. 

**==> picture [13 x 13] intentionally omitted <==**

IPsec service in RouterOS does not support rate limitations.
