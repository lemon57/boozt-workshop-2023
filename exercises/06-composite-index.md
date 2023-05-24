### Multicolumn(composite) index

1. Check that our table doesn't have any index. If it has, drop it.   
 `SHOW INDEX from orders;`

2. Create multicolumn(composite) index
`CREATE INDEX created_at_amount_idx ON orders(created_at, amount);` 

2. Execute this query.  
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Execute the same query but for specific customer.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
 AND customer_id = 1687394;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

5. Try to explain why there is the difference between results.

6. The goal:
 - understand composite index
 - get and read execution plans for queries on table with composite index 

7. Drop current index.

8. Extra: 
 - common mistakes with composite index