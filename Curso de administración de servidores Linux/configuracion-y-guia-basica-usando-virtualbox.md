Vamos a configurar nuestra maquina virtual con virtualbox, utilizaremos la versión 16.04 de Ubuntu.

Recuerda debes tener instalado VirtualBox y dentro del programa debes darle la opción file/import y seleccionar la imagen de Ubuntu que descargaste.

Los datos para iniciar sesión son:

Usuario: ubuntu
Password: ubuntu123

Configurando las interfaces de red

Para poder conectarnos a la maquina virtual, dentro de los settings en la sección de network debes seleccionar bridge adapter y la interface de red que vas a usar.

Podemos primero crear una nueva interface en preferencias/network y creamos una red vboxnet0

Una vez tengas conexión entre las dos máquinas, podemos configurar para poder conectarnos con ssh
Autenticarse

Una opción es iniciar con el usuario ubuntu usando el comando ssh ubuntu@192.168.56.101 recuerda que debes usar la ip que se le asigne al server.

Pero usar usuario y contraseña no es una forma correcta de conectarse a un servidor.
Crear llaves

Dentro del host debemos crear una llave para podernos conectar, lo hacemos con el comando ssh-keygen -b 4096

Al crear esto se crean dos imágenes, una pública y una privada, nunca compartas la privada.

Ahora debemos subir la imagen publica al servidor, esto lo podemos hacer con ssh-copy-id -i .ssh/id_rsa.pub ubuntu@192.168.56.101

Es hora de volver a conectarte al servidor.
Desactivar opción con contraseña

Para poder desactivar el entrar el sistema remoto con contraseña debemos abrir el archivo /etc/ssh/sshd_config, recuerda que requieres permisos de super usuario.

Buscamos la opción PasswordAuthentication y le configuramos el valor no.

Reiniciamos el servicio de ssh con sudo /etc/init.d/ssh restart

-------------------------------------

Comandos utilizados en el vídeo:

    ifconfig: Permite ver las network interfaces

    ifdown [network interface]: Desactiva dicha interface

    ifup [network interface]: Activa dicha interface
    Los binarios se encuentran en: /sbin/if…

    ping [ip address]: Permite realizar ping a dicha IP

    ssh [ip address] o ssh [username]@[ip address]: Permite conectarse por medio de SSH a un servidor (ubicado en dicha IP)

    ssh-keygen -t rsa -b 4096 -C [your_email@example.com]: Permite generar una llave ssh tipo rsa

    ssh-copy-id -i [ssh-key address].pub [username]@[ip address]: Envia una copia de la llave ssh “pública” a un servidor (ubicado en dicha IP)
    En el servidor se crea una carpeta en el home (.ssh/authorized_keys); donde almacena la llave ssh “pública”.

    sudo vim /etc/ssh/sshd_config: En este archivo de configuración se debe editar la opción para que la única forma de conectarse al servidor sea por medio de ssh y no por medio de username y password.
    La opción a editar es: PasswordAuthentication [no], colocar no; para evitar la autenticación por medio de username y password

    sudo /etc/init.d/ssh restart: Reinicia el servicio ssh; y aplica los cambios


