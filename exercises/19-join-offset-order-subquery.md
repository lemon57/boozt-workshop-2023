### 19 - Optimization JOIN query with OFFSET and ORDER BY

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them.   
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`
 - drop index: 
 `DROP INDEX {index_name} ON {table_name};`

2. Execute this query:
```
-- EXPLAIN
SELECT SQL_NO_CACHE email, prefixed_order_id, status FROM customers 
LEFT JOIN orders ON orders.customer_id = customers.id
ORDER BY email LIMIT 1000, 10;
```

3. Lets create index on `orders` table
`CREATE INDEX customer_prefixed_status_idx ON orders(customer_id, prefixed_order_id, status);`
- check the index:
`SHOW INDEX from orders;`

4. Run the same query.

5. Lets create index on `customers` table
`CREATE INDEX email_idx ON customers(email);`
- check the index:
`SHOW INDEX from customers;`

6. Run the same query.

7. Now execute this query:
```
-- EXPLAIN
SELECT SQL_NO_CACHE oc.email, prefixed_order_id, status FROM orders 
INNER JOIN (
 SELECT SQL_NO_CACHE *
 FROM customers
 ORDER BY email
) AS oc ON orders.customer_id = oc.id
ORDER BY oc.email LIMIT 1000, 10;
```
- run this query with index and without index

8. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

9. The goal:
- to see how the storage engine perfome JOIN query with OFFSET and ORDER BY
- analyze and describe the results 
