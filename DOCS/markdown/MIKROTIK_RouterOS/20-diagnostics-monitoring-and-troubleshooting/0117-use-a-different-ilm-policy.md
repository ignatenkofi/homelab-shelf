## Use a different ILM policy 

If you want your NetFlow data to have a different retention period, then you need to do the following steps: 

1.  Create a new ILM policy, give it a new name and set the desired period for the delete phase, or use this API request: 

```
PUT _ilm/policy/netflow-logs
{
  "policy": {
    "phases": {
      "hot": {
        "min_age": "0ms",
        "actions": {
          "rollover": {
            "max_age": "30d",
            "max_primary_shard_size": "50gb"
          },
          "set_priority": {
            "priority": 101
          }
        }
      },
      "delete": {
        "min_age": "1000d",
        "actions": {
          "delete": {
            "delete_searchable_snapshot": true
          }
        }
      }
    }
  }
}
```

1829 

2.  Goto Kibana, open "Stack Management", then go to "Index Management" and then "Component Templates" 3.  Search for "logs-netflow.log@custom", open it and edit it 4.  Go to the "Index settings" section 5.  Paste in the following: 

```
{
  "index": {
    "lifecycle": {
      "name": "netflow-logs"
    }
  }
}
```

6.  Press "Next" and then "Save component template" 

1830
