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
- differential 12 hours
- transaction log 5-10mins
Use retention policies to setup how long to retain backups
Delete Server -> all backups deleted
Delete DB -> can be restored
PIR default is 7days, can be extended to 35days
No Managed backup -> SQL restore