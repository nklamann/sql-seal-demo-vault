> [!INFO] Stacked Bar Example
> Below you can see how you can perform advanced aggregation / pivot table on your data and then stack them on the interactive chart.

```sqlseal
TABLE commute = file(/Data/transport.csv)


CHART {
	xAxis: {
		type: 'category'
	},
	legend: { show: true },
	yAxis: { },
	series: [{
		type: 'bar',
		name: 'Walk',
		encode: { y: 'walk' },
		stack: 'x'
	},
	{
		type: 'bar',
		name: 'Bus',
		encode: { y: 'bus' },
		stack: 'x'
	},
	{
		type: 'bar',
		name: 'Bike',
		encode: { y: 'bike' },
		stack: 'x'
	}
]
}
SELECT
	Date,
	round(sum(case when transport_type = "walk" then distance_km end), 2) as walk,
	round(sum(case when transport_type = "bus" then distance_km end), 2) as bus,
	round(sum(case when transport_type = "bike" then distance_km end), 2) as bike,
	round(sum(distance_km), 2) as total
FROM commute
GROUP BY Date
ORDER BY DATE DESC
```
