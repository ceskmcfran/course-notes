Las aplicaciones que se trabajan en React son llamadas **single page apps**. Esto es posible gracias a React Router que es una librería Open Source****.

**Multi Page Apps**: Cada página implica una petición al servidor. La respuesta usualmente tiene todo el contenido de la página.

**Single Page Apps (SPA)**: Aplicaciones que cargan una sola página de HTML y cualquier actualización la hacen re-escribiendo el HTML que ya tenían.

**React Router (v4)**: Nos da las herramientas para poder hacer SPA fácilmente. Usaremos 4 componentes:

- BrowserRouter: es un componente que debe estar siempre lo más arriba de la aplicación. Todo lo que esté adentro funcionará como una SPA.
- Route: Cuando hay un match con el +path+, se hace render del +component+. El component va a recibir tres props: match, history, location.
- Switch: Dentro de Switch solamente van elementos de Route. Switch se asegura que solamente un Route se renderize.
- Link: Toma el lugar del elemento `<a>`, evita que se recargue la página completamente y actualiza la URL. Link internamente tiene un elemento pero va a interceptar el clic para navegar de manera interna sin refrescar toda la página.

Para instalar React Router lo hacemos desde la terminal con `npm install react-router`. Como es importante usar exactamente la misma versión, del `package.json` en “dependencies” se quita lo que está delante del 4.

# React Fragment

React.Fragment es la herramienta que te ayudará a renderizar varios componentes y/o elementos sin necesidad de colocar un div o cualquier otro elemento de HTML para renderizar sus hijos. Al usar esta característica de React podremos renderizar un código más limpio y legible, ya que React.Fragment no se renderiza en el navegador.

- El 404 es la ruta que se renderizará cuando ninguna otra coincida con la dirección ingresada.

Otra forma de hacer que todas tus URL’s que no existan sean redirigidas a tu componente de 404 sería de la siguiente forma:
~~~
import { Redirect, Route } from "react-router-dom";

~~~

Como podemos observar llamamos a nuestro componente 404 y luego utilizamos Redirect, el cual es un componente de React Router para hacer redirecciones; en este caso hacemos que todas las URL’s que no correspondan a alguna que hayamos declarado, sean redirigidas a MiComponente404.