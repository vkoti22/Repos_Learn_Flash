Title: File Upload

Tracks 

Architect
Developer

Owners

-Praveen

-Attie

-Vikram

-Titus

Rank:200

# High-Level Process  

- The system permits a certain range of file sizes from 100k+ to 5 million (100,000 to 5,000,000).

- Once it uploads, it validates the schema, and then it reads the header of the file.

- The header information is then passed to the client.  
  
- Maps with the user perform. It re-validates the schema based on the data and saves the information. 
  

![image.png](/.attachments/image-cbedf0c5-91c9-41aa-a7b4-ea584df21619.png)



# Approach (we are not taking)

From the client server through API associated with chunks of the data into Raw BLOB/storage account.

- It reads the file and connects to the Library(Web Server)

- It saves in a temporary manner and shows active on deployment.


![image.png](/.attachments/image-2b415bea-9abf-42d8-8a7e-ed90e748fed2.png)

# Approach (to follow)
This kind of approach is a combination of file upload and a complete approach process.
- The Process starts with file reading from the client source through API associated with chunks of the data into the Raw BLOB/storage account.

- It uses web API serves to read data from ADX along with KGL query.

- From the steps of the BLOB/storage account it deviates to trigger the ADF process which directs to complete the process of ADF. 

- ADF starts with Read Header, validates the data and saves it into cosmos and function call to send a response back. 

- At the Runtime validation scheme it turns the file into CSV Bronze creates an external table and repeats for the functional call.

- ADF send the signal response and it reaches the client. 

![File_Upload_Rand-Cool Stuff.drawio.png](/.attachments/File_Upload_Rand-Cool%20Stuff.drawio-595eac0d-0cca-4156-9a01-24fd7f8f270e.png)


# Approach (to follow)
This approach is a combination of file upload and a complete approach process.
- The Process starts with file reading from the client source through API associated with chunks of the data into the Raw BLOB/storage account.

- It uses web API serves to read data from ADX along with KGL query.

- From the steps of the BLOB/storage account it deviates to trigger the ADF process which directs to complete the process of ADF. 

- ADF starts with Read Header, validates the data and saves into cosmos and function call to send a response back. 

- At Runtime validation scheme it turns the file into CSV Bronze and creates an external table and repeats for functional call.

- ADF send the signal response and it reaches the client. 

![File_Upload_Rand-Cool Stuff.drawio.png](/.attachments/File_Upload_Rand-Cool%20Stuff.drawio-595eac0d-0cca-4156-9a01-24fd7f8f270e.png)