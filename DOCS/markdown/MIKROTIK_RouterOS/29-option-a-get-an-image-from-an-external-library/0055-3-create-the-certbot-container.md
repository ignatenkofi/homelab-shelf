## 3.  Create the Certbot Container: 

1866 

```
/container/mounts/add name=MOUNT_CERTBOT_CONFIG src=disk1/volumes/certbot/config dst=/etc/letsencrypt
/container/mounts/add name=MOUNT_CERTBOT_DATA src=disk1/volumes/certbot/data dst=/var/lib/letsencrypt
/container/mounts/add name=MOUNT_CERTBOT_LOG src=disk1/volumes/certbot/log dst=/var/log/letsencrypt
/container/mounts/add name=MOUNT_CERTBOT_HAPROXY src=disk1/volumes/haproxy/config dst=/etc/haproxy
/container/add remote-image=certbot/dns-rfc2136 cmd="certonly -n --agree-tos --dns-rfc2136 --dns-rfc2136-
credentials /etc/letsencrypt/rfc2136.ini -m admin@<FQDN> --deploy-hook 'cat /etc/letsencrypt/li\
    ve/<FQDN>/fullchain.pem /etc/letsencrypt/live/<FQDN>/privkey.pem | tee /etc/haproxy/certs/<FQDN>.pem
> /dev/null; echo -e \"set ssl cert /usr/local/e\
    tc/haproxy/certs/<FQDN>.pem <<\
```

```
    \n\$(cat /etc/haproxy/certs/<FQDN>.pem)\
    \n\" | nc 127.0.0.1:9999; echo \"commit ssl cert /usr/local/etc/haproxy/certs/<FQDN>.pem\" | nc
127.0.0.1:9999' -d <FQDN> --cert-name <FQDN>" \
```

```
    interface=veth1 logging=yes mounts=MOUNT_CERTBOT_CONFIG,MOUNT_CERTBOT_DATA,MOUNT_CERTBOT_LOG,
MOUNT_CERTBOT_HAPROXY name=certbot root-dir=\
```

```
    disk1/images/certbot start-on-boot=yes workdir=/opt/certbot
```

**==> picture [13 x 13] intentionally omitted <==**

Make sure to replace all `<FQDN>` placeholders in the example above with your fully qualified domain name! 

4.  Wait for the Container image to be downloaded and start the Certbot Container: 

```
/container start [find where name=certbot]
```

5.  Check the logs to make sure you successfully received a new certificate: 

```
/log print follow
```
