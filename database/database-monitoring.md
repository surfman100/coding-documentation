# Monitoring

| What | how |
| --- | --- | 
| Region | Azure status & Azure Health |
| Instance, Server, DB | use cli/powershell to ping dbs. Use PerfMon or DMV's |
| backups | view expected creation of new backups in Azure activity log |
| replica status | view using DMV sys.dm_database_replica_status |

Note difference between umbrella **azure monitor** and the visual **azure metrics**
Azure monitor will not show you SQL Server performance details

| Solution | Description | Best For | 
| --- | --- | --- | 
| Metrics and Alerts | DB, Elastic Pool resource consumption and health | |
| Query Performance Insight |  | |
| Monitor using DMVs |  | some views are for current performance |
| Monitor using Query Store | 7 views | Best for viewing issues with historical performance |
| Database Watcher | Dashboards, single glass | |
| Extended Events | admin, operational, analytic, debug | Use instead of Profiler or Trace to debug |

## Database Watcher
To collect data, use either
- Azure Data Explorer (real time analytics)
- Real-Time Analtics in Fabric

## Metrics
Available on overview page. Clicking brings you to *metric explorer* 
Stored in *Azure Monitor metrics database*
This is different from Log Analystics type data which can be viewed using Log Analytics

## Auditing
Applies to SQL Server only.
Configure: Under security, auditing
Send the data to Sentinel LogAnalytics Workspace
Build on Extended Events
- Audit object
  - Server Specification: audit action groups, 1 per audit
  - Database Specification: 
- Target: Audit results are sent here

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

## Live Query Statistics
View the query as it executes 