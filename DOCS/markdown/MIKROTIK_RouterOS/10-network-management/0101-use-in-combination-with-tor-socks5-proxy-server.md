## Use in combination with TOR SOCKS5 proxy server 

Socksify can be used in combination with TOR to achieve better privacy and anonymity for the application that does not have integrated SOCKS support. Configuration below will allow you to forward HTTP/s traffic through TOR SOCKS5 proxy server. First you will need to configure socksify service. 

```
/ip socksify
add connection-timeout=10 disabled=no name=TOR_socksify socks5-port=9050 socks5-server=<TOR_SOCKS_proxy_IP>
```

After that you will need to configure firewall to ensure that correct traffic is being socksified and socks traffic is allowed. 

927 

```
/ip firewall filter
```

```
add action=accept chain=input dst-port=952 protocol=tcp src-address=<SOCKS_client_IP>
/ip firewall nat
```

```
add action=socksify chain=dstnat dst-port=80,443 protocol=tcp socksify-service=TOR_socksify src-
address=<SOCKS_client_IP>
```

928
