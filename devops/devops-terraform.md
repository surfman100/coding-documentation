# Azure and Terraform
You can use either
- AzureRM: stable, mature, full lifecycle, documentation
- AzAPI: thin layer, latest features, fine control  

## Quickstart 

### File Structure
Note: ensure files are in the root directory. An *init* command will not error out if main.tf in a subfolder.

| File | Description | Example |
| --- | --- | --- |
| providers.tf | lists the required providers and modules | |
| variables.tf | defines the variables and their types / defaults | |
| main.tf | creates the resources |  |
| outputs.td | | 
| .terraform.lock.hcl | Lock file created by init | |
| terraform.tfvars | use to set the variables. do not check in ||

### Plan and Apply 
initialise to create the lock file and validate  
```
# the upgrade fetches the most recent that complies with stated minimum versions
terraform init -upgrade
```

create the plan which tells you what will be created  
```
az login --tenant TENANT_ID
terraform plan -out main.tfplan
```

execute the plan  
```
terraform apply main.tfplan
```

cleanup by destroying  
```
terraform plan -destroy -output main.destroy.tfplan
terraform apply main.destroy.tfplan
```  

## handles errors

Import state by using syntax below
```
# syntax 
terraform import [address_of_resource_in_terraform] [id_of_resource_in_azure]

# run 
terraform import azurerm_app_configuration.app-configuration  "/subscriptions/1b6a05e4-7e7f-40c7-9045-854487cd81c2/resourceGroups/rsg_apps_shamrock_test_we/providers/Microsoft.AppConfiguration/configurationStores/appcs-shamrock-dae-84599"

## child objects also need to be imported
terraform import azurerm_key_vault_access_policy.key-vault-access "/subscriptions/1b6a05e4-7e7f-40c7-9045-854487cd81c2/resourceGroups/rsg_apps_shamrock_test_we/providers/Microsoft.KeyVault/vaults/kv-shamrock-dae-84599/objectId/dba920c0-a0de-41eb-b17e-dfdd4887f4f1"
```

This can be useful if your terraform script has a lot of interlinked dependancies, you can't just remove a failing resource.
Process:
- run terraform apply and determine whats failing  
- setup the failing resource manually  
- import the created resource  
- repeat  


## Register Provider in Azure 

```
az provider register --namespace Microsoft.AzureTerraform
```

## Terraform Types
types include:  
- string  
- number  
- bool  
- list  

## Azure Export for Terraform 
Install
```
winget install aztfexport
```

this tool:
- uses **aztft** to identify terraform resource type to azure resoure id 
- runs **terraform import** to import each resource 
- then **tadd** to generate HCL code  


### Gotcha's
Some are: 
- First plan might not work and require script finessing.    
- Moving between machines you might lose state. If this is the case you can import using **import** statement and markup  


```
terraform state list
```