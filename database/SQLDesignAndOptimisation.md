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
