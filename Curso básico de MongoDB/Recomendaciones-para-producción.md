# Arquitectura y paso a producción
- Usar proveedores cloud con alta disponibilidad: AWS, Google Cloud o Azure son muy buenas opciones
- No te compliques pensando en administración de servidores con MongoDB, servicios como MongoDB Atlas o mlab son muy buenas opciones
- Guardar las credenciales en variables de entorno o archivos de configuración fuera del proyecto
- Asegura que tu cluster se encuentra en la mis región del proveedor que tu aplicación
- Has VPC peering entre la VPC de tu aplicación y la VPC de tu cluster
- Cuida la lista de IPs blancas
- Puedes habilitar la autenticación en dos pasos
- Actualiza constantemente tu versión de MongoDB
- Separa los ambientes de desarrollo, test y producción
- Habilita la opción de almacenamiento encriptado

[14 cosas que quería saber antes de empezar con MongoDB](https://www.infoq.com/articles/Starting-With-MongoDB/)
[Series temporales y Mongo (diseño de esquema)](https://www.mongodb.com/blog/post/time-series-data-and-mongodb-part-2-schema-design-best-practices)
[Best practices](https://www.mongodb.com/collateral/mongodb-performance-best-practices)
[What is MongoDB Sharding and the Best Practices?](https://geekflare.com/mongodb-sharding-best-practices/)
