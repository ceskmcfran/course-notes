# Tokens en Ethereum
Un token es básicamente un contrato inteligente que sigue algunas reglas comunes, es decir, implementa un conjunto estándar de funciones que comparten el resto de tokens (contratos).
Por ejemplo `transfer(address _to, uint256 _value)` y `balanceOf(address _owner)`.

Internamente, el contrato inteligente tiene por lo general un mapeo, `mapping(address => uint256) balances`, que realiza un seguimiento de cuánto saldo tiene cada dirección.

Así que, básicamente, un token es sólo un contrato que realiza un seguimiento de quién posee la cantidad de ese token y algunas funciones para que los usuarios puedan transferir sus tokens a otras direcciones.

Dado que todos los tokens ERC20 comparten el mismo conjunto de funciones con los mismos nombres, todos pueden interactuar de la misma manera. Esto significa que si creas una aplicación que es capaz de interactuar con un token de tipo ERC20, también será capaz de interactuar con cualquier token de tipo ERC20. De esta forma, más tokens se pueden añadir fácilmente a su aplicación en el futuro, sin necesidad de tener códigos personalizados por cada uno de los tipos de token ERC20.

### Otros standards de token
Los tokens **ERC20** son realmente geniales porque actúan como si fueran monedas.

Los tokens **ERC721** no son intercambiables entre sí, ya que se supone que cada uno de ellos es totalmente único e indivisible. Solo se pueden intercambiar en unidades completas, y cada uno tiene una ID única.


# ERC721
~~~
contract ERC721 {
  event Transfer(address indexed _from, address indexed _to, uint256 _tokenId);
  event Approval(address indexed _owner, address indexed _approved, uint256 _tokenId);

  function balanceOf(address _owner) public view returns (uint256 _balance);
  function ownerOf(uint256 _tokenId) public view returns (address _owner);
  function transfer(address _to, uint256 _tokenId) public;
  function approve(address _to, uint256 _tokenId) public;
  function takeOwnership(uint256 _tokenId) public;
}
~~~

### BalanceOf
Esta función simplemente recibe una dirección `address`, y devuelve cuántos tokens tiene esa dirección `address`.

### OwnerOf
Esta función recibe un ID de un token y devuelve la dirección de la persona que lo posee.

### Transfer
Transfiere la propiedad de una persona a otra.

### TakeOwnership
Pide la propiedad de un token a otra persona.

### Approve
Aprueba a transferir la propiedad de un token a otra persona cuando se la pidan.

Primero se llama a `approve` y luego la otra persona llama a `takeOwnership`


# Mejoras de seguridad en el contrato: Desbordamientos por exceso (Overflows) y por defecto (Underflows)
Primero, tenemos la palabra clave reservada `library`. Las librerías son similares a los contracts pero con algunas diferencias. Para nuestros propósitos, las librerías nos permiten usar la palabra clave reservada `using`, que automáticamente asocia a todos los métodos de la librería con unos tipos de datos.
~~~
using SafeMath for uint;
// ahora podemos usar los metodos de SafeMath para cualquier uint.
uint test = 2;
test = test.mul(3); // test now equals 6
test = test.add(5); // test now equals 11
~~~

Para mejorar la seguridad de nuestros contratos es conveniente utilizar la librería **SafeMath** en todas las operaciones básicas.


# Comentarios
`// Este es un comentario de una sola línea.`
~~~
/* Este es un comentario 
con múltiples líneas.*/
~~~

El estándar en la comunidad Solidity es usar un formato llamado natspec, que tiene esta apariencia:
~~~
/// @title Un contrato para operaciones matemáticas básicas
/// @author H4XF13LD MORRIS 💯💯😎💯💯
/// @notice Por ahora, este contrato solo añade una función de multiplicar
contract Math {
  /// @notice Multiplica 2 números juntos
  /// @param x el primer uint.
  /// @param y el segundo uint.
  /// @return z el resultado de (x * y)
  /// @dev Esta función actualmente no verifica desbordamientos
  function multiply(uint x, uint y) returns (uint z) {
    // Este es solo un comentario normal, y no será recogido por natspec
    z = x * y;
  }
}
~~~

`@notice` explica a un usuario lo que hace el contrato o la función. `@dev` es para explicar detalles adicionales a los desarrolladores.

`@param` y `@return` son para describir para qué sirve cada parámetro y el valor de retorno de una función.