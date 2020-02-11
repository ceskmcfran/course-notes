# If-else

El **if/else** ejecuta una sentencia si una condición especificada es evaluada como **verdadera**. Si la condición es evaluada como **falsa**, otra sentencia puede ser ejecutada.
La sintaxis básica es:

```
  if(condicion){
        //Codigo al cumplir condicion
  }else if(condicion){
        //Codigo al cumplir condicion
  }else{
        //Codigo al No cumplirse
  }
```

Puede utilizarse la sintaxis corta `expr1 ? expr2 : expr3`

# Switch y Case

**Switch/Case** es una estructura de control utilizada para la toma de decisiones múltiples en las que se **evalúa un valor** y realiza un **set de acciones** dependiendo de cuál es el valor.
Ejemplo:

```
switch(valor) {
   case expresion1: {
      // acciones;
   }
   break;
   case expresion2: {
      //acciones;
   }
   break;

   default: {
      //acciones si no aplican las demás;
   }
   break;
}
```

# For

El **for** es una estructura de control en la que se indica el número de iteraciones. **El índice inicia desde 0**

La estructura de un ciclo for es:

```
for(inicializador, condicion, incrementar/decrementar){
      //codigo
}
```

El ciclo **for in** recorre el contenido de una lista.

La estructura de un ciclo for in es:

```
List lista = ['a','b','c','d'];
for(Tipo nombreVariable in lista){
      print(nombreVariable);
}
```

El ciclo **forEach** recorre también una lista pero se utiliza como un método

```
List lista = ['a','b','c','d'];
lista.forEach((color) => print(color));
```

# While y do-while

La estructura de control **while** evalúa una sentencia al inicio y luego ejecuta el código. La sintaxis es:

```
while(i <= 10){
    print('Valor actual $i');
}
```

Por otro lado **do/while** primero se ejecuta y luego evalúa si continuar.

```
do {
    print('Valor actual $i');
} while(i <= 10)
```

# Break, Continue y etiquetas

**Break**
Se utiliza break para detener el trabajo del ciclo actual.

**Continue**
Con este se detiene el trabajo pero únicamente del bloque de código que continúe inmediatamente después pero el ciclo continuará trabajando.

**Etiquetas**
Lo que hacen estas es continuar la ejecución de tu código desde un punto definido utilizando por una etiqueta (). Se utilizan con la siguiente sintaxis:

```
forExterno: for(int i = 0;  i<3 ; i++){
    forInterno: for(int j = 0;  j<5 ; j++){
        print('$i $j');
        if(i==2 && j==1) continue forInterno;
    }
}
```
