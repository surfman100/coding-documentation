# Database Security
3 Scopes for securing:
- server
- database
- schema. Each user has a default schema (default is predefined dbo)

**logins** are used to access the database (irrelevant of authentication method)
setup at server instance level and stored in *master* database. can be disabled.
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

create entra users at the database level directly
```
create user [bti@nac.dk] from external provider
```

## Network Filtering
Two Types: 
- Server Firewall rules: control via portal
- Database Firewall rules: control via TSQL only *sp_set_database_firewall_rule*

Database checks for database level rules first, if none checks Server level

## Microsoft Defender for SQL
providers
- SQL Vulnerability Assessment
- Advanced Threat Protection: detect and respond to unusual access attempts, SQL injections attacks. Think alerts / integratioin with Defender for Cloud

SQL Auditing Logs -> Sentinel Log Analytics Workspace

## Dynamic Data Masking
Inbuilt masking functions. 
Only users with UNMASK permission can see the value. 
Does not alter the data, just the viewing of it
```
alter table [mytable] alter column [mycol] add masked with (function = 'partial(0,"XXXX-XXXX-XXXX-",4)')
```

## Transparent Data Encryption (TDE)
Encrypts at page level, decrypted on read to memory.
hence DBA's might be able to see the decrypted data. 
prevents backup restore to another computer
- create master key encryption, certificate, database encryption key, alter database 

## Always Encrypted
based on master encryption key and column encryption key (each col encrypted using different key)
use SSMS. Random (use on low variance data) or deterministic
Client apps:
- need access to key store
- Always encrypted driver. 
- encrypts data in writes.
- in connection string use "Column Encryption Setting=enabled"
Secure Enclaves build on this.

## Transport Layer Security (TLS)
Protocol layer.
Use SQL Server Configuration Manager for certificates and configure server to use TLS

## Sensitivity Classifications
Add classifications for columns
- information type
- sensitivity label

## Row Level security (RLS)
no encryption. user can't perform actions based on group membership
- filter predicates: select/update/delete rows (like a where clause)
- block predicates: after s/i/u/d -> prevents action
you see your own rows

1. create filter predicate table function (use seperate schema)
2. grant select on function to users
3. create security policy that joins function to table

## Ledger
tamper evidence
each transaction is hashed and all transactions linked 
- append only ledger tables: block all updates/deletes at API level 
enabled on db creation only

## Purview
Add data connections, initiate scans for configured rule types.
scans to be triggered on a schedule

## Encryption
SQL Server key types:
- symmetric: same password to encrypt/descrypt -> created on server server creation
- asymmetric: public/private key -> created by OS

Used:
- service master key: autogen. encrypts the DMK's. Used by Windows/Service.
- database master key: symmetric. protects the DB's certs & asym keys.

Certificate binds the Key to identity of service/device/person

Encrypt a Column:
- Create DB Master Key
- Create Certificate
- Create Symmetric Key with Certificate
- Open Symmetric Key
- Update data using function *EncryptByKey*
Test using 
- Open Symmetric Key
- select data using function *DecryptByKey*

Always On Encryption:
- encryption keys are never exposed to the Database Engine
- Uses Column Encryption keys and Column master keys
- Column master key stored in Azure Key Vault
- Determinisitc: same data in -> same encrypted value. allows additional operations
- Randomized: more secure