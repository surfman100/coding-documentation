# Azure Policy 
Stike a balance! Control & Stability v Speed & Results.   
Compromise required...be careful before introducing policy!  

Policy operates in the **control plane**.   
Policy is Integrated with Resource Manager for control of these operations.  

For data operations, which do not go through RM, services can implement Azure Policy extension to integrate.  
e.g. with these providers: 
- Microsoft.Kubernetes.Data 
- Microsoft.KeyVault.Data 
- Microsoft.DataFactory.Data 

![Policy is Integrated with Resource Manager](/Azure/azure-management/azure-policy-and-resource-manager.png)

Paths
- **GreeenField**: Policy in place, Policy kicks in *after* RBAC check 
- **BrownField**: Resource in place, compliance check every 24 hours -> non compliant list.  

## Terms 

| Term | Defintion |
| --- | --- |
| Definitions | define policy and effect |
| Initiative | groups policies to simplify assignments | 
| Assignments | assigns policies/initiatives to a scope of resources | 
| Exemptions | exemption a resource for a policy or initiative |
| Attestations | Set the compliance state of a resource for manual policy |
| Remediations | tasks to address |

is a section under the Policy blade. 