# Azure Storage

| Storage Type | Notes |
| --- | --- |
| Blob Storage | Useful for images/files directly to browser, video/audio streaming, now access blobs using NFS |
| File Storage | Network file share, SMB & NFS |
| Queue Storage | up to 64kb messages |
| Table Storage | NoSQL, Key/Attribute. Cosmos is newer |

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

## Security 
public: can restrict to VNets (same) or IPs  
private endpoints: stop traffic going over internet 



## Blob Client library

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

## Connecting using SDK
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
