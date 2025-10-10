# Powershell
Hints & tips on using Powershell. 

## Pros
Unlike bash, powershell returns Objects
Output as Object. Can be manipulated more than if just text based 
Has **cmdlets** in

## Latest versions
Use
- Powershell 7+. check version using ```$PSVersionTable.PSVersion```
- Az module instead of deprecated AzureRM
```
Get-Modules -list     // list modules
SetExecutionPolicy -ExcutionPolicy RemoteSigned -Scope CurrentUser
Install-Module -Name Az -Repository PSGallery -Force
```

## General
use the ` character to span across lines  
remember boolean is $true/$false and not 'true'/'false' !  
arrays @()  
objects [type]@{}  

```
Get-Module  
Get-Command -module "ModuleName" *searchstring*  

# output to table
Get-AzResourceGroup | Format-Table -Property ResourceGroupName  

# simple loop
foreach ($id in Get-CGIPUserPoolList -Select 'UserPools.Id')  
{   
    Write-Output ('Deleting existing pool ' + $id)  
    Remove-CGIPUserPool -UserPoolId $id -Force  
}   
```

## Help
- use *help* as a shortcut for Get-Help  
- install latest update-help
- pipe to *Get-Member* to end of command to get the output members

## Startup location
create file profile.ps1 in **Documents\WindowsPowershell**. \
Add the line: \
`
Set-Locations C:\
`

## AWS scripting
Install-Module -name AWS.Tools.CognitoIdentityProvider

Get-AWSCredential -ListProfileDetail  
Get-DefaultAWSRegion  
Set-AWSCredential -AccessKey [accessKey] -SecretKey [secretKey] default  
Set-DefaultAWSRegion us-east-1  

## Azure scripting
Install-Module -name Az  

## IIS recipes
Excellent backgrounder here:  
https://octopus.com/blog/iis-powershell

## Syntax
[Automatic Variables](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_automatic_variables?view=powershell-7.5) store state information. Common ones:
- **$/?** last command successful/not  
- **$Error** error array  
- **$Home** users home directory  
- **$pwd** current directory  
- **$input** inputs to a function, 

```
$variable = variable
Write-host $variable
```

```
# script to read parameters etc
param(
    [Parameter(Mandatory=$true)][string]$resourceGroupName,
    [Parameter][string]$appServiceName,
)

#params in string
Write-Host "The paramater is $resourceGroupName , ok?"

#function with parameters
function Test-Param {
	param([string]$Name, [string]$Value)
	if ([string]::IsNullOrWhiteSpace($Value)) {
		throw "Parameter '$Name' is required and cannot be empty."
	}
}

#pass variables to a function 
"one", "two" | myFunction
```

## Useful commands  
Include:  
- **$SetLocation** changes current directory  

