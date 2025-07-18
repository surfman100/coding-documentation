# Oracle SQL
Over tip and tricks when using ORACLE PL/SQL

# Drop existing object before creation

```
DECLARE
    table_does_not_exist EXCEPTION;
   PRAGMA EXCEPTION_INIT(table_does_not_exist, -942);
BEGIN
    execute immediate 'drop table MY_TABLE';
EXCEPTION WHEN table_does_not_exist THEN
    NULL; 
END;
/
```

# Escape character on Declare blocks
note lack of escape character  here
```
create table my_table(
ID INT NULL
);
````

but use here
```
DECLARE
BEGIN
    NULL;
END;
/
````
