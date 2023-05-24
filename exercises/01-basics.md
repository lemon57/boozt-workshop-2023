### Basics command to operate with index:
1. Show index:
 `SHOW INDEX from orders;`

2. Create index:
 `CREATE INDEX created_at_idx ON orders(created_at);`

3. Remove index:
 `DROP INDEX created_at_idx ON orders;`

4. Show execution plan of the query - prepend your query by `EXPLAIN` keyword
 `EXPLAIN SELECT * FROM orders where YEAR(created_at) > 2022;`

5. Use EXPLAIN along with ANALYZE (gives us more details about query execution):
 `EXPLAIN ANALYZE SELECT * FROM orders where YEAR(created_at) > 2022;`