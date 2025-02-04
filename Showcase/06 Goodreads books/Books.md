---
author: Kurt Vonnegut
---
```sqlseal
TABLE books = file(books.csv)

HTML
SELECT
	a(title, 'https://openlibrary.org/isbn/' || CAST(isbn13 as int)) as title,
	authors,
	img('https://covers.openlibrary.org/b/isbn/' || CAST(isbn13 as INT) || '-L.jpg') as cover FROM books
WHERE authors
	LIKE '%' || @author || '%'
LIMIT 10
```
