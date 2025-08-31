
## SQL Types
| Type | Tier | Pros | Features | Description |
| ---- | ---- | ---- | ---- | ---- |
| Azure SQL | PAAS | low administration, migration to cloud ease | more backup features, automatic |
| Managed SQL | PAAS | | cross DB queries, CLR, System DB access, SQL Agent | shares sames code base as Azure SQL. Backup to blob |
| SQL on VM | IAAS | Bring in out of Cloud servers using ARC |

- Azure SQL Purchasing Model
  - **vCore-based**. Service Tiers:
      - GP. (1 replica, no read scale replicas)
      - Business Critical (several secondary replicas). *HA*
      - Hyperscale (allows several secondary replicas)
    - Hyperscale new Tech, once converted you can't go back. High Perf, instant backup / scaling. moves beyoud standard limiations. Cost marginally more than Azure SQL db.
  - **DTU-based**. Service Tiers:
      - Basic
      - Standard
      - Premium (managed db does not support this option) *HA*
- Compute Tier
  - Provisioned
  - Serverless (good for test and development: auto scale, auto pause)


  - Features
  - Elastic Query
  - Predict for Machine Learning
  - Table paritioning -> when large rowcount impacts queries. Use of partition functions
  - Data Compression -> compress indexes, more data on the 8kb page, less I/O
  - Elastic Pool -> good option for multitenant databases. Scaling happens with very little interruption

- SQL on VM
  - types of disk
  - IaaS agent:
    - registers VM SQL on Azure (SQL Virtual Machines)
    - automates patching, backup etc
 
