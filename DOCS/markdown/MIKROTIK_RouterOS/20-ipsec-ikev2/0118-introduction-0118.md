## Introduction 

Let's take a look at the SSTP connection mechanism: 

**==> picture [504 x 212] intentionally omitted <==**

1.  A TCP connection is established from client to server (by default on port 443); 

2.  SSL validates the server certificate. If a certificate is valid, a connection is established otherwise the connection is turned down. (But see note below); 

3.  The client sends SSTP control packets within the HTTPS session which establishes the SSTP state machine on both sides; 

4.  PPP negotiation over SSTP. The client authenticates to the server and binds IP addresses to the SSTP interface; 

SSTP tunnel is now established and packet encapsulation can begin; 

**==> picture [13 x 13] intentionally omitted <==**

Starting from v5.0beta2 SSTP does not require certificates to operate and can use any available authentication type. This feature will work only between two MikroTik routers, as it is not in accordance with Microsoft standards. Otherwise to establish secure tunnels mschap authentication and client/server certificates from the same chain should be used. 

1263 

**==> picture [13 x 13] intentionally omitted <==**

TLS SNI support has been added starting with 7.15beta10 version, Extension will be added to client hello packets if "Add SNI" checkbox is checked or set in CLI: 

interface/sstp-client/set add-sni=yes
