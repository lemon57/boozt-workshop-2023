### Extra exercises

1. Analyze perfomance the JOIN query with OFFSET and GROUP BY
2. Two separate indexes for different columns VS one composite index with two columns
 - query with OFFSET
 `SELECT SQL_NO_CACHE prefixed_order_id, status FROM orders ORDER BY status LIMIT 1000, 10;`
 - query with inequality operator for specific customer
```
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
AND customer_id = 1687394;
```
3. Analizy perfomance the query with LIKE
```
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
LEFT JOIN customers ON orders.customer_id = customers.id
WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'
AND customers.email LIKE '%yahoo%';
```
 - try to optimize the query