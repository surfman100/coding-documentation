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

## Query Store
- Plan store: Stores estimated execution plan information.
- Runtime stats store: Stores execution statistics information.
- Wait stats store: Persists wait statistics information.

available under DB->QueryStore->7 views