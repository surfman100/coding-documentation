# Database Automation

## Automation Types
| Type | Which | Pros | How | Cons | 
| ---- | ---- | --- | --- | --- |
| SQL Agent | SQL Server and Managed SQL Server | robust scheduling | |  |
| Elastic Jobs | All | Run TSQL across DBs, load data |  | Limited? | requires its own DB. use job_executions to query |
| Azure Automation | Fully featured. Periodic jobs are low cost. | Automation Account, Functions, Logic Apps and more! | There's a lot to this area |
| Azure Policy | enforcement of standards | | |

## SQL Agent 
Create **Maintenance Plans** via SSMS Wizard.   
Scheduling regular maintenance - indexes, statistics  
*Notifications* - Enable Agent email profile, sent to operators(define) - Job success/failure
*Alerts* - Select Metric, counter
types
- SQL Server event: specific error occurs
- SQL Server performance condition: metrics based

## Elastic Jobs
Similar to Agent but only TSQL. 
Create new database on a server
Create User Managed Identity
On target databases, add the logon/user for the UMI
Create a job group
Add targets to the group
Create a job
Run the job


