# SQL Design and Optimisation

## Query Plans
1. Query is parsed -> parse tree
2. Algebrizer validations -> query processor tree
3. Checks current query using query_hash for cached execution plan in plan cache
4. Use cost-based optimizer -> query execution plan
5. Excution

memory grant = memory required for joining,sorting etc

show plan
- Expected: set showplan_all on
- Actual: set statistics profile on

## Dynamic Management Views/Functions
all prefixed **sys.dm_**

e.g. 
sys.dm_db_tuning_recommendations
sys.dm_db_missing_index_details

## Query Store
available under DB->QueryStore->7 views
- Plan store: Stores estimated execution plan information.
- Runtime stats store: Stores execution statistics information.
- Wait stats store: Persists wait statistics information.

Query store persists multiple execution plans


The views include

| View | Description | Use / Addressing issues |
| --- | --- | --- |
| Regresssed Queries | Performance degradation over time | Force a query to use a plan |
| Overall resource consumption | Top 25 resource consumer queries for metric | Use when system resource contention becomes an issue | |
| Top Resource Consuming Queries | Top 25 most impactful queries based on filter/timeframe | Might show some big impact queries only run once |
| Queries With Forced Plans | | Relevant if a forced plan no longer performs as expected. Buttons for unforcing plan |
| Queries With High Variation | | Use to tune unpredicatble queries | 
| Query Wait Statistics | | helps identify queries that are affecting user experience across applications. |
| Tracking Query | Enter a query id | shows time based history |

## Identifying problems

The views include

**Hardware Constraints**: Not single query. CPU: observe "% Processor time". Storage: monitor at O/S level. Suboptimal queries biggest culprit.
**Suboptimal Query constructs**:  Watch out for single row operations, cursors scalar functions, table value functions.
**SARGability**: Where clause formatted to use an index. Avoid two sided "like" and parsing column e.g. "left(city,1) = 'M'". 
**Missing Indexes**: Vital. Drop unused. *Clustered Index Scan* is sign index used. *Nonclustered Index seek*,*Key lookup* indicate missing columns on index
**Missing/out of date Statistics**: Check *sys.dm_db_stats_properties* for last update.

## Locking and Blocking
Deadlocks are auto resolved after a period of time. A Deadlock Victim is choosen. 
*sys.dm_tran_locks* and *sys.dm_exec_requests* can assist 
Typically poor transactional design

## ToDo
- Understand wait types
- Isolation types

## Performance
First step is to collect data measurements that form a baseline. 
Automatic Tuning uses FORCE PLAN and monitors 
Normalise OLTP but Denormalise OLAP 
First, Second, Third forms

For OLAP
- Facts: for measurements e.g. sales
- Dimensions: smaller row counts but lot of columns e.g. investory, time, geography
- Star Schema: Facts join the dims
- Snowflake: more normalisation, so less space but more joins

Indexes:
- Keep **clustered** as narrow as possible ie unique. Also good to have this as the typical sort by direction. 
- Note this is logical order (physical changes over time with deletions etc)
- **Non-clustered** suited to multi column indexes. Can also be unqiue
- Think workloads, optimise around typical queries
- Properly indexed DB results in less IOs (ie disk reads)
- GOAL: most benefit from fewest number of indexes
- check with dvms index usage, carefull delete non-used (might be used diff time of year), test on non-prod?, drop/recreate indexes as period occurs
- maintenance operations should take place at non busy times
- avoid query hints (options)
  - maxdop
  - recompile (temp plan each run)
  - Fast: return top few records and continue 

Before change:
- Issues cause by: concurrent user activity, system resources utilisation & overall workload
- understand broader effects of change & monitor
- optimising queries v maintaining system stability

## Waits
- Resource: locks, latches, disk I/O
- Queue: worker thread is idle
- External: eg linked server, network

 sys.dm_os_wait_stats v sys.dm_db_wait_stats (Azure)

 Query Store Hints
 - use query store hints to add options to queries.
 - useful where you can't modify the query

 Log Governance
 - be aware that Azure SQL enforce resource limits so as to meet SQL. 

## Columnstore
Unlike traditional rowstore, data is physicall stored as column-wise data format. 
Both logically stored as table with rows & columns 
Columnstore slices table into *rowgroups* with high compression 
Each column in rowgroup is stored in *column segment* 
*Clusterd Columnstore index* is the physical storage. Might use additional deltastore/b-tree in the background. 
*Non clustered columnstore index* is additional index. For real-time operational analytics 
Recommended for DataWarehousing, queries that run large aggregation workloads


## Plan operators
[documentation](https://learn.microsoft.com/en-us/sql/relational-databases/showplan-logical-and-physical-operators-reference?view=sql-server-ver17)

| operator | description | usage |
| --- | --- | --- |
| Key lookup | lookup on a table with clustered index | indicates the query might benefit from performance tuning by adding covering index |
| Nested Loops | used in joins. search on inner table for each row on outer. | |
| Table scan | retrieves all row on a table | |

## Extended Events
Built on SQL Profiler 
Monitor I/O, DDL operations, deadlocks 
Create a session to capture selected events 
Can filter by some criteria to only caputure instances you are interested in. 
Store to: File, In Memory ring, event counter, 

## Database Watcher
New preview product.
Dashboards that can be used to monitor a range of servers/databases 

## Workload Groups
Container for session requests
Usefull to limit how much resources a workload can use