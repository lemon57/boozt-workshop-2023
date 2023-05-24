### 20 - Two separate indexes for two differet columns vs one composite index with two columns

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them. 
`SHOW INDEX from orders;`
`SHOW INDEX from customers;`
 - drop index: 
 `DROP INDEX {index_name} ON {table_name};`

2. Execute this query:
```
-- EXPLAIN
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
```

3. Create separate index only for `created_at` column
`CREATE INDEX created_at_idx ON orders(created_at);`

4. Execute the same query

5. Create separate index only for `amount` column
`CREATE INDEX amount_idx ON orders(amount);`

6. Execute the same query

7. Create composite index for `created_at` and `amount` columns
`CREATE INDEX created_at_amount_idx ON orders(created_at, amount);`

8. Execute the same query

9. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

10. The goal:
- to see the difference with two separate indexes on the table and one composite index for the same columns
- analyze and describe the results 