# Azure Database Migrations

## Migration Services
Steps:
Install
- Azure Data Studio
- Azure SQL Migration Extension
- Create Database Migration Service
Both of the above tools look like Azure Data Factory pipeline monitoring section. 

Speed depends on SKU (P15?). ADF initialisation time can be slow.

Azure Migrate creates only VMs/Nics/Disks. Other Associated resources should be created.
Rights
- Local: Remote management users, hyper-v administrators, performance monitor users
- Azure: Virtual Machine Contributor, Owner/Contributor for app registrations

On prem servers need access to a handful of azure/ms/vs domains

Agent is downloaded to a new seperate VM on your VM area.
Azure Site Recovery is the service used in background and it installs its agent to the source VMs and also installs the provider. 
Process:
- snapshot of VM is taken and pushed to storage account
- New Azure VM created from this snapshot
- Snapshort delete 
- Changes are stored in log files.
- Delta replication begins 



## Migrate at Scale 
Use powershell or CLI

## Data Migration Assistant
One stop standalone experience application. Offline only.

## BacPac
BacPac is metadata and data.
Use SqlPackage
Must be a new/clean target database.

## Transactional Replication (Publisher / Subscriber)
Great for online migrations. There is a fair amount of setup required! 
Can only use SQL Server authentication
Need to create a distributor database, distributor pulishers and agents. 
Monitor Snapshot & Log Reader Agents for SQL Server, not Azure SQL. (Agents run on this too) 

| Role	| Definition | 
| --- | --- | 
| Publisher | A database instance that hosts the data to be replicated (source). |
| Subscriber | Receives the data being replicated by the Publisher (target). |
| Distributor | Collects changes in the articles from a Publisher and distributes them to the Subscribers. |
| Article | A database object; for example, a table that's included in the Publication. |
| Publication | A collection of one or more articles from the database being replicated. |
| Subscription | A request from a Subscriber for a Publication. |