# Database Security


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