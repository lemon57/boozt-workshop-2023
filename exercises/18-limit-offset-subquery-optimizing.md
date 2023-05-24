### Another technic to omptimize query with OFFSET and LIMIT 
Using subquery
// The idea is lets the DB engine examine as little data as possible in a index without accesing the rows
 
To see the difference more precise it is better to remove all indexes. 
After you can execute these queries with index.

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them.   
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`
 - drop index: 
 `DROP INDEX {index_name} ON {table_name};`

2. Execute this query:
```
-- EXPLAIN
SELECT SQL_NO_CACHE prefixed_order_id, status FROM orders ORDER BY status LIMIT 1000, 10;
```
 - Get execution plan, use EXPLAIN statement.

3. Get perfomance schema details for the executed query
 - find unique piece of text in your query
 - get the `digest` of your query
 - save it to compare it with another query

4. Now execute following query:
```
-- EXPLAIN
SELECT prefixed_order_id, status FROM orders
INNER JOIN (
	SELECT id FROM orders
	ORDER BY status LIMIT 1000, 10
) AS lim USING(id);
```
 - Get execution plan, use EXPLAIN statement.

5. Get perfomance schema details for last executed query
 - find unique piece of text in your query
 - get the `digest` of your query
 - save it to compare it with another query

6. Compare results from perfomance schema details for each query
 - try to explain the reasons why one query faster then other

7. Lets create index on `orders` table
 with `status` column 
 `CREATE INDEX customer_idx ON orders(customer_id);`
 - check the index
 `SHOW INDEX from orders;`

8. Execute these queries now with index

9. Compare results from perfomance schema details for each query

10. The goal: 
 - learn the technic how to optimize the query with OFFSET and LIMIT
 - see the difference between the query execution time with index and without index 
 - based on knowledge how storage engine is working to perform such query, interpret the result