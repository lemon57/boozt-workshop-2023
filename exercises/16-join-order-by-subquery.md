### Optimization JOIN query with ORDR BY with subquery
// The temporary table created by the subquery has no indexes

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them.   
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`
 - drop index: 
 `DROP INDEX {index_name} ON {table_name};`

2. Execute this query
```
-- EXPLAIN
SELECT SQL_NO_CACHE email, g.cnt FROM customers
INNER JOIN (
 SELECT SQL_NO_CACHE customer_id, COUNT(*) AS cnt
 FROM orders
 GROUP BY customer_id
) AS g ON g.customer_id = customers.id;
```

3. Lets create index on `orders` table
 with `customer_id` column 
 `CREATE INDEX customer_idx ON orders(customer_id);`
 - check the index
 `SHOW INDEX from orders;` 

4. Execute the same SELECT query.

5. Lets create index on `customers` table
with `email` column
 `CREATE INDEX email_idx ON customers(email);`
 - check the index
 `SHOW INDEX from customers;`

6. Execute the same query.

7. Get perfomance schema details for the executed queries
 - find unique piece of text in your query
 - get the `digest` of your query
 - get the perfomance schema details
 - analyze the results

8. The goal:
 - understand how the query with JOIN, ORDER BY and subquery perfome in the storage engine
 - see the difference between the query execution time with index and without index