[[_TOC_]]

# Aggregator Service

- Across different services operating under a standard API, the service offers a framework for flash design data. It also offers a common endpoint for configuring data within the system. 

- The client can request one or multiple data points from this endpoint
  

![](https://miro.medium.com/v2/resize:fit:700/1*qK2uEGMAn_fXt8ietv4FGg.png)

- There is no data stored by this service. It is an alteration of data that has been taken from various services. 
  
- This will help the runtime system to pull design data points as needed.
  

# Example

This aggregator service allows clients to obtain data for any entity from runtime.

The client requests entities A, C, and D on page 1, and additional entities are requested on the following page.

As a result, runtime views on design time deployment are no longer created. Give a closely coupled data API as well.

![2023-04-02-07-39-44-image.png](/.attachments/2023-04-02-07-39-44-image-f8f4e7c4-be18-4004-9a7a-4dfd751770bf.png)
# Flow

- Endpoint uses a factory pattern for the implementation
  
- Factory contains a collection of entities and their corresponding query.
  
- System run those query parallelly and map them to the object
  
- If no entity is requested, the system returns an empty object

![2023-04-02-07-43-47-image.png](/.attachments/2023-04-02-07-43-47-image-a3daffda-34e9-48e9-b543-1ec589cbd061.png)


# Endpoints

- Service contains 2 endpoints
  
  - First give design data for the given sponsor, study, and study version. 

   - The second one to provide cots Data
    
- The client can request data for an entity by passing the entity name in the query string. Example
  

```
http://dev-flash.api.eclinical.ai/api/study-config?entity=countries&entity=term-mapping&entity=study-elements
```

#### COTS API 


https://dev-flash-api-doc.eclinical.ai/api-details#api=Aggregator&operation=Cots-Configuration-Aggregator

![image.png](/.attachments/image-15571105-bc20-47d3-9207-76e7aa8e5c4d.png)

#### Study Design API

https://dev-flash-api-doc.eclinical.ai/api-details#api=Aggregator&operation=Design-Configuration-Aggregator

![image.png](/.attachments/image-07a8fc0b-0336-4118-98c6-4cc0c56f4a53.png)