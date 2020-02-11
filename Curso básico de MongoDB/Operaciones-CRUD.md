# Bases de datos, Colecciones y Documentos en MongoDB
Las **Bases de Datos** son los contenedores físicos para nuestras colecciones. Cada base de datos tiene un archivo propio en el sistema de archivos de nuestra computadora o servidor y un Cluster puede tener múltiples bases de datos.

- Contenedor físico de colecciones.
- Cada base de datos tiene su archivo propio en el sistema de archivos.
- Un cluster puede tener múltiples bases de datos.


Las **Colecciones** son agrupaciones de documentos. Son equivalentes a las tablas en bases de datos relacionales pero NO nos imponen un esquema o estructura rígida para guardar información.

- Agrupación de documentos.
- Equivalente a una tabla en las bases de datos relacionales.
- No impone un esquema.


Los **Documentos** son registros dentro de las colecciones. Son la unidad básica de MongoDB y son análogos a los objetos JSON pero en realidad son BSON.

- Un registro dentro de una colección.
- Es análogo a un objeto JSON (BSON).
- La unidad básica dentro de MongoDB.

# Operaciones CRUD desde la consola de MongoDB

**Instrucciones y comandos de la clase:**
- Conexión con el cluster de MongoDB Atlas: `mongo "URL DE NUESTRO CLUSTER"`, (recuerda añadir tu IP a la lista de IPs permitidas para no tener problemas en esta parte).
- Listar las bases de datos de nuestro cluster: `show dbs`.
- Seleccionar una base de datos: `use NOMBRE_BD`. Debemos crear por lo menos un documento si la base de datos es nueva porque MongoDB no crea bases de datos vacías.
- Recordar qué base de datos estamos usando: `db`.
- Listar las colecciones de nuestra base de datos: `show collections`.
- Crear una colección (opcional) y añadir un elemento en formato JSON: `db.NOMBRE_COLECCIÓN.insertOne({ ... })`. La base de datos responde true si la operación fue exitosa y crea el campo irrepetible de `_id` si nosotros no lo especificamos.
- Crear una colección (opcional) y añadir algunos elementos en formato JSON: `db.NOMBRE_COLECCIÓN.insertMany([{ ... }, { ... }])`. Recibe un array de elementos y devuelve todos los IDs de los elementos que se crearon correctamente.
- Encontrar elementos en una colección: `db.NOMBRE_COLECCIÓN.find()`. Podemos aplicar filtros si queremos o encontrar solo el primer resultado con el método `findOne()`.
- Listar todos los posibles comandos que podemos ejecutar: `db.NOMBRE_COLECCIÓN.help()`.

**Comparaciones:**
`$eq` -> Matches values that are equal to a specified value.
`$gt` -> Matches values that are greater than a specified value.
`$gte` -> Matches values that are greater than or equal to a specified value.
`$in` -> Matches any of the values specified in an array.
`$lt` -> Matches values that are less than a specified value.
`$lte` -> Matches values that are less than or equal to a specified value.
`$ne` -> Matches all values that are not equal to a specified value.
`$nin` -> Matches none of the values specified in an array.