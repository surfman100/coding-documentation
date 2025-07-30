# Azure Resources

## Resource providers
Limit what can be provided/used on a subscription. ie do not add ability provision VM's until they are actually needed.
```"
Get-AzResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState | Where-Object RegistrationState -eq  "Registered"
```
