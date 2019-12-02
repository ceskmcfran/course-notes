# Payable
Las funciones **payable** son un tipo de función especial que pueden recibir Ether.
Ya que tanto el dinero (Ether), los datos (payload de transacción) y el mismo código de contrato viven en Ethereum, es posible para usted llamar a una función y pagar dinero por el contrato al mismo tiempo.
~~~
contract OnlineStore {
  function buySomething() external payable {
    // Requiere que se asegure que 0.001 ether han sido enviados en la llamada de la función:
    require(msg.value == 0.001 ether);
    // si es así, transferimos algo al que ha pagado:
    transferThing(msg.sender);
  }
}
~~~
**msg.value** es una manera de ver cuanto Ether fue enviado al contrato, y **ether** es una unidad incorporada.

Si una función *no es marcada como payable* y usted intenta enviar Ether a esta, como se hizo anteriormente, la función **rechazará su transacción**.


# Retiros
Luego de enviar Ether a un contrato, este se almacena en la cuenta de Ethereum del contrato y estará atrapado ahí a menos que añada una función para retirar el Ether del contrato:
~~~
contract GetPaid is Ownable {
  function withdraw() external onlyOwner {
    owner.transfer(this.balance);
  }
}
~~~
Puede transferir Ether a una dirección utilizando la función **transfer** y **this.balance** devolverá el balance total almacenado en el contrato.
`Si 100 usuarios han pagado 1 Ether a nuestro contrato, this.balance sería igual a 100 Ether.`


# Generación de números aleatorios MAL HECHA
La mejor fuente de aleatoriedad que tenemos en solidity es la función hash **keccak256**.
~~~
// Genera un numero aleatorio entre 1 y 100;
uint randNonce = 0;
uint random = uint(keccak256(now, msg.sender, randNonce)) % 100;
randNonce++;
uint random2 = uint(keccak256(now, msg.sender, randNonce)) % 100;
~~~
**Este método es vulnerable a ataques de nodos deshonestos**
En Ethereum, cuando llama a una función en un contrato, lo transmite a un nodo o nodos en la red como una transacción. Los nodos en la red luego recolectan un montón de transacciones, intentan ser el primero en resolver el problema de matemática intensamente informático como una "Prueba de Trabajo", para luego publicar ese grupo de transacciones junto con sus Pruebas de Trabajo (PoW) como un bloque para el resto de la red.

Una vez que un nodo ha resuelto la PoW, los otros nodos dejan de intentar resolver la PoW, verifican que las transacciones en la lista de transacciones del otro nodo son válidas, luego aceptan el bloque y pasan a tratar de resolver el próximo bloque.

**Esto hace que nuestra función de números aleatorios sea explotable.**


# Generación de números aleatorios BIEN HECHA
Ya que todos los contenidos de la blockchain son visibles para todos los participantes, este es un problema dificil, y su solución está más allá del rango de este tutorial. Puede leer este hilo de [StackOverflow](https://ethereum.stackexchange.com/questions/191/how-can-i-securely-generate-a-random-number-in-my-smart-contract) para que se haga un idea. Una idea sería utilizar un oráculo para ingresar una función de número aleatorio desde fuera de la blockchain de Ethereum.


