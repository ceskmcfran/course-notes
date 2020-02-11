# Definición de clases y miembros

Una **clase** es el plano de un objeto, es la descripción del objeto, pero no el objeto, más bien **es una plantilla para crear objetos**.

Todo puede ser descrito como un objeto, con ciertas variables de instancia y métodos, por ejemplo casas, carros, personas, animales, etc.

Se le llama **miembros de una clase** a **todas las variables de instancia y métodos que se existen dentro de ella** y podemos acceder a ellos llamándolos desde un objeto.

```
main(List<String> args) {

  // * Así se declara un objeto.
  Empleado emp = new Empleado();

  emp.id = 1;
  emp.nombre = "Argel";


  if(emp.cumplioHorario()){
    emp.trabajar();
  }


  // * También se puede declarar así, el uso de la palabra reservada "new" es opcional.
  Empleado emp2 = Empleado()
  ..id = 2
  ..nombre = "Pedro"; // ! También existe la notación tipo cascada, para inicializar el objeto con valores para sus miembros.


  emp2.cumplioHorario() ? emp2.trabajar() : print('No se presento a trabajar hoy.');
}

// ? Qué es una clase?
// * Una clase es el plano de un objeto, se puede crear una clase de
// * cualquier cosa, por ejemplo: Casas, Carros, Personas, Animales, etc.

class Empleado{

  //  ? Miembros de una clase
  // * Se le llama miembros de una clase a todas las variables de instancia
  // * y métodos que existen dentro de ella y podemos acceder a ellos llamándolos
  // * desde un objeto.

  var id;
  var nombre;

  bool cumplioHorario(){
    returntrue;
  }

  void trabajar(){
    print("$nombre realizó su trabajo...");
  }
}

```

# Constructores por defecto, por parámetro o nombrados

Los constructores se utilizan para inicializar una clase, son el primer método que se visualiza al instanciar un objeto.

**Constructores por defecto**
El constructor por defecto ya existe cuando se crea una clase y se define creando un método con el mismo nombre de la clase “nombreClase(){…}”

**Constructores con parámetros**
Los constructores con parámetros son aquellos que pueden definir los miembros mediante el constructor.

No puede existir en la misma clase un constructor por defecto y uno con parámetros.

**Constructores nombrados**
También podemos definir constructores con un nombre definido por nosotros y ésto hace que puedan existir múltiples constructores.

```
main(List<String> args) {
  Empleado juan = Empleado();
  Gerente jose = Gerente(103, "José");
  Guardia roberto = Guardia.trabajo(303, "Roberto", false);
}

// ! Existen tres tipos de constructores:

class Empleado{
  var id;
  var nombre;

  // ? Constructores por defecto
  // * Ya existe cuando se crea una clase y se define creando un método
  // * con el mismo nombre de la clase "nombreClase(){}"

  Empleado(){
    print("Contratamos a un empleado.");
  }

  bool cumpleHorario(){
    returntrue;
  }

  void trabajar(){
    print("$nombre realizó su trabajo...");
  }
}

class Gerente{
  var id;
  var nombre;

  // ? Constructores con parámetros
  // * Son constructores que reciben parámetros para ya sea inicializar
  // * sus miembros o para realizar acciones durante la inicializacion
  // * de otras acciones

  Gerente(int id, String nombre){
    this.id = id;
    this.nombre = nombre;
    print("Contratamos a un gerente llamado $nombre y su id es $id");
  }

  // * Otra forma de inicializar parámetros, es:
  // Gerente(this.id, this.nombre);

  bool cumpleHorario(){
    returntrue;
  }

  void trabajar(){
    print("$nombre realizó su trabajo...");
  }
}

class Guardia{
  var id;
  var nombre;
  var trabajo;

  // ? Constructores nombrados.
  // * Tambien podemos definir constructores con un nombre definido por
  // * nosotros y de estos pueden existir múltiples constructores.

  Guardia.trabajo(this.id, this.nombre, this.trabajo){
    if(trabajo){
      print("Contratamos a un guardia de seguridad llamado $nombre y ya hizo su trabajo.");
    }else{
      print("Contratamos a un guardia de seguridad llamado $nombre, pero aun no ha hecho su trabajo.");
    }
  }

  bool cumpleHorario(){
    return trabajo;
  }

  void trabajar(){
    print("$nombre realizó su trabajo...");
  }
}
```

