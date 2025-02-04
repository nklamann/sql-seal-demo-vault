---
geändert: "true"
---
# Thai in the database

> [!NOTE] Example of support for non-latin languages
> SQLSeal should allow for any UTF8 language to be supported. The limitation is the column names need to comply with general SQLite rules.


```sqlseal
TABLE thailand_tourism = file(Data/thailand_domestic_tourism_2019_2023.csv)

SELECT province_thai, AVG(value) as average_value  FROM thailand_tourism
WHERE region_thai='ภาคกลาง'
GROUP BY province_thai
```


# German in the Properties

> [!NOTE] Special characters transformations
> If your column contains special character, it will get transformed to `_`. That's why `geändert` below is transformed to `ge_ndert`. This should be fixed in the later versions of the plugin to allow you for nicer character escaping.


```sqlseal
HTML
SELECT name, ge_ndert FROM files
WHERE ge_ndert IS NOT NULL
```
