# Azure Automation

## Automation
Create runbooks to run powershell or python
- There is a graphical editor

## Logical Apps
- Connectors
- LoCode, NoCode
- eg trigger when a row is created in a table

## Automated Deployments
ARM Templates
- JSON

Bicep
- more terse code

Both execute using powershell. Azure CLI doesn't support Bicep
```
New-AzResourceGroup -Name exampleRG -Location eastus
New-AzResourceGroupDeployment -ResourceGroupName exampleRG -TemplateFile ./main.bicep -administratorLogin "<admin-login>"
```