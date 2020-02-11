# Super Queries

Se pueden realizar super queries utilizando funciones del lenguaje como `sum()`. Por ejemplo:

```
SELECT nationality, COUNT(book_id),
	SUM(IF(year < 1950, 1, 0)) AS`<1950`,
	SUM(IF(year >= 1950ANDyear < 1990, 1, 0)) AS`<1990`,
	SUM(IF(year >= 1990ANDyear < 2000, 1, 0)) AS`<2000`,
	SUM(IF(year >= 2000, 1, 0)) AS`<hoy`
FROM books AS b
JOINauthorsAS a
	ON a.author_id = b.author_id
WHERE
	a.nationality ISNOTNULL
GROUPBY nationality;
```

# Mysqldump

Realiza backups sobre la base de datos.

- Realizar un backup completo: `mysqldump -u usuario -p baseDeDatos`
- Realizar un backup sin datos: `mysqldump -u usuario -p -d baseDeDatos`
- Realizar un backup sin datos a un fichero: `mysqldump -u usuario -p baseDeDatos > esquema.sql`

Se añade la redirección al archivo para volcarlo en un fichero facilmente versionable.
