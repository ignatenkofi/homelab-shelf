## Using Kibana 

**==> picture [13 x 13] intentionally omitted <==**

Some steps might change over time, refer to Elastic's manual to find the most up-to-date steps. 

The NetFlow Records integration provides some useful assets that can be used to analyze NetFlow data. Make sure you install the assets first before continuing. The following section will give you some basic ways how to see NetFlow data. 

1.  Log into your Kibana 

2.  Open the "Dashboards" menu in the main menu 

3.  Search the Dashboards and find "NetFlow" 

You should now see multiple NetFlow Dashboards. For example, try opening the "[Logs Netflow] Overview". If your NetFlow data is properly ingested, then you should now see graphs that summarizes your traffic. 

Another useful Dashboard is the "[Logs Netflow] Flow records", which shows you exact NetFlow records. A very useful feature is the filtering option (the + button on top), that allows you add filters to NetFlow data, for example, you can filter the records to show only a single IP address: 

**==> picture [505 x 116] intentionally omitted <==**

There are other options such as searching for a specific time range. You should read more about Discover to understand the possibilities better. 

For quick reference, these are the fields that you are most likely going to want to use for searching NEtFlow data: 

source.ip source.port destination.ip destination.port network.transport 

If you want to examine a single record, it is recommended to use the Discover view. NetFlow data can be found as "data_stream.dataset: netflow.log".
