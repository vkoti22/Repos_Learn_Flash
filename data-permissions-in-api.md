---
title: Data Permissions in API
category: Development
tags:
  - permissions
  - COTS

tracks:
  - Architect
  - Developer

owners:
  - Praveen
  - Attie
  - Vikram
  - Titus

rank: 200
---

# Process
The follow steps outline the process for Data Permissions in API:
- A wrapper is added which runs a regular process like **auth**, getting data from DB & other business logic. 
- Once the response is ready, then the data permission will be applied at the field level. 
- Furthermore, if user has the correct permission:
	- (1) then user will get the data.
	- (2) otherwise/else data will be scrubbed from response and user will get a restricted text instead of actual value (i.e. unicode for lock emoji). 
		- The restricted text is configurable per service. 

![image.png](/.attachments/image-699cb6cf-4d8e-44a5-ac5a-27653d14ba17.png)
*The diagram displays the Process for Data Permissions in API*




# Processing

![image.png](/.attachments/image-7bcc9072-3a0a-41e6-8ada-c0defb2b5df8.png)
*The diagram displays the Processing for Data Permissions in API*

 1. Get Permission Config from COTS.
 2. Get User Data Permission in a given context.
 3. Get Permission Config from COTS specific for a study.
 4. Check if User Data Permission matches data permission.
 5. If matches, then user gets **actual** text.
 6. If not-match, then user gets **restricted** text. 

### Further guidance
- As a Developer, you provide the properties on which data restriction need to be applied.
- In the API call, fields not specifically permissioned, (i.e. other fields) in response are treated as **non-restricted** fields. 
- If COTS is missing, then the response is treated as **non-restricted**.

- COTS can process all types of fields:
   - simple field - specific property name (i.e. username)
   - complex field - specific in pattern of parent.child (i.e. user.name)
   - Array - represent array as * (i.e. users[*].name)

# Sample config 


```
[
  {
    "ttl": -1,
    "id": "PatientView", //Unique Id
    "isActive": true, //Whether record is active or not
    "docType": "DataRestrictionConfigModel", // Should be same always
    "startDate": "2022-08-09T11:18:37.2608317-04:00", //Start Date 
    "endDate": "9999-12-31T23:59:59.9999999+00:00", //End date should be 99999
    "partitionKey": "DataRestrictionConfigModel", // Should be same always
    "dataKey": "PatientView",  //Name of the model 
    "propertyDataRestrictions": [ 
      {
        "property": "Pii.Initials", //name of the property
        "dataPermissions": { // As of today we just have these 3 data permisison, specific all which needs permission.
          "AccessToPersonalHealthInformation": false, 
          "AccessToPersonalIdentifiableInformation": true,
          "AccessToUnblindedInformation": false
        }
      }
    ],
    "uniqueConstraintId": {
      "constraint1": "PatientView"
    }
  }
]
```

# Code File

https://github.com/endpoint-Clinical/flash-core/blob/main/Endpoint.Flash.Core.Function/HttpFunction/HttpGetFunctionExecutor.cs

### 🪄Magic file doing all processing. 