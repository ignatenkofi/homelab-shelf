## Using Kibana 

Kibana allows you to search the ingested CEF logs to see ingested logs do the following: 

1.  Log into your Kibana 2.  Open "Discover" from the main menu 3.  Add a filter, use the following parameters: 

```
Select a field: data_stream.dataset
Select operator: IS
Select a value: cef.log
```

4.  For simplicity we recommend searching for fields in the  Discover menu and searching for "message", then adding the field to the view 

5.  We also recommend searching for "host.name" field and adding to the view as well. 6.  Consider saving the search for easier access later 7.  Done! 

1780
