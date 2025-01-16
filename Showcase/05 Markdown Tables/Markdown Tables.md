You can use tables inside your markdown file to query their content using `table(number)`. Check example below and [more documentation here](https://hypersphere.blog/sql-seal/query-markdown-tables.html).


```sqlseal
TABLE expenses = table(0)
```

| Date       | Name          | Amount |
| ---------- | ------------- | ------ |
| 2025-01-01 | Grocery       | 20.40  |
| 2025-01-01 | Cinema Ticket | 8.20   |
| 2025-01-02 | Grocery       | 5.0    |
| 2025-01-02 | Game on Steam | 20.0   |
| 2025-01-03 | Grocery       | 15.98  |

```sqlseal
TABLE expenses = table(0)

markdown
SELECT date, ROUND(SUM(Amount), 2) as Spent
FROM expenses
GROUP BY date
ORDER BY date
```


I've spent in total `S> SELECT ROUND(SUM(amount), 2) FROM expenses`.


