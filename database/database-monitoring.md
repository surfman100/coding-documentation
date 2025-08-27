# Monitoring

| What | how |
| --- | --- | 
| Region | Azure status & Azure Health |
| Instance, Server, DB | use cli/powershell to ping dbs. Use PerfMon or DMV's |
| backups | view expected creation of new backups in Azure activity log |
| replica status | view using DMV sys.dm_database_replica_status |

Note difference between umbrella **azure monitor** and the visual **azure metrics**
Azure monitor will not show you SQL Server performance details

## Auditing
Configure: Under security, auditing
Send the data to Sentinel LogAnalytics Workspace

## Alerts 
types
| Type | Description
| --- | --- |
| Metric | resource metrics at regular intervals |
| Log Search | log results at set frequency | 
| Activity | Log events eg Service / Health | 
| Smart | Web App from App Insights | 
| Promethus | |

Dynamic alerts: use to report significant changes   

stateless (fire each time) v stateful (fire once and no more until fixed)