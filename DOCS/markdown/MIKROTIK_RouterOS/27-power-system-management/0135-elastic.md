## Elastic 

**==> picture [13 x 13] intentionally omitted <==**

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps. 

Log into your Kibana 

Open the Fleet section under the main menu Open the "Agent policies" section 

Press "Create agent policy" button to create a new Agent Policy 

Give the policy a name, for example, "CEF policy", adjust advanced settings if required, create the policy. Or you can use the API request below: 

```
POST kbn:/api/fleet/agent_policies
{
  "name": "CEF policy",
  "description": "",
  "namespace": "default",
  "monitoring_enabled": [
    "logs",
    "metrics"
  ],
  "inactivity_timeout": 1209600,
  "is_protected": false
}
```

Open your newly created policy by clicking on it's name Press "Add integration" Search for "Common Event Format (CEF)" and press "Add Common Event Format (CEF)" Adjust configuration, make sure: - Under the "Collect CEF application logs (input: udp)" section set "Syslog Host" to "0.0.0.0" - Under the "Collect CEF application logs (input: tcp)" section set "Syslog Host" to "0.0.0.0" Save the integration Press the "Add Elastic Agent to your host" button Follow the instructions on how to add Elastic Agent to your host 

**==> picture [13 x 13] intentionally omitted <==**

Official Elastic's manual recommends installing the Elastic Agent as Fleet-managed. Consider following the recommendation since managing the agents is easier when they are Fleet-managed. 

Go to "Stack Management" on the main menu, then open "Ingest Pipelines" Create a new Ingest Pipeline by pressing "Create pipeline" then "New pipeline" Set "Name" to "logs-cef.log@custom" Press "Import processors" and paste the following processors: 

```
{
        "processors": [
                {
                        "set": {
                        "ignore_empty_value": true,
                        "field": "host.name",
                        "copy_from": "cef.extensions.deviceHostName"
                        }
                },
                {
                        "set": {
                        "ignore_empty_value": true,
                        "field": "host.ip",
                        "copy_from": "cef.extensions.deviceAddress"
                        }
                }
        ]
}
```

1779 

**==> picture [13 x 13] intentionally omitted <==**

The "logs-cef.log@custom" pipeline is not required, but it makes searching the logs easier when you are using Elasticsearch for other types of logs too. 

Press "Save pipeline" 

Make sure you have opened the 9003/UDP port on your host and elsewhere in the path from your RouterOS device (10.0.0.1). Your Elastic Agent is now ready to receive CEF logs!
