# Inmutabilidad
Despues de implementar un contrato en Ethereum, es **inmutable**, lo que significa que nunca va a ser modificado o actualizado de nuevo.

Si hay un error en el código del contrato, no hay forma de solucionarlo más adelante. Tendrás que decirles a tus usuarios que empiecen a usar otra dirección de contrato inteligente que incluya ese arreglo.

Por este motivo, a veces tiene sentido programar funciones que te permitan actualizar partes de nuestra DApp.


# Contratos Apropiables
**OpenZeppelin** es una librería segura donde hay contratos inteligentes para utilizar en tus propias DApps revisados por la comunidad. El contrato más basico es **Ownable()**
Basicamente Ownable hace lo siguiente:
1. Cuando el contrato ha sido creado, su constructor inicializa owner con msg.sender (la persona que lo ha implementado)
2. Añade el modificador onlyOwner, que puede restringir el acceso a solo el owner en una función.
3. Permite transferir el contrato a un nuevo owner.

onlyOwner es un requisito tan común que la mayoría de las DApps en Solidity suelen empezar con un copia/pega de este contrato Ownable, y después su primer contrato heredaría de él.


# Modificadores de funciones
Los modificadores (**modifier**) son como semifunciones que son usadas para modificar otras funciones, normalmente para comprobar algunos requisitos antes de la ejecución. 

Un modificador de función es igual que una función, pero usa la palabra clave **modifier** en vez de **function**. Pero no puede ser llamado directamente como una función - en vez de eso, podemos añadirle el nombre del modificador al final de la definición de la función para cambiar el comportamiento de ella.
~~~
modifier onlyOwner() {
  require(msg.sender == owner);
  _;
}
~~~
Tendremos que usar **onlyOwner()** de la siguiente manera
~~~
contract MyContract is Ownable {
  event LaughManiacally(string laughter);

  // Mira como se usa `onlyOwner` debajo:
  function likeABoss() external onlyOwner {
    LaughManiacally("Muahahahaha");
  }
}
~~~
Cuando llamas a likeABoss, el código dentro de **onlyOwner** se ejecuta primero. Entonces cuando se encuentra con la sentencia **_;** en **onlyOwner**, vuelve y ejecuta el código dentro de **likeABoss**.

Darle poderes especiales de esta manera al dueño a lo largo del contrato es usualmente necesario, pero puede también ser usado malintencionadamente.
Por ejemplo, el dueño puede añadir una función oculta qué le permita transferirse algo de cualquiera a sí mismo.

### Más sobre modificadores
Un modificador puede también recibir argumentos:
~~~
// Un mapeo para guardar la edad de un usuario(id):
mapping (uint => uint) public age;

// Modificador que requiere que ese usuario sea mayor a cierta edad:
modifier olderThan(uint _age, uint _userId) {
  require (age[_userId] >= _age);
  _;
}

// Tiene que ser mayor a 16 años para conducir un coche (en EEUU, al menos).
// Podemos llamar al modificador de función `olderThan` pasandole argumentos de esta manera:
function driveCar(uint _userId) public olderThan(16, _userId) {
  // La lógica de la función
}
~~~


# GAS
En Solidity, tus usuarios tienen que pagar cada vez que ejecuten una función en tu DApp usando una divisa llamada **gas**. Los usuarios compran gas con **Ether**, así que deben gastar ETH para poder ejecutar funciones en tu DApp.

La cantidad de gas necesaria para ejecutar una función depende en cuán compleja sea la lógica de la misma. Cada operación individual tiene un coste de gas basado aproximadamente en cuantos recursos computacionales se necesitarán para llevarla a cabo.

El total **coste de gas** de tu función es la suma del coste de cada una de sus operaciones.

### ¿Por qué es necesario el gas?
Ethereum es como un ordenador grande, lento, pero extremandamente seguro. Cuando ejecutas una función, cada uno de los nodos de la red necesita ejecutar esa misma función para comprobar su respuesta - miles de nodos verificando cada ejecución de funciones es lo que hace a Ethereum descentralizado, y que sus datos sean inmutables y resistentes a la censura.

Los creadores de Ethereum querian estar seguros de que nadie pudiese obstruir la red con un loop infinito, o acaparar todos los recursos de la red con cálculos intensos. Por eso no hicieron las transacciones gratuitas, y los usuarios tienen que pagar por su poder de computo así como por su espacio en memoria.

