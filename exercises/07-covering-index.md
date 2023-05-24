### Covering index
Does the order in index matter?

1. Check that our table doesn't have any index. If it has, drop it.   
 `SHOW INDEX from orders;`

2. Create multicolumn(composite) index for three columns:
 - created_at,
 - amount,
 - customer_id

3. Execute this query.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
 AND customer_id = 1687394;
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

4. Drop current index and create a new index where 
 - place customer_id on the SECOND place in the composite index
 Then
 - get execution plan
 - run SELECT statement and measure execution time

5. Drop last index and create a new index where 
 - place customer_id on the FIRST place in the composite index
 Then
 - get execution plan
 - run SELECT statement and measure execution time
 - impact the inequality operator on the execution time

6. Now lets run this query for all customers(remove from where clause specific customer condition)
 You still should have the index with `customer_id` on the first place.
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE SUM(amount)
 FROM orders
 WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59';
 ```
 - Measure execution time.
 - Get execution plan, use EXPLAIN statement.

7. Get the perfomance schema details
 - use the queries from 04th lesson with `digest` for your query
 - analyze the results, find the best one

8. Try to explain why there is the difference between results.

9. The goal:
 - learn that the order in the composite index is important
 - index which includes all columns from the query is covering index