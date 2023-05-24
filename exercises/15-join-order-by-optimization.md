### Optimization JOIN query with ORDER BY

1. Check that our tables `orders` and `customers` don't have any index. If they have, drop them.   
 `SHOW INDEX from orders;`
 `SHOW INDEX from customers;`
 - drop index: 
 `DROP INDEX {index_name} ON {table_name};`

2. Execute this JOIN query with ORDER BY
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE customer_id, COUNT(*) FROM customers
 LEFT JOIN orders ON orders.customer_id = customers.id
 GROUP BY customer_id;
 ``` 

3. Lets create index on `orders` table 
 with these column `customer_id` since you are using them in the query
 `CREATE INDEX customer_id_idx ON orders(customer_id);`
 - check the index
 `SHOW INDEX from orders;`

4. Execute the same query.

5. Get perfomance schema details for the executed queries
 - find unique piece of text in your query
 - get the `digest` of your query
 - get the perfomance schema details
 - analyze the results

6. Try to test this query
 ```
 -- EXPLAIN
 SELECT SQL_NO_CACHE country, COUNT(*) FROM customers
 LEFT JOIN orders ON orders.customer_id = customers.id
 GROUP BY country;
 ``` 

7. The goal:
 - understand how the query with JOIN and ORDER BY perfome in the storage engine
 - see the difference between the query execution time with index and without index