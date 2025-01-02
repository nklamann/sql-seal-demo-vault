```sqlseal
SELECT
a(name, path) as name,
img(picture) as image,
Cast ((
    JulianDay('now') - JulianDay(birthday)
) / 365 AS Integer) as age
FROM files WHERE type = 'contact'
```
