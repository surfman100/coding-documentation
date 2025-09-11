# Azure and Entra Roles

- Entra Roles: GA, AppA, AppD, BillingA  
- Azure roles: Owner, Contrib., Reader, UserAccessA

## Azure Roles

**main roles**
| role | permissions |
| --- | --- |
| Owner | full access, can assign RBAC roles |
| Contributor | full access |
| Reader | view resources | 
| RBAC Admin | manage user access, can assign owner/RBAC role |
| User Access Admin | manage user access, can assign owner/RBAC role |

other resource specific roles e.g. VM Contributor

**privledged administrator roles**
roles that grant admin access
have actions like:   
- */delete */write


## Entra Roles (Roles and administrators in AzPortal)
Manage Entra resources in a directory e.g.
- create/edit users, devices, MS Services - exchange
- assign admin roles to others
- manage user licenses 
- manage domains
- manage app registrations

** important roles **
| role | permissions |
| --- | --- |
| GA | all Entra admin features, assign admin roles, reset passwords for all |
| UA | manage users/groups, tickets/health, reset passwords for users |
| BillingA | purchases, manage subs, tickets/health |

Scope: tentant, admin unit, object
Azure & Entra roles are not related  
e.g. GA in entra does nothing for you in Azure  

## Use Entra GA to regain Azure control
However GA & UA allow you to regain access to Azure  
Log into portal as GA, navigate to properties blade of Entra Id resource. Enable!  

## Role Definitions
A role definition includes:
- id, name, isCustomFlag, created date
- actions (e.g. *), notActions (e.g. "Microsoft.Authorization/*/Delete"), dataActions, dataNotActions  

## Plane Access differences
**Control plane access** is not inherited to **Data plane access**! Hence cannot see Key Vault Secrets. 
use RBAC instead of access policies (older tech)  
clicking on KeyVault secrets page is a **data plane action** and so it is checked against the dataAction & dataNoAction properties.  

## Deny assignments
attaches deny actions

## Eligible and Time-bound
Need to have Entra PIM

## Best Practices  
- Use RBAC instead of older admin roles or resource specific functionality
- groups not users
- Use PIM to time-bound access
- limit subscription owners