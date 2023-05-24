### Using function in query 
How it can affect our query perfomance?  

1. Check that our table doesn't have the index. If has, drop it.   
 `SHOW INDEX from orders;`  

2. Execute this query with function YEAR.  
```
-- EXPLAIN
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
WHERE YEAR(created_at) = 2019 OR YEAR(created_at) = 2020;
```
- Measure execution time.

3. Get execution plan for this query, use EXPLAIN statement.

4. Creat index for `created_at` column. 
 - `CREATE INDEX created_at_idx ON orders(created_at);`
 - Execute SELECT statement.   
 - Measure execution time.  

5. Drop `created_at` index.
 `DROP INDEX created_at_idx ON orders;`

6. The goal: 
 - create and drop index for the table
 - get execution plan for the query
 - learn how to read the result of the EXPLAIN statement
 - understand the impact of using functions in the SQL query

** You can include or exclude SQL_CACHE or SQL_NO_CACHE modifiers in the SELECT statement. 