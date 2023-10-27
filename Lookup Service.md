# Reason 

- Flash, a microservices/mini service architecture, has specific requirements for querying small data from other services. 
- These kind of data can be used for query in service and validation purpose.
-  The Lookup service utilizes an audit record to create a quick key value pair, which can be retrieved via point read, providing a cache-like response. 

# Process Flow 

![image.png](/.attachments/image-57c79afc-64e2-410e-a8b5-bfabfeb909ea.png)


# Config 
- The configuration in the ancillary includes a key named LookupConfigs.
- This dictionary contains a DocType from an audit, along with a path and unique identifier for linking to a document.
- Example

```
{
      "KeyName": "LookupConfigs",
      "Value": {
        "SponsorModel": [
          {
            "Path": "Name",
            "UniqueIdentifier": "Id"
          }
        ],
        "StudySettingViewModel": [
          {
            "Path": "StudyName",
            "UniqueIdentifier": "Id"
          }
        ]
      },
      "Content_Type": "application/json"
    }
```
