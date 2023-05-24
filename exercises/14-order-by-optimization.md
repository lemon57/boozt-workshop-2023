### Optimization QUERY with ORDER BY
// DB engine can use a temporary table or a filesort to perfome such query

1. Check what index we have on `orders` table. If it has any, drop it.   
 `SHOW INDEX from orders;`
 - drop index: 
 `DROP INDEX {index_name} ON orders;`

2. Execute this query:
 ```
 -- EXPLAIN   
 SELECT SQL_NO_CACHE customer_id, COUNT(*) AS cnt
 FROM orders
 GROUP BY customer_id;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Create index for `customer_id` column 
 `CREATE INDEX customer_idx ON orders(customer_id);`
 - check the index
 `SHOW INDEX from orders;`
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Execute the same query.

5. Get perfomance schema details for the executed queries
 - find unique piece of text in your query
 - get the `digest` of your query
 - get the perfomance schema details
 - analyze the results

6. The goal:
 - understand how the query with ORDER BY condition perfome in the storage engine
 - see the difference between the query execution time with index and without index