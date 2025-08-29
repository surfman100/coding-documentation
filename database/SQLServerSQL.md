# Transaction SQL tips

## Indexing
- dont select cols you dont need, possibly more i/o operations to retrieve from other pages
- always have a clustered index, minimze non clustered
- add index seperately, not as part ok PK constraint
- leaf level is bottom of index and contains index columns in their sort order
- intermediate levels and root


## Delete duplicates in a table
This is dead handy

```
delete T
FROM
(
SELECT *
, DupRank = ROW_NUMBER() OVER (
              PARTITION BY [date],  operator, serial_number
              ORDER BY (SELECT NULL)
            )
FROM FleetUtilization
) AS T
WHERE DupRank > 1
```

