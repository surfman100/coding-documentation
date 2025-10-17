# Azure File Storage

4TiB size limit on one file. 
true directory objects 


## Access using
**SMB** Server Message Block  
**NFS** Network File System (linux file system)  
Rest API 
Client libraries

## Tiers
Are:
- premium : SSD, LRS/ZRS
- stanadard: HHD, LRS->GZRS 

## Auth
Are:
- Access Key
- SAS 
- Identity based over SMB (port 445)  

## Backup
- snapshots at file share level 
- soft delete at storage account level 