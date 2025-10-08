# Azure CLI

## Installation
Install the **az** command via MSI

## Extensions
List the available extensions, add container app extension 
```
az extension list-available --output table

az extension add --name containerapp --upgrade 
```


## Copy the contents of Storage Account to another Storage Account
This copy works across tenants and is super quick
```
az storage copy 
-s https://nacprod9e1857d09194817e.blob.core.windows.net/documents 
-d https://stslasernetbackup.blob.core.windows.net/documents --recursive --source-connection-string "DefaultEndpointsProtocol=https;AccountName=myaccountname;AccountKey=myaccountkey;EndpointSuffix=core.windows.net;" --source-account-name "myaccountname"
```

## Connecting  
```
az login
az account set --subscription "Production"  

// use a default location!
az configure --defaults location=northeurope
```

## Useful commands
```
// find your UPN
az rest --method GET --url https://graph.microsoft.com/v1.0/me --headers 'Content-Type=application/json' --query userPrincipalName --output tsv

// find storage account resource id
az storage account show -n "storageacct992314" -g rg-bill-test --query id --output tsv

// find a VM's NIC id
az vm show --name "VM1" --resource-group "RG1" --query "networkProile.networkInterfaces[0].id"

// role assignements
az role assignment create --assignee $userPrincipal --role "Storage Blob Data Owner" --scope $resourceId
```

