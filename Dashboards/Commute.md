```sqlseal
TABLE commute = file(/Data/transport.csv)

SELECT
	Date,
	sum(case when transport_type = "walk" then distance_km end) as walk,
	sum(case when transport_type = "bus" then distance_km end) as bus,
	sum(case when transport_type = "bike" then distance_km end) as bike,
	sum(distance_km) as total
FROM commute
GROUP BY Date
ORDER BY DATE DESC
```
