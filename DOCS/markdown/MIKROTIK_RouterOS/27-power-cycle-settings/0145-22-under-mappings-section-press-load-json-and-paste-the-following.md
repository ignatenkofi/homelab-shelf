## 22.  Under "Mappings" section, press "Load JSON" and paste the following: 

```
{
  "dynamic_templates": [],
  "properties": {
    "service": {
      "type": "object",
      "properties": {
        "name": {
          "type": "keyword"
        }
      }
    },
    "destination": {
      "type": "object",
      "properties": {
        "port": {
          "type": "long"
        },
        "ip": {
          "type": "ip"
        }
      }
    },
    "host": {
      "type": "object",
      "properties": {
        "ip": {
          "type": "ip"
        }
      }
    },
    "client": {
      "type": "object",
      "properties": {
        "ip": {
          "type": "ip"
        },
        "mac": {
          "type": "keyword"
        }
```

1785 

```
      }
    },
    "source": {
      "type": "object",
      "properties": {
        "geo": {
          "type": "object",
          "properties": {
            "continent_name": {
              "ignore_above": 1024,
              "type": "keyword"
            },
            "region_iso_code": {
              "ignore_above": 1024,
              "type": "keyword"
            },
            "city_name": {
              "ignore_above": 1024,
              "type": "keyword"
            },
            "country_iso_code": {
              "ignore_above": 1024,
              "type": "keyword"
            },
            "country_name": {
              "ignore_above": 1024,
              "type": "keyword"
            },
            "location": {
              "type": "geo_point"
            },
            "region_name": {
              "ignore_above": 1024,
              "type": "keyword"
            }
          }
        },
        "as": {
          "type": "object",
          "properties": {
            "number": {
              "type": "long"
            },
            "organization": {
              "type": "object",
              "properties": {
                "name": {
                  "ignore_above": 1024,
                  "type": "keyword",
                  "fields": {
                    "text": {
                      "type": "match_only_text"
                    }
                  }
                }
              }
            }
          }
        },
        "address": {
          "ignore_above": 1024,
          "type": "keyword"
        },
        "port": {
          "type": "long"
        },
        "domain": {
          "ignore_above": 1024,
          "type": "keyword"
        },
        "ip": {
```

1786 

```
          "type": "ip"
        },
        "mac": {
          "type": "keyword"
        }
      }
    },
    "event": {
      "type": "object",
      "properties": {
        "duration": {
          "type": "long"
        },
        "category": {
          "type": "keyword"
        },
        "outcome": {
          "type": "keyword"
        }
      }
    },
    "message": {
      "type": "match_only_text"
    },
    "user": {
      "type": "object",
      "properties": {
        "name": {
          "type": "keyword"
        }
      }
    },
    "network": {
      "type": "object",
      "properties": {
        "bytes": {
          "type": "long"
        },
        "name": {
          "type": "keyword"
        },
        "transport": {
          "type": "keyword"
        }
      }
    },
    "tags": {
      "ignore_above": 1024,
      "type": "keyword"
    }
  }
}
```

23.  Press "Next" and then press "Save component template" 

**==> picture [13 x 13] intentionally omitted <==**

If a component template exists with such a name, then edit the existing one instead. 

24.  Go to "Stack Management" on the main menu, then select "Index Management" and then select "Index templates" 

> 25.  Create a new template by pressing "Create template" 

26.  Set the "Name" to "logs-routeros" 

27.  Set "Index patterns" to "logs-routeros-*" 28.  Under "Component templates" section add the following templates to your new Index template: 

1787 

```
logs@settings
logs-routeros@custom
ecs@mappings
```

29.  Press "Next" and then "Save template" 

30.  Make sure you have opened the 5514/UDP port on your host and elsewhere in the path from your RouterOS device (10.0.0.1). 31.  Your Elastic Agent is now ready to receive Syslog data!
