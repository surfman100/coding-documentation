# Database Automation

## Elastic Jobs
Create new database on a server
Create User Managed Identity
On target databases, add the logon/user for the UMI
Create a job group
Add targets to the group
Create a job
Run the job

## Polybase
You can connect to Oracle DB etc without installing oracle software. Not AzureSQL

## Automation

| Type | Pros | How | Cons | 
| ---- | ---- | --- | --- |
| SQL Agent | robust scheduling | | only SQL Server and Managed SQL Server |
| Elastic Jobs | Run TSQL across DBs |  | Limited? | requires its own DB. use job_executions to query |
| Azure Automation | Fully featured. Periodic jobs are low cost. | Functions, Logic Apps and more! | There's a lot to this area |
| Azure Policy | enforcement of standards | | |

