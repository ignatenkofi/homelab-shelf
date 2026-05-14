## Subscriptions 

This section is used to manage already-added subscriptions (that were previously added via the Subscribe section). It has the same properties as the Subscribe section. Starting with v7.12beta9 , this menu allows you to add the " on-message " setting to your subscriptions. Property Description on-message (string; Default: ) Configure a script that will be automatically initiated/run whenever a new message is received in the subscribed topic. 

To check already subscribed topics, issue the command: 

`/iot mqtt subscriptions print 0 broker=broker topic="my/test/topic" qos=0` After you publish a test message as shown in the Publish section above: `/iot mqtt publish message="test-message" broker="broker" topic="my/test/topic"` 

You should be able to check the received message under: 

```
/iot mqtt subscriptions recv print
 0 broker=broker topic="my/test/topic" data="test-message" time=2023-05-22 16:57:00
```

**==> picture [13 x 13] intentionally omitted <==**

Received message list is limited to 1024 entries. After which, older entries will get overwritten with the new ones. 

To clear stored messages, issue the command: `/iot mqtt subscriptions recv clear` To run a script (for example, a basic "log" script) whenever any new message appears in the subscribed topic, you can use the `on-message` feature: 

`/iot mqtt subscriptions set on-message={:log info "Got data {$msgData} from topic {$msgTopic}"} broker=broker 0` The script can use $msgData and $msgTopic variables. $msgData defines the MQTT message that was published and $msgTopic defines the MQTT topic, where the message was published. Both variables are automatically generated when a new message appears. 

**==> picture [13 x 13] intentionally omitted <==**

- $msgData and $msgTopic variables will not work when used in the " System>Script " section created scripts, meaning, they will not work inside "/iot mqtt subscriptions set on-message={/system script run x} " added scripts. Both variables will work only when they are used inside the " on-message={} " written script, like, for example, " on-message={:log info "Got data {$msgData} from topic {$msgTopic}"} ". The same applies to global variable usage. If there are global variables that are "generated" using other scripts (variables that appear under System>Script>Environment section), they will not work inside the "on-message" script. 

After you publish a new MQTT message to the subscribed topic, a new log entry should appear: 

1642 

```
/log print
```

```
10:19:15 script,info Got data {test-message} from topic {my/test/topic}
```

A second example shows how to run a script whenever a specific message (keywords from the message) appears. To achieve a scenario, where we want to run a script only when the MQTT message has specific content or a keyword, we can utilize the if condition statement: `/iot mqtt subscriptions set 0 on-messag={:if ($msgData~"\\{\"test\":\"123\"\\}") do={:log info "Got data {$msgData} from topic {$msgTopic}"}}`
