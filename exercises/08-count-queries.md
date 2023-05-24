### How count function work
COUNT() - function that counts *values* and *rows*.

1. Drop all previous indexes. 
 `SHOW INDEX from orders;`
 `DROP INDEX {index_name} ON orders;`

2. Execute count query.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE COUNT(*) FROM orders;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Make some values on `currency_code` column NULL.

4. Execute count query using column name `currency_code`.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE COUNT(currency_code) FROM orders;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

5. Create index for `currency_code`.
 `CREATE INDEX currency_idx ON orders(currency_code);`
 `SHOW INDEX from orders;`

6. Execute the count query with `currency_code` column.
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

7. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

8. Try to explain why there is the difference between results.

9. Drop current index.

10. The goal:
 - understand how COUNT() function work
 - learn how to use index to improve count query