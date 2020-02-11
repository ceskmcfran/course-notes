# Proteger el puerto 22 contra ataques ssh

```
cd /etc/ssh
vim sshd_config
```

Cambiar el puerto del 22 al que se quiera

`systemctl reload sshd`

# Volumes y Power

Para trabajar con **Volumes** a veces es necesario apagar nuestro droplet, para esto tenemos dos opciones:

- **Power Off**: reiniciar por sistema.
- **Power Cycle**:. es un reinicio forzoso, como cuando en un equipo físico presionas el botón de encendido por mucho tiempo. Se pueden perder datos y sólo deber ser usado cuando no tienes más opción.

Montar el volumen:

1. Se formatea (solo la primera vez)
2. Se crea el punto de montaje
3. Se monta el volumen en el punto
4. Se cambia `fstab` para que el volumen se monte tras los reinicios

# Resize (Escalamiento vertical)

Es muy util cuando se prevee que va a haber un gran volumen o picos de tráfico.

Para checkear la memoria de la maquina: `cat /proc/meminfo`

El escalamiento vertical requiere de un apagado de sistema. En caso de querer hacer un resize en caliente es necesario tener 2 droplets haciendo un balanceo de cargas.

# Networking y Firewall

- **Networking**: IPs flotantes, balanceadores de carga, firewall, etc. Esta opción nos permitirá configurar todos los temas relacionados con la red.
- **Firewall**: Es un software del SO que permite manejar y administrar todas las reglas de conexiones entrantes y salientes de nuestro droplet.
- **Floating IP**: Permite añadir más IP publicas a nuestro Droplet.

Una red privada nos servirá para por ejemplo conectar dos droplet a través de esta dirección sin necesidad de que sean accedidas desde internet.
Para configurar la red privada:

1. Copiar la IP privada
2. Logearse por ssh
3. Mirar las interfaces de red del server con `ifconfig`
4. Mirar la configuración de la red que se agregó con `lshw -class network` y copiar la MAC (serial)
5. `nano /etc/netplan/50-cloud-init.yaml`
6. Pegar la siguiente plantilla al final del fichero:

```
        eth1:
            addresses:
            - <IP PRIVADA>/<Mask>
            match:
                macaddress: <MAC (serial)>
            set-name: eth1
```

7. Ejecutar `netplan apply --debug` si está todo bien nos devuelve a la consola.
8. Reiniciar con `reboot`

# Backups y Snapshots

Los **Backups** son copias de seguridad semanales que se hacen el domingo por la noche o lunes por la mañana con costo de un dólar mensual.

Los **Snapshots** son una copia exacta de nuestro droplet, son muy útiles cuando haces cambios en el sistema operativo o la base de datos ya que puedes crear un snapshot para hacer comparaciones con la versión anterior y restaurar de ser necesario.

Al momento de restaurar tienes la opción de hacerlo en un nuevo droplet o directamente en el droplet actual.

# Kernel

En el mundo de los droplets y de Linux tenemos un concepto clave a la hora de manejar los sistemas operativos: el **Kernel** (o núcleo).

El **Kernel** es el corazón del sistema operativo Linux, es el software que se encuentra entre el sistema operativo (SO) y el hardware del equipo. Veamos por qué es tan importante:

- **Gestiona toda la conexión entre el software y el hardware**: Cuando una aplicación le solicita al sistema operativo el acceso a un hardware, como por ejemplo el disco duro para realizar almacenamiento, el SO le solicita a el Kernel el acceso, y este verifica si el recurso físico se puede facilitar a la aplicación.
- El Kernel **es el encargado de gestionar la memoria RAM**, es decir, cuando un programa requiere más memoria para poder cargar más información, debe solicitar dicha gestión al Kernel quien se encarga de verificar cuánta memoria hay y entregar de acuerdo a la disponibilidad, también se encarga de liberar la memoria RAM.
- El Kernel **se encarga también de la gestión del procesador**, es decir, es quien decide qué operaciones tienen más prioridad de ejecución.

En Digital Ocean tenemos la opción de manipular el Kernel de nuestro Droplet, es decir podemos actualizarlo e incluso modifícarlo, sin embargo se recomienda tener mucha precaución, ya que una actualización o modificación fallida puede dañar el Droplet.

# History y Destroy

El **History** es una bitácora de todo lo que ocurre en nuestro droplet. Nos da información como: el evento, su momento de ejecución y duración.

La opción **Destroy** sirve para eliminar droplets que ya no necesitamos y así evitar cargos innecesarios.

# Tags, Recovery y Graphs

Los **Tags** son una forma de agrupar todos los droplets que tenemos, por ejemplo: _DataBase, Backend, Firewall, WebServer etc_.

**Recovery** permite iniciar el droplet a partir de una imagen ISO de recuperación para intentar recuperar un droplet que no inicia.

**Graphs** muestra estadísticas de los recursos de nuestro droplets como son: _CPU RAM, ancho de banda etc_.
