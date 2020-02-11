Hay 4 repositorios distintos en Ubuntu, los cuales son Main, Restricted, Universe, y Multiverse

*Main:* Son software open source que son mantenidos oficialmente por Canonical (la compañía detras de ubuntu), esto significa que ante cualquier problema de seguridad en los software de repositorios Main, Canonical va a arreglar esos problemas de seguridad, ya que el software es de código abierto. Un ejemplo es Firefox.

*Restricted:* Es software que es distribuido oficialmente por Canonical y no es de código abierto, pero que son esenciales para el uso del equipo. Un ejemplo son los drivers del hardware gráfico. Aunque si hay un problema de seguridad Canonical no puede arreglarlo por ellos mismos, se ocupan de distribuir la actualización cuando el propietario del driver saque el parche.

*Universe:* Es software open source que no esta mantenido oficialmente por Canonical, pero que tiene el soporte de la comunidad de ubuntu ante cualquier fallo. Aunque la comunidad es muy grande y posiblemente puedan sacar un parche rápido ante cualquier problema de seguridad, tiene cierto riesgo poner estos programas en un entorno de producción, ya que los arreglos de seguridad no estan garantizados y el mismo canonical avisa de esto.

*Multiverse:* Acá esta el software de código cerrado o paquetes que dependen de programas cerrados, no son necesarios como los restricted y además no se tiene ningún control en lo relatado a parches de seguridad por ser código cerrado, son los menos recomendables en lo que a seguridad se refiere.
