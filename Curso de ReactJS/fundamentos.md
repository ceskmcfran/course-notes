# ReactDOM.render

**React** y **ReactDOM** trabajarán en conjunto.
 - React como análogo a createElement
 - ReactDOM a appendChild

**ReactDOM.render()** toma dos argumentos: Qué queremos renderizar y dónde lo queremos renderizar.

Siempre que escribas **JSX** es requisito **importar React**.

# JSX
**JSX** es una extensión de JavaScript creada por Facebook para el uso con la biblioteca React. Sirve de preprocesador (como Sass o Stylus a CSS) y transforma el código generado con React a JavaScript.

JSX tiene **su alternativa que es React.createElement** pero es preferible JSX porque es mucho más legible y expresivo. Ambos tienen el mismo poder y la misma capacidad.

**React.createElement** recibe 3 argumentos:

 - El tipo de elemento que estamos creando
 - sus atributos o props
 - y el children que es el contenido.
~~~
Ejemplo:
React.createElement(‘a’, { href: ‘https://platzi.com’ }, ‘Ir a Platzi’);
~~~

En JSX se utilizan las llaves para introducir variables o expresiones de Javascript. Lo que sea que esté adentro se va a evaluar y su resultado se mostrará en pantalla.

Las expresiones pueden ser llamadas a otras funciones, cálculos matemáticos, etc. Si las expresiones son false, 0, null, undefined, entre otros, no se verán

~~~
//----SIN USAR REACT----
/*const element = document.createElement("h1");
element.innerText = "Hello, Titlex.!";

const container = document.getElementById("app");

container.appendChild(element);*/

//-----USANDO REACT-----
import React from "react";
import ReactDOM from "react-dom";

//const name = "Fran";

//---USANDO React.createElement---
/*const element = React.createElement(
  "h1",
  {},
  "Hola Titlex.! con React.createElement"
);
const element = React.createElement(
  "a",
  { href: "https://www.titlex.es" },
  "Hola Titlex.! con React.createElement"
);*/
/*const element = React.createElement("h1", {}, `Hola soy ${name}`);*/

//---USANDO JSX---
//const element = <h1>Hola soy, {name}</h1>;
//const element = <h1>Hola Titlex.!</h1>;
//const element = <h1>Hola tengo, {20 + 3} años</h1>;
const element = (
  <div>
    <h1>Titlex.</h1>
    <p>Con tu título no te la juegues</p>
  </div>
);

    const container = document.getElementById("app");
// ReactDom.render(__qué__, __dónde__)
ReactDOM.render(element, container);
~~~