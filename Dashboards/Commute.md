
> [!NOTE] Example
> The following example summarises [[Data/transport.csv]] file that contains records of commute across multiple days. The transportation mode and distance is provided for each of them.
> The query below summarises this data by date and mode of transport. It shows how you can use aggregation with `CASE` clause to filter data for aggregation purpouses.

```sqlseal
TABLE commute = file(/Data/transport.csv)

HTML
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
