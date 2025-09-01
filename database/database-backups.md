# Database Backups
types:
- Full: all the pages backed up
- Differential: all pages since last full backup
- Transaction Log: clears the log as part of the backup

to use differential/logs the db must be restored *with norecovery* or *with standby*
note use of recovery modes

## IaaS Backups
use Azure Backup to backup the VM. Is SQL app aware.
backup locations include disks or to url (blob storage):
- use FROM/TO url
Automatic backups are available as part of the SQL aware VM setup
Need to create credential (SAS) in sys.credentials if backing up from URL

## PaaS Backups
Automatically provided. 
- full weekly
- differential 12 hours  (different since full. only restore lastest)
- transaction log 5-10mins
Use retention policies to setup how long to retain backups
Delete Server -> all backups deleted
Delete DB -> can be restored
PIR default is 7days, can be extended to 35days
No Managed backup -> SQL restore

## Maintenance Plans
Is an Integration Services package run by SQL Server Agent job.

## Recovery Models & Restore
Data written to Transaction Log
Periodically this is written to Disk
Recovery decides to use or disregard this data to bring to consistency

| Option | Description |
| --- | --- |
| Compression |  | 
| Encryption |  | 
| noinit | appends to existing media set  | 
| format | format media | 
| stats | displays messsage of % complete |
| copy_only | independent of regular schedule (ie special purpose) | 
| file_snapshot | backups in azure storage |

Recovery is the process for DB to start in clean state
| Type | Description | Pros | Cons |
| --- | --- | --- | --- |
| Simple | | reduced admin overhead | Lose all since last backup, no PITR |
| Full | | minimize work-loss exposure | Requires log backups
| Bulk Logged | like above + high perf bulk copy operations| minimize work-loss exposure | 

Roll Forward: after first restore, apply each transaction log backup to roll forward the transactions
Roll Back: Transactions that weren't complete on backup

| Option | Description |
| --- | --- |
| DB | whole db is restored and recovered, offline | 
| Data File | file(s). The filegroup is offline |
| Data Page | restore individual pages |

Restore to another Server
| Type | Description |
| --- | --- |
| Long Term Backup |  | 
| [Geo-Restore](https://learn.microsoft.com/en-us/azure/azure-sql/database/recovery-using-backups?view=azuresql&tabs=azure-portal#geo-restore) | requires GRS!, need to create DB first. Create DB from Geo-Restore backup using wizard |
| Database Copy |  |
| [Active Geo-Replication](Active Geo-Replication) | Think Replica's.  |


**Recovery State**
Restore
| With Option | Description |
| --- | --- |
| Recovery | DB is ready to go |
| NoRecovery | DB in restoring state, need to use first option after |
| Standby | DB in standby state, uses standby file to allow undoing of restore |