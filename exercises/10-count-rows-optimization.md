### Optimize simple count query 

1. Check that our table doesn't have any index. If it has, drop it.   
 `SHOW INDEX from orders;`
 No index needed here since `id` is a primary key which is the index.

2. Execute count query.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE COUNT(*) FROM orders WHERE id > 10;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. But we still can improve this query.
```
-- EXPLAIN
SELECT (SELECT COUNT(*) FROM orders) - COUNT(*) FROM orders WHERE id <= 10; 
```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

5. Try to explain why there is the difference between results.

6. The goal:
 - learn simple technic to improve count query
 - read execution plan for query with subquery