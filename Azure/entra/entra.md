# Entra 

## Self Service Password Reset SSPR 
Reset your password via browser/portal 
Requires P1 license 

Entra Connect - synch users,groups,passwords between on prem AD and Entra ID. 

## Roles

| | Entra roles | Azure roles | 
| --- | --- | --- |
| Manages acces to | entra (& office365)| azure resources |
| custom roles | yes | yes |
| scope | tenant or administrative unit | management group, subscription, resource group, resource |
| accessed via | azure portal, M365 admin center, graph, powershell | Azure portal, Azure CLI, Azure Powershell, ARM templates, Rest API |

**GA** in entra gives you **User Access Administrator** in Azure on all subs.  

**Administrative Units** contain users, groups add/or devices 
Its a way of limiting GA actions to specific U, G, D's
