
> [!NOTE] Description
> This dashboard shows notes that you have "TODO". These can be notes that have TODO in their name or have todo tag assigned to them.
> It shows how you can filter your notes by name or a tag.


```sqlseal
HTML
SELECT name, path
FROM files
WHERE name LIKE '%todo%'
OR (SELECT COUNT(*) FROM tags WHERE fileid=files.path AND tag = '#todo')
```

