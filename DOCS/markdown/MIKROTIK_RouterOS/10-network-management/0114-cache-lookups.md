## Cache Lookups 

```
/ip/proxy/lookup
```

This menu shows statistics on objects read from cache (cache lookups). 

Read-only properties: 

**==> picture [501 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>denied  (integer) Number of requests denied by the access list.<br>expired  (integer) Number of requests found in cache, but expired, and, thus, requested from an external server<br>**----- End of picture text -----**<br>

938 

no-expiration-info (integ Conditional request received for a page that does not have the information to compare the request with er) non-cacheable (integer) Number of requests requested from the external servers unconditionally (as their caching is denied by the cache access list) not-found (integer) Number of requests not found in the cache, and, thus, requested from an external server (or parent proxy if configured accordingly) successes (integer) Number of requests found in the cache.
