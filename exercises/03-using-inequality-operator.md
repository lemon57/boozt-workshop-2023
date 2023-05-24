### Using inequality operator

1. Check that our table doesn't have the index. If it has, drop it.   
`SHOW INDEX from orders;`

2. Execute this query with inequality operators BETWEEN ... AND.  
```
-- EXPLAIN
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
```
- Measure execution time.

3. Get execution plan for this query, use EXPLAIN statement.

4. Creat index for `created_at` column. 
 - `CREATE INDEX created_at_idx ON orders(created_at);`
 - Execute SELECT statement.   
 - Measure execution time.  

5. Don't drop the index, we will use it on next exercise.

6. The goal: 
 - get execution plan for the query
 - read the result of the EXPLAIN statement
 - understand the impact of using inequality operators in the SQL query