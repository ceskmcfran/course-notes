# Distribuciones más utilizadas de Linux

Vamos a usar dos distribuciones de Linux: Ubuntu Server en su versión 18.04 y CentOS Server versión 7.

Recuerda que puedes usar cualquier versión para hacer pruebas y estudiar, pero al trabajar con servidores debemos instalar las versiones LTS, ya que incluyen soporte de largo plazo (actualizaciones de software por al menos 5 años).

Recuerda que puedes probar estas distribuciones con una máquina virtual o el proveedor de nube que prefieras (Google, Amazon, Digital Ocean, entre otros).

# Gestión del arbol de directorios

- **pwd**: nos muestra nuestra ubicación actual en el árbol de directorios (Print Working Directory).
- **ls**: nos muestra el contenido de las carpetas de nuestro sistema operativo. Podemos especificar alguna ruta o, por defecto, listar el contenido de la carpeta donde estamos trabajando.
- **cd**: cambiar nuestra ubicación en el árbol de directorios (Change Directory). Usamos dos puntos (..) para referirnos al directorio padre y solo uno (.) para referirnos a nuestro directorio actual.
- **touch**: nos ayuda a crear archivos desde la terminal.
- **mkdir**: nos ayuda a crear carpetas desde la terminal.
- **cp**: nos permite duplicar archivos y carpetas.
- **mv**: cambiar el nombre de nuestros archivos y carpetas.

Recuerda que la terminal de Linux es sensible a la diferencia entre mayúsculas o minúsculas.

# Diferencias entre LESS, CAT, HEAD y TAIL para lectura de archivos

- **cat**: nos permite leer archivos en su totalidad. Muestra un archivo sin paginar
- **less**: nos ayuda a leer el contenido de nuestros archivos por páginas. Nos movemos con las flechas del teclado o la tecla de espacio. Salimos de la lectura del archivo con la letra q. Buscamos palabras específicas escribiendo /palabra. Muestra un archivo paginado. Pulsando “/” y escribiendo una palabra, puedo buscar las coincidencias de la misma en el archivo. Con la tecla “n” me muevo entre coincidencias hacia adelante, y con shift + “n” me muevo entre coincidencias hacia atras. Con espacio cambio de página. Salgo con "q"
- **tail**: nos muestra las últimas 10 líneas de nuestros archivos. Muestra las últimas 10 líneas de un archivo específico. Con la opción “-n” puedo modificar la cantidad de líneas que veo. Con la opción -f puedo poner los cambios en escucha
- **head**: nos muestra las primeras 10 líneas de nuestros archivos. Muestra las primeras 10 lineas de un archivo específico. Con la opción “-n” puedo modificar la cantidad de líneas que veo.
- **man**: Muestra ayuda sobre comandos.

# Interacción con archivos y permisos

Con el comando `ls -l` podemos observar la lista de archivos de nuestro directorio actual con información un poco más detallada. El primer campo nos indica los diferentes permisos para cada archivo o directorio. Por ejemplo: _-rwxrw-r--_.

El primer carácter nos indica si tenemos un archivo (-), enlace simbólico (l) o directorio (d).

Los siguientes caracteres se dividen en grupos de 3: lectura (r), escritura (w) y ejecución (x). El primer grupo son los permisos del usuario que creó ese archivo, el segundo para el grupo al que pertenece este usuario y el tercero para cualquier otro usuario de tu sistema operativo.

Los grupos nos ayudan a darle los mismos permisos a diferentes usuarios sin necesidad de asignarlos a cada uno individualmente. Todos los usuarios que pertenezcan al grupo tendrán los mismos permisos.

Si en vez de estas letras encuentras un guion significa que ese usuario o grupo de usuarios no tiene permiso para esa acción en particular.

Por ejemplo: -rwxrw-r-- nos indica que trabajamos con un archivo. Todos los usuarios del sistema tienen permisos de lectura. El usuario creador y su grupo tienen permiso de escritura. Y solo el usuario creador puede ejecutar el archivo.

También podemos encontrar estos permisos como 3 números del 1 al 7. Estos números son la suma de los 3 caracteres de permisos para cada usuario o grupo.

```
    - = 0
    x = 1
    w = 2
    r = 4
```

Por lo tanto, los permisos de nuestro archivo de ejemplo serían: 7 (1+2+4) 6 (0+2+4) 4 (0+0+4).

Para cambiar los permisos de un archivo o directorio podemos usar el comando `chmod + a quién queremos añadir o quitar los permisos`:

