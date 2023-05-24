### DB engine is smart
When DB engine doesn't use the index even when the tabla has it?

1. Check that our table has the index. If not, create the index.   
 `SHOW INDEX from orders;`

2. Execute this query with wider date range (2019-2020).  
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

3. Execute this query with wider date range (2019-2020) using FORCE_INDEX modifier.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders FORCE INDEX(created_at_idx)
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Execute this query with less date range (2020-2020).
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2020-10-24 00:00:00' AND '2020-10-25 23:59:59';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

5. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

6. Compare results of these three queries and try to explain them.

7. The goal:
 - learn what execution plans DB engine can use for different queries
 - using optimizer hint: FORCE INDEX

8. Drop current index.