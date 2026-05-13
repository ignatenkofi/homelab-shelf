## Prerequisites 

Setup Elasticsearch 

**==> picture [13 x 13] intentionally omitted <==**

Elasticsearch is widely supported on many platforms. It is recommended to setup a cluster of Elasticsearch nodes. 

Setup kibana 

**==> picture [13 x 13] intentionally omitted <==**

Kibana can be installed on the same device on which you installed Elasticsearch, but it can also be installed on a separate device for performance reasons. While it is possible to analyze CEF logs without Kibana, it requires writing your own API requests, Kibana is very easy to use and has a wide range of features. 

Setup Fleet Server 

**==> picture [13 x 13] intentionally omitted <==**

It is possible to setup Fleet Server on the same device on which you installed Elasticsearch and/or Kibana. It is recommended to install Fleet Server on a different device. Refer to Elasticsearch manual for recommendations on hardware and topology requirements.
