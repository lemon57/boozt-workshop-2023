### Get query perfomance from MYSQL performance_schema database
The MySQL Performance Schema is a feature for monitoring MySQL Server execution at a low level.

1. Turn on storing the query execution details in performance_schema database
 - choose `performance_schema` database
 - run following queries:
 `UPDATE performance_schema.setup_instruments SET enabled = 'YES', timed = 'YES';`
 `UPDATE performance_schema.setup_consumers SET enabled = 'YES';`
 The data will be stored inside this table
 `performance_schema.events_statements_history_long`

2. Execute this query; 
```
SELECT SQL_NO_CACHE SUM(amount)
FROM orders
WHERE created_at BETWEEN '2019-10-24 00:00:00' AND '2020-10-25 23:59:59'; 
```

3. Shema perfomance can provide additional level of detail on query execution stage.
 Execute this query:
 ```
SELECT
    TRUNCATE(timer_wait / 1000000000000, 2) AS timer_wait_sec,
    rows_sent,                             
    rows_examined,                                           
    select_scan,                          
    no_index_used, 
    digest,
    sql_text                             
FROM
    performance_schema.events_statements_history_long
WHERE
    sql_text LIKE '%SELECT SQL_NO_CACHE%'; -- use the unique piece of text from your query 
 ```
 By `sql_text` column in the result of this query you can find your query
 for what you want to get additional execution details. 
 When you find your query, take the value from `digest` column.
 It should look similar to this string:
 `844a184cb9b369331dde961c1458cf5572034e225884c3a11768763a196fc7b2`

 4. Having `digest` of the query you can get all needed the query execution details
 by running following query:
 ```
 SELECT
    TRUNCATE(timer_wait / 1000000000000, 2) AS timer_wait_sec,
    rows_sent,                             
    rows_examined,                                           
    select_scan,                          
    no_index_used               
 FROM
    performance_schema.events_statements_history_long
 WHERE
    digest = '844a184cb9b369331dde961c1458cf5572034e225884c3a11768763a196fc7b2';
 ``` 

5. Get the execution details for the JOIN query what you run on previous lesson.
 - determine the unique piece of text from your query 
 - get the entries from `performance_schema.events_statements_history_long` 
 by using this unique piece of text in LIKE condition
 - find the `digest` of your query
 - get the execution details for the query you are interested in by using `digest` 

6. The goal:
 - pick up some knowledge about MySQL perfomance schema - Server low level execution details
 - find perfomance details for specific query