# Schema y types
El **Schema** es la base de una API en GraphQL, es el encargado de describir todos los tipos de información que va a contener.

Ya que termina de correr el comando es momento de añadir la dependencia de GraphQL a nuestro proyecto:
`npm i graphql`

Dentro de GraphQL contamos con **distintos tipos** de datos escalares:
- String
- Int
- Float
- Boolean
- ID


# Queries y Resolvers
Una query permite ejecutar una petición al API, dentro de una query debes indicar la consulta que quieres ejecutar y los campos que deseas obtener. GraphQL te va a devolver la información que solicitaste dentro del objeto data.

El resultado de tu petición no se va a ejecutar de manera mágica, para ello debes definir el objeto resolvers, este objeto va a contener una propiedad del mismo nombre que la query que va a resolver o ejecutar.

[Buenas prácticas de GraphQL](https://medium.com/paypal-engineering/graphql-resolvers-best-practices-cd36fdbcef55)


## Construir un esquema basico y ejecutar una instrucción
~~~
"use strict";

const { graphql, buildSchema } = require("graphql");

// Definiendo el schema
const schema = buildSchema(`
  type Query {
    hello: String
    saludo: String
  }
`);

// Configurar los resolvers
const resolvers = {
  hello: () => {
    return "Hola Mundo";
  },
  saludo: () => {
    return "Que pasa wey";
  }
};

// Ejecutar el query hello
graphql(schema, "{ saludo }", resolvers).then(data => {
  console.log(data);
});
~~~


# Sirviendo el API en la web
Ya viste que nuestra API funciona a través de la línea de comandos, pero necesitamos que está funcione dentro de la web, para ello necesitas de las dependencias de express y un middleware de GraphQL, vamos a instalarlo con el siguiente comando: `npm i express express-graphql`

Para evitar el proceso de detener nuestro servidor cada que ejecutamos un nuevo cambio vamos a utilizar la dependencia de desarrollo Nodemon: `npm i nodemon -D`


# Custom types
Para este proyecto vamos a seguir el estándar de estilos Standard, para instalarlo corremos el siguiente comando:
`npm i standard -D`

GraphQL nos permite configurar nuestros propios tipos de datos, estos deben tener la siguientes sintaxis:
```Javascript
type <Nombre del tipo> {
  propiedad: Tipo de dato
}
```
Dentro de nuestros tipos de datos podemos configurar un campo de un tipo como obligatorio con el signo “!”, quedando por ejemplo:
```Javascript
type Course {
  title: String!
}
```


# Argumentos
Vamos a instalar una nueva dependencia para facilitar el trabajo con GraphQL, vamos a correr el siguiente comando:
`npm i graphql-tools`

Podemos pasar argumentos con distintos tipos de información dentro de las peticiones que hagamos en GraphQL, su sintaxis quedaría de la siguiente manera:
`nombreQuery(campo: tipo): tipo`

Dentro del resolver los argumentos de la petición pasarían como segundo parámetro, el primero es root y el segundo es args.


# Mutations e Inputs
Ya hemos visto cómo consultar información mediante GraphQL, pero en un API también vas a necesitar mandar información para que sea almacenada, dentro de GraphQL esto es posible gracias a la especificación [mutation](https://graphql.org/learn/queries/#mutations).

Un mutation va a requerir de un campo de tipo Input que son como plantillas que le van a indicar qué campos son necesarios para insertar o modificar información.

La sintaxis de una mutation queda de la siguiente manera:
`nombreMutation(input: InputType): tipo`


# Errores
Si sucede un error al momento de realizar una petición GraphQL nos va a retornar un objeto llamado errors que contendrá la información del error y su mensaje. Podemos configurar el mensaje que le retorne al usuario simplemente con una función que lance un error con el mensaje que queramos.