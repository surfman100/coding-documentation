# Database Security
3 Scopes for securing:
- server
- database
- schema. Each user has a default schema (default is predefined dbo)

**logins** are used to access the database (irrelevant of authentication method)
setup at server instance level and stored in *master* database
**users** are setup in the specific *database* level and have access to that database only. 
are either SQL Auth or Windows/Entra Auth 
**roles** predefined by microsoft and allows creation of custom ones, database or server level.  
**server roles** not available in Azure SQL
create the roles, add the users to role, grant the permissions to role.
**application roles** no users. are activated using password 

| DB Role | definition |
| --- | --- |
| public | default role, no permissions |
| db_accessadmin | create users |
| db_datareader | read every table/view in db |
| db_datawriter | insert/update/delete every table/view in db |
| db_deny* | denies the right when granted some other way |
| db_securityadmin | grant access to other user, no data but can grant themselves |
| db_owner | any action |

a view additional roles exist for Azure SQL Database (virtual master)

| Fixed Server Role | definition
| --- | --- |
| sysadmin | any action |
| serveradmin | server config |
| dbcreator | create, restore, alter, drop | 
| public | default for each login |

**permissions**
basic ones: select, insert, update, delete on *tables and views*
you can: grant, revoke, deny
others: control, references, take ownership, view change tracking, view definition
procs and functions: alter, control, execute, view change tracking, view definition

use Execute As to switch user being used (not Azure SQL)

## Network Filtering
Two Types: 
- Server Firewall rules: control via portal
- Database Firewall rules: control via TSQL only

Database checks for database level rules first, if none checks Server level

## Microsoft Defender for SQL
providers
- SQL Vulnerability Assessment
- Advanced Threat Protection: detect and respond to unusual access attempts, SQL injections attacks. Think alerts / integratioin with Defender for Cloud

SQL Auditing Logs -> Sentinel Log Analytics Workspace

## Dynamic Data Masking
Inbuilt masking functions. 
Only users with UNMASK permission can see the value. 