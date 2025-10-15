# Azure Storage

| Storage Type | Notes |
| --- | --- |
| Blob Storage | Useful for images/files directly to browser, video/audio streaming, now access blobs using NFS |
| File Storage | Network file share, SMB & NFS |
| Queue Storage | up to 64kb messages |
| Table Storage | NoSQL, Key/Attribute. Cosmos is newer |

## Blob Storage 
**Hierachial Namespace HNS**  
organise in hierachy of directories & sub directories  
increases storage cost but can lower compute costs  

**data lake** 
data stored in natural format. requires HNS & blob storage. Optimised for analytics workloads.  
allows you treat data as if it's stored in an HDFS.  
allows you to access via ABFS (Azure Blob File System - part of Apache Hadopp).  
Access data in one place (don't move) using Azure DataBricks, Azure HDInsights, Synapse Analytics  
- supports ACL, RBAC, Shared Key Authorization, SAS authorization    
- connect using HDFS Cli
- connect using NFS  
- connect using SFTP (setup a user)  

```
# Connect to Blob Storage account with a local user that has a home directory

sftp <myaccount>.<myusername>@<myaccount>.blob.core.windows.net

# Connect to Blob Storage account with a local user that doesn’t have a home directory

sftp <myaccount>.<mycontainer>.<myusername>@<myaccount>.blob.core.windows.net
```

### Costs 
- Tier Storage Costs
- Data Access Costs (more for cooler) 
- Transaction Costs (more for cooler) 
- Geo Replication Costs 
- Outbound Data Transfer Costs 
- Tier change Costs

### Other features 
Storage analystics to see who was using what when  
Storage insights 
- metrics and logs 
- actionable insights/alerts 
- unified view  


### Security 
container access:
- private (no anonymous access)
- container (anonymous read for containers/blobs)
- blob (anonymous read for blobs only)

public: can restrict to VNets (same) or IPs  
private endpoints: stop traffic going over internet 

use of AAD recommended, then SAS over Shared Account Keys 
Set a Stored Accces Policy using RestAPI

**URI and SAS Parameters**
| | |
| --- | --- |
| sv | storage version. later have more capabilities | 
| ss | storage services. e.g. bf = blob and files | 
| st | start time |
| se | expiry time | 
| sr | resource. e.g. b = blobs | 
| sp | permissions. e.g. rw | 
| sip | ip range | 
| spr | protocal e.g. https | 
| sig | signature. authentication code | 




### Tiers 
Cool/Cold/Archive. Must stay in for 30/90/180 days or there is a retrieval charge   
Lifecycle rules to move between tiers. If created/updated more than x days ago. Delete the blob option available. 

**URL** is https://[storageaccountname].blob.core.windows.net  
can create a DNS for blob access 

| Account Type | Notes |
| --- | --- |
| Std GP v2 | most scenarios! (page blobs) | 
| Premium Block Blobs | append/block blobs. High transactions, small blobs, low latency |
| Premium File Shares | high performance needs, SMB & NFS support | 
| Premium Page Blobs | High performace for page blobs. Index-based, sparse data structures (OS's), DBs |

**SMB** Server Message Block  
**NFS** Network File System (linux file system)  

| Blob Type | Description |
| --- | --- |
| Block Blobs | Text or binaries, default type |
| Append Blobs | similiar to blobs but optimized for append operations |
| Page Blobs | up to 8TB in size. More efficient for frequent r/w. VMs use this for OS disks etc | 

| Redundancy | Notes | SLA (# of 9's) | 
| --- | --- |
| LRS | 3 copies, single data centre | |
| ZRS | 3 copies across isolated AV zones| |
| GRS | LRS in 2 regions | 16 |
| RA-GRS | Same but provides read only capability from region 2 | |
| GZRS | ZRS primary + LRS secondary | 16 |
| RA-GZRS | Same but provides read only capability from region 2 | |

Use **G** for regional protection 
Use **Z** for data center protection

### Blob Replication
Requires blob versioning is enabled on both source and destination accounts.   
Tiers can be different, 

### Blob Client library

| Class | Description |
| --- | --- |
| BlobClient | manipulate blob items | 
| BlobClientOptions | configuration options for connecting |
| BlobContainerClient | manipulate blob containers and their blob items |
| BlobServiceClient | manipulate service resources and blob containers |
| BlobUriBuilder | helper for a URI to point to account, container, blob |

namespaces
- Azure.Storage.Blobs: primary classes for working with service, containers and blobs
- Azure.Storage.Blobs.Specialized: specific type operations eg Block Blobs 
- Azure.Storage.Blobs.Models: everything else

### Connecting using SDK
**BlobServiceClient**
```
using Azure.Identity
using Azure.Storage.Blobs

public BlobServiceClient GetBlobServiceClient(string accountName)
{
    DefaultAzureCredentialOptions options = new()
    {
        ExcludeEnvironmentCredential = true,
        ExcludeManagedIdentityCredential = true
    };

    BlobServiceClient client = new (
        new Uri($"https://{accountName}.blob.core.windows.net"),
        new DefaultAzureCredential(options)
    );

    //OR
    //BlobServiceClient client = new BlobServiceClient("connectionstring");

    return client
}

public BlobContainerClient GetBlobContainerClient(BlobServiceClient blobServiceClient, string containerName)
{
    return blobServiceClient.GetBlobContainerClient(containerName)

    //OR
    // BlobContainerClient blobContainerClient = await blobServiceClient.CreateBlobContainerAsync(containerName)
}

public BlobClient GetBlobClient(BlobServiceClient blobServiceClient, string containerName, string blobName){
    return blobServiceClient.GetBlobContainerClient(containerName).GetBlobClient(blobName);
}

public BlobClient Uploadfile(BlobContainerClient blobContainerClient, string fileName, string fullPath){
    BlobClient blobClient = containerClient.GetBlobClient(fileName);

    using (FileStream uploadFileStream = File.OpenRead(localFilePath))
    {
        BlobContentInfo blobContent = await blobClient.UploadAsync(uploadFileStream);
        uploadFileStream.Close();
    }
    
    return blobClient;
}


```
