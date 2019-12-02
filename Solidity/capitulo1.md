# Variables de estado
Se guardan permanentemente en el almacenamiento del contrato. **Esto significa que se escriben en la cadena de bloques de Ethereum**. Piensa en ellos como en escribir en una base de datos.
~~~
uint dnaDigits = 16;
int dnaModulus = 10 ** dnaDigits;
~~~


# Tipos
- **uint**: Unsigned Integer (Entero sin signo). Su valor siempre debe ser no-negativo.
- **int**: Integer (Entero).


# Operaciones matemáticas
- **Suma**: `x + y`
- **Resta**: `x - y`
- **Multiplicación**: `x * y`
- **División**: `x / y`
- **Módulo**: `x % y` (por ejemplo, 13 % 5 es 3, ya que al dividir 13 entre 5, 3 es el resto).
- **Exponente**: `x ** 2` (por ejemplo, 5² = 25).


# Estructuras (structs)
Se declaran de la siguiente manera:
~~~
struct Zombie {
  string name;
  uint dna;
}
~~~
Y se inicializan de la siguiente manera:
`Zombie franMuerto = Zombie("fran", "1234516567234");`


# Arrays
Hay dos tipos de arrays dependiendo de la longitud:
- **Fijos**: Tienen longitud fija. `uint[2] fixedArray;`
- **Dinámicos**: Tienen longitud variable por lo que pueden seguir creciendo. `uint[] dynamicArray;`

## Arrays de structs
Además se pueden crear *arrays de structs*. Un *arrays de structs* puede ser muy útil para guardar datos estructurados en tu contrato, como una base de datos.
`Zombie[] arrayDeZombies;`

Para añadir algo al array se utiliza el metodo *push()*:
`arrayDeZombies.push(franMuerto);`

## Arrays Públicos
Puedes declarar un array como público, y Solidity creará automaticamente una función *getter* para acceder a él. La sintaxis es así:
`Zombie[] public arrayDeZombies;`
Los arrays públicos se usan para mostrar algo a otras aplicaciones o contratos.


# Funciones
~~~
function nombreDeFuncion(tipo _parametro, tipo _parametro2, tipo _parametro3) {

}
~~~
Se suele seguir el convenio de llamar a los parametros con un subrayado `_` para diferenciarlos de variables globales

## Visibilidad de las funciones

En Solidity, las funciones son públicas (`public`) por defecto. Esto significa que cualquiera (o cualquier otro contrato) puede llamarla y ejecutar su código.
Es por lo tanto una **buena práctica marcar tus funciones como privadas** (`private`), y solamente hacer públicas aquellas que queramos exponer al mundo exterior.
~~~
function _nombreDeFuncion(tipo _parametro, tipo _parametro2, tipo _parametro3) private {

}
~~~
Se suele seguir el convenio de llamar a las funciones con un subrayado `_` si son privadas.

## Valores de retorno
Para devolver valores en las funciones se declara el tipo de valor que va a retornar la funcion en la declaración de esta y se usa `return` para devolver un valor:
~~~
function sayHello() public returns (string) {
  return "Hola";
}
~~~

Si la función declarada no modifica ningun valor o escribe se suele declarar como `view`. Esto signfica que solo puede ver los datos pero no modificarlos.
~~~
string greeting = "Qué tal viejo!";

function sayHello() public view returns (string) {
  return greeting;
}
~~~

También existen funciones que son como cajas negras. Es decir, no pueden leer el estado de la aplicación, por lo que el valor devuelto depende por completo de los parametros que le pasemos.
Estas funciones son declaradas como `pure`.
~~~
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
~~~
Como podemos ver la diferencia entre `view` y `pure` es que `pure` solo puede trabajar con `a` y `b` que le pasan por parametro, mientras que `view` si puede acceder a `greeting` aunque no se le pase nada por parametro.


# Hasheo
Ethereum incluye una función llamada `keccak256()`, que es una versión de SHA3. Una función hash lo que hace es mapear una cadena de caracteres a un número aleatorio hexadecimal de 256-bits. Un pequeño cambio en la cadena de texto producirá un hash completamente distinto.


# Casteo
~~~
uint8 a = 5;
uint b = 6;
// dará un error porque a * b devuelve un `uint` y no un `uint8`:
uint8 c = a * b;
// debemos de forzar la variable b para que sea convertida a `uint8`
uint8 c = a * uint8(b);
~~~


# Eventos
Los eventos son la forma en la que nuestro contrato comunica que algo sucedió en la cadena de bloques a la interfaz de usuario, el cual puede estar 'escuchando' ciertos eventos y hacer algo cuando sucedan.

Los eventos se declaran poniendo `event`:
~~~
// declara el evento
event IntegersAdded(uint x, uint y, uint z);
~~~
Se dispara el evento declarando `emit`:
`emit IntegersAdded(_x, _y, _z)`


# Bucles FOR
~~~
for (uint i = 1; i <= 10; i++) {
	// Código del bucle
}
~~~
