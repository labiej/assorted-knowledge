# Update queries
When refactoring a database schema it is not uncommon to update a row based on the results of a JOIN query. The naive approach is to first perform a select with a JOIN and store the results in a temporary table or a table variable.
```sql
-- First select the data (and store it somewhere)
SELECT
	Id
FROM Entity
JOIN OtherEntity ON OtherEntity.EntityId = Entity.Id
WHERE OtherEntity.Value = 'I need to change'

-- Next update
UPDATE Entity SET [Column] = 'something has changed' WHERE Id in (SELECT * FROM #TempTable)
```

While this is a viable method it can be done in a single query as follows
```sql
UPDATE e
SET
	e.[Column] = 'something has changed'
FROM Entity e
JOIN OtherEntity ON OtherEntity.EntityID = e.Id
WHERE OtherEntity.Value = 'I need to change'
```
