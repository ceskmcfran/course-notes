Las **funciones** son una colección de declaraciones agrupadas para desarrollar una operación, éstas pueden ser **llamadas** y **reutilizadas**.

Una **función** tendrá un tipo (mismo que regresará al utilizarse), un nombre, argumentos e instrucciones y seguirá la siguiente estructura.

```
type functionName([args]){
	//code
	return returnValue;
}
```

**main()** es la función de alto nivel que define el inicio de la aplicación y sigue la siguiente estructura, recuerda que _en web no se requieren los argumentos_.

```
void main(List<String> arguments) {
    //code
}
```

Nota: _En Dart las variables también son objetos, así que las podemos asignar a una variable_.

# Funciones Arrow y Anónimas (Lambda)

Las **funciones de sintaxis corta (Arrow)** son **declaradas en la misma línea** y **sólo pueden tener una expresión**, misma que se declara después de una **flecha** (=>), por ejemplo:

`void functionName(int a, int b) => a + b;`

Las funciones anónimas, también conocidas como **lambda o closures** son similares a las nombradas pero con la diferencia de que no llevan nombre y suelen utilizarse para realizar una **acción dentro de otro proceso,** por ejemplo:

```
  List list=["Rojo","Rosa","Verde"];
    list.forEach((val){
      print(val);
    });
  }
```

# Parámetros requeridos, opcionales, posicionados, nombrados y por defecto

- **Parametros requeridos**: Siempre debemos mandarlo a la función.

  ```
    void parametrosRequeridos(int x, int y) {
      print((x + y));
    }

    parametrosRequeridos(3, 5);
  ```

- **Parametros opcionales**: Mandarlos es opcionales, se escriben con **corchetes** ([]).

  ```
    void parametrosOpcionales(int x, [int y]) {
      print((x + y));
    }

    parametrosOpcionales(3);
  ```

- **Parametros posicionados**: Cuando los mandamos hay que nombrarlos, se escriben con **llaves** ({}).

  ```
    void parametrosOpcionalesNombrados(int x, {int param2: 6}) {
      print((x + y));
    }

    parametrosOpcionalesNombrados(3, param2: 2);
  ```
