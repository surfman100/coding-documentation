# Azure Database Migrations

## Migration Services
Steps:
Install
- Azure Data Studio
- Azure SQL Migration Extension
- Create Database Migration Service
Both of the above tools look like Azure Data Factory pipeline monitoring section. 

Speed depends on SKU (P15?). ADF initialisation time can be slow.

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