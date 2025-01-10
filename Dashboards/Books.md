# Books read in 2024

```sqlseal
SELECT name, author FROM files
WHERE type = 'book'
AND strftime("%Y",date_finished)="2024"
```
