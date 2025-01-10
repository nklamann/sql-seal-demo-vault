
> [!NOTE] Example
> Example below queries all notes from the vault that have `type=contact`. It uses properties from these files: `picture` to show picture of the person and `birthday` to compute their age.
> The query uses SQLite built in `JulianDay` method to compute age of the friend.





```sqlseal
SELECT
a(name, path) as name,
img(picture) as image,
Cast ((
    JulianDay('now') - JulianDay(birthday)
) / 365 AS Integer) as age
FROM files WHERE type = 'contact'
```
