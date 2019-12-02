# Direcciones
La blockchain de Ethereum está creada por cuentas, que podrían ser como cuentas bancarias. Una cuenta tiene un balance de Ether (la divisa utilizada en la blockchain de Ethereum), y puedes recibir pagos en Ether de otras cuentas, de la misma manera que tu cuenta bancaria puede hacer transferencias a otras cuentas bancarias.

Cada cuenta tiene una **dirección**, que sería como el número de la cuenta bancaria. Es un identificador único que apuntado a una cuenta, y se asemejaría a algo así:
`0x0cE446255506E92DF41614C46F1d6df9Cc969183`

**Una direccion está asociada a un usuario específico (o un contrato inteligente).**

## Mapping
Los mapeos son otra forma de organizar los datos en Solidity. Un mapeo es esencialmente una asociación valor-clave para guardar y ver datos. 
~~~
mapping (uint => address) public zombieToOwner;  // Mapea un zombie a una cuenta, el zombie es la clave y la cuenta es el valor.
mapping (address => uint) ownerZombieCount;  // Mapea una cuenta a un numero de zombies
~~~

## msg.sender
En Solidity, hay una serie de variables globales que están disponibles para todas las funciones. Una de estas es **msg.sender**, que hace referencia a la dirección de la persona (o el contrato inteligente) que ha llamado a esa función.
~~~
zombieToOwner[id] = msg.sender;  // Asocia una id a la cuenta de la persona (dirección) que llama a la función.
ownerZombieCount[msg.sender]++;  // Incrementa el contandor de Zombies de la persona (dirección) que llama a la función.
~~~

## require
**require** hace que la función lanze un error y pare de ejecutarse si la condición no es verdadera. Es como un *if* pero que hace que salte un error
~~~
require(ownerZombieCount[msg.sender] == 0);  // Si el contandor de Zombies de la persona (dirección) que llama a la función es igual a 0 sigue ejecutando el resto del código, sino lanza error.
/*Resto del codigo...*/
~~~
**assert** es similar a **require**, donde lanzará un error si es falso. La diferencia entre **assert** y **require** es que require devolverá al usuario el resto del gas cuando la función falle, mientras que assert no lo hará.

Por lo tanto, la mayor parte del tiempo deseará utilizar `require` en su código; `assert` se usará normalmente sólo cuando algo ha ido terriblemente mal con el código (como un desbordamiento en `uint`)


# Herencia
Se utiliza la palabra clave **is**
~~~
contract Doge {
  function catchphrase() public returns (string) {
    return "So Wow CryptoDoge";
  }
}

contract BabyDoge is Doge {
  function anotherCatchphrase() public returns (string) {
    return "Such Moon BabyDoge";
  }
}
~~~
**EN SOLIDITY ESTÁ PERMITIDA LA HERENCIA MÚLTIPLE**


# Importar contratos
Cuando tienes multiples archivos y quieres importar uno dentro de otro, Solidity usa la palabra clave **import**
`import "./someothercontract.sol";`


# Storage vs Memory
En Solidity, hay dos sitios donde puedes guardar variables - en **storage** y en **memory**.

**Storage** se refiere a las variables guardadas permanentemente en la blockchain.
Las variables de tipo **memory** son temporales, y son borradas en lo que una función externa llama a tu contrato.
Piensa que es como el disco duro vs la RAM de tu ordenador.

La mayoría del tiempo no necesitas usar estas palabras clave ya que Solidity las controla por defecto.
Las **variables de estado** (variables declaradas fuera de las funciones) son por defecto del tipo **storage** y son guardadas permanentemente en la blockchain, mientras que las **variables declaradas dentro de las funciones** son por defecto del tipo **memory** y desaparecerán una vez la llamada a la función haya terminado.

Hay momentos en los que necesitas usar estas palabras clave, concretamente cuando estes trabajando con structs y arrays dentro de las funciones.


# Visibilidad de las funciones II
Si se intenta llamar a una funcion privada desde otro contrato retornará error.

Además de **public** y **private**, Solidity tiene dos tipos de visibilidad más para las funciones: **internal** y **external**.

**internal** es lo mismo que **private**, a excepción de que es también accesible desde otros contratos que hereden de este.

**external** es parecido a **public**, a excepción que estas funciones SOLO puedes ser llamadas desde fuera del contrato — no pueden ser llamadas por otras funciones dentro de ese contrato.


# Interfaces
Para que nuestro contrato pueda hablar a otro contrato de la blockchain que no poseemos, necesitamos definir una **interfaz**.
~~~
/*Tenemos este contrato*/
contract LuckyNumber {
  mapping(address => uint) numbers;

  function setNum(uint _num) public {
    numbers[msg.sender] = _num;
  }

  function getNum(address _myAddress) public view returns (uint) {
    return numbers[_myAddress];
  }
}
~~~
~~~
/*Vamos a utilizar una interfaz para acceder a getNum del contrato anterior.*/
contract NumberInterface {
  function getNum(address _myAddress) public view returns (uint);
}
~~~
Primero, solo declaramos las funciones con las que queremos interactuar y no mencionamos ninguna otra función o variables de estado.
Segundo, no definimos el cuerpo de la función. En vez de usar las llaves (`{ }`), solamente terminaremos la función añadiendo un punto y coma al final de la declaración (`;`).
Sería como definir el esqueleto del contrato. Así es como conoce el compilador a las interfaces.
Incluyendo esta interfaz en el código de tu dapp nuestro contrato sabe como son las funciones de otro contrato, como llamarlas, y que tipo de respuesta recibiremos.

Para usar las interfaces lo haremos de la siguiente manera:
~~~
contract MyContract {
  address NumberInterfaceAddress = 0xab38... // La dirección del contrato FavoriteNumber donde hemos hecho la interfaz NumberInterface
  NumberInterface numberContract = NumberInterface(NumberInterfaceAddress)  // Ahora `numberContract` está apuntando al otro contrato

  function someFunction() public {
    // Ahora podemos llamar a `getNum` de ese contrato:
    uint num = numberContract.getNum(msg.sender);
    //...
  }
}
~~~


# Multiples Returns
~~~
// Así es como hacemos múltiples asignaciones:
(a, b, c) = multipleReturns();

// Podemos dejar el resto de campos en blanco si no nos interesan:
(,,c) = multipleReturns();
~~~