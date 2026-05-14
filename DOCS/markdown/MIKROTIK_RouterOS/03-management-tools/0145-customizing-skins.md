## Customizing skins 

Here is an example of the "Status" page that can be used within the skin *.json file: status.json 

The status content is structured as follows: 

```
{"Status": {"Status": {}}}
```

Status records are displayed in numbered order, example: 

```
"7": {
```

```
  "alias": (path to the record),
```

```
  "note": (optional; free form text that appears under the record),
```

```
  "name": (optional; alternative name for the record),
```

```
  "tab": (optional; name of the tab that this and following records belong to),
  "separator": 1 (optional; should a separating line be placed above his record)
},
```
