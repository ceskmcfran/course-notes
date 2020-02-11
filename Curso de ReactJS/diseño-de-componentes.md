Los componentes en React son **bloques de construcción**.
Las aplicaciones hechas con React son como figuras de Lego. Junta varias piezas (componentes) y puedes construir un website tan pequeño o tan grande como quieras.
Los componentes serán barras de búsquedas, enlaces, encabezados, el header, etc.

**”Componente” vs “elemento"**
Un elemento es a un objeto como un componente es a una clase. Si el elemento fuera una casa, el componente serían los planos para hacer esa casa.

**Identificación de componentes**
Para identificarlos debes hacerte las siguientes preguntas:

- ¿Qué elementos se repiten? Estos son los elementos en una lista o los que comparten aspecto visual y su funcionalidad
- ¿Qué elementos cumplen una función muy específica? Estos sirven para encapsular la lógica y permiten juntar muchos comportamientos y aspectos visuales en un solo lugar.

**Identificar componentes es una habilidad esencial para poder desarrollar aplicaciones de React.**

- Es una buena práctica que los componentes vivan en su propio archivo y para ello se les crea una carpeta.
- Todos los componentes requieren por lo menos el método render que define cuál será el resultado que aparecerá en pantalla.
- El source de las imágenes en React puede contener direcciones en la web o se le puede hacer una referencia directa importándola. Si se importa deben usarse llaves para que sea evaluado.

# Aplicar estilos
- Para los estilos crearemos una carpeta llamada **Styles** y allí vivirán todos los archivos de estilos que tienen que ver con los componentes.
- Para usar los estilos es necesario importarlos con import
- React funciona ligeramente diferente y para los atributos de clases no se utiliza class sino className
- Es posible utilizar **Bootstrap** con React, sólo debe ser instalado con `npm install bootstrap` y debe ser importado en el index.js
- Existen estilos que son usados de manera global o en varios componentes, así que deben ser importados en el index.js

# Props
Los **props** que es la forma corta de *properties* son argumentos de una función y en este caso serán los atributos de nuestro componente como class, src, etc.

Estos props salen de una variable de la clase que se llama *this.props* y los valores son asignados directamente en el **ReactDOM.render()**.

# Páginas
Las páginas en React son componentes conseguir distinguirlas nos servirá para saber que es un componente que adentro lleva otros componentes.

- Al escribir los props no importa el orden en el que lo hagas, únicamente importa el nombre.

# Enlazando eventos
- React dispone de **eventos**. Cada vez que se recibe información en un input se obtiene un evento **onChange** y se maneja con un método de la clase *this.handleChange*
- Los elementos button también tienen un evento que es **onClick**.
- Cuando hay un botón dentro de un formulario, este automáticamente será de tipo **submit**. Si no queremos que pase así hay dos maneras de evitarlo: especificando que su valor es de tipo *button* o manejándolo desde el formulario cuando ocurre el evento **onSubmit**.
~~~
handleChange = e => {
    console.log({
      name: e.target.name,
      value: e.target.value
    });
  };
~~~
Hay otra manera en la que los componentes pueden producir su propia información y guardarla para ser consumida o pasada a otros componentes a través de sus props. La clave está en que la información del **state** a otros componentes pasará en una sola dirección y podrá ser consumida pero no modificada.

- Para guardar la información en el estado se usa una función de la clase *component* llamada `setState` a la cual se le debe pasar un objeto con la información que se quiere guardar.
- Aunque no se ve, la información está siendo guardada en dos sitios. Cada *input* guarda su propio valor y al tiempo la está guardando en `setState`, lo cual no es ideal. Para solucionarlo hay que modificar los *inputs* de un estado de no controlados a controlados.
~~~
class TitleForm extends React.Component {
  state = {};

  handleChange = e => {
    this.setState({
      [e.target.name]: e.target.value
    });
  };

  handleClick = e => {
    console.log("Button was clicked");
  };

  handleSubmit = e => {
    e.preventDefault();
    console.log("Submited!");
  };

  render() {
    return (
      <div>
        <h1>New Attendant</h1>

        <form onSubmit={this.handleSubmit}>
          <div className="form-group">
            <label>First Name</label>
            <input
              onChange={this.handleChange}
              className="form-control"
              type="text"
              name="firstName"
              value={this.state.firstName}
            />
          </div>
          <div className="form-group">
            <label>Last Name</label>
            <input
              onChange={this.handleChange}
              className="form-control"
              type="text"
              name="lastName"
              value={this.state.lastName}
            />
          </div>
          <button onClick={this.handleClick} className="btn btn-primary">
            Save
          </button>
        </form>
      </div>
    );
  }
}

export default TitleForm
~~~
**Levantar el estado** es una técnica de React que pone el estado en una localización donde se le pueda pasar como *props* a los componentes. Lo ideal es poner el estado en el lugar más cercano a todos los componentes que quieren compartir esa información.

Algo interesante que le da el nombre a React es su parte de “reactivo” ya que cada vez que hay un cambio en el estado o en los props que recibe un componente se vuelve a renderizar todo el componente y todos sus descendientes.

# Introducción al ciclo de vida de un componente
Cuando React renderiza los componentes decimos que entran en escena, cuando su estado cambia o recibe unos props diferentes se actualizan y cuando cambiamos de página se dice que se desmontan.

**Montaje:**
- Representa el momento donde se inserta el código del componente en el DOM.
- Se llaman tres métodos: `constructor`, `render`, `componentDidMount`.

**Actualización:**
- Ocurre cuando los props o el estado del componente cambian.
- Se llaman dos métodos: `render`, `componentDidUpdate`.

**Desmontaje:**
- Nos da la oportunidad de hacer limpieza de nuestro componente.
- Se llama un método: `componentWillUnmount`.
