# Infrastructure as Code

- Consistent configurations
- Improved scalability
- Faster deployments
- Better traceability

## Azure Resource Manager
A service used to deploy and manage resources in Azure. 
Receives request, sends it to specific Azure resource provider. 

**Control Plane** requests are sent to [https://management.azure.com/subscriptions...](https://management.azure.com/subscriptions...)

**Data Plane** requests are sent a specific endpoint eg Key Vault 


## ARM Templates
run faster than scripted deployments 
can been broken down into smaller reusabel and nested  

## Deployments
Deploy into a resource group using 

```
az deployment group create --resource-group rg-test --name rollout1 --template-uri https://myresource/azuredeploy.json --paramaters @myparameters.json
```

Parameters may be supplied from a file using the `@{path}` syntax, a JSON string, or as `<KEY=VALUE>` pairs
use
- template-uri
- template-file  

## Providers
Use resource providers to create specific resources 

```
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.1",
  "apiProfile": "",
  "parameters": {},
  "variables": {},
  "functions": [],
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2023-05-01",
      "name": "stsbillstesttesttest",
      "location": "northeurope",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "StorageV2",
      "properties": {
        "supportsHttpsTrafficOnly": true
      }
    }
  ],
  "outputs": {}
}
```

## Bicep 
Simpler syntax, modules, type validation and intellisense 
Looks similar to Terraform!! 
Bicep tooling eg Az Cli, converts (**transpilation**) bicep->json 

```
param location string = resourceGroup().location
param namePrefix string = 'storage'

var storageAccountName = '${namePrefix}${uniqueString(resourceGroup().id)}'
var storageAccountSku = 'Standard_RAGRS'

resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
  name: storageAccountName
  location: location
```

**Advantages**
- Azure-native   
- Azure integration  
- Azure support  
- tracks state  
- use **build** and **decompile** to see ARM Json 

**Disadvantages**
Not for multicloud 