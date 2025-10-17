# Graph 
Install using Powershell
```
# include * to see all
Get-Module "Microsoft.Graph.*"
```

if install/conflict issues
- check if modules are in disk or in onecloud
- remove the modules from session using ```Remove-Module "Microsoft.Graph.*"```
- remove the modules from disk using ```Uninstall-Module "Microsoft.Graph.*"```
- delete the physical files in Documents/Powershell/Modules

## Connect using powershell 
```
# you need to PIM up to User Administrator first!
Connect-MgGraph -scopes "User.Read.All" -tenantid "<tenantid>"

Get-MgUser -UserId "bti@[domain]"
```