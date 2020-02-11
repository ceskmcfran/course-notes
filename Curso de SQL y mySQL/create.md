# Crear base de datos

- Crear una base de datos: `CREATE database nombreDatabase;`
- Crear una base de datos si no existe: `CREATE database IF NOT EXISTS nombreDatabase;`
- Mostrar warnings: `SHOW warnings;`
- Eliminar tabla: `drop nombreDeLaTabla;`
- Informacion de la tabla: `describe nombreDeLaTabla` o `desc nombreDeLaTabla` o `show full columns from nombreDeLaTabla`

# Crear tablas

Las tablas se suelen nombrar en plural. Por ejemplo: _books_

- Crear una tabla: `CREATE TABLE books();`
- Crear una tabla si no existe: `CREATE TABLE IF NOT EXISTS books();`

Las tablas necesitan una **columna unica**

```
CREATE TABLE IF NOT EXISTS books(
  book_id INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
  author_id INTEGER UNSIGNED,
  title VARCHAR(100) NOT NULL,
  `year` INTEGER UNSIGNED NOT NULL DEFAULT 1900,
  language VARCHAR(2) NOT NULL DEFAULT 'es' COMMENT 'ISO 639-1 Language',
  cover_url VARCHAR(500),
  price DOUBLE(6,2) NOT NULL DEFAULT 10.0,
  sellable TINYINT(1) DEFAULT 1,
  copies INTEGER NOT NULL DEFAULT 1,
  description TEXT
);
```

```
CREATE TABLE IF NOT EXISTS authors(
  author_id INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  nationality VARCHAR(3)
);
```

```
CREATE TABLE IF NOT EXISTS client(
    client_id INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    birthdate DATETIME,
    gender ENUM('M','F','ND') NOT NULL,
    active TINYINT(1) NOT NULL DEFAULT 1,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ONUPDATE CURRENT_TIMESTAMP
);
```

```
CREATE TABLE IF NOT EXISTS operation(
    operation_id INTEGER UNSIGNED PRIMARY KEY AUTO_INCREMENT,
    operation_type ENUM('BOOK LOAN','BOOK RETURN','SALE') NOTNULL,
    book_id INTEGER NOT NULL,
    client_id INTEGER NOT NULL,
    active TINYINT(1) NOT NULL DEFAULT 1,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ONUPDATE CURRENT_TIMESTAMP,
    operation_reference INTEGER,
    finished TINYINT(1) NOT NULL DEFAULT
);
```

En caso de auto incrementar una columna, si se borra una tupla, el siguiente número no sustituirá al borrado. Esto quiere decir que la última tupla no tiene por qué reflejar la cardinalidad de la tabla (número total de tuplas).

Es muy buena práctica (si cumple con los marcos legales de la app) no borrar las tuplas sino desactivarlas mediante una columna `active TINYINT(1) NOT NULL DEFAULT 1`.

# Tipos de columnas

- **INTEGER**: Es un entero,Ocupa 4 bytes.
- **AUTO_INCREMENT**: Hace enteros que se auto incrementan, se meten a una dupla y detecta el numero para hacerlo crecer automáticamente. Al borrar un dato de MYSQL no lo nota y sigue aumentando números, EJEMPLO 1 2 4, si se elimina el 3 no le importa y sigue contando.
- **UNSIGNED**: hace que un entero sea positivo o negativo o solo positivo. (perdón no lo comprendí bien).
- **TINYINT**: Ocupa 1 byte.
- **SMALLINT**: Ocupa 2 byes.
- **Varchar**: Tu le tienes que indicar el numero de caracteres a almacenar de texto.EJEMPLO VARCHAR(2) SI.
- **NOT NULL**: Es decirle a MYSQL que no almacene algo ,algo nulo es que no existe información, en otras palabras es nada.
- **Year**: 10/11/1900
- **DEFAULT**: Es que no le mando información por defecto debe poner el valor que se agrega después del mismo.
- **COMMENT**: Comentario a la columna, que solo se ve al revisar el código.
- **DOUBLE**: Almacena los números enteros y los decimales. \*DOUBLE (6,2) esto hace que de los 6 números que le estamos diciendo 2 de ellos los use solo para decimales.
- **FLOAT**: Es un numero que esta almacenando hasta 6 decimales, es para cálculos precisos.
- **TEXT**: Es meter tanto como se pueda. EJEMPLO Descripción de un libro
