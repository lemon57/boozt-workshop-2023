### Summary for indexing ans query optimization

1. Using functions decrease query perfomance
2. Order in composite index is matter
3. Inequality operators make index optimization harder
4. DB engine is quite smart in most simple quieres
5. Covering index is not the silver bullet
6. Optimization count queries is hard. Dilemma: Fast, accurate, and simple - pick any two.
7. JOIN query:
  - indexes on the columns using in ON or USING clauses
  - consider JOIN order when add indexes
  - add indexes only on the second table in the join order
9. GROUP BY or ORDER BY should refer only to columns from single table 
10. Subquery: preferance to JOIN where it is possible
11. The temporary table created by the subquery has no indexes
12. LIMIT and OFFSET: 
  - index should support ordering
  - do offset on a covering index rather than the full rows
  - use JOIN for such queries,then the server will examine as little data as possibel in an index
    without accesing rows
13. Two separate indexes for two differet columns is not the same as one composite index with two columns