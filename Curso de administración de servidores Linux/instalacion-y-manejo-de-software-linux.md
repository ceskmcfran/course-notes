# Análisis de los parámetros de red

Una IP es un identificador único para los equipos que están conectados a una red.

Las **IPs Privadas** se utilizan para identificar los dispositivos dentro de una red local. Por ejemplo: los dispositivos conectados en tu casa u oficina.

Las **IPs Públicas** son la que se asignan a cualquier dispositivo conectado a Internet. Por ejemplo: los servidores que alojan tus sitios web, el router que te da acceso a internet, entre otros.

Si tu dispositivo tiene una IP pública significa que puede conectarse a otro que también tenga una. Por esto mismo, no puede haber dos dispositivos con la misma IP pública.

Para encontrar la dirección IP de nuestros dispositivos podemos usar los comandos `ifconfig` en Linux y Mac o `ipconfig` en Windows. También podemos usar el comando `ip a`.

Para ver el nombre/identificador de nuestro equipo en todas las redes podemos usar el comando `hostname`. También podemos ver qué dispositivo nos permite acceso a Internet con el comando `route -n`.

Para identificar las IPs de diferentes dominios podemos usar el comando `nslookup nombredominio.ext`. También podemos usar el comando `curl` para realizar consultas a algún servidor.

# Administración de paquetes acorde a la distribución

Cada distribución de Linux maneja su software de maneras diferentes.

### Red Hat / CentOS / Fedora

Su gestor de paquetes es `.rpm` (Red hat Package Manager). La base de datos de este gestor está localizada en `/var/lib/rpm`.

El comando `rpm -qa` nos permite listar todos los rpms instalados en la máquina. Con `rpm -i nombre-del-paquete.rpm` instalamos los paquetes y con `rpm -e nombre-del-paquete.rpm` los removemos el sistema.

Los paquetes se pueden instalar desde un repositorio sin tener que conocer la ruta del archivo o las dependencias con el comando `yum install nombre-del-paquete`.

También podemos buscar paquetes más específicos con el comando `yum search posible-nombre-del-paquete`.

### Debian / Ubuntu

Su administración de paquetes es `.deb`. Podemos realizar las instalaciones con `dpkg -i nombre-del-paquete.deb` o repositorios `apt`.

Su base de datos está localizada en `/var/lib/dpkg`. Con el comando `dpkg -l listamos` todos los debs instalados en la máquina. Instalamos los paquetes con `dpkg -i nombre-del-paquete` y los removemos del sistema con `dpkg -r nombre-del-paquete`.

Si ya tenemos software configurado podemos usar el comando `dpkg-reconfigure nombre-paquete` para volver a ejecutar el asistente de configuración (si está disponible).

También podemos realizar las instalaciones con el comando `apt install nombre-paquete`y búsquedas de paquetes con `apt search posible-nombre-paquete`.

Antes de actualizar el software de nuestro sistema debemos ejecutar el comando `sudo apt update` para saber qué paquetes pueden actualizarse y desde dónde se realizará la descarga. Luego de esto podremos actualizar todas las herramientas del sistema usando el comando `sudo apt upgrade`.

Recuerda que todo lo que tenga que ver con actualizaciones o modificaciones del sistema operativo necesitará permisos con `sudo`. También necesitarás conexión a Internet.

# Nagios: Desempaquetado, descompresión, compilación e instalación de paquetes

No todo el software que necesitamos se encuentra en los repositorios. Debido a esto, algunas veces debemos descargar el software, realizar un proceso de descompresión y desempaquetado para finalmente instalar la herramienta.

Instalación de algunas herramientas para manejar una base de datos MySQL (recuerda que instalaremos y trabaremos con MySQL en una próxima clase):
`sudo apt install build-essential libgd-dev openssl libssl-dev unzip apache2 php gcc libdbi-perl libdbd-mysql-perl`

Instalación de Nagios:
`wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.4.tar.gz -O nagioscore.tar.gz`

Descomprimir y desempaquetar archivos con tar:
`tar xvzf nagioscore.tar.gz`

Este comando creará una carpeta **nagios-4.4.4**. El nombre de la carpeta puede variar dependiendo de la versión que descargaste. Entrando a esta carpeta podemos ejecutar diferentes archivos y comandos para configurar el software y realizar la instalación.

```
# 1:
sudo ./configure --with-https-conf=/etc/apache2/sites-enabled
# 2:
sudo make all
# 3:
sudo make install
# 4:
sudo make install-init
# 5:
sudo make install-commandmode
# 6:
sudo make install-config
# 7:
sudo make install-webconf
```

Por último, para administrar el servicio de nagios podemos usar el comando `sudo systemctl (status, start, restart, reload, stop, enable, disable, list-dependencies) nagios`.
