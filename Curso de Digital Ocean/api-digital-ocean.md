# Conociendo una API

Las **APIs o interfaces para programar aplicaciones** son un conjunto de recursos que ofrece una organización o aplicación para que desarrolladores puedan interactuar con datos, es decir, consultar datos, crearlos, modifícarlos e incluso en algunos casos, eliminarlos.

Las APIs en la web nacieron de la necesidad de compartir datos y recursos entre organizaciones, y hoy en día muchas empresas ofrecen acceso a sus datos mediante APIs, veamos un caso práctico.

Cuando un usuario desea acceder a Platzi para ver contenido lo puede hacer mediante un login de usuario y contraseña, pero también puede autenticarse mediante redes sociales como Facebook o Twitter, y el flujo es el siguiente:

- El usuario presiona en el botón de Twitter.
- Se carga el sitio de Twitter donde el usuario debe iniciar sesión, y si ya tiene una sesión activa se le preguntará si desea autorizar el uso de sus credenciales en la aplicación Platzi.
- El usuario acepta y Twitter envía un token hacia el Platzi.
- En el backend de Platzi se recibe el token adicional con la información del usuario de Twitter.
- Platzi crea una sesión de usuario.

Digital Ocean cuenta con una API que nos permite mediante peticiones HTTP (con los métodos _get, post, put, delete_) realizar operaciones sobre los productos que ellos ofrecen como droplets, volumes, etc.

Es decir, podemos crear un droplet, apagarlo, destruirlo o incluso redimensionarlo mediante el llamado a la API.

En la documentación oficial podremos encontrar más casos de uso, lo único que debemos tener en cuenta es que requerimos de un token de autorización para interactuar con la API y este se obtiene en el panel de control.

# Generar una API Key en Digital Ocean

La **API de Digital Ocean** nos permite automatizar todo lo que hacemos en el panel de control pero usando comandos a través de peticiones http.

**API Key** es un hash que identifica el equipo que se conecta a Digital Ocean.
