## Introduction 

Elasticsearch is a popular NoSQL database that can be used to store a wide range of data, including CEF logs. Alongside with Kibana you can create a powerful tool to analyze CEF logs from your RouterOS devices. This guide will rely on Elasticsearch integrations and for it to work you need to have a working Elasticsearch setup. This guide will not cover setup instructions for Elasticsearch and Kibana, but will cover the relevant steps to setup CEF log collection and analysis. 

There are many possible configurations that can be made with Elasticsearch, but for the sake of this guide we will use the following principle: 

A RouterOS (10.0.0.1) device sends out CEF logs to a server (10.0.0.2) running CEF integration 

The server (10.0.0.2) running CEF integration ingests CEF logs, processes the data and sends it to a Fleet Server (10.0.0.3) A Fleet Server (10.0.0.3) stores the data in Elasticsearch (10.0.0.4) Kibana (10.0.0.5) retrieves data from Elasticsearch (10.0.0.4), analyzes it and allows you to search the data 

**==> picture [13 x 13] intentionally omitted <==**

This guide will not use Logstash as a part of analyzing CEF logs, it has been replaced by a Fleet Server. 

**==> picture [13 x 13] intentionally omitted <==**

It is possible to install Elasticsearch, Kibana, Fleet Server and CEF logs integration on the same device.
