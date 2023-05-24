### Optimize count query by specific column

1. Check that our table doesn't have any index. If it has, drop it.   
 `SHOW INDEX from orders;`

2. Lets count how many orders exist by specific currency.
 ```
 -- EXPLAIN
 SELECT 
  COUNT(currency_code = "SEK" or NULL) as SEK_orders, 
  COUNT(currency_code = "DKK" or NULL) as DKK_orders 
 FROM orders;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Create index for `currency_code`.
 `CREATE INDEX currency_idx ON orders(currency_code);`
 `SHOW INDEX from orders;`

4. Execute previous SELECT query.
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

5. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

6. Try to explain why there is the difference between results.

7. Drop current index.

8. The goal:
 - learn simple technic to improve count query
 - see how correct index can improve query perfomance