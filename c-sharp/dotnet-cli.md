# Dot Net Cli

## create an app at the command line
In a directory
```
dotnet console new
dotnet add package Azure.Storage.Blobs
dotnet add package Azure.Identity

mkdir data

```

## Simple project program file 
```
using Azure.Storage.Blobs;
using Azure.Storage.Blobs.Models;
using Azure.Identity;

Console.WriteLine("Azure Blob Storage exercise");

DefaultAzureCredentialOptions options = new()
{
    ExcludeEnvironmentCredential = true,
    ExcludeManagedIdentityCredential = true
};

await ProcessAsync();

Console.WriteLine("\nPress enter to exit");
Console.ReadLine();

async Task ProcessAsync()
{
    await Task.Delay(1);
}
```