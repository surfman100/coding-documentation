# Container Development

why?
- speed & flexibility in sharing and development  
- simplified testing 
- streamlined deployment 
- higher workload density 

## Differences to VM's  
less secure, less resources needed. 

## Enabling containerisation
On windows, necessary BIOS settings are ready. Use *Features* to turn on "Virtual Machine Platform".    
[podman](https://github.com/containers/podman/releases) is a lightweight alternative to dockers desktop.  
use  *windows terminal* for UI  
install the *windows subsystem for linux*  [WSL](https://learn.microsoft.com/en-us/windows/wsl/)  

## Azure Container Instances (ACI) 
Don't have to worry about VM's (container will run in a container host VM)
Image contains:
- code  
- runtime  
- system tools  
- system libraries  
- settings   
Fast startup. Persist to Azure File shares. 
Set the DNS name in creation process. 

**Container App Environment** environment for groups of ACA's.  
**Container Group** collection on containers that get scheduled on the same host machine. (**pod** on kubernetes)  
Share life cycles, resources, network, storage volumes.  
Can share IP Address  
E.g. contains ACA for app and ACA for DB  
reasons to not share Environment:
- never share compute resources  
- Dapr apps can't communicate using Dapr API  

```
az containerapp env create --name --resource-group --location 
```
![Container Apps](/containers/azure-container-apps-containers.png)


## Namespaces 
require
- Microsoft.App
- Microsoft.OperationalInsights 


## Azure Container Apps (ACA)
Powered by kubernetes (do direct access to K api). Simple to get going on. **AKS** more advanced/complex. 
Designed for microservices and serverless. 
Event driven app architecture, scale based on http traffic, CPU, mem, events. 

```
az containerapp create --name --resource-group --environment --image --target-port -- ingress 
```
ingress external = available for public requests 

## Azure Container Registry (ACR) 
Based on Docker Registry 2.0 
In addition to images, stored related content (Helms charts) & OCI images 
**ACR Tasks** to automate e.g. as code checked in (inner-loop development), docker build/push, 

| Service Tier | Description |
| --- | --- | 
| Basic | storage and image throughput limited | 
| Standard | ideal for production |
| Premium | geo-replication , private link |

Logon using this command. You need to have docker desktop running!!
```
az acr login --name [nameofregistry]
```

## Containers 
App can have multiple containers but this is advanced scenario 

## Authentication 
Middlesware runs as a sidecar container on each replica  
- without SDK: Delegation for browser apps. 
- with SDK: browless apps that submit auth token. 

## Revisions 
Revision is an immutable snapshot of container app version. 
Use 
Naming is: [containerappname]--[revisionsuffix] 

```
az containerapp revision list --name --resource-group
``` 

## Secrets 
Scoped to Application (outside of revisions) 
KV not supported  