Esto no es necesariamente verdadero en las sidechains. Es probable que nunca se ejecute un juego como World of Warcraft directamente en la mainnet de Ethereum - el coste de gas sería excesivamente caro. Pero puede ejecutarse en una sidechain con un algoritmo de consenso diferente.

### Empaquetado struct para ahorrar gas
Normalmente no hay ningún beneficio en usar cualquiera de estos subtipos porque Solidity reserva 256 bits de almacenamiento independientemente del tamaño del uint.
Por ejemplo, usando uint8 en vez de uint (uint256) no te ahorrará nada de gas.

Pero **hay una excepción** para esto: dentro de los struct.

Si tienes varios uints dentro de una estructura, usar un uint de tamaño reducido cuando sea posible permitirá a Solidity empaquetar estas variables para que ocupen menos espacio en memoria.
~~~
struct NormalStruct {
  uint a;
  uint b;
  uint c;
}

struct MiniMe {
  uint32 a;
  uint32 b;
  uint c;
}

// `mini` costará menos gas que `normal` debido al empaquetado de la estructura
NormalStruct normal = NormalStruct(10, 20, 30);
MiniMe mini = MiniMe(10, 20, 30); 
~~~
Querrás también agrupar los tipos de datos que sean iguales (es decir, ponerlos al lado en la estructura) así Solidity podrá minimizar el espacio requerido.
Por ejemplo, una estructura con campos 
`uint c; uint32 a; uint32 b;`
costará menos gas que una estructura con campos
`uint32 a; uint c; uint32 b;`
porque los campos uint32 están agrupados al lado.

### Ahorrando gas con funciones 'VIEW'
Las funciones **view** no cuestan *gas* cuando son llamadas externamente por un usuario.

Esto es debido a que las funciones **view** no cambia nada en la blockchain - solo leen datos. Así que marcar una función con **view** le dice a *web3.js* que solo necesita consultar a tu nodo local de Ethereum para ejecutar la función, y que no necesita crear ninguna transacción en la blockchain.

Si una función **view** es llamada internamente por otra función que no sea **view** en el mismo contrato, esta seguira costando *gas*.
Esto es porque la otra función crea una transacción en Ethereum, y necesita ser verificada por el resto de nodos.
Por lo que las funciones view son gratuitas siempre que sean llamadas externamente.


# Unidades de tiempo
La variable **now** devolverá el actual tiempo unix.
Solidity también contiene **seconds**, **minutes**, **hours**, **days**, **weeks** y **years** como unidades de tiempo. Estos convertirán a un uint la cantidad de segundos que contengan esos números. Es decir 1 minutes son 60, 1 hours son 3600 (60 seconds x 60 minutes), 1 days son 86400 (24 hours x 60 minutes x 60 seconds), etc...


# Pasando estructuras como argumentos
Puedes pasar un puntero **storage** a una estructura como argumento a una función **private** o **internal**.


# Seguridad en funciones Públicas
Una práctica importante de seguridad es examinar todas tus funciones **public** y **external**, y prueba a pensar las maneras en las que los usuarios podrían abusar de ellas. Recuerda - a no ser que estas funciones tengan un modificador como **onlyOwner**, cualquier usuario puede llamarlas y pasarles los datos que quieran.


# Coste de Storage
Una de las operaciones más caras en Solidity es usar **storage** — especialmente la escritura.

Esto es debido a que cada vez que escribes o cambias algún dato, este se guarda permanentemente en la blockchain. ¡Para siempre! Miles de nodos alrededor del mundo necesitan guardar esos datos en sus discos duros, y esa cantidad de datos sigue creciendo a lo largo del tiempo a medida que crece la blockchain.

Para seguir manteniendo los costes bajos, querrás evitar escribir datos en **storage** a no ser que sea absolutemente necesario.
A veces esto implica usar en programación una lógica ineficiente: como volver a construir un array en memoria cada vez que una función es llamada en vez de simplemente guardar ese array en una variable para acceder a sus datos más rápido.

En la mayoría de lenguajes de programación, usar bucles sobre largos conjuntos de datos es costoso.
Pero en Solidity, esta es una manera más barata que usar **storage** si está en una función **external view**, debido a que las funciones **view** no les cuesta a los usuarios nada de gas.


# Arrays en memoria
Puedes usar la palabra clave **memory** con arrays para crear un nuevo arrays dentro de una función sin necesidad de escribir nada en **storage**.
El array solo existirá hasta el final de la llamada de la función, y esto es más barato en cuanto a gas que actualizar un array en **storage** (gratis si está dentro de una función **view** llamada externamente).
