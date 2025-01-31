> [!INFO] Simple Bar Chart Example
> You can visualise any data stored in your vault. In this case we are visualising creation date of the files.

```sqlseal
CHART {
	xAxis: {
		type: 'category'
	},
	yAxis: {},
	series: [{
	type: 'bar',
	}]
}
SELECT
	strftime("%Y-%m-%d", created_at) as created_date,
	COUNT(*) as count
FROM files
GROUP BY created_date
ORDER BY created_date
```
