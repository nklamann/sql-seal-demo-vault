You can use advanced functionality like JSON functions to further interact with your data.
Every property that is of type list will get transformed into an array stored as JSON inside the database. To expand it into individual rows (which might result with many rows per original table) you can use `json_each` function. For more information refer to the [SQLite documentation](https://www.sqlite.org/json1.html#the_json_each_and_json_tree_table_valued_functions).


Below we have expanded categories for each note we have. This results with more notes than originally, one for each category x note combination that we had.

```sqlseal
HTML
SELECT name, files.path, c.value as category
FROM files, json_each(files.categories) c
WHERE categories IS NOT NULL
```

Based on that we can start filtering by the categories. For example let's get all the notes that have [[Category 2]] assigned to them:

```sqlseal
SELECT name, files.path, c.value as category
FROM files, json_each(files.categories) c
WHERE categories IS NOT NULL
AND
c.value='[[Category 2]]'
```
