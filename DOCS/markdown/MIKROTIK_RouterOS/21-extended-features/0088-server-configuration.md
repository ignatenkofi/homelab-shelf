## Server configuration 

You should have generated ca.crt (Certificate Authority file), server.crt (server certificate) and server.key (server's key): 

```
C:\Users\Administrator\Desktop\Container>dir
 Directory of C:\Users\Administrator\Desktop\Container
```

```
07/12/2023  10:58 AM    <DIR>          .
07/12/2023  10:58 AM    <DIR>          ..
07/12/2023  10:56 AM             1,322 ca.crt
07/12/2023  10:56 AM             1,854 ca.key
07/12/2023  09:57 AM                35 mosquitto.conf
07/12/2023  10:58 AM             1,164 server.crt
07/12/2023  10:57 AM               960 server.csr
07/12/2023  10:56 AM             1,704 server.key
               6 File(s)          7,039 bytes
               2 Dir(s)  52,401,184,768 bytes free
```

Open mounted " mosquitto.conf " via your preferred text editor (notepad or any other), and just overwrite it with the lines shown below: 

```
tls_version tlsv1.2
port 8883
allow_anonymous true
cafile /mosquitto/config/ca.crt
keyfile /mosquitto/config/server.key
certfile /mosquitto/config/server.crt
```

tls_version line sets minimal TLS version; 

listener 8883 , will make the installation listen for incoming network connection on the specified port; allow_anonymous true , determines whether clients that connect without providing a username are allowed to connect; 

1879 

**==> picture [13 x 13] intentionally omitted <==**

We are using a basic SSL configuration for testing purposes. allow_anonymous true is not a secure setting for the production environment. 

cafile /mosquitto/config/ca.crt line specifies a path to the CA certificate file; keyfile /mosquitto/config/server.key line specifies a path to the server key file; certfile /mosquitto/config/server.crt line specifies a path to the server certificate file. 

Upload the certificate files, and updated SSL-ready mosquitto.conf file into the mounted folder " mosquitto_mounted ": 

```
C:\Users\Administrator\Desktop\Container>sftp admin@192.168.88.1
Connected to 192.168.88.1.
sftp> cd mosquitto_mounted
sftp> dir
mosquitto.conf
sftp> put ca.crt
Uploading ca.crt to /mosquitto_mounted/ca.crt
ca.crt                                                                                100% 1322   323.0KB/s
00:00
sftp> put server.crt
Uploading server.crt to /mosquitto_mounted/server.crt
server.crt                                                                            100% 1164   227.3KB/s
00:00
sftp> put server.key
Uploading server.key to /mosquitto_mounted/server.key
server.key                                                                            100% 1704   415.7KB/s
00:00
sftp> dir
ca.crt           mosquitto.conf   server.crt       server.key
sftp> put mosquitto.conf
Uploading mosquitto.conf to /mosquitto_mounted/mosquitto.conf
mosquitto.conf                                                                        100%  162    32.2KB/s
00:00
```
