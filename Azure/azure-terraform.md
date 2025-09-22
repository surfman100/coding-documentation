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