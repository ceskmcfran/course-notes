# Qué es Digital Ocean

La “nube” son sólo servicios a los que tienes acceso a través de Internet, existen tres categorías:

- SaaS: Software as a Service.
- PaaS: Platform as a Service.
- IaaS: Infrastructure as a Service.

Digital Ocean es una solución de infraestructura muy bien documentada que entra en la categoría IaaS y tiene precios competitivos además de permitir métodos de pago como PayPal.

**Software-as-a-Service (SaaS):**
Todo el desarrollo, mantenimiento, actualizaciones, copias de seguridad es responsabilidad del proveedor, es decir, si el servicio se cae es responsabilidad del proveedor volver a hacer que funcione.
Ejemplos : El Webmail de Gmail, Google Docs, Salesforce, Dropbox

**Platform-as-a-Service (PaaS):**
Nuestra única preocupación es la construcción de nuestra aplicación, ya que la infraestructura nos la da la plataforma, pero también debemos centrarnos en que estén lo mejor optimizadas posibles para consumir menos recursos posibles.
Ejemplos: Google App Engine, Heroku

**Infraestructure-as-a-Service (IaaS):**
Tendremos mucho más control que con PaaS, pero deberemos encargarnos de la gestión de infraestructura,escalar nuestras aplicaciones según nuestras necesidades, además de preparar todo el entorno en las maquinas.
Ejemplos: Amazon Web Service (AWS)

# Cuándo usar Digital Ocean

Existen varias opciones para llevar nuestro proyecto a Internet:

- Hosting gratis: no se puede administrar el hardware, sirve para aproximadamente una decena de usuarios, está muy limitada y puede contener publicidad.
- Shared Hosting: no se puede administrar el hardware, tienen un poco más de potencia pero normalmente vienen limitados a la arquitectura LAMP (Linux, Apache, MySQL y PHP).
- VPS (Virtual Private Server): es un dispositivo virtual donde si puedes administrar el hardware (de forma virtual), sirve para miles de usuarios o más al mes.
- Dedicado: maquina física donde todos los recursos están dedicados para nuestra aplicación con la desventaja de que no es tan fácil aumentar recursos cómo almacenamiento, memoria RAM, etc. Sirve para miles o cientos de miles de usuarios al mes.
- Cloud (PaaS/IaaS): solución de tipo VPS donde podemos administrar nuestros recursos de hardware, tener múltiples servidores como: servidores web, servidores de bases de datos, balanceadores de carga, firewalls, etc. Aquí entra Digital Ocean.
- Datacenter: cuando ya se llega a millones de usuarios esto es una opción pero tiende a ser muy costosa.

Digital Ocean es útil cuando necesitamos una solución de VPS, que permita administrar recursos de hardware e ir creciendo a medida de forma fácil y rápida.

# ¿Qué es un DROPLET?

**Droplet** es la forma en la que Digital Ocean llama a sus **VPS**, tienen la ventaja de utilizar discos de tipo SSD con lecturas y escrituras más rápidas que los discos mecánicos convencionales.

# Storage: Volumes y Spaces

Tipos de Storage:

- **Volumes**: bloques de almacenamiento (SSD) de alta disponibilidad, que puedes añadir y quitar de tus droplets.
- **Spaces**: sistemas de almacenamiento masivo enfocados a CDNs (red entrega de contenidos) que pueden entregar imágenes videos, archivos de código, etc. Tienen un precio competitivo y son compatibles con Amazon S3.

La diferencia entre éstos, es que volumes está pensado en agregar espacio de almacenamiento mientras que spaces está enfocado en la entrega de contenidos.

# Marketplace de Digital Ocean

Es una tienda de aplicaciones o droplets preconfigurados para desplegar en minutos, incluso segundos.
