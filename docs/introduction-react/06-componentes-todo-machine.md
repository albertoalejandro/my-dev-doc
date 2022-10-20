# Componentes de TODO Machine

Ya que conocemos qué es JSX y cómo funciona, cómo pasar propiedades a los componentes, podemos comenzar con la creación de nuestra aplicación.

## Análisis de nuestra aplicación

Anteriormente, hemos detectado los componentes y sus comportamientos dentro de nuestro TODO app, necesitamos crear:

- **Counter:** para llevar un conteo de las tareas totales y las completadas.
- **Search:** para filtrar los TODOs de la lista.
- **List:** en donde tendremos cada uno de los TODOs.
- **Item:** será cada uno de los TODOs.
- **Add Todo:** botón para agregar un nuevo TODO.

Adicionalmente, tendremos que crear un modal para ingresar los datos del nuevo TODO (Lo veremos más adelante).

Para empezar a trabajar en el código, primero eliminaremos algunos archivos que no son necesarios para nuestra aplicación, solamente dejaremos dentro de nuestra carpeta *src/* los archivos *index.js, App.js* y los estilos.

## index.js

En la versión 18 de React añadieron cambios importantes, principalmente el método para crear una raíz para renderizar o desmontar:

### Versión menor a React V18

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import App from './components/App'

// ReactDOM.render(__qué__, __dónde__);
ReactDOM.render(<App />, document.getElementById('root'))
```

En la versión menor a la 18 de React, utilizamos el método render de ReactDOM, que recibe dos argumentos, el componente que queremos renderizar y el contenedor.

### Versión mayor o igual a React V18

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

En la versión 18 o superior de React, utilizamos el método *createRoot* de **ReactDom**, en el que le pasamos el contenedor, guardamos este contenedor en una variable y luego ejecutamos el método *render* con el componente que queremos renderizar.

## App.js

Dentro de nuestro componente App borraremos todo lo que estaba dentro del componente (No tengas miedo a romper el código), también quitaremos las importaciones de los estilos y de la imagen.

Ahora empezaremos a escribir nuestros componentes, tendremos algo como lo siguiente:

```jsx
function App() {
  return (
      <TodoCounter />    
      <TodoSearch />
      <TodoList>
        <TodoItem />
      </TodoList>
      <CreateTodoButton />
  );
}

export default App;
```

Una vez iniciamos el proyecto nos aparecerá un error como el siguiente: *SyntaxError: Adjacent JSX elements must be wrapped in an enclosing tag.*, esto es porque solamente se puede regresar un solo componente al trabajar con JSX, si queremos regresar varios necesitamos encerrarlos en un solo elemento padre.

Para esto existen 2 posibles opciones:

1. Envolver todos nuestros elementos y componentes en un ```<div></div>``` u otra etiqueta.
2. Utilizar el componente Fragment, que será invisible al momento de renderizar nuestros elementos en el DOM.

Para no tener problemas con los estilos y no tener que crear etiquetas extras por cada componente, se usa Fragment y para utilizarlo existen 2 formas.

### Maneras de utilizar Fragment en React

```jsx
import React from "react

function App() {
  return (
    <React.Fragment>
        ...
    </React.Fragment>
  );
}

// Desestructurándolo desde React
import { Fragment } from "react

function App() {
  return (
    <Fragment>
        ...
    </Fragment>
  );
}
```

O una forma muy común y la más utilizada, envolviendo nuestros elementos dentro de etiquetas vacías, que es lo equivalente a *React.Fragment*

```jsx
function App() {
  return (
    <>
        ...
    </>
  );
}
```

Puedes utilizar la manera que veas más cómoda.

Ahora si vemos nuestro proyecto nos aparecerá otro error, como ya te imaginas es porque no hemos creado nuestros componentes, eso es justo lo que haremos.

Para esto utilizaremos los módulos de JavaScript, existen varias maneras de exportar nuestros componentes, podemos exportarlos por defecto, pero no es una buena práctica porque puede causar futuros problemas al importar estos componentes.

Para evitar este problema debemos intentar evitar *export default*, y exportar nuestros componentes por su nombre, por ejemplo: *export { Componente };*, así lo tendremos que importar exactamente como lo exportamos: *import { Componente } from './Componente';*

### TodoCounter

```jsx
import React from "react";

function TodoCounter(){
    return(
        <h2> Has complentado 2 de 3 ToDos</h2>
    )
}

export {TodoCounter};
```

### TodoSearch

```jsx
import react from "react";

function TodoSearch(){
    return(
        <input placeholder="Cebolla" />
    );
}
export {TodoSearch};
```

### TodoList

```jsx
import react from "react";

function TodoList(props){
    return(
        <section>
            <ul>
                {props.children}
            </ul>
        </section>
    );
}

export { TodoList};
```

### TodoItem

```jsx
import react from "react";

function TodoItem(props){
    return(
        <li>
            <span>C</span>
            <p>{props.text}</p>
            <span>X</span>
        </li>
    );
}

export { TodoItem };
```

### CreateTodoButtom

```jsx
import react from "react";

function CreateTodoButtom(){
    return(
        <button>+</button>
    );
}

export { CreateTodoButtom};
```

## Importar componentes

Una vez creamos nuestros componentes no se nos olvide importarlos en *App.js* para ahora si usarlos.

```jsx
import react from "react";
import { TodoCounter } from "./TodoCounter";
import { TodoSearch } from "./TodoSearch.js";
import { TodoList } from "./TodoList.js";
import { TodoItem } from "./TodoItem.js";
import { CreateTodoButtom } from "./CreateTodoButton.js";

function App() {
  return (
   <react.Fragment>
      <TodoCounter />    
      <TodoSearch />
      <TodoList>
        <TodoItem />
      </TodoList>
      <CreateTodoButtom />      
   </react.Fragment>
  );
}

export default App;

```

## Lógica para renderizar nuestros TODOs

Ahora crearemos la lógica para renderizar todas las TODOs que creen nuestros usuarios, nuestro componente ya recibe una propiedad llamada texto, entonces creemos un arreglo con algunas tareas dentro de App.js y ahora mapearemos cada una de nuestras TODOs con *map* y por cada TODO regresaremos un componente *TodoItem*.

```jsx
import react from "react";
import { TodoCounter } from "./TodoCounter";
import { TodoSearch } from "./TodoSearch.js";
import { TodoList } from "./TodoList.js";
import { TodoItem } from "./TodoItem.js";
import { CreateTodoButtom } from "./CreateTodoButton.js";

const todos=[
  {text:'Cortar cebolla', completed:false},
  {text:'Tormar el curso de intro a react', completed:false},
  {text:'Llorar con la llorona', completed:false}
];
function App() {
  return (
   <react.Fragment>
      <TodoCounter />    
      <TodoSearch />
      <TodoList>
        {todos.map(todo => (
            <TodoItem text={todo.text} />
        ))}
      </TodoList>
      <CreateTodoButtom />      
   </react.Fragment>
  );
}

export default App;
```

¡Nuestra aplicación está tomando forma! Todavía nos faltan algunas cosas, pero… ¿Notaste que en la consola ahora nos aparece este error? 
*Warning: Each children in a list should have a unic "key" prop.*

Esto es porque cuando renderizamos varios elementos en una lista debemos que pasarle una propiedad especial a cada item, que es *key*, esta propiedad ayuda a React para mantener un registro de los elementos que han cambiado, y saber cuál elemento es cuál, también es importante que esta propiedad no se repita en ningún otro item.

Entonces añadamos esta propiedad:

```jsx
import react from "react";
import { TodoCounter } from "./TodoCounter";
import { TodoSearch } from "./TodoSearch.js";
import { TodoList } from "./TodoList.js";
import { TodoItem } from "./TodoItem.js";
import { CreateTodoButtom } from "./CreateTodoButton.js";

const todos = [
  {text:'Cortar cebolla', completed:false},
  {text:'Tormar el curso de intro a react', completed:false},
  {text:'Llorar con la llorona', completed:false}
];

function App() {
  return (
   <react.Fragment>
      <TodoCounter />    
      <TodoSearch />
      <TodoList>
        {todos.map(todo => (
            <TodoItem key={todo.text} text={todo.text} />
        ))}
      </TodoList>
      <CreateTodoButtom />      
   </react.Fragment>
  );
}

export default App;
```

## MIS NOTAS

```<React.Fragment>``` -> react requiere una etiqueta por componente. Por dentro luego podemos poner las que queramos
esta etiqueta no afecta a nuestra interfaz. Porque si lo envolvieramos con un div ensuciaría nuestro HTML y haría que no funcionara el CSS

```jsx
<div>
	<TodoCounter />
      <h2>Has completado 2 de 3 TODOs</h2>
      <TodoSearch />
      <input placeholder="Cebolla" />
      <TodoList>
        {todos.map(todo => (
          <TodoItem />
        ))}
      </TodoList>

      <CreateTodoButton />
      <button>+</button>
</div>
```

Haciendo esto:

{props.children}

es como si mandaráramos ha que pusiera:

```jsx
{todos.map(todo => (
  <TodoItem />
))}
```