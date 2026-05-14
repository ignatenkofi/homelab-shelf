## Setting up scheduler 

Last, create your scheduler that will run the previously created script. Choose a proper scheduler interval, so two or more events do not overlap with each other. For this example above, 3 minutes will be enough. 

```
/system scheduler add interval=3m on-event=roamingScript name=Roaming
```

```
/system scheduler add interval=3m on-event=failoverScript name=Failover
```

Keep in mind that a "home" SIM card will consume some roaming data because changing SIM slots does not happen instantly. 

833
