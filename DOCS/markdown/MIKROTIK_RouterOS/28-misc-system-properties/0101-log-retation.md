## Log retation 

Depending on your local laws you might be required to store NetFlow data for a specified period of time. Be aware that busy networks can generated a lot of NetFlow data, even terabytes per day. You are most likely going to want to adjust LIfecycle Policy. By default the NetFlow data should go under the "logs" policy. If you have multiple Elasticsearch nodes, you can utilize "phases", which allows you to store data on different types of storage media, but if you only have a single Elasticsearch node, your options are limited and you will most likely want to delete old data. For example, if you want to delete data after 6 months, then you can simply change the ILM policy to delete data after 6 months or use this API request: 

1828 

```
PUT _ilm/policy/logs
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
        "min_age": "180d",
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

**==> picture [13 x 13] intentionally omitted <==**

If you change the "logs" policy, this will apply to ALL your logs, not just NetFlow data. If you need a different retention period for other logs, then it is better to create a new ILM policy and specify the NetFlow integration to use the newly created ILM policy.
