# Postgres

Flexible server. Azure Storage.
Managed service. Optimiszed for predictable performance.
Postmaster daemon. Collection of dbs = cluster
Client apps - Azure Data Studio, DBeaver, pgAdmin, psql

## Extensibility
Has extensions. pgSQL. Supports Ruby on Rails.
SQL works best with Optimizer.
Note Stored Procedure creation
```
Create Procedure myproc (myarg int)
    language SQL
    as $$
        Insert into mytable values(myarg);
    $$
```

## Memory
shared_buffers(loads tables and indexes), work_mem (sort ops), effective_cache_size (% of machine mem) 

## Security
Roles (users)
```
CREATE DATABASE testdb;
CREATE ROLE <db_user> WITH LOGIN NOSUPERUSER INHERIT CREATEDB NOCREATEROLE NOREPLICATION PASSWORD '<StrongPassword!>';
GRANT CONNECT ON DATABASE testdb TO <db_user>;
```

you cannot create a user with superuser role

Roles
- azure_su: reserved for use by Microsoft
- azure_pg_admin: administrator role

## Functions and Stored Procedures
Functions can't include transactions, DML. Can't call procedures.
```
--call a stored procedure
call myproc(1,2);

call myproc(
    myarg => 1,
    myarg2 => 2
)

--call a function
select myfunc(3) from [table]
```

you can write function in: 
- SQL
- C
- pl.sql
- ?

| Function Type | Description |
| --- | --- |
| volatile | can modify db and return diff result each time |
| stable | can't modify db and returns same result in same statement. Query Optimizer can use previous runs | 
| immutable | can't modify db and returns same result. |

```
-- stable is hint to optimizer
create function myfunc (myarg int)
returns int 
language 'language_name';
stable
called on null input
as
$$
    <body>
$$
```

## Write ahead logging
inserts/updates are first written to a log and then to disk. reduces disk writes.
controlled using **wal_** server parameters

High availability: secondary server placed in different availability zone
Logical decoding: decodes entires in write ahead log to make them understandable

create publication/subscriber in the seperately setup databases. great for reporting