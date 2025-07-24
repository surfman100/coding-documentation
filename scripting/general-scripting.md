# Scripting tips

## Powershell v Azure CLI

| Command | Azure CLI |	Azure PowerShell |
| --- | --- | --- | 
| Sign in with Web Browser	| az login |	Connect-AzAccount |
| Get available subscriptions	| az account list	| Get-AzSubscription |
| Set Subscription	| az account set –subscription |	Set-AzContext -Subscription |
| List all virtual machines |	az vm list |	Get-AzVM |
| Create a new SQL server |	az sql server create |	New-AzSqlServer |