# SQL Server System Tables

## Tables / Views

| table / area | description | when to use |
| --- | --- | --- |
| Query Store | tracks query usage/stats | checking CPU usage |
| sys.dm_exec_requests | info on each request/session | checking CPU usage |
| sys.dm_exec_query_stats | aggregate performance stats for cached plans | checking CPU usage |
| sys.dm_exec_procedure_stats | ditto, for sp's | checking CPU usage | 
| sys.dm_db_resource_stats | db resource snapshot every 15 seconds | db system health
| sys.server_resource_stats | server resource snapshot every 15 seconds | server system health
| sys.dm_exec_query_plan() | capture actual plan for a query | | 
| sys.dm_db_index_physical_stats | check index fragmentation | |
| sys.dm_db_column_store_row_group_physical_stats | check index fragmentation | |


## Waits
| wait / wait view | description | when to use |
| --- | --- | --- |
| SOS_SCHEDULE_YIELD | high volumes of these suggest CPU stress  |  |
| sys.dm_os_wait_stats | info on all waits | Checking waiting |
| sys.dm_os_wait_tasks | tasks that are waiting on some resource | Checking waiting | 
| *_GOVERNOR | Azure SQL Log Governance effects | |

## Areas