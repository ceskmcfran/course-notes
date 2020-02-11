# Una conexión ssh:

`ssh -i [llave local] [usuario]@[ip]`

Por ejemplo:

`ssh -i ~/.ssh/platzi.pem ubuntu@54.196.172.97`

*Para crear una configuración de conexión ssh para acceder más rápido:*

1- Crear archivo config en ruta ~/.ssh/ que debe contener lo siguiente por cada conexión que se quiera tener:

`Host [nombre para identificar después]`
`HostName [ip]`
`User [nombre de usuario que se va a usar]`
`IdentityFile [ruta a la llave local]`

*Ejemplo:*
`Host platzi`
`HostName 54.196.172.97`
`User ubuntu`
`IdentityFile ~/.ssh/platzi.pem`

*Se usa de esta forma posteriormente:*

`ssh plazi`

Mucho más corto y simple para usar, sin tener que acordarse de los datos de conexión.

# Manejar conexiones con tmux.

Podemos utilizar tmux para poder tener varias terminales bajo la misma conexión, para esto debemos instalarlo dentro del servidor con:

`sudo apt-get install tmux`

Usamos el comando `tmux` para iniciarlo

Una vez iniciado podemos usar el comando `CTRL + B` y la opción que queramos,

`CTRL + B` y `c` abre una nueva terminal
`CTRL + B` y `n` avanza a la siguiente terminal
`CTRL + B` y `d` Desconecta la sesión
`tmux attach` Conectarse a la sesión de tmux

Recuerda: En Linux todas las carpetas que inician con `.` son carpetas ocultas.
