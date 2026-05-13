## CAPsMAN device: 

In CAPsMAN Manager menu set Certificate and CA Certificate to auto: 

```
/caps-man manager
set ca-certificate=auto certificate=auto
```

Print output: 

```
[admin@CAPsMAN] /caps-man manager print
                  enabled: yes
              certificate: auto
           ca-certificate: auto
             package-path:
           upgrade-policy: none
 require-peer-certificate: no
    generated-certificate: CAPsMAN-D4CA6D987C26
 generated-ca-certificate: CAPsMAN-CA-D4CA6D987C26
```

CAPsMAN device first will generate CA-Certificate and then it will generate Certificate which depends on CA-Certificate.
