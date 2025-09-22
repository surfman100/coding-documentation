# Azure CLI
Basic setup  
```
az login
az account set --subscription "Production"  

az vm show --name "VM1" --resource-group "RG1" --query "networkProile.networkInterfaces[0].id"
```