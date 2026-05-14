## Sending information to a remote host 

It is possible to use an HTTP POST request to send information to a remote server, that is prepared to accept it. In the following example, we send geographic coordinates to a PHP page: 

```
/tool/fetch http-method=post http-header-field="Content-Type:application/json" http-data="{\"lat\":\"56.12\",\"
lon\":\"25.12\"}" url="https://testserver.lv/index.php"
```

In this example, the data is uploaded as a file. Important note, since variable data comes from a file, a file can only be in size up to 4KB. This is a limitation of RouterOS variables. 

```
/export file=export.rsc
```

```
:global data [/file get [/file find name=export.rsc] contents];
```

```
:global $url "https://prod-51.westeurope.logic.azure.com:443/workflows/blabla/triggers/manual/paths/invoke....";
```

```
/tool fetch mode=https http-method=put http-data=$data url=$url
```
