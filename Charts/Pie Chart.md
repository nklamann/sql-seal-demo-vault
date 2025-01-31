
> [!INFO] Pie Chart Example
> Code below shows how easy you can create PieChart out of your data. Change data in your table and see chart updating automatically.

| Category      | Amount |
| ------------- | ------ |
| Rent          | 1500   |
| Groceries     | 200    |
| Entertainment | 150    |
| Repairs       | 200    |
```sqlseal
TABLE finances = table(0)

CHART {
	series: [{
		type: 'pie'
	}]
}
SELECT * FROM finances
```
