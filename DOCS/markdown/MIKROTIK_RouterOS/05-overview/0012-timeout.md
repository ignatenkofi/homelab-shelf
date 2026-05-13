## Timeout 

If the command runs indefinitely, it will timeout and the connection will be closed with an error. The current timeout interval is 60 seconds. To avoid timeout errors, add a parameter that would sufficiently limit the command execution time. 

**==> picture [13 x 13] intentionally omitted <==**

Timeout is not affected by the parameters passed to the commands. If the command is set to run for an hour, it will terminate early and return an error message. 

For example, let's see what we get when the ping command exceeds the timeout and how to prevent this by adding a count parameter: 

- `$ curl -k -u admin: -X POST https://10.155.101.214/rest/ping \` 

- `--data '{"address":"10.155.101.1"}' \` 

- `-H "content-type: application/json"` 

- `{"detail":"Session closed","error":400,"message":"Bad Request"}` 

230 

- `$ curl -k -u admin: -X POST https://10.155.101.214/rest/ping \` 

- `--data '{"address":"10.155.101.1","count":"4"}' \` 

- `-H "content-type: application/json"` 

```
[{"avg-rtt":"453us","host":"10.155.101.1","max-rtt":"453us","min-rtt":"453us","packet-loss":"0","received":"1","
sent":"1","seq":"0","size":"56","time":"453us","ttl":"64"},
```

```
{"avg-rtt":"417us","host":"10.155.101.1","max-rtt":"453us","min-rtt":"382us","packet-loss":"0","received":"2","
sent":"2","seq":"1","size":"56","time":"382us","ttl":"64"},
{"avg-rtt":"495us","host":"10.155.101.1","max-rtt":"650us","min-rtt":"382us","packet-loss":"0","received":"3","
sent":"3","seq":"2","size":"56","time":"650us","ttl":"64"},
{"avg-rtt":"461us","host":"10.155.101.1","max-rtt":"650us","min-rtt":"359us","packet-loss":"0","received":"4","
sent":"4","seq":"3","size":"56","time":"359us","ttl":"64"}]
```

Another example is a bandwidth test tool, which can be limited by providing run duration: 

```
$ curl -k -u admin: -X POST 'https://10.155.101.214/rest/tool/bandwidth-test' \
  --data '{"address":"10.155.101.1","duration":"2s"}' \
```

```
  -H "content-type: application/json"
[{".section":"0","connection-count":"20","direction":"receive","lost-packets":"0",
```

```
"random-data":"false","rx-10-second-average":"0","rx-current":"0","rx-size":"1500",
```

```
"rx-total-average":"0",
"status":"connecting"},
```

```
{".section":"1","connection-count":"20","direction":"receive","duration":"1s",
```

```
"lost-packets":"0","random-data":"false","rx-10-second-average":"0","rx-current":"0",
```

```
"rx-size":"1500","rx-total-average":"0",
```

```
"status":"running"},
```

```
{".section":"2","connection-count":"20","direction":"receive","duration":"2s",
```

```
"lost-packets":"581175","random-data":"false","rx-10-second-average":"854372352",
```

```
"rx-current":"854372352","rx-size":"1500","rx-total-average":"854372352",
"status":"running"},
```

```
{".section":"3","connection-count":"20","direction":"receive","duration":"3s",
```

```
"lost-packets":"9014","random-data":"false","rx-10-second-average":"891979008",
```

```
"rx-current":"929585664","rx-size":"1500","rx-total-average":"891979008",
"status":"done testing"}]
```
