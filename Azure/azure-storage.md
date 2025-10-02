# Azure Storage


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
    BlobServiceClient client = new (
        new Uri($"https://{accountName}.blob.core.windows.net"),
        new DefaultAzureCredential()
    );

    //OR
    //BlobServiceClient client = new BlobServiceClient("connectionstring");

    return client
}

public BlobContainerClient GetBlobContainerClient(BlobServiceClient blobServiceClient, string containerName)
{
    return blobServiceClient.GetBlobContainerClient(containerName)
}

public BlobClient GetBlobClient(BlobServiceClient blobServiceClient, string containerName, string blobName){
    return blobServiceClient.GetBlobContainerClient(containerName).GetBlobClient(blobName);
}
```
