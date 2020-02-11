# UI Components y Container Components
En la programación es bueno separar las tareas en diferentes funciones y en React sucede lo mismo. Cuando un componente hace demasiado, probablemente es mejor dividirlo en dos.
Esta técnica de componentes presentacionales y componentes container es común, útil y hace parte de las buenas prácticas.

# Portales
Hay momentos en los que queremos renderizar un *modal*, un *tooltip*, etc. Esto puede volverse algo complicado ya sea por la presencia de un z-index o un overflow hidden.

En estos casos lo ideal será renderizar en un nodo completamente aparte y para esto React tiene una herramienta llamada **Portales** que funcionan parecido a ReactDOM.render; se les dice qué se desea renderizar y dónde, con la diferencia de que ese dónde puede ser fuera de la aplicación.

La técnica de usar componentes genéricos para crear uno nuevo especializado se llama **composición** y es una herramienta que todo buen programador debe saber utilizar.

# Hooks
Las funciones no tienen un estado propio que manejar como ciclos de vida a los que deben suscribirse, mientras tanto las clases sí cuentan con ello.

React tiene un feature llamado Hooks que permite que las funciones también tengan features que solamente tienen las clases.

Hooks: Permiten a los componentes funcionales tener características que solo las clases tienen:

- `useState`: Para manejo de estado.
- `useEffect`: Para suscribir el componente a su ciclo de vida.
- `useReducer`: Ejecutar un efecto basado en una acción.

**Custom Hooks**: Usamos los hooks fundamentales para crear nuevos *hooks custom*. Estos hooks irán en su propia función y su nombre comenzará con la palabra *use*. Otra de sus características es que **no** pueden ser ejecutados condicionalmente (`if`).

- `useState` regresa un arreglo de dos argumento

**LOS HOOKS SOLAMENTE FUNCIONAN DENTRO DE COMPONENTES FUNCIONALES**