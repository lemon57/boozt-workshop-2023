### Query with JOIN optimization

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them.   
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`

2. Execute this query.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 LEFT JOIN customers ON orders.customer_id = customers.id
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
 AND customers.email LIKE '%yahoo%';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Create index for `orders.customer_id`.
The main rule to optimize JOIN query say: create index on column using on ON or USING clauses.
`CREATE INDEX customer_id_idx ON orders(customer_id);`

4. Execute previous query.
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

5. But we use more columns in our query such as `customers.email`
 - create index for `customers.email`
 `CREATE INDEX email_idx ON customers(email);`
 - execute the query
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

6. In addition to that we also use
 inequality operator `BETWEEN...AND` and range operator `LIKE`.
 - drop previous index on `orders` table
 `DROP INDEX customer_id_idx ON orders;`
 - create the composite index for `orders` table
 `CREATE INDEX customer_created_amount_idx ON orders(customer_id, created_at, amount);`
 - execute the query
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

7. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

8. Try to explain why there is the difference between results.

8. Try to explain current results.
 - what can be the solution to improve the query perfomance more?

9. The goal:
 - get execution plan for JOIN query
 - understand the execution plan for JOIN query
 - trying to find the way to improve the query perfomance 