```
    El usuario propietario: u.
    El grupo, g.
    El resto de usuarios, o.
    Para todos, a.
```

Por ejemplo, para añadir permisos de ejecución a nuestro usuario propietario usamos:

`chmod u+x nombre-del-archivo`

También podemos cambiar al usuario propietario del archivo con el comando `chown`.

`sudo chown nuevo-usuario:grupo-usuarios nombre-del-archivo`

# Conociendo las terminales en linux

Las distribuciones de Linux para servidores no incluyen interfaz gráfica, ya que consumen muchos recursos. Esto significa que siempre vamos a trabajar desde la terminal.

Tendremos disponibles 6 terminales virtuales a las que podemos entrar o salir con las teclas `Ctrl + Alt + F(x)` siendo (x) cada uno de los numeros de las teglas F1, F2,.... También podemos usar el comando `chvt`. La séptima terminal es la interfaz gráfica, así que en este caso no disponemos de ella.

Cada usuario activo en nuestro sistema operativo crea una nueva conexión. Podemos ver todas estas conexiones con los comandos `who` y `w` (este último nos da un poco más de información).

Para ver todos los procesos que corren en el sistema podemos usar el comando `ps`. Para filtrar los procesos y ver únicamente las conexiones de los usuarios usamos `ps -ft tty`.

Este comando nos muestra el identificador de cada proceso. Para terminarlo podemos usar el comando `kill -9 PID`.

# Manejo y monitoreo de procesos y recursos del sistema

Para ver todos los procesos que corren en el sistema podemos usar el comando `ps`. Recuerda que puedes ver la documentación de este comando con el comando `man ps`.

El comando `grep` nos ayuda a filtrar el resultado de un comando o archivo dependiendo de las palabras de cada línea. Para esto también vamos a usar el **pipe** (|), un símbolo que nos ayuda a enviar el resultado de un comando a un segundo comando.

Por ejemplo, el comando `ps aux | grep platzi` imprime los procesos activos del sistema y, con ayuda del pipe, envía la lista al comando grep para filtrar el resultado, mostrando únicamente las líneas con la palabra platzi.

`ps`: Muestra los procesos corriendo. Modificadores:
`aux`: Muestra todos los procesos
`jobs`: Al igual que el comando anterior, muestra los procesos. A diferencia de ps, es un comando interno de la terminal
`fg`: Abre un proceso que estaba pausado
`nohup`: Genera un archivo llamado “nohup.out” que muestra toda la información que produjo un proceso
`grep`: Nos ayuda a filtrar el resultado de un comando o el contenido de un archivo dependiendo de las palabras (o incluso expresión regular) que le indiquemos

### Símbolos especiales

"|" Pipe: Envia el standard output de un comando al standard input de otro.
"&" Ampersand: Envia un proceso al background
"./": Ejecuta un archivo

# Monitoreo de recursos del sistema

El comando `top` nos permite interactuar con una interfaz gráfica que nos muestra información específica del sistema operativo: cantidad de usuarios, tareas corriendo o “durmiendo”, identificadores de los procesos, entre otras.

Para ver la información de la CPU podemos usar el comando `cat /proc/cpuinfo | grep "processor"`. Recuerda que Linux hace diferencia entra mayúsculas y minúsculas, pero puedes usar el comando `grep -i` para filtrar sin estas diferencias.

Para ver la información de la memoria podemos usar el comando free o, para que la información sea más fácil de leer, `free -h`. Y para ver el uso del disco duro está el comando `du` o `du -hsc`.

top: Muestra la siguiente información del sistema:

- load average (carga promedio): Provee una representación en números del 1 al número de procesadores que tenga nuestro servidor del uso de los mismos.
- Uso de la memoria
- Cantidad de usuarios
- Uso del CPU
- Procesos
- Etc

`free`: Me muestra información sobre la memoria de mi sistema. Con el modificador -h la información es más legible para un humano
`du`: Muestra información sobre el disco duro. Con el modificador -hsc y un directorio especificado muestra el tamaño de ese directorio
`htop`: Funciona como top pero funciona de forma más intuitiva

### Comandos útiles

`cat /proc/cpuinfo | grep "processor"`: Muestra información sobre el CPU
`sudo ps auxf | sort -nr -k 3 | head -5`: Muestra los 5 procesos que más uso hacen del CPU
`sudo ps auxf | sort -nr -k 4 | head -5`: Muestra los 5 procesos que más uso hacen de la memoria RAM
