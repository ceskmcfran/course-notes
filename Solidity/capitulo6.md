# ¿Qué es Web3.js?
Recuerda, que la red de Ethereum está formada por nodos, cada uno de los cuales contiene una copia de la blockchain. Cuando quieres llamar una función de un Contrato Inteligente, necesitas consultar uno de estos nodos y contarle:

1. La dirección del Contrato Inteligente.
2. La función que quieres llamar, y
3. Las variables que quieres pasar a dicha función.

Los nodos de Ethereum solamente hablan un idioma llamado *JSON-RPC*, cuyo lenguaje es bastante difícil de leer para un humano.

Web3.js oculta estas desagradables consultas debajo de la superficie, así que solamente necesitas interactuar con una interfaz JavaScript más fácil de leer.


# Instalación
~~~
// Usando NPM
npm install web3
// Usando Yarn
yarn add web3
// Usando Bower
bower install web3
// ...etc.
~~~
O simplemente puedes descargar el minificado .js archivo desde [github](https://github.com/ethereum/web3.js/blob/1.0/dist/web3.min.js) y después incluirlo en tu proyecto:
`<script language="javascript" type="text/javascript" src="web3.min.js"></script>`


# Web3 "Providers"
Lo primero que necesitamos, es un **Web3 Provider**.
Al configurar un proveedor Web3 en Web3.js le decimos qué nodo deberíamos de estar hablando para manejar nuestras lecturas y escrituras. Es como configurar la URL de un servidor remoto para tus llamadas API en una aplicación web tradicional.

Podrías "hostear" tu propio nodo Ethereum como proveedor. Sin embargo, hay un servicio de terceros que te hace la vida más fácil así que no necesitas mantener tu propio nodo Ethereum para ofrecer tu DApp a tus usuarios — **Infura**.


# Infura
[Infura](https://infura.io/) es un servicio que mantiene un conjunto de nodos Ethereum con una capa de almacenamiento en caché para lecturas rápidas, el cual puedes acceder de forma gratuita a través de su API. Usando Infura comno proveedor, puedes enviar y recibir mensajes de manera confiable desde/hacia la blockchain de Ethereum sin necesidad de mantener y configurar tu propio nodo.
En el siguiente ejemplo, se muestra como se puede configurar Web3 para usar Infura como proveedor Web3:
~~~
var web3 = new Web3(new Web3.providers.WebsocketProvider("wss://mainnet.infura.io/ws"));
~~~


# Metamask
[Metamask](https://metamask.io/) en una extensión de navegador para Chrome y Firefox que permite a los usuarios administrar de forma segura sus cuentas Ethereum y claves privadas, y usar estas cuentas para interactuar con sitios web que usan Web3.js.

Metamask usa los servidores de Infura como un proveedor de web3 pero también le da al usuario la opción de elegir su propio proveedor web3. Así que usando Metamask como proveedor web3, le estás dando al usuario una opción, y es una cosa menos de la que debes preocuparte en tu aplicación.

Metamask inyecto su proveedor web3 en el navegador en el objeto JavaScript global `web3`. Entonces, tu applicación puede verificar si `web3` existe, y si usa `web3.currentProvider` como proveedor.

Abajo hay un ejemplo de una plantilla de código proporcionado por Metamask para saber cómo detectar si nuestro usuario tiene Metamask instalado, y si no lo tiene el navegador le dará un aviso diciendo que necesitará instalar Metamask para usar nuestra aplicación:
~~~
window.addEventListener('load', function() {
  // Aquí se comprueba si Web3 ha sido inyectado por el navegador (Mist/Metamask)
  if (typeof web3 !== 'undefined') {
    // Usar el proveedor Mist/MetaMask
    web3js = new Web3(web3.currentProvider);
  } else {
    // Esto se activará si el usuario no tiene instalado Mist/Metamask. Sería 
    // recomendable avisar al usuario de que debe instalarse Misk/Metamask
    // para poder usar nuestra DApp.
  }
  // Ahora ya puedes iniciar tu DApp y acceder a Web3.js libremente:
  startApp()
})
~~~


# Interactuar con Smart Contracts
Web3.js va a necesitar dos cosas para poder hablar con nuestro contrato inteligente: su **address** (dirección) y su **ABI**.

Una vez que ya tengas la dirección de su contrato y su respectiva ABI, ya podrás crear una instancia en Web3 de la siguiente manera:
~~~
// Instantiate myContract
var myContract = new web3js.eth.Contract(myABI, myContractAddress);
~~~

### Dirección del contrato
Después de terminar de escribir tu contrato inteligente, lo tendrás de compilar y desplegar en Ethereum. Después de implementar tu contrato, obtiene una dirección fija en Ethereum donde vivirá por siempre.

### ABI
Es una representación de los métodos de sus contratos en formato JSON que le dice a Web3.js cómo formatear las llamadas de función de una manera que su contrato lo entienda.
Cuando to compilas tu contrato para implementarlo en Ethereum el compilador de Solidity le dará el ABI, por lo que deberá copiar y guardar esto además de la dirección del contrato.


# Llamar a funciones de un contrato
**call** es usado para funciones `view` and `pure`. Solamente se ejecuta en el nodo local, así que no creará una transacción en la Blockchain.
`myContract.methods.myMethod(123).call()`

**send** creara una transacción y cambiará los datos de la Blockchain. Deberás usar send para cualquier función que **no** sea `view` o `pure`.
`myContract.methods.myMethod(123).send()`

En Solidity,cuando tú declaras una variable `public`, automáticamente se crea una función pública **getter con el mismo nombre**.
~~~
//Llamar al zombie con id 15 del array de zombies "zombies"
zombies(15)
~~~
~~~
//Funcion JS que devolvera el zombie con un "id"
function getZombieDetails(id) {
  return cryptoZombies.methods.zombies(id).call()
}
// Aquí llamamos la función para después con el .then hacer algo con el resultado:
getZombieDetails(15)
.then(function(result) {
  console.log("Zombie 15: " + JSON.stringify(result));
});
~~~


# Integración con Metamask y las cuentas
Podemos ver qué cuenta está actualmente activa en la variable web3 inyectada a través de:
`var userAccount = web3.eth.accounts[0]`

Como los usuarios puede cambiar la cuenta activa en cualquier momento en MetaMask, las apps web necesitan monitorear esta variable para ver si ha cambiado y actualizar la UI en consecuencia.
Podemos hacer esto con una función `setInterval` de la siguiente manera:
~~~
var accountInterval = setInterval(function() {
  // Aquí se comprueba si la cuenta ha sido cambiada por otra
  if (web3.eth.accounts[0] !== userAccount) {
    userAccount = web3.eth.accounts[0];
    // Si es así, llamamos una función para que actualize la UI (puede ser cualquiera como "getZombiesByOwner()")
    updateInterface();
  }
}, 100);
~~~
Lo que hace es verificar cada 100 milisegundos si `userAccount` sigue siendo igual a `web3.eth.accounts[0]`. Si no es así, reasigna `userAccount` a la cuenta actualmente activa, y llama a una función para actualizar la pantalla.


# Enviando transacciones
Hay algunas consideraciones a tener en cuenta con las funciones `send`:
1. `send`ing (enviando) una transacción requiere una `from` address de quien está llamando la función (que se convierte en `msg.sender` en nuestro códio Solidity). Queremos que este sea el usuario de nuestra DApp, para así que MetaMask pueda aparecer en la pantalla para solicitar al usuario que firme la transacción.
2. `send`ing (enviando) cuesta gas.
3. Habrá un retraso significativo desde que el usuario envía una transacción y cuando esa transacción realmente tenga efecto en la Blockchain. Esto se debe a que tenemos que esperar a que la transacción se incluya en un bloque, y el block time para Ethereum es, en promedio, 15 segundos. Si hay muchas transacciones pendientes en Ethereum o si el usuario envía un precio de gas demasiado bajo, nuestra transacción puede tener que esperar varios bloques para ser incluida, y esto podría tomar varios minutos.

Por lo tanto, **necesitaremos lógica en nuestra aplicación para manejar la naturaleza de la asincronía de este código**.
~~~
function createRandomZombie(name) {
  // Como esto va a tardar un poco, vamos a actualizar la UI cuando la transacción
  // se haya completado correctamente.
  $("#txStatus").text("Creating new zombie on the blockchain. This may take a while...");
  // Enviar el texto a nuestro contrato:
  return cryptoZombies.methods.createRandomZombie(name)
  .send({ from: userAccount })
  .on("receipt", function(receipt) {
    $("#txStatus").text("Successfully created " + name + "!");
    // Si la transacción es aceptada por la blockchain, vamos a redibujar la UI
    getZombiesByOwner(userAccount).then(displayZombies);
  })
  .on("error", function(error) {
    // Si la transacción no se produce correctamente, vamos a mostrar por pantalla el error
    $("#txStatus").text(error);
  });
}
~~~
Nuestra función envía una transacción a nuestro proveedor de Web3 y encadena algunos **event listeners**:
- `receipt` se activará cuando la transacción se incluya en un bloque en Ethereum, lo que significa que nuestro zombie ha sido creado y guardado en nuestro contrato.
- `error` se activará si hay un problema que impide que la transacción se incluya en un bloque, como que el usuario no envíe suficiente gas. Queremos informar al usuario en nuestra IU de que la transacción no se realizó para que puedan volver a intentarlo.

Opcionalmente puedes especificar gas y gasPrice cuando llamas send, por ejemplo .send({ from: userAccount, gas: 3000000 }). Si no especificas esto, MetaMask va a permitir al propio usuario a especificar los valores.


# Llamando a funciones payables
La forma de enviar Ether junto con una función es simple, con una advertencia: necesitamos especibicar cuantos **weis** queremos enviar, **y no Ethers**.
**1 Ether = 10^18 weis**
~~~
// Esto va a convertir 1 Eher a Weis
web3js.utils.toWei("1", "ether");
~~~
`cryptoZombies.methods.levelUp(zombieId).send({ from: userAccount, value: web3.utils.toWei("0.001", "ether") })`


# Suscripción a eventos
En Web3.js, puedes suscribirte a un evento, por lo que tu proveedor Web3 desencadena cierta lógica en su código cada vez que se dispara:
~~~
cryptoZombies.events.NewZombie()
.on("data", function(event) {
  let zombie = event.returnValues;
  // Podemos acceder a los 3 objetos de este evento mediante el objeto `event.returnValues`:
  console.log("A new zombie was born!", zombie.zombieId, zombie.name, zombie.dna);
}).on("error", console.error);
~~~

### Usando indexed
Para filtrar eventos y solo escuchar cambios relacionados con el usuario actual, nuestro contrato Solidity tendría que usar la palabra clave `indexed`:
`event Transfer(address indexed _from, address indexed _to, uint256 _tokenId);`

En este caso, porque `_from` y `_to` son **indexed**, eso significa que podemos filtrar por ellos en nuestro event listener de nuestro front-end:
~~~
// Use `filter` to only fire this code when `_to` equals `userAccount`
cryptoZombies.events.Transfer({ filter: { _to: userAccount } })
.on("data", function(event) {
  let data = event.returnValues;
  // ¡El usuario actual acaba de recibir un zombi!
  // Haz algo aquí para actualizar la UI y mostrarlo
}).on("error", console.error);
~~~
El uso de los campos `events` y `indexed` puede ser una práctica bastante útil para escuchar los cambios en tu contrato y reflejarlos en el front-end de tu aplicación.

### Consultando eventos pasados
Podemos consultar eventos pasados usando getPastEvents, y usar los filtros fromBlock y toBlock para darle a Solidity un rango de tiempo para los registros de eventos("block" en este caso, se refiere al número de bloque de Ethereum):
~~~
cryptoZombies.getPastEvents("NewZombie", { fromBlock: 0, toBlock: "latest" })
.then(function(events) {
  // `events` is an array of `event` objects that we can iterate, like we did above
  // Este código nos dará una lista de cada zombie que se haya creado
});
~~~
Como puede usar este método para consultar los registros de eventos desde el principio de los tiempos, esto presenta un caso de uso interesante: Usar eventos como una forma de almacenamiento más económica.

Si recuerdas, guardar datos en la blockchain es una de las operaciones más costosas de Solidity. Pero usar eventos es mucho más barato en términos de gas.

La compensación aquí es que los eventos no son legibles desde el propio contrato inteligente. Pero es un caso de uso importante a tener en cuenta si tiene datos que desea que se registren históricamente en la blockchain para que pueda leerlos desde el front-end de su aplicación.

*Ejemplo*:
~~~
Podríamos usar esto como un registro histórico de batallas de zombies — podríamos crear un evento por cada vez que un zombie ataque a otro y quien gane. El contrato inteligente no necesita estos datos para calcular los resultados futuros, pero son datos útiles para que los usuarios puedan navegar desde el front-end de la aplicación.
~~~