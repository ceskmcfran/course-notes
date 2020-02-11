# Alias y Fragments
Dentro de GraphQL podemos correr más de una petición a la vez y nombrarlas de distinta manera para poder identificarlas, esto es posible gracias a los **Aliases** o simplemente Alias.

La sintaxis de un Alias es bastante simple:
```graphql
nombreDelAlias: tipoDeDato(argumento: tipo) {
  datos
}
```

Además de los Alias, podemos agrupar campos para ser reutilizados en distintas peticiones gracias a los **Fragments**.
```graphql
fragment NombreFragment on NombreAlias {
  datos
}
```


# Variables
Podemos utilizar variables dentro de las peticiones que hagamos a GraphQL simplemente definiéndolas con la siguiente sintaxis:
```graphql
$nombre: tipo
```


# Enums
Los **Enums** o enumeration types son tipos de datos escalares cuyos valores son configurables. Si definimos un tipo de dato como enum sus valores posibles solamente serán aquellos que se encuentren entre los definidos en el enum.


# Interfaces
Las interfaces son muy importantes y útiles cuando nos encontramos con tipos de datos similares. Una **interfaz** nos permite definir un tipo de dato padre que utilizando la palabra `implements` va a implementar los campos que tenga definidos dentro del tipo de dato que queramos.


# Directivas
Las **directivas** son una instrucción que permite agregar condicionales a nuestras peticiones. Podemos modificar de manera dinámica nuestra query simplemente añadiendo:
```graphql
@include(if: Boolean) {
  datos
}
```
Dentro del schema se puede añadir la directiva `@deprecated` a un campo para indicar que está deprecado en la API


# Unions
**Unions** permite agrupar varios custom types sin importar si tienen algo en común, su sintaxis es la siguiente:

`union SearchResult = CustomType1 | CustomType2 | CustomType3`

Al momento de realizar una query que retorna una union podemos identificar el tipo de dato solicitando el campo `__typename`.