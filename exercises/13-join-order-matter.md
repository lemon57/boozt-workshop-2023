### Continue optimization for JOIN query
Lets improve execution time for the query from 12th lesson.
// orders.customer_id = {1000000...2000000}

1. Check what indexes we have in our tables:
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`
You should have:
 - on `orders` table, composite index with such columns and such order: *customer_id*, *created_at*, *amount*
 - on `customers` table, index for `email` column

2. The query for this lesson:
```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 LEFT JOIN customers ON orders.customer_id = customers.id
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
 AND customers.email LIKE '%yahoo%';
 ```

3. Change the index for `orders` table
 - drop current index
 `DROP INDEX customer_created_amount_idx ON orders;` 
 - create new one with follwong column order 
 `CREATE INDEX created_customer_amount_idx ON orders(created_at, customer_id, amount);` 
 - execute the query
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Change the index again for `order` table
 - drop current index
 `DROP INDEX created_customer_amount_idx ON orders;` 
 - create new one with follwong column order 
 `CREATE INDEX created_amount_customer_idx ON orders(created_at, amount, customer_id);` 
 - execute the query
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.
 
5. Get the perfomance schema details
 - use query from 12th lesson with `digest` for our query
 - analyze the results, find the best one
 - what index gets the best result, try to explain

6. The goal:
 - create different composite indexes for the query
 - get perfomance schema details for the executed queries
 - find the best query
 - get the understanding why this index works better compare to others

