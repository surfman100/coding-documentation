# Azure Resources

## Resource provider
Is a set of REST Operations that support a particular service e.g. Microsoft.KeyVault

Limit what can be provided/used on a subscription. ie do not add ability provision VM's until they are actually needed.
```"
Get-AzResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState | Where-Object RegistrationState -eq  "Registered"
```

See what operations are supported for a ResourceType
```
(Get-AzResourceProvider -ProviderNamespace Microsoft.Sql).ResourceTypes.ResourceTypeName
```
