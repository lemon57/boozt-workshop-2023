### Optimize query with LIMIT and OFFSET using index
// LIMITS and OFFSET usually used with ORDER BY clause
// Do offset on covering index
// Also it is a good practice to have index on ordering otherwise there will be a lot of filesorts

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

3. Lets create index on `orders` table
 with `status` column 
 `CREATE INDEX status_idx ON orders(status);`
 - check the index
 `SHOW INDEX from orders;` 

4. Run the same SELECT query

5. Lets create index on `orders` table
 with `status` and `prefixed_order_id` column 
 `CREATE INDEX prefixed_status_idx ON orders(prefixed_order_id, status);`
 - check the index
 `SHOW INDEX from orders;` 

6. Run the same SELECT query

7. Get perfomance schema details for the executed queries
 - find unique piece of text in your query
 - get the `digest` of your query
 - get the perfomance schema details
 - analyze the results

8. The goal: 
 - understand how the query with OFFSET and LIMIT perfome in storage engine,
 - see the difference between the query execution time with index and without index