**React** cumple su función como biblioteca ya que para utilizar su código se debe importar. También es un _Framework_ aunque las convenciones de cómo debe ser organizado todo no son estrictas.
En este curso aprenderás las prácticas que la comunidad ha decidido que son buenas.

**React es declarativo**, lo que quiere decir que se le indica qué debe hacer pero no cómo debe hacerse, ahorrando de esta manera muchos pasos.

**JSX** es HTML dentro de Javascript, esto se verá más adelante en detalle.

React está estructurado por **componentes** que son como pequeños bloques de lego que al ser unidos forman aplicaciones de React. Estos componentes pueden tener estilos, ser enlazados a eventos y sus estados pueden ser modificados.

Con React también se tiene la ventaja de que será escrito una sola vez y podrá ser utilizado en aplicaciones web, móviles, entre otras.

**Create-react-app** es una aplicación moderna que se usa desde una línea de comando. Antes de ella se configuraba todo el entorno manualmente lo cual tomaba mucho tiempo.

Pasos para obtenerlo:
Se debe instalar desde la línea de comando usando
`npm install -g create-react-app`

Una vez instalado se crea la carpeta del proyecto con
`create-react-app -nombre del proyecto-`

En este punto se estará instalando React y otras herramientas, también se configurará el entorno usando Webpack.

Una vez se instala todo entra a la carpeta src donde estará todo el código fuente de la aplicación, siendo el más importante index.js que es el punto de entrada a la aplicación.

Finalmente para correr la aplicación se usa el comando
`npm run start`

Otras herramientas:

- **Babel**: Traduce Javascript moderno (JSX) a un Javascript que todos los navegadores puedan interpretar.
- **Eslint**: Lee el código y avisa de errores.