# Metodos Getter y Setter y variables privadas

Para inicializar una variable privada se utiliza la siguiente sitaxis:
`tipo_variables _nombre`

La sintaxis para el Getter es:

```
tipo_variable_retorno get nombre_getter{
    return _variable
}
```

La sintaxis para el Setter es:

```
void set nombre_setter(tipo_variable variable){
    //Codigo del setter
}
```

# Herencia

La **herencia** nos permite adquirir las propiedades de una clase ‘Padre’.

**La clase hijo entonces tiene las propiedades de la clase ‘Padre’** y además tiene sus **propiedades propias**, mismas que heredará a sus hijos.

Por ejemplo **todas las clases heredan por defecto de la clase ‘Object’** ya que en Dart todo es un objeto, por lo tanto todas las clases de Dart comparten algunos miembros.

Se utiliza `super` para utilizar el constructor de la clase Padre en el constructor de la clase Hija

```
main(List<String> args) {
  Frontend dev = Frontend(1, "Sebastián", 9999999, "Reactjs");

  print(
      "El dev ${dev.id} llamado ${dev.name} trabaja con el framework ${dev.framework} y gana \$${dev.salary}.");
}

class Developer{
  int id;
  String name;
  int salary;

  Developer(this.id, this.name, this.salary);

  void calcSalary() => print("This developer earn ${salary * 5.5}.");
}

class Frontend extends Developer{
  String framework;

  Frontend(int id, String name, int salary, Stringthis.framework)
      : super(id, name, salary);
  void skill() =>
      print("He is a Frontend Developer and works with $framework Framework.");
}
```

# Clases abstractas

Una **clase abstracta no puede ser instanciada**, es decir, no se puede crear objetos, aunque puede ser extendida.

Un método abstracto es estructurado, pero no definido, deberá ser sobrescrito (**override**) en el futuro.

```
void main(){
  var fruta=Fruta();
  fruta.imprimir();
  fruta.imprimirPadre();
}

abstract class Alimento{
  var list;
  bool bandera=true;

  void imprimir(){
    print (bandera);
  }
  void imprimirPadre()=>print(list);
}

class Fruta extends Alimento{
  @overridevar list='Sandia';
  @overridevoid imprimir() => print('Valor de bandera es: ${this.bandera}');
}
```

# Interfaces implicitas

Una clase normal puede funcionar como una interfaz a esto de le llama **interfaces implícitas**, éstas se harán implementando múltiples clases utilizando las clases como una interfaz.

Para que la interfaz implícita sea descrita correctamente, la clase **deberá de definir todos los miembros de las clases de las que va a implementar**.

En Dart a esto se le conoce como **mixings**.

´´´
main(List<String> args) {
Cajero cajero = Cajero(1, "Sebastián", 900);
cajero.buenaConducta();
cajero.calcSal();
}

classEmpleado{
int id;
String nombre;
int salario;

Empleado(this.id, this.nombre, this.salario);

void calcSal() => print("El empleado $nombre gana ${salario \* 5} cada mes.");
}

classConducta{
void buenaConducta() => print("El empleado tiene un buen comportamiento");
}

// Una clase en Dart puede extender de una sola clase o clase abstracta
// Una clase en Dart puede implementar más de una clase, las cuales actuan como Interfaces y no necesitan una palabra reservada como las clases abstractas.
classCajeroimplementsEmpleado, Conducta{
int id;
String nombre;
int salario;

Cajero(intthis.id, Stringthis.nombre, intthis.salario);

@override
void calcSal() => print("El empleado $nombre gana ${salario \* 10} cada mes.");

@override
void buenaConducta() => print("El empleado no tiene un buen comportamiento");
}
´´´
