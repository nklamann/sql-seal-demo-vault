You can select all tags by joining files and tags table. They share `path` column so you can use natural join to make it easier.

```sqlseal
SELECT * FROM files NATURAL JOIN tags
```

