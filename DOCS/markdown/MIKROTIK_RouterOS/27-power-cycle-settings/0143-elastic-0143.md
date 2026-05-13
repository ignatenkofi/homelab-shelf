## Elastic 

**==> picture [13 x 13] intentionally omitted <==**

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps. 

1.  Log into your Kibana 2.  Open the Fleet section under the main menu 3.  Open the "Agent policies" section 4.  Press "Create agent policy" button to create a new Agent Policy 

5.  Give the policy a name, for example, "Syslog policy", adjust advance settings if required, create the policy. Or you can use the API request below: sads 

```
POST kbn:/api/fleet/agent_policies
{
  "name": "Syslog policy",
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

6.  Open your newly created policy by clicking on it's name 7.  Press "Add integration" 8.  Search for "Custom UDP logs" and press "Add Custom UDP logs" 

9.  Adjust configuration, make sure: - Specify "Listen Address" to the IP address of your server that is going to run the Custom UDP logs integration , in this example the address should be "10.0.0.2" 

- Set "Listen Port" to "5514" 

   - Set" Dataset name" to "routeros" 

   - Set "Ingest Pipeline" to "logs-routeros@custom" 

   - Set "Syslog Parsing" to "Yes" 

10.  Save the integration 

11.  Press the "Add Elastic Agent to your host" button 12.  Follow the instructions on how to add Elastic Agent to your host 

**==> picture [13 x 13] intentionally omitted <==**

Official Elastic's manual recommends installing the Elastic Agent as Fleet-managed. Consider following the recommendation since managing the agents is easier when they are Fleet-managed. 

13.  Go to "Stack Management" on the main menu, then open "Ingest Pipelines" 14.  Create a new Ingest Pipeline by pressing "Create pipeline" then "New pipeline" 

15.  Set "Name" to "logs-routeros@custom" 

16.  Press "Import processors" and paste the following processors: 

```
{
        "processors": [
                {
                        "grok": {
                        "field": "message",
                        "patterns": [
                                "^first L2TP UDP packet received from %{IP:source.ip}$",
                                "^login failure for user %{USERNAME:user.name} from %{IP:source.ip} via %
{DATA:service.name}$",
                                "^%{USERNAME:user.name} logged in, %{IP:client.ip} from %{IP:source.
ip}$",
                                "^dhcp alert on %{DATA}: discovered unknown dhcp server, mac %{MAC:
source.mac}, ip %{IP:source.ip}$",
                                "in:%{DATA} out:%{DATA}, ?(connection-state:%{DATA},|)?(src-mac %{MAC:
source.mac},|) proto %{DATA:network.transport} \\(%{DATA}\\), %{IP:source.ip}:?(%{INT:source.port}|)->%
{IP:destination.ip}:?(%{INT:destination.port}|), len %{INT:network.bytes}$",
                                "in:%{DATA} out:%{DATA}, ?(connection-state:%{DATA},|)?(src-mac %{MAC:
```

1782 

```
source.mac},|) proto %{DATA:network.transport}, %{IP:source.ip}:?(%{INT:source.port}|)->%{IP:destination.
ip}:?(%{INT:destination.port}|), len %{INT:network.bytes}$",
                                "^%{DATA:network.name} (deassigned|assigned) %{IP:client.ip} for %{MAC:
client.mac} %{DATA}$",
                                "^%{DATA:user.name} logged out, %{INT:event.duration} %{INT} %{INT} %
{INT} %{INT} from %{IP:client.ip}$",
                                "^user %{DATA:user.name} logged out from %{IP:source.ip} via %{DATA:
service.name}$",
                                "^user %{DATA:user.name} logged in from %{IP:source.ip} via %{DATA:
service.name}$",
                                "^%{DATA:network.name} client %{MAC:client.mac} declines IP address %{IP:
client.ip}$",
                                "^%{DATA:network.name} link up \\(speed %{DATA}\\)$",
                                "^%{DATA:network.name} link down$",
                                "^user %{DATA:user.name} authentication failed$",
                                "^%{DATA:network.name} fcs error on link$",
                                "^phase1 negotiation failed due to time up %{IP:source.ip}\\[%{INT:
source.port}\\]<=>%{IP:destination.ip}\\[%{INT:destination.port}\\] %{DATA}:%{DATA}$",
                                "^%{DATA:network.name} (learning|forwarding)$",
                                "^user %{DATA:user.name} is already active$",
                                "^%{GREEDYDATA}$"
                        ]
                        }
                },
                {
                        "lowercase": {
                        "field": "network.transport",
                        "ignore_missing": true
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.category",
                        "description": "Enrich logon events",
                        "allow_duplicates": false,
                        "value": [
                                "authentication"
                        ],
                        "if": "ctx.message =~ /(login failure for user|logged in from|logged in,)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.outcome",
                        "description": "Enrich successful login events",
                        "allow_duplicates": false,
                        "value": [
                                "success"
                        ],
                        "if": "ctx.message =~ /(logged in from|logged in,)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.outcome",
                        "description": "Enrich failed login events",
                        "allow_duplicates": false,
                        "value": [
                                "failure"
                        ],
                        "if": "ctx.message =~ /(login failure for user)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.category",
                        "description": "Enrich network events",
```

1783 

```
                        "allow_duplicates": false,
                        "value": [
                                "network"
                        ],
                        "if": "ctx.message =~ /( fcs error on link| link down| link up)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.outcome",
                        "description": "Enrich network failures",
                        "allow_duplicates": false,
                        "value": [
                                "failure"
                        ],
                        "if": "ctx.message =~ /( fcs error on link)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.category",
                        "allow_duplicates": false,
                        "value": [
                                "session"
                        ],
                        "if": "ctx.message =~ /(logged out)/"
                        }
                },
                {
                        "append": {
                        "ignore_failure": true,
                        "field": "event.category",
                        "allow_duplicates": false,
                        "value": [
                                "threat"
                        ],
                        "if": "ctx.message =~ /(from address that has not seen before)/"
                        }
                },
                {
```

```
                        "append": {
                        "ignore_failure": true,
                        "field": "service.name",
                        "value": [
                                "l2tp"
                        ],
                        "if": "ctx.message =~ /(^L2TP\\/IPsec VPN)/"
                        }
                },
                {
```

```
                },
                {
```

```
                },
                {
```

1784 

```
                        "field": "client.ip",
                        "target_field": "client.geo"
                        }
                }
        ]
}
```
