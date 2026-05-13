## Overview 

Watch our video about this feature. 

The term "REST API" generally refers to an API accessed via HTTP protocol at a predefined set of resource-oriented URLs. Starting from RouterOS v7.1beta4 , it is implemented as a JSON wrapper interface of the console API. It allows to create, read, update and delete resources and call arbitrary console commands. 

To start using REST API, the `www-ssl` or `www` (starting with RouterOS v7.9 ) service must be configured and running. When the `www-ssl` service (HTTPS access) is enabled, the REST service can be accessed by connecting to `https://<routers_IP>/rest` . When `www` service (HTTP access) is enabled the REST service can be accessed by connecting to `http://<routers_IP>/rest` . 

**==> picture [13 x 13] intentionally omitted <==**

We do not advise enabling HTTP access ( `www` service). The main risk is that authentication credentials can be read with passive eavesdropping. You can use it only when performing tests (not in a production environment) and when you are certain that nobody can listen in (inspect your traffic)! 

The easiest way to start is to use cURL, wget, or any other HTTP client even RouterOS fetch tool. 

```
$ curl -k -u admin: https://10.155.101.214/rest/system/resource
[{"architecture-name":"tile","board-name":"CCR1016-12S-1S+",
"build-time":"Dec/04/2020 14:19:51","cpu":"tilegx","cpu-count":"16",
"cpu-frequency":"1200","cpu-load":"1","free-hdd-space":"83439616",
"free-memory":"1503133696","platform":"MikroTik",
"total-hdd-space":"134217728","total-memory":"2046820352",
"uptime":"2d20h12m20s","version":"7.1beta4 (development)"}]
```
