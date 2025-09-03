# Disaster Recovery
thinking of: 
- Availibility capabiltiies  
- Backup and Restore strategy  


## RTO & RPO
**Recovery Time Objective** - max time to bring resources online
**Recovery Point Objective** - max amout of data loss
if 15mins RTO, its ok to restore current outage from backup 15mins ago
business decides. define at:
- component level and overall architecture level 
- different for HA and DR 

**High Availability events** - localised, easier to recover from
**Disaster Recovery event** - regional, take hours or longer

PAAS - HADR options built in

## SQL Server HADR
**Cluster Mechanism**
built on
- Windows Server Failover Cluster (WSFC)
- Pacemaker (Linux)
Instance level protection (logins, sql agents etc)
Concepts:
- Witness Resource: disk/fileshare for coordination
- AD & DNS required if using FCI
- enable failover clustering feature on windows node
- Validation process via FCI manager or powershell, checks nodes suitable/healthy
```
New-Cluster -Name MyWSFC -Node Node1,Node2,NodeN -StaticAddress w.y.x.z
```

*Always On* refers to FCI & AG (so not Azure SQL!)

**Failover Cluster Instances** configured on installation, can't convert later. 
Is an instance of SQL Server installed on all nodes. Appears as a single instance. 
On prem or in Azure. In Azure, internal load balancer is required.
On failover, full stop/start required, app will need to reconnect once node up after recovery process.
DB on shared storage, requires AD DS & DNS
Bit old skool -> handle network card/disk failures, these issue rarely happen in cloud abstraction
Failover Cluster Manager is available under server tools

**Availability Groups**
SQL Server provides AGs by using WSFC services and capabilities
DB level protection. 
- standard: 1 db, 1 w/r & 1 r replica. 
- Enterprise: multipele dbs, 1 w/r & 8 r replicas.
Quicker failover times and no shared storage (simpler to implement), increased storage costs
Additional setup for instance level logins, agents etc
Enabled on the SQL server properties page. Use this of TSQL/Powershell.
v2022 on, can include instance level objects, properties
Active Secondary replicas: backup off the replica, read only access to replicas, 
To bring up secondary replica use **restore with norecovery** to leave the DB non-operational


| Type | Description | Specifics | 
| --- | --- | --- |
| Basic | For Standard edition | Single replica, no read access, no backups off secondary |
| Contained | Additional instance details | include relevant portions of master & msdb, create users etc at AG level | 
| Distributed | Cross region | A AG that contains 2+ AG groups |

| Availability Mode | Description | Pros | Cons | Failover |
| --- | --- | --- | --- |
| asynchronous-commit | primary commits transaction without waiting for secondary ack. | low latency | possible data loss | only forced |
| synchronous-commit | wait for secondary ack. | some latency | no data loss | planned or automatic |
| configuration only | ag's not ont WSFC | 

Sync process: incoming log records (hardens the log), replies ack, status = SYNCHRONIZED

**distributed availability groups**
useful as an easy means of migrating server to new version

**Log shipping**
DB level protection. No automatic failover, switching server names required.
Process:
- Full backup
- Restore it in a loading state (**standby** or **norecovery**) ie warm standby
- auto backs up primary db transaction log and restores to standbys 

## Azure HADR for IaaS
**availability sets**
seperates VMs into 
- Fault Domains: groups of servers with same powersource, network (FD0,FD1,FD2)
- Update Domains: groups of machines that can be be rebooted simultaneously (server updates)
doesn't protect against OS/RDBMs crashes
create an AS for each tier in multi tier app

**availability zone**
alternative to previous. no gaurentee that AV1 is the same for two different subs

**azure site recovery**
crude, has no knowledge of whats on VM (lost SQL data.)
extension installed on vm
adjust the *app consistent snapshot frequency* from 60mins to desired. might cause issues with SQL.

## Azure HADR for PaaS
Already has 99.99 availability built in. eg Advanced Database Recovery
Applications should have retry logic as transient issues can occur. 
Capabilities like OFFLINE, EMERGENCY state not available/needed.  

**active geo-replication (replicas)**.
replciates data to read only secondary (geo-replica or geo-secondary) in same or diff region
all databases must be same service tier, configured per database
Cross subscription geo-replica via programmatically
Is a BCP solution
up to 4 readable replicas in different regions
RPO - a few seconds
Readable Secondary replicas *in the same region* - create on a different server
- Good for scale out
- not for DR **if you use same region** (but allows you to recovery)
- Good for HA (data center goes down) **if you use zone redundancy**

**zone redundancy** 
enable this to ensure DB uses availability zones in your region to replicate data across locations

**auto failover**
auto failover or customer initiated. 
abstraction on top of geo-replication! 

| Features | Geo-Replication | Failover Groups |
| --- | --- | --- |
| Automatic Failover | No | Yes |
| Fail over multiple db's simultaneously | No | Yes |
| User must update connection string after failover | Yes | No |
| SQL Managed Instance support | No | Yes |
| Can be in same region | Yes | No |
| Multiple replicas | Yes | No |
| supports read scale | Yes | No |

