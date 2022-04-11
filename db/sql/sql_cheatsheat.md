### distinct value_counts()

```sql
select col, count(*) as num from table group by col
```

### retrieve data by chunks

https://www.tutorialspoint.com/retrieve-a-large-select-by-chunks-in-mysql

```
SELECT *FROM yourTableName ORDER BY yourColumnName LIMIT 0,10;
SELECT *FROM yourTableName ORDER BY yourColumnName LIMIT 10,20; //11 to 30
SELECT *FROM yourTableName ORDER BY yourColumnName LIMIT 30 ,20; 31 to 50.
```

-   python & sql datetype mapping

    https://docs.microsoft.com/en-us/sql/machine-learning/python/python-libraries-and-data-types?view=sql-server-ver15
