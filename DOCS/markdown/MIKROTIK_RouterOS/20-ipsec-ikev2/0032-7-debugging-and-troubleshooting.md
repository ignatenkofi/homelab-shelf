## 7. Debugging and Troubleshooting 

To verify QKD integration and key retrieval, enable IPsec debug logging: 

```
/system logging add topics=ipsec,debug action=memory
```

Sample debug output showing QKD key retrieval: 

```
2025-10-11 17:32:38 ipsec,debug,packet POST /api/v1/keys/mt-aaa/enc_keys HTTP/1.1\r\n
2025-10-11 17:32:38 ipsec,debug,packet Host: 10.13.2.9\r\n
2025-10-11 17:32:38 ipsec,debug,packet {"number":1,"size":64}
2025-10-11 17:32:38 ipsec,debug,packet HTTP/1.1 200 OK\r\n
2025-10-11 17:32:38 ipsec,debug,packet {"keys":[{"key_ID":"37f4c842-dd82-4c49-8dfc-52a3793e5331","key":"m
/JIEIUCzAE="}]}
2025-10-11 17:32:38 ipsec,debug,packet qkd: add to cache key 37f4c842-dd82-4c49-8dfc-52a3793e5331: 9bf24
```

If keys are not being added to cache, check network connectivity to the KME, certificate validation, and correct `kme-id` and `peer-sae-id` configuration.
