# INTRODUCCIÓN
Las llamadas a una API siguen un patrón similar siempre que las hacemos, cada llamada consta de tres estados:

- **Loading**: cuando la petición se envía y estamos esperando.
- **Error**: se debe dejar un mensaje para el usuario para arreglar el error o volver a intentarlo.
- **Data**: los datos nos pueden llegar de dos formas, o en error o con los datos requeridos.

Una llamada a una API tiene tres estados

*Una promesa*
~~~
    Loading
    =>
        Error
        ||
        Data
            Without data {}
            ||
            With data {…}
~~~
Es vital indicar que se está cargando para que el usuario tenga paz. Si no hay data es vital hacer un CTA para introducir data

# Traer datos de una API
Una llamada a una **API** es un *proceso asíncrono*, es decir que lo comenzamos pero no sabemos cuándo acabará. Por lo mismo la función a escribir debe ser asíncrona.
La llamada se hará usando `fetch` que es una función de React que al pasarle una dirección de internet, hará una petición **GET** y lo que sea que exista ahí será devuelto.

