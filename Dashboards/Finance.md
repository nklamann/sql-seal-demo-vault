
```sqlseal
TABLE finance = file(/Data/finance.csv)

HTML
SELECT date, COUNT(*) as noTransactions, avg(amount) as avgAmount, sum(amount) as totalSpent FROM f GROUP BY date
```
