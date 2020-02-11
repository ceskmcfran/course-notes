**Sintaxis**
`INSERT INTO tabla(COLUMNA1, COLUMNA2,...) VALUES('VALOR1','VALOR2')`

# On Duplicate Key

En caso de que haya una clave duplicada se puede manejar con `ON DUPLICATE KEY`:

- `IGNORE ALL`: Ignora los errores (NO UTILIZAR)
- `UPDATE SET campo = VALUES(...)`: Updatea un campo. Muy util con el campo de "tupla activa"

# Queries anidados

Se pueden anidar las Queries de la siguiente manera:
_Sin anidar_: `INSERT INTO books(title, author_id) VALUES('El laberinto del fauno', 6);`
_Anidado_: `INSERT INTO books(title, author_id) VALUES('El laberinto del fauno', (SELECT author_id FROM authors WHERE name = 'Juan Manuel' LIMIT 1));`
