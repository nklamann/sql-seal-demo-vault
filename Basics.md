This file shows the basics of using SQLSeal. Feel free to play with each of the examples and modify them to your liking.
# Querying vault files

## Basics
You can query files inside your vault by interacting with the `files` table. It consists of all the files you have in your vault. It automatically combines all the properties so they are accessible as columns.

```sqlseal
SELECT * FROM files LIMIT 10
```

## Aggregation
You can use [any aggregation functions available in SQLite](https://www.sqlite.org/lang_aggfunc.html) to process your data. In the following example we will select all the data that has type set and group them by it.

```sqlseal
SELECT COUNT(*), type FROM files
WHERE type IS NOT NULL
GROUP BY type
```

## Tags
You can access all the tags associated to the files by accessing the `tags` table. It consists of tag name and fileid:

```sqlseal
SELECT * FROM tags
```

## Tasks
You can also access all tasks by accessing the `tasks` table.

```sqlseal
SELECT * FROM tasks
```

SQLSeal also exposes a special function called `checkbox` which allows you to display checkboxes instead of 0/1 value for a completed field. Please note that it will not be interactive so you cannot change the status of a task (at least for now).
```sqlseal
SELECT checkbox(completed), task FROM tasks
```

# Interacting with CSV files
You can create a table from your CSV file in SQLSeal using this special syntax:
```
TABLE tableName = file(pathToTheFile)
```

This will create a table named `tableName` and make it accessible **across the whole file it was defined in**.

> [!NOTE] Visibility of the tables
> Internally tables are prefixed with the identifier of the file. This means you can create tables with the same name across multiple files and they will not clash with each other. Currently only `files`, `tags` and `tasks` are available globally but in future users will be able to define custom global tables.

The following example creates local table `movies` based on the `watchlist.csv` file:

```sqlseal
TABLE movies = file(Movies/watchlist.csv)

SELECT * FROM movies LIMIT 10
```

## Aggregation
You can aggregate, filter and process data with a majority of the SQL functions, including CTE.

```sqlseal
WITH most_voted AS (
SELECT * FROM movies WHERE num_votes > 5000
)
SELECT title, runtime__mins_, directors FROM most_voted
```


## Grouping
```sqlseal
TABLE ratings = file(/Movies/ratings.csv)

HTML
SELECT 
    genre,
    COUNT(*) as movies_watched,
    ROUND(AVG(rating), 1) as average_rating,
    group_concat(title) as titles
FROM ratings
WHERE rating > 4
GROUP BY genre
```

## Expenses example

```sqlseal
TABLE expenses = file(/Data/expenses.csv)

SELECT 
    category,
    SUM(amount) as total_spent,
    COUNT(*) as number_of_purchases,
    ROUND(AVG(amount), 2) as avg_per_purchase
FROM expenses
GROUP BY category
ORDER BY total_spent DESC
```

# Changing views / renderers
SQLSeal comes with 3 views included - `GRID` (default), `HTML` (basic table) and `MARKDOWN` (markdown text you can copy if you want to use table results in your other documents without using SQLSeal later). Here is the same data in all 3 formats:

```sqlseal
GRID
SELECT title, genres FROM movies LIMIT 10
```

```sqlseal
HTML
SELECT title, genres FROM movies LIMIT 10
```

```sqlseal
MARKDOWN
SELECT title, genres FROM movies LIMIT 10
```
