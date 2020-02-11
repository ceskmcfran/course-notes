Una de las alternativas que nos permite Digital Ocean para acceder a nuestro droplet es mediante dominios y subdominios. Esto quiere decir que en vez de entrar a nuestro sitio Wordpress mediante una URL con una IP pública, por ejemplo: http://192.34.61.42, lo podemos hacer mediante un dominio como misitiowp.com o un subdominio wordpress.midominio.com
Para utilizar un subdominio en uno de tus droplets necesitas tener un dominio, lo puedes adquirir con algún proveedor como name.com, namecheap o google domains.

_Para este tutorial utilizaré esta configuración:_

```
    Nombre droplet: backend
    IP pública: 192.34.61.42
    Subdominio a utilizar: wordpress.aumentada.net
```

1. En el panel de control donde gestionas el dominio (puede ser un Cpanel si tienes un plan de hosting u otro sistema) vas a entrar a la opción de gestión de dominio. Es algo parecido a la siguiente imagen:
2. Crea el subdominio, deja el TTL en 14400 o 3600, esto es básicamente el tiempo que dura el registro antes de que se refresque o actualice en el servidor DNS, seleccionamos que sea de tipo A y agregamos la IP pública del droplet al final, finalmente presionamos el botón añadir registro.
3. Regresa al panel de control de Digital Ocean, en la opción de la izquierda en el menú Manage, dirígete a la opción Networking, y selecciona la pestaña Domains.
4. Agregar el subdominio que previamente creaste y asocialo al proyecto que creaste.
5. Finalmente entramos por el navegador a la URL del subdominio, en este caso http://wordpress.aumentada.net y estarás accediendo al droplet.

Esta es una de las recomendaciones que te doy para gestionar con mayor facilidad tus droplets y sus conexiones con otros servidores. No es obligatorio que hagas este ejercicio, sin embargo es importante que conozcas que puedes realizar este tipo de configuración.
