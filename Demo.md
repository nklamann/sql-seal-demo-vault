This file contains demos that has been used in the initial introduction video for SQLSeal:


![Video](https://www.youtube.com/watch?v=yXDrpWDeQPg).

# Intro

> [!NOTE] SQLSeal Intro
> SQLSeal allows you to query notes in your vault using SQL syntax. By default it exposes tables: `files`, `tags` and `tasks`.

> [!NOTE] New to SQL?
> If you're new to SQL, don't worry. SQL is an industry standard where it comes to operating on data, so there are plenty of tutorials to help you get started. I recommend https://sqlbolt.com


# Querying files
```sqlseal
SELECT * FROM files
```

# Querying tags

```sqlseal
SELECT * FROM tags
```

# Example: Get all files with TODO in the name

```sqlseal
SELECT *
FROM files LEFT JOIN tags ON files.path=tags.fileid
WHERE name LIKE '%todo%'
OR tag='#todo'
```

# Inline Queries

My vault contains `S> SELECT COUNT(*) FROM files` files and `S> SELECT COUNT(DISTINCT tag) FROM tags` tags.
# Using CSV files


> [!NOTE] Querying CSV files
> SQLSeal allows to query data stored in CSV (comma separated values) files. It also allows you to preview these files and edit them in the interface. This makes a great way to store additional data you might want to use in your notes.

# Analysing expenses
```sqlseal
TABLE expenses = file(Data/expenses.csv)

MARKDOWN
SELECT date, SUM(amount) as amount FROM expenses
GROUP BY date
ORDER BY date
```

# Live Updates


# Changing views


| date       | amount |
| ---------- | ------ |
| 2023-12-29 | 152.09 |
| 2023-12-30 | 201.71 |
| 2023-12-31 | 284.2  |
| 2024-01-01 | 171.27 |
| 2024-01-02 | 314.11 |



```sqlseal
SELECT checkbox(completed) as isCompleted, task, a(files.name, filepath) as sourceFile 
FROM tasks JOIN files
	ON tasks.filepath=files.path
```
