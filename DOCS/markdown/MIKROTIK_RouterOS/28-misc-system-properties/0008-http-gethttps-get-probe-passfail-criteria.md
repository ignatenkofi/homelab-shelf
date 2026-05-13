## HTTP-GET/HTTPS-GET probe pass/fail criteria 

**==> picture [516 x 240] intentionally omitted <==**

**----- Start of picture text -----**<br>
Property Description<br>thr-http-time  (Default:  10s ) Fail threshold for http-resp-time<br>http-code-min  (Default:  1 OK/fail criteria for HTTP response code.<br>00 )<br>http-code-max  (Default:  2 Response in the range [ http-code-min  ,  http-code-max ] is a probe pass/OK; outside - a probe fail. See mozilla-http-<br>99 ) status or rfc7231<br>DNS probe options<br>Property Description<br>host  (Default:"") DNS name that should be resolved.<br>record-type  (A | AAAA | MX | NS; Default:  A Record type that will be used for DNS probe.<br>)<br>dns-server The DNS server that the probe should send its requests to, if not specified it will use the value from " /ip<br>dns ".<br>**----- End of picture text -----**<br>
