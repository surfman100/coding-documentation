# DP300 Exam - SQL 

| Type | Tier | Pros | Features | Description |
| ---- | ---- | ---- | ---- | ---- |
| Azure SQL | PAAS | low administration, migration to cloud ease | more backup features, automatic |
| Managed SQL | PAAS | | cross DB queries, CLR, System DB access, SQL Agent | shares sames code base as Azure SQL. Backup to blob |
| SQL on VM | IAAS | Bring in out of Cloud servers using ARC |



- Azure SQL Purchasing Model
  - vCore-based (GP, Business Critical, Hyperscale)
    - Hyperscale new Tech, once converted you can't go back. High Perf, instant backup / scaling. moves beyoud standard limiations. Cost marginally more than Azure SQL db.
  - DTU-based (Basic, Standard, Premium) (managed db does not support this option)
- Tier
  - Provisioned
  - Serverless (good for test and development: auto scale, auto pause)

- Features
  - Elastic Query
  - Predict for Machine Learning
  - Table paritioning -> when large rowcount impacts queries. Use of partition functions
  - Data Compression -> compress indexes, more data on the 8kb page, less I/O
  - Elastic Pool -> good option for multitenant databases

- SQL on VM
  - types of disk
  - IaaS agent automates patching, backup etc
 
## Distaster Recovery
SQL Server Failover Cluster Instance 
Windows Server Failover Cluster
Azure Site Recovery is a low-cost solution that will perform block level replication of your Azure virtual machine -> good for web servers, not OLTP
Availability Sets (HA)
Always On availability groups (HA & DR) -> automatic failover of DB but not instance
