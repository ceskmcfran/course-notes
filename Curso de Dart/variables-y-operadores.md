# Variables: Números (int, double), Strings y booleanos

Las **variables** son espacios reservados en la memoria que pueden **cambiar de contenido** a lo largo de la ejecución de un programa

Para **declarar** una variable podemos utilizar la palabra reservada var, seguido del nombre de la variable o también podemos escribir el tipo de variable (int, double, String y bool) seguido del nombre de la variable.

En Dart tenemos los **tipos básicos** de variables que encontramos en casi todos los lenguajes tales como **int, double, String y bool** y funcionan de la siguiente manera:

- **int** son valores numéricos enteros que no aceptan punto decimal,
- **double** son valores numéricos decimales que tienen punto decimal,
- **String** son cadenas de caracteres que aceptan textos,
- **bool** son constantes en tiempo de compilación que permiten valores verdaderos (true) o falsos (false).

Las variables de tipo **dynamic** aceptarán cualquier tipo de variable y cambiarán según la necesidad.

Se utilizan las triples comillas simples para textos (respeta los saltos de linea).

Para utilizar símbolos y variables de escape se utilizará una `r` antes de las comillas: `print(r"8197~#234 \n linea 2");`

# Colecciones

Las **colecciones** son objetos de tipo **estructuras de datos** que almacenan diversos elementos, existen 2 tipos de colecciones, las **listas** y los **sets**.

En Dart los arreglos son Objetos ordenados de tipo **List** los cuales almacenan con un índice a cada uno de los elementos, mientras que los **sets** son colecciones que contiene valores únicos (no se pueden repetir) no ordenados (no se pueden recuperar mediante índices).

Una **lista** permitirá agregar los elementos que se desees, mientras que un **set** no permitirá volver a agregar un valor ya existente, pero tampoco mandará un error.

```
  // List estoEsUnaLista; Forma simple de declarar una lista.
  List<String> estoEsUnaLista; // * Se puede declarar una lista de String de esta manera.
  print(estoEsUnaLista); // ! Se prueba que es un objeto, por eso sin inicializarse, su valor es null.

  estoEsUnaLista = []; // ! Los corchetes sin contenido, simbolizan que ya se inicializó la lista, pero sin embargo no tiene ningún valor asignado.
  print(estoEsUnaLista); // ? Ya no es nulo.

  estoEsUnaLista = ['Amarillo', 'Azul'];
  print(estoEsUnaLista); // ? Ahora imprime su contenido.

  estoEsUnaLista.add("Rojo"); // ! Este es un método para agregar contenido nuevo a la lista sin sobreescribirla.
                              // ? Se remarca también que se pueden usar comillas simples '' o comillas dobles ""

  print(estoEsUnaLista); // * Tiene nuevo contenido.

  estoEsUnaLista.removeLast(); // ! Con este método, se elimina el último valor en la lista
  print(estoEsUnaLista); // ? Ya no está en la lista "Rojo".

  List<String> otraLista = ['Negro', 'Blanco']; // * Se pueden inicializar las listas al ser declaradas.
  print(otraLista); // * Contiene sus valores de inicialización

  estoEsUnaLista.addAll(otraLista); // ! De esta forma, estamos agregándole a la primera Lista, los valores de la segunda Lista.
  print(estoEsUnaLista); // ? Se puede ver los nuevos valores de la primera lista.

  estoEsUnaLista.removeAt(1); // ! Este es un método para eliminar objetos de una lista en un punto específico, para determinar cúal queremos borrar, usamos su index.
  print(estoEsUnaLista); // ? Se borró el color en el index 1 (segunda posición, debido a que la primera posición es el index 0).

  // * Set
  // * En este tipo de colección un elemento solo puede existir una vez.
  // * Esta no regresará en el mismo orden y por este motivo no se puede pedir por index.

  Set estoEsUnSet; // * Así se puede declarar un set
  print(estoEsUnSet); // ! Prueba de nuevo, que sin inicialización, su valor es nulo.

  estoEsUnSet = Set.from(['Carlos','Diego', 'Emmanuel', 'Johan']); // ! Inicializamos un Set, agregándole datos de una Lista.
  print(estoEsUnSet); // ? Se muestra el contenido del Set.

  estoEsUnSet.add('Paco'); // * Agregamos contenido igual que en una Lista, comparten este método.
  print(estoEsUnSet); // ? Ahora Paco forma parte del Set.

  estoEsUnSet.remove('Diego'); // ! Esta es la forma de eliminar contenido de un Set, podemos hacerlo específicando exctamente que queremos que se elimine de él.
  print(estoEsUnSet); // ? Diego ya no está más en el Set.
```

