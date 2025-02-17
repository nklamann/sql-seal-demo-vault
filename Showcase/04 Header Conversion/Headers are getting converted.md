SQLSeal will sanitise headers in your query. If your query has characters which are unaccepted as SQLite column names, they will get transformed into underscores (`_`). For example the CSV imported below has header with the name `[person] name > lastname` and it get transformed into `_person___name___lastname`.

```sqlseal
TABLE file = file(file.csv)
HTML
SELECT * FROM file
```
