## Using Kibana 

Kibana allows you to search the ingested Syslog data, to see ingested logs do the following: 

1.  Log into your Kibana 

2.  Open "Discover" from the main menu 3.  Add a filter, use the following parameters: 

```
Select a field: data_stream.dataset
Select operator: IS
Select a value: routeros
```

4.  For simplicity we recommend searching for fields in the  Discover menu and searching for "message", then adding the field to the view 

5.  We also recommend searching for "log.syslog.hostname" field and adding to the view as well. 

6.  Consider saving the search for easier access later 7.  Done! 

**==> picture [13 x 13] intentionally omitted <==**

While searching for logs can be useful, you are more likely looking for a way to create alerts for certain activities and create connectors to send alerts e-mail, webhooks, chats and other options. Consider enabling the Spike in failed logon events rule to alert for excessive failed login attempts. You can also create a threshold rule and set it to alert after fixed amount of failed logins. 

1788