# Diccionarios

Los **Maps**, también llamadas **Hash** o **Diccionarios** son objetos que tienen una **asociación entre llaves y valores**.
Las llaves de los **Maps** deben ser únicas.

Se inicializan de la siguiente manera: `Map<tipo_variable_key, tipo_variable_value> map;`

```
  Map estoEsUnMapa; // ! Esto es una declaración de un objeto tipo Map
  estoEsUnMapa = {1:'Rojo', 2:'Verde'}; // ? La declaración es diferente a las colecciones,
  // ? debe ser realizada entre llaves {} y debe asignársele una llave a cada valor.

  print(estoEsUnMapa); // * He aquí su impresión, y se visualiza igual de cómo se declara.

  Map<int, dynamic> estoEsUnMapaDinamico; // ! Con esta sintaxis, podemos definir cual será la llave int:dynamic y cual será el valor almacenado.
  // ! En este caso, al ser dinámico el valor asignado, puede tomar muchos tipos de valores.

  estoEsUnMapaDinamico = {1:'Uno', 2:2, 3:3.124}; // ! Prueba de lo anterior dicho.
  estoEsUnMapaDinamico[4] = true; // ? Otra forma de agregar contenido a un mapa.

  print(estoEsUnMapaDinamico); // * Visualización de su contenido

  estoEsUnMapaDinamico.remove(3); // ! Eliminamos un valor, dándole a este métodos u llave.

  print(estoEsUnMapaDinamico); // * Visualizamos.

  bool estaVacioElMapa = estoEsUnMapaDinamico.isEmpty; // * Método para comprobar si el mapa está vacio
  int longitud = estoEsUnMapaDinamico.length; // * Método para comprobar la longitud del mapa.

  print("Está vacio el mapa? : $estaVacioElMapa, cual es su longitud? : $longitud"); // ! Prueba de lo anterior mencionado.

```

# Final y Const

Las variables de tipo **const** y **final** sólo pueden ser _declaradas al mismo tiempo de ser creadas_, su diferencia mayor es que **final es inicializada al momento de usarse**, mientras **const al momento de escribirse**.

```
  final nombre = "Angel";
  final String otroNombre = "Arturo";

  const nombreConst = 23;
```

# Operadores

Los operadores utilizados en Dart son los siguientes:

Unario PostExpr
`expr++ expr-- () [] . ?.`

Unario PreExpr
`-expr !expr ~expr ++expr --expr`

Multiplicativo
`* / % ~/`

Adición
`+ -`

Shift
`<< >>`

Bitwise
`& ^ |`

Relacional y tipo prueba
`>= > <= < as is is!`

Igualdad
`== !=`

Lógicos
`&& ||`

Si Nulo
`??`

Condicional
`expr1 ? expr2 : expr3`

Cascada
`..`

Asignación
`*= /= ~/= %= += -= <<= >>= &= ^= |= ??=`

- Suma ( +)
- Resta ( - )
- -expr Unario menos también conocido como negación (invierte el signo de la expresión)
- Multiplicación
- / División
- ~/ Divide, regresando el valor entero
- % regresa el restante del entero en una división (modulo)
