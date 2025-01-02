This dashboard shows notes that you have "TODO". These can be notes that have TODO in their name or have todo tag assigned to them.


```sqlseal
HTML
SELECT name, path
FROM files
WHERE name LIKE '%todo%'
OR (SELECT COUNT(*) FROM tags WHERE fileid=files.path AND tag = '#todo')
```

