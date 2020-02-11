# La consola de MySQL

- Para conectarse: `mysql -u root -h localhost -p`
- Mostrar las bases de datos: `show databases;`
- Usar una base de datos: `use NombreDatabase;`
- Mostrar tablas: `show tables;`
- Ver que DB está seleccionada: `select database();`

# Qué son las bases de datos

Una **base de datos** nos permite almacenar datos y relaciones entre datos para que podamos convertirlos en información.

# Tablas por defecto

Dos tipos de tablas por defecto en MySQL:

- **MyISAM**: directa, sencilla, más rápida y las transacciones son completamente uno a uno:
- **InnoDB**: nueva, recuperable en caso de falla de disco duro pero es un poco más lenta.

En la vida real usamos las tablas con dos propósitos:

- **Catalogo**: crecerá en un orden lento, según las necesidades de la propia BD. (Listado de Usuarios, InnoDB)
- **Operación**: se enfocan a lectura, mayor acceso a disco duro. (Prestamos de libros, MyISAM).
