# Tipos de datos
**Strings**: Nos sirven para guardar textos.
**Boolean**: Información cierta o falsa (true y false).
**ObjectId**: Utilizan el tiempo exacto en el que generamos la consulta para siempre generan IDs únicos. Existen en BSON pero no en JSON.
**Date**: Nos sirven para guardar fechas y hacer operaciones de rangos entre ellas.
**Números**: *Doubles, Integers, Integers 64 bits y Decimals.*
**Documentos** Embebidos: Documentos dentro de otros documentos ({}).
**Arrays**: Arreglos o listas de cualquier otro tipo de datos, incluso, de otras listas.


# MongoDB vs SQL
- MongoDB tiene mucha flexibilidad y no nos impone seguir una estructura o esquema bien definido.
- SQL nos impone una estructura bien definida a más no poder; es super no-flexible.
- Con MongoDB es más fácil empezar y añadir nuevas funcionalidades.
- Con SQL es más demorado de empezar porque debemos tener el orden super claro siempre. Todos los elementos deben tener los mismos elementos y todos deben ser del mismo tipo. Si queremos agregar un nuevo campo debemos añadirlo en todas partes con un valor pode defecto, aunque no lo necesitemos.
- Si no seguimos buenas prácticas en MongoDB, vamos a necesitar queries ultra-complejas, demoradas y una visita diaria al psicólogo .
- El orden impuesto de SQL no es por nada. Las queries son fáciles de entender porque todo sigue su orden y tranquilidad. Aunque, implementar nuevas features toma su buen tiempo.

Para mi el ganador es MongoDB siempre y cuando sigamos buenas prácticas desde el principio. Un gran poder conlleva a una gran responsabilidad.


# Esquemas y relaciones
Los **esquemas** son la forma en que organizamos nuestros documentos en nuestras colecciones. MongoDB no impone ningún esquema pero podemos seguir buenas prácticas y estructurar nuestros documentos de forma parecida (no igual) para aprovechar la flexibilidad y escalabilidad de la base de datos sin aumentar la complejidad de nuestras aplicaciones.

Las **relaciones** son la forma en que nuestras entidades o documentos sen encuentran enlazados unos con otros. Por ejemplo: Una carrera tiene multiples cursos y cada curso tiene multiples clases.

### Relaciones entre documentos
Las documentos embebidos nos ayudan a guardar la información en un solo documento y nos ahorra el tiempo que tardamos en consultar diferentes documentos a partir de referencias. Sin embargo, las referencias siguen siendo muy importantes cuando debemos actualizar información en diferentes lugares de forma continua.

- *One to one*: Documentos embebidos
- *One to many*: Documentos embebidos cuando la información no va a cambiar muy frecuentemente y referencias cuando si.

