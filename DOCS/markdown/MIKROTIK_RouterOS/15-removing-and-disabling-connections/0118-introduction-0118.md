## Introduction 

Socksify is a service that allows the router to send specific traffic through a SOCKS proxy server, even if the application itself does not natively support proxy connections. 

It intercepts network calls and redirects them through configured SOCKS proxy. 

Socksify service is used in combination with NAT action= `socksify.` 

All available firewall filters can be used to precisely select only per-application/source traffic to be redirected via socks proxy. 

Multiple Socksify services can be configured simultaneously, which allows connections to multiple SOCKS servers for better traffic management.
