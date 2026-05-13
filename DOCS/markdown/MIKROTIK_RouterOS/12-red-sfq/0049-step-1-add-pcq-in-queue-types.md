## Step 1: add PCQ in Queue Types 

Add two new entries - one for download and one for upload. `dst-address` is a classifier for the user's download traffic, and `src-address` for upload traffic: 

```
/queue type add name="PCQ_download" kind=pcq pcq-rate=64000 pcq-classifier=dst-address
/queue type add name="PCQ_upload" kind=pcq pcq-rate=32000 pcq-classifier=src-address
```
