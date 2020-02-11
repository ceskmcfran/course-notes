# Comandos

- Seleccionar todas las tuplas y todas las columnas: `SELECT * from nombreTabla;`
- Seleccionar todas las tuplas de una columna: `SELECT [columna1, columna2, columna3] from nombreTabla;`
- Seleccionar todas las tuplas de una columna limitados: `SELECT [columna1, columna2, columna3] from nombreTabla limit [numeroLimite];`
- Seleccionar todas las tuplas de una columna por condición: `SELECT [columna1, columna2, columna3] from nombreTabla WHERE [condicion = valor];`
- Seleccionar todas las tuplas de una columna por condición: `SELECT * from nombreTabla WHERE columna BETWEEN valor1 and valor2;`
- Seleccionar todas las tuplas de una columna por rango de edad: `SELECT YEAR(NOW()) - YEAR(birthdate) from nombreTabla;`
- Seleccionar todas las tuplas de una columna por coincidencia en la cadena: `SELECT columna1 from nombreTabla WHERE [condicion like '%cadena%'];`
- Contar cuantas tuplas hay en una tabla: `SELECT count(*) from nombreTabla;`

# JOIN (INNER JOIN)

Muestra solo los datos que están relacionados con ambas tablas
`SELECT [alias1.columna1, alias2.columna4, alias1.columna3] FROM tablaPivote AS alias1 JOIN tablaRelacionada AS alias2 ON [alias2.columna = alias1.columna] WHERE [condicion] GROUP BY [columna] ORDER BY [columna];`

# LEFT JOIN

Muestra todos los datos, los que están y los que no se encuentran en ambas tablas
`SELECT [alias1.columna1, alias2.columna4, alias1.columna3] FROM tablaPivote AS alias1 LEFT JOIN tablaRelacionada AS alias2 ON [alias2.columna = alias1.columna] WHERE [condicion] GROUP BY [columna] ORDER BY [columna];`

# Tipos de JOIN

1. Inner Join

Esta es la forma mas fácil de seleccionar información de diferentes tablas, es tal vez la que mas usas a diario en tu trabajo con bases de datos. Esta union retorna todas las filas de la tabla A que coinciden en la tabla B. Es decir aquellas que están en la tabla A Y en la tabla B, si lo vemos en conjuntos la intersección entre la tabla A y la B.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
INNER JOIN Tabla_B B
ON A.pk = B.pk
```

2. Left Join

Esta consulta retorna todas las filas que están en la tabla A y ademas si hay coincidencias de filas en la tabla B también va a traer esas filas.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
LEFT JOIN Tabla_B B
ON A.pk = B.pk
```

3. Right Join

Esta consulta retorna todas las filas de la tabla B y ademas si hay filas en la tabla A que coinciden también va a traer estas filas de la tabla A.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
RIGHT JOIN Tabla_B B
ON A.pk = B.pk
```

4. Outer Join

Este join retorna TODAS las filas de las dos tablas. Hace la union entre las filas que coinciden entre la tabla A y la tabla B.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
FULL OUTER JOIN Tabla_B B
ON A.pk = B.pk
```

5. Left excluding join

Esta consulta retorna todas las filas de la tabla de la izquierda, es decir la tabla A que no tienen ninguna coincidencia con la tabla de la derecha, es decir la tabla B.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
LEFT JOIN Tabla_B B
ON A.pk = B.pk
WHERE B.pk IS NULL
```

6. Right Excluding join

Esta consulta retorna todas las filas de la tabla de la derecha, es decir la tabla B que no tienen coincidencias en la tabla de la izquierda, es decir la tabla A.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <columna_1> , <columna_2>,  <columna_3> ... <columna_n>
FROM Tabla_A A
RIGHT JOIN Tabla_B B
ON A.pk = B.pk
WHERE A.pk IS NULL
```

7. Outer excluding join

Esta consulta retorna todas las filas de la tabla de la izquierda, tabla A, y todas las filas de la tabla de la derecha, tabla B que no coinciden.
Esto lo podemos implementar de esta forma cuando estemos escribiendo las consultas:

```
SELECT <select_list>
FROM Table_A A
FULL OUTER JOIN Table_B B
ON A.Key = B.Key
WHERE A.Key IS NULL OR B.Key IS NULL
```

# UPDATE

Modifica tuplas.

- Modificar una tupla: `UPDATE nombreTabla SET [Columna = valor,...] WHERE [condicion] LIMIT [numeroDeTuplasAActualizarPorSeguridad]`

# DELETE

Elimina tuplas.

- Vaciar la tabla: `DELETE FROM nombreTabla`
- Eliminar una tupla: `DELETE FROM nombreTabla WHERE [condicion] LIMIT [numeroDeTuplasABorrarPorSeguridad]`
