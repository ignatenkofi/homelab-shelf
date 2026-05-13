## RouterOS script 

You can run this script in the Scheduler tool, with an interval of 1s, to have your coordinates sent every 1 second. 

```
{
:global lat
:global lon
/system gps monitor once do={
:set $lat $("latitude")
:set $lon $("longitude")
}
tool fetch mode=http url="http://YOURSERVER.com/index.php" port=80 http-method=post http-data=("{\"lat\":\"" .
$lat . "\",\"lon\":\"" . $lon . "\"}") http-header-field="Content-Type: application/json"
:put ("{\"lat\":\"" . $lat . "\",\"lon\":\"" . $lon . "\"}")
}
```
