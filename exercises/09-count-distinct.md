### Optimize count query with distinct

1. Check that our table doesn't have any index. If has, drop it.   
 `SHOW INDEX from orders;`

2. Execute count query with DISTINCT keyword on *currency_code* column.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE COUNT(DISTINCT currency_code) FROM orders;
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
 - see how the correct index can significantly improve execution count query time