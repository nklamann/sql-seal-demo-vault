---
geändert: "true"
prefer-view: edit
หมวดหมู่: note
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
> If your column contains special character, it will get transformed to its romanised form. That's why `geändert` below is transformed to `geandert`.


```sqlseal
HTML
SELECT name, geandert, prefer_view FROM files
WHERE geandert IS NOT NULL
```

