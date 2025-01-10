
> [!NOTE] Example
> This example uses [[Data/finance.csv]] CSV file and groups them by date. This show how you can use SQL aggregation functions like `COUNT`, `SUM` and `AVG` to process your data.


```sqlseal
TABLE finance = file(/Data/finance.csv)

HTML
SELECT date, COUNT(*) as noTransactions, round(avg(amount),2) as avgAmount, round(sum(amount),2) as totalSpent FROM finance GROUP BY date
```
