# Azure CLI
Azure Command Line Interface

## Installation
Install the **az** command via MSI

## Extensions
List the available extensions
```
az extension list-available --output table
```

## Copy the contents of Storage Account to another Storage Account
This copy works across tenants and is super quick
```
az storage copy 
-s https://nacprod9e1857d09194817e.blob.core.windows.net/documents 
-d https://stslasernetbackup.blob.core.windows.net/documents --recursive --source-connection-string "DefaultEndpointsProtocol=https;AccountName=myaccountname;AccountKey=myaccountkey;EndpointSuffix=core.windows.net;" --source-account-name "myaccountname"
